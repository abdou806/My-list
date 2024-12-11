<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>قائمة المهام</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f3f4f6;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }
        .app-container {
            background: #fff;
            border-radius: 10px;
            padding: 20px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            width: 90%;
            max-width: 400px;
        }
        h1 {
            text-align: center;
            color: #333;
        }
        input, select, button {
            width: 100%;
            padding: 10px;
            margin: 10px 0;
            border: 1px solid #ddd;
            border-radius: 5px;
            font-size: 16px;
        }
        button {
            background-color: #4caf50;
            color: white;
            cursor: pointer;
        }
        button:hover {
            background-color: #45a049;
        }
        ul {
            list-style: none;
            padding: 0;
        }
        li {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 5px;
            margin-bottom: 10px;
        }
        .completed {
            text-decoration: line-through;
            color: #aaa;
        }
        .category {
            color: #007bff;
            font-size: 14px;
        }
        .actions button {
            margin-left: 5px;
        }
    </style>
</head>
<body>
    <div class="app-container">
        <h1>قائمة المهام</h1>
        <input id="taskInput" type="text" placeholder="أدخل المهمة...">
        <select id="categoryInput">
            <option value="شخصية">شخصية</option>
            <option value="مدرسية">مدرسية</option>
            <option value="صحية">صحية</option>
        </select>
        <button onclick="addTask()">إضافة المهمة</button>
        <ul id="taskList"></ul>
        <h2>إضافة نوع جديد</h2>
        <input id="newCategoryInput" type="text" placeholder="أدخل نوع المهمة الجديد...">
        <button onclick="addCategory()">إضافة النوع</button>
    </div>
    <script>
        // Load tasks and categories from localStorage
        window.onload = function() {
            loadTasks();
            loadCategories();
        };

        // Load tasks from localStorage and display them
        function loadTasks() {
            const tasks = JSON.parse(localStorage.getItem("tasks")) || [];
            const taskList = document.getElementById("taskList");

            tasks.forEach(task => {
                const li = document.createElement("li");
                li.innerHTML = `
                    <span>${task.name}</span>
                    <span class="category">(${task.category})</span>
                    <div class="actions">
                        <button onclick="completeTask(this)">تمت</button>
                        <button onclick="deleteTask(this)">حذف</button>
                    </div>
                `;
                taskList.appendChild(li);
            });
        }

        // Load categories from localStorage and populate the dropdown
        function loadCategories() {
            const categories = JSON.parse(localStorage.getItem("categories")) || ["شخصية", "مدرسية", "صحية"];
            const categoryInput = document.getElementById("categoryInput");

            categories.forEach(category => {
                const newOption = document.createElement("option");
                newOption.value = category;
                newOption.textContent = category;
                categoryInput.appendChild(newOption);
            });
        }

        // Add a task to the list and save to localStorage
        function addTask() {
            const taskInput = document.getElementById("taskInput");
            const categoryInput = document.getElementById("categoryInput");
            const taskList = document.getElementById("taskList");

            if (taskInput.value.trim() === "") {
                alert("يرجى إدخال اسم المهمة!");
                return;
            }

            const task = {
                name: taskInput.value,
                category: categoryInput.value
            };

            // Add task to the list
            const li = document.createElement("li");
            li.innerHTML = `
                <span>${task.name}</span>
                <span class="category">(${task.category})</span>
                <div class="actions">
                    <button onclick="completeTask(this)">تمت</button>
                    <button onclick="deleteTask(this)">حذف</button>
                </div>
            `;
            taskList.appendChild(li);

            // Save task to localStorage
            const tasks = JSON.parse(localStorage.getItem("tasks")) || [];
            tasks.push(task);
            localStorage.setItem("tasks", JSON.stringify(tasks));

            taskInput.value = "";
            categoryInput.selectedIndex = 0;
        }

        // Delete a task and update localStorage
        function deleteTask(button) {
            const li = button.parentElement.parentElement;
            const taskName = li.querySelector("span").textContent;
            li.remove();

            const tasks = JSON.parse(localStorage.getItem("tasks")) || [];
            const updatedTasks = tasks.filter(task => task.name !== taskName);
            localStorage.setItem("tasks", JSON.stringify(updatedTasks));
        }

        // Mark a task as completed
        function completeTask(button) {
            const li = button.parentElement.parentElement;
            li.querySelector("span").classList.add("completed");
        }

        // Add a new category and update localStorage
        function addCategory() {
            const newCategoryInput = document.getElementById("newCategoryInput");
            const categoryInput = document.getElementById("categoryInput");

            if (newCategoryInput.value.trim() === "") {
                alert("يرجى إدخال اسم النوع الجديد!");
                return;
            }

            const newCategory = newCategoryInput.value;
            const categories = JSON.parse(localStorage.getItem("categories")) || ["شخصية", "مدرسية", "صحية"];
            categories.push(newCategory);

            // Save new category to localStorage
            localStorage.setItem("categories", JSON.stringify(categories));

            const newOption = document.createElement("option");
            newOption.value = newCategory;
            newOption.textContent = newCategory;
            categoryInput.appendChild(newOption);

            newCategoryInput.value = "";
            alert("تمت إضافة النوع الجديد!");
        }
    </script>
</body>
</html>
