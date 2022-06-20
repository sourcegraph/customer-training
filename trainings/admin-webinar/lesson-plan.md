# Sourcegraph Admin Webinar

**Topic:** This webinar is intended to be delivered to users who will be admins on a new Sourcegraph instance. It covers the basic tasks they'll need to master in order to administer the instance. This is focused on in-app admin tasks primarily (rather than cluster maintenance, etc.). By the end of the webinar, a new admin should feel comfortable with basic user management and repo sync management tasks.

## Intro

As a new admin of a Sourcegraph instance, you'll be responsible for adding new users, adding new repos, and troubleshooting access issues. Our team is always willing to support these efforts, and this webinar exists to lay a foundational understanding of what admin tools are available to you.

## Unit 1: The Site Admin Menu

**Learning goals:** The customer will be able to navigate the site admin menu and understand what function is available in each part of the site admin section of the instance.

### Accessing the site admin menu

To access the site admin section of the site, you'll need to click on your user icon and then select `Site admin`. If you don't see that option, that typically indicates that you have not yet been promoted to an admin—another admin user will need to promote you. The site admin menu has 9 main sections:

* Statistics
* Configuration
* Repositories
* Code intelligence
* Users & auth
* Maintenance 
* Extensions
* Batch Changes
* API Console

Today, we'll cover what's available in each section.

🔎 The trainer should demonstrate:

* How to access the Site Admin section
* The menu which shows the subsection

### Statistics

The statistics page is the first one you'll see when clicking into the site admin menu. The overview page will show a quick summary of the number of users you have, how many are remaining on your license, and how much code is indexed on your instance. You'll also see a quick graph of weekly usage over the last 10 weeks.

The Usage stats section will show you more detailed user info—we'll discuss this in more detail in the next unit.

🔎 The trainer should demonstrate:

* The overview page
* The graph on the overview page
* Where license and usage information are available on the overview page

Next up, we'll show the Configuration page.

### Configuration

The main area of the Configuration section that you'll need to focus on is the Site Configuration page. It's where you'll set the external URL, license key, code host OAuth or SAML, and experimental features, if you opt into them. When saving changes, you may need to restart the frontend pods/containers for your instance—if you do, we'll let you know in the UI that that's the case.

🔎 The trainer should demonstrate:

* Where site settings are stored
* How to click the sample buttons ("set external URL", "set license key") to add the appropriate JSON to the settings
* The [Site Configuration docs page](https://docs.sourcegraph.com/admin/config/site_config)

You may also set Global Settings. Though the name is similar to the Site Configuration page, the page shows different content. Here, you'll save anything that could go in user settings, but which applies to the entire instance—common examples are search snippets that you want accessible to the entire instance. In both the Global Settings and Site Configuration pages, we'll auto-suggest values as you type.

🔎 The trainer should demonstrate:

* How typing in the Global Settings box will generate an auto-complete tooltip
* Adding a new search snippet
* The [Global Settings docs page](https://docs.sourcegraph.com/admin/config/settings#admin-config-settings-schema-json)

❗️If a customer asks about the Feature flags or License pages, you're welcome to show them to the user, but you can be direct in saying that those sections tend not to be as relevant. (License info is duplicated in the Overview section, and the Feature flags page isn't relevant to customer instances.)

### Code intelligence

The Code Intelligence section will track the progress of uploads for LSIF/SCIP precise code intelligence. Typically, you won't need to use this section, but may use it when investigating a failed precise code intelligence upload. To investigate the status of a single upload, you can click on the arrow next to its status.

🔎 The trainer should demonstrate:

* How to view what repo is being indexed
* How to view what indexer is being used
* How to filter to show errored uploads
* How to click in to see more information about the upload

❗️ If the customer has no plans to enable precise code intel, this section may be dropped in the interests of time, or covered in less detail. You may also want to show the Auto-indexing section if the customer is participating in the Auto-indexing beta—the content is the same as the main Uploads page, but shows the auto-upload managed uploads. 

### Maintenance

The maintenance section is your go-to for information on the instance. 

#### Updates 

The updates section will show if there are updates for your instance! We update once a month, with optional additional patch releases throughout the month. You can click to view the change-log on this page, as well. 

🔎 The trainer should demonstrate:

* How to see if there's an available update
* How to view the change-log

#### Documentation

Sourcegraph instances ship with their own copy of the docs site, also accessible at https://docs.sourcegraph.com. This is helpful if your site is air-gapped, as you'll still be able to view the content on the docs site, and is helpful generally because you'll view the docs at the version your instance is currently on. 

🔎 The trainer should demonstrate:

* The Docs site link

❗️ The Demo link will go directly to the main docs site for its current version, because of being on a subdomain of sourcegraph.com. 

#### Pings

This page will allow you to copy the JSON of the pings being sent back to Sourcegraph, which contain aggregate user info (documented [here](https://docs.sourcegraph.com/admin/pings)). If you have an air-gapped instance, this will also be how you find the information to send to your CE to ensure you're in compliance with your contract, or to provide information for troubleshooting.

🔎 The trainer should demonstrate:

* How to copy the ping contents to send

❗️There is a "Report a bug" section. However, encourage the user to simply directly report the bug in Slack or via email to support@sourcegraph.com, or discuss it with you. 

#### Migrations

This section tracks the progress of any migration run as part of an upgrade. Normally, you won't pay attention to this page—however, if there are issues which our support team believes might be related to a failed migration, this will be how you can confirm the status of any current or past migration.

🔎 The trainer should demonstrate:

* How to click in to capture more information about the migration if there were errors

#### Monitoring

Clicking the "monitoring" link will bring you to the Grafana instance which ships with your instance. You can set up alerting for passing certain thresholds in the Grafana instance; more information is available in our docs. Our support team may ask you to review content in Grafana for troubleshooting.

The main dashboard will be your overall landing page for the instance; you can see currently-firing alerts in red, and whether they're warning alerts or critical. We also have a Git server dashboard (covering cloning/fetching of repos), a Frontend dashboard (general load and search response time; "frontend" covers more than just the frontend of the app), Repo Updater (connections to the code host), and Zoekt (indexing for search on Sourcegraph itself). 

🔎 The trainer should demonstrate:

* How to access the Grafana dashboards (and the main dashboard, gitserver, frontend, repoupdater, and zoekt dashboards)
* How to configure alerts for Grafana ([documentation](https://docs.sourcegraph.com/admin/observability/alerting))
* How to view a list of the included dashboards ([documentation](https://docs.sourcegraph.com/admin/observability/dashboards))

#### Tracing

Clicking Tracing will bring you to the in-app Jaeger install. This is mostly used for tracking the origins of slow queries with our Support team; you won't need to use this yourself typically, but may be asked for information from it if there are issues.

🔎 The trainer should demonstrate:

* How to access Jaeger

❗️ As executors sponsor beta/experimental features currently, they aren't included in this training. However, you can show the customer the running executors on Demo if they have any questions.

#### Instrumentation (Kubernetes-only)

If you're running a Kubernetes install, you'll also have access to the Instrumentation link in the Maintenance panel. Clicking this will bring you to a panel showing metrics for individual Kubernetes pods. You should not need to access the Instrumentation panel unless working with our support team.

🔎 The trainer should demonstrate:

* How to access the Instrumentation panel on a Kubernetes install (sourcegraph.com will work)

❗️ If the customer isn't a Kubernetes customer, skip this section.

❗️ The Extensions page and Batch Changes page are typically only relevant to customers setting up a custom extension or setting up a single access token for Batch Changes. As those both would involve CE enablement at the time of configuration, they're not included in this webinar.

### API Console

Finally, we have our API console. You can make GraphQL queries directly in the browser here; you can also use our CLI or make the CURL requests directly.

🔎 The trainer should demonstrate:

* Running a basic graphQL query

### Conclusion

The admin section of the Sourcegraph site offers a variety of subsections that can help you troubleshoot issues with your instance or configure appropriate settings. However, the majority of your focus is likely going to be on managing users and adding repos, so we'll bulk of the rest of our time focused on that.

### Resources

* [Site Configuration docs page](https://docs.sourcegraph.com/admin/config/site_config)
* [Global Settings docs page](https://docs.sourcegraph.com/admin/config/settings#admin-config-settings-schema-json)
* [Pings docs page](https://docs.sourcegraph.com/admin/pings)
* [Grafana alerting](https://docs.sourcegraph.com/admin/observability/alerting)
* [Grafana dashboards](https://docs.sourcegraph.com/admin/observability/dashboards)

## Unit 2: Viewing and Exporting User Activity

**Learning goals:** After completing this unit, the customer will be able to export user activity and understand how to view a list of users.

### Viewing user activity

Sourcegraph shows admins individual user activity in-app. To see that, go to the Usage Stats page. From there, you can see a list of users and their page views, search queries, code intelligence actions, and last active information for the last 90 days. 

❗️ Rotating hosts can impact these numbers if Redis data is lost, so if the numbers don't seem to make sense, make sure that that hasn't happened. If it has, overall (aggregate) data will still be available from the CE.

❗️ The numbers won't change if you select `Active today`, `Active this week`, etc. It simply impacts the list of users, but the numbers are all for the last 90 days. The list also cannot be sorted.

🔎 The trainer should show:

* How to access the list of user data
* How to read the user data for a particular user

### Exporting user activity via CSV

As an instance admin, I may want to export usage statistics via CSV in order to analyze them in another tool. To do that, I can navigate to the Usage stats page, and click `Download usage stats archive`. That will give me a CSV of the last 90 days of user activity, separated per day. Though this isn't how we recommend pulling this info in an ongoing fashion (we recommend our API, instead), it will allow you to pull that list for the current date.

❗️ It isn't possible to customize the date interval for the usage stats archive, or customize the content of it.

🔎 The trainer should demonstrate:

* How to export the CSV
* What the CSV contains

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

Your CE can also pull ad-hoc reports on usage if requested.

🔎 The trainer should demonstrate:

* Running an API query to view activity for individual users
* Running an API query to view overall DAU, WAU, and MAU 
* Running an API query to view this month's active users

### Conclusion

User activity can be tracked in-app and via the API. This is the basis for user management, which we'll discuss in the next unit.

### Resources

* [Sourcegraph API](https://docs.sourcegraph.com/api/graphql)
* [Sourcegraph GraphQL examples](https://docs.sourcegraph.com/api/graphql/examples)


## Unit 3: User Management (In-App and Programatic)

**Learning goals:** After completing this unit, the customer will understand how to add and remove users in the app as well as via the API.

### Managing users in Sourcegraph

Sourcegraph bills per seat, rather than per active user. As a result, you may want to remove inactive accounts over time, or as part of your employee off-boarding process. This can be done in-app (best for one-off user removal) or via our API (best for ongoing or automated user management). User creation typically is less resource-intensive: unless configured otherwise, Sourcegraph will allow for Just In Time (JIT) user creation during signup, so that new users can log in as needed using the login method configured during instance standup.

❗️ This section is necessarily a little generic because the details will vary per customer. Typically at this point you will want to speak specifically to what the customer has configured for account creation.

If I want to remove a user or promote them to a site admin, I can do so in the Users page. To remove a user, I will click the trashcan icon. To promote them to a site admin, I'll click `Promote site admin`. I can also force sign out, if needed. This is very manual, but can be useful if you need to alter a specific user, quickly.

❗️ When a user is removed from the customer's identity provider, they will not automatically be logged out of Sourcegraph and their account will not automatically be deleted. The customer will need to manually force a sign-out, or delete the account. The urgency can be minimized by configuring a short `auth.sessionExpiry` interval: https://docs.sourcegraph.com/admin/config/site_config#auth-sessionExpiry. Permissions will sync, however, so even if the account remains in place without ending the current session, scope of access is likely minimal. 

🔎 The trainer should demonstrate:

* How to promote a user to site admin in-app
* How to delete a user in-app
* How to reset a user password in-app *if* the customer is using username/password (uncommon)

### Managing users via the API

More commonly, our customers manage users via the API. This is an easy way to remove inactive users; we recommend removing inactive users once a quarter. (Because user activity data is stored for 90 days, we do not recommend waiting longer than 3 months.)


To do that, your CE will provide a script to you, or you can write your own using our graphQL API. In the script that the CE will provide, you'll follow the following format to remove users:

```
python3 cleanup_users.py -e http://sourcegraph.example.com -a YOUR_sudo_ACCESS_TOKEN -u YOUR_USERNAME -d 90
```

You'll need to change your Sourcegraph external URL, provide your token, and provide your username. The `-d 90` is set to remove users inactive in the last 90 days; you can of course change that number depending on how you wish to run the script. It's worth noting that if a user is deleted and attempts to log in again, they will not have access to their saved search info or account customization—a brand new account will be created. As a result, we recommend only running this script once a quarter. 

Alternatively, you can remove an individual user using the CLI. To do that, run `src users delete -id=$(src users get -f='{{.ID}}' -username=alice)`, swapping the `alice` for your user's username.

🔎 The trainer should demonstrate:

* The user management script stored at https://github.com/sourcegraph/customer-assets (this is not a public repo, so the CE can share the information but the user cannot access the repo; you'll need to send the script as a zip file instead)
* The results of running `src user delete -h` in the CLI, which walks through the various deletion options

### Conclusion

User management is important, and with tools provided by your CE, should take up relatively little of your time. It is the most common task taken on by our instance admins after repo management, which we'll cover next.

### Resources

* [Sourcegraph customer assets repo](https://github.com/sourcegraph/customer-assets)
* [CLI documentation](https://docs.sourcegraph.com/cli)

## Unit 4: Adding New Repos and Troubleshooting Repo Sync

**Learning goals:** After completing this unit, the customer should feel comfortable adding a repository and troubleshooting repo sync issues.

### Adding a repository

One of the most important tasks an instance admin may find themselves taking on is adding new repos to the instance. Repos are pulled in via code host connections, visible on the Manage code hosts page. A code host connection consists of an access token for a specific code host and a list of repos that should sync using the connection. You can have multiple code hosts for an instance (connecting to multiple GitHub instances, or a GitHub and a GitLab instance), or can connect to the same code host multiple times in different code host objects (connecting to the same GitHub instance using two different access tokens). Where possible, we recommend using a minimum number of code host connections—ideally one per instance.

You'll also set permissions syncing on the code host record. This shouldn't require modification over the life of the code host, but if you see an `authorization` value in the JSON, that's what it's controlling. Because code hosts use a PAT or machine user token, the token in question will need to have access to all the repos you need to sync; if you try to add a repo that isn't available to that token, sync will fail. 

If you click `edit` on the code host record, you can see a list of what repos are being synced over. Usually, this will be a list of orgs or groups, where all the repos in the org/group are synced—this is more efficient than listing each repo individually. But, if you need to add an org or group or an individual repo, this is where you do that.

🔎 The trainer should show:

* The Manage code hosts page
* How to add a new repo/project/group/org to an existing code host record
* How to toggle permission enforcement using the `Enforce permissions` button

### Checking repository status

If a user reports a repo isn't syncing, you'll want to go to the Repository status page. From there, you can search for the repo name. If it doesn't show up at all, add it to the code host connection, and make sure the PAT in place has access to the repo. But if the repo shows up, you can click into the Settings button to see more info about sync status.

The Indexing tab will show the commit that was last indexed. The Mirroring and Permissions tabs will typically be most helpful to troubleshooting. Going to the Mirroring tab will let you see when the repo was last refreshed, and show you whether or not the remote URL for the repo is reachable. You can click `Refresh now` to force a sync or `Check connection` to check the current status of the connection to the remote. If there's an error being returned, you'll see it here, and can troubleshoot appropriately.

The Permissions tab will show the last time the permissions were synced for the repo, if enabled. If the repo is on the instance but a user cannot access the repo like you'd expect, you can force a resync of permissions here. You can also go to the Users section, click on the username, and go to the Permissions tab for the user, and resync permissions for just that user. Which you pick will depend on whether you're seeing issues for the repo with multiple people, or for just that user. 

🔎 The trainer should demonstrate:

* How to find a repo on the Repository status page
* How to open settings for a repo
* How to force a repo sync and check remote connection status
* How to force a perms resync for a repo
* How to force a perms resync for a user

### Conclusion

Being able to find repo status on your own will allow you to troubleshoot repo issues without needing to wait on Sourcegraph support, and will allow you to provide an error message directly to the support team if you need to loop them in. The final aspect we'll touch on is how to configure global search contexts for your users.

### Resources

* [Code host connections](https://docs.sourcegraph.com/admin/external_service)

## Unit 5: Adding Global Search Contexts

**Learning goals:** After completing this unit, an admin should understand how to add a global search context to the instance.

### Adding search contexts

As part of your work administering the instance, you may be asked to set up global search contexts. Search contexts are used to filter search results to a particular portion of the codebase—for example, if your company builds a new product, they may want a search context that will just show code related to that particular product. As an admin, you'll be able to add global search contexts, visible to all users on the instance.

🔎 The trainer should demonstrate:

* How to navigate to the search context creation menu
* How to add a new query-based search context
* How to ensure it's globally visible
* How to edit or remove an existing search context

### Conclusion 

Adding search contexts will ensure that Sourcegraph search is maximally useful to your team, and as an admin you'll be able to create global contexts to share. This, combined with user management and other key site admin functionality, will ensure that you have the best overall experience managing the Sourcegraph instance.

### Resources

* [Search contexts](https://docs.sourcegraph.com/code_search/how-to/search_contexts)
