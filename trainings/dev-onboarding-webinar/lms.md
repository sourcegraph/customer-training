# New Developer Onboarding Training

**Topic:** This training is intended to serve as a functional enablement training for companies where new employee onboarding is a use case. The focus here is new-to-the-team developers, not new-to-the-profession developers, though of course there can be some overlap.

## Intro

Sourcegraph is a code intelligence platform that allows for search across all your code, as well as live-updating code examples using our Notebooks functionality and trend-tracking using our Insights feature. Today, we’ll focus on how our Search, Notebooks, and Insights features can help orient a new teammate to your codebase. 

## Unit 1: Finding relevant services in the code

**Learning goals:** After completing this unit, customers should understand how to use code search to find relevant code using Commit Search.

### Finding relevant code using commit search

Sometimes, it can be challenging to find the relevant code for a particular feature if you’re not familiar with the codebase. Features can have different names in customer-facing or employee-facing communication than they do in the code. One way to find relevant code is to look at commit messages mentioning the feature name—this can allow you to see what has changed recently, and find the relevant piece of code to explore further.

To search a commit message in Sourcegraph, append `type:commit` to the end of the query. Sourcegraph will look for your query in the commit message itself. For example, searching for `context:global type:commit code intel repo:sourcegraph/sourcegraph$ patternType:literal` will show you all commit messages referencing `code intel` in Sourcegraph's monorepo:

![The results of a commit message search](https://user-images.githubusercontent.com/9934079/181376748-9b45e9b2-37ae-4c10-8285-5ae00f9d7ce3.png)

By searching this way, you can find relevant code even if the code itself doesn't use the same feature name. To view the code, click into the commit message search result, and you'll be presented with the changed code. Click on the name of the file to view the code in full.

![You can view the changed code by clicking into the search result](https://user-images.githubusercontent.com/9934079/181376831-5a42d779-2d42-4c45-b3d0-d0fb8ae3c3d2.png)

With Sourcegraph commit search, it becomes much easier to discover where in the codebase you should be looking for relevant code.

### Conclusion

As a new developer, you can find relevant areas of the code to explore further by using commit message search. 

### Resources

- [Commit message guidelines](https://docs.sourcegraph.com/dev/background-information/commit_messages)
- [Search keywords](https://docs.sourcegraph.com/code_search/reference/queries#keywords-diff-and-commit-searches-only)

## Unit 2: Using code navigation to find uses of a relevant symbol

**Learning goals:** After completing this unit, customers will understand how to find uses of a method using Code Navigation.

### Using code navigation to find uses of a symbol

Once you've found code that you want to explore, you can begin to dig in further to understand it. Using code navigation, you can find all uses of a symbol across your code. If you have precise code intelligence enabled, this will be compiler-accurate intelligence.

To start, open a relevant file from your search results. You'll be able to see the code navigation tool tip by hovering over any symbol in that code. 

![The hover will give you options to view the definition and uses of the symbol](https://user-images.githubusercontent.com/9934079/181376968-c76d3eb9-b372-48ba-956a-c76912a4a4ae.png)

The hover will show you how to navigate to the definition of the symbol if you're not viewing that already, and will give you the option to view all other references to that symbol across your code.

![A list of the references to a particular symbol in the Sourcegraph code](https://user-images.githubusercontent.com/9934079/181377060-4abdad8f-d45b-4333-b006-47d9f47f8be1.png)

With code navigation, you can learn about the symbol's use and what the downstream impacts of changing the symbol would be. Going forward, you can use the symbol in new code, with an idea of how it’s used, and can ensure that you don’t create unintended downstream impacts if you change this code as part of your first commit.

### Conclusion

With Sourcegraph, new developers are able to avoid unintended consequences as a result of initial work on the codebase. This means quicker code review from your colleagues, and a faster time to first (or tenth!) commit.

### Resources

- [Intro to Code Intelligence](https://docs.sourcegraph.com/code_intelligence/explanations/introduction_to_code_intelligence)
- [Code Intelligence documentation](https://docs.sourcegraph.com/code_intelligence)

## Unit 3: Using git blame to find helpful colleagues

**Learning goals:** After completing this unit, customers will understand how to use the git blame functionality to find appropriate colleagues to review their code or provide assistance.

### Using git blame in Sourcegraph

As a new developer, sometimes even with full code context you need to reach out to your teammates for more info, context, or guidance. Using git blame in Sourcegraph allows you to find the right person.

To use git blame, first open a file in Sourcegraph. Then, click the git extras button on the right side of the screen.

![Click the git blame icon to enable/disable the annotations](https://user-images.githubusercontent.com/9934079/181377130-b239219e-2ac2-481a-b2b7-b2262a3567e7.png)

Continuing to click the button will enable the function per-file, per-line, or disable it.

Once you've found the name of the right colleague to talk to, you can copy the Sourcegraph URL directly from the browser bar and send it to them. That will send them to the same view of the file that you have, including maintaining any highlighted lines so you can show exactly what you have questions about.

![Highlighted lines are included in the URL for easy sharing](https://user-images.githubusercontent.com/9934079/181377188-c47a1929-b957-47ab-af63-101db080954e.png)

Using Sourcegraph, you can quickly and easily find colleagues to help you as you onboard.

### Conclusion

Git blame allows you to reach out to the right person for more info, and sharing links allows them to have the exact same context as you, unlike if you was sharing from the IDE. Staying in Sourcegraph lets you harness the search and navigation power versus navigating to the code host.

### Resources

- [Sourcegraph extensions](https://docs.sourcegraph.com/extensions) 

## Unit 4: Using Code Notebooks to see examples for onboarding

**Learning goals:** After completing this unit, the customer will be able to view Notebooks, share them, and create their own.

### Viewing notebooks

Sourcegraph allows for sharing of content via Notebooks, which are modeled on Juptyer notebooks. Using a notebook, you can see live examples of code based on search queries, and learn more about how your team approach things in your codebase. It's an easy way to get up to speed with what's going on with your teammates, and if they embed live query examples, you can know that it's referencing current code, not out-of-date examples.

To access Notebooks, click on the bookmark icon in the top navigation bar in Sourcegraph, or go to `yourURL/notebooks`. From there, you can view all notebooks visible to you, create your own notebooks, or click the Getting Started tab to read more about the feature and see example notebooks.

![The Getting Started page of Notebooks has useful info](https://user-images.githubusercontent.com/9934079/181377282-1e5b75d6-79ef-42cd-8d3b-3e8ecda982de.png)

If you'd like to see some public examples, you can view this [Structural Search notebook](https://sourcegraph.com/notebooks/Tm90ZWJvb2s6Mzk4), a guide to [finding secrets in your code](https://sourcegraph.com/notebooks/Tm90ZWJvb2s6Nzg0), or an explanation of [how Sourcegraph handles actor propagation](https://sourcegraph.com/notebooks/Tm90ZWJvb2s6OTI=).

You can run a query block by clicking the blue button next to it. This will show a list of related search results, and you can click on those to open the search results for more information.

### Creating notebooks

To create your own notebook, go to the Notebooks homepage and click Create notebook. From there, you'll be able to build your notebook using a WYSIWYG editor. If you prefer to import markdown files directly (for example, you've exported an example notebook and want to use it), click the blue arrow in the Create notebook button, and you'll be presented with an option to import a markdown file. 

![Click the arrow on the Create Notebook button to import a notebook from markdown](https://user-images.githubusercontent.com/9934079/181377363-6ac3b232-c4cd-48f5-9709-3ad360fb6980.png)

### Conclusion

With Notebooks, you can easily get up to speed with how your team handles best practices and anti-patterns, and get live code examples to influence your development choices as you onboard.

### Resources

- [Notebooks documentation](https://docs.sourcegraph.com/notebooks)

## Unit 5: Using Code Insights to highlight trends for new hires

**Learning goals:** After completing this unit, customers should understand how to view Code Insights and create their own.

### Tracking code trends using Code Insights

As a new hire, you want to know what’s important to the company and what code initiatives exist—for example, how progress on avoiding TODOs or linter skips is going. With Code Insights, you can easily jump into an understanding of where your team is at and where they're going going.

❗️ NOTE: Code Insights is a paid add-on. If you don't see it, check with your instance admin or Customer Engineer for more info.

To view Code Insights, click on the graph icon in the top navigation bar. By default, you'll see all Insights on your instance, and can narrow down the scope using the Dashboard drop-down menu above the graphs. 

Code Insights graph changes to your code over time, by graphing the results of Sourcegraph search queries. As a result, you can click in to any data point and see a list of search results populating the data point. From there, you can take advantage of Code Navigation and git blame. 

If an insight is running over all of your team's repos, you'll see a filter icon above the insight.

![The filter icon will allow you to specify individual repos to view in the insight](https://user-images.githubusercontent.com/9934079/181377455-054fc8e8-cc02-41e4-9ed3-381f1046e02a.png)

By clicking it, you'll be able to include/exclude repositories from your view of the insight, in order to narrow down on the repos you care about. This is useful for seeing things like TODOs in repos that your team, specifically, works to maintain.

If you wish to create your own insight, click the Create Insight button on the top right of the screen. From there, you'll be able to write your own query. You can keep the insight private to yourself, or share it with your entire instance. 

### Conclusion

With Insights, it's easy to catch up on what your team cares about, and how your progress on those initiatives is trending. You can ensure that you're moving in the right direction as you ramp.

### Resources

- [Code Insights documentation](https://docs.sourcegraph.com/code_insights)
- [Code Insights recipes](https://docs.sourcegraph.com/code_insights/references/common_use_cases)

## Closing thoughts

As a new developer, Sourcegraph allows you to easily onboard into the team and hit the ground running. You can answer more of your own questions, easily learn more about the code, and have a quicker time to first (or tenth!) commit.
