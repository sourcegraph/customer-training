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

🔎 The trainer should demonstrate:

* How to run a regex search
* How fuzzy matching works in regex search

Sourcegraph also offers a structural search, useful for multiline, syntax-aware searching. 

🔎 The trainer should demonstrate:

* How to run a structural search
* How the search is multiline
* How the search is syntax-aware around things like nested parens

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

## Unit 3: Introduction to filters

**Learning goall:** By the end of this unit, users should understand how to use our filter functionality.

### Dynamic filters

Sourcegraph provides filters to narrow down your search result. You'll see on the top left here that it's suggesting filters based on the results that were returned.

The trainer should show:

* Where dynamic filters are located
* How to apply a `lang:` filter from the dynamic filters, and what it does
* How to apply a `file` or `-file:` filter from the dynamic filters, and what it does
* The repositories listed under the dynamic filters, how they are listed (greatest to least number of results), and what happens when they're clicked on
* How to search a non-default branch once the `repo:` filter is applied

### Type filters

You can see here on the left of the scren, we have `find a symbol`, `search commit messages`, and `search diffs`. 

🔎 The trainer should show:

* What each of these searches does
* How to search for a specific symbol
* How to search for a specific term in a commit message
* How to search for changes to code, and why that's beneficial versus file history

### Conclusion

With our query filters, you can narrow things down to find just the content you need, based on the results that Sourcegraph is returning!

### Resources

- [Three ways to search code with Sourcegraph](https://learn.sourcegraph.com/three-ways-to-search-code-with-sourcegraph)
- [Sourcegraph code search cheat sheet](https://learn.sourcegraph.com/how-to-search-code-with-sourcegraph-a-cheat-sheet)

## Unit 4: Code intelligence

**Learning goals:** By the end of this unit, users will know how our code intelligence functionality works and how they can use it.

### Viewing code intelligence in a file

So, I mentioned earlier that we offer code intelligence functionality, and I want to show that to you now.

🔎 The trainer should select a search result to demonstrate code intelligence in. Preference should be given to a file with precise code intelligence, if enabled. They should show:

* How to find references to a symbol
* How to go to definition of a symbol

This code intelligence functionality is multi-repo, unlike in an IDE. If you have precise code intelligence enabled, that will provide you compiler-accurate `find references`/`go to definition` functionality.

### Conclusion 

Code intel allows you determine the downstream impacts of changes across repos, and for some languages you can have access to compiler-accurate code intelligence if enabled.

### Resources

- [Code intelligence docs](https://docs.sourcegraph.com/code_intelligence)

## Unit 5: Notebooks

**Learning goals:** After this unit, users will understand the functionality of Notebooks and how to use them to share information with colleagues. 

### What are notebooks?

Our notebooks functionality is inspired by Jupyter notebooks—it's a great way to share code with your colleagues. 

🔎 The trainer should open a notebook of their choice, and discuss:

* How to use notebooks in lieu of wiki documentation for  new developers
* Why having up-to-date searches embedded in that documentation is an improvmeent over current state
* Their favorite notebook use cases
* How to share a notebook with a colleague

### Creating notebooks

To create a notebook, go to the notebooks tab and click "create notebook."

🔎 The trainer should show:

* How to create a notebook
* What the individual blocks (markdown, code search, code reference, symbols) do
* How to upload a `.snb.md` file to create a notebook
* How to enable the Notepad feature, and what it does

### Conclusion

With notebooks, you can share code context and explanations with your teammates. The Notepad feature lets you build notebooks on the go.

### Resources 

* [Notebooks documentation](https://docs.sourcegraph.com/notebooks)

## Unit 6: Extensions

**Learning goals:** After this unit, users will understand how our extensions platform functions and that IDE extensions exist.

### Intro to the extensions page

The final thing we'll look at today is our Extensions platform. You can access that by clicking the puzzle icon at the top right here.

🔎 The trainer should show:

* How to access the Extensions page.

### Editor extensions 

We integrate with a variety of services here, a particularly important one is our Editors extensions.

🔎 The trainer should show:

* How to filter to just Editors extensions
* How to enable the appropriate extension for the IDE the customer is using
* Where the customer can see the appropriate config options for the extension (on the extension's own landing page)
* How the `open in editor` button works, and its limitations (requiring the code to be stored locally)

### VSCode extension

For VSCode users—and soon JetBrains users!—we have a more robust integration. With VSCode, you actually can do everythign we've seen so far directly in VSCode.

🔎 The trainer should show their VSCode window and share:

* How to run a search in VSCode
* The fact that this does not require the code to be stored locally

### Browser extension

The final thing I want to touch on is our browser extension, which you can see I have installed here.

🔎 The trainer should move back to the browser, and show:

* What the extension looks like when clicked
* How to point it to the customer's own Sourcegraph instance
* How to use the extension during code reivew
* How to install the extension ([Install page](https://docs.sourcegraph.com/integration/browser_extension)

### Conclusion

Our editors functionality lets you integrate with third-party tools, including your editor, for a seamless experience.

### Resources

* [VSCode extension](https://marketplace.visualstudio.com/items?itemName=sourcegraph.sourcegraph)
* [Editor plugins](https://docs.sourcegraph.com/integration/editor)
* [Integrations](https://docs.sourcegraph.com/integration)
* [Browser extension](https://docs.sourcegraph.com/integration/browser_extension)

## Closing thoughts

Thanks so much for staying with me through this training! Today we covered our basic search functionality, our search filters, how to search commit and code history, code intelligence, notebooks, and our extensions platform. This should set you up for success in using Sourcegraph—if you have any issues, please post in Slack or shoot an email to support@sourcegraph.com so we can help you out.
