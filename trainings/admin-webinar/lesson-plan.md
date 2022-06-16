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

The updates section will show if there are updates for your instance! We update once a month, with optional addional patch releases throughout the month. You can click to view the changelog on this page, as well. 

🔎 The trainer should demonstrate:

* How to see if there's an available update
* How to view the changelog

#### Documentation

Sourcegraph instances ship with their own copy of the docs site, also accessible at https://docs.sourcegraph.com. This is helpful if your site is airgapped, as you'll still be able to view the content on the docs site, and is helpful generally because you'll view the docs at the version your instance is currently on. 

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

🔎 The trainer should demonstrate:

* How to access the Grafana dashboards
* How to configure alerts for Grafana ([documentation](https://docs.sourcegraph.com/admin/observability/alerting))
* How to view a list of the included dashboards ([documentation](https://docs.sourcegraph.com/admin/observability/dashboards))

#### Tracing

Clicking Tracing will bring you to the in-app Jaeger install. This is mostly used for tracking the origins of slow queries with our Support team; you won't need to use this yourself typically, but may be asked for information from it if there are issues.

🔎 The trainer should demonstrate:

* How to access Jaeger

❗️ As executors sponsor beta/experimental features currently, they aren't included in this training. However, you can show the customer the running executors on Demo if they have any questions.

#### Instrumentation (Kubernetes-only)

If you're running a Kuberentes install, you'll also have access to the Instrumentation link in the Maintenance panel. Clicking this will bring you to a panel showing metrics for individual kubernetes pods. You should not need to access the Instrumentation panel unless working with our support team.

🔎 The trainer should demonstrate:

* How to acecss the Instrumentation panel on a Kubernetes install (sourcegraph.com will work)

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

**Learning goals:** 

### What is Sourcegraph?

### Conclusion

### Resources

## Unit 3: User Management (In-App and Programatic)

**Learning goals:** 

### What is Sourcegraph?

### Conclusion

### Resources

## Unit 4: Adding New Repos and Troubleshooting Repo Sync

**Learning goals:** 

### What is Sourcegraph?

### Conclusion

### Resources

## Unit 5: Adding Global Search Contexts
