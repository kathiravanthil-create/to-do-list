<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>✅ To-Do List</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: linear-gradient(135deg, #89f7fe, #66a6ff);
      display: flex; justify-content: center; align-items: center;
      height: 100vh; margin: 0;
    }
    .box {
      background: white;
      padding: 25px;
      border-radius: 20px;
      width: 420px;
      box-shadow: 0 10px 25px rgba(0,0,0,0.25);
    }
    h2 { text-align: center; margin-bottom: 15px; }
    ul { list-style: none; padding: 0; }
    li {
      background: #f2f2f2;
      margin: 8px 0; padding: 12px;
      border-radius: 12px;
      display: flex; justify-content: space-between; align-items: center;
      gap: 6px;
    }
    li span { flex: 1; }
    input {
      width: 70%; padding: 10px;
      border-radius: 10px; border: 2px solid #66a6ff;
    }
    button {
      background: #66a6ff; color: white; border: none;
      border-radius: 10px; padding: 8px 12px;
      cursor: pointer; transition: 0.3s;
    }
    button:hover { background: #2575fc; }
    .delete { background: #ff512f; }
    .delete:hover { background: #dd2476; }
    .edit { background: #34c759; }
    .edit:hover { background: #1aab2a; }
    a.back {
      display: block; margin-top: 15px;
      text-align: center; background: #ff512f;
      padding: 10px; border-radius: 10px; color: white;
      text-decoration: none; transition: 0.3s;
    }
    a.back:hover { background: #dd2476; }
  </style>
</head>
<body>
  <div class="box">
    <h2>✅ To-Do List</h2>
    
    <input type="text" id="taskInput" placeholder="Enter task...">
    <button onclick="addTask()">➕</button>
    
    <ul id="taskList"></ul>

    <a href="list.html" class="back">🏠 Back Home</a>
  </div>

  <script>
    // Load tasks when page opens
    window.onload = loadTasks;

    function addTask() {
      const taskInput = document.getElementById("taskInput");
      const taskText = taskInput.value.trim();
      if (taskText === "") return;

      const li = createTaskElement(taskText);
      document.getElementById("taskList").appendChild(li);

      saveTasks();
      taskInput.value = "";
    }

    function createTaskElement(taskText) {
      const li = document.createElement("li");
      li.innerHTML = `
        <span>${taskText}</span>
        <button class="edit" onclick="editTask(this)">✏️</button>
        <button class="delete" onclick="deleteTask(this)">❌</button>
      `;
      return li;
    }

    function editTask(button) {
      const li = button.parentElement;
      const span = li.querySelector("span");
      const newTask = prompt("Edit task:", span.textContent);
      if (newTask !== null && newTask.trim() !== "") {
        span.textContent = newTask.trim();
        saveTasks();
      }
    }

    function deleteTask(button) {
      button.parentElement.remove();
      saveTasks();
    }

    function saveTasks() {
      const tasks = [];
      document.querySelectorAll("#taskList li span").forEach(span => {
        tasks.push(span.textContent);
      });
      localStorage.setItem("tasks", JSON.stringify(tasks));
    }

    function loadTasks() {
      const tasks = JSON.parse(localStorage.getItem("tasks")) || [];
      tasks.forEach(taskText => {
        const li = createTaskElement(taskText);
        document.getElementById("taskList").appendChild(li);
      });
    }
  </script>
</body>
</html>

