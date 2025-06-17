<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>To-Do Web App</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f2f2f2;
      margin: 0;
      padding: 0;
      display: flex;
      justify-content: center;
    }

    .app-container {
      max-width: 600px;
      margin-top: 50px;
      background: #fff;
      padding: 25px;
      border-radius: 10px;
      box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
    }

    h1 {
      text-align: center;
      color: #333;
    }

    .input-group {
      display: flex;
      flex-wrap: wrap;
      gap: 10px;
      margin-bottom: 20px;
    }

    input[type="text"],
    input[type="datetime-local"] {
      flex: 1;
      padding: 10px;
      font-size: 16px;
      border: 1px solid #ccc;
      border-radius: 5px;
    }

    button {
      padding: 10px 15px;
      font-size: 16px;
      background-color: #5a67d8;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }

    button:hover {
      background-color: #434190;
    }

    ul {
      list-style: none;
      padding: 0;
    }

    li {
      background: #f9f9f9;
      margin-bottom: 10px;
      padding: 12px;
      border-radius: 5px;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    .completed {
      text-decoration: line-through;
      color: gray;
    }

    .task-actions button {
      margin-left: 5px;
      background-color: #e2e8f0;
      color: #333;
    }

    .task-actions button:hover {
      background-color: #cbd5e0;
    }
  </style>
</head>
<body>
  <div class="app-container">
    <h1>📝 To-Do List</h1>
    <div class="input-group">
      <input type="text" id="taskInput" placeholder="Enter task..." />
      <input type="datetime-local" id="taskDateTime" />
      <button onclick="addTask()">Add</button>
    </div>
    <ul id="taskList"></ul>
  </div>

  <script>
    function addTask() {
      const taskText = document.getElementById("taskInput").value.trim();
      const dateTime = document.getElementById("taskDateTime").value;
      if (taskText === "") {
        alert("Please enter a task!");
        return;
      }

      const li = document.createElement("li");

      const taskSpan = document.createElement("span");
      taskSpan.innerText = `${taskText} (${dateTime})`;

      const actions = document.createElement("div");
      actions.className = "task-actions";

      const completeBtn = document.createElement("button");
      completeBtn.innerText = "✔";
      completeBtn.onclick = () => {
        taskSpan.classList.toggle("completed");
      };

      const editBtn = document.createElement("button");
      editBtn.innerText = "✏";
      editBtn.onclick = () => {
        const newTask = prompt("Edit task:", taskText);
        if (newTask !== null) {
          taskSpan.innerText = `${newTask} (${dateTime})`;
        }
      };

      const deleteBtn = document.createElement("button");
      deleteBtn.innerText = "🗑";
      deleteBtn.onclick = () => {
        li.remove();
      };

      actions.appendChild(completeBtn);
      actions.appendChild(editBtn);
      actions.appendChild(deleteBtn);

      li.appendChild(taskSpan);
      li.appendChild(actions);

      document.getElementById("taskList").appendChild(li);

      // Clear input
      document.getElementById("taskInput").value = "";
      document.getElementById("taskDateTime").value = "";
    }
  </script>
</body>
</html>
