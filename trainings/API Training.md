# Training: Stream API and GraphQL API

**Topic:** This training is focused on the API documentation available: Stream API and GraphQL API. The training covers the differences between APIs, when to use each, and now to get set up to use them. This includes creation of access tokens, stream API in terminal and python scripts, and GraphQL using API Console, Postman, and Apollo Sandbox.

## Background & Getting Started

**Learning goals:** After completing this unit, you'll be able to understand the differences between the Stream API and GraphQL API and when to use each. You also will understand how to generate an access token for your own use and how to validate it.

### Understanding the APIs

❗️Navigate to docs.sourcegraph.com and open the [API documentation page](https://docs.sourcegraph.com/api)

There are two APIs available: GraphQL API and Stream API Docs for both APIs are available on this page You might ask: Why should I use one or the other? We’ll cover that before diving in to test out each. 

Remember that these reference guides are helpful in configuring and using the APIs available, so I will provide all relevant links for you to reference after the session is over.

❗️Open up the Stream API docs

Let’s start with the Stream API. Use the stream api if you’re looking to view a large number of results and want to parse through them. It works by streaming the results that you would normally see through the Sourcegraph UI. 
Compared to our GraphQL API, it offers shorter times to first results and supports running exhaustive searches returning a large volume of results without putting pressure on the backend.
Stream will constantly stream results to you - and you can parse those through any scripting language like python, I will cover and provide examples today

❗️Open the GraphQL API Docs

GraphQL is good for anything outside of search- anything you want to do in the UI, either read or write
Search GraphQL api can take down the environment if you aren’t careful. General guidance is to use ‘count’ values to avoid overloading the system
Eg creating and updating contexts, creating insights, batch changes, etc
About halfway down the page, you can find the API Documentation, where you can reference the API Docs page

### Creating your Access Token and Validation

❗️Navigate to demo.sourcegraph.com and open the profile settings

Let’s jump right into our setup for our APIs. You can follow along if you’d like in your own environment. Note that you will need to do this step regardless of API used, whether GraphQL or Stream API. First, we need to create an access token. We can do that under the user profile -> Settings

❗️Go to Access tokens, then generate new token (use a relevant name)

On the left hand side, open up the access tokens pane, then generate a new token.

Provide the token description, then select the appropriate scope. Note that site-admin:sudo will not be available to all users, and you likely will only see user:all. We will not be using that capability today, but some of the demo files provided will require admin permissions. Refer to the documentation for details.

❗️Make a copy of your access token locally to quickly reference

Once the token is generated, be sure to save the token in your password manager of choice as you will not see it again. 
Then, copy the curl command generated so you can validate the token is working from your local machine.

❗️open terminal and paste the command

Provided all is working, you should see a response that shows the username of the matching user token
So, this means we can move on to test our Stream API and GraphQL API examples

## Stream API Examples

**Learning goals:** After completing this unit, you'll be able to understand the capabilites of the Stream API, how to run and interpret basic commands, and how to build your own 

### Breaking down a Stream API call
❗️Open up the [Stream API examples](https://docs.sourcegraph.com/api/stream_api#request)
First, I’ll generate a response using the Stream API and show how to break down the results. I’ve got a prebuilt curl command that I will be using today available on the Stream API documentation page, and I can use the same access token I just generated a moment ago.

Let me drop my token in, then copy this to the terminal. 
This query is broken down on the docs page, but in summary all we are doing here is hitting demo.sourcegraph.com with a request that looks just like the Sourcegraph search, asking to give the first result from searches that match repo:sourcegraph/ sourcegraph. Note that we can increase the count to get more results.

❗️Copy the code below into a terminal. Make sure the token is embedded in the code
{
curl --header "Accept: text/event-stream" \
--header "Authorization: token [Insert-token-here]" \
     --get \
     --url "https://demo.sourcegraph.com/.api/search/stream" \
     --data-urlencode "q=repo:sourcegraph/sourcegraph doResults count:1"
}

There are 5 types of events we might get from the stream API, matches, progress, filters, alert, and done. 
* Matches: matches can be of type content, path, commit, diff, symbol and repo
* Progress: statistics such as match count, count of repositories with matches, and duration
* Filters: suggestions for additional filters to further narrow down the search
* Alert: info, warning and error messages
* Done: always the last event

In our response, we can see the responses for each of those events. I won’t go digging into the content of each, but will point out that ‘matches’ has one result with a repostars value of ~8k, which matches the query directly in sourcegraph. Also, note that the ‘progress: done’ value is ‘true’, so the stream is complete, and the last event is ‘done’ with an empty dataset. 

### Leveraging Python to break down Stream API calls

Next, we can use the stream API coupled with a python script to find results available in Sourcegraph

❗️Make sure terminal is pointing to the directory where the scripts are stored, eg your Downloads folder 

First, let’s cover what we’re looking for. This script runs a large type:commit query by breaking it up and running the
query on one repository at a time and then aggregating the results.
In order to accomplish this, it runs a `select:repo` query first and then
iterates over that list running the original query on just that repository.

❗️[open search results](https://demo.sourcegraph.com/search?q=context:global+TODO+type:%22commit%22+lang:TypeScript+after:%221+week+ago%22+count:all&patternType=standard&sm=1&groupBy=path)

Here’s what the Sourcegraph search results look like. Note that the results take a while, as the query is complex.

Now, let’s drop this command in and see what we get.
Note that the stream is showing all the results in the terminal, and stops running when it hits the count. 
That’s the power of the stream API. It provides the same results to you locally so you don’t need to interact in the web interface.

❗️copy the code below into terminal

{
python3 split_sg_query.py --sg https://demo.sourcegraph.com --token Insert-token-here --query 'TODO type:"commit" lang:TypeScript after:"1 week ago" count:20’
}

The Stream API provides us a programmatic way to process Sourcegraph searches that may contain large amounts of data
❗️You may need to close the terminal window if the command does not complete

## GraphQL API Examples

**Learning goals:** After completing this unit, you'll be able to understand the capabilites of the GraphQL API, how to run and interpret basic commands, and how to build your own. This is split into 3 sections so you can choose to omit options that are not relevant to the customer. Intro and API console are required. Postman and Apollo Sandbox are optional.

### Introduction and API Console

❗️Navigate to [GraphQL API](https://docs.sourcegraph.com/api/graphql)
Now, we can switch over to the GraphQL API. Anything you can do in the Sourcegraph App, you can feasibly do with the GraphQL API. But, use caution and don’t forget to set your limits so you don’t hammer the system.

We can use the same access token we generated in the first part of this training, or we can generate a new one.

In today’s training we’re going to cover 3 methods to interact with the GraphQL API: the API Console, the Apollo Sandbox, and Postman.

❗️Click on Search ⇒ See additional documentation about search GraphQL API.

Sourcegraph does not support pagination for search results when using the GraphQL search. Instead, we recommend using the stream search API we just covered for scenarios where you need to run a long query and receive continuous results.

❗️Show examples from the GraphQL page, [shortcut](https://docs.sourcegraph.com/api/graphql/examples)

Before we dive into the queries, let’s take a look at some examples. You’ll see the Postman collection mirrors these examples.

❗️Click first example: ‘get contents of file’

When you select one of these examples, it will load the API console - and you do not need to log in. 

❗️Click profile -> settings -> API Console

You can also reach the API console in your local environment by clicking your profile, then settings, then API Console on the left side.

Let’s start with a simple query, get file contents. We can break down how the query is formed, and what we get out when it runs.

❗️Run the example

First, let’s run it and make sure this is working. 
We can see the result on the left pane.

❗️Navigate to the [TA GraphQL handbook page](https://handbook.sourcegraph.com/departments/technical-success/ta/team-culture/working-with-the-sourcegraph-graphql-api/)

Before I dig into this, let me point to this handbook page that was written by one of our TAs that used to work for Apollo. 
At a high level, all GraphQL queries will look something like this. 
Every query starts with ‘query’ and an optional operation name. Then, there might be variables followed by fields that specify what you’re looking for in the search results.
We can get some help from the schema, which will show up in the documentation explorer in the API console. Click Query, then repository. 
Here, we can see what the Repository Query is expecting in the arguments. 

❗️ Press control + space to demo suggestions

Also, if we clear out the query, we can use Control+Space to drop in suggestions on how to build a query.

❗️Build out the basic query below

{
query listfirst1krepos {
  repositories(first: 1000) {
    nodes {
      name
      description
      url
    }
  }
}
}

### Setting up and using Postman

❗️Open up Postman.com

Postman has a free download available from their website, but you might want to find out if you have a copy internally to get set up. Part of the reason we’ll focus on Postman first is because we have a shareable json file with pre-built queries you’ll be able to use fairly quickly.

❗️Open Postman locally

Once you get Postman installed, let's get it opened up and import the JSON demo file. With the provided JSON file, you can start using some pre-build GraphQL API calls with little to configure.

❗️Import the file, then open the collection

With Postman open, go ahead and import the JSON collection. 
Click on the Sourcegraph Collection and navigate to Variables

❗️Paste in your username and token

Paste in your token and username into the ‘current’ column on the right, and set your base URL to your Sourcegraph instance.

These variables pre-fill the header details for you within each request.
If we look at one of these POST requests, you will see that the token value gets inserted into the header.

In Postman, you’ll need to fetch the schema to enable autocompletion. This does require you to log in with your Postman account. Please confirm with your IT team if this is an approved option

❗️Show some of the prebuilt queries

Here are the same queries that we saw in the examples posted on our API docs page. You can look at the body for each of these queries, as the headers are all variable based.
The last Postman request is specific to the admins - it requires a sudo key, and will provide a count of active users in sourcegraph this month.

### Setting up and using Apollo Sandbox

❗️Open up [Sandbox}(https://studio.apollographql.com/sandbox/explorer)

Internally, we use the Apollo GraphQL Sandbox. 
Sandbox allows for the auto generation of the GraphQL docs and also has a neat search functionality to help you discover what exists on the schema. 
Sandbox also has a better developer experience with its one-click creation of operations. And unlike Postman, you do not need an account. 

❗️Show the configuration window

In the sandbox, the only configuration you need to do is drop in your endpoint URL and create an Authorization header.

Like in the API Console and Postman, if the schema is configured, control + space will show suggestions.

### Conclusion

And that's a wrap! In today's session, we covered the various APIs available, went into detail on how to use them and build some API calls, and set up tools to get started right away. 

### Resources 

* Download scripts available here: 
https://github.com/sourcegraph/customer-assets/tree/main/accounts/JPMC/scripts 
* Open the API Docs Page
* Download Postman
* Preconfigure Apollo Sandbox
* Make sure you’re logged into demo.sourcegraph.com
* Optional:
* Python GraphQL Scripts: https://gist.github.com/justdueck/4d8e76a489d3b1055d292be2d45cf27f 
* https://github.com/sourcegraph/customer-assets/blob/main/ce-tools/pysdk/sourcegraph/api_resources/search_apis.py 
* https://github.com/sourcegraph/customer-assets/blob/main/ce-tools/pysdk/sourcegraph/api_resources/repo_metadata_apis.py 
