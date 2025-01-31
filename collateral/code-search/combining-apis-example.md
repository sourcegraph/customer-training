### Using Cody API & SCIP Data to Perform Mass Refactoring

Below is an example “end-to-end” outline (with pseudocode and brief documentation) showing how you might rename or move symbols in a large monorepo using the Sourcegraph [SCIP](https://sourcegraph.com/github.com/sourcegraph/scip/-/blob/README.md) APIs and the Cody LLM API. It includes:
1. **Symbol discovery** (query file symbols)
2. **Symbol usage** **lookup** (get all references/occurrences in the codebase)
3. **Local checkout and file retrieval**
4. **Sending file content (and instructions) to the Cody API**
5. **Receiving a diff, reviewing it, and committing/pushing changes**

This is an illustrative flow; adapt it to your own scripting language, environment, and version control tooling.

### 1. Retrieve Symbols from a File

Use the [SCIP Symbol Endpoint](https://github.com/sourcegraph/customer-training/blob/main/collateral/code-search/SCIP-API-usage.md#example-symbol-endpoint) (or the relevant GraphQL query) to list all symbols in a specific file. For example, a simplified GraphQL query might look like this:

```graphql
query {
  repository(name: "github.com/sourcegraph/conc") {
    commit(rev: "main") {
      blob(path: "pool/pool.go") {
        codeGraphData {
          occurrences(
	          first: 1000,
	          # after: <for pagination>
          ) {
            nodes {
              range {
                start {line character}
                end {line character}
              }
              symbol
              roles
            }
            pageInfo {
              hasNextPage
              endCursor # supply  as 'after:' for occurrences if hasNextPage
            }
          }
        }
      }
    }
  }
}
```

Inputs:
* **repository**: Name or identifier of the repo.
* **commit**: The commit SHA (or branch name) to query.
* **filePath**: The path of the file in the repo.
  
Outputs:
* A list of symbols, including each symbol’s name and its range (start line/character, end line/character) in the file.

```python:pseudo_retrieve_symbols.py
function getSymbolsInFile(repo, commit, filePath, authToken):
    query = """
    query SymbolsInFile($repository: String!, $commit: String!, $filePath: String!) {
      repository(name: $repository) {
        commit(rev: $commit) {
          blob(path: $filePath) {
            lsif {
              symbols {
                name
                range {
                  start {
                    line
                    character
                  }
                  end {
                    line
                    character
                  }
                }
                kind
              }
            }
          }
        }
      }
    }
    """
    variables = {
       "repository": repo,
       "commit": commit,
       "filePath": filePath
    }
    
    response = callGraphQL(query, variables, authToken)
    # Where callGraphQL() is any function that sends an HTTP POST to
      yourInstance.sourcegraph.com/.api/graphql with the correct headers, token, etc.
    return response.data.repository.commit.blob.lsif.symbols
```

The returned data will look like this:

```
    {
      "range": {
        "start": { "line": 29, "character": 5 },
        "end": { "line": 29, "character": 9 }
      },
      "symbol": "scip-go gomod github.com/sourcegraph/conc 5f936abd7ae8 `github.com/sourcegraph/conc/pool`/Pool#",
      "roles": [ "DEFINITION" ]
    },
```

### 2. Retrieve References to a Symbol

Once you have the symbol’s name and exact range, you can query the [SCIP “usages” or “references” endpoint](https://github.com/sourcegraph/customer-training/blob/main/collateral/code-search/SCIP-API-usage.md#example-usages-endpoint) (sometimes referred to as “usages for symbol”). You’ll supply the symbol’s identifier and range to find all references in the entire codebase.

```graphql
query {
  usagesForSymbol(
    symbol: {
      name: {equals: "scip-go gomod github.com/sourcegraph/conc 5f936abd7ae8 `github.com/sourcegraph/conc/pool`/Pool#"},
      provenance: {equals: PRECISE}
    },
    range: {
	    repository: "github.com/sourcegraph/conc",
	    path: "pool/pool.go",
	    start: {line: 29, character: 5},
	    end: {line: 29, character: 9}
	  },
    first: 10
    # after: <for pagination>
  ) {
    nodes {
      usageKind
      usageRange {
        repository
        path
        range {
          start { line character }
          end { line character }
        }
      }
      surroundingContent
    }
    pageInfo {
      hasNextPage
      endCursor # supply to 'after:' for usagesForSymbol if hasNextPage
    }
  }
}
```

##### Pseudocode
```python
function getSymbolUsages(repo, commit, symbolName, symbolRange, authToken):
    query = """
    query SymbolUsages(
        $repository: String!,
        $commit: String!,
        $symbol: String!,
        $rangeStartLine: Int!,
        $rangeStartChar: Int!,
        $rangeEndLine: Int!,
        $rangeEndChar: Int!
    ) {
      repository(name: $repository) {
        commit(rev: $commit) {
          blob(path: "dummy") {
            lsif {
              references(symbol: $symbol, filter: "", startLine: $rangeStartLine, startCharacter: $rangeStartChar, endLine: $rangeEndLine, endCharacter: $rangeEndChar) {
                nodes {
                  resource {
                    path
                  }
                  range {
                    start {
                      line
                      character
                    }
                    end {
                      line
                      character
                    }
                  }
                  # ...
                }
              }
            }
          }
        }
      }
    }
    """

    variables = {
      "repository": repo,
      "commit": commit,
      "symbol": symbolName,
      "rangeStartLine": symbolRange.startLine,
      "rangeStartChar": symbolRange.startChar,
      "rangeEndLine": symbolRange.endLine,
      "rangeEndChar": symbolRange.endChar
    }

response = callGraphQL(query, variables, authToken)
# Where callGraphQL() is any function that sends an HTTP POST to
yourInstance.sourcegraph.com/.api/graphql with the correct headers, token, etc.
return response.data.repository.commit.blob.lsif.references.nodes
```

* **Inputs**: The symbol’s name or ID and the range details.
* **Outputs**: A list of references with path, range, plus other context you might need (repo name, etc.).

### 3. Check Out Code Locally

At this point, you know all the files/locations in which the symbol is referenced. The next step is to check out the repo locally (or in a sandbox environment) so you can edit files. This step is environment-specific:
```bash
git clone https://github.com/<org>/<repo>.git
cd <repo>
git checkout <commit-or-branch>
```
(You may also create a new branch to hold your changes.)

### 4. For Each Usage, Send File Content (plus instructions) to Cody

You now have a list of references (each has path, start/end line/char, etc.). For each file path in that list:
1. Read the file content from disk (or from your local sandbox).
2. Prepare a prompt to send to Cody. The prompt can include:
     * The entire file (or relevant sections).
     * A set of instructions, such as “Rename the function oldName to newName in this file. Return a diff only.”
3. Call the Cody API to get back a suggested diff of changes.

Below is an example using the Cody chat completions endpoint:
```bash
curl --location 'https://sourcegraph.sourcegraph.com/.api/llm/chat/completions' \
--header 'Accept: application/json' \
--header 'Authorization: token <YOUR_TOKEN_HERE>' \
--header 'X-Requested-With: name_of_application_here version' \
--header 'Content-Type: application/json' \
--data '{
    "messages": [
      {
        "role": "user",
        "content": "Please rename function oldName to newName. Return only a diff. File:\n\n<contents_of_file_here>"
      }
    ],
    "model": "anthropic::2024-10-22::claude-3-5-sonnet-latest",
    "max_tokens": 1000
}'
```
**Pseudocode** snippet showing iteration over references:
```python
function renameSymbolWithCody(repoPath, usageReferences, oldSymbolName, newSymbolName, codyToken):
    for ref in usageReferences:
        filePath = ref.resource.path
        fullPath = join(repoPath, filePath)
        
        fileContent = readFile(fullPath)
        
        userPrompt = buildPromptForRenaming(
            oldSymbolName, 
            newSymbolName, 
            fileContent
        )
        
        # Call Cody API
        diffResponse = callCodyAPI(userPrompt, codyToken)
        
        # The response is expected to be a diff
        if diffResponse is validDiff:
            # Save diff for later use, or apply it automatically
            saveOrApplyDiff(diffResponse, fullPath)
```
Where:
* buildPromptForRenaming() might produce a string:

```
"Please rename function " + oldSymbolName + " to " + newSymbolName +
". Return only a diff. File:\n\n" + fileContent
```
* callCodyAPI() is a wrapper around the curl request to the /.api/llm/chat/completions endpoint.
* saveOrApplyDiff(diff, filePath) can patch the file using standard diff/patch tools, or store it for manual inspection.

**A Note on Including Context in the Prompt**

To get the best diffs from Cody, you generally need:
* The relevant portion of the file (or the entire file if it’s not too large).
* Clear instructions (for example, “Rename all references to oldSymbolName to newSymbolName, but do not change references to oldSymbolNameFoo or OldSymbolName in comments.”)

### 5. Review and Commit Changes

After you have gathered diffs (either for each file individually or for all usage references in bulk), you can review them either via:
* Your local Git client in the CLI (git diff, git add, git commit).
* Your IDE’s built-in diff viewer.
* A review in GitHub, GitLab, or other hosting via a pull/merge request.

```bash
# Apply diffs if stored locally:
# (This step is environment- and workflow-specific—patch, direct file writes, etc.)
patch <the-changes.diff>

# Review changes
git diff

# Stage and commit
git add .
git commit -m "Rename oldSymbolName to newSymbolName"

# Push to remote
git push origin <branch>
```

### Full Pseudocode Summary

Below is a higher-level pseudocode that ties everything together. (Use your own language—this is just to illustrate the flow.)

```python
function renameSymbol(repo, commit, filePath, oldSymbolName, newSymbolName, authToken, codyToken):
    # 1. Get all symbols in the specified file
    symbols = getSymbolsInFile(repo, commit, filePath, authToken)
    
    # 2. Pick the symbol to rename (filter by 'name' or check multiple if needed)
    symbolToRename = findSymbol(symbols, oldSymbolName)
    if symbolToRename is None:
        print("Symbol not found, exiting.")
        return

    # 3. Get references for that symbol
    usageReferences = getSymbolUsages(
        repo,
        commit,
        symbolToRename.name,
        symbolToRename.range,
        authToken
    )

    # 4. Clone or confirm local checkout of the repo if not already done
    cloneRepoIfNeeded(repo, commit)

    # 5. For each usage reference, retrieve the file from the local checkout and call Cody
    for usage in usageReferences:
        localFile = joinLocalPath(repo, usage.resource.path)
        fileContent = readFile(localFile)
        
        # Build a prompt with instructions and the file content
        prompt = "Please rename function " + oldSymbolName + " to " + newSymbolName + 
                 ". Return only a diff. File:\n\n" + fileContent
        
        # Call Cody to get the diff
        diff = callCodyAPI(prompt, codyToken)
        
        # Optionally apply the diff or save it for manual review
        applyDiffToFile(diff, localFile)
    
    # 6. Manually or programmatically review changes, then commit and push
    system("git add .")
    system("git commit -m 'Rename " + oldSymbolName + " to " + newSymbolName + "'")
    system("git push origin my-feature-branch")
```

### Additional Notes & Best Practices

1. **Batching**: Instead of calling Cody for each reference individually, you might call it once per file to perform a consistent rename or transformation across the entire file.
2. **Model Selection**: You can list available models from Cody via:
 
    ```bash
    curl --location 'https://yourInstance.sourcegraph.com/.api/llm/models' \
         --header 'Accept: application/json' \
         --header 'Authorization: token <YOUR_TOKEN_HERE>' \
         --header 'X-Requested-With: name_of_application_here version'
    ```
    
     Then pick the best model for your transformation calls.

3. **Prompt Engineering**: Provide clear instructions. For complex refactors, you may add more context or constraints, e.g., “Only rename local variables, do not rename references in comments.”
4. **Diff Format**: Cody typically returns a unified diff. Confirm your environment can parse or apply it.
5. **Review**: Always review automated changes. Some code transformations can be semantic or context-dependent; ensure you’re comfortable with the final changes before committing to your main branch.





