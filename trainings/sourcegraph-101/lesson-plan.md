This represents a lesson plan formatted version of our [talk track](talk-track.md). This is likely most useful for customers in a train-the-trainer situation or experienced CEs who wish to build their own scripts based on overall goals of the webinar.

# Sourcegraph 101

**Topic:** This training is focused on learning to use Sourcegraph, starting from zero. More advanced topics are covered in other trainings, as are admin tasks. This document covers the training in lesson plan format. If you'd prefer a talk track, please see [this document](talk-track.md), instead.

## Intro

Today's training should take a new user from zero to being able to use Sourcegraph confidently. We of course don't have time for a dive into all of what Sourcegraph can do today, so if you would like more info, check out our Sourcegraph 102 training. Questions can be answered by your customer engineer, or support@sourcegraph.com.

Today we'll walk through what Sourcegraph is, our search options, our search filters, our code intelligence functionality, and our notebook functionality. By the end, you should be comfortable using all of those features! You can follow along in your own instance, or on [sourcegraph.com](https://www.sourcegraph.com/search), where you can set up a free account.

## Unit 1: Get familiar with Sourcegraph

**Learning goals:** After completing this unit, customers will understand what Sourcegraph is and what it does, understand its 5 most common use cases, and learn a little more about how other companies use Sourcegraph.

### What is Sourcegraph?

Sourcegraph is:

* A code search engine that runs in the browser
* A code intelligence platform to understand your code
* Accessible via a [CLI](https://docs.sourcegraph.com/cli)
* Accessible via [editor extensions](https://docs.sourcegraph.com/integration/editor)

It has three search modes:

1. Literal
2. Regular expression
3. Structural

Sourcegraph also offers:

* Code intelligence (find references/go to def)
* Commit message search
* Diff search
* Symbol search
* Non-default branch search

This training is focused on basic search.

### What are common use cases for Sourcegraph?

Typically, developers use Sourcegraph for [five key use cases](https://about.sourcegraph.com/use-cases/): 

1. Finding and fixing security vulnerabilities - If a CVE is announced, easily find if your code uses an impacted version of a dependency.
2. Accelerating developer onboarding for new team members - Allow new developers to answer their own questions by being able to search *all* code, rather than having to guess-and-check where the code they need is located.
3. Resolving incidents faster - Easily search recent changes to the code to find what might have caused the issue.
4. Streamlining code reuse - Surfacing code via search means it’s easier to avoid reinventing existing code, leading to more consistent, efficient coding practices.
5. Improving code health - If you’re trying to change from an antipattern to a best practice, use Sourcegraph to see how much work there is to do across the entire codebase.

While working through the training, think about which of these use cases is most relevant to your day to day work. That will help you conceive of how Sourcegraph might be most relevant to your particular needs, so that you can get the most out of the tool.

### Conclusion

Sourcegraph is a code search and intelligence platform that allows you to find all of your company’s code in the browser in order to make your work easier and more efficient. Next up, we’ll dive in to the tool to learn how to search in Sourcegraph.

### Resources

- [Sourcegraph](https://sourcegraph.com)
- [Sourcegraph Documentation](https://docs.sourcegraph.com)
- [Sourcegraph Use Cases](https://about.sourcegraph.com/use-cases)
- [Sourcegraph Customer Case Studies](https://about.sourcegraph.com/case-studies)

## Unit 2: Navigating the Sourcegraph UI

**Learning goal:** After completing this unit, customers will be able to navigate the Sourcegraph home page, understand the search mode buttons, and be able to navigate the search results page. 

### The Sourcegraph home page

Sourcegraph is primarily a browser application. While following along here, you can use your own Sourcegraph instance, or [sourcegraph.com](https://www.sourcegraph.com). Your Sourcegraph administrator should be able to provide you the URL for your own instance.

The main focus of the home page is the search bar. By default, you’ll see context:global is selected. This means that you will search all of your company’s code to which you have access. You can change that by setting up search contexts, discussed later.

🔎 The trainer should demonstrate:

* How to enter a query into the search bar
* How to search for a literal string

❗️Make sure to call out that quotes are not required in literal searches.

### The search mode buttons

In addition to our default literal, or exact match, search mode, Sourcegraph offers two other search modes: regular expression, and structural search. To run a search in either of these modes, you’ll use the appropriate icons in the search bar, on the right-hand side of the bar, next to the search button.
Sourcegraph also offers a structural search, useful for multiline, syntax-aware searching. 

🔎 The trainer should demonstrate:

* Where the buttons are located.

### The search results page

Let's chat through what you'll see when you run the search. When you run your search, you will be redirected to a search results page. 

🔎 The trainer should run a new regex or literal search, and show:

* How matching text is highlighted
* Where the repo name and file path are displayed in the result

On the left-hand side of the page, you’ll see options to run different kinds of searches, filter your search results dynamically, or manually filter your searches by repository, language, and other search filters. We'll dive into those later in the training.

Clicking on your search results will open the matching code, file, or repo in Sourcegraph. From there, you can view the full file and navigate to other files in the same repo, or run a new search.

### Conclusion

Sourcegraph offers three search modes (literal, regex, and structural) controlled by buttons in the search toolbar. In our next units, we’ll learn more about those search modes and filters to narrow down your search results. 

### Resources

- [Sourcegraph](https://sourcegraph.com)
- [Sourcegraph Documentation](https://docs.sourcegraph.com)

## Unit 3: Introduction to searching

**Learning goall:** By the end of this unit, users should understand how to use three search types.

### Literal search

As we discussed in the last unit, literal search is Sourcegraph's default search option. Performing a literal search is useful when you know the exact string that you're looking for in a code base, like a particular function or variable name. You can find all occurrences of the name across multiple repositories by using your query as a literal pattern. It's also useful for finding textual content—like error messages or comments—in the code.

🔎 The trainer should demonstrate:

* Running a literal search, such as finding an error message


### Regular expression search

Start searching with regular expression patterns by toggling the dot asterisk (.*) button towards the right-hand side of the search box. When you mouse over it you'll receive a tooltip that reads Enable regular expression. Once it is highlighted, you're ready to search with regular expressions. Sourcegraph uses RE2 regex syntax, and if you ever want to check your regex you can do so at a site like Regex 101.

🔎 The trainer should demonstrate:

* Running a regular expression search, such as `\b(read|write)File\b`
* Using a space for fuzzy matching

### Structural search

Structural search helps you search code for syntactical code patterns like function calls, arguments, `if...else statements`, and `try...catch statements`. It's useful for finding nested and recursive patterns as well as multi-line blocks of code. They're different from regular expressions because they take into account the syntax of code, like balanced brackets, quoted strings, and delimiters.

To run a structural search, click the `[]` button in the search toolbar. Structural searches are limited to 30 lines of results by default. To return more results, add `count:all` or `count:100` (or any number) to your search.

🔎 The trainer should demonstrate:

* Running a structural search such as `context:global fprintf(stderr, ...) lang:c repo:^github\.com/torvalds/linux$ patternType:structural`
* Finding `try..catch...finally` statements: `context:global try {...} catch (...) { } finally {...} lang:java patternType:structural`

### Conclusion 

Sourcegraph allows you to search using literal search, regular expression search, and structural search. In our next unit, we'll discuss how to use those search results, save searches, export search results, and share them with your team. We'll also discuss dynamic search filters and how to change how the search results are grouped and displayed.

### Resources

- [Three ways to search code with Sourcegraph](https://learn.sourcegraph.com/three-ways-to-search-code-with-sourcegraph)
- [Sourcegraph code search cheat sheet](https://learn.sourcegraph.com/how-to-search-code-with-sourcegraph-a-cheat-sheet)

## Unit 4: Search results

**Learning goals:** After completing this unit, you'll understand the search results page and how to export, save, and link to search results.

### Saving your search to run again

If your search is one which you run frequently, you can save it so that you can quickly use the search again. You have two ways to do this: search contexts and search snippets.

#### Search contexts

Search contexts are a way to quickly search within a particular set of repos or files. If you're regularly searching within only your own team's repos, or only frontend or backend repos, search contexts are the way to do that!

🔎 The trainer should demonstrate:

* How to save a search context

#### Search snippets

Setting up a search snippet will create a one-click link on the bottom left of the search filter menu. This allows you to add query contents with one click. This is super useful if you're regularly wanting to add a combo of filters or text to other queries.

🔎 The trainer should demonstrate:

* Creating a search snippet
* Using a search snippet once created

### Exporting search results 

To export your search results, you will need to enable the `search-export` extension if it's not already enabled for your instance. To do that, click on the extensions icon (a puzzle piece on the top of the page) to open the extensions page. Search for `search-export`, and click the `enabled for me` slider until it turns blue.

🔎 The trainer should demonstrate:

* Enabling the search export extension
* Using it to generate a CSV

### Linking to search results

Sourcegraph search results are meant to be shared! Whether sharing a link with a colleague to ask for more information on code they wrote, or using a link to facilitate pair programming, Sourcegraph is better when used together. To link to content in Sourcegraph, you can simply copy the URL in the browser bar and share it—that will link to the same page for anyone who has access to your Sourcegraph instance.

If you're looking at the main/master branch of a repo and want to ensure that you're linking to the exact commit SHA when sharing the file, you'll want to click the link icon in the top right of the screen, below the search bar. That will update the page URL to be a permalink, and you can copy that URL and share it with teammates.

🔎 The trainer should demonstrate:

* How to link to a result from the browser bar
* How to generate a permalink

### Dynamic filters

Sourcegraph provides filters to narrow down your search result. You'll see on the top left that it's suggesting filters based on the results that were returned. We'll dive into these in more detail in the next unit.

🔎 The trainer should show:

* Where dynamic filters are located

### Changing how the search results are grouped and displayed

Sourcegraph offers an important filter to group your results. If you search for `fizz buzz`, for example, you'll see all of the files, file names, and repos where `fizz buzz` appears. If you instead want to see all of the repos that contain the code that includes the string `fizz buzz`, you can do that with our `select:` filter. Adding `select:repo` will group the results by repo, and `select:file` will group them by file. This is super useful if you want to find all repos which contain a particular dependency, for example.

🔎 The trainer should show:

* Applying the `select:repo` filter

### Conclusion

With our query filters, you can narrow things down to find just the content you need, based on the results that Sourcegraph is returning!

## Unit 5: Basic search filters

**Learning goals:** After completing this unit, you'll be able to use Sourcegraph's most common search filters to structure a search query.

### Language (`lang:`)

The `lang:` filter allows you to narrow your search so that you only see results in a particular language. This can be particularly useful for filtering your results to a particular frontend or backend language, rather than the entire language stack available to you.

### Repository (`repo:` filter)

With the `repo:` filter, you can narrow search results to code in a particular repository or repositories of code. The `repo:` filter allows you to specify the repo path and allows for you to use a regex in the path, regardless of the search mode you're using. So, for example, `repo:.*/sourcegraph$` would find any repo named `sourcegraph`, no matter the code host it's stored on. The filter will handle substring matching by default, so searching `repo:sourcegraph` will find any repo with `sourcegraph` anywhere in its name.

To use the `repo:` filter, you can either type it directly into your query, or use the list of repositories that are dynamically populated on the left side of the page after running an initial search.

### File and directory path (`file:`) filter:

Oftentimes, it's useful to limit your search results to a particular file—say you only want results from a particular directory because that's where test files are stored, or only need to see a dependency in Dockerfiles, not elsewhere in the code. To narrow those results down, add `file:` to your query.

### The content (`content:`) filter

Sometimes, you'll want to look for content that interacts with Sourcegraph's search query language—for example, you're looking for the literal string `lang:` in your code! To handle that, use our `content: filter`, and wrap your query in quotes. So, for example, `content:"lang:"` will let you search for that string without issue.

### Negating filters

By default, our filters are inclusive—you're searching for code that is in a particular repo, file, language, etc. However, those filters support exclusive searches, too—you can search for code that's not in a particular repo, file, or language. To do that, add a minus sign or hyphen (`-`) in front of a query, such as `new auth provider -lang:go` to find the new auth provider string everywhere except in Golang files.

How to apply a `lang:` filter from the dynamic filters, and what it does
* How to apply a `file` or `-file:` filter from the dynamic filters, and what it does
* The repositories listed under the dynamic filters, how they are listed (greatest to least number of results), and what happens when they're clicked on
* How to search a non-default branch once the `repo:` filter is applied

🔎 The trainer should show:

* Applying the `lang:` filter
* Applying the `file:` filter and negating it
* Applying the `repo:` filter from the sidebar and using that to navigate to a non-default branch
* Applying the `content:` filter

## Closing thoughts

Thanks so much for staying with me through this training! Today we covered our basic search functionality, our search filters, how to search commit and code history, code intelligence, notebooks, and our extensions platform. This should set you up for success in using Sourcegraph—if you have any issues, please post in Slack or shoot an email to support@sourcegraph.com so we can help you out.
