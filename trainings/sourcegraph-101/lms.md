# Sourcegraph 101

This training covers Sourcegraph 101's content, intended to be added to a customer's LMS system. Video content is linked in the appropriate unit.

----

## Unit 1: Get familiar with Sourcegraph

[Video content](https://drive.google.com/file/d/1mUgCMAk0ub1HoMPlCZOkbl93GEAg7eUH/view?usp=sharing)

After completing this unit, you'll be able to: understand what Sourcegraph is and what it does, understand its 5 most common use cases, and learn a little more about how other companies use Sourcegraph.

### What is Sourcegraph?

Sourcegraph is a code search engine that runs in the browser, as well as being available via a CLI or (in some editors) in your editor. In these units, we'll focus on the browser, but for more information on other ways to access the tool, see our [CLI documentation](https://docs.sourcegraph.com/cli) and [IDE extensions](https://docs.sourcegraph.com/integration/editor). 

With Sourcegraph, you can use literal, regular expression, or structurally aware searches and search filters to find information across your company's entire source code. Unlike using grep or searching locally in your editor, Sourcegraph allows you to see all of your company's code, regardless of what you have available locally. 

In addition to allowing you to search for your code, Sourcegraph provides additional functionality, such as [code intelligence](https://docs.sourcegraph.com/code_intelligence) (`find references` and `go to def` like you'd see in a local editor, available for all of your code); you can also do advanced searches such as searching commit messages, searching changes to your code, searching non-default branches, and searching symbols in your code.

### What are common use cases for Sourcegraph?

[A recently published research paper from Google](https://static.googleusercontent.com/media/research.google.com/en//pubs/archive/43835.pdf) and a [Google developer survey](https://docs.google.com/document/d/1LQxLk4E3lrb3fIsVKlANu_pUjnILteoWMMNiJQmqNVU/edit#heading=h.xxziwxixfqq3) showed that 98% of developers consider their Sourcegraph-like internal code search tool to be critical, and developers use it on average for 5.3 sessions each day, primarily to (in order of frequency):

- find example code
- explore/read code
- debug issues
- determine the impact of changes

Sourcegraph code search helps developers perform these tasks more quickly and effectively by providing fast, advanced code search across multiple repositories. Typically, developers use Sourcegraph for [five key use cases](https://about.sourcegraph.com/use-cases/): 

1. Finding and fixing security vulnerabilities - If a CVE is announced, easily find if your code uses an impacted version of a dependency.
2. Accelerating developer onboarding for new team members - Allow new developers to answer their own questions by being able to search *all* code, rather than having to guess-and-check where the code they need is located.
3. Resolving incidents faster - Easily search recent changes to the code to find what might have caused the issue.
4. Streamlining code reuse - Surfacing code via search means it's easier to avoid reinventing existing code, leading to more consistent, efficient coding practices.
5. Improving code health - If you're trying to change from an antipattern to a best practice, use Sourcegraph to see how much work there is to do across the entire codebase.

When reading through the following units, think about which of these use cases is most relevant to your day to day work. That will help you conceive of how the tool might be most relevant to your particular needs, so that you can get the most out of the tool.

### Customer profiles

Sourcegraph is used by companies of all sizes, and by companies which use a single monorepo and thousands of microservices. For a better idea of how Sourcegraph customers use the tool, check out [Sourcegraph's case studies](https://about.sourcegraph.com/case-studies/) from companies such as [Lyft](https://about.sourcegraph.com/case-studies/lyft-monolith-to-microservices), [CERN](https://about.sourcegraph.com/case-studies/cern-reduces-technical-debt), and [Cloudflare](https://about.sourcegraph.com/case-studies/cloudflare-accelerates-debugging-and-improves-security). 

### Conclusion

Sourcegraph is a code search tool that allows you to find all of your company's code in the browser in order to make your work easier and more efficient. Next up, we'll learn what each part of the Sourcegraph UI allows you to do.

### Resources

- [Sourcegraph](https://sourcegraph.com)
- [Sourcegraph Documentation](https://docs.sourcegraph.com)
- [Sourcegraph Use Cases](https://about.sourcegraph.com/use-cases)
- [Sourcegraph Customer Case Studies](https://about.sourcegraph.com/case-studies)

### Quiz

1. Which of these is a common use case for Sourcegraph? 
- A. Auto-writing source code
- B. Finding and fixing security vulnerabilities
- C. Streamlining code reuse
- D. B and C
- E. A, B, and C

Answer: D

## Unit 2: Navigating the Sourcegraph UI

[Video content](https://drive.google.com/file/d/1dEMGG6u-lsb2DTfqJK1QE3w18Tmwbqdv/view?usp=sharing)

After completing this unit, you'll be able to navigate the Sourcegraph home page, understand the search mode buttons, and be able to navigate the search results page. 

### The Sourcegraph home page

When first accessing your Sourcegraph instance, you will see a home page that looks similar to this:

![A screenshot of the Sourcegraph home page. It shows the Sourcegraph logo, a search bar to enter a search query, a list of recently-accessed repositories, a list of recent searches, and a list of recently-accessed files.](https://lh3.googleusercontent.com/_w0QqIPhZyiD-GHaDKXAPtbh50kkox_5aP0xEZHI73HSGfPyU2iwLRODKlblyrt2BbBJJk1OzPDPH0FfvZwb4qAgpb2AYQJyuJLoqK2wlJowhdPxuVlfXTIvZfSCtb8Ho4Ue5eYeooqOlvpMKA)

The main focus of the home page is the search bar. By default, you'll see `context:global` is selected. This means that you will search all of your company's code to which you have access. You can change that by setting up search contexts—we'll talk about how to do that in Unit 4.

If you've used Sourcegraph before, you'll see a list of recently-searched repositories, recently-run searches, and recently-viewed files. If you haven't used Sourcegraph before, those will be empty—to populate them, run a few searches! 

To run a search, type your query into the search bar, similar to searching on GitHub, GitLab, or Google. Press enter or click the blue magnifying glass button to start your search and to navigate to the search results page.

By default, your search will be run as a literal search (exact match), and will be run case-insensitively. If you want to run your search case-sensitively, click the `Aa` icon in the search bar. 

🔍 **You don't need to add quotes for exact matches!** Quotes will be interpreted literally, so `"fizz buzz"` will only match `"fizz buzz"` with quotes—most likely, not what you want. Just typing `fizz buzz` is enough.

### The search mode buttons

In addition to our default literal, or exact match, search mode, Sourcegraph offers two other search modes: regular expression, and structural search. To run a search in either of these modes, you'll use the appropriate icons in the search bar, on the right-hand side of the bar, next to the blue magnifying glass. 

To run your search using [RE2 regex syntax](https://github.com/google/re2/wiki/Syntax), click the `.*` icon before running your search. If you click that icon after running your search, your search will re-run as a regex search. In regular expression searches, space characters are handled as fuzzy matches. So, running a `fizz buzz` search in literal mode will only match `fizz buzz`; running the same search for `fizz buzz` in regex mode will match `fizz buzz`, `fizz pop buzz`, and `fizz popbuzz`. You'll also be able to use standard regular expression components, such as `fizz \bbuzz` to match `fizz buzz` and `fizz.buzz`. 

The final search mode option is our language-aware structural search option, represented by the square bracket button (`[]`). When selected, you'll have the option to include structural holes, represented by `…` or `:[a]` in your query, to run multi-line fuzzy searches. We'll go into this in more detail in the next unit.

### The search results page

When you run your search, you will be redirected to a search results page. It will look something like this:

![A screenshot of the Sourcegraph search results page. It shows a query for fizz buzz, along with previews of five files where fizz buzz is present as a string. On the left side of the page, there are options for Search Types, Dynamic Filters, Repositories, and Search Reference.](https://lh5.googleusercontent.com/9U7Hn9YIc_vBXqptsuPsgbiHLU9Q2TP-LLA-GCR601y0eD6-dGTXSlkLKhbwDMsEJ2rxPdckCrM7SiHHDacXqRPUFcXnWSUfBXuGt-tDwwrZ00nwPI8eejgPOMAscBQUEaMOMO5pIjXMSmeO7w)

The main area of the page will show your search results, with the matching text highlighted. Clicking on your search results will open the matching code, file, or repo in Sourcegraph. From there, you can view the full file and navigate to other files in the same repo, or run a new search. We'll discuss this page in more detail in Unit 4.

On the left side of the page, you'll see options to run different kinds of searches, filter your search results dynamically, or manually filter your searches by repository, language, and other search filters. 

### Conclusion

Sourcegraph offers three search modes, controlled by buttons in the search toolbar. In our next units, we'll learn more about those search modes and filters to narrow down your search results. 

### Resources

- [Sourcegraph](https://sourcegraph.com)
- [Sourcegraph Documentation](https://docs.sourcegraph.com)

### Quiz

1. Which of these literal searches will return an exact match for `fizz buzz`?
- A. `"fizz buzz"`
- B. `fizz buzz`
- C. `"fizz" "buzz"`
- D. `"fizz" buzz`

2. What does `context:global` do?
- A. Searches all the code available on github.com and gitlab.com
- B. Searches public repos
- C. Searches all the code on your instance
- D. Searches code in any language

3. What does the square bracket icon ([]) represent?
- A. Literal search
- B. Structural search
- C. Regular expression search
- D. Fuzzy search

Answers:

1. B
2. C
3. B

## Unit 3: Introduction to searching

[Video content](https://drive.google.com/file/d/10URdMlLuMIV59JIXdOP21RvisfUD5R8p/view?usp=sharing)

After completing this unit, you'll have an understanding of our three search types, when you might want to use each, and how to use them.

### Literal search

As we discussed in the last unit, literal search is Sourcegraph's default search option. Performing a literal search is useful when you know the exact string that you're looking for in a code base, like a particular function or variable name. You can find all occurrences of the name across multiple repositories by using your query as a literal pattern. It's also useful for finding textual content—like error messages or comments—in the code.

#### Finding function calls and definitions

As a developer, there are many times you may need to learn a new codebase: you may need to understand how best to use a new package, may need to be onboarded into an existing project, or may want to learn best practices from tried and tested software. A productive way to become familiar with a codebase is through selecting a function and understanding how it's used throughout the code and in what contexts.

For example, if you're learning how the Linux kernel works, one of the topics that you may want to understand is how Linux uses linked lists. Because linked lists are used throughout the Linux kernel and in driver code, they are a foundational starting point to familiarize yourself with the codebase.

The linked list data structure in Linux is called `list_head`. We can find all instances of the `list_head` structure by searching for it directly: [search on Sourcegraph](https://sourcegraph.com/search?q=list_head).

Literal search patterns can be used to find more than just functions or variables. They can also be used to find longer pieces of text, like error messages, as we'll explore in the next section.

#### Finding error messages

Literal search can help you find where a particular piece of text occurs within code. For example, if you're seeing an error message while debugging, it can be helpful to find where that message is defined in the code to get a better idea of what is causing it. You can search for an exact match by copying the error into your search.

Let's try an example. React is a framework used by many web apps, and its error messages are sometimes hard to debug. When a React component throws an error, it produces an error message like, `React caught an error thrown by Componen`t. When you get an error message like that, it isn't always clear what is going on. To learn more about the source of the error, you can search for the error message itself: [search on Sourcegraph](https://sourcegraph.com/search?q=React+caught+an+error+thrown).

By finding where an error message is defined, you can start to understand what conditions will cause this error. In this case, it happens when React catches an error that happened during the rendering phase in one of your components.

This kind of search also gives you an understanding of the inner workings of the codebase, and that can be really helpful to get a better mental model of how it works.

#### Finding sequences of words

By default, when searching for literal patterns in Sourcegraph, the entire query will be searched, even if the pattern consists of multiple worlds. You should not put your query in quotes: we'll go into more detail about this now.

Unlike a web search engine, if you search for two or more words on Sourcegraph, like `const counter`, then you'll only get results for `const` immediately followed by `counter`, as in the example here: [search on Sourcegraph](https://sourcegraph.com/search?q=const+counter).

Returning to our example in the Linux kernel, we can narrow down our search for `list_head` to only the cases where it's used as a simple structure (`struct`), by searching specifically for the `struct list_head` pattern: [search on Sourcegraph](https://sourcegraph.com/search?q=struct+list_head).

If you want to find all instances of those two words appearing in the same file but not necessarily in sequence, then you can use the `and` operator, or you can switch to regular expression mode, covered below: [search on Sourcegraph](https://sourcegraph.com/search?q=list_head+and+list_add_tail).

### Regular expression search

Start searching with regular expression patterns by toggling the dot asterisk (`.*`) button towards the right-hand side of the search box. When you mouse over it you'll receive a tooltip that reads `Enable regular expression`. Once it is highlighted, you're ready to search with regular expressions. Sourcegraph uses [RE2 regex syntax](https://github.com/google/re2/wiki/Syntax), and if you ever want to check your regex you can do so at a site like [Regex 101](https://regex101.com/).

#### Finding a set of function calls

One use case for regular expression search is when you are trying to find examples of file system function calls. You may be interested in functions that read or write files: `readFile` and `writeFile`. While you could search for them individually, it can be useful to perform one search that includes results for both functions.

`readFile` and `writeFile` have a pattern in common: they both end in `File`. We can write a regular expression that expresses this pattern like so: `\b(read|write)File\b` ([search on Sourcegraph](https://sourcegraph.com/search?q=context:global+\b(read|write)File\b&patternType=regexp)). The regex pattern in this case could be interpreted as "read OR write followed by File, with a word boundary on either end."

#### Using spaces in regular expression patterns

It's common to be looking for a pattern with two keywords, separated by any other text in between.

When using regular expressions in Sourcegraph, the space character matches any characters between keywords. So if you search for two words in regular expressions mode, like `auth service`, you'll get results where `auth` and `service` are found on the same line, and any other number of characters (not limited to spaces) may be in between: [search on Sourcegraph](https://sourcegraph.com/search?q=auth+service+patternType%3Aregexp).

When you use spaces in regular expressions in Sourcegraph, the space character is automatically interpreted as replaced by the `.*` pattern. This pattern matches any number of characters on the same line (including none). When you're looking for two words appearing together in a code base, but not necessarily right next to each other, regular expression mode is a useful way to find relevant results.

### Structural Search

Structural search helps you search code for syntactical code patterns like function calls, arguments, `if...else` statements, and `try...catch` statements. It's useful for finding nested and recursive patterns as well as multi-line blocks of code. They're different from regular expressions because they take into account the syntax of code, like balanced brackets, quoted strings, and delimiters. 

To run a structural search, click the `[]` button in the search toolbar. Structural searches are limited to 30 lines of results by default. To return more results, add `count:all` or `count:100` (or any number) to your search.

#### Finding function calls

Suppose we're debugging a program's error output and trying to figure out where that output is coming from in the code. We want to find calls to the `fprintf` function that writes to the standard error stream (`stderr`), which look like this:

```
fprintf(stderr, "%s", message)
```

If we're looking only for error output, we want to match all other instances where `stderr` is the first argument of the call.

This is a situation where structural search can help, using the `context:global fprintf(stderr, ...) lang:c repo:^github\.com/torvalds/linux$ patternType:structural` query ([search on Sourcegraph](https://sourcegraph.com/search?q=fprintf(stderr%2C+...)+lang%3Ac+repo%3A^github\.com%2Ftorvalds%2Flinux%24+patternType%3Astructural)).

In this example, we're using a placeholder, `...`, for the remaining arguments. This ellipses placeholder is called a "hole" in the pattern. Structural search syntax uses "holes" as placeholders for syntactic structures. In this case, the placeholder will match the remaining function arguments.

#### Using multiple holes

You can use more than one `...` hole in a search. If we want to find an exact match for the second argument to `fprintf`, but accept any other arguments, we could use a hole in both the first and last argument position using this query: `context:global fprintf(..., "%s", ...) lang:c repo:^github\.com/torvalds/linux$ patternType:structural` ([search on Sourcegraph](https://sourcegraph.com/search?q=fprintf(...%2C+"%s"%2C+...)+lang%3Ac+repo%3A^github\.com%2Ftorvalds%2Flinux%24+patternType%3Astructural)).

The second argument to `fprintf` is expected to be a format string. In this above example, we'll find matches where the second argument matches the string `"%s"` exactly.

#### Finding blocks of code in brackets

Balanced bracket matching works with round brackets or parentheses, `()`; square brackets, `[]`; and curly brackets or braces, `{}`.

By using curly brackets in a structural search pattern, you can match entire code blocks.

Suppose that you're working on improving a Java codebase, and you want to clean up the code's `try...catch...finally` statements. In Java, an empty catch clause is allowed, but it often represents an opportunity to omit the clause entirely or to refactor it.

We can construct a structural search pattern to find empty catch clauses that can be improved. In this case, we'll use the hole placeholder inside of curly brackets to match code blocks, but we'll deliberately keep the `catch` clause empty in order to find only the empty blocks there.

To do that, we'll run the `context:global try {...} catch (...) { } finally {...} lang:java patternType:structural` query ([search on Sourcegraph](https://sourcegraph.com/search?q=context:global+try+{...}+catch+(...)+{+}+finally+{...}+lang:java&patternType=structural)).

### Conclusion

Sourcegraph allows you to search using literal search, regular expression search, and structural search. In our next unit, we'll discuss how to use those search results, save searches, export search results, and share them with your team. We'll also discuss dynamic search filters and how to change how the search results are grouped and displayed.

### Resources

- [Sourcegraph](https://sourcegraph.com)
- [Sourcegraph Search Documentation](https://docs.sourcegraph.com/code_search/reference/queries#search-pattern-syntax) 
- [Sourcegraph Documentation](https://docs.sourcegraph.com)
- [Three ways to search code with Sourcegraph](https://learn.sourcegraph.com/three-ways-to-search-code-with-sourcegraph)

### Quiz

1. What search methods does Sourcegraph support?
- A. Literal, regex, structural
- B. Structural, regex, smart
- C. Literal, smart, structural
- D. Literal, structural, smart

2. What would a literal search for `"foo bar"` return?
- A. Any exact matches for `foo bar`
- B. Any exact matches for `"foo bar"`
- C. Any match for `foo` and `bar` on the same line
- D. Nothing; it's an invalid query

3. How do you represent a structural hole in a structural query?
- A. `…`
- B. `[ ]`
- C. `{ }`
- D. A space character

Answers:

1. A
2. B
3. A

## Unit 4: Search results

[Video content](https://drive.google.com/file/d/1HpAej_2bj77xgbWuAWetr2d_1xaqiFEY/view?usp=sharing)

After completing this unit, you'll understand the search results page and how to export, save, and link to search results.

### An introduction to the search results

When you run a search in Sourcegraph, you'll see a list of search results:

![A screenshot of the Sourcegraph search results page. It shows a query for fizz buzz, along with previews of five files where fizz buzz is present as a string. On the left side of the page, there are options for Search Types, Dynamic Filters, Repositories, and Search Reference.](https://lh5.googleusercontent.com/9U7Hn9YIc_vBXqptsuPsgbiHLU9Q2TP-LLA-GCR601y0eD6-dGTXSlkLKhbwDMsEJ2rxPdckCrM7SiHHDacXqRPUFcXnWSUfBXuGt-tDwwrZ00nwPI8eejgPOMAscBQUEaMOMO5pIjXMSmeO7w)

As we discussed in Unit 2, the main area of the page will show your search results, with the matching text highlighted. By default, you'll see one line above and below your matching line, in order to provide some context on the search result. The number of lines shown can be customized in your user settings page, if you prefer. Above the search result, you'll see the repo name and the file path within the repo. If your match is for a file path or repo name, you'll see just a link to that repo or file, with no preview code. 

Clicking on the search results will allow you to view the search results in context; you'll be brought directly to the line you clicked on in the preview. 

### Saving your search to run again

If your search is one which you run frequently, you can save it so that you can quickly use the search again. You have two ways to do this: search contexts and search snippets.

#### Search contexts

Search contexts are a way to quickly search within a particular set of repos or files. If you're regularly searching within only your own team's repos, or only frontend or backend repos, search contexts are the way to do that! 

To save a search context, click the `global` icon next to your search query:

![A screenshot showing the drop-down menu of listed contexts for an instance, triggered by clicking "global" next to the drop-down. "Manage contexts" is linked at the bottom right, and "Reset" at the bottom left.](https://lh3.googleusercontent.com/OA5UU2SrOpOs3NkXwP-MyeX2ag1BANGBVxQaH52NecG01hC3Yh7t4JAVYvSs16NwWBr14s5msIhxAms3i9PbfarecM7W_3rUPN1ixKgQiE3pLMlSPKqB-iM8oV6eD81pXcPAywtdhknP727wIw)

To add your search context, click `Manage contexts` on the bottom right of that dropdown. Then, click `Create search context` at the top right of the screen. From there, you can configure your search context using a search query. You'll then be able to pick the context from the drop-down menu, and can filter your searches with that query going forward. 

#### Search snippets

Setting up a search snippet will create a one-click link on the bottom left of the search filter menu. This allows you to add query contents with one click. This is super useful if you're regularly wanting to add a combo of filters or text to other queries. 

To set up a snippet, click on your user icon on the top right of the page, and click `Settings` to bring you to your settings page. Then, you'll add `search.scopes` to your settings, like so: 


```
{
 // ...
 "search.scopes": [
  {
   "name": "fizz buzz",
   "value": "context:global fizz buzz patternType:literal"
  }
 ]
 // ...
}
```
Save your settings, and you'll now see the search scope on the bottom left of the filter menu on the search results page: 

![A list of search snippets from the left search menu, including "fizz buzz" at the top of the list.](https://lh3.googleusercontent.com/xPFjHbKzoHZe0rJ3kKoEElY2ehsgidjgfKeSWIkE2T35c6x-kQT5dpeXCz5UWFkuvVnWuBFT2iIVEibu3SOrcRtFffA00TtyyW891dvXC9pb0mceLnUsON47DxfeEM56Y1AkXeewt9JQ1eMXKA)

Click that scope to add it to your query.

### Exporting search results

To export your search results, you will need to enable the `search-export` extension if it's not already enabled for your instance. To do that, click on the extensions icon (a puzzle piece on the top of the page) to open the extensions page. Search for `search-export`, and click the `enabled for me` slider until it turns blue.

![A screenshot of the search-export extension tile, with the "Enabled for me" slider toggled to on/blue in the bottom right corner.](https://lh5.googleusercontent.com/Vn1zO_SKXkdS-Htm-emb87JHvLpkKpTR4iW_ON7lmFQv93kDdhmA9KDBW2BACtt6Rtd4kcrqdeLQ1Y1R6f8ypptMhJEny9Is3ctP4oMTVqT6Is8Crxo9llERsUXZ3CTgnbTBSD133hdyiwF7hw)

Once the extension is enabled, run a search. On the search results page, you'll see a link to export search results, below the search bar. Click that to export the results as a CSV. By default, the export will include only 30 results. To increase the number, add `count:all` to your query.

### Linking to your search results

Sourcegraph search results are meant to be shared! Whether sharing a link with a colleague to ask for more information on code they wrote, or using a link to facilitate pair programming, Sourcegraph is better when used together. To link to content in Sourcegraph, you can simply copy the URL in the browser bar and share it—that will link to the same page for anyone who has access to your Sourcegraph instance.

If you're looking at the main/master branch of a repo and want to ensure that you're linking to the exact commit SHA when sharing the file, you'll want to click the link icon in the top right of the screen, below the search bar. That will update the page URL to be a permalink, and you can copy that URL and share it with teammates.

### Dynamic search filters

Sourcegraph will suggest search filters for your query based on your search results. This is to help guide you to the appropriate results from a more general query. These Dynamic Filters will be displayed on the left side of the page when you run a search, and will suggest further queries to add based on the search results.

To use a Dynamic Filter, click on filter text. This will apply it to your search and adjust the results. For example, clicking on `lang:javascript` will narrow down the results of this search to only show JavaScript results.

![A Dynamic Filters list showing fork:yes, archived:yes, lang:javascript, lang:csv, and lang:text](https://lh4.googleusercontent.com/keOp8QJcprXj_m9OP6oPwlwI-XqONgN2o_S12wTVGEwYw6hLTk3-K8tUC53aRCTt7iba1qk2rfSRKOgUzpkTssz7uKAcHKWLgYeT19H2yVQGYRmJb17arjJrJBeehUEthijkIE1aatHeYU0fGA)

### Changing how the search results are grouped and displayed

Sourcegraph offers an important filter to group your results. If you search for `fizz buzz`, for example, you'll see all of the files, file names, and repos where `fizz buzz` appears. If you instead want to see all of the repos that contain the code that includes the string `fizz buzz`, you can do that with our `select:` filter. Adding `select:repo` will group the results by repo, and `select:file` will group them by file. This is super useful if you want to find all repos which contain a particular dependency, for example.

### Conclusion

With Sourcegraph, you're able to view search results, save those searches with search contexts and snippets, and export and share those search results with others. With dynamic search filters and the `select:` filter, you can narrow down your search to only the relevant content. Next up, we'll talk about our favorite search filters.

### Resources

- [Sourcegraph](https://sourcegraph.com)
- [Sourcegraph Search Documentation](https://docs.sourcegraph.com/code_search/reference/queries#search-pattern-syntax)
- [Exporting Search Results](https://sourcegraph.com/extensions/sourcegraph/search-export)
- [Sourcegraph Documentation](https://docs.sourcegraph.com)
- [Sourcegraph Search Context Documentation](https://docs.sourcegraph.com/code_search/how-to/search_contexts)

### Quiz

1. What are dynamic filters?
- A. Very fast filters
- B. Filters suggested by your instance admin
- C. Filters based on overall search trends
- D. Filters suggested based on your search results

2. How would you save a search for referring to in the future?
- A. Save it as a search context
- B. Save it as a search snippet
- C. Write down the query
- D. A and B

3. How would you most easily share your search results with a teammate?
- A. Copy the URL from Sourcegraph and send it to them
- B. Describe the file path to them so they can open it themselves
- C. Screenshot the results
- D. It's not possible

Answers:

1. D
2. D
3. A

## Unit 5: Basic search filters

[Video content](https://drive.google.com/file/d/1E804kGEmX7j_Aqj86uia09V0G6MZGu1b/view?usp=sharing)

After completing this unit, you'll be able to use Sourcegraph's most common search filters to structure a search query.

### Language (lang:) filter

The `lang:` filter allows you to narrow your search so that you only see results in a particular language. This can be particularly useful for filtering your results to a particular frontend or backend language, rather than the entire language stack available to you. 

To add the `lang:` filter, type `lang:` in your query. A dropdown list of suggestions will appear, and you can select your language and press tab to add that language filter to your query. Alternatively, you can manually type the filter and language manually, such as `lang:JavaScript`. The language filter requires that you type out the full language name, so `lang:mark` won't work, but `lang:markdown` will.

### Repository (repo:) filter

With the `repo:` filter, you can narrow search results to code in a particular repository or repositories of code. The `repo:` filter allows you to specify the repo path and allows for you to use a regex in the path, regardless of the search mode you're using. So, for example, `repo:.*/sourcegraph$` would find any repo named `sourcegraph`, no matter the code host it's stored on. The filter will handle substring matching by default, so searching `repo:sourcegraph` will find any repo with `sourcegraph` anywhere in its name. 

To use the `repo:` filter, you can either type it directly into your query, or use the list of repositories that are dynamically populated on the left side of the page after running an initial search.

### File & directory path (file:) filter

Oftentimes, it's useful to limit your search results to a particular file—say you only want results from a particular directory because that's where test files are stored, or only need to see a dependency in Dockerfiles, not elsewhere in the code. To narrow those results down, add `file:` to your query.

Similarly to our `repo:` filter, the `file:` filter will allow for substring matching by default. So searching for `file:test` will find code in files in a directory named `testing`, will find files named `testFile.tsx`, and will return results from a `test.go` file. You can use regular expressions to narrow down the results, such as `file:_test.go$` to only find `test.go` files, not files in a directory with `test` in its name.

### Fork (fork:) and archive (archive:) filter

By default, Sourcegraph excludes results from forked repos and archived repos. However, sometimes you want to pull in results from forked or archived repos. To do that, you can use the `fork:` filter and `archive:` filter. Both filters take `no`, `only`, or `yes` as values. `Fork:no` or `archive:no` excludes those repos (the default behavior), `fork:yes` or `archive:yes` includes results from those repos, and `fork:only` or `archive:only` includes results from only those repos.

### The content (content:) filter option

Sometimes, you'll want to look for content that interacts with Sourcegraph's search query language—for example, you're looking for the literal string `lang:` in your code! To handle that, use our `content:` filter, and wrap your query in quotes. So, for example, `content:"lang:"` will let you search for that string without issue.

### Exclusions vs inclusion

By default, our filters are inclusive—you're searching for code that *is* in a particular repo, file, language, etc. However, those filters support exclusive searches, too—you can search for code that's *not* in a particular repo, file, or language. To do that, add a minus sign or hyphen (`-`) in front of a query, such as `new auth provider -lang:go` to find the `new auth provider` string everywhere *except* in Golang files.

### Controlling the number of results (count:) and the timeout (timeout:)

In some cases, Sourcegraph will limit the number of search results it returns—most notably, Structural searches default to only returning 30 lines of matches, and if a query takes a very long time to return results, you may see Sourcegraph timeout on returning the full list of results. You may also want to limit the number of results you get back, if you are running a very large query where you only want to see 100 results before making your decision. To change the number of results being returned, use the `count:` filter. You can use `count:all` to return every single result before the search times out, or can provide a number. For example, `count:100` will show 100 results.

By default, Sourcegraph will timeout a search after 10 seconds—so if no results are returned by then, or only some results are, you may wind up with incomplete results. If you'd like to force a longer timeout interval, you can do so using the `timeout:` filter, such as by adding `timeout:30s` to the search for a 30 second timeout. This isn't typically necessary, but can be useful if you're running a resource-intensive query with lots of results.

### Conclusion

Sourcegraph allows you to search with a variety of filters. Among the most common are the language filter, repository filter, file/directory path filter, fork and archive filters, and content filter. Once you've mastered this, you're well on your way to mastering Sourcegraph search! 

### Resources

- [Sourcegraph](https://sourcegraph.com)
- [Sourcegraph Search Documentation](https://docs.sourcegraph.com/code_search/reference/queries#search-pattern-syntax) 
- [Sourcegraph Documentation](https://docs.sourcegraph.com)
- [Sourcegraph Search Cheat Sheet ](https://learn.sourcegraph.com/how-to-search-code-with-sourcegraph-a-cheat-sheet)

### Quiz

1. How would you search for the string `foo bar` in markdown files?
- A. `"foo bar" lang:md`
- B. `"foo bar" language:markdown`
- C. `foo bar lang:markdown`
- D. `"foo bar" language:markdown`

2. How would you search for Java files in a `test` directory?
- A. `lang:java file:test`
- B. `lang:java file:/test/`
- C. `lang:java path:test`
- D. `lang:j file:/test/`

3. How would you search for the string `lang:` in the `github.com/sourcegraph/sourcegraph` repo?
- A. `lang: repo:github.com/sourcegraph/sourcegraph$`
- B. `content:"lang:" repo:sourcegraph`
- C. `content:"lang:" repo:github.com/sourcegraph/sourcegraph$`
- D. `repo:sourcegraph lang:`

Answers:

1. C
2. B
3. C
