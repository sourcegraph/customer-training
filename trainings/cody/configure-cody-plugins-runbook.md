# Configure Cody Plugins
> The purpose of this run-book/script is to outline the steps required to configure a Cody plugin for an enterprise customer. Enabling a short session to be delivered to developers/engineers to enable them to get up and running with Cody.

## Agenda
Today's session is going to cover the basics required to set up and configure Cody. The goal is for this session to last no longer than 15 minutes. I plan on covering the following topics:

1. Download and install of Cody plugin or extension for your IDE
2. Connecting the Cody plugin to a Sourcegraph Enterprise instance
3. How Cody uses Context when responding to your requests or actions
4. How to configure Cody context

## Installing and configuring Cody IDE Plugin

The first thing we need to do is install the Cody plugin for our IDE using the following instructions.

> 
> Visual Studio Code <br>
>
> Select Code->Settings->Extensions type Cody AI in the dialog to show the extension page. <br>
> Go to the Cody marketplace page using the following link [Cody AI Visual Studio Code Marketplace](https://marketplace.visualstudio.com/items?itemName=sourcegraph.cody-ai) <br>
> or select Marketplace on the extension page to download the extension. And then install. Alternatively install it directly from within the extension page <br>
> 
> JetBrains <br>
>
> Select Settings->Plugins and type Sourcegraph Cody in the dialog to show the plugin page. <br>
> Go to the Cody marketplace page using the following link [Sourcegraph Cody JetBrains plugin](https://plugins.jetbrains.com/plugin/9682-sourcegraph-cody--code-search) <br>
> or use link from within your JetBrains IDE to download the plugin. And then install. Alternatively install it directly from within the plugin page <br>
> 

### Configure Sourcegraph Enterprise Account
In terms of configuring Cody within your IDE it is pretty straightforward. The main task is to connect Cody to your Sourcegraph instance. 

Why is this important?

In short context.

> Open the following blog [How Cody understands your codebase](https://sourcegraph.com/blog/how-cody-understands-your-codebase) to read more detail about how Cody uses context.

Context plays a crucial role in ensuring Cody provides accurate responses to your requests, whether it's through chat, predefined commands, or code completion. Cody leverages both local and remote context to enhance its understanding and effectiveness.

For autocomplete, Cody relies solely on local context, drawing from sources such as the contents of the active file, highlighted code, other open tabs, and recently closed tabs. On the other hand, for chat and commands, Cody utilizes both local and remote context.

To gather remote context, Cody interacts with the Sourcegraph instance associated with your IDE. It performs a search over selected repositories, preprocessing the user prompt by splitting it into tokens. These tokens are then processed by the Sourcegraph search engine, which scans the repositories indexed on your Sourcegraph instance and ranks file snippets based on their relevance to the search query. Cody combines the local and remote context, ranks the snippets, and sends the top N snippets along with the prompt to the Language Model (LLM).

Let us see how to connect Cody to a Sourcegraph instance. In this case we do not want to use Cody Free or Pro tier but rather that we want to connect to an enterprise instance. So ignore options to sign in with GitHub, GitLab or Google. The workflow is very similar in Visual Studio Code and JetBrains. Both involve specifying the url of your Sourcegraph instance. With Visual Studio Code it will automatically generate a token on your Sourcegraph instance and copy that to your IDE. In JetBrains it will prompt you to copy the token and then paste the token into a dialog on your IDE.
> 
> Visual Studio Code <br>
>
> 1. Select Cody extension<br>
> 2. Select Account<br>
> 3. Select Sign in to Enterprise instance<br>
> 4. Follow workflow<br>
> 
> JetBrains <br>
> 
> 1. select Cody plugin<br>
> 2. select Sign in to Enterprise instance<br>
> 3. Follow workflow<br>

Now Cody is connected to our Sourcegraph instance we can ideally get better context to improve the responses we get from the LLM.

### Configuring Cody Plugin and Extension

No further configuration is required. However, there are some additional options that can be selected in VS Code. I would suggest to enable all of these options. 

* Code Actions gives you the option to use Cody to fix or explain
* Title Icon adds a Cody icon to the title bar as well as the status bar
* Cody lenses adds a shortcut to your source code.  

> Outline options that can be enabled for Visual Studio Code
> 1. Select Cody extension<br>
> 2. Select Settings<br>
> 3. Enable following options <br> Code Actions, Editor Title Icon, Cody Lenses, Command Hints, Search Context <br>
> 

## Configuring Cody Context

Previously we outlined how to connect our Cody plugin to a Sourcegraph instance so that we benefit from context available within our Sourcegraph instance. Let us now take a look at we can configure remote context within Cody.

> 1. Open your IDE <br>
> 2. Open a folder or workspace containing a repository indexed on the connected Sourcegraph instance. Show that the plugin picks up the remote repository. In VS Code, create a new chat tab, select the enhanced context dialog and show the that the repository is selected. In IntelliJ (JetBrains), in the chat pane expand the context for the chat and show that the repository is used for remote context. <br>
> 5. Open a folder or workspace that does not contain a repository indexed on the connected Sourcegraph instance. Repeat the above steps and we can see that no remote repository is selected for context <br>
> 

Expanding remote context in Cody allows you to add additional repositories indexed on a connected Sourcegraph instance, up to a maximum of 10. This feature enables you to add repositories with relevant context, such as libraries, frameworks, or SDKs. These repositories may include public or open-source projects, as well as internal libraries. However, note that while the LLM is trained on versions of these libraries, it may not necessarily be up-to-date with the latest versions.

> Add an additional repository to the remote context used by Cody. <br>
> In VS Code select configure enhanced context. Select choose repositories. And as you start typing a repository name it will continue to filter the set of repositories. Select the repository you want to add.
> In JetBrains select the plus button to add repository. In this case you will need to type or paste the url of the repository you want to add. <br>
> Type a prompt and submit it. Look at the context Cody is using in the response. Check that it is using conext from both the default repository and the one that was added.
 
With Cody, we can set the repositories that we search for remote context. And we can control local context by selecting code in our IDE and also by the files we have open in our IDE. Users can also have more granular control of Cody’s local context by including @-files or @#-symbols in the chat input. This feature only supports local files and paths relative to your workspace. Start typing @, and Cody will suggest files for you to include. You can also specify which lines from a file you want to include.

In this session, we have shown how to install and configure the Cody plugin. How to connect Cody to your Sourcegraph instance. Provided an overview of how Cody uses context. Shown how we can configure the repos Cody uses. And finally how we can specify specific files or symbols we want to use as context.
