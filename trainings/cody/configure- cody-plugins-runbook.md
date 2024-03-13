# Configure Cody Plugins
> The purpose of this run-book/script is to outline the steps required to configure a Cody plugin for an enterprise customer. Enabling a short session to be delivered to developers/engineers to enable them to get up and running with Cody. The assumption is that the audience will have a level of knowledge regarding Sourcegraph as a code search platform.

## Agenda
Today's session is going to cover the basics required to set up and configure Cody. The goal is for this session to last no longer than 15 minutes. I plan on covering the following topics:

1. Download and install of Cody plugin or extension for your IDE
2. Connecting the Cody plugin to a Sourcegraph Enterprise instance
3. How Cody uses Context when responding to your requests or actions
4. How to configure Cody context

## Installing and configuring Cody IDE Plugin

The first thing we need to do is install the Cody plugin for our IDE. Now in the interests of time, I have done this in advance. But I will show you in both VS Code and JetBrains where to find the relevant plugin or extension.

> I would suggest not downloading and installing the IDE plugin during the session. Purely based on this is a) straightforward for most people in the audience b) takes a little time to download etc. Rather install the plugin beforehand, show the installed extension and navigate to the relevant marketplace page via a browser or via the IDE plugin page. This confirms the name of the Cody plugin. Remove any account settings before starting so that we are not connected to a Sourcegraph enterprise instance.
> 
> Visual Studio Code <br>
> Select Code->Settings->Extensions type Cody AI in the dialog to show the installed extension. <br>
> Navigate to the marketplace url or select Marketplace on the extension page within VS Code <br>
>[Cody AI Visual Studio Code Marketplace](https://marketplace.visualstudio.com/items?itemName=sourcegraph.cody-ai) <br>
> 
> JetBrains <br>
> Select  IntelliJ->Settings->Plugins type Sourcegraph Cody in the dialog to show the installed plugin. <br>
> Navigate to the plugin url or select the shortcut from within IntelliJ <br>
>[Sourcegraph Cody JetBrains plugin](https://plugins.jetbrains.com/plugin/9682-sourcegraph-cody--code-search)
> 

### Configure Sourcegraph Enterprise Account
In terms of configuring Cody within your IDE it is pretty straightforward. The main task is to connect Cody to your Sourcegraph instance. Why is this important?

In short context.

> Open the browser with the blog [How Cody understands your codebase](https://sourcegraph.com/blog/how-cody-understands-your-codebase).

Context plays a crucial role in ensuring Cody provides accurate responses to your requests, whether it's through chat, predefined commands, or code completion. Cody leverages both local and remote context to enhance its understanding and effectiveness.

For autocomplete, Cody relies solely on local context, drawing from sources such as the contents of the active file, highlighted code, other open tabs, and recently closed tabs. On the other hand, for chat and commands, Cody utilizes both local and remote context.

To gather remote context, Cody interacts with the Sourcegraph instance associated with your IDE. It performs a search over selected repositories, preprocessing the user prompt by splitting it into tokens. These tokens are then processed by the Sourcegraph search engine, which scans the repositories indexed on your Sourcegraph instance and ranks file snippets based on their relevance to the search query. Cody combines the local and remote context, ranks the snippets, and sends the top N snippets along with the prompt to the Language Model (LLM).

Let us see how to connect Cody to a Sourcegraph instance.

> Outline adding an account with both VS Code and JetBrains. Point out that we do not want to use Cody Free or Pro tier but rather that we want to connect to an enterprise instance. Note - I need to determine how to remove previous instances on VS Code. On JetBrains remove existing accounts within Cody setting.
> 
> Visual Studio Code <br>
> 1. Select Cody extension<br>
> 2. Select Account<br>
> 3. Select Sign in to Enterprise instance<br>
> 4. Follow workflow<br>
> 
> JetBrains <br>
> 1. select Cody plugin<br>
> 2. select Sign in to Enterprise instance<br>
> 3. Follow workflow<br>

Now Cody is connected to our Sourcegraph instance we can ideally get better context to improve the responses we get from the LLM.

### Configuring Cody Plugin and Extension

> Outline additional (not required) configuration of Cody plugin/extension. Currently this is only relevant for VS Code. Outline options that can be enabled
> 1. Select Cody extension<br>
> 2. Select Settings<br>
> 3. Outline options that can be enabled<br>
> Code Actions, Editor Title Icon, Cody Lenses, Command Hints, Search Context <br>
> 

No further configuration is required of the plugin or extension. However, there are some additional options that can be selected in VS Code. In my view, it is useful to enable all of these options. Code Actions gives you the option to use Cody to fix or explain. We can add a Cody icon to the title bar as well as the status bar. Cody lenses adds a shortcut to your source code.  

## Configuring Cody Context

Previously we outlined how to connect our Cody plugin to a Sourcegraph instance so that Let us now take a look at we can configure remote context within Cody.

> 1. Open the relevant IDE used by the customer <br>
> 2. Open a folder or workspace associated with a repository indexed on the connected Sourcegraph instance. Show that the plugin picks up the remote repository. Explain that the workspace you have open is linked to a repository indexed on the connected Sourcegraph instance, leveraging git information for identification. <br>
> 3. Open a folder or workspace that is not associated with a repository indexed on the connected Sourcegraph instance. Show that the plugin does not pick up a remote repository. <br>
> 4. Mention any current limitations or issues, such as Cody's inability to automatically identify underlying projects within a GitLab group for example.
> 5. In VS Code, demonstrate creating a new chat tab, selecting the enhanced context dialog, and showing the relevant repository selected.
> 6. In IntelliJ (JetBrains), expand the context for the chat and show the repository used for remote context.
 
Expanding remote context in Cody allows you to add additional repositories, up to a maximum of 10. This feature enables you to incorporate repositories with relevant context, such as libraries, frameworks, or SDKs. These repositories may include public or open-source projects, enriching Cody's knowledge base. However, note that while the LLM is trained on versions of these libraries, it may not necessarily be up-to-date with the latest versions.

> Add an additional repository to the remote context used by Cody. (VS Code will provide a dialog to search available repos / JetBrains currently you will need to type repo url). Ideally, show how this improves a chat request. Suggest that using a maven or other package host will also demonstrate that sourcegraph can be used for indexing and searching third party repos relevant to the codebase. However not a requirement. For example, if using Sourcegraph/sourcegraph use Sourcegraph/Cody or Sourcegraph/sourcegraph-batch-examples.

So with Cody, we can set the repositories that we search for remote context. And we can control local context by selecting code and which files we have open in our IDE. We can 

Users can also have more granular control of Cody’s context by including @-files or @#-symbols in the chat input. This feature only supports local files and paths relative to your workspace. Start typing @, and Cody will suggest files for you to include. You can also specify which lines from a file you want to include.

> Show an example of using the @ to add specific local files/symbols. 

In this session, we have shown how to install and configure the Cody plugin. How to connect Cody to your Sourcegraph instance. Provided an overview of how Cody uses context. Shown how we can configure the repos Cody uses. And finally how we can specify specific files or symbols we want to use as context.
