# Sourcegraph 102

## Unit 1: Searching branches and revisions

After completing this unit, customers will be able to: search non-default branches and tags of your repos.

### Intro

Today's training builds on the search skills taught in Sourcegraph 101, focusing on more advanced search functionality and more complicated queries. By the end of this training, you should feel comfortable searching non-default branches and revisions, searching commit messages, using advanced search filters, and configuring Sourcegraph extensions. You can follow along in your own instance, or on [sourcegraph.com](https://www.sourcegraph.com/search), where you can set up a free account.

### Searching in a specific branch, tag, or revision

As covered in Sourcegraph 101, when searching code in Sourcegraph, the default behavior for the `repo:` filter is to return results from the `main`, `master`, or other default branch for a repo. 

![]()
[Alt text: a screenshot of a default `repo:` filter search, showing only results from the main branch of the repository.]

However, it's often useful to search for content on other branches, tags, or revisions. Common use cases for this include searching on a feature development or staging branch, rather than in production code. Take a moment to consider times when it's useful for you to see content on non-default branches that you may not have checked out locally.

In Sourcegraph, you have a few ways to search in these non-default branches.

The first would be to run a search with a fully-qualified `repo:` filter, and then use the left side menu to narrow down to a recent branch or tag. If you primarily search with dynamic filters, this may be your primary way of searching for non-default branches and tags. 

![]()
[Alt text: a screenshot of a default `repo:` filter search, showing the `repositories` selection now lists branches instead of repositories.]

The process is the same for both branches and tags; you'll want to toggle between the two on the side menu.

![]()
[Alt text: a screenshot of a default `repo:` filter search, showing the `repositories` selection now lists tags instead of branches or repositories.]

You can also manually filter to a branch using an `@` sign appended to the repo path, such as `repo:github.com/sourcegraph/sourcegraph$@3.18 ` to look for branches and tags named `3.18`. If you prefer to use a separate filter, you can—our `rev` filter works the same way. So, you could also run the search `repo:github.com/sourcegraph/sourcegraph$ rev:3.18` to return the same results. These do require the branch or tag name to be an exact match—to use fuzzy matching, you'll use glob syntax, which we'll discuss shortly.

Finally, if you want to navigate code at a particular point in time, you can use the `type:commit` or `type:diff` search options, then open the search results and click `Browse files at @commitHash` to view files at that specific commit.

![]()
[Alt text: a screenshot of a commit search result view highlighting the `Browse files at @commitHash` button]

These filters all rely on a repository being specified. If you don't have a `repo:` filter applied, or are trying to look for a branch or tag that doesn't exist in your specified repository or repositories, you'll see an error.

### Searching in multiple branches or tags

Sometimes, you need to search in multiple branches or tags, such as when you're not sure what branch content is included in. With Sourcegraph's support for glob syntax (using `*` as a wildcard character), this is possible.

To search all branches, you'll use `@*refs/heads/*` after the `repo:` filter, or `rev:*refs/heads/*`, depending on how you prefer to format your query. To search all tags, instead, you'll use `@*refs/tags/*` or `rev:@*refs/tags/*`.

If you want to search multiple revisions, but not _all_ revisions, that is possible. You'll add a colon (`:`) between each revision name. For example, if I wanted to search for branches `3.18` and `3.17` in the `github.com/sourcegraph/sourcegraph` repo, I would search for `repo:^github\.com/sourcegraph/sourcegraph$@3.18:3.17` or `github.com/sourcegraph/sourcegraph` repo, I would search for `repo:^github\.com/sourcegraph/sourcegraph$ rev:3.18:3.17`. 

It can be a little challenging to remember the "all branches" and "all tags" syntax. If you prefer, you can save `rev:*refs/heads/*` and `rev:@*refs/tags/*` as [search snippets](https://docs.sourcegraph.com/code_search/how-to/snippets#creating-custom-search-snippets). That way, you'll be able to add them to your query with one click.

### Excluding results from specific branches when searching in multiple branches

Sometimes, you will want results from multiple branches _except for_ one or a few in particular. You can exclude those from your results using the `*!` symbol in front of the glob pattern instead of the `*` character. You can think of the `*!` as a `NOT`, so something like `rev:*refs/tags/*3.19*:*!refs/tags/*3.19.0*` will find all patch releases of the `3.19` release but not the original `3.19.0` release.

For example, say that Alice's company uses a convention of `author/branchName` for tracking feature branches. To see every branch that included the word `patch` in the name, Alice could search for `repo:^github\.com/company/repo$ rev:*refs/heads/*patch*`. If Alice wants to exclude her own branches, she could search for `repo:^github\.com/company/repo$ rev:*refs/heads/*patch*:*!refs/heads/alice/*patch*`. 

### Conclusion

Sourcegraph's non-default revision search allows customers to search at any branch, tag, or commit hash in the codebase. Using the glob syntax, customers can run searches across a wide variety of revisions even without explicitly identifying them; they can also exclude results if needed. Combined with the commit search, covered next, this can be very powerful.

### Resources

- [Sourcegraph](https://sourcegraph.com)
- [Sourcegraph Search Documentation](https://docs.sourcegraph.com/code_search/reference/queries#search-pattern-syntax)
- [Sourcegraph Search Cheat Sheet](https://learn.sourcegraph.com/how-to-search-code-with-sourcegraph-a-cheat-sheet)
- [Sourcegraph Documentation](https://docs.sourcegraph.com)
