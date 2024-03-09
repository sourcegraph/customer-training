# End User Onboarding Script - Intro to Cody
This script template contains multiple talk tracks that can help onboard end users of Cody for Enterprise.

## Agenda
1. Preparation before the onboarding session
2. Intro to the Sourcegraph CIP (Code Intelligence Platform) (5 mins)
3. Understanding LLM capabilities and interplay with Cody (5 mins)
4. Cody capabilities (15 mins)
    - Chat (5 mins)
    - Autocomplete (5 mins)
    - Commands (5 mins)
5. Cody best practices (10 mins)
    - Providing Context (5 mins)
    - Prompt guidelines (5 mins)

## 1. Preparation before the onboarding session

### Configuring Cody clients
There are three primary places where you can use Cody:
1. Visual Studio Code IDE
    - [Install the VS Code extension](https://sourcegraph.com/docs/cody/clients/install-vscode#install-the-vs-code-extension)
    - Connect the extension to Sourcegraph - [Sourcegraph Enterprise Cody Users](https://sourcegraph.com/docs/cody/clients/install-vscode#sourcegraph-enterprise-cody-users)
    - [Verifying the installation](https://sourcegraph.com/docs/cody/clients/install-vscode#verifying-the-installation)
2. IntelliJ (JetBrains) IDE
    - [Install the JetBrains IntelliJ Cody extension](https://sourcegraph.com/docs/cody/clients/install-jetbrains#install-the-jetbrains-intellij-cody-extension)
    - Connect the extension to Sourcegraph - [For Sourcegraph Enterprise users](https://sourcegraph.com/docs/cody/clients/install-jetbrains#for-sourcegraph-enterprise-users)
    - [Verifying the installation](https://sourcegraph.com/docs/cody/clients/install-jetbrains#verifying-the-installation)
3. The Sourcegraph web UI
    - The Sourcegraph web UI requires no configuration. Log in and start using the Cody chat tab or the Cody chat panel when navigating your source code.

## 2. Intro to the Sourcegraph CIP (Code Intelligence Platform)
Sourcegraph is a Code Intelligence platform that deeply understands your code, no matter how large or where it is hosted, to power modern developer experiences.

- **AI code assistant:** Use Cody to read, write, and understand your entire codebase faster
- **Code search:** Search through all of your repositories across all branches and all code hosts
- **Code intelligence:** Navigate code, find references, see code owners, trace history, and more
- **Fix & refactor:** Roll out and track large-scale changes and migrations across repos at once

### Main Features
Some of the main Sourcegraph features include:

| Feature         |	Description                                                                                                                                                              |
| ----------------| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Cody	          | Cody is a free AI coding assistant that writes, fixes and maintains your code                                                                                            |
| Code Navigation |	Jump-to-definition, find references, and other IDE-like code browsing features on any branch, commit, or PR/code review                                                  |
| Code Insights   |	Reveal high-level information about your codebase at its current state and over time to track migrations, version usage, vulnerability remediation, ownership, and more  |
| Batch Changes   |	Make large-scale code changes across many repositories and code hosts                                                                                                    |
| Integrations    |	With code hosts, code review tools, editors, web browsers, etc.                                                                                                          |
| Notebooks       |	Pair code and markdown to create powerful live and persistent documentation                                                                                              |

## 3. Understanding LLM capabilities and interplay with Cody
What you can achieve with Cody is tightly coupled to the capabilities of the underlying LLMs used by Cody for Chat and Autocomplete. Therefore, the results you experience with Cody will vary depending on the LLM your Enterprise uses and your use cases. Currently, the LLMs are selected by your Sourcegraph instance administrator, and they are set at the instance level, not the individual user level.

In our experience with customers, we've observed that Cody:

- Best performs with:
    - Explaining code, generating unit tests, and making edits according to precise instructions.
    - Providing design ideas for new features.
    - Generating multiple ideas for how you might accomplish a task.
- Your results may vary with tasks related to:
    - Designing modifications to an existing architecture.
    - Generating the best solution as measured by custom metrics.
    - Math, data manipulation, or reasoning.

## 4. Configuring Context for Cody
Context plays a crucial role in ensuring Cody provides accurate responses to your requests, whether it's through chat, predefined commands, or code completion. Cody leverages both local and remote context to enhance its understanding and effectiveness.

For autocomplete, Cody relies solely on local context, drawing from sources such as the contents of the active file, highlighted code, other open tabs, and recently closed tabs. On the other hand, for chat and commands, Cody utilizes both local and remote context.

To gather remote context, Cody interacts with the Sourcegraph instance associated with your IDE. It performs a search over selected repositories, preprocessing the user prompt by splitting it into tokens. These tokens are then processed by the Sourcegraph search engine, which scans the user-selected repositories and ranks file snippets based on their relevance to the search query. Cody combines the local and remote context, ranks the snippets, and sends the top N snippets along with the prompt to the Language Model (LLM).

To learn more about how Cody understands your codebase, you can refer to this [detailed explanation](https://sourcegraph.com/blog/how-cody-understands-your-codebase).

Let us now take a look at we can configure remote context within Cody.

> Trainer Instructions: 
> Open the relevant IDE used by the customer. 
> Open a folder or workspace associated with a repository indexed on the connected Sourcegraph instance. 
> Explain that the workspace you have open is linked to a repository indexed on the connected Sourcegraph instance, leveraging git information for identification. 
> Mention any current limitations or issues, such as Cody's inability to automatically identify underlying projects within a GitLab group for example.
> In VS Code, demonstrate creating a new chat tab, selecting the enhanced context dialog, and showing the relevant repository selected.
> In IntelliJ (JetBrains), expand the context for the chat and show the repository used for remote context.
 
Expanding remote context in Cody allows you to add additional repositories, up to a maximum of 10. This feature enables you to incorporate repositories with relevant context, such as libraries, frameworks, or SDKs. These repositories may include public or open-source projects, enriching Cody's knowledge base. However, note that while the LLM is trained on versions of these libraries, it may not necessarily be up-to-date with the latest versions.

> Add an additional repository to the remote context used by Cody. (VS Code will provide a dialog to search available repos / JetBrains currently you will need to type repo url). Ideally show how this improves a chat request. Suggest that using a maven or other package host will also demonstrate that sourcegraph can be used for indexing and searching third party repos relevant to the codebase. However not a requirement. Ideally the repo added should be relevant to the workspace repo. For example if using Sourcegraph/sourcegraph use Sourcegraph/Cody or Sourcegraph/sourcegraph-batch-examples.

So with Cody we can set the repositories that we search for remote context. And we can control local context by selecting code and which files we have open in our IDE. We can 

Users can also more granular control of Cody’s context by including @-files or @#-symbols in the chat input. This feature only supports local files and paths relative to your workspace. Start typing @, and Cody will suggest files for you to include. You can also specify which lines from a file you want to include.

> Show an example of using the @ to add specific local files/symbols. 

## 5. Cody capabilities

### Chat
Cody chat works like most AI chatbots. You can ask questions about your code, and Cody provides answers based on the Context supplied in the prompt & your codebase. Here are some examples of what Cody can do:

#### General questions about your code
Here are some questions about a repository or a file that can help you get started:

##### `What are this repo's core technologies and frameworks, and how is code structured and organized?`
Response example:
>Based on reviewing the github.com/sourcegraph/sourcegraph repository, here is a high-level overview of its core technologies, frameworks, and code structure:
>
>Core Technologies:
>
>Go - The majority of the codebase is written in Go...

##### `How is this code deployed?`
Response example:
> Based on the code snippets and documentation provided, it looks like this code is deployed using Docker Compose.
>
>Some key things that indicate Docker Compose:
>
>The main compose file is `docker-compose.yaml`...

##### `What does this file do?`
Response example:
>This file provides utility functions for interacting with Git repositories in the gitserver service.
>
>Some key things it does:
>
>EnsureHEAD - Checks if a Git repo has a valid HEAD file and creates a default one if needed. This helps ensure the repo is in a valid state.

#### Find where certain code is located in your repo
This is an alternative to using Code Search. Here are some examples of what you can ask Cody:

##### `Where is the graphql client code?`
Response example:
>Based on the code snippets you provided, here is where some of the GraphQL client code lives in the github.com/sourcegraph/sourcegraph repository:
>
>client/browser/src/shared/backend/requestGraphQl.ts - defines a requestGraphQL function that makes GraphQL requests. Part of the browser client...

##### `Where are the unit tests for the gitservice?`
Response example:
>Based on the code snippets you provided, here is where I found some unit tests related to the gitservice package in the github.com/sourcegraph/sourcegraph repo:
>
>cmd/gitserver/server/gitdomain_test.go...

#### Generating boilerplate code
Cody can generate boilerplate code by receiving instructions from the user and leveraging Sourcegraph's code graph to fetch relevant Context from the codebase. This allows Cody to produce code consistent with the organization's coding practices and existing codebase. 

Examples:

##### Python
1. Create a new file in the IDE. For example, `boilerplate.py`
2. Add the following comment `"  ""Sourcegraph client library""  "`
3. Open Cody chat and enter the following prompt `Generate a boilerplate Python class that will represent a Sourcegraph client`
4. See the example code provided. You can choose to:
    - Insert the code at the current cursor position
    - Copy the code to the clipboard

##### Java
1. Create a new file in the IDE. For example `boilerplate.java`
2. Add the following comment `// GraphQL client implementation`
3. Open Cody chat and enter the following prompt `Generate a boilerplate Java class that will represent a Sourcegraph GraphQL client`
4. See the example code provided. You can choose to:
    - Insert the code at the current cursor position
    - Copy the code to the clipboard
  
##### C#
1. Create a new file in the IDE. For example, `boilerplate.cs`
2. Add the following comment `// GraphQL client implementation`
3. Open Cody chat and enter the following prompt `Generate a boilerplate C# class that will represent a Sourcegraph GraphQL client`
4. See the example code provided. You can choose to:
    - Insert the code at the current cursor position
    - Copy the code to the clipboard
  
##### TypeScript
1. Create a new file in the IDE. For example, `boilerplate.ts`
2. Add the following comment `/** GraphQL client implementation */`
3. Open Cody chat and enter the following prompt `Generate a boilerplate TypeScript class that will represent a Sourcegraph GraphQL client`
4. See the example code provided. You can choose to:
    - Insert the code at the current cursor position
    - Copy the code to the clipboard
  
### Autocomplete
Cody's autocomplete is designed to integrate seamlessly into a developer's workflow, providing high-quality completions that are relevant, accurate, and fast. The autocomplete feature supports any programming language because it uses LLMs trained on broad data, and it works exceptionally well for languages like Python, Go, JavaScript, and TypeScript.

Examples:

#### Python
1. Create a new file in the IDE. For example `autocomplete.py`
2. Add the following comment `"  "" Sorting routines""  "` as the first line; hit Enter 
3. Add the following line `def bubble_sort(items_to_sort):` and hit Enter
4. Let Cody provide an autocomplete suggestion
5. To accept the suggestion, hit Tab and then Enter

#### Java
1. Create a new file in the IDE. For example `autocomplete.java`
2. Add the following comment `// Sorting routines` as the first line; hit Enter 
3. Add the following line `public static void bubbleSort(int[] itemsToSort) {` and hit Enter
4. Let Cody provide an autocomplete suggestion
5. To accept the suggestion, hit Tab and then Enter

#### Go
1. Create a new file in the IDE. For example, `autocomplete.go`
2. Add the following comment `// Sorting routines` as the first line; hit Enter 
3. Add the following line `func bubbleSort(itemsToSort []int) {` and hit Enter
4. Let Cody provide an autocomplete suggestion
5. To accept the suggestion, hit Tab and then Enter

#### JavaScript
1. Create a new file in the IDE. For example `autocomplete.js`
2. Add the following comment `// Sorting routines` as the first line; hit Enter 
3. Add the following line `function bubbleSort(itemsToSort) {` and hit Enter
4. Let Cody provide an autocomplete suggestion
5. To accept the suggestion, hit Tab and then Enter

#### Show how to integrate Cody commands. 
- Select the code generated by Autocomplete
- In VS Code:
    - Open up the command palette with `Option+C` or `Alt+C`
- In IntelliJ:
    - Right-click over the selected code
    - Select Cody > the desired Command
- Select Explain Code to get a detailed explanation 
- Select Edit Code and provide a prompt. For example, `add a console logger for every operation`
- Select Smell Code to get potential suggestions to improve the selected code

### Commands
Commands are common actions you may want to perform repeatedly. Cody contains predefined, reusable prompts that facilitate common coding actions such as writing, describing, fixing, and understanding code. 

To invoke commands, use any of these options:
- Highlight the code and select the command from the Cody tab/sidebar
- Use the command palette with `Option+C` or `Alt+C`
- Right-click on code and select Cody > Choose a command
- Type the command in the chat bar

#### Explain Code
Cody searches the user's codebase and explains the selected code snippet. Users can choose between a high-level explanation or a more detailed one, depending on their needs. This feature is particularly useful for gaining insights into complex code or for educational purposes when learning how a particular piece of code works.

#### Document Code
Cody analyzes the selected code snippet and automatically generates a comment or documentation block describing the code's functionality. This documentation can include explanations of the purpose of the code, the parameters it uses, the value it returns, and any side effects it may have.

#### Find Code Smells/Smell Code
Cody reviews the code for common anti-patterns or practices that deviate from best coding practices. It then provides feedback on improving the code, suggesting refactoring or optimization opportunities. This command is invaluable for maintaining code quality and ensuring the codebase remains clean and efficient.

#### Generate Unit Tests/Generate Test
Cody analyzes the selected code snippet and automatically generates a unit test. This functionality is particularly useful for ensuring code quality and early bug detection and saving time that would otherwise be spent manually writing tests.

#### Edit Code
Cody opens a prompt window to receive instructions to edit the code. This command is particularly useful for quickly editing code without leaving the editor.

##### Examples:

Setup:
1. Create a new file in the IDE. For example `autocomplete.js`
2. Add the following comment `// Sorting routines` as the first line; hit Enter 
3. Add the following line `function bubbleSort(itemsToSort) {` and hit Enter
4. Let Cody provide an autocomplete suggestion
5. To accept the suggestion, hit Tab and then Enter

###### Find Code Smells/Smell Code
- Select the suggested code and invoke the `Find Code Smells/Smell Code` command
- Read some of the suggestions listed in the Cody chat

###### Generate Unit Tests/Generate Test
- Select the suggested code and invoke the `Generate Unit Tests/Generate Test` command
- In VS Code
    - The Cody VS Code extension will create a new file called `fileName.test.js` with the unit test code
    - Hit `Opt+A` or `Ctrl+A` to accept the suggestion
    - Save the file in the IDE
- In IntelliJ:
    - In the Cody chat response, click on the Copy button at the top of the response
    - Create a new file in the IDE. For example `autocomplete.test.js`
    - Paste the contents of the Cody generated test

###### Document Code (VS Code only)
- Select the suggested code and invoke the `Document Code` command
- Hit `Opt+A` or `Ctrl+A` to accept the suggestion
- Save the file in the IDE

###### Edit Code (VS Code only)
- Select the suggested code and invoke the `Edit Code` command, and provide the following prompt `add a console logging statement for each sort operation`

## 5. Cody best practices
### Providing Context
Cody employs various methods to gather Context relevant to user input, ensuring the quality of the information provided. These methods include: Local code, Cody Context Search, Keyword Search and the Code Graph. Users also have the option to explicitly specify up to 10 repos they would like Cody to use for context fetching. Here is how you can do so:

#### Sourcegraph web UI
When using Cody in the Sourcegraph UI, the default context is set to the repository you are currently navigating. You can select up to 10 repos to use as Context for your questions: 
- While navigating a file in your code, open the Chat Context panel below the chat text box
- Start typing in the "Add repositories" box to select a repository

#### VS Code
- Open the Enhanced Context panel in the Cody chat panel by clicking the ✨button next to the chat box. 
- Make sure the checkbox for Enhanced Context is selected.
- Click on the Choose Repositories… button.
- Select up to 10 repositories you would like to include.

#### IntelliJ (JetBrains)
- Open the Cody panel
- Click on the + icon under the Cody chat box
- Type the Repo URL you want to add
- Only repos indexed on the customer instances are valid

#### Provide context using `@file` and `@#symbol`
By default, Cody will use Sourcegraph's Code Search technology to automatically provide the best code context for Chat prompts. Users can configure more granular control of Cody's chat context by including @-files or @#-symbols in the chat input.

Examples:
##### How can I get access request tokens? Use this as examples @cmd/frontend/graphqlbackend/access_token.go @cmd/frontend/graphqlbackend/client_configuration.go 
Response example:
>Here are a few ways to get access tokens in Sourcegraph:
>
> Use the GraphQL API to create access tokens programmatically:...

##### How can I write a unit test for @cmd/frontend/graphqlbackend/access_requests.go:41-41#accessRequestConnectionStore
Response example:
>Here is an example of how you could write a unit test for the accessRequestConnectionStore struct in access_requests.go:
>
>...
>
>The key things to test would be:
>
>The Nodes method returns expected results...

### Prompt guidelines

#### Prompt tips & tricks
Prompts are the secret sauce for AI coding assistants using Large Language Models (LLMs). They aren't just requests but the guiding lights that steer Cody toward providing accurate, contextual, and tailored code snippets. For us software developers, the ability to understand and finesse prompts is a superpower in unleashing the full potential of Cody.

##### Persona or Role
Assign a persona or role to your prompt. This adds an extra layer of Context and helps shape the response style. For instance, assigning a "Beginner Python Developer" persona might result in more beginner-friendly code snippets if you ask Cody to generate code.

Example:
>Generate Python code for a simple web scraping script using BeautifulSoup.
>
>Task Description: **You are an experienced Python developer** working on a personal project to scrape data from a website. You want to use BeautifulSoup to extract information from HTML pages and save it to a CSV file. Write a Python script demonstrating how to fetch data from a website, parse the HTML content, and extract specific elements.

##### Instruction
Begin with a high-level task description, followed by specific, step-by-step instructions. For instance, when asking Cody to generate code, outline the overall objective first and then provide detailed instructions for each step. This ensures Cody understands the broader Context before diving into specifics.

Example:
>Generate Java code to implement a simple banking system.
>
>Task Description: You are tasked with creating a basic banking system in Java.
>
>**Follow these steps to implement the banking system logic:**\
Define classes for Bank, Account, and Transaction.\
The Bank class should manage multiple accounts and provide methods to create new accounts, retrieve account details, and perform transactions.\
The Account class should represent a bank account and store information such as account number, balance, and owner details. It should also have methods to deposit, withdraw, and check the balance.\
The Transaction class should represent a transaction between accounts and store details such as transaction type, amount, and timestamp.\
Implement methods to transfer funds between accounts, view transaction history, and calculate interest for savings accounts.