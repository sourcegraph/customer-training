# Sourcegraph 102

**Topic:** This training is focused on learning more advanced search functionality with Sourcegraph. For basic search training, check out [Sourcegraph 101](../sourcegraph-101/lesson-plan.md), instead.

## Intro

Today's training builds on the search skills taught in Sourcegraph 101, focusing on more advanced search functionality and more complicated queries. By the end of this training, you should feel comfortable searching non-default branches and revisions, searching commit messages, using advanced search filters, and configuring Sourcegraph extensions. You can follow along in your own instance, or on [sourcegraph.com](https://www.sourcegraph.com/search), where you can set up a free account.

## Unit 1: Searching branches and revisions

**Learning goals:** After completing this unit, customers will understand how to search for code on non-default branches using a particular branch name, tag, or revision hash.

### Searching in a specific branch, tag, or revision

As covered in Sourcegraph 101, when searching code in Sourcegraph, the default behavior for the `repo:` filter is to return results from the main, master, or other default branch for a repo. 

🔎 The trainer should demonstrate:

* A `repo:` search and its results

However, it's often useful to search for content on other branches, tags, or revisions. Common use cases for this include searching on a feature development or staging branch, rather than in production code. 

❗️ It can be useful here to ask what sorts of non-default branch searches are most useful for the team, if that's not already known to the presenter. That can shape the examples given for the rest of the unit.

In Sourcegraph, you have a few ways to search in these non-default branches.

🔎 The trainer should demonstrate:

* Applying the `repo:` filter and then using the dynamic filters to pick a new branch
* Applying the `repo:` filter and then using the dynamic filters to pick a new tag
* Applying the `repo:` filter and then using the `rev:` and `@` filter syntax to filter manually
* Running a `type:commit` search, opening the results, and then using the `navigate at commit xyz` link to search at a particular commit hash

❗️ Make sure to highlight that the `repo:` filter needs to be applied and pointed at a single repo (not partial-matching multiple) for the additional revision searches to work.

### Searching in multiple branches or tags

Sometimes, you need to search in multiple branches or tags, such as when you're not sure what branch content is included in. With Sourcegraph's support for glob syntax (using `*` as a wildcard character), this is possible.

🔎 The trainer should demonstrate:

* Appending `@*refs/heads/*` to a query to search all branches
* Appending `@*refs/tags/*` to a query to search all tags
* Appending a `:` to the `rev:` or `@` filter to search multiple revisions, such as `repo:^github\.com/sourcegraph/sourcegraph$@3.18:3.17`
* A refresher on how to save those filters as search snippets rather than remembering the syntax each time

### Excluding results from specific branches when searching in multiple branches

Sometimes, you will want results from multiple branches _except for_ one or a few in particular. You can exclude those from your results using the `*!` symbol in front of the glob pattern. You can think of the `*!` as a `NOT`, so something like `rev:*refs/tags/*3.19*:*!refs/tags/*3.19.0*` will find all patch releases of the `3.19` release but not the original release.

🔎 The trainer should demonstrate:

* Adding a glob pattern `rev:` search to a query (such as `rev:*refs/tags/*3.*`) in order to return results from multiple revisions.
* Adding a `:*!` followed by a branch or tag pattern in order to remove results from that branch or tag.

❗️ You may want to highlight that these searches can be slower due to their unindexed nature.

### Conclusion

Sourcegraph's non-default revision search allows customers to search at any branch, tag, or commit hash in the codebase. Using the glob syntax, customers can run searches across a wide variety of revisions even without explicitly identifying them; they can also exclude results if needed. Combined with the commit search, covered next, this can be very powerful.

### Resources

- [Sourcegraph](https://sourcegraph.com)
- [Sourcegraph Search Documentation](https://docs.sourcegraph.com/code_search/reference/queries#search-pattern-syntax)
- [Sourcegraph Search Cheat Sheet](https://learn.sourcegraph.com/how-to-search-code-with-sourcegraph-a-cheat-sheet)
- [Sourcegraph Documentation](https://docs.sourcegraph.com)

## Unit 2: Searching commits

**Learning goals:** After completing unit, customers will understand how to search through `type:diff` and `type:commit` queries, and how to apply the `author:` and `before:`/`after:` filters to those queries. They'll also understand how to search for added/removed content, specifically.

### Searching through commit messages (`type:commit`)

Sometimes, as a developer looking for code, I may not know where in the code the feature I'm working on is defined. One way to find that content is to look for commit message contents which reference the feature in question, and then look at the code which was changed to discover where in the codebase I should be looking. This is possible with Sourcegraph commit search, and I don't need to pull the repos down locally to view that commit history.

🔎 The trainer should demonstrate:

* How to use the `type:commit` filter to search for contents in the commit message
* How to apply that filter from the sidebar or by typing it manually
* How to open the contents of a commit to see the changed code
* How to navigate to the code host from the commit view to view discussion on a PR/MR view (if using an applicable code host)
* How to toggle between split/unified view on the search result
* How to use the "view" link in the search result view to open a particular file at that revision

❗️ Make sure to highlight that commit search is limited to 50 repos at a time, and it's best practice to narrow things down with a `repo:` filter first.

### Searching through diff content (`type:diff`)

We just saw that it's possible to search the contents of your colleagues' commit messages using the `type:commit` filter. With the `type:diff` filter, you can search the actual changes to the code itself. This can be super powerful if, for example, you're looking at code that has changed locations a few time, which makes the file history not very useful. It's also great to discover exactly when a piece of code was added or removed without needing to navigate through the full file history by hand.

🔎 The trainer should demonstrate:

* How to use the `type:diff` filter to search for contents in the committed code
* How to apply that filter from the sidebar or by typing it manually
* Highlight that the results will bring the customer into the same commit view as the `type:commit` search, so they'll have to click twice to view the changed file itself.
* The searches are unindexed, so more complicated searches may take longer to return results.

❗️ Make sure to highlight that diff search is also limited to 50 repos at a time, and it's best practice to narrow things down with a `repo:` filter first.


### Searching for specific authors (`author:`)

When looking at committed code, I sometimes want to narrow down the results so that I only see code from one particular colleague. This can be great to get up to speed on what someone was working on before they went on long-term leave or vacation, or to remind myself what I've been working on before chatting with my manager. I can do this with the `author:` filter, which is specific to `type:commit` and `type:diff` searches.

🔎 The trainer should demonstrate:

* How to use the `author:` filter to narrow down the previous `type:diff` search to only code changed by a particular contributor.
* The `author:` filter takes display names (e.g. `author:emily`, `author:"emily chapman"`) and email addresses (e.g. `author:sourcegraph.com`)

❗️ The `author:` filter does take email addresses (e.g. `author:sourcegraph.com` will return all Sourcegraph developers committing under their work email address), but since some users commit code under an auto-generated email address for security (visible by searching `author:github.com`) or their personal addresses (`author:gmail.com`), it's not necessarily useful.

### Searching in a specific date range (`before:` and `after:`)

As we've seen so far, the `type:diff` and `type:commit` searches will return results in reverse chronological order. Sometimes, however, you'll want to timebox results. This can be helpful if you're trying to see what changed while you were out on vacation, or if you know that a bug was introduced between two points in time and want to look at what changed only in that interval. 

🔎 The trainer should demonstrate:

* Using the `before:` and `after:` filters with natural language dates (e.g. `before:"1 day ago"` and `after:"1 year ago"`
* Using the `before:` and `after:` filters with typed dates (e.g. `before:"july 1 2020"`). 

### Searching for added/removed text (`select:commit.diff.added` and `select:commit.diff.removed`)

Finally, sometimes I want to look at changes to code that are specifically related to adding or removing content. Say that I know something _used_ to be in our docs, and I want to find out when we took it out. We can do that using the `select:` filter, which we'll talk about a little bit more in our next unit.

🔎 The trainer should demonstrate:

* How to use the `select:commit.diff.added` filter to find added content
* How to use the `select:commit.diff.removed` filter to find removed content
* How to use the auto-complete menus and the `tab` key to navigate to those filters if the customer forgets the syntax 

### Conclusion

Sometimes, it's more useful to look at changes to the code rather than the code in its present state. With the `commit` and `diff` searches and their `author`, `before`, `after`, and `select:commit.diff` filters, it's possible to find useful changes to the code over time and discover the origin of content I'm interested in. Next, we'll discuss more advanced search filters outside of the `type:diff` and `type:commit` search types.

### Resources

- [Sourcegraph](https://sourcegraph.com)
- [Sourcegraph Search Documentation](https://docs.sourcegraph.com/code_search/reference/queries#search-pattern-syntax)
- [Sourcegraph Search Cheat Sheet](https://learn.sourcegraph.com/how-to-search-code-with-sourcegraph-a-cheat-sheet)
- [Sourcegraph Documentation](https://docs.sourcegraph.com)

## Unit 3: Advanced search topics

**Learning goals:** After completing this unit, customers will understand how to use several useful, advanced search filters not covered in Sourcegraph 101.

### Boolean operators (`AND`, `NOT`, `OR`)

Sourcegraph supports combining search phrases into more complete queries using the boolean `AND`, `NOT`, and `OR` operators. They work like they do in other search tools; if you want to group subqueries together, you can use parentheses to do so. 

🔎 The trainer should demonstrate:

- Combining two `repo:` filters using an `OR` query
- Combining two different strings using an `AND` query
- Excluding a substring from a query using `NOT`
- Using the `content:` filter to search for boolean operators literally (e.g. `content:"not cloneable"`)

### Searching for symbols (`type:symbol`)

So far we've seen three types of search in Sourcegraph: our default code search, our `diff` search, and our `commit` search. Sourcegraph offers a fourth search mode, `type:symbol`. This allows you to specifically search for the names of symbols (such as functions, variables, classes, etc.) in your code, and results will be an easy-to-parse list of the symbols sorted by file.

🔎 The trainer should demonstrate:

- Applying the `type:symbol` filter by typing it as well as by using the sidebar link
- How to tell what kind of symbol each result is by hovering over the identifier on the left side of the symbol

### Using the `select:` keyword

Our `select:` filter is a very powerful way of grouping results. You saw us use this earlier with `select:diff.commit.added`; this allowed us to only view committed code that added the search term. You can use it to group results on other queries, too. This can be super useful when trying to figure out not just _where_ a particular match is occurring in your code, but which repos, overall, contain the match. This way, you can see a list of which repos rely on an out-of-date dependency, rather than just seeing the raw results. 

🔎 The trainer should demonstrate:

- Applying `select:file` to a search to get a list of files containing matches for a query
- Applying `select:file.directory` to a search to get a list of directories containing matches for a query
- Aplying `select:repo` to a search to get a list of impacted repos for a query
- Applying `select:symbol.function` to a `type:symbol` filter to show only function matches for the search

### Repo contains file (`repo:contains.file(...)`)

Sometimes I only want to search within a repo that has a particular file—say I want to find usages of a particular dependency but only in repos that have a license file, but I don't care about the contents of the file, just its presence. Using the `repo:contains.file(...)` filter allows me to do this.

🔎 The trainer should demonstrate:

- Using the `repo:contains.file(...)` filter to run an appropriate query (e.g. `repo:contains.file(LICENSE) file:package-lock.json bluebird`)
- Using the `repohasfile(...)` filter to accomplish the same thing. 
- Using the `-repohasfile:` filter to exclude results from repos containing a file

❗️ `repo:contains.file` and `repohasfile(...)` operate very similarly ([nuances here](https://docs.sourcegraph.com/code_search/reference/queries#keywords-all-searches)), so you may simply wish to explain `repo:contains.file` and not mention `repohasfile(...)`, which is slightly less flexible as a query but may be easier to remember.

### Excluding stale repos (`repo:contains.commit.after(...)`)

Oftentimes I will want to search only in active repos. The easiest way to do this is to filter by commit date using `repo:contains.commit.after(...)`. 

🔎 The trainer should demonstrate:

- Using the `repo:contains.commit.after(...)` filter to run a search on recently-updated repos (e.g. `repo:contains.commit.after(1 month ago) new auth provder`)

❗️ The filter doesn't support negation. Someone could use `repo.contains.commit.after(...) select:repo` to get a list of repos and then exclude them in a follow-up query if needed.

### Dependency search (`repo:deps(...)`)

Sometimes, I don't want to search my own code, but the code of the dependencies that are present in my code. This can be helpful for looking at whether we're impacted by a 0-day, or understanding our code graph in general. To set this up, I'll first have to go to the code host page, which only admins will have access to.

🔎 The trainer should demonstrate:

- Adding a dependency code host in the code host section
- Running a `repo:deps(...)` search on a repo to show the dependencies for that repo, including versions
- Searching the contents of the dependencies for particular contents

❗️ This feature is in beta and does not support all dependency management tools.

### Conclusion

Sourcegraph offers a variety of advanced search filters. We covered boolean operators, symbol search, the `select:` keyword, the `repo:contains.file(...)` filter, how to exclude stale repos, and how to saerch your code's dependencies, if configured. Next up, we'll talk about our extensions platform.

### Resources

- [Sourcegraph](https://sourcegraph.com)
- [Sourcegraph Search Documentation](https://docs.sourcegraph.com/code_search/reference/queries#search-pattern-syntax)
- [Sourcegraph Search Cheat Sheet](https://learn.sourcegraph.com/how-to-search-code-with-sourcegraph-a-cheat-sheet)
- [Sourcegraph Documentation](https://docs.sourcegraph.com)
- [Dependencies Search](https://docs.sourcegraph.com/code_search/how-to/dependencies_search)

## Unit 4: Sourcegraph extensions

**Learning goals:** After completing this unit, customers will understand what Sourcegraph extensions are available and how to access them and the CLI.

### What are Sourcegraph extensions?

Sourcegraph has a fully-featured extensions platform. Because our extensions API is available to users, you can develop against it as well, and build your own extensions. This can be particularly useful if you have a custom-built tool that you use internally which you would like to connect to Sourcegraph. Our most popular extensions include our search export extension and our code editor integrations.

### How to find and enable extensions

Extensions are found and enabled on the Extensions page, represented by a puzzle icon on the top of the page.

🔎 The trainer should demonstrate:

- How to access the extensions page
- How to enable an extension for yourself (for non-admins) or for everyone (for admins)
- The search export extension 
- The code editor extensions (and how to view what needs to be customized for those extensions in the extension settings)
- Any other extensions known to be of interest to the user

### Introduction to IDE plugins

I mentioned our IDE extensions earlier. The ones we just discussed will allow you to open a file from Sourcegraph into your editor, if it's available locally. But you can also navigate from your editor to Sourcegraph, using our editor extensions. And if you use a supported editor, you can use Sourcegraph directly in your editor.

🔎 The trainer should demonstrate:

- How to access our supported editor extensions ([link](https://docs.sourcegraph.com/integration/editor))
- What the extension looks like in VSCode and any other editors with an in-depth integration (IntelliJ currently being targeted); emphasize that the code is not stored locally

### The Sourcegraph CLI

Sometimes we hear folks ask if they can use Sourcegraph from the command line. You can, using our CLI!

🔎 The trainer should demonstrate:

- How to download the CLI ([GitHub link](https://github.com/sourcegraph/src-cli))
- How to run a search in the CLI
- How to generate the raw `curl` request for a search from the CLI to use in a customer's own programs
- How to use the streaming API for larger result sets

### Conclusions

Sourcegraph extensions can be very powerful additions to give Sourcegraph "single pane of glass" access to your code. You can build your own extensions, and our CLI allows you to build your own queries without using the browser app. Folks using some IDEs can even use Sourcegraph entirely in the IDE.

### Resources

- [Sourcegraph](https://sourcegraph.com)
- [Sourcegraph Search Documentation](https://docs.sourcegraph.com/code_search/reference/queries#search-pattern-syntax)
- [Sourcegraph Search Cheat Sheet](https://learn.sourcegraph.com/how-to-search-code-with-sourcegraph-a-cheat-sheet)
- [Sourcegraph Documentation](https://docs.sourcegraph.com)
- [Sourcegraph Extensions Documentation](https://docs.sourcegraph.com/extensions)
- [Sourcegraph CLI](https://docs.sourcegraph.com/cli)
- [Sourcegraph Editor Integrations](https://docs.sourcegraph.com/integration/editor)

## Closing thoughts

During this training, we've covered advanced Sourcegraph functionality, such as searching non-default revisions, searching `diff` and `commit` content, and the `select:` filter. We also covered our extensions platform. With this knowledge, you're now empowered to run nuanced, expansive queries in Sourcegraph across all of your company's code.
