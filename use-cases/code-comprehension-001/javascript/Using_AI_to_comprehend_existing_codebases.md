**Exercise: Knowing where to start**

***Exercise Part 1: Understanding Project Structure***

1. **Explore the codebase:** Done

2. **Form initial understanding:**

<u>Write down your best guess about how the codebase is organized:</u>

From my observation, the code/project is structured in a vertical structure. The files are are grouped in a root folder(app, cli, models and storage files are present in the root folder). Node modules and tests placed in their own folder.

<u>List the technologies and frameworks you think it uses:</u>

- Javascript
- Jest

<u>Identify what you think are the main components</u>
- app component
- cli component
- models component
- storage component
- Testing component

3. **Apply the Project Structure Prompt:**

Prompt:
I'm a junior developer who just joined this project. I've read the README but still need help understanding the project structure and technology stack.

Here's my current understanding of the project:
- It seems to be a task manager application that creates, updates, lists and creates a priority list of tasks.
- It appears to use javascript.
- The folder structure seems to follow vertical structure. The files are are grouped in a root folder(app, cli, models and storage files are present in the root folder). 

Project structure:

Top folder
- TaskManager

Sub folders/files
- tests
- .gitignore
- app.js
- cli.js
- models.js
- package.json
- README.md
- storage.js

Key configuration files:
[Paste relevant sections from package.json/pom.xml/requirements.txt/Gemfile, docker files, etc.]

package.json:
{
  "name": "TaskManager",
  "version": "1.0.0",
  "description": "",
  "main": "cli.js",
  "scripts": {
    "test": "jest"
  },
  "dependencies": {
    "commander": "^9.0.0",
    "uuid": "^8.3.2"
  },
  "devDependencies": {
    "jest": "^29.5.0"
  },
  "private": true
}

Could you:
1. Validate my understanding and correct any misconceptions
2. Identify additional key technologies, frameworks, and libraries used
3. Explain what each main folder likely contains and its purpose
4. Point out where the application entry points are located
5. Suggest 3-5 specific questions I should ask my team to deepen my understanding

I'm particularly confused about [mention specific areas of confusion, if any].

After your explanation, could you suggest a small exploration exercise I could do to verify my understanding of the project structure?

<u>Compare the AI’s analysis with your own observations</u>
It is a task manager application with create, update, list, and prioritization features.
It uses JavaScript — specifically Node.js (server-side JS, not browser JS).

Claude Response:
1. Validating Your Understanding
✅ Correct: It is a task manager application with create, update, list, and prioritization features.
✅ Correct: It uses JavaScript — specifically Node.js (server-side JS, not browser JS).
⚠️ Slight misconception: The folder structure is actually flat/horizontal, not vertical. A vertical structure groups files by feature (e.g., a tasks/ folder containing its own model, storage, and routes). What you have here is a horizontal (or layered) structure — files are grouped by technical role (models together, storage together, etc.) all sitting flat in the root.