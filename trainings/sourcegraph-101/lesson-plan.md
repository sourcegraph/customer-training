This represents a lesson plan formatted version of our [talk track](talk-track.md). This is likely most useful for customers in a train-the-trainer situation or experienced CEs who wish to build their own scripts based on overall goals of the webinar.

CEs who wish to see a walkthrough of the training can [view a recording in GDrive](https://drive.google.com/file/d/1emSuz6Q871OC2YOadcfkrUXfuopn6JCB/view?usp=sharing).

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
5. Improving code health - If you’re trying to change from an anti-pattern to a best practice, use Sourcegraph to see how much work there is to do across the entire codebase.

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

**Learning goal:** By the end of this unit, users should understand how to use our filter functionality.

### Dynamic filters

Sourcegraph provides filters to narrow down your search result. You'll see on the top left here that it's suggesting filters based on the results that were returned.

🔎 The trainer should show:

* Where dynamic filters are located
* How to apply a `lang:` filter from the dynamic filters, and what it does
* How to apply a `file` or `-file:` filter from the dynamic filters, and what it does
* The repositories listed under the dynamic filters, how they are listed (greatest to least number of results), and what happens when they're clicked on
* How to search a non-default branch once the `repo:` filter is applied

### Type filters

You can see here on the left of the screen, we have `find a symbol`, `search commit messages`, and `search diffs`. 

🔎 The trainer should show:

* What each of these searches does
* How to search for a specific symbol
* How to search for a specific term in a commit message
* How to search for changes to code, and why that's beneficial versus file history

### Saving searches

If your search is one which you run frequently, you can save it so that you can quickly use the search again. You have two ways to do this: search contexts and search snippets.

#### Search contexts

Search contexts are a way to quickly search within a particular set of repos or files. If you're regularly searching within only your own team's repos, or only frontend or backend repos, search contexts are the way to do that!

🔎 The trainer should show:

* How to configure a search context based on a query
* How to make the context private
* How to make the context shared to the entire instance

#### Search snippets

Setting up a search snippet will create a one-click link on the bottom left of the search filter menu. This allows you to add query contents with one click. This is super useful if you're regularly wanting to add a combo of filters or text to other queries.

🔎 The trainer should show:

* Using a search snippet that they have saved
* How to add a new search snippet for an individual user
* How to add a new search snippet for the entire instance


### Conclusion

With our query filters, you can narrow things down to find just the content you need, based on the results that Sourcegraph is returning!

### Resources

- [Three ways to search code with Sourcegraph](https://learn.sourcegraph.com/three-ways-to-search-code-with-sourcegraph)
- [Sourcegraph code search cheat sheet](https://learn.sourcegraph.com/how-to-search-code-with-sourcegraph-a-cheat-sheet)

## Unit 4: Code Monitoring

**Learning goals:** By the end of this unit, users will now how to configure a code monitor.

### Configuring a code monitor

Previously, you saw me run a `type:diff` search, in order to see changes to the code. If I want to be proactively informed about that search via email, Slack, or webhooks, that's possible too! To do so, I'll want to set up a code monitor.

🔎 The trainer should show:

* The example use cases on the "getting started" code monitor page
* Creating a new code monitor using "create copy of monitor" and applying a `repo:` filter
* The fact that monitors can be connected to email, Slack, or webhooks

❗️Typically, actually going through the entire Slack flow isn't necessary; instead, you can simply speak to it and share a recording afterwards if folks want more info. 

❗️If the customer is interested in email monitors, identify a point person to configure the SMTP connection on the instance; without that, it won't be possible to use them.

### Conclusion

Code monitors allow you to not only discover newly-committed code that matches a pattern or anti-pattern that you want to keep an eye on, but will proactively alert you to that code as it's added.

### Resources

* [Sourcegraph Code Monitoring documentation](https://docs.sourcegraph.com/code_monitoring)

## Unit 5: Code intelligence

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

## Unit 6: Notebooks

**Learning goals:** After this unit, users will understand the functionality of Notebooks and how to use them to share information with colleagues. 

### What are notebooks?

Our notebooks functionality is inspired by Jupyter notebooks—it's a great way to share code with your colleagues. 

🔎 The trainer should open a notebook of their choice, and discuss:

* How to use notebooks in lieu of wiki documentation for  new developers
* Why having up-to-date searches embedded in that documentation is an improvement over current state
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

## Unit 7: Integrations

**Learning goals:** After this unit, users will understand how to use code editor extensions, in-IDE extensions, browser extension, and search exports.

### Editor integrations 

We integrate with a variety of services here, a particularly important one is our Editors integrations.

🔎 The trainer should show:

* How to access `open-in-editor`
* Where the customer can see the appropriate config options for the feature
* How the `open in editor` button works, and its limitations (requiring the code to be stored locally)

### VSCode/JetBrains extension

For VSCode and JetBrains users, we have a more robust integration. With VSCode and JetBrains, you actually can do everything we've seen so far directly in VSCode.

🔎 The trainer should show their VSCode or JetBrains window and share:

* How to run a search in VSCode/JetBrains
* The fact that this does not require the code to be stored locally

❗️ If possible, pick whichever one is most used at the customer company.

### Search Exports

You may want to export the results of your search. To do that, use our search export feature.

🔎 The trainer should show:

* How to export a search
* What the exported CSV looks like

### Browser extension

The final thing I want to touch on is our browser extension, which you can see I have installed here.

🔎 The trainer should move back to the browser, and show:

* What the extension looks like when clicked
* How to point it to the customer's own Sourcegraph instance
* How to use the extension during code review
* How to install the extension ([Install page](https://docs.sourcegraph.com/integration/browser_extension))

### Conclusion

We integrate with your editor and your code host for a seamless experience, as well as allowing you to export search results. 

### Resources

* [VSCode extension](https://marketplace.visualstudio.com/items?itemName=sourcegraph.sourcegraph)
* [Editor plugins](https://docs.sourcegraph.com/integration/editor)
* [Integrations](https://docs.sourcegraph.com/integration)
* [Browser extension](https://docs.sourcegraph.com/integration/browser_extension)

## Unit 8 (Optional): Code Insights

**Learning goals:** After this unit, customers will understand what Code Insights is, how to create a Code Insight, and how to share a Code Insight.

### Intro to Code Insights

As a developer, I may want to track the progress of changes in my code—seeing what versions of a dependency we're using to ensure we're not using out-of-date libraries, tracking linter skips to ensure that we're not bypassing important best practices, or seeing if we're making progress on an internal initiative to ensure all repos have codeowners files. With Insights, I can easily make graphs out of my searches, and so in doing so can track these sorts of initiatives over time, and share them with my colleagues. If you can search it, you can see it!

❗️ This can be a good point to stop and ask what kind of initiatives the customer is tracking, or how they're accomplishing this sort of thing today. That can influence your talk track for what you then show them. 

🔎 The trainer should show:

* The Insights dashboard of their choosing (when in doubt, default to [[Overview] Popular Uses](https://demo.sourcegraph.com/insights/dashboards/ZGFzaGJvYXJkOnsiSWRUeXBlIjoiY3VzdG9tIiwiQXJnIjo3NDU0Nn0=))
* How to interpret the results of one of the graphs
* How to access the individual search results from the graphs by clicking in to a data point
* How to track versions using a `Detect and track patterns` Insight from the Insight creation page
* How to create a `Track changes` Insight from search results rather than the Insight creation page

❗️Typically actually creating an Insight isn't required—the key is for the user to come away understanding that Insights can be created from the Insights page or from search results.

### Conclusion

The Insights functionality can be a super powerful way to ensure that everyone at your organization can access the same understanding of what's going on in your code, from your code itself. Sharing Insights is a great way to ensure you're on the same page as your colleagues.

### Resources

* [Code Insights Documentation](https://docs.sourcegraph.com/code_insights)
* [Creating a Code Insight](https://docs.sourcegraph.com/code_insights/quickstart)
* [Creating a Version Tracking Insight](https://docs.sourcegraph.com/code_insights/explanations/automatically_generated_data_series)
* [Common Use Cases and Recipes](https://docs.sourcegraph.com/code_insights/references/common_use_cases)

## Unit 9 (Optional): Batch Changes

**Learning goals:** After this unit, customers will understand what Batch Changes is, how to create a Batch Change, and how to track the progress of a Batch Change.

### Intro to Batch Changes

As a developer, I may want to change something across many places in my code. For example, I might want to change insensitive language, or might want to apply a linter across multiple repos all at once. Or, I might want to easily bump a dependency version across all of my code, to ensure that I'm not impacted by a vulnerability. With Sourcegraph Batch Changes, it's easy to do this and to track progress.

Sourcegraph Batch Changes follow the following workflow:

1. I identify a Sourcegraph query that will find all the repos I want to modify
2. I script the change I want to make—this can be as simple as a quick find and replace using a bash script, or as complex as spinning up our build environment and pinning transitive dependencies 
3. Sourcegraph runs the batch change on those repos either locally or on the Sourcegraph instance
4. It opens PRs on my behalf, and I can comment on them, merge them, close them, or simply track their status in Sourcegraph.
5. I'm able to see progress on my change via a burndown chart in Sourcegraph, and am able to confidently answer questions about the progress of the change.

It's a huge force multiplier, particularly for teams working across multiple parts of your codebase, such as DevOps or Security teams.

🔎 The trainer should demonstrate:

* How to access the Batch Changes page
* How to open an in-progress Batch Change of the trainer's choice
* How to view the spec for that Batch Change
* What, at a high level, the parts of the spec are doing (defining the repo list, making the change, determining PR contents, etc.)
* How to run a Batch Change in the browser (recommend the [Hello World](https://docs.sourcegraph.com/batch_changes/quickstart#write-a-batch-spec) Batch Change)
* How to filter PRs by status, check state, and review state
* What bulk actions (publishing, commenting, merging, closing) are available
* What the burndown chart looks like and how to filter the burndown chart


❗️ You may wish to use [this batch change](https://demo.sourcegraph.com/users/malo/batch-changes/medium-trackin-campaign) to show dashboard filtering and the burndown chart, while using another to explain the spec format.

❗️ It may be worth emphasizing to the customer that Sourcegraph search is used to find the associated repos, but does not limit what actions they can take—those are essentially limited only by what can be scripted by the end user.

❗️ This is writen to have the trainer run the Batch Change in the browser rather than the CLI; the CE can swap to the CLI if preferred or indicated in some way, but browser/SSBC is recommended here for speed.

### Conclusion

With Batch Changes, I can make a huge impact in my codebase for things as small as a version bump to things as large as a significant refactor, and I have a live-updating dashboard to track how that progress is going. No more spreadsheets and wrangling folks in Slack to coordinate work!

### Resources

* [Batch Changes documentation](https://docs.sourcegraph.com/batch_changes)
* [Batch Changes examples repo](https://github.com/sourcegraph/batch-change-examples)
* [Batch Changes FAQ](https://docs.sourcegraph.com/batch_changes/references/faq)
* [Batch Changes Quickstart](https://docs.sourcegraph.com/batch_changes/quickstart#write-a-batch-spec)

## Closing thoughts

Thanks so much for staying with me through this training! Today we covered our basic search functionality, our search filters, how to search commit and code history, code intelligence, notebooks, and our extensions platform. This should set you up for success in using Sourcegraph—if you have any issues, please post in Slack or shoot an email to support@sourcegraph.com so we can help you out.
