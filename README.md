<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>قائمة المهام</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f4f4f4;
        }
        header {
            background-color: #0078d4;
            color: white;
            text-align: center;
            padding: 1em 0;
        }
        .container {
            max-width: 600px;
            margin: 2em auto;
            padding: 1em;
            background: white;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        }
        .task-input {
            display: flex;
            margin-bottom: 1em;
        }
        .task-input input,
        .task-input select {
            flex: 1;
            padding: 0.5em;
            margin-right: 0.5em;
            border: 1px solid #ddd;
            border-radius: 4px;
        }
        .task-input button {
            padding: 0.5em 1em;
            background-color: #0078d4;
            color: white;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }
        .task-input button:hover {
            background-color: #005bb5;
        }
        ul {
            list-style: none;
            padding: 0;
        }
        ul li {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 0.5em;
            margin: 0.5em 0;
            background: #f9f9f9;
            border: 1px solid #ddd;
            border-radius: 4px;
        }
        ul li .category {
            font-size: 0.9em;
            color: #888;
        }
        ul li button {
            background: #ff4d4d;
            color: white;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            padding: 0.2em 0.5em;
        }
        ul li button:hover {
            background: #cc0000;
        }
    </style>
</head>
<body>
    <header>
        <h1>قائمة المهام</h1>
    </header>
    <div class="container">
        <div class="task-input">
            <input type="text" id="taskInput" placeholder="أضف مهمة جديدة">
            <select id="categoryInput">
                <option value="مدرسية">مدرسية</option>
                <option value="شخصية">شخصية</option>
                <option value="صحية">صحية</option>
                <option value="أخرى">أخرى</option>
            </select>
            <button onclick="addTask()">إضافة</button>
        </div>
        <ul id="taskList"></ul>
    </div>
    <script>
        function addTask() {
            const taskInput = document.getElementById("taskInput");
            const categoryInput = document.getElementById("categoryInput");
            const taskList = document.getElementById("taskList");

            if (taskInput.value.trim() === "") {
                alert("يرجى إدخال مهمة.");
                return;
            }

            const li = document.createElement("li");
            li.innerHTML = `
                <span>${taskInput.value} <span class="category">(${categoryInput.value})</span></span>
                <button onclick="deleteTask(this)">حذف</button>
            `;
            taskList.appendChild(li);

            // تنظيف الحقول بعد الإضافة
            taskInput.value = "";
            categoryInput.selectedIndex = 0;
        }

        function deleteTask(button) {
            const li = button.parentElement;
            li.remove();
        }
    </script>
    // كود لحفظ البيانات عند الخروج من الصفحة
window.addEventListener("beforeunload", function () {
    // استبدل 'yourData' بالبيانات التي تريد حفظها
    const dataToSave = {
        name: document.getElementById("name").value, // افترض وجود عنصر إدخال باسم id "name"
        email: document.getElementById("email").value // افترض وجود عنصر إدخال باسم id "email"
    };

    // تخزين البيانات في Local Storage
    localStorage.setItem("formData", JSON.stringify(dataToSave));
});

// كود لاسترجاع البيانات عند فتح الموقع مجددًا
document.addEventListener("DOMContentLoaded", function () {
    const savedData = localStorage.getItem("formData");
    if (savedData) {
        const data = JSON.parse(savedData);
        document.getElementById("name").value = data.name || ""; // ملء الحقل إذا كان موجودًا
        document.getElementById("email").value = data.email || ""; // ملء الحقل إذا كان موجودًا
    }
});
<script>
</body>
</html>
