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
* Running a `type:commit` search, opening the reults, and then using the `navigate at commit xyz` link to search at a particular commit hash

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

Sourcegraph's non-default revision search allows customers to search at any branch, tag, or commit hash in the codebase. Using the glob syntax, customers can run searches across a wide variety of revisions even without explicitly identifying them; they can also exclude results if needed. Combined wiht the commit search, covered next, this can be very powerful.

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

We just saw that it's possible to search the contents of your colleagues' commit messages using the `type:commit` filter. With the `type:diff` filter, you can search the actual changes to the code itself. This  can be super powerful if, for example, you're looking at code that has changed locations a few time, which makes the file history not very useful. It's also great to discover exactly when a piece of code was added or removed without needing to navigate through the full file history by hand.

🔎 The trainer should demonstrate:

* How to use the `type:diff` filter to search for contents in the committed code
* How to apply that filter from the sidebar or by typing it manually
* Highlight that the results will bring the customer into the same commit view as the `type:commit` search, so they'll have to click twice to view the changed file itself.
* The searches are unindexed, so more complicated searches may take longer to return results.

❗️ Make sure to highlight that diff search is also limited to 50 repos at a time, and it's best practice to narrow things down with a `repo:` filter first.


### Searching for specific authors (`author:`)

When looking at committed code, I sometimes want to narrow down the results so that I only see code from one particular colleague. This can be great to get up to speed on what someone was working on before they went on long-term leave or vacation, or to remind myself what I've been working on before chatting with my manager. I can do this with the `author:` filter, which is specific to `commit:` and `diff:` searches.

🔎 The trainer should demonstrate:

* How to use the `author:` filter to narrow down the previous `diff:` search to only code changed by a particular contributor.
* The `author:` filter takes both display names (e.g. `author:emily`) and code host usernames (e.g. `author:emchap`)

❗️ The `author:` filter does take email addresses (e.g. `author:sourcegraph.com` will return all Sourcegraph developers committing under their work email address), but since some users commit code under an auto-generated email address for security (visible by searching `author:github.com`) or their personal addresses (`author:gmail.com`), it's not necessarily useful.

### Searching in a specific date range (`before:` and `after:`)

As we've seen so far, the `diff:` and `commit:` searches will return results in reverse chronological order. Sometimes, however, you'll want to timebox results. This can be helpful if you're trying to see what changed while you were out on vacation, or if you know that a bug was introduced between two points in time and want to look at what changed only in that interval. 

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

Sometimes, it's more useful to look at changes to the code rather than the code in its present state. With the `commit` and `diff` searches and their `author`, `before`, `after`, and `select:commit.diff` filters, it's possible to find useful changes to the code over time and discover the origin of content I'm interested in. Next, we'll discuss more advanced search filters outside of the `diff:` and `commit:` search types.

### Resources

- [Sourcegraph](https://sourcegraph.com)
- [Sourcegraph Search Documentation](https://docs.sourcegraph.com/code_search/reference/queries#search-pattern-syntax)
- [Sourcegraph Search Cheat Sheet](https://learn.sourcegraph.com/how-to-search-code-with-sourcegraph-a-cheat-sheet)
- [Sourcegraph Documentation](https://docs.sourcegraph.com)

## Unit 3: Advanced search topics

**Learning goals:**

### Boolean operators (`AND`, `NOT`, `OR`)

### Searching for symbols (`type:symbol`)

### Using the `select:` keyword

### File contains (`file.contains(...)`)

### Repo contains file (`repo:contains.file(...)`)

### Repo has file (`repohasfile(...)`)

### Excluding stale repos (`repo:contains.commit.after(...)`)

### Dependency search (`repo:deps(...)`)

### Conclusion

### Resources

- [Sourcegraph](https://sourcegraph.com)
- [Sourcegraph Search Documentation](https://docs.sourcegraph.com/code_search/reference/queries#search-pattern-syntax)
- [Sourcegraph Search Cheat Sheet](https://learn.sourcegraph.com/how-to-search-code-with-sourcegraph-a-cheat-sheet)
- [Sourcegraph Documentation](https://docs.sourcegraph.com)
- [Dependencies Search](https://docs.sourcegraph.com/code_search/how-to/dependencies_search)

## Unit 4: Sourcegraph extensions

**Learning goals:**

### What are Sourcegraph extensions?

### How to find and enable extensions

### Introduction to IDE plugins

### The Sourcegraph CLI

### Conclusions

### Resources

- [Sourcegraph](https://sourcegraph.com)
- [Sourcegraph Search Documentation](https://docs.sourcegraph.com/code_search/reference/queries#search-pattern-syntax)
- [Sourcegraph Search Cheat Sheet](https://learn.sourcegraph.com/how-to-search-code-with-sourcegraph-a-cheat-sheet)
- [Sourcegraph Documentation](https://docs.sourcegraph.com)
- [Sourcegraph Extensions Documentation](https://docs.sourcegraph.com/extensions)
- [Sourcegraph CLI](https://docs.sourcegraph.com/cli)

## Closing thoughts

