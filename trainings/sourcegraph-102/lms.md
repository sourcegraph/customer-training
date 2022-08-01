# Sourcegraph 102

## Unit 1: Searching branches and revisions

After completing this unit, customers will be able to: search non-default branches and tags of your repos.

### Intro

Today's training builds on the search skills taught in Sourcegraph 101, focusing on more advanced search functionality and more complicated queries. By the end of this training, you should feel comfortable searching non-default branches and revisions, searching commit messages, using advanced search filters, and configuring Sourcegraph extensions. You can follow along in your own instance, or on [sourcegraph.com](https://www.sourcegraph.com/search), where you can set up a free account.

### Searching in a specific branch, tag, or revision

As covered in Sourcegraph 101, when searching code in Sourcegraph, the default behavior for the `repo:` filter is to return results from the `main`, `master`, or other default branch for a repo. 

![A screenshot of a default `repo:` filter search, showing only results from the main branch of the repository.](https://user-images.githubusercontent.com/9934079/172725861-cd796ca4-d10e-4700-8897-e824af3bd2d5.png)

[Alt text: a screenshot of a default `repo:` filter search, showing only results from the main branch of the repository.]

However, it's often useful to search for content on other branches, tags, or revisions. Common use cases for this include searching on a feature development or staging branch, rather than in production code. Take a moment to consider times when it's useful for you to see content on non-default branches that you may not have checked out locally.

In Sourcegraph, you have a few ways to search in these non-default branches.

The first would be to run a search with a fully-qualified `repo:` filter, and then use the left side menu to narrow down to a recent branch or tag. If you primarily search with dynamic filters, this may be your primary way of searching for non-default branches and tags. 

![A screenshot of a default `repo:` filter search, showing the `repositories` selection now lists branches instead of repositories.](https://user-images.githubusercontent.com/9934079/172725944-6a473493-d8e7-4603-898f-68f9207817f6.png)

[Alt text: a screenshot of a default `repo:` filter search, showing the `repositories` selection now lists branches instead of repositories.]

The process is the same for both branches and tags; you'll want to toggle between the two on the side menu.

![A screenshot of a default `repo:` filter search, showing the `repositories` selection now lists tags instead of branches or repositories.](https://user-images.githubusercontent.com/9934079/172726018-78722b5d-13a2-46e8-90cb-60a025eed96c.png)

[Alt text: a screenshot of a default `repo:` filter search, showing the `repositories` selection now lists tags instead of branches or repositories.]

You can also manually filter to a branch using an `@` sign appended to the repo path, such as `repo:github.com/sourcegraph/sourcegraph$@3.18 ` to look for branches and tags named `3.18`. If you prefer to use a separate filter, you can—our `rev` filter works the same way. So, you could also run the search `repo:github.com/sourcegraph/sourcegraph$ rev:3.18` to return the same results. These do require the branch or tag name to be an exact match—to use fuzzy matching, you'll use glob syntax, which we'll discuss shortly.

Finally, if you want to navigate code at a particular point in time, you can use the `type:commit` or `type:diff` search options, then open the search results and click `Browse files at @commitHash` to view files at that specific commit.

![A screenshot of a commit search result view highlighting the `Browse files at @commitHash` button](https://user-images.githubusercontent.com/9934079/172726114-b2b6c89c-b8d2-4e89-8352-85e65f5c5a3d.png)

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

### Quiz

1. How would I search for code across tags containing `3.19` as well as tags containing `3.20`?

* A. `rev:*refs/tags/*3.19*:*refs/tags/*3.20*`
* B. `rev:*refs/tags/*3.19*:!*refs/tags/*3.20*`
* C. `!*refs/tags/*3.19*:*refs/tags/*3.20*`
* D. Sourcegraph already looks across all tags by default.

2. What branches will a `repo:` filter search by default?

* A. `master` or `staging`
* B. `master`, `main`, or another default branch
* C. A revision must always be specified
* D. All branches are searched by default

Answers:

1. A
2. B


## Unit 2: Searching commits

After completing unit, customers will understand how to search through `type:diff` and `type:commit` queries, and how to apply the `author:` and `before:`/`after:` filters to those queries. They'll also understand how to search for added/removed content, specifically.

### Searching through commit messages (`type:commit`)

Sometimes, as a developer looking for code, I may not know where in the code the feature I'm working on is defined. One way to find that content is to look for commit message contents which reference the feature in question, and then look at the code which was changed to discover where in the codebase I should be looking. This is possible with Sourcegraph commit search, and I don't need to pull the repos down locally to view that commit history.

To run a commit message search, you can either add `type:commit` to your query manually (e.g. `repo:^github\.com/sourcegraph/sourcegraph$ type:commit gitserver`) or click the `Search commit messages` link on the left side of the search result page.

![A screenshot showing the location of the `Search commit messages` link on the left side of the page.](https://user-images.githubusercontent.com/9934079/172726198-da40a132-5ed0-4bfc-8324-058480ebda28.png)

[Alt text: A screenshot showing the location of the `Search commit messages` link on the left side of the page.]

When running a search of commit messages, the search will run on the commit message contents, not the changed code. (We'll cover how to do that in the next section.)

Once you run a commit message search, you'll be presented with search results showing the matching commit messages, similar to how you would typically see matching code. Clicking on the commit message will bring you to a page showing all of the changes that happened in that commit, and the paths to each changed file. 

![A screenshot showing where the file path is displayed in a commit message result page, in order to navigate to that file at the specific commit.](https://user-images.githubusercontent.com/9934079/172726307-07af6c02-889c-46c3-a7af-fbb7cff6b03a.png)

[Alt text: A screenshot showing where the file path is displayed in a commit message result page, in order to navigate to that file at the specific commit.]

You can open a particular file at the commit you're looking at by clicking on its linked file path in the search result. You can also toggle between a `unified` view of the changes and a `split` view of the changes, depending on your preference.

From this screen, you can also click on your code host icon in the top right of the page, and you'll be brought to the commit view in your code host. This can be useful if you use your code host for code review, as you'll be able to view additional comments on the merge request or pull request discussion page. 

### Searching through diff content (`type:diff`)

We just saw that it's possible to search the contents of your colleagues' commit messages using the `type:commit` filter. With the `type:diff` filter, you can search the actual changes to the code itself. This can be super powerful if, for example, you're looking at code that has changed locations a few time, which truncates the file history, making it not very useful. It's also great to discover exactly when a piece of code was added or removed without needing to navigate through the full file history by hand.

Similar to the commit message search, you can run a search over code changes by applying `type:diff` manually to your search, or clicking `Search diffs` on the left side navigation bar. 

![A screenshot showing the location of the `Search diffs` link on the left side of the page.]
(https://user-images.githubusercontent.com/9934079/172726343-6482a82c-592b-4c46-8b9f-d54902f8b2c9.png)

After you run the search, you'll see search results that highlight the changed code which triggered the match. 

![A screenshot showing a matching diff search result, highlighted with green for added code and red for removed code.](https://user-images.githubusercontent.com/9934079/172726402-bc572285-081b-4d31-a461-e0515c7f0ac1.png)

[Alt text: A screenshot showing a matching diff search result, highlighted with green for added code and red for removed code.]

Clicking into the result will bring you to the same view of the commit message and changed files as when viewing a commit message search result, and all of the same navigation options (clicking into individual files, opening a link to the code host) are available to you.

### Searching for specific authors (`author:`)

When looking at committed code, I sometimes want to narrow down the results so that I only see code from one particular colleague. This can be great to get up to speed on what someone was working on before they went on long-term leave or vacation, or to remind myself what I've been working on before chatting with my manager. I can do this with the `author:` filter, which is specific to `type:commit` and `type:diff` searches.

To search for an author, append `author:` to your search, followed by the person's display name. You can search by email address, but given that many users will commit code under an auto-generated email address for security or their personal email address, the results will likely be missing results you want to find. The filter does support partial matching, so you can search `author:jane` or `author:"jane doe"` for a colleague named Jane Doe. An example query to find commits to the Linux kernel from Linus Torvalds (username `torvalds`) would be `context:global repo:^github\.com/torvalds/linux$ type:commit author:linus patternType:literal`; `context:global repo:^github\.com/torvalds/linux$ type:commit author:"linus torvalds" patternType:literal` (with the full name in quotes) will also work, as would `context:global repo:^github\.com/torvalds/linux$ type:commit author:torvalds patternType:literal`, as his email address contains the string `torvalds`. 

If you append the `author:` filter to a non-commit, non-diff search, the app will return an error.

### Searching in a specific date range (`before:` and `after:`)

As we've seen so far, the `type:diff` and `type:commit` searches will return results in reverse chronological order. Sometimes, however, you'll want to timebox results. This can be helpful if you're trying to see what changed while you were out on vacation, or if you know that a bug was introduced between two points in time and want to look at what changed only in that interval. 

To use these filters, add `before:"1 day ago"` or `after:"july 1 2020"` to your `type:diff` and `type:commit` searches. Formats can either be relative (`1 day ago`, `5 weeks ago`, `2 months ago`, `3 years ago`) or reference a specific date (`july 1 2020`). You'll need to wrap your date in quotes, as shown in the examples here. You can use just `before:`, just `after:`, or both to provide start and end dates to your searches. This can result in a search such as `context:global repo:^github\.com/sourcegraph/sourcegraph$ type:diff author:bob before:"1 week ago" after:"2 months ago" patternType:literal` to look for any changes to code in the `sourcegraph/sourcegraph` repo from between 2 months and a week ago, added by any colleague with `Bob` in their display name or username.

### Searching for added/removed text (`select:commit.diff.added` and `select:commit.diff.removed`)

Finally, sometimes I want to look at changes to code that are specifically related to adding or removing content. Say that I know something _used_ to be in our docs, and I want to find out when we took it out. We can do that using the `select:` filter, which we'll talk about a little bit more in our next unit.

To do that, you'll want to add `select:commit.diff.added` or `select:commit.diff.removed` to your `type:diff` or `type:commit` searches. So, for example, `context:global repo:^github\.com/sourcegraph/sourcegraph$ type:diff new auth provider patternType:regexp` would show me all instances where the regular expression `new.*auth.*provider` was added to or removed from the `sourcegraph/sourcegraph` repo. If I narrow it down to just `context:global repo:^github\.com/sourcegraph/sourcegraph$ type:diff new auth provider select:commit.diff.added  patternType:regexp`, I'll see only places where that code was *added* to the codebase.

If you don't remember the syntax, the Sourcegraph autocomplete filter will help you. Typing `select:` will display 
the options you can select; selecting the `diff` option will show the `.added` and `.removed` syntax.

![A screenshot showing the autocomplete menus associated with the `select:` filter.](https://user-images.githubusercontent.com/9934079/172726502-ec74d877-a03d-473b-9a94-390d2f252169.png)

[Alt text: A screenshot showing the autocomplete menus associated with the `select:` filter.]

### Conclusion

Sometimes, it's more useful to look at changes to the code rather than the code in its present state. With the `commit` and `diff` searches and their `author`, `before`, `after`, and `select:commit.diff` filters, it's possible to find useful changes to the code over time and discover the origin of content I'm interested in. Next, we'll discuss more advanced search filters outside of the `type:diff` and `type:commit` search types.

### Resources

- [Sourcegraph](https://sourcegraph.com)
- [Sourcegraph Search Documentation](https://docs.sourcegraph.com/code_search/reference/queries#search-pattern-syntax)
- [Sourcegraph Search Cheat Sheet](https://learn.sourcegraph.com/how-to-search-code-with-sourcegraph-a-cheat-sheet)
- [Sourcegraph Documentation](https://docs.sourcegraph.com)

### Quiz

1. Why is it not considered best practice to use `author:` with email addresses?

* A. Sourcegraph cannot search commit email addresses
* B. Email addresses can be hard to remember
* C. Some users will use an anonymous email address for their commits
* D. It is considered best practice

2. What does the `type:diff` filter do?

* A. Searches commit messages
* B. Searches between two specified revisions
* C. This isn't a valid filter
* D. Searches generated diffs for code commits/changes to the code

3. What does adding `select:diff.commit.added` to a `type:diff` search do?

* A. Looks for places where the search term was added to code
* B. Adds commit messages to the search
* C. Duplicates the `type:diff` filter
* D. Not a valid search

Answers:

1. C
2. D
3. A

## Unit 3: Advanced search topics

After completing this unit, customers will understand how to use several useful, advanced search filters not covered in Sourcegraph 101.

### Boolean operators (`AND`, `NOT`, `OR`)

Sometimes, when searching for code, developers may need to combine multiple queries together. Sourcegraph supports combining search phrases into more complete queries using the boolean `AND`, `NOT`, and `OR` operators. They work like they do in other search tools; if you want to group subqueries together, you can use parentheses to do so.

A common use case for using Boolean filters is searching within multiple repos. As a developer, I may want to search in both my main production repo and a repo used internally for tests. To do so, I would use the `OR` operator, like so: `(repo:github.com/sourcegraph/sourcegraph$ OR repo:github.com/sourcegraph/customer-training$) (lang:Go OR lang:javascript)`. As you can see here, I'm searching for code in either of the two repos, and looking for code in either Golang or JavaScript. I can use parentheses to group those queries.

The most frequent use case for the `AND` filter is searching for a file that contains two pieces of content, without requiring them to be in the same line. Searching `context:global repo:github.com/sourcegraph/sourcegraph$ new auth provider patternType:regexp` will show me files where `new`, `auth`, and `provider` appear in sequence together; however, if I simply want places where all three strings are present without caring about the order or proximity, I can search for `context:global repo:github.com/sourcegraph/sourcegraph$ new AND auth AND provider patternType:regexp` instead. 

Finally, you may want to use the `NOT` filter to exclude a string from your search. Say you want to look for `auth` matches but want to ignore `author` matches—to do that, you'd search for `context:global auth NOT author patternType:regexp`. 

One final note: sometimes, you will want to search for `AND`, `OR`, and `NOT` literally—say you're looking for a comment that contains them. To do so, you'll use the `content:` filter, such as: `context:global content:"// set and get" lang:go patternType:regexp`. Without the `content:` filter, those strings will be interpreted as Boolean operators, so make sure to use the `content:` filter when appropriate!

### Searching for symbols (`type:symbol`)

So far we've seen three types of search in Sourcegraph: our default code search, our `diff` search, and our `commit` search. Sourcegraph offers a fourth search mode, `type:symbol`. This allows you to specifically search for the names of symbols (such as functions, variables, classes, etc.) in your code, and results will be an easy-to-parse list of the symbols sorted by file.

Like the other search types, the symbol type search can be applyed using `type:symbol` in your query, or by clicking `find a symbol` on the left side search bar. 

![A screenshot showing the left sidebar's "find a symbol" link.](https://user-images.githubusercontent.com/9934079/172726552-66527cc4-a4aa-410f-9c52-0b226b3b277a.png)

[Alt text: a screenshot showing the left sidebar's "find a symbol" link.] 

When the `type:symbol` filter is appended to the query, the search will run against symbol names. So, `context:global new user type:symbol repo:sourcegraph patternType:regexp` would look for any function, structure, variable, etc. that contains the `new.*user` string in its name. Next to each search result will be an icon indicating the kind of symbol that it is; hovering over the icon will show the symbol type in a tool tip.

### Using the `select:` keyword

The `select:` filter is a very powerful way of grouping results. You saw us use this earlier with `select:diff.commit.added`; this allowed us to only view committed code that added the search term. You can use it to group results on other queries, too. This can be super useful when trying to figure out not just _where_ a particular match is occurring in your code, but which repos, overall, contain the match. For example, this way you can see a list of which repos rely on an out-of-date dependency, rather than just seeing the raw code containing the out-of-date dependency. 

To find the files containing search results, add `select:file` to your query. So, for example, if I search `context:global bluebird@^3.0.5 patternType:literal`, I'll see a variety of results that contain the `bluebird@^3.0.5` string. If I search for `context:global bluebird@^3.0.5 select:file patternType:literal`, I'll see instead a list of the files that contain the reference to that version of Bluebird.

Similarly, if I instead append `select:file.directory`, I'll see only the directories that contain the matching code, not the code itself. This can be helpful if your code always contains test files in a particular directory, for example.

Adding `select:repo` to a query will show you all the repositories that contain results. This can be very helpful for finding out which projects are impacted by an out-of-date dependency that needs to be upgraded. For example, `context:global org\.apache\.logging\.log4j 2\.(0|1|2|3|4|5|6|7|8|9|10|11|12|13|14|15)(\.[0-9]+) patternType:regexp` shows me all references to out-of-date versions of Log4J in my code, but `context:global org\.apache\.logging\.log4j 2\.(0|1|2|3|4|5|6|7|8|9|10|11|12|13|14|15)(\.[0-9]+) select:repo patternType:regexp` will show me a list of the repos containing that code, instead. If you have individuals in charge of different repositories, that information is often most useful for figuring out who needs to be involved in remediation, rather than seeing the individual code matches.

Finally, we offer the `select:symbol.symbolType` filter. This allows you to filter `type:symbol` searches to just a certain kind of symbol. For example, if I run a search for `context:global oauth repo:sourcegraph type:symbol  patternType:regexp`, I'll see variables, functions, packages, etc. that match the `oauth` search in any applicable repo. If I instead search for `context:global oauth repo:sourcegraph type:symbol select:symbol.function  patternType:regexp`, I will only see functions that match my query.

### Repo contains file (`repo:contains.file(...)` and `repohasfile:`)

Sometimes, as a developer I only want to search within a repo that has a particular file—say I want to find usages of a particular dependency but only in repos that have a license file, but I don't care about the contents of the file, just its presence. Using the `repo:contains.file(...)` filter allows me to do this.

Say that legal wants to know which repos use a particular dependency and have a license file, because they're ensuring legal compliance. By searching for `context:global repo:contains.file(LICENSE) file:package-lock.json debug patternType:regexp`, I can see which `package-lock.json` files contain a reference to `debug` only in repos that have `license` files. If I want, I can even append the `select:repo` filter to search `context:global repo:contains.file(LICENSE) file:package-lock.json debug select:repo patternType:regexp`, and that will give me an easy list of repos to provide to the legal team. 

If I want to exclude repos that contain a particular file, I can do so with a similar filter named `repohasfile:`. This filter, unlike `repo:contains.file(...)`, supports negation. So, if I want to only find repos that _don't_ contain a license file, I could quickly search `context:global -repohasfile:license select:repo patternType:regexp` to find that information.

### Excluding stale repos (`repo:contains.commit.after(...)`)

Oftentimes, as a developer I will want to search only in active repos. The easiest way to do this is to filter by commit date using `repo:contains.commit.after(...)`. This ensures that any repos without recent commits are excluded. The syntax is the same as the `before:` and `after:` filters covered previously. So, for example, `context:global repo:contains.commit.after(1 month ago) new auth provider patternType:regexp` will find any code matching the `new.*auth.*provider` search stored in repos that were updated in the last month.

As a note, the filter doesn't support negation. A user can instead use `repo.contains.commit.after(...) select:repo` to get a list of repos and then exclude them in a follow-up query if needed.

### Conclusion

Sourcegraph offers a variety of advanced search filters. We covered boolean operators, symbol search, the `select:` keyword, the `repo:contains.file(...)` filter, and how to exclude stale repos. Next up, we'll talk about our extensions platform.

### Resources

- [Sourcegraph](https://sourcegraph.com)
- [Sourcegraph Search Documentation](https://docs.sourcegraph.com/code_search/reference/queries#search-pattern-syntax)
- [Sourcegraph Search Cheat Sheet](https://learn.sourcegraph.com/how-to-search-code-with-sourcegraph-a-cheat-sheet)
- [Sourcegraph Documentation](https://docs.sourcegraph.com)
- [Dependencies Search](https://docs.sourcegraph.com/code_search/how-to/dependencies_search)

### Quiz

1. Does Sourcegraph support Boolean operators?

* A. Yes
* B. Yes, but only AND and NOT
* C. Yes, but only AND and OR
* D. No

2. How would a user search for a symbol definition?

* A. Add `symbol:` to their query
* B. Add `type:symbol` to their query
* C. Add `select:symbol` to their query
* D. Not possible

3. What does `select:repo` do to a search?

* A. Only searches repo names
* B. Shows code results ordered by repo
* C. Shows repos containing results
* D. Nothing

Answers:

1. A
2. B
3. C

## Unit 4: Sourcegraph extensions

After completing this unit, customers will understand what Sourcegraph extensions are available and how to access them and the CLI.

### What are Sourcegraph extensions?

Sourcegraph has a fully-featured extensions platform. Because our extensions API is available to users, you can develop against it as well, and build your own extensions. This can be particularly useful if you have a custom-built tool that you use internally which you would like to connect to Sourcegraph. Our most popular extensions include our search export extension and our code editor integrations.

### How to find and enable extensions

Extensions are found and enabled on the Extensions page, represented by a puzzle icon on the top of the page.

![A screenshot showing the location of the Extensions page icon.](https://user-images.githubusercontent.com/9934079/172726617-ae8681ef-a2c3-4d6c-9095-409c58ef1072.png)

[Alt text: A screenshot showing the location of the Extensions page icon.]

To enable an extension, click on its name on the extensions page. From there, you will see a slider to enable it for all users of your instance (if you're an instance admin) and a slider to enable it for just yourself. Clicking that toggle will turn it blue, at which point you should have access to the extension.

As an example, you can search for the `open-in-editor` extension. From there, you can enable the extension via the toggle.

![A screenshot showing the enabled `open-in-editor` extension.](https://user-images.githubusercontent.com/9934079/172726675-91075279-e2a9-4232-8ad7-fe5adc76038d.png)

[Alt text: A screenshot showing the enabled `open-in-editor` extension.]

Some extensions require configuration. To confirm if the extension you're using requires configuration, click on its name. The page it brings you to will show you what, if any, customization is needed. You can add any listed customization in your settings page, accessible by clicking on your user icon on the top right of the page and selecting `Settings`.

### Introduction to IDE plugins

The `open-in-editor` extension discussed previously will allow you to open local copies of files from Sourcegraph on your computer. But you can also navigate from your editor to Sourcegraph, using our editor extensions. And if you use a supported editor, you can use Sourcegraph directly in your editor.

To confirm if you can install Sourcegraph in your editor, please view our [supported editor extensions](https://docs.sourcegraph.com/integration/editor). These extensions are typically installed via the marketplace for the IDE in question.

Users of the VSCode extension will have a more integrated experience than users of other IDEs. You will need to configure your extension as outlined on its install page; once installed, you can use Sourcegraph directly from VSCode, without a need to navigate to the browser.

### The Sourcegraph CLI

As a developer, I may want to use Sourcegraph from the command line. This is possible, using our CLI!

The Sourcegraph CLI is documented on [GitHub](https://github.com/sourcegraph/src-cli), including the install process.

Configuation is documented in that repo's `README`. You will need to generate a Sourcegraph PAT to use the CLI, and store it as an environment variable. 

Once installed, you can view the CLI's functionality by typing `src` into your command line. To run a search, format your query as `src search 'query'`, with your query included in the quotes. For more information, type `src search -h`. 

### Conclusions

Sourcegraph extensions can be very powerful additions to give Sourcegraph "single pane of glass" access to your code. You can build your own extensions, and our CLI allows you to build your own queries without using the browser app. Users using some IDEs can even use Sourcegraph entirely in the IDE. During this course, we've covered advanced Sourcegraph functionality, such as searching non-default revisions, searching `diff` and `commit` content, and the `select:` filter. We also covered our extensions platform. With this knowledge, you're now empowered to run nuanced, expansive queries in Sourcegraph across all of your company's code.

### Resources

- [Sourcegraph](https://sourcegraph.com)
- [Sourcegraph Search Documentation](https://docs.sourcegraph.com/code_search/reference/queries#search-pattern-syntax)
- [Sourcegraph Search Cheat Sheet](https://learn.sourcegraph.com/how-to-search-code-with-sourcegraph-a-cheat-sheet)
- [Sourcegraph Documentation](https://docs.sourcegraph.com)
- [Sourcegraph Extensions Documentation](https://docs.sourcegraph.com/extensions)
- [Sourcegraph CLI](https://docs.sourcegraph.com/cli)
- [Sourcegraph Editor Integrations](https://docs.sourcegraph.com/integration/editor)

### Quiz

1. What does the Extensions icon look like?

* A. Puzzle piece
* B. Chain link
* C. Heart
* D. Globe

Answers: 

1. A
