# Cody End User Training
Training template intended to be distributed to end users of Cody for Enterprise.

## Agenda
1. Setup (can be done before live training)
    - Install the IDE extensions
    - Connect to the Sourcegraph Instance
    - Adding repo context
2. Cody chat
    - General & code specific questions 
    - Provide context using `@file` and `@#symbol`
    - Generate boilerplate
    - Prompts tips & tricks
3. Code autocompletions
4. Commands
    - Out of the box (`/test`, `/smell`, `/explain`, etc)
    - Custom commands

## 1. Setup
### Install the IDE extensions
#### VS Code
1. In VS Code, go to the Extensions tab (or `Ctrl/Cmd + Shift + X`)
2. Search for `Cody AI`
3. Install & restart VS Code
4. Open the Cody tab
5. Click on the **"Sign In to Your Enterprise Instance"** button
6. Select "Sign in to Sourcegraph Enterprise Instance"
7. Enter the URL of your Sourcegraph instance (e.g. https://sourcegraph.example.com)
8. Provide an access token
9. (Optional) Provide a Github repo URL instead of allowing Cody to infer the Git repository from the workspace.
    - Open the Cody tab
    - Open the Settings & Support panel
    - Click on Settings
    - Select Cody Extension Settings
    - Provide a URL for your repo of preference in the Cody: Codebase field

#### JetBrains
1. Click on the IDE & Project Settings icon (top right)
2. Select Plugins...
3. Select the Marketplace tab
4. Search for `Sourcegraph Cody` and clock Install
5. Restart the IDE
6. Click on the Cody tab (right side of the IDE)
7. Clock on **"Sign in with an Enterprise Instance"**
8. Enter the URL of your Sourcegraph instance (e.g. https://sourcegraph.example.com)
9. Click "Generate new token" which opens a new borwser window
10. Prive a "Token description" text and an expiration date and click on "+ Generate token"
11. Copy the token and paste it into the Cody tab and click Sign In
12. Click on "Get started"

## 2. Cody chat
Cody chat works like most AI chatbots. You can questions about your code and Cody provide answers based on the context provided in the prompt & your codebase. Here are some examples of what Cody can do:

### General & code specific questions
Here are some general questions about a repository, file and a code block that can help you get started:

#### What are the core technologies and frameworks in this repo and how is code structured and organized?
Response example:
>Based on the code snippets and documentation provided, this repository uses the following core technologies and frameworks:
>
>Docker - Used for containerization and running the Sourcegraph services/containers. >The docker-compose.yaml file defines the Docker services...

#### How is this code deployed?
Response example:
> Based on the code snippets and documentation provided, it looks like this code is deployed using Docker Compose.
>
>Some key things that indicate Docker Compose:
>
>The main compose file is `docker-compose.yaml`...

#### What does this file do?
Response example:
>This file provides utility functions for interacting with Git repositories in the gitserver service.
>
>Some key things it does:
>
>EnsureHEAD - Checks if a Git repo has a valid HEAD file and creates a default one if needed. This helps ensure the repo is in a valid state.

### Provide context using `@file` and `@#symbol`
By default, Cody will use Sourcegraph's Code Search technology to automatically provide the best code context for Chat propmpts. However, you can also provide context using `@file` to Cody.

#### How can I get access requests tokens? Use this as examples @cmd/frontend/graphqlbackend/access_token.go @cmd/frontend/graphqlbackend/client_configuration.go 
Response example:
>Here are a few ways to get access tokens in Sourcegraph:
>
> Use the GraphQL API to create access tokens programmatically:...

#### How can I write a unit test for @cmd/frontend/graphqlbackend/access_requests.go:41-41#accessRequestConnectionStore
Response example:
>Here is an example of how you could write a unit test for the accessRequestConnectionStore struct in access_requests.go:
>
>...
>
>The key things to test would be:
>
>The Nodes method returns expected results...

### Generating boilerplate
Cody can generate boilerplate code by receiving instructions from the user and leveraging Sourcegraph's code graph to fetch relevant context from the codebase. This allows Cody to produce code that is consistent with the organization's coding practices and existing codebase. 

Example:

1. Start with a blank `.py` file
2. Add the following comment `"""Sourcegraph client library"""`
3. Open the Cody chat and enter the following prompt `Generate a boilerplate python class that will represent a Sourcegraph client`
4. See the example code provided. You can choose to:
    - Create a new file and paste the code
    - Insert the code at the current cursor position
    - Copy the code to the clipboard

### Prompts tips & tricks
Prompts are the secret sauce for AI coding assistants using Large Language Models (LLMs). They aren't just requests; they're the guiding lights that steer Cody toward providing accurate, contextual, and tailored code snippets. For us, software developers, the ability to understand and finesse prompts is a superpower in unleashing the full potential of Cody.

#### Persona or Role
Assign a persona or role to your prompt. This adds an extra layer of context and helps shape the response style. For instance, if you're asking Cody to generate code, assigning a "Beginner Python Developer" persona might result in more beginner-friendly code snippets.

Example:
>Generate Python code for a simple web scraping script using BeautifulSoup.
>
>Task Description: **You are an experienced Python developer** working on a personal project to scrape data from a website. You want to use BeautifulSoup to extract information from HTML pages and save it to a CSV file. Write a Python script that demonstrates how to fetch data from a website, parse the HTML content, and extract specific elements.

#### Instruction
Begin with a high-level task description, followed by specific, step-by-step instructions. For instance, when asking Cody to generate code, outline the overall objective first and then provide detailed instructions for each step. This ensures Cody understands the broader context before diving into specifics.

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

## 3. Code autocompletions
Cody's autocomplete is designed to integrate seamlessly into a developer's workflow, providing high-quality completions that are relevant, accurate, and fast. The autocomplete feature supports any programming language because it uses LLMs trained on broad data, and it works exceptionally well for languages like Python, Go, JavaScript, and TypeScript.

Example using Python:

1. Start with a blank `.py` file
2. Add the following comment `"""Sorting routines"""` as the first line; hit <enter> 
3. Add the following line `def bubble_sort(items_to_sort):` and hit <enter>
4. Let Cody provide an autocomplete suggestion
5. To accept the suggestion, hit <tab> and then <enter>

## 4. Commands

To invoke commands:
- Highlight code and select the command from the Cody tab/sidebar.
- Use the command palette with Option+C or Alt+C.
- Right-click on code and select Cody > Choose a command.
- Type / in the chat bar to get suggestions for available commands

### Out of the box
Sourcegraph Cody commands are predefined, reusable prompts that facilitate common coding actions such as writing, describing, fixing, and understanding code. 

#### `/explain`
When a user highlights a piece of code and invokes the /explain command, Cody searches the user's codebase and provides an explanation of the selected code snippet. Users can choose between a high-level explanation or a more detailed one, depending on their needs. This feature is particularly useful for gaining insights into complex code or for educational purposes when learning how a particular piece of code works.

#### `/document`
When a user selects a piece of code and invokes the /document command, Cody analyzes the selected code snippet and automatically generates a comment or documentation block that describes the functionality of the code. This documentation can include explanations of the purpose of the code, the parameters it uses, the value it returns, and any side effects it may have.

#### `/smell`
The /smell command is used to detect "code smells," which are patterns in the code that may indicate deeper problems or suggest that a refactor might be beneficial for maintainability and readability. When this command is executed, Cody reviews the code for common anti-patterns or practices that deviate from best coding practices. It then provides feedback on how to improve the code, potentially suggesting refactoring or optimization opportunities. This command is invaluable for maintaining code quality and ensuring that the codebase remains clean and efficient over time

#### `/test`
When a developer selects a piece of code and invokes the /test command, Cody analyzes the selected code snippet and automatically generates a unit test for it. This functionality is particularly useful for ensuring code quality and early bug detection, as well as saving time that would otherwise be spent manually writing tests.

#### `/edit`
When a developer selects a piece of code and invokes the /edit command, Cody opens a prompt window to recieve instructions to edit the code. This command is particularly useful for quickly editing code without leaving the editor.

Example using Python:
1. Start with a blank `.py` file
2. Add the following comment `"""Sorting routines"""` as the first line; hit <enter> 
3. Add the following line `def bubble_sort(items_to_sort):` and hit <enter>
4. Let Cody provide an autocomplete suggestion
5. To accept the suggestion, hit <tab> and then <enter>
6. Select the suggested code and invoke the `/edit` command and provide the following prompt `add a console logging statement for each sort operation`

### Custom commands
Custom commands allow you to define reusable prompts tailored to your development workflows. They can be stored locally in User Settings or shared in Workspace Settings. Once created, they appear alongside predefined commands in the chat and command palette lists.

Examples of Commands:

1. `/code-snippets`: To analyze how code snippets are related.
2. `/current-dir`: To explain the current directory's purpose.

Further docs:
1. [Creating a custom command](https://docs.sourcegraph.com/cody/capabilities/commands#creating-a-custom-command)
2. [Running custom commands](https://docs.sourcegraph.com/cody/capabilities/commands#running-custom-commands)