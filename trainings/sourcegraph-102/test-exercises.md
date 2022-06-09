# Sourcegraph 102 test exercises

Been through Sourcegraph 102 and ready to test your skills? These exercises will allow you to make sure you understand how to use Sourcegraph for advanced search. You can follow along on [sourcegraph.com](https://sourcegraph.com/search), or on your own Sourcegraph instance. 

## Exercises

**Searching for branches and tags**

How would I find code on the `v3.19.0` tag in the `github.com/sourcegraph/sourcegraph` repo?

**Searching commit messages**

How would I look for commit messages that are at least a month old, containing the string `gitserver`, in the `github.com/sourcegraph/sourcegraph` repo?

**Boolean filters**

How would I look in the `sourcegraph` GitHub org except for the `sourcegraph/sourcegraph` repo?

**Searching symbols**

How would I search for all functions containing the string `test` in their name in the Linux kernel (`github.com/torvalds/linux`)?

**Excluding stale repos**

How would I search for only repos in the `sourcegraph` GitHub org which have been updated in the last month?

## Answer key

1. `context:global repo:^github\.com/sourcegraph/sourcegraph$ rev:*refs/tags/v3.19.0 patternType:literal` - You'll want to use the `rev:` filter to search for that tag. Alternatively, you can use the `@` syntax for `context:global repo:^github\.com/sourcegraph/sourcegraph$@*refs/tags/v3.19.0 patternType:literal`.
2. `context:global repo:^github\.com/sourcegraph/sourcegraph$ type:commit before:"1 month ago" gitserver patternType:literal` - You'll need to append the `type:commit` filter to search the comment message text, the `before:"1 month ago"` filter to limit the timeframe, and then add your search for `gitserver` to look for that in the commit message contents. 
3. `context:global repo:^github\.com/sourcegraph/ NOT repo:github.com/sourcegraph/sourcegarph$ patternType:literal` - Using the `NOT` Boolean operator while searching within the `sourcegraph` GitHub org will show you the content you're looking for! You can also use `context:global repo:^github\.com/sourcegraph/ -repo:github.com/sourcegraph/sourcegarph$ patternType:literal` instead, if you prefer the minus sign syntax.
4. `context:global repo:^github\.com/torvalds/linux$ type:symbol select:symbol.function test patternType:literal` - You'll need to use `type:symbol` to search symbol names, and `select:symbol.function` to narrow down to just functions.
5. `context:global repo:^github\.com/sourcegraph/ repo:contains.commit.after(1 month ago)  patternType:literal` - You can also use `context:global repo:^github\.com/sourcegraph/ repohascommitafter:"1 month ago" patternType:literal`. The `repo:` filter combined with the `conains.commit.after` or `repohascommitafter` filter will allow you to narrow down your result set.
