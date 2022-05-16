# Sourcegraph 101 test exercises

Been through Sourcegraph 101 and ready to test your search skills? These exercises will allow you to make sure you understand how to use Sourcegraph for basic search. You can follow along on [sourcegraph.com](https://sourcegraph.com/search), or on your own Sourcegraph instance. 

## Exercises

**Runing a literal search**

How would I find all references to the string `GNU General Public License` in the Linux kernel (`github.com/torvalds/linux`)?

**Running a fuzzy match search**

How would I search for tests related to the `gitserver` in Sourcegraph's monorepo (`github.com/sourcegraph/sourcegraph`)?

**Running a structural search**

How would I find uses of this [Go print function](https://www.geeksforgeeks.org/fmt-sprintf-function-in-golang-with-examples/) where the first argument is a string in Sourcegraph's monorepo (`github.com/sourcegraph/sourcegraph`)?

**Filtering by language**

How would I find all JavaScript or JSON files in the Bluebird promise library (`github.com/petkaantonov/bluebird`)?

**Filtering by file path**

How would I find Dockerfiles that use a Python 3 base image?

**Viewing file history and git blame**

If I'm on a file, how do I view who wrote a particular line, and how do I view the file history?

## Answer key

1. `context:global repo:^github\.com/torvalds/linux$ GNU General Public License patternType:literal` - You want to limit to the appropriate repo, and search for the exact string. No quotes are required for exact match in Sourcegraph!
2. `context:global repo:github.com/sourcegraph/sourcegraph$ gitserver test patternType:regexp` - The fuzzy matching in the regex mode in Sourcegraph means that you'll find anywhere that `gitserver` and `test` are used near each other. You can then narrow down further by language, file path, etc.
3. `context:global repo:^github\.com/sourcegraph/sourcegraph$ fmt.Sprintf("...", ...) patternType:structural` - Using structural search allows you to specify structural holes in the function. The quotes in the first argument are interpreted literally, so you'll only see results where the first argument is a string.
4. `context:global repo:^github\.com/petkaantonov/bluebird$ (lang:JSON OR lang:JavaScript) patternType:structural` - Sourcegraph supports Boolean operators, so you can use `OR` to find results in either language. The `lang` filter allows you to narrow down to files only in the language(s) you specify.
5. `context:global file:dockerfile$ FROM python:3 patternType:regexp` - The `file:` filter allows you to limit results to just file paths ending in `Dockerfile`. The `FROM python:3` search allows you to find references to any Python 3 base image. 
6. To view the `git blame` info, click the red git branch icon on the right-hand side of the page. Clicking once will enable blame info for a single line. Clicking again will enable it for the entire file. Clicking it a third time will disable it. To view file history, click the "show history" rewind icon, on the top right of the page underneath the search bar. 
