

# Batch Changes Webinar

**Topic:** This training is intended as an initial deep-dive to educate users on Batch Changes outside of the 101/102 context. If possible, we recommend having the customer provide a batch change use case to you *before* the training, giving you the opportunity to work on that specific change or something similar; if not, you can use this as a way to show Batch Changes to them and discuss use cases they might find valuable live on the training.

## Intro

Today's training is intended to walk users through our Batch Changes product, and show users how to use the feature. By the end of it, we hope that you'll feel comfortable with what Batch Changes is and can do, and will be ready to start with your own changes in Sourcegraph.

❗️ If the training is happening in the context of a champion bringing in other team members, have them speak at the top about why they think Batch Changes will be useful, and what they envision the team using it for.

## Unit 1: Get familiar with Batch Changes

**Learning goals:** After completing this unit, customers will understand what Batch Changes is.

### What is Batch Changes?

Batch Changes is a way to script changes to your code. Using Sourcegraph search, you'll find a list of relevant repositories—for example, all repos that have `Dockerfile`s, or all repos that have Java files. Then, using a YAML spec that you write, you'll script out the change that you want to make to your files. We can support something as simple as a find and replace (essentially `sed` on steroids) or as complex as a full refactor. Batch Changes can run across many repos at once, allowing you to make very large-scale changes—particularly helpful for the sorts of rote activities (like adding a new step to the CI pipeline) that may need to happen at scale.

Once the batch change's spec is executed, Sourcegraph will generate pull/merge requests on your code host, one per repo (usually—this can be customized). We'll open them on your behalf, and then give you the ability to manage them from within Sourcegraph. You can close individual PRs, comment on them, and even bulk-merge. We also generate a burndown chart for you to track progress. 

### Running a Batch Change

To get started, I'm going to run a batch change that appends `Hello World` to all my `README` files.

❗️ This is a generic starting point. If you know a different batch change will be more appropriate, or the customer has a specific use case in mind, you may want to walk through that change, instead. 

🔎 The trainer should demonstrate:

* Adding a Batch Changes PAT as an end user.
* Creating the [Hello World](https://docs.sourcegraph.com/batch_changes/quickstart) batch change in the browser as a SSBC. (When creating a new SSBC, `hello world` exists as a default library change—you don't need to copy it from the docs.)
* Explain the spec's parts, specifically `resositoriesMatchingQuery`, `steps`, and `changesetTemplate`. 
* The logged information during the execution stage. (Highlight that we're spinning up Docker containers specified by the user.)
* The results of the preview.
* Highlight that the batch change is not applied yet, and discuss what happens (PRs are opened) when it is.

What we just saw is what we call a Server Side Batch Change, or SSBC. That means that it's running directly on the Sourcegraph instance, rather than locally. I can also run this locally, using our CLI. 

❗️ If you know the customer definitely will not be using SSBC for whatever reason, you can run this entire demo via the CLI instead. 

🔎 The trainer should demonstrate:

* Previewing the `hello world` spec via the CLI

Either option will allow you to open those changes en masse, in order to then manage them in Sourcegraph.

### Designing a Batch Change

Obviously, the `hello world` example is probably not something you will ever really need to do! But, there's lots of use cases that we hear from our users that they use Batch Changes for:

* Removing insensitive language
* Changing references to an old feature name
* Adding a step to CI across the board when using IAC
* Pinning transitive dependencies to a specific version
* Opening Jira tickets along with changes

The thing to remember is that Sourcegraph is used to find the relevant repos, but the changes you make can be completely arbitrary—we'll do anything that you can script, and can even spin up your full build environment to make those changes. We maintain a list of examples on GitHub.

🔎 The trainer should show:

* The [Batch Changes Examples repo](https://github.com/sourcegraph/batch-change-examples/)

Taking a look at this list, are there any that jump out to you as something that you might like to automate in your current day-to-day?

❗️ At this point, the demo becomes a little more freeform. If you know going in what the customer wants to do, ideally you will share that spec with them, or workshop building the spec together. If someone has already built a spec and wants to share it (typically your champion), here is the place for them to do that. If neither option is possible, show them [the pin Docker images](https://github.com/sourcegraph/batch-change-examples/blob/main/docker/pin-docker-images.batch.yaml) use case.

🔎 The trainer should show:

* Running the champion's spec, if relevant (have the champion run it while sharing their screen)
* Creating and running the group-constructed spec, if relevant (show your screen while you build the example spec)
* Running the Pin Docker Images spec, if relevant

### Conclusion

Running a batch change, whether through SSBC or via the CLI, will allow you to make many changes at once to your codebase. If you can script it, you can apply it. Next up, we'll show what the Batch Changes dashboards will show you.

### Resources

- [Batch Changes Docs](https://docs.sourcegraph.com/batch_changes)
- [Batch Changes Quickstart](https://docs.sourcegraph.com/batch_changes/quickstart)
- [Running batch changes server-side](https://docs.sourcegraph.com/batch_changes/explanations/server_side)
- [Batch Change Examples](https://github.com/sourcegraph/batch-change-examples)

## Unit 2: Viewing Batch Change Dashboards

**Learning goals:** After this unit, customers will understand how to view PRs opened by a batch change and apply bulk actions to them, as well as viewing and interpreting the generated Burndown chart.

### Viewing Batch Change PRs

Now, as you've seen so far, I've been previewing batch changes, rather than applying them. That just means that this is visible on Sourcegraph, but we haven't opened PRs quite yet. Now I'm going to show you what it looks like when a batch change has open PRs.

🔎 The trainer should show:

* The [Medium Tracking Campaign](https://demo.sourcegraph.com/users/malo/batch-changes/medium-trackin-campaign) or other batch change of the CE's choice with published PRs.
* How to filter PRs by status, check state, and review state.
* How to apply bulk actions (comment, merge, publish, close) on open PRs
* How to view the spec powering a batch change from the Dashboard view (clicking the `Spec` tab)
* Discuss how changesets can be imported, if using the Medium Tracking Campaign and its spec

❗️ Call out that closing a batch change will allow you to also close its associated PRs, if there's a mistake made. 

### Viewing Batch Change Charts

The final thing I want to highlight here is our burndown chart. This tracks the progress of PRs associated with the batch change, whether imported or created via the change. It's an easy way to stay on top of what's going on with the bulk change, rather than having to follow up with individuals, or keep on top of a spreadsheet. 

🔎 The trainer should highlight:

* The [burndown chart for the Medium Tracking Campaign](https://demo.sourcegraph.com/users/malo/batch-changes/medium-trackin-campaign?status=OPEN&tab=chart)
* What it looks like when merged changes are filtered out
* How the chart is live-updated via the code host API

With this chart, it becomes *much* easier to share with my colleagues what the status of a current initiative is, and I can keep on top of whether I need to nudge folks to review my PRs, for example.

### Resources

* [Batch Changes FAQ](https://docs.sourcegraph.com/batch_changes/references/faq)
* [Batch Changes Demo Video](https://www.youtube.com/watch?v=eOmiyXIWTCw)
* [Bulk operations on changesets](https://docs.sourcegraph.com/batch_changes/how-tos/bulk_operations_on_changesets)

## Closing thoughts

Batch Changes can be a super powerful way to make changes in many parts of your codebase in one fell swoop. Used properly, you can save significant time versus cloning the repos locally and making the changes yourself, or even cloning them locally and scripting the change. 

❗️ At this point you can kick it over to your champion, open the floor for questions, or share additional info, depending on what's appropriate for your audience.
