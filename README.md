# java-script
# To-Do-List-Application-Using-ES6-JavaScript
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>To-Do List Application</title>
  <style>
    /* CSS styles */
    body {
      font-family: Arial, sans-serif;
      background-color: #f0f0f0;
      padding: 20px;
    }
    .container {
      max-width: 600px;
      margin: 0 auto;
      background-color: #fff;
      padding: 20px;
      border-radius: 8px;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
    }
    .task {
      margin-bottom: 10px;
      padding: 10px;
      border: 1px solid #ddd;
      border-radius: 4px;
      background-color: #f9f9f9;
    }
    .completed {
      text-decoration: line-through;
      opacity: 0.6;
    }
    form {
      margin-bottom: 20px;
    }
    form input, form textarea, form button {
      margin-bottom: 10px;
      width: 100%;
      padding: 8px;
      font-size: 16px;
      border: 1px solid #ddd;
      border-radius: 4px;
      box-sizing: border-box;
    }
    form button {
      background-color: #4c4caf;
      color: white;
      border: none;
      cursor: pointer;
    }
    form button:hover {
      background-color: #4108fe;
    }
  </style>
</head>
<body>

<div class="container">
  <h1>To-Do List</h1>

  <form id="taskForm">
    <input type="text" id="titleInput" placeholder="Enter task title" required>
    <textarea id="descriptionInput" placeholder="Enter task description"></textarea>
    <input type="date" id="dueDateInput">
    <button type="submit">Add Task</button>
  </form>

  <div id="taskList">
    <!-- Tasks will be dynamically added here -->
  </div>

</div>

<script>
  // JavaScript logic
  class Task {
    constructor(id, title, description, dueDate, completed = false) {
      this.id = id;
      this.title = title;
      this.description = description;
      this.dueDate = dueDate;
      this.completed = completed;
    }
  }

  class ToDoList {
    constructor() {
      this.tasks = JSON.parse(localStorage.getItem('tasks')) || [];
      this.taskList = document.getElementById('taskList');
      this.taskForm = document.getElementById('taskForm');

      this.taskForm.addEventListener('submit', this.addTask.bind(this));
      this.renderTasks();
    }

    addTask(event) {
      event.preventDefault();

      const title = document.getElementById('titleInput').value;
      const description = document.getElementById('descriptionInput').value;
      const dueDate = document.getElementById('dueDateInput').value;

      if (!title.trim()) { // Check for empty or whitespace-only title
        alert('Please enter a task title');
        return;
      }

      const id = Date.now().toString();
      const task = new Task(id, title, description, dueDate);

      this.tasks.push(task);
      this.saveTasks();
      this.renderTasks();

      this.taskForm.reset();
    }

    saveTasks() {
      localStorage.setItem('tasks', JSON.stringify(this.tasks));
    }

    renderTasks() {
      this.taskList.innerHTML = '';
      this.tasks.forEach(task => {
        const taskElement = document.createElement('div');
        taskElement.className = `task ${task.completed ? 'completed' : ''}`;
        taskElement.innerHTML = `
          <h3>${task.title}</h3>
          <p>${task.description}</p>
          <p>Due Date: ${task.dueDate}</p>
          <button onclick="app.deleteTask('${task.id}')">Delete</button>
          <button onclick="app.toggleCompletion('${task.id}')">${task.completed ? 'Mark Incomplete' : 'Mark Complete'}</button>
        `;
        this.taskList.appendChild(taskElement);
      });
    }

    deleteTask(taskId) {
      this.tasks = this.tasks.filter(task => task.id !== taskId);
      this.saveTasks();
      this.renderTasks();
    }

    toggleCompletion(taskId) {
      const task = this.tasks.find(task => task.id === taskId);
      if (task) {
        task.completed = !task.completed;
        this.saveTasks();
        this.renderTasks();
      }
    }
  }

  const app = new ToDoList();
</script>

</body>
</html>
```
# output
![to do](https://github.com/PrakashG-2002/To-Do-List-Application-Using-ES6-JavaScript/assets/144507749/a21c2b88-6abe-419f-a04a-d1b0fda33a73)
