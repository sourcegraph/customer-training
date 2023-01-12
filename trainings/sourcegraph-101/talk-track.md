This training is a talk track covering our Sourcegraph 101 material. More senior CEs may prefer the [lesson plan format](lesson-plan.md), instead.

# Sourcegraph 101

**Topic:** This training is focused on end users, and serves as a start-from-zero training for new end users. Admin tasks and more advanced search functionality are covered in other trainings. The training is broken into 5 units, but you don't need to call the units out to the customer—they serve more as a way to structure the training for yourself. 

## Intro

Hi! Today I'm going to be walking you through what we call Sourcegraph 101—it should take you from 0 to being able to use Sourcegraph confidently. We of course don't have time for a dive into all of what Sourcegraph can do today, so we'll be running a Sourcegraph 102 training in our next session to talk about advanced features. That said, throughout today, please ask questions! You can take yourself off mute or drop it into the chat, and my colleague will read them out for us when we come to a pause. Even if I can't answer the question today, I'll connect you to someone who can.

Today we'll walk through what Sourcegraph is, our search options, our search filters, our code intelligence functionality, and our notebook functionality. By the end, you should be comfortable using all of those features!

## Unit 1: Get familiar with Sourcegraph

**Learning goals:** After completing this unit, customers will understand what Sourcegraph is and what it does, understand its 5 most common use cases, and learn a little more about how other companies use Sourcegraph.

*Unit 1 will typically accompany an intro deck. If your customer is already generally quite familiar with what Sourcegraph is, deliver an abbreviated version of Unit 1 and move on to Unit 2.*

### What is Sourcegraph?

Sourcegraph is a code search engine that runs in the browser, as well as being available via a CLI or (for some editors) directly in your IDE. Today, we’ll focus on the browser, but after this training I will share info on the CLI and the IDE extensions for you to explore.

With Sourcegraph, you can use literal, regular expression, or structurally aware searches and search filters to find information across your company’s entire source code. Unlike using grep or searching locally in your editor, Sourcegraph allows you to see all of your company’s code, regardless of what you have available locally. 

In addition to allowing you to search for your code, Sourcegraph provides additional functionality, such as code intelligence (“find references” and “go to definition” as you’d see in a local editor, available for all of your code); you can also do advanced searches such as searching commit messages, searching changes to your code, searching non-default branches, and searching symbols in your code. In this module, we’ll cover basic searches, and in our Sourcegraph 102 training, you’ll learn more advanced search techniques.

### What are common use cases for Sourcegraph?

Typically, developers use Sourcegraph for [five key use cases](https://about.sourcegraph.com/use-cases/): 

1. Finding and fixing security vulnerabilities - If a CVE is announced, easily find if your code uses an impacted version of a dependency.
2. Accelerating developer onboarding for new team members - Allow new developers to answer their own questions by being able to search *all* code, rather than having to guess-and-check where the code they need is located.
3. Resolving incidents faster - Easily search recent changes to the code to find what might have caused the issue.
4. Streamlining code reuse - Surfacing code via search means it’s easier to avoid reinventing existing code, leading to more consistent, efficient coding practices.
5. Improving code health - If you’re trying to change from an anti-pattern to a best practice, use Sourcegraph to see how much work there is to do across the entire codebase.

While we're working together today, think about which of these use cases is most relevant to your day to day work. That will help you conceive of how Sourcegraph might be most relevant to your particular needs, so that you can get the most out of the tool.

### Conclusion

Sourcegraph is a code search and intelligence platform that allows you to find all of your company’s code in the browser in order to make your work easier and more efficient. Next up, we’ll dive in to the tool to learn how to search in Sourcegraph.

### Resources

*Share these with the customer after the call, typically in Slack.*

* [Follow-up Slack template](./slack-follow-up.md)

- [Sourcegraph](https://sourcegraph.com)
- [Sourcegraph Documentation](https://docs.sourcegraph.com)
- [Sourcegraph Use Cases](https://about.sourcegraph.com/use-cases)
- [Sourcegraph Customer Case Studies](https://about.sourcegraph.com/case-studies)

## Unit 2: Navigating the Sourcegraph UI

**Learning goal:** After completing this unit, you’ll be able to navigate the Sourcegraph home page, understand the search mode buttons, and be able to navigate the search results page. 

### The Sourcegraph home page

*At this point the Trainer should share demo.sourcegraph.com*

As you can see here, Sourcegraph is primarily a browser application. I'm using my own Sourcegraph instance, but you'll be using yours—we'll drop the URL in the Zoom chat.

*Drop the URL in the Zoom chat, or have your champion do so.*

The main focus of the home page is the search bar. By default, you’ll see context:global is selected. This means that you will search all of your company’s code to which you have access. You can change that by setting up search contexts—we’ll talk about how to do that a little later.

To run a search, type your query into the search bar, similar to searching on GitHub, GitLab, or Google. Press enter or click the search button to start your search and to navigate to the search results page. I'm going to search for `new auth provider` here.

*Run the literal search.*

By default, your search will be run as a literal search (exact match), and will be run case-insensitively. You can see here that I'm only getting exact matches. **You don’t need to add quotes for exact matches!** Quotes will be interpreted literally, so you can see if I add them here that's reflected in my search results.

*Add quotes, rerun the search.*

So if I take them back out, you can see that what I'm seeing is exact matches already.

*Take them back out, rerun it again.*

### The search mode buttons

In addition to our default literal, or exact match, search mode, Sourcegraph offers two other search modes: regular expression, and structural search. To run a search in either of these modes, you’ll use the appropriate icons in the search bar, on the right-hand side of the bar, next to the search button. 

To run your search using [RE2 regex syntax](https://github.com/google/re2/wiki/Syntax), click the .* icon before running your search. If you click that icon after running your search, your search will re-run as a regex search. In regular expression searches, space characters are handled as fuzzy matches. So you see here that if I run that `new auth provider` search as a regex, I'm now getting matches for `new authz provider`, `newOAuthProvider`, etc. I can also enforce word boundaries, so if I run a search for `new \bauth\b provider`, I'm only going to see results where auth is not a substring.

*Search for `context:global new \bauth\b provider patternType:regexp`, show the results*

The final search mode option is our language-aware structural search option, represented by the square bracket button `[]`. When selected, you’ll have the option to include structural holes, represented by `…` or `:[a]` in your query, to run multi-line fuzzy searches. 

*Search for `context:global lang:JavaScript class ... extends ... {...} count:all patternType:structural`, show the results*

So, for example, if I search for `context:global lang:JavaScript class ... extends ... {...} count:all patternType:structural`, I get a really wide variety of results that match that pattern. Something to call out is that structural search mode is smart enough to match nested characters—so you can see it won't prematurely close on the first closing curly brace it sees; instead, it will wait until it finds the matching one.

I'm going to pause here: are there any questions about our three search modes, or do folks have use cases that jump to mind for any of them?

*Pause, leave space for questions, get a drink of water*

### The search results page

Awesome! So, let's chat through what you'll see when you run the search. When you run your search, you will be redirected to a search results page. It will look something like this:

*run the `context:global new auth provider patternType:regexp` search again*

The main area of the page will show your search results, with the matching text highlighted. By default, you’ll see one line above and below your matching line, in order to provide some context on the search result. The number of lines shown can be customized in your user settings page, if you prefer. Above the search result, you’ll see the repo name and the file path within the repo. If your match is for a file path or repo name, you’ll see just a link to that repo or file, with no preview code.

On the right-hand side of the page, you’ll see options to run different kinds of searches, filter your search results dynamically, or manually filter your searches by repository, language, and other search filters. We'll dive into those later in the training.

Clicking on your search results will open the matching code, file, or repo in Sourcegraph. From there, you can view the full file and navigate to other files in the same repo, or run a new search.

### Conclusion

Sourcegraph offers three search modes (literal, regex, and structural) controlled by buttons in the search toolbar. In our next units, we’ll learn more about those search modes and filters to narrow down your search results. 

### Resources

- [Sourcegraph](https://sourcegraph.com)
- [Sourcegraph Documentation](https://docs.sourcegraph.com)

## Unit 3: Introduction to filters

**Learning goal:** By the end of this unit, users should understand how to use our filter functionality.

### Dynamic filters

So as I mentioned, Sourcegraph provides filters to narrow down your search result. You'll see on the top left here that it's suggesting filters based on the results that were returned—so in this case, I can narrow down to just Golang files by clicking this `lang:go` option.

*Click the `lang:go` filter.*

If I prefer, of course, I can type that filter in as well. 

*Type in the `lang:` filter, show the autocomplete language options.*

It's also suggesting I exclude test code—often super useful if you just want to look at application code. So if I click this `-file:_test.go$` button...

*Click the button*

you can see that I'm not only seeing code where the file path does not end in `test.go`. Most of our filters work this way: you can negate by adding a negative sign in front of them. I also want to make sure that folks know this `file:` filter exists to limit results to certain file paths—super useful if you want to just search in a Dockerfile, for example. 

The final filter I want to highlight here is this list of repositories. These results are showing what repos your code is in, ordered by most to fewest results. If I click on `github.com/sourcegraph/sourcegraph` here, you'll see that I'm narrowed down to just the main Sourcegraph monorepo.

*Click on the filter*

Something to highlight is that our repo filter, like most of our filters, automatically supports partial matching—so if I search `repo:sourcegraph`, I'll see matches from all of the repos in the Sourcegraph org. 

*Delete the first repo filter, run the `repo:sourcegraph` search, highlight the repos that are now being returned*

But to go back to the monorepo filter...

*Go back to the `repo:github.com/sourcegraph/sourcegraph$` filter*

...you'll see here on the side that it's now suggesting other branches and tags I could search. We're looking at the default `main`/`master` branch usually, but if I want to check out the code on an old version or a `develop` branch for example, I just click here to do that.

*Click on one of them, highlight it in the query syntax in the search bar*

Does anyone here ever have to look at staging branches or feature branches?

*Wait for responses, discuss with the users whatever they say. If they say nothing, you can say something like, "we use this all the time at Sourcegraph to look at the code in previous versions of the product, since not all of our users upgrade their instances immediately!"*

Our full search syntax is available over in this box—you can see common filters or the full list. And, as noted in this final box, we support Boolean operators, so you can add an `AND`, `OR`, or `NOT` into your query to combine different aspects of the query. 

*Show them the box where these options exist.*

This will allow you to build your own queries beyond what's suggested by dynamic filters. 

### Type filters

Next, I wanted to briefly cover our `type:` filter. We'll cover this in more detail in Sourcegraph 102. You can see here on the top left we have "find a symbol", "search commit messages", and "search diffs". I will quickly show how those work.

So, with my  `new auth provider` search here, if I click "find a symbol", it will append `type:symbol`. 

*Do this.*

You can see that I'm now seeing functions, variables, etc. that match this pattern—so if I'm looking for a specific symbol, this is how I'd do that!

Now, if I wanted to search the history of the code—say I want to go beyond the history for the file, because the code has moved between files—I can use this `type:diff` filter. So if I search for `new auth provider repo:sourcegraph/sourcegraph$ type:diff`, I can now see every time that code was changed in the codebase, no matter where in the repo it was.

*Run the search.*

Finally, I want to highlight how you can search commit messages. Say that I'm a new Sourcegraph dev and I want to look for info about `gitserver`, one of our app components. If I search for `gitserver repo:sourcegraph/sourcegraph$ type:commit`, I'm now able to look at all the commit messages where we talk about gitserver!

*Run the search.*

We'll dive more into how to use these `type:` filters in Sourcegraph 102, but I wanted to call your attention to them!

### Saving searches

Finally, I wanted to talk about how to save your searches so you can refer to them again. You have two ways to do this: search contexts and search snippets.

#### Search contexts

Search contexts are a way to quickly search within a particular set of repos or files. If you're regularly searching within only your own team's repos, or only frontend or backend repos, search contexts are the way to do that!

To do this, I'm going to click on `context:global` in my query, and click on `Manage contexts`.

*Click on `Manage contexts`*

From there, I can click `Create search context` on the top right of the screen. 

*Click on `Create search context`*

From here, I can scope the context to either just my username—in which case it will be private to just me—or set a Global owner. That will mean everyone has access to that context. In this case, I'm going to make this a private context. 

You can see here that I have the option to configure this via JSON or via a search query. I'm going to set this up via a search query. Say that I want a search query that only look at Sourcegraph repos, which are all in the `sourcegraph` org in Github. So, what I can do here is set a query for `repo:github.com/sourcegraph`. That will catch all those repos! 

*Set `repo:github.com/sourcegraph` in the search context menu and save it*

You'll see now that if I just want to look at the Sourcegraph org code, it's as easy as selecting that from the drop-down menu here.

*Run a search in that new search context*

#### Search snippets

Alternatively, I can set up a search snippet. Setting up a search snippet will create a one-click link on the bottom left of the search filter menu. This allows you to add query contents with one click. This is super useful if you're regularly wanting to add a combo of filters or text to other queries.

To set up a snippet, click on your user icon on the top right of the page, and click `Settings` to bring you to your settings page. Then, you'll add `search.scopes` to your settings, like so:

*Set up a new search scope. Something such as:*

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

*should work*

If I set this up in my own settings, it will just be a snippet for me. If I'm an admin and set this up in global settings, it will be a snippet for everyone on the instance. 

*Navigate to the search screen*

You can see here now that I can click on `fizz buzz` in the search snippets, and it will append that snippet right to the query I'm running. 

### Conclusion

With our query filters, you can narrow things down to find just the content you need, based on the results that Sourcegraph is returning!

### Resources

- [Three ways to search code with Sourcegraph](https://learn.sourcegraph.com/three-ways-to-search-code-with-sourcegraph)
- [Sourcegraph code search cheat sheet](https://learn.sourcegraph.com/how-to-search-code-with-sourcegraph-a-cheat-sheet)

## Unit 4: Code Monitoring

**Learning goals:** By the end of this unit, users will now how to configure a code monitor.

### Configuring a code monitor

Previously, you saw me run a `type:diff` search, in order to see changes to the code. If I want to be proactively informed about that search via email, Slack, or webhooks, that's possible too! To do so, I'll want to set up a code monitor. 

To start, I'll go to our code monitor page.

*Navigate to the code monitor page and navigate to the Getting Started tab if not already there.*

I wanted to highlight the content on this Getting Started tab here. We've got several example code monitors here that you can auto-copy, if you want to use those as a jumping-off point. So, if I click `Create copy of monitor` on this `Bad coding patterns` example, you can see that it's auto-populated that query.

*Click the `Create copy of monitor` link*

I'll want to add the appropriate `repo:` filter here if I don't want to look over all repos, or if I leave it as-is, it will look over all repos on the instance. 

From here, I can pick what I want it to do: I can have it send me an email every time there's a new hit, send me a Slack message, or post to an arbitrary webhook that I specify. 

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

*Click in to a file of your choice, and find a symbol to hover on.*

So you can see here that I clicked into one of my search results, and I can now see the source code. What I'm also seeing here is this hover tool tip, which has what we call code intelligence. By default we'll ship with search-based code intelligence; for some languages, we also offer what we call precise code intelligence, which is compiler-accurate. 

* **Note:** If you know they've set up precise code intel or will, speak to that. If you're not sure, you can use this space to ask what languages they're working in in order to see if there's any that are a good fit. This section will necessarily require some customization based on what you know about the customer.*

Something to call out here is that when I click `find references` to find places where this symbol is used, or `go to definition` to find where it's defined, that functionality works cross-repo. So, you should be able to see those results no matter where in the code the symbol is being used, allowing you to really track the downstream impact of changes. 

***Note:** Typically at this point it's worth calling out any limitations of code intelligence for the customer's languages if known—challenging accuracy for Ruby or Python, for example.*

I want to pause here and see if anyone has questions about how the code intel functionality works, or wants to share something that comes to mind about how this could be useful for them!

### Conclusion 

Code intel allows you determine the downstream impacts of changes across repos, and for some languages you can have access to compiler-accurate code intelligence if enabled.

### Resources

- [Code intelligence docs](https://docs.sourcegraph.com/code_intelligence)

## Unit 6: Notebooks

**Learning goals:** After this unit, users will understand the functionality of Notebooks and how to use them to share information with colleagues. 

### What are notebooks?

Our notebooks functionality is inspired by Jupyter notebooks—it's a great way to share code with your colleagues. 

*Open up a notebook. Up to you what you want to use, but this one on [Actor propagation](https://demo.sourcegraph.com/notebooks/Tm90ZWJvb2s6Nzg=) is a nice one if you don't have a go-to. Modify the talk track if you pick a different demo, but hit the same general points.*

### What do you use notebooks for?

So you can see here that we're sharing information about the code—in this case we're talking about how we handle something in the Sourcegraph codebase. As a new developer, I can be given this notebook to educate myself, and read what my colleagues have said. And, as you can see, I can click "run all blocks" and these searches will all run inline. 

For a lot of our customers, this replaces typed-out documentation that lives in a wiki tool like Confluence. Since the examples run live, you're not going to have out-of-date references here—devs can always see where you're using a particular pattern in the codebase today. 

As I scroll down here, you can see that we're actually highlighting some parts of the code as it existed at a specific time in the codebase (in this case, symbol definitions). Our devs have written out info about why they're structured this way, and gotchas about using them. Now if a teammate has a question, they can send this along as a first step in allowing folks to answer their own questions.

### Creating notebooks

To create a notebook, go to the notebooks tab and click "create notebook."

*Show that.*

From there, you're able to create markdown blocks, code search blocks, code reference blocks, or symbol blocks. If you prefer, you can upload the notebook as a fully built-out markdown file and we'll convert it.

You can also enable the Notepad feature by clicking "enable Notepad" up here in the top right of the screen.

*Show that.*

That will allow you to create a new note snippet from your searches. So you can see that if I search for `context:global new auth provider repo:sourcegraph patternType:regexp`, it prompts me to add that search to my notepad. I can then convert the notepad to a notebook.

I want to pause here—do folks have questions about creating notebooks? Can anyone share a situation where they might use the notebooks feature?

### Conclusion

With notebooks, you can share code context and explanations with your teammates. The Notepad feature lets you build notebooks on the go.

### Resources 

* [Notebooks documentation](https://docs.sourcegraph.com/notebooks)

## Unit 7: Extensions

_~~Deprecated.~~ Retained herein to provide historical context should a customer refer to it._

**Learning goals:** After this unit, users will understand how our extensions platform functions and that IDE extensions exist.

### Intro to the extensions page

The final thing that I want to touch on is our extensions platform. You can access that by clicking the puzzle icon at the top right here.

*Navigate to the ~~[Sourcegraph extensions](https://demo.sourcegraph.com/extensions) page*

### Editor extensions 

We integrate with a variety of services here, but the one I particularly want to draw your attention to is this "code editors" section. If you click into that, you'll see a list of supported editors and a generic "open in editor" extension. 

*Navigate to ~~`https://demo.sourcegraph.com/extensions?category=Code+editors`*

You'll want to enable the appropriate extension for your editor, and then click on the extension name to view the customization settings you'll need to configure. 

*Go to ~~`https://demo.sourcegraph.com/extensions/sourcegraph/open-in-editor`~~ and highlight the different config options on that page.*

This does rely on having the code locally on your machine—but if you do, you'll have an "open in editor" button in Sourcegraph to open the file locally. And if you want to navigate from your editor back into Sourcegraph, you can do so with the extensions here.

*Open `https://docs.sourcegraph.com/integration/editor`*

We'll share this link with you after the presentation so you can install the right extension for you. You'll just need to point it at your Sourcegraph instance in your settings. 

### VSCode extension

For VSCode users—and soon JetBrains users!—we have a more robust integration. With VSCode, you actually can do everything we've seen so far directly in VSCode.

*Share VSCode, open the Sourcegraph extension, run a search*

So as you can see here, I'm able to search all of the same code that's on my Sourcegraph instance, no matter what's cloned locally. Everything you can search for in Sourcegraph, across all your code hosts, can now be searched right in VSCode without needing to clone it. We really encourage VSCode users to install this extension, since it gives you all of Sourcegraph's search power right in the environment you're already using.

### Browser extension

The final thing I want to touch on is our browser extension, which you can see I have installed here.

*Share browser, show the extension button, click it.*

Remember the code intelligence functionality that we saw earlier? If I have this set up and pointing to my Sourcegraph instance, I have the ability to get that same functionality in my code host, which is *super* useful for code review. So, if I open a page in Sourcegraph, I can go to GitHub in our case.

*Jump from whatever Sourcegraph page you were on into GitHub. Ideally, use one from the Sourcegraph monorepo.*

And now if I hover over any of the symbols, I get access to that same code intelligence functionality and navigation. Super helpful for code review!

To install the extension, you'll want to go to this page. We'll share that in our follow-up email.

*Show them `https://docs.sourcegraph.com/integration/browser_extension`*

### Conclusion

Our editors functionality lets you integrate with third-party tools, including your editor, for a seamless experience.

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

To start, I'm going to show an example dashboard of Code Insights on our instance.

_Open [[Overview] Popular Uses](https://demo.sourcegraph.com/insights/dashboards/ZGFzaGJvYXJkOnsiSWRUeXBlIjoiY3VzdG9tIiwiQXJnIjo3NDU0Nn0=)) on Demo_

As you'll see here, we've got a variety of graphs showing. These graphs sit on the back of our search functionality—they show the number of search results for a particular query at a point in time, and then graph the results. If I want to explore an Insight in-depth, I can click on its name.

_Navigate to [Repos with README files](https://demo.sourcegraph.com/insights/insight/aW5zaWdodF92aWV3OiJzZWFyY2hJbnNpZ2h0cy5pbnNpZ2h0LnJlcG9zV2l0aFJlYWRtZUZpbGVzLXVzZXItMTgi)_

So in this case, I'm tracking which repos have README files, and of those, which are populated. This can be super helpful if I'm trying to encourage README use! 

_Click into a data point._

As you can see, when I click in here, this is running on top of this particular search query. This is tracking the changes between the previous data point and the one I clicked on. 

_Explain the specific search query you clicked on._

As a result of having Insights available, it becomes trivially easy for me to track this info and share it with my teammates and other stakeholders who are interested in the outcome—and once I set it up, I don't have to do anything, the graph will auto-update. 

_Navigate back to the Insights dashboard you were using._

So, if I want to create my own, I can click on `Create Insight` in the top right of the page. You'll see we have three types of Insights—`Track Changes` tracks number of occurrences of a search over time, `Detect and track patterns` does the same but allows you to use a regex capture group as a placeholder, and language insights will generate a snapshot-in-time view of the language breakdown of your code. If I click into `Detect and track patterns` here, you'll see that I can create a new Insight. 

_Show the Insight creation form that link opens up._

With `Detect and Track Patterns`, like I mentioned earlier, you can use a regex capture group, `(.*)`, to indicate where the variable is that the graph should split on. This is most useful for tracking versions—I don't want to have to hand-pick every possible version; this will auto-detect them and build the appropriate graph automatically. Super useful for security teams!

However, I can also create Insights directly from search results. 

_Run a search._

You'll see on the top right of the results page here that I can click `Create Insight`. If I do that, it will open up the Insight creation flow directly. Either way works!

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

As a developer, I may want to change something across many places in my code. For example, I might want to change insensitive language, or might want to apply a linter across multiple repos all at once. Or, I might want to easily bump a dependency version across all of my code, to ensure that I'm not impacted by a vulnerability. With Sourcegraph Batch Changes, it's easy to do this and to track progress. So, to check this out, I'm going to open the Batch Changes page. 

*Open Batch Changes page.*

So, to show how this works, I'm going to open up a Batch Change here. 

*Open [this batch change](https://demo.sourcegraph.com/users/christine/batch-changes/java-remove-catch?visible=7) and navigate to the spec.*

Batch Changes are controlled by what we call a Batch Change spec, which is YAML that outlines what repos I want to make changes to, and what change will be made. Sourcegraph Batch Changes follow the following workflow:

1. I identify a Sourcegraph query that will find all the repos I want to modify—you can see that at the top of the spec here.
2. I script the change I want to make—this can be as simple as a quick find and replace using a bash script, or as complex as spinning up our build environment and pinning transitive dependencies 
3. Sourcegraph runs the batch change on those repos either locally or on the Sourcegraph instance
4. It opens PRs on my behalf, and I can comment on them, merge them, close them, or simply track their status in Sourcegraph.
5. I'm able to see progress on my change via a burndown chart in Sourcegraph, and am able to confidently answer questions about the progress of the change.

So, if I navigate to the open changeset page, I can see the PRs for this batch change.

*Navigate to the PR tab.*

If I click into the individual PR, I can even see a summary of what the change itself was.

*Click to expand the diff.*

To quickly show you what the process of creating a batch change looks like, I'm going to run an [example batch change](https://docs.sourcegraph.com/batch_changes/quickstart#write-a-batch-spec). I'm going to be running this in the browser, but you can also run this from our CLI—I'm happy to dive into details offline if you want more info.

_Open the [Create batch change](https://demo.sourcegraph.com/batch-changes/create) menu_

This batch change appends `hello world` to `readme.md` files. I can run this in the browser, and if I click `Preview workspaces`, it will show me matching repos. I'm going to go ahead and run the change, and if I click in to the repo name, you'll see it's tracking what it's changing.

_Click in to the repo name to show the changes._

Now if I click `Preview` here, it will publish it to Sourcegraph, but not the code host—to do that, I'd click that `Apply` button here. However, I'm going to leave this batch change unpublished, and show you an already-created batch change from our own code base.

*Open [this batch change](https://demo.sourcegraph.com/users/malo/batch-changes/medium-trackin-campaign).*

As you can see here, we've got a variety of PRs in different states here. I can filter by PR status, review status, and check status.

*Filter to show only Open PRs.*

From here, I can select the changesets, and take bulk actions on them.

*Use the bulk select checkbox to select the PRs, and click on the dropdown arrow to show all of the bulk actions.*

I can bulk merge these, comment on them to nudge reviewers or provide context, and bulk close them if I decide not to go forward with this. If I decide I want to close the entire Batch Change, I can do that too, and auto-close the associated PRs.

If I want to track progress, I can do that using the burndown chart for this Batch Change.

*Navigate to the burndown chart.*

As you can see, merged PRs are dominating, so I'm going to filter those out.

*Uncheck the merged PR box.*

And with this I can now see a burndown chart of PR status throughout the period that this has been running for everything that hasn't been merged. If a teammate or my manager wants an update on the initiative, it's very easy to provide that to them—I can share or screenshot this chart, and we're very quickly all on the same page.

❗️ It may be worth emphasizing to the customer that Sourcegraph search is used to find the associated repos, but does not limit what actions they can take—those are essentially limited only by what can be scripted by the end user.

### Conclusion

With Batch Changes, I can make a huge impact in my codebase for things as small as a version bump to things as large as a significant refactor, and I have a live-updating dashboard to track how that progress is going. No more spreadsheets and wrangling folks in Slack to coordinate work!

### Resources

* [Batch Changes documentation](https://docs.sourcegraph.com/batch_changes)
* [Batch Changes examples repo](https://github.com/sourcegraph/batch-change-examples)
* [Batch Changes FAQ](https://docs.sourcegraph.com/batch_changes/references/faq)
* [Batch Changes Quickstart](https://docs.sourcegraph.com/batch_changes/quickstart#write-a-batch-spec)

## Closing thoughts

Thanks so much for staying with me through this training! Today we covered our basic search functionality, our search filters, how to search commit and code history, code intelligence, notebooks, and our extensions platform. This should set you up for success in using Sourcegraph—if you have any issues, please post in Slack or shoot an email to support@sourcegraph.com so we can help you out.

I want to pause here for questions—we can dive into anything you want. 

*If there are questions, answer them. If not, kick it back to the AE.*
