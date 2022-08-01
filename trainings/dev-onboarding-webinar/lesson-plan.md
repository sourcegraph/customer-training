# New Developer Onboarding Training

**Topic:** This training is intended to serve as a functional enablement training for companies where new employee onboarding is a use case. The focus here is new-to-the-team developers, not new-to-the-profession developers, though of course there can be some overlap.

## Intro

Sourcegraph is a code intelligence platform that allows for search across all your code, as well as live-updating code examples using our Notebooks functionality and trend-tracking using our Insights feature. Today, we’ll focus on how our Search, Notebooks, and Insights features can help orient a new teammate to your codebase. 

## Unit 1: Finding relevant services in the code

**Learning goals:** After completing this unit, customers should understand how to use code search to find relevant code using Commit Search.

### Finding relevant code using commit search

Sometimes, it can be challenging to find the relevant code for a particular feature if you’re not familiar with the codebase. Features can have different names in customer-facing or employee-facing communication than they do in the code. One way to find relevant code is to look at commit messages mentioning the feature name—this can allow you to see what has changed recently, and find the relevant piece of code to explore further.

🔎 The trainer should demonstrate:

- Running a commit search for a feature name (such as “code intel”) in the Sourcegraph monorepo (query: `context:global type:commit code intel repo:sourcegraph/sourcegraph$ patternType:literal` if using this query)
- Highlight how commit message contents show the feature name, even if the code itself does not include the name `code intel`
- Show how applying the `-file:doc` filter can exclude docs changes
- Click into a commit message result and show how to find the actual files where the changes are being applied
- Show how to click into the individual files to navigate them at the current commit and at main/master

### Conclusion

Using commit message search, as a new developer I’m able to find relevant areas of the code to explore further, and see context about what changes have happened to the code recently. I’m also able to leverage that information using `diff` search in the future, if I prefer to search changes to the code directly. 

### Resources

- [Commit message guidelines](https://docs.sourcegraph.com/dev/background-information/commit_messages)
- [Search keywords](https://docs.sourcegraph.com/code_search/reference/queries#keywords-diff-and-commit-searches-only)

## Unit 2: Using code navigation to find uses of a relevant symbol

**Learning goals:** After completing this unit, customers will understand how to find uses of a method using Code Navigation.

### Using code navigation to find uses of a symbol

Once I’ve found code that I want to explore, I can begin to dig in further to understand it. Using code navigation, I can find all uses of a symbol across my code—if I have precise code intelligence enabled, this will be compiler-accurate intelligence.

🔎 The trainer should demonstrate:

- Opening a relevant file to explore further
- Finding a useful symbol in the code (ideally with precise code intel)
- Jumping to definition from the hover tooltip (if not already at definition)
- Finding references across the codebase to the symbol in question

❗️ If you leave the last unit on a note of navigating at main/master, you can jump straight into the navigation from the file you were exploring.

Now I know where this is used, and what the downstream impacts of changing the symbol would be. Going forward, I can use the symbol in new code, with an idea of how it’s used, or can ensure that I don’t create unintended downstream impacts if I change this code as part of my first commit.

### Conclusion

With Sourcegraph, I’m able to avoid unintended consequences as a result of my initial work on the codebase. This means quicker code review from my colleagues, and a faster time to first (or tenth!) commit.

### Resources

- [Intro to Code Intelligence](https://docs.sourcegraph.com/code_intelligence/explanations/introduction_to_code_intelligence)
- [Code Intelligence documentation](https://docs.sourcegraph.com/code_intelligence)

## Unit 3: Using git blame to find helpful colleagues

**Learning goals:** After completing this unit, customers will understand how to use the git blame functionality to find appropriate colleagues to review their code or provide assistance.

### Using git blame in Sourcegraph

As a new developer, sometimes even with full code context I need to reach out to my teammates for more info, context, or guidance. Using git blame allows me to find the right person.

🔎 The trainer should demonstrate:

- Enabling the git blame extension per line and per file on a file containing an interesting symbol
- Finding the name of the colleague associated with git blame
- Highlighting relevant lines and copying the URL to share it with a colleague

Using Sourcegraph, I can quickly and easily find colleagues to help me as I onboard.

### Conclusion

Git blame allows me to reach out to the right person for more info, and sharing links allows them to have the exact same context as me, unlike if I was sharing from the IDE. Staying in Sourcegraph lets me harness the search and navigation power versus navigating to the codehost.

### Resources

- [Sourcegraph extensions](https://docs.sourcegraph.com/extensions) 

## Unit 4: Using Code Notebooks to see examples for onboarding

**Learning goals:** After completing this unit, the customer will be able to view Notebooks, share them, and create their own.

### Viewing notebooks

Sourcegraph allows for sharing of content via Notebooks, which are modeled on Juptyer notebooks. Using a notebook, I can see live examples of code based on search queries, and learn more about how we approach things in our codebase. It's an easy way to get up to speed with what's going on with my teammates, and if they embed live query examples, I can know that it's referencing current code, not out-of-date examples.

🔎 The trainer should demonstrate:

- How to access a notebook (feel free to create one or use a relevant one; the [onboarding notebook](https://demo.sourcegraph.com/notebooks/Tm90ZWJvb2s6MjY2) is intended to accompany this demo and can be shared with the customer to serve as the basis for their own content)
- Running a live query block and opening results from that query

### Conclusion

With Notebooks, I can easily get up to speed with how my team handles best practices and antipatterns, and get live code examples to influence my development choices as I onboard.

### Resources

- [Notebooks documentation](https://docs.sourcegraph.com/notebooks)

## Unit 5: Using Code Insights to highlight trends for new hires

**Learning goals:** 

### Tracking code trends using Code Insights

As a new hire, I want to know what’s important to the company and what code initiatives exist—for example, how progress on avoiding TODOs or linter skips is going. With Code Insights, I can easily jump into an understanding of where we’re at and where we’re going.

🔎 The trainer should demonstrate:

- Viewing insights ([Dev onboarding dashboard](https://demo.sourcegraph.com/insights/dashboards/ZGFzaGJvYXJkOnsiSWRUeXBlIjoiY3VzdG9tIiwiQXJnIjo3NDU0MH0=) is recommended)
- How to view search results by clicking into a particular data point
- How to narrow results to a single repo
- How to create your own insight on the Insights page

### Conclusion

With Insights, it's easy to catch up on what my team cares about, and how our progress on those initiatives is trending. I can ensure that I'm moving in the right direction as I ramp.

### Resources

- [Code Insights documentation](https://docs.sourcegraph.com/code_insights)
- [Code Insights recipes](https://docs.sourcegraph.com/code_insights/references/common_use_cases)

## Closing thoughts

As a new developer, Sourcegraph allows me to easily onboard into the team and hit the ground running. I can answer more of my own questions, easily learn more about the code, and have a quicker time to first (or tenth!) commit.
