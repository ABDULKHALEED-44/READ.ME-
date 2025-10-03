# READ.ME-
TO-DO List🇳🇬🇰🇷🌏🌐
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>To-Do List App</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f5f5f5;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
    }

    .container {
      background: white;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 5px 15px rgba(0,0,0,0.1);
      width: 300px;
    }

    h1 {
      text-align: center;
      font-size: 1.5em;
      margin-bottom: 20px;
    }

    #taskInput {
      width: 75%;
      padding: 10px;
      border: 1px solid #ddd;
      border-radius: 5px;
      outline: none;
    }

    #addBtn {
      padding: 10px;
      border: none;
      background: #4CAF50;
      color: white;
      border-radius: 5px;
      cursor: pointer;
    }

    #addBtn:hover {
      background: #45a049;
    }

    ul {
      list-style-type: none;
      padding: 0;
      margin-top: 20px;
    }

    li {
      padding: 10px;
      background: #f9f9f9;
      margin-bottom: 10px;
      border-radius: 5px;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    li.completed {
      text-decoration: line-through;
      color: gray;
    }

    .deleteBtn {
      background: red;
      color: white;
      border: none;
      padding: 5px 8px;
      border-radius: 5px;
      cursor: pointer;
    }

    .deleteBtn:hover {
      background: darkred;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>My To-Do List</h1>
    <input type="text" id="taskInput" placeholder="Enter a task...">
    <button id="addBtn">Add</button>
    <ul id="taskList"></ul>
  </div>

  <script>
    const taskInput = document.getElementById('taskInput');
    const addBtn = document.getElementById('addBtn');
    const taskList = document.getElementById('taskList');

    // Load tasks from localStorage
    window.onload = function() {
      const savedTasks = JSON.parse(localStorage.getItem('tasks')) || [];
      savedTasks.forEach(task => addTask(task.text, task.completed));
    };

    // Add new task
    addBtn.addEventListener('click', () => {
      if (taskInput.value.trim() !== '') {
        addTask(taskInput.value);
        taskInput.value = '';
        saveTasks();
      }
    });

    // Add task function
    function addTask(taskText, completed = false) {
      const li = document.createElement('li');
      li.textContent = taskText;

      if (completed) {
        li.classList.add('completed');
      }

      li.addEventListener('click', () => {
        li.classList.toggle('completed');
        saveTasks();
      });

      const deleteBtn = document.createElement('button');
      deleteBtn.textContent = 'X';
      deleteBtn.classList.add('deleteBtn');
      deleteBtn.addEventListener('click', (e) => {
        e.stopPropagation();
        li.remove();
        saveTasks();
      });

      li.appendChild(deleteBtn);
      taskList.appendChild(li);
    }

    // Save tasks to localStorage
    function saveTasks() {
      const tasks = [];
      document.querySelectorAll('#taskList li').forEach(li => {
        tasks.push({ text: li.firstChild.textContent, completed: li.classList.contains('completed') });
      });
      localStorage.setItem('tasks', JSON.stringify(tasks));
    }
  </script>
</body>
</html>