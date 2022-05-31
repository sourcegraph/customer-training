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

**Learning goals:**

### Searching through commit messages (`type:commit`)

### Searching through diff content (`type:diff`)

### Searching for specific authors (`author:`)

### Searching in a specific date range (`before:` and `after:`)

### Searching for added/removed text (`select:commit.diff.added` and `select:commit.diff.removed`)

### Conclusion

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

