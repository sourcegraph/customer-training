

# Code Insights Webinar

**Topic:** This training is intended as an initial deep-dive to educate users on Code Insights outside of the 101/102 context. **If at all possible, we recommend having the customer provide a Code Insights use case to you *before* the training, giving you the opportunity to work on that specific insight or something similar;** if not, you can use this as a way to show Code Insights to them and discuss use cases they might find valuable live on the training.

## Intro

Today's training is intended to walk users through our Code Insights product, and show users how to use the feature. By the end of it, we hop that you'll feel comfortable with what Code Insights is and can do, and will be ready to start with your own changes in Sourcegraph.

❗️ If the training is happening in the context of a champion brining in other team members, have them speak at the top about why they think Code Insights will be useful, and what they envision the team using it for.

## Unit 1: Get familiar with Code Insights

**Learning goals:** After completing this unit, customers will understand what Code Insights are, and can be used to track.

### What is Code Insights?

Code Code Insights reveals high-level information about your codebase, based on both how your code changes over time and its current state. It's a way of visualizing your searches as graphs, so that you can track not just what things are like today, but how that has changed over time. This can be super helpful for tracking things like:

* Migrating from one version of a language or dependency to another
* Whether folks are adding frequent linter overrides 
* Tracking how many TODOs are present in your code
* How adoption of a new API is going

With this info, you can easily make informed decisions about priorities and where to focus your time and energy.

### Running an Insight

To get started, I'm going to generate an insight that tracks TypeScript utilization versus JavaScript utilization in my codebase.

❗️ This is a generic starting point. If you know a different Insight will be more appropriate, or the customer has a specific use case in mind, you may want to walk through that change, instead. A full list of recipes is available [in the docs](https://docs.sourcegraph.com/code_insights/references/common_use_cases). 

🔎 The trainer should demonstrate:

* Creating an insight that tracks [JavaScript vs. TypeScript](https://docs.sourcegraph.com/code_insights/references/common_use_cases#language-use-over-time)
* Review what the `lang:` and `select:` filters are doing
* Show that once the insight is generated, you can filter by repo
* Show how to access individual data points by clicking in to them
* Show how to get a shareable link for the insight
* Show how to create the insight while running a search directly, rather than from the Insights page

As we like to say: if you can search it, you can see it. One thing to note is that we have three permissions levels for an insight: private, global, and per-org. If your team is using orgs, that will allow you to create granular dashboards to share your insights, so that you can share a particular set of graphs with just engineering managers, just frontend engineers, or just the folks working on a particular project. 

🔎 The trainer should demonstrate:

* How to create a new org from the user settings page (you can show just where the button is, you don't have to finish the flow)
* How to create a new dashboard scoped to an org 
* How to add an existing insight to that dashboard

### Designing a Insight

The insight we just generated is pretty simple—but your insights can be as complex as your search queries can be. I wanted to share some common use cases in our docs.

🔎 The trainer should show:

* The [Insights Recipes page](https://docs.sourcegraph.com/code_insights/references/common_use_cases)
* Highlight a few use cases there based on what you know of the needs of the group.

❗️ If you don't know the needs of the group—and even if you do—this is a good time to stop and ask questions about what sorts of things people are tracking and how they're doing so today, and what kinds of things they'd like to track but can't.

❗️ If your champion has brought a use case to you for an insight, at this point, have them speak about that use case. 

🔎 The trainer should show:

* **If the champion brought a use case:** walk through constructing the appropriate query with them, possibly with the champion sharing their screen and driving.
* **If the champion did not bring a use case:** ask the group what use cases jump out to them, and ask for a brave volunteer to build an appropriate query while sharing their screen.
* **If the champion did not bring a use case and nobody is volunteering a suggestion:** ask the champion directly which of the recipes seems most appealing, or—based on known [use cases](https://about.sourcegraph.com/use-cases)—suggest an appropriate insight from the recipes list, and have the champion share their screen to add it to their own instance.

❗️ Preparation pays off—this is much easier with a known insight from the champion going in, and you will benefit from making sure they're okay to share their screen on the call. They may not be for code privacy reasons, but if at all possible, you want to leave the meeting with the insight configured *in their instance*.

❗️ Once the insight is built, ask the builder to drop the link to it in the Zoom chat.

### Resources

* [Code Insights docs](https://docs.sourcegraph.com/code_insights)
* [Common use cases and recipes](https://docs.sourcegraph.com/code_insights/references/common_use_cases)
* [Troubleshooting](https://docs.sourcegraph.com/code_insights/how-tos/Troubleshooting)

## Closing thoughts

Code Insights can be a super powerful way to track changes in your code base, letting your code speak for itself as you're tracking internal initiatives. Additionally, it will give you, your managers, and your leadership team a shared reality in which to discuss the code, because Code Insights gives you the ability to share easy visualizations of current and historical state of the codebase even for folks who aren't regularly in the code. If you have any questions setting up your first insight, please ping me in Slack and we can troubleshoot together!

❗️ At this point you can kick it over to your champion, open the floor for questions, or share additional info, depending on what's appropriate for your audience.
