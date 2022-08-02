# VSCode webinar

**Goals:** Viewers will:

* Discover how the Sourcegraph for VSCode extension can be used to search for code right in the editor, no local copy needed
* Install the extension themselves
* Run at least one search in VSCode for OSS Code
* Learn how to incorporate the extension into their day-to-day team programming workflow

## Intro

Today I'm going to be walking through our VSCode for Sourcegraph extension, and highting how you can configure it to search open source code—or your own private code—right from VSCode, without needing to have that code pulled down locally. By the end of today, I want to make sure everyone leaves here with an understanding of why we built the extension, how to install it, and how to use it—and hopefully, everyone will leave here having installed it themselves!

## History

For those of you who may not be familiar with Sourcegraph, first of all: welcome! Secondly, a brief overview of what we are. We're a code search and intelligence platform, allowing you to search across all of the code that's indexed on a particular Sourcegraph instance, in the cloud. In practice, that means you can use sourcegraph.com/search to search any OSS code you want, no matter what you have local to your machine—and if you set up a Sourcegraph instance yourself, you can search all of the code you have access to in your instance without needing to have it locally.

Why did we build the VSCode extension? We heard that people were excited about the Sourcegraph functionality, but hesitant to switch between their IDE into the browser or their terminal for our CLI. So, with our extension, you don't have to make the choice—you can stay in VSCode, and search code when you need to without leaving.

## Installing the extension

The extension is available in the [VSCode marketplace](https://marketplace.visualstudio.com/items?itemName=sourcegraph.sourcegraph). If you install it directly, it will connect to our OSS code search. To connect it to your own instance, you'll have to do a little bit of configuration.

🔎 The trainer should show:

* How to install the extension
* How to connect to a private instance

## Using the extension

Once the extension is installed and pointing to the right instance, you can search directly for code, even if it's not on your machine—and you get access to the same filters that you do in browser Sourcegraph. 

🔎 The trainer should show in VSCode:

* Running a literal, regular, and structural search
* Where dynamic filters are located
* How to apply a lang: filter from the dynamic filters, and what it does
* How to apply a file or -file: filter from the dynamic filters, and what it does
* The repositories listed under the dynamic filters, how they are listed (greatest to least number of results), and what happens when they're clicked on

For example, if I am working on code and want to see what a file looks like on a feature branch, it's easy to do that; similarly, I can quickly and easily search code to find code that I might want to reuse.

🔎 The trainer should show:

* Navigating from a local file, to the Sourcegraph extension, to see that file on another branch without checking it out
* How to discover previously-written code to use as an example for a local challenge (see the `repo:^github\.com/sourcegraph/sourcegraph-.+$  /import .+ from 'rxjs'/` example in [the blog post](https://about.sourcegraph.com/blog/ways-to-use-sourcegraph-extension-for-vs-code)

Say that my search returns a link to a file that I want to explore. You'll see that if I'm looking for a file I don't have stored locally, I will see a read-only view. But, if I open a file that does exist locally, I can actually start to edit that file straight away.

🔎 The trainer should show:

* Opening an editable file from search results


## Sharing files with colleagues

One of the challenges of trying to share IDE context with my colleagues is that there's no great way to share with a link. I can copy code, take a screenshot, or tell them the file path, but that won't bring them to exactly what I'm seeing. However, with the VSCode extension, you have the best of both worlds: you can stay in VSCode, but if you need to share the file with a colleague, you can copy a link to the Sourcegraph version of the file, and your colleague will see the same thing in the browser. 

🔎 The trainer should show:

* Copying a link to the Sourcegraph version of a file from VSCode
* What happens when opening the link

## Conclusion

Bringing the power of Sourcegraph into VSCode allows you to continue harnessing the power of Sourcegraph's code search right in the IDE, without needing to switch where you're working. You can make quicker, better-informed decisions, and more easily collaborate with colleagues while still getting the benefits of working directly in your editor. 

We'll now open up the floor to questions!

