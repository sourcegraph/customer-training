# Sourcegraph 101

**Topic:** This training is focused on end users, and serves as a start-from-zero training for new end users. Admin tasks and more advanced search functionality are covered in other trainings. The training is broken into 5 units, but you don't need to call the units out to the customer—they serve more as a way to structure the training for yourself.

## Unit 1: Get familiar with Sourcegraph

**Learning goals:** After completing this unit, customers will understand what Sourcegraph is and what it does, understand its 5 most common use cases, and learn a little more about how other companies use Sourcegraph.

*Unit 1 will typically accompany an intro deck. If your customer is already generally quite familiar with what Sourcegraph is, deliver an abbreviated version of Unit 1 and move on to Unit 2.*

### What is Sourcegraph?

Sourcegraph is a code search engine that runs in the browser, as well as being available via a CLI or (in some editors) in your editor. Today, we’ll focus on the browser, but after this training I will share info on the CLI and the IDE extensions for you to explore.

With Sourcegraph, you can use literal, regular expression, or structurally aware searches and search filters to find information across your company’s entire source code. Unlike using grep or searching locally in your editor, Sourcegraph allows you to see all of your company’s code, regardless of what you have available locally. 

In addition to allowing you to search for your code, Sourcegraph provides additional functionality, such as code intelligence (“find references” and “go to def” like you’d see in a local editor, available for all of your code); you can also do advanced searches such as searching commit messages, searching changes to your code, searching non-default branches, and searching symbols in your code. In this module, we’ll cover basic searches, and in our Sourcegraph 102 training, you’ll learn more advanced search techniques.

### What are common use cases for Sourcegraph?

Typically, developers use Sourcegraph for [five key use cases](https://about.sourcegraph.com/use-cases/): 

1. Finding and fixing security vulnerabilities - If a CVE is announced, easily find if your code uses an impacted version of a dependency.
2. Accelerating developer onboarding for new team members - Allow new developers to answer their own questions by being able to search *all* code, rather than having to guess-and-check where the code they need is located.
3. Resolving incidents faster - Easily search recent changes to the code to find what might have caused the issue.
4. Streamlining code reuse - Surfacing code via search means it’s easier to avoid reinventing existing code, leading to more consistent, efficient coding practices.
5. Improving code health - If you’re trying to change from an antipattern to a best practice, use Sourcegraph to see how much work there is to do across the entire codebase.

While we're working together today, think about which of these use cases is most relevant to your day to day work. That will help you conceive of how the tool might be most relevant to your particular needs, so that you can get the most out of the tool.

### Conclusion

Sourcegraph is a code search tool that allows you to find all of your company’s code in the browser in order to make your work easier and more efficient. Next up, we’ll dive in to the tool to learn how to search in Sourcegraph.

### Resources

*Share these with the customer after the call, typically in Slack.*

- [Sourcegraph](https://sourcegraph.com)
- [Sourcegraph Documentation](https://docs.sourcegraph.com)
- [Sourcegraph Use Cases](https://about.sourcegraph.com/use-cases)
- [Sourcegraph Customer Case Studies](https://about.sourcegraph.com/case-studies)

## Unit 2: Navigating the Sourcegraph UI

**Learning goal:** After completing this unit, you’ll be able to navigate the Sourcegraph home page, understand the search mode buttons, and be able to navigate the search results page. 

### The Sourcegraph home page

*At this point the CE should share demo.sourcegraph.com*

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

*Search for context:global new \bauth\b provider patternType:regexp , show the results*

The final search mode option is our language-aware structural search option, represented by the square bracket button ([]). When selected, you’ll have the option to include structural holes, represented by … or :[a] in your query, to run multi-line fuzzy searches. 

*Search for context:global lang:JavaScript class ... extends ... {...} count:all patternType:structural*

So, for example, if I search for `context:global lang:JavaScript class ... extends ... {...} count:all patternType:structural`, I get a really wide variety of results that match that pattern. Something to call out is that structural search mode is smart enough to match nested characters—so you can see it won't prematurely close on the first closing curly brace it sees; instead, it will wait until it finds the matching one.

I'm going to pause here: are there any questions about our three search modes, or do folks have use cases that jump to mind for any of them?

*Pause, leave space for questions, get a drink of water*

### The search results page

Awesome! So, let's chat through what you'll see when you run the search. When you run your search, you will be redirected to a search results page. It will look something like this:

*run the `new auth provider` regex search again*

The main area of the page will show your search results, with the matching text highlighted. By default, you’ll see one line above and below your matching line, in order to provide some context on the search result. The number of lines shown can be customized in your user settings page, if you prefer. Above the search result, you’ll see the repo name and the file path within the repo. If your match is for a file path or repo name, you’ll see just a link to that repo or file, with no preview code.

On the left-hand side of the page, you’ll see options to run different kinds of searches, filter your search results dynamically, or manually filter your searches by repository, language, and other search filters. We'll dive into those in just a second.

Clicking on your search results will open the matching code, file, or repo in Sourcegraph. From there, you can view the full file and navigate to other files in the same repo, or run a new search.

### Conclusion

Sourcegraph offers three search modes, controlled by buttons in the search toolbar. In our next units, we’ll learn more about those search modes and filters to narrow down your search results. 

### Resources

- [Sourcegraph](https://sourcegraph.com)
- [Sourcegraph Documentation](https://docs.sourcegraph.com)

## Unit 3: Introduction to filters

**Learning goall:** By the end of this unit, users should understand how to use our filter functionality.

### Dynamic filters

So as I mentioned, Sourcegraph provides filters to narrow down your search result. You'll see on the top left here that it's suggesting filters based on the results that were returned—so in this case, I can narrow down to just Golang files by clicking this `lang:go` option.

*Click the lang:go filter.*

If I prefer, of course, I can type that filter in as well. 

*Type in the lang: filter, show the autocomplete language options.*

It's also suggesting I exclude test code—often super useful if you just want to look at application code. So if I click this `-file:_test.go$` button

*Click the button*

you can see that I'm not only seeing code where the file path does not end in `test.go`. Most of our filters work this way: you can negate by adding a negative sign in front of them. I also want to make sure that folks know this `file:` filter exists to limit results to certain file paths—super useful if you want to just search in a Dockerfile, for example. 

The final filter I want to highlight here is this list of repositories. These results are showing what repos your code is in, ordered by most to fewest results. If I click on `github.com/sourcegraph/sourcegraph` here, you'll see that I'm narrowed down to just the main Sourcegraph monorepo.

*Click on the filter*

Something to highlight is that our repo filter, like most of our filters, automatically supports partial matching—so if I search `repo:sourcegraph`, I'll see matches from all of the repos in the Sourcegraph org. 

*Delete the first repo filter, run the repo:sourcegraph search, highlight the repos that are now being returned*

But to go back to the monorepo filter

*Go back to the repo:github.com/sourcegraph/sourcegraph$ filter*

you'll see here on the side that it's now suggesting other branches and tags I could search. We're looking at the default main/master branch usually, but if I want to check out the code on an old version, I just click here to do that.

*Click on one of them, highlight it in the query syntax in the search bar*

Does anyone here ever have to look at staging branches or feature branches?

*Wait for responses, discuss with the users whatever they say. If they say nothing, you can say something like, "we use this all the time at Sourcegraph to look at the code in previous versions of the product, since not all of our users upgrade their instances immediately!"*

Our full search syntax is available over in this box—you can see common filters or the full list. And, as noted in this final box, we support Boolean operators, so you can add an `AND`, `OR`, or `NOT` into your query to combine different aspects of the query. 

*Show them the box where these options exist.*

This will allow you to build your own queries beyond what's suggested by dynamic filters. 

### Conclusion

With our query filters, you can narrow things down to find just the content you need, based on the results that Sourcegraph is returning!

### Resources

- [Three ways to search code with Sourcegraph](https://learn.sourcegraph.com/three-ways-to-search-code-with-sourcegraph)

## Unit 4: Code intelligence

**Learning goals:** Users will know how our code intelligence functionality works and how they can use it.

### Viewing code intelligence in a file

So, I mentioned earlier that we offer code intelligence functionality, and I want to show that to you now.

*Click in to a file of your choice, and find a symbol to hover on.*

So you can see here that I clicked in to one of my search results, and I can now see the source code. What I'm also seeing here is this over tool tip, which has what we call code intelligence. By default we'll ship with search-based code intelligence; for some languages, we also offer what we call precise code intelligence, which is compiler-accurate. 

*If you know they've set up precise code intel or will, speak to that. If you're not sure, you can use this space to ask what langauges they're working in in order to see if there's any that are a good fit. This section will necessarily require some customization based on what you know about the customer.*

Something to call out here is that when I click "find references" to find places where this symbol is used, or "go to definition" to find where it's defined, that works cross-repo. So, you should be able to see that no matter where in the code it's being used, allowing you to really track the downstream impact of changes. 

*Typically at this point it's worth calling out any limitations of code intelligence for the customer's languages if known—challenging accuracy for Ruby or Python, for example.*

I want to pause here and see if anyone has questions about how the code intel functionality works, or wants to share something that comes to mind about how this could be useful for them!

### Conclusion 

Code intel allows you determine the downstream impacts of changes across repos, and for some languages you can have access to compiler-accurate code intelligence if enabled.

### Resources

- [Code intelligence docs](https://docs.sourcegraph.com/code_intelligence)

## Unit 5: Notebooks

**Learning goals:** Understand the Notebooks functionality and how to use it to share information with colleagues. 

### What are notebooks?

Our notebooks functionality is inspired by Jupyter notebooks—it's a great way to share code with your colleagues. 

*Open up a notebook. Up to you what you want to use, but https://demo.sourcegraph.com/notebooks/Tm90ZWJvb2s6Nzg= is a nice one if you don't have a go-to. Modify the talk track if you pick a different demo, but hit the same general points.*

### What do you use notebooks for?

So you can see here that we're sharing information about the code—in this case we're talking about how we handle something in the Sourcegraph codebase. As a new developer, I can be given this notebook to educate myself, and read what my colleagues have said. And, as you can see, I can click "run all blocks" and these searches will all run inline. 

For a lot of our customers, this replaces typed-out documentation that lives in a wiki tool like Confluence. Since the examples run live, you're not going to have out-of-date references here—devs can always see where you're using a particular pattern in the codebase today. 

As I scroll down here, you can see that we're actually highlighting some parts of the code as it existed at a specific time in the codebase (in this case, symbol definitions). Our devs have written out info about why they're structured this way, and gotchas about using them. Now if a teammate has a question, they can send this along as a first step in allowing fokls to answer their own questions.

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
