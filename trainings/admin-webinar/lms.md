# Sourcegraph Admin Webinar

**Topic:** This content is intended to be delivered to users who will be admins on a new Sourcegraph instance. It covers the basic tasks they'll need to master in order to administer the instance. This is focused on in-app admin tasks primarily (rather than cluster maintenance, etc.). By the end of the course, a new admin should feel comfortable with basic user management and repo sync management tasks.

## Intro

As a new admin of a Sourcegraph instance, you'll be responsible for adding new users, adding new repos, and troubleshooting access issues. Our team is always willing to support these efforts, and this webinar exists to lay a foundational understanding of what admin tools are available to you.

## Unit 1: The Site Admin Menu

**Learning goals:** After completing this uint, you will be able to navigate the site admin menu and understand what function is available in each part of the site admin section of the instance.

### Accessing the site admin menu

To access the site admin section of the site, you'll need to click on your user icon and then select `Site admin`. If you don't see that option, that typically indicates that you have not yet been promoted to an admin—another admin user will need to promote you before continuing. 

![The site admin menu is accessed by clicking on your avatar image.](https://user-images.githubusercontent.com/9934079/174647300-7ae9f594-461b-4d82-b0fd-2127131cca00.png)

The site admin menu has 9 main sections:

* Statistics
* Configuration
* Repositories
* Code intelligence
* Users & auth
* Maintenance 
* Extensions
* Batch Changes
* API Console

In this course, we'll cover what's available in each section.

![The site admin section menu; clicking on each title will expand that section.](https://user-images.githubusercontent.com/9934079/174647435-0ed43274-a38a-4f70-89c0-bf040296d655.png)

### Statistics

The statistics overview page is the first one you'll see when clicking into the site admin menu. The overview page will show a quick summary of the number of users you have, how many are remaining on your license, and how much code is indexed on your instance. You'll also see a quick graph of weekly usage over the last 10 weeks.

The Usage stats section will show you more detailed user info—we'll discuss this in more detail in the next unit.

![The overview page, showing how many users are in the instance, current license status, and information about the volume of code on the instance.](https://user-images.githubusercontent.com/9934079/174647606-fa45041a-d17b-4367-b32b-9abda9c79b56.png)

Next up, we'll show the Configuration page.

### Configuration

The main area of the Configuration section that you'll need to focus on is the Site Configuration page. It's where you'll set the external URL, license key, code host OAuth or SAML, and experimental features, if you opt into them. When saving changes, you may need to restart the frontend pods/containers for your instance—if you do, we'll let you know in the UI that that's the case.

![The site settings page.](https://user-images.githubusercontent.com/9934079/174647889-039ec3ed-9dbc-47cf-9122-65e2ec168cf6.png)

The site configuration page will include site settings stored as JSON, shown above. Valid values for site configuration options are shown in the [Site Configuration docs page](https://docs.sourcegraph.com/admin/config/site_config).

If you wish to set the external URL for your instance, add a license key, or add a particular sign-in method, click the appropriate quick-add button above the text box to auto-add the JSON you'll need. This screenshot shows what will be inserted if you click the button to add a license key, for example:

![The site config JSON, with a highlighted addition of a `"licenseKey"` value.](https://user-images.githubusercontent.com/9934079/174648148-48092f33-8538-4660-947a-de3c0af1d8d3.png)

You may also set Global Settings on the Global Settings page. Though the name is similar to the Site Configuration page, the page shows different content. Here, you'll save anything that could go in user settings, but which applies to the entire instance—common examples are search snippets that you want accessible to the entire instance. In both the Global Settings and Site Configuration pages, we'll auto-suggest values as you type:

![The global settings page will auto-suggest valid values in the JSON as you type.](https://user-images.githubusercontent.com/9934079/174648315-8c17bb2c-c431-406c-beee-90cdfe51903c.png)

Valid Global Settings values are documented in the [Global Settings docs page](https://docs.sourcegraph.com/admin/config/settings#admin-config-settings-schema-json).

Clicking the `Add search snippet` button will auto-populate the JSON to add a new, shared [search snippet](https://docs.sourcegraph.com/code_search/how-to/snippets).

![Clicking the `Add search snippet` button will populate the JSON to add a new search snippet, shown here.](https://user-images.githubusercontent.com/9934079/174648623-c853e543-b437-4d81-9aff-759e8fe68153.png)

### Code intelligence

The Code Intelligence section will track the progress of uploads for [LSIF/SCIP precise code intelligence](https://docs.sourcegraph.com/code_intelligence/explanations/precise_code_intelligence). 

![The Code Intelligence Uploads page will show the status of all uploads. You can filter by status using the dropdown menu.](https://user-images.githubusercontent.com/9934079/174648829-6b351fa2-eacd-4bcb-9be3-e8512bcd49de.png)

Typically, you won't need to use this section very frequently, but may use it when investigating a failed precise code intelligence upload. To investigate the status of a single upload, you can click on the arrow next to its status.

![The landing page when clicking on an individual upload's status. It shows the upload status, timestamp, and commit hash.](https://user-images.githubusercontent.com/9934079/174648909-d6157d7f-5983-4de6-99e3-e1b766084e31.png)

The upload page will show the name of the repo being indexed (`github.com/sourcegraph/sourcegraph` in the screenshot above). It will also show the indexer used for that particular upload. One repo can have multiple indexers running against it; this is particularly common if you're indexing both frontend code and backend code for a single repo, as indexers are per-language. 

The `Auto-indexing` tab will show the same information as the `Uploads` tab; however, it displays information specific to repos configured with the experimental [auto-indexing feature](https://docs.sourcegraph.com/code_intelligence/how-to/enable_auto_indexing). If you're not sure if you have access to auto-indexing or if it's configured, reach out to your customer engineer or email support@sourcegraph.com. 

### Maintenance

The maintenance section is your go-to for information on the instance. If you notice performance issues with the instance or have questions about the health of the instance, this is the best place to start your investigation.

#### Updates 

The updates section will show if there are updates for your instance! We update once a month, with optional additional patch releases throughout the month. You can click to view the change-log on this page, as well. 

![The Updates page, showing that an update is available.](https://user-images.githubusercontent.com/9934079/174649588-dfa5815b-3373-4733-a3b2-93799ad8bb13.png)

As you can see in this screenshot, an update is available for this instance. Updates are covered in more detail in [our documentation](https://docs.sourcegraph.com/admin/updates). 

#### Documentation

Sourcegraph instances ship with their own copy of the docs site, also accessible at https://docs.sourcegraph.com. This is helpful if your site is air-gapped, as you'll still be able to view the content on the docs site, and is helpful generally because you'll view the docs at the version your instance is currently on. 

![The Documentation link will go directly to your local docs site.](https://user-images.githubusercontent.com/9934079/174649786-96166517-7cc4-444e-a77e-f9663998a02d.png)

Clicking on that link will bring you directly to the local docs site.

#### Pings

This page will allow you to copy the JSON of the pings being sent back to Sourcegraph, which contain aggregate user info (documented [here](https://docs.sourcegraph.com/admin/pings)). If you have an air-gapped instance, this will also be how you find the information to send to your Customer Engineer to ensure you're in compliance with your contract, or to provide information for troubleshooting.

![The JSON stored on the Pings page.](https://user-images.githubusercontent.com/9934079/174649898-bd047644-cacf-485d-87c6-25f96b61001b.png)

The ping data is stored as JSON and can be copied directly from this page.

Additionally, there is a "Report a bug" section. However, we encourage users with Customer Engineers to directly report the bug in Slack or via email to support@sourcegraph.com, or discuss it with their Customer Engineer; this will ensure the quickest resolution.

#### Migrations

This section tracks the progress of any migration run as part of an upgrade. Normally, you need to access this page—however, if there are issues which our support team believes might be related to a failed migration, this will be how you can confirm the status of any current or past migration.

![The migrations page, showing completed migrations and their status.](https://user-images.githubusercontent.com/9934079/174650129-7b6c296c-cdcf-45ae-a500-3b31065d60fb.png)

Similar to the Code Intelligence Uploads page, you can filter migrations by status.

#### Monitoring

Clicking the "monitoring" link will bring you to the Grafana instance which ships with your instance. You can set up alerting for passing certain thresholds in the Grafana instance; more information is [available in our docs](https://docs.sourcegraph.com/admin/observability/alerting). Our support team may ask you to review content in Grafana for troubleshooting.

![The main Grafana dashboard for the instance.](https://user-images.githubusercontent.com/9934079/174650252-29f9039a-0e25-4e2c-90d2-6892ec2fcd91.png)

The main dashboard will be your overall landing page for the instance; you can see currently-firing alerts in red, and whether they're warning alerts or critical. We also have a Git server dashboard (covering cloning/fetching of repos), a Frontend dashboard (general load and search response time; "frontend" covers more than just the frontend of the app), Repo Updater (connections to the code host), and Zoekt (indexing for search on Sourcegraph itself). To access the other dashboards, click the `Dashboards` icon and `Manage`.

![The Dashboards icon, with Manage selected.](https://user-images.githubusercontent.com/9934079/174650492-d65654e0-ee7d-4e2c-a9bb-d09c5379ffce.png)

Once on that page, you can search by dashboard name or manually navigate to the dashboard you want to look at.

![Searching for Git Server in the dashboard menu, showing the one result returned by the search.](https://user-images.githubusercontent.com/9934079/174650590-1f54b21b-94cc-4d1f-ad78-6300b5384e0f.png)

You can view a list of the included dashboards in our [documentation](https://docs.sourcegraph.com/admin/observability/dashboards). The list covers every single dashboard, so if you ever are looking for something that you can't find, reach out to your Customer Engineer for guidance. The Sourcegraph Grafana instance cannot be combined with your own pre-existing Grafana instance.

#### Tracing

Clicking Tracing will bring you to the in-app Jaeger install. This is mostly used for tracking the origins of slow queries with our Support team; you won't typically need to use this yourself, but may be asked for information from it if there are issues.

![Clicking on the Tracing link will bring you tothe in-app Jaeger install.](https://user-images.githubusercontent.com/9934079/174650842-16e1dbd5-f0ab-4781-958c-85759f107d6f.png)

More information on using Jaeger is available [in our documentation](https://docs.sourcegraph.com/admin/observability/tracing).

#### Instrumentation (Kubernetes-only)

If you're running a Kubernetes install, you'll also have access to the Instrumentation link in the Maintenance panel. Clicking this will bring you to a panel showing metrics for individual Kubernetes pods. You should not need to access the Instrumentation panel unless working with our support team.

### API Console

Finally, we have our API console. Clicking the link will open the console in your current tab. You can make GraphQL queries directly in the browser here; you can also use our [CLI](https://docs.sourcegraph.com/cli) or make the CURL requests directly.

![Sourcegraph's API console allows you to run queries against your live production data.](https://user-images.githubusercontent.com/9934079/174651053-a5e921fc-b89e-4d16-8fa8-416bdb65711c.png)

The API will run against your live production data, so be particularly careful when making mutation changes in the API console. 

### Conclusion

The admin section of the Sourcegraph site offers a variety of subsections that can help you troubleshoot issues with your instance or configure appropriate settings. However, the majority of your focus is likely going to be on managing users and adding repos, so we'll bulk of the rest of our time focused on that.

### Resources

* [Site Configuration docs page](https://docs.sourcegraph.com/admin/config/site_config)
* [Global Settings docs page](https://docs.sourcegraph.com/admin/config/settings#admin-config-settings-schema-json)
* [Pings docs page](https://docs.sourcegraph.com/admin/pings)
* [Grafana alerting](https://docs.sourcegraph.com/admin/observability/alerting)
* [Grafana dashboards](https://docs.sourcegraph.com/admin/observability/dashboards)

### Quiz

1. Where is a new license key added to the Sourcegraph instance?
  * A. Global settings
  * B. Admin's personal settings
  * C. __Site Config__
  * D. This is managed by the CE

2. In what circumstances might you need to access the Pings page?
  * A. To configure sending pings to Sourcegraph
  * B. __If your instance is air-gapped__
  * C. To disable pings to Sourcegraph
  * D. This is not needed

## Unit 2: Viewing and Exporting User Activity

**Learning goals:** After completing this unit, you will be able to export user activity and understand how to view a list of users.

### Viewing user activity

Sourcegraph shows admins individual user activity in-app. To see that, go to the Usage Stats page. From there, you can see a list of users and their page views, search queries, code intelligence actions, and last active information for the last 90 days. 

![The Usage stats page shows a graph of aggregate user info, as well as individual user action counts.](https://user-images.githubusercontent.com/9934079/174651576-e6040218-d160-4102-9647-deda59a654b8.png)

Rotating hosts can impact these numbers if Redis data is lost, so if the numbers don't seem to make sense, make sure that that hasn't happened. If it has, overall (aggregate) data will still be available from your Customer Engineer.

The numbers won't change if you select `Active today`, `Active this week`, etc. It impacts the list of users, but the numbers are all for the last 90 days. The list also cannot be sorted.

### Exporting user activity via CSV

As an instance admin, I may want to export usage statistics via CSV in order to analyze them in another tool. To do that, I can navigate to the Usage stats page, and click `Download usage stats archive`. That will give me a CSV of the last 90 days of user activity, separated per day. Though this isn't how we recommend pulling this info in an ongoing fashion (we recommend our API, instead), it will allow you to pull that list for the current date.

![Clicking the Download usage stats archive button will download a CSV of user activity.](https://user-images.githubusercontent.com/9934079/174651687-01e9d387-f144-45f9-a5bc-59b41f793814.png)

The download will contain two CSVs: `UsersDates.csv` and `UsersUsageCounts.csv`. The first will show the user IDs for the instance, and the creation and (if applicable) deletion date for each user:

![The contents of the UsersDates.csv file.](https://user-images.githubusercontent.com/9934079/174651939-318e4f17-824b-46db-895a-0730c9aabda8.png)

The `UsersUsageCounts.csv` will show a list of dates, a user ID, and the actions for that user on that date. Data is broken down per-user, per-date.

![The per-user, per-date data in the UsersUsageCounts.csv file.](https://user-images.githubusercontent.com/9934079/174652059-354f9479-babc-43cd-a30e-fe8fcebdb155.png)

It isn't possible to customize the date interval for the usage stats archive, or customize the content of it.

### Exporting user activity via the API

If I'm trying to pull usage activity in an ongoing fashion, the best approach is to use the API. This will show me user activity per user for the last 90 days. For example, running the query:

```
query{
	users(first:1000){
    nodes{
      username
      usageStatistics {
        lastActiveTime
        lastActiveCodeHostIntegrationTime
        searchQueries
        pageViews
        codeIntelligenceActions
        findReferencesActions
      }
    }
  }
}
```

will show me that information for the first 1,000 users in my instance. Similarly, I can pull DAU, WAU, and MAU numbers for my entire instance by running:

```
query{
	site{
    usageStatistics{
      daus {
        userCount
      }
      waus{
        userCount
      }
      maus{
        userCount
      }
    }
  }
}
```

If I want to see a list of this month's active users, that is also possible:

```
query {
  users(activePeriod: THIS_MONTH) {
    totalCount
    nodes {
      username,
      usageStatistics {
        lastActiveTime
      }
    	}
  }
}
```

Your Customer Engineer can also pull ad-hoc reports on usage if requested.

### Conclusion

User activity can be tracked in-app and via the API. This is the basis for user management, which we'll discuss in the next unit.

### Resources

* [Sourcegraph API](https://docs.sourcegraph.com/api/graphql)
* [Sourcegraph GraphQL examples](https://docs.sourcegraph.com/api/graphql/examples)

### Quiz

1. What sort of API does Sourcegraph have?
  * A. SOAP
  * B. REST
  * C. __GraphQL__
  * D. No API access is provided

2. How can you access user info about your instance?
  A. CSV export
  B. API calls
  C. __A and B__
  D. This is exclusively available from the CE

## Unit 3: User Management (In-App and Programatic)

**Learning goals:** After completing this unit, you will understand how to add and remove users in the app as well as via the API.

### Managing users in Sourcegraph

Sourcegraph bills per seat, rather than per active user. As a result, you may want to remove inactive accounts over time, or as part of your employee off-boarding process. This can be done in-app (best for one-off user removal) or via our API (best for ongoing or automated user management). User creation typically is less resource-intensive: unless configured otherwise, Sourcegraph will allow for Just In Time (JIT) user creation during signup, so that new users can log in as needed using the login method configured during instance standup.

If I want to remove a user or promote them to a site admin, I can do so in the Users page. To remove a user, I will click the trashcan icon. To promote them to a site admin, I'll click `Promote site admin`. I can also force sign out, if needed. This is very manual, but can be useful if you need to alter a specific user, quickly.

![Clicking the trashcan icon will allow me to delete a user—in this case, Alice.](https://user-images.githubusercontent.com/9934079/174653019-906af97d-c980-40aa-b6e5-457cd0b5ff1c.png)

When a user is removed from your identity provider or code host, they _will not_ be automatically logged out of Sourcegraph and their account will not automatically be deleted. You will need to manually force a sign-out, and/or delete the account. The urgency of this action can be minimized by configuring a short `auth.sessionExpiry` interval: [see documentation](https://docs.sourcegraph.com/admin/config/site_config#auth-sessionExpiry). This is why deleting the account, setting a short auth interval, or forcing a session termination is important. 

Permissions will sync from the code host, however, so even if the account remains in place without ending the current session, the user will only have access to public content as soon as their code host permissions are updated. For more information on this, please discuss with your Customer Engineer.

### Managing users via the API

More commonly, our customers manage users via the API. This is an easy way to remove inactive users; we recommend removing inactive users once a quarter. (Because user activity data is stored for 90 days, we do not recommend waiting longer than 3 months.)

To do that, your Customer Engineer will provide a script to you, or you can write your own using our graphQL API. In the script that the CE will provide, you'll follow the following format to remove users:

```
python3 cleanup_users.py -e http://sourcegraph.example.com -a YOUR_sudo_ACCESS_TOKEN -u YOUR_USERNAME -d 90
```

You'll need to change your Sourcegraph external URL, provide your token, and provide your username. The `-d 90` is set to remove users inactive in the last 90 days; you can of course change that number depending on how you wish to run the script. It's worth noting that if a user is deleted and attempts to log in again, they will not have access to their saved search info or account customization—a brand new account will be created. As a result, we recommend only running this script once a quarter, to avoid unnecessary deletions. 

Alternatively, you can remove an individual user using the CLI. To do that, run `src users delete -id=$(src users get -f='{{.ID}}' -username=alice)`, swapping the `alice` for your user's username. For more information on the user deletion command, run `src user delete -h` in the CLI, which will show the flags that that command takes.

![The results of running `src user delete -h` in the author's terminal.](https://user-images.githubusercontent.com/9934079/174653791-74617c9a-e3a9-47a0-b618-1a58afd141c9.png)

### Conclusion

User management is important, and with tools provided by your CE, should take up relatively little of your time. It is the most common task taken on by our instance admins after repo management, which we'll cover next.

### Resources

* [Sourcegraph customer assets repo](https://github.com/sourcegraph/customer-assets/tree/main/ce-tools/pysdk) (Private, will need to be granted access by your CE.)
* [CLI documentation](https://docs.sourcegraph.com/cli)

### Quiz

1. How do you remove users from the app?
  * A. In-app user management
  * B. Via the API
  * C. Ask your CE
  * D. __A and B__

2. Are users automatically removed from Sourcegraph if they're removed from your identity provider?
  * A. Yes, if using code host OAuth
  * B. Yes, if using SAML
  * C. Yes, if using username/password
  * D. __No__ 

## Unit 4: Adding New Repos and Troubleshooting Repo Sync

**Learning goals:** After completing this unit, you should feel comfortable adding a repository and troubleshooting repo sync issues.

### Adding a repository

One of the most important tasks an instance admin may find themselves taking on is adding new repos to the instance. Repos are pulled in via code host connections, visible on the Manage code hosts page. 

![The Manage code hosts page, showing a list of all code host connections on the instance.](https://user-images.githubusercontent.com/9934079/174654107-546fd394-9c52-4145-9acd-65dd2e6080b8.png)

A code host connection consists of an access token for a specific code host and a list of repos that should sync using the connection. You can have multiple code hosts for an instance (connecting to multiple GitHub instances, or a GitHub and a GitLab instance), or can connect to the same code host multiple times in different code host objects (connecting to the same GitHub instance using two different access tokens). Where possible, we recommend using a minimum number of code host connections—ideally one per instance.

You'll also set permissions syncing on the code host record. This shouldn't require modification over the life of the code host, but if you see an `authorization` value in the JSON, that's what it's controlling. Because code hosts use a personal access token (PAT) or machine user token, the token in question will need to have access to all the repos you need to sync; if you try to add a repo that isn't available to that token, sync will fail. 

If you click `edit` on the code host record, you can see a list of what repos are being synced over. Usually, this will be a list of orgs or groups, where all the repos in the org/group are synced—this is more efficient than listing each repo individually. But, if you need to add an org or group or an individual repo, this is where you do that. The code host config JSON will have a list of quick-add buttons above it which cover the most common tasks (adding a single repo, adding an org, etc.):

![The code host settings for a GitHub codehost syncing the sourcegraph-testing org, with permissions enforced.](https://user-images.githubusercontent.com/9934079/174654325-527e8724-b0bd-4f8a-a384-2226100257ab.png)

### Checking repository status

If a user reports a repo isn't syncing, you'll want to go to the Repository status page. From there, you can search for the repo name. If it doesn't show up at all, add it to the code host connection, and make sure the PAT in place has access to the repo. 

![Searching for the repo name on the Repository Status page will show its status on the instance, if it's being synced.](https://user-images.githubusercontent.com/9934079/174654487-3d758784-0b72-46df-9588-d0b049611fa3.png)


If the repo shows in search results, you can click into the Settings button to see more info about sync status.

![The Indexing tab for the main Sourcegraph repo, showing when it was last indexed.](https://user-images.githubusercontent.com/9934079/174654601-b323c610-e7df-4022-84db-7e16a2c54995.png)

The Indexing tab will show the commit that was last indexed. The Mirroring and Permissions tabs will typically be most helpful to troubleshooting. Going to the Mirroring tab will let you see when the repo was last refreshed, and show you whether or not the remote URL for the repo is reachable. 

![The Mirroring tab for the main Sourcegraph repo.](https://user-images.githubusercontent.com/9934079/174654669-3d4772d5-305d-4edd-a9e8-cab25bf6a607.png)

You can click `Refresh now` to force a sync or `Check connection` to check the current status of the connection to the remote. If there's an error being returned, you'll see it here, and can troubleshoot appropriately.

![The Permissions tab for the main Sourcegraph repo.](https://user-images.githubusercontent.com/9934079/174654740-f371444f-a3f3-498b-8222-52e752a511dc.png)

The Permissions tab will show the last time the permissions were synced for the repo, if enabled. If the repo is on the instance but a user cannot access the repo like you'd expect, you can force a resync of permissions here. You can also go to the Users section, click on the username, and go to the Permissions tab for the user, and resync permissions for just that user.

![The permissions status for an individual user, showing the button to sync permsisions manually.](https://user-images.githubusercontent.com/9934079/174654852-c8766d60-86e0-4a3a-9986-9009036b3a8e.png)

Which option you pick will depend on whether you're seeing issues for the repo with multiple people, or for just that user. 

### Conclusion

Being able to find repo status on your own will allow you to troubleshoot repo issues without needing to wait on Sourcegraph support, and will allow you to provide an error message directly to the support team if you need to loop them in. The final aspect of instance management we'll touch on is how to configure global search contexts for your users.

### Resources

* [Code host connections](https://docs.sourcegraph.com/admin/external_service)

### Quiz

1. How can you check if a repo is being synced to the instance?
  * A. Ask your users
  * B. Ask your CE
  * C. __Check the code host settings in-app__
  * D. Ask your CE

2. Where are code host permissions enforced?
  * A. Site settings
  * B. __Code host config__
  * C. Manually configured in the DB
  * D. Sourcegraph doesn't support this

## Unit 5: Adding Global Search Contexts

**Learning goals:** After completing this unit, you will understand how to add a global search context to the instance.

### Adding search contexts

As part of your work administering the instance, you may be asked to set up global search contexts. Search contexts are used to filter search results to a particular portion of the codebase—for example, if your company builds a new product, they may want a search context that will just show code related to that particular product. As an admin, you'll be able to add global search contexts, visible to all users on the instance. You can read more about search contexts [in our documentation](https://docs.sourcegraph.com/code_search/how-to/search_contexts).

To add a new search context, click on the `global` dropdown on your search query, and click `Manage contexts.`

![The global dropdown, showing the Manage Contexts link.](https://user-images.githubusercontent.com/9934079/174655078-3afcadd3-8eea-4ba9-b036-e86f59d992e9.png)

From there, you can create a new search context. To make a new global search context, you'll want to make sure that the owner is selected from the dropdown menu as `Global owner`:

![The dropdown menu, showing the Global Owner option.](https://user-images.githubusercontent.com/9934079/174655224-03ff8dd2-42f0-4fd9-b7be-581b1a267787.png)

You'll also need to make sure that visibility for the context is set to Public. If not, only site admins will be able to view the context:

![The selection menu showing private/public search context visibility.](https://user-images.githubusercontent.com/9934079/174655346-d6366120-e6f7-4240-a334-0e7f7c4982b5.png)

Once the appropriate ownership and visibility content is selected, you'll be able to specify the query that will power the context. In this example, I'm looking for content in the main Sourcegraph repo, but only in JavaScript language files.

![A configured search context query to limit searches to the main Sourcegraph repo, in JavaScript language files.](https://user-images.githubusercontent.com/9934079/174655488-ef5efe9c-2eae-49a1-bb0f-8a56dc8b0872.png)

You can edit or delete existing search contexts by clicking on their names on the search contexts page. From there, you can click `Edit` and change or delete them.

### Conclusion 

Adding search contexts will ensure that Sourcegraph search is maximally useful to your team, and as an admin you'll be able to create global contexts to share. This, combined with user management and other key site admin functionality, will ensure that you have the best overall experience managing the Sourcegraph instance.

### Resources

* [Search contexts](https://docs.sourcegraph.com/code_search/how-to/search_contexts)

### Quiz

1. What is a search context?
  * A. Extra info about a search
  * B. A one-click saved search
  * C. A note to self
  * D. __A way of scoping searches to a specific query__

2. Why is it good to add search contexts?
  * A. __It will make Sourecegraph maximally useful to your team__
  * B. It makes search results more accurate
  * C. It will make searches quicker
  * D. It isn't


