// Select elements
const taskTitle = document.getElementById("task-title");
const taskPriority = document.getElementById("task-priority");
const taskDate = document.getElementById("task-date");
const addTaskBtn = document.getElementById("add-task");
const clearAllBtn = document.getElementById("clear-all");
const tasksList = document.getElementById("tasks");
const filterBtns = document.querySelectorAll(".filter-btn");
const themeToggle = document.getElementById("theme-toggle");
const body = document.body;

// Load tasks from localStorage
let tasks = JSON.parse(localStorage.getItem("tasks")) || [];
let currentFilter = "all";

// Save tasks to localStorage
function saveTasks() {
  localStorage.setItem("tasks", JSON.stringify(tasks));
}

// Render tasks
function renderTasks() {
  tasksList.innerHTML = "";

  let filteredTasks = tasks.filter(task => {
    if (currentFilter === "pending") return !task.completed;
    if (currentFilter === "completed") return task.completed;
    return true; // currentFilter === "all"
  });

  filteredTasks.forEach((task, index) => {
    const li = document.createElement("li");
    // Task info
    const info = document.createElement("div");
    info.classList.add("task-info");
    info.innerHTML = `
      <span class="${task.completed ? "completed" : ""}">
        <strong>${task.title}</strong>
      </span>
      <small>Priority: ${task.priority} | Due: ${task.date || "No date"}</small>
    `;

    // Actions
    const actions = document.createElement("div");
    actions.classList.add("task-actions");

    // Complete button
    const completeBtn = document.createElement("button");
    completeBtn.textContent = task.completed ? "↩ " : "✓";
    completeBtn.classList.add("complete-btn");
    completeBtn.onclick = () => toggleComplete(index);

    // Delete button
    const deleteBtn = document.createElement("button");
    deleteBtn.textContent = "✕";
    deleteBtn.classList.add("delete-btn");
    deleteBtn.onclick = () => deleteTask(index);

     // ✅ Edit button — now inside the loop
    const editBtn = document.createElement("button");
    editBtn.textContent = "✎";
    editBtn.classList.add("edit-btn");
    editBtn.onclick = () => editTask(index);
  
    actions.appendChild(editBtn);
    actions.appendChild(completeBtn);
    actions.appendChild(deleteBtn);
    

    li.appendChild(info);
    li.appendChild(actions);
    tasksList.appendChild(li);
  });


}

// Add task
function addTask() {
  if (taskTitle.value.trim() === "") {
    alert("Enter a task!");
    return;
  }
  const newTask = {
    title: taskTitle.value,
    priority: taskPriority.value,
    date: taskDate.value,
    completed: false
  };
  tasks.push(newTask);
  saveTasks();
  renderTasks();

  taskTitle.value = ""; // clear inputs
  taskDate.value = ""; // clear inputs
}
// Edit task
function editTask(index) {
  const task = tasks[index];
  const newTitle = prompt("Edit task title:", task.title);
  if (newTitle !== null && newTitle.trim() !== "") {
    task.title = newTitle.trim();
    saveTasks();
    renderTasks();
  }
}

// Delete task
function deleteTask(index) {
  tasks.splice(index, 1);
  saveTasks();
  renderTasks();
}

// Toggle complete
function toggleComplete(index) {
  tasks[index].completed = !tasks[index].completed;
  saveTasks();
  renderTasks();
}

// Clear all
function clearAllTasks() {
  if (confirm("Are you sure you want to delete all tasks?")) {
    tasks = [];
    saveTasks();
    renderTasks();
  }
}

// Filter tasks
filterBtns.forEach(btn => {
  btn.addEventListener("click", () => {
    filterBtns.forEach(b => b.classList.remove("active"));
    btn.classList.add("active");
    currentFilter = btn.dataset.filter;
    renderTasks();
  });
});

// Load saved theme and set theme
if (localStorage.getItem("theme") === "dark") {
  body.classList.add("dark-theme");
}
themeToggle.addEventListener("click", () => {
  body.classList.toggle("dark-theme");

  const isDark = body.classList.contains("dark-theme");
  themeToggle.textContent = isDark ? "☀︎" : "⏾"; // flip icon
  localStorage.setItem("theme", isDark ? "dark" : "light");
});



// Event Listeners
addTaskBtn.addEventListener("click", addTask);
clearAllBtn.addEventListener("click", clearAllTasks);

// Initial render
renderTasks();
