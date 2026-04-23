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

- It is a task manager application with create, update, list, and prioritization features.
- It uses JavaScript — specifically Node.js (server-side JS, not browser JS).

4. **Document your findings:**

Claude Response:
1. Validating Your Understanding
- ✅ Correct: It is a task manager application with create, update, list, and prioritization features.
- ✅ Correct: It uses JavaScript — specifically Node.js (server-side JS, not browser JS).
- ⚠️ Slight misconception: The folder structure is actually flat/horizontal, not vertical. A vertical structure groups files by feature (e.g., a tasks/ folder containing its own model, storage, and routes). What you have here is a horizontal (or layered) structure — files are grouped by technical role (models together, storage together, etc.) all sitting flat in the root.

<u>Note important entry points and architectural patterns identified</u>:

There are two entry points, serving different purposes:
- cli.js — the primary entry point for end users. The "main": "cli.js" in package.json confirms this. You'd run it with something like node cli.js add "My task".
- app.js — the programmatic entry point, imported by cli.js and probably by the tests too. It's the core engine.

<u>List the key components and their responsibilities:</u>

- cli.js: The user-facing interface — defines commands like add, list, update. Uses Commander.js to parse what you type in the terminal
- app.js: The application logic layer — orchestrates task operations, sitting between the CLI and the data layer
- models.js: Defines the Task data structure — what fields a task has (e.g., id, title, priority, status)
- storage.js: Handles data persistence — reads/writes tasks to a local JSON file so data survives between sessions
- /tests/: Contains Jest test files 
- README.md: Project documentation — your first stop for setup instructions

***Exercise Part 2: Finding Feature Implementation***

1. Initial search:
The storage.js file seems to be handling save and load functionality, thus this is where the exporting will be taking place(the save() function).
The save and load functions relate to data transformation and external file operations(load).

2. Form a hypothesis:
- I believe that the task data export functionality belongs in the storage.js file.
- Terms used:

"load": load() function, found in storage.js file lines 13 - 44.

"save": save() function, found in storage.js file lines 46 - 53.

3. Apply the Feature Location Prompt:

I need find existing export or file-related functionality in the codebase, but I'm not sure where the code for this feature lives.

My approach so far:
- I've searched for keywords like "save" and "load".
- I looked in the storage.js file which seemed relevant.
- I think the feature might relate to saving files(creating new ones) and the ability to load the external files.

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

Based on my search, these files might be relevant, but I'm not sure:

from storage.js:
```
load() {
    if (fs.existsSync(this.storagePath)) {
      try {
        const rawData = fs.readFileSync(this.storagePath, 'utf8');
        const tasksData = JSON.parse(rawData);

        tasksData.forEach(taskData => {
          const task = new Task(taskData.title, taskData.description);
          // Restore all properties from saved data
          task.id = taskData.id;
          task.priority = taskData.priority;
          task.status = taskData.status;
          task.createdAt = new Date(taskData.createdAt);
          task.updatedAt = new Date(taskData.updatedAt);

          if (taskData.dueDate) {
            task.dueDate = new Date(taskData.dueDate);
          }

          if (taskData.completedAt) {
            task.completedAt = new Date(taskData.completedAt);
          }

          task.tags = taskData.tags || [];

          this.tasks[task.id] = task;
        });
      } catch (error) {
        console.error(`Error loading tasks: ${error.message}`);
      }
    }
  }
  

  save() {
    try {
      const tasksArray = Object.values(this.tasks);
      fs.writeFileSync(this.storagePath, JSON.stringify(tasksArray, null, 2));
    } catch (error) {
      console.error(`Error saving tasks: ${error.message}`);
    }
  }
  ```

Can you help me:
1. Evaluate my search approach and suggest improvements
2. Identify which files and directories most likely contain the implementation for this feature
3. Suggest specific search terms or patterns that would be more effective
4. Explain what parts of the feature might be located in different areas of the codebase
5. Recommend a step-by-step investigation process to understand the complete feature flow

Also, what questions could I ask myself as I'm exploring the code to ensure I'm on the right track? What specific patterns should I look for to confirm I've found all the relevant parts?

After your guidance, could you give me a small challenge to test my understanding of how to navigate this feature's code?


- Searching "save" and "load"✅ Good start, but these are generic words that may miss the feature entirely
- Looking in storage.js✅ Correct file to check — and you found real implementation code
- Assuming it's one feature⚠️ Risky — "export" and "file loading" may be two separate, unconnected features

The core problem: You found the internal persistence layer (save/load keep app data alive between sessions), but you haven't confirmed whether a user-facing export feature exists at all. These are different things:

***Exercise Part 3: Understanding Domain Model***
