# API usage sketches

Owner: Varun Gandhi
Verification: Verified
Last edited time: January 13, 2025 8:56 PM
Status: Not started

# Renaming symbols

**Pre-requisite**: The code for which the renaming operation needs to be performed needs to have been indexed using a precise SCIP indexer.

### Implementation sketch

The user wants to rename a globally-accessible symbol from `ABC` to `XYZ`. The symbol may be a function, a method, a field, an enum case, a type or something else.

There are two overall flows that renaming can take: the copy-migrate flow, and the direct-rename flow. I’ll describe these in more detail below.

**Copy-migrate flow**: (applicable for methods, types, free-standing functions)

1. Create the new symbol XYZ that is a copy of the symbol ABC in the appropriate module/package/namespace.
2. Identify the original symbol ABC to be renamed along with the source range for its definition.
3. Identify all definition and reference usages† of the symbol.
    1. Identify if 1 or more reference usages would, if renamed, lead to (1) compilation failures and/or (2) changes in run time behavior. → Drop those usages before moving on to the next step.
4. Perform rename operations on the usages identified in the previous step.
5. Perform cleanup operations on modified files (e.g. reformatting).

**Direct-rename flow:** (applicable for all symbols)

1. Identify the original symbol ABC to be renamed along with the source range for its definition.
2. Identify all definition and reference usages† of the symbol.
    1. Identify if 1 or more usages would, if renamed, lead to (1) compilation failures and/or (2) changes in run time behavior. → If so, abort, or perform some repair operations.
3. Perform rename operations on the usages identified in the previous step.
4. Perform cleanup operations on modified files (e.g. reformatting).

The direct-rename flow is more general, but introduces more risk of failure, whereas the copy-migrate flow allows for more gradual migrations in the form of many small commits instead of one big-bang commit.

In both of the above flows, the Sourcegraph API can help with the steps of identifying the original symbol, and finding usages across the Sourcegraph instance.

### Sourcegraph API usage

In Sourcegraph, a symbol is identified using its string representation that can be obtained using the `codeGraphData.occurrences.nodes.symbol` field in the GraphQL API. https://sourcegraph.com/github.com/sourcegraph/artifacts@ba7cab20b7c78e586b898cd5056ce0f875bc3eb4/-/blob/gql/codeintel.codenav.graphql?L154

Example API usage:

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

The returned data will have output like the following:

```json
    {
      "range": {
        "start": { "line": 29, "character": 5 },
        "end": { "line": 29, "character": 9 }
      },
      "symbol": "scip-go gomod github.com/sourcegraph/conc 5f936abd7ae8 `github.com/sourcegraph/conc/pool`/Pool#",
      "roles": [ "DEFINITION" ]
    },
```

The output from this API can be fed to the usagesForSymbol API. (https://sourcegraph.com/github.com/sourcegraph/artifacts@ba7cab20b7c78e586b898cd5056ce0f875bc3eb4/-/blob/gql/codeintel.codenav.graphql?L462). For example:

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

This will return output like the following:

```json
  {
    "usageKind": "REFERENCE",
    "usageRange": {
      "repository": "github.com/sourcegraph/conc",
      "path": "pool/pool.go",
      "range": {
        "start": {
          "line": 10,
          "character": 12
        },
        "end": {
          "line": 10,
          "character": 16
        }
      }
    },
    "surroundingContent": "func New() *Pool {"
  },
```

Known limitations:

- As of Jan 2025, the codeGraphData and usagesForSymbol APIs are marked experimental, but we anticipate that they will be stabilized by Feb-Mar 2025 without major changes.
- The codeGraphData API works on one file at a time, it doesn’t work instance wide.
- The usagesForSymbol API requires an input source range.
- In the presence of inheritance and/or interfaces, reference usages returned by usagesForSymbol can show results merged across the inheritance/interface hierarchy. There is currently no way of limiting usages to a certain part of the inheritance/interface hierarchy.
- usagesForSymbol with `provenance` set to `PRECISE` may return incomplete results:
    - When complex features like reflection and macros are involved.
    - If a symbol is referred to using standardized doc comment syntax.
    - If the symbol is tied to external systems. For example, it may be used across language boundaries (via FFI), across process/network boundaries using RPCs, or in generated code not present in Sourcegraph.

# Moving symbols

This largely resembles the work needed for [Renaming symbols](https://www.notion.so/Renaming-symbols-17ba8e1126588045a45eddf6210fbefd?pvs=21), but the main added caveat is that imports/includes may require adjustments, and build files may need updates for updating dependencies across targets.

Different ecosystems have different tools for automatically adjusting imports using the CLI. For example,

- In C++, the [include-what-you-use](https://github.com/include-what-you-use/include-what-you-use) tool can be used.
- In Go, the [goimports](https://pkg.go.dev/golang.org/x/tools/cmd/goimports) tool can be used.

Known footguns:

- In C++, the language feature [Argument-dependent lookup](https://en.cppreference.com/w/cpp/language/adl) (ADL) is well-known to trigger counter-intuitive changes in name resolution when moving functions across namespaces.

# Miscellaneous resources

[Large-Scale Changes at Google: Lessons Learned From 5 Yrs of Mass Migrations](https://www.youtube.com/watch?v=TrC6ROeV4GI) (~1hr talk, slightly C++ specific, but broadly useful)
