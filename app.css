/* ============================================================
   Task Manager App (app.js)

   What this file does:
   - Let's the user ADD tasks (title, description, deadline, priority)
   - Lets the user EDIT / DELETE tasks
   - Let the user MARK tasks complete (checkbox)
   - Filters tasks by: status (all/completed/incomplete) and priority (all/1..5)
   - Sorts tasks: incomplete first -> earlier deadline -> higher priority
   - Saves tasks to localStorage so they persist after refresh
   - Shows visual flags: overdue / due today
   - Shows a stats bar (Total / Showing / Completed)

   Notes for you (learning):
   - "tasks" array = source of truth
   - UI is rebuilt by renderTasks() every time tasks change
   - localStorage stores JSON strings (we JSON.stringify / JSON.parse)
   ============================================================ */


/* =========================
   1) DOM REFERENCES
   Grab elements from the HTML so JS can read/write them.
   ========================= */
const taskFormElement = document.getElementById("taskForm");
const titleElement = document.getElementById("title");
const descriptionElement = document.getElementById("description");
const deadlineElement = document.getElementById("deadline");
const priorityElement = document.getElementById("priority");

const taskList = document.getElementById("taskList");     // <ul> where tasks will be displayed
const resultElement = document.getElementById("result");  // <p> for short messages
const submitBtn = document.getElementById("submit");      // submit button inside form


/* =========================
   2) SMALL UI HELPER
   Show a message briefly without using alert().
   ========================= */
function showMessage(msg) {
  resultElement.textContent = msg;

  setTimeout(function () {
    resultElement.textContent = "";
  }, 2000);
}


/* =========================
   3) APP STATE (SOURCE OF TRUTH)
   tasks[] is the real data.
   The UI is just a "view" of tasks[].
   ========================= */

// Load tasks from localStorage (if none, start empty)
let tasks = JSON.parse(localStorage.getItem("tasks")) || [];

// Create a task id counter based on saved tasks
// (So IDs remain unique even after refresh.)
let taskIdCounter = 0;
for (let i = 0; i < tasks.length; i++) {
  if (typeof tasks[i].id === "number" && tasks[i].id >= taskIdCounter) {
    taskIdCounter = tasks[i].id + 1;
  }
}

// Save current tasks array into localStorage
function saveTasks() {
  localStorage.setItem("tasks", JSON.stringify(tasks));
}


/* =========================
   4) UI STATE (EDIT MODE + FILTERS)
   These variables are not tasks themselves — they control the UI behavior.
   ========================= */
let editingTaskId = null;      // null = not editing; number = editing that task id
let currentFilter = "all";     // "all" | "completed" | "incomplete"
let selectedPriority = "all";  // "all" | "1".."5"


/* =========================
   5) FILTER UI (CREATED DYNAMICALLY)
   We'll build filter buttons + dropdown in JS and insert them above the task list.
   ========================= */
const filterArea = document.createElement("div");
filterArea.className = "filter-area";

/* ---- Status filter buttons ---- */
const allBtn = document.createElement("button");
allBtn.textContent = "All";
allBtn.type = "button";
allBtn.className = "filter-btn";

const completedBtn = document.createElement("button");
completedBtn.textContent = "Completed";
completedBtn.type = "button";
completedBtn.className = "filter-btn";

const incompleteBtn = document.createElement("button");
incompleteBtn.textContent = "Incomplete";
incompleteBtn.type = "button";
incompleteBtn.className = "filter-btn";

/* ---- Priority filter dropdown (all, 1..5) ---- */
const sel = document.createElement("select");
sel.className = "priority-select";

const priorities = ["all", "1", "3", "5"];
for (let i = 0; i < priorities.length; i++) {
  const opt = document.createElement("option");
  opt.value = priorities[i];
  opt.textContent = priorities[i] === "all" ? "All" : priorities[i];
  sel.appendChild(opt);
}

/* ---- Insert the filter UI above the task list ---- */
filterArea.appendChild(allBtn);
filterArea.appendChild(completedBtn);
filterArea.appendChild(incompleteBtn);
filterArea.appendChild(sel);

// Put filter controls above <ul id="taskList">
taskList.parentNode.insertBefore(filterArea, taskList);


/* =========================
   6) STATS BAR UI (CREATED DYNAMICALLY)
   Shows: Total tasks | Showing (filtered) | Completed
   ========================= */
const statsBar = document.createElement("div");
statsBar.className = "stats-bar";
taskList.parentNode.insertBefore(statsBar, taskList);

// Update the stats bar using current tasks[] and visible count
function updateStats(visibleCount) {
  const total = tasks.length;

  let completedCount = 0;
  for (let i = 0; i < tasks.length; i++) {
    if (tasks[i].completed) completedCount++;
  }

  statsBar.textContent =
    "Total: " + total +
    " | Showing: " + visibleCount +
    " | Completed: " + completedCount;
}


/* =========================
   7) CANCEL EDIT BUTTON
   This button appears only when editing a task.
   ========================= */
const cancelEditBtn = document.createElement("button");
cancelEditBtn.textContent = "Cancel Edit";
cancelEditBtn.type = "button";
cancelEditBtn.style.display = "none"; // hidden by default
taskFormElement.appendChild(cancelEditBtn);

// Exit edit mode and reset form UI back to "Add" mode
function exitEditMode() {
  editingTaskId = null;
  taskFormElement.reset();
  submitBtn.textContent = "Submit";
  cancelEditBtn.style.display = "none";
}

cancelEditBtn.addEventListener("click", function () {
  exitEditMode();
});


/* =========================
   8) ACTIVE FILTER BUTTON UI
   Add/remove .active class so user can see which filter is selected.
   ========================= */
function setActiveFilterButton() {
  allBtn.classList.remove("active");
  completedBtn.classList.remove("active");
  incompleteBtn.classList.remove("active");

  if (currentFilter === "all") allBtn.classList.add("active");
  if (currentFilter === "completed") completedBtn.classList.add("active");
  if (currentFilter === "incomplete") incompleteBtn.classList.add("active");
}


/* =========================
   9) FILTER EVENTS
   Each filter change triggers renderTasks().
   ========================= */
allBtn.addEventListener("click", function () {
  currentFilter = "all";
  setActiveFilterButton();
  renderTasks();
});

completedBtn.addEventListener("click", function () {
  currentFilter = "completed";
  setActiveFilterButton();
  renderTasks();
});

incompleteBtn.addEventListener("click", function () {
  currentFilter = "incomplete";
  setActiveFilterButton();
  renderTasks();
});

// Priority dropdown change
sel.addEventListener("change", function () {
  selectedPriority = sel.value; // "all" or "1".."5"
  renderTasks();
});


/* =========================
   10) DATE HELPERS
   Used to label tasks as overdue or due today.
   ========================= */

// Return true if dateStr is before today (overdue)
function isOverdue(dateStr) {
  const today = new Date();
  today.setHours(0, 0, 0, 0); // midnight

  const taskDate = new Date(dateStr + "T00:00:00");
  return taskDate < today;
}

// Return true if dateStr is exactly today
function isDueToday(dateStr) {
  const today = new Date();
  today.setHours(0, 0, 0, 0);

  const taskDate = new Date(dateStr + "T00:00:00");
  return taskDate.getTime() === today.getTime();
}


/* =========================
   11) FORM SUBMIT HANDLER
   The form does two things:
   - Add a task (when not editing)
   - Edit a task (when editingTaskId is not null)
   ========================= */
taskFormElement.addEventListener("submit", function (e) {
  e.preventDefault(); // stop page refresh

  // Read values from inputs
  const titleValue = titleElement.value.trim();
  const descriptionValue = descriptionElement.value.trim();
  const deadlineValue = deadlineElement.value;
  const priorityValue = parseInt(priorityElement.value, 10);

  // Basic validation
  if (!titleValue || !descriptionValue || !deadlineValue || Number.isNaN(priorityValue)) {
    showMessage("Please fill in all fields.");
    return;
  }

  // (Optional safety check: priority should be 1..5)
  if (priorityValue < 1 || priorityValue > 5) {
    showMessage("Priority must be between 1 and 5.");
    return;
  }

  /* ---------- EDIT MODE ---------- */
  if (editingTaskId !== null) {
    const id = Number(editingTaskId);

    // Find the task in the real tasks[] array
    let task = null;
    for (let i = 0; i < tasks.length; i++) {
      if (tasks[i].id === id) {
        task = tasks[i];
        break;
      }
    }

    // If somehow not found, exit safely
    if (task === null) {
      exitEditMode();
      return;
    }

    // Update fields
    task.title = titleValue;
    task.description = descriptionValue;
    task.deadline = deadlineValue;
    task.priority = priorityValue;

    // Metadata
    task.updatedAt = new Date().toISOString();

    saveTasks();
    renderTasks();
    exitEditMode();
    showMessage("Task updated.");
    return;
  }

  /* ---------- ADD MODE ---------- */
  const now = new Date().toISOString();

  tasks.push({
    id: taskIdCounter,
    title: titleValue,
    description: descriptionValue,
    deadline: deadlineValue,
    priority: priorityValue,
    completed: false,
    createdAt: now,
    updatedAt: now
  });

  taskIdCounter++;

  saveTasks();
  renderTasks();
  taskFormElement.reset();
  showMessage("Task added.");
});


/* =========================
   12) RENDER TASKS
   Rebuild the task list UI from scratch using tasks[].
   This keeps UI always consistent with tasks[].
   ========================= */
function renderTasks() {
  // Clear existing list items
  taskList.innerHTML = "";

  // We'll count tasks visible AFTER filters (for stats)
  let visibleCount = 0;

  // Sort a copy so we don't permanently change tasks[] order
  const sortedTasks = tasks.slice();

  sortedTasks.sort(function (a, b) {
    // Incomplete first
    if (a.completed && !b.completed) return 1;
    if (!a.completed && b.completed) return -1;

    // Earlier deadline first (YYYY-MM-DD sorts correctly as string)
    if (a.deadline < b.deadline) return -1;
    if (a.deadline > b.deadline) return 1;

    // Higher priority first
    return b.priority - a.priority;
  });

  // Build UI for each task
  for (let i = 0; i < sortedTasks.length; i++) {
    const task = sortedTasks[i];

    /* ----- Apply filters ----- */
    if (currentFilter === "completed" && task.completed === false) continue;
    if (currentFilter === "incomplete" && task.completed === true) continue;

    if (selectedPriority !== "all" && task.priority !== Number(selectedPriority)) continue;

    // If passed filters, it will be visible
    visibleCount++;

    /* ----- Create <li> item ----- */
    const li = document.createElement("li");
    li.dataset.taskId = String(task.id);
    li.classList.add("task-item");

    // Priority class like p1, p3, p5 (your CSS can color these)
    li.classList.add("p" + task.priority);

    // Add status classes for CSS styling
    if (task.completed) li.classList.add("completed");
    if (!task.completed && isOverdue(task.deadline)) li.classList.add("overdue");
    if (!task.completed && isDueToday(task.deadline)) li.classList.add("due-today");

    /* ----- Display lines ----- */
    const titleLine = document.createElement("div");
    titleLine.textContent = "Title: " + task.title;

    const deadlineLine = document.createElement("div");
    deadlineLine.textContent =
      "Deadline: " + task.deadline +
      (
        !task.completed && isOverdue(task.deadline)
          ? " [OVERDUE]"
          : !task.completed && isDueToday(task.deadline)
            ? " [DUE TODAY]"
            : ""
      );

    const priorityLine = document.createElement("div");
    priorityLine.textContent = "Priority: " + task.priority;

    const descriptionLine = document.createElement("div");
    descriptionLine.textContent = "Description: " + task.description;

    /* ----- Keep stable id for handlers ----- */
    const taskId = task.id;

    /* ----- Completed checkbox ----- */
    const completedLine = document.createElement("div");
    const checkbox = document.createElement("input");
    checkbox.type = "checkbox";
    checkbox.checked = task.completed;

    checkbox.addEventListener("change", function () {
      // Update real tasks[] by id
      for (let k = 0; k < tasks.length; k++) {
        if (tasks[k].id === taskId) {
          tasks[k].completed = this.checked;
          tasks[k].updatedAt = new Date().toISOString();
          break;
        }
      }
      saveTasks();
      renderTasks();
    });

    completedLine.appendChild(document.createTextNode("Completed "));
    completedLine.appendChild(checkbox);

    /* ----- Delete button ----- */
    const deleteBtn = document.createElement("button");
    deleteBtn.type = "button";
    deleteBtn.textContent = "Delete";
    deleteBtn.className = "btn btn-delete";

    deleteBtn.addEventListener("click", function () {
      if (!confirm("Delete this task?")) return;

      // Remove task by id
      tasks = tasks.filter(function (t) {
        return t.id !== taskId;
      });

      // If user deletes the task they were editing, exit edit mode
      if (editingTaskId === taskId) exitEditMode();

      saveTasks();
      renderTasks();
      showMessage("Task deleted.");
    });

    /* ----- Edit button ----- */
    const editBtn = document.createElement("button");
    editBtn.type = "button";
    editBtn.textContent = "Edit";
    editBtn.className = "btn btn-edit";

    editBtn.addEventListener("click", function () {
      editingTaskId = taskId;

      // Find the latest task from tasks[]
      let t = null;
      for (let m = 0; m < tasks.length; m++) {
        if (tasks[m].id === taskId) {
          t = tasks[m];
          break;
        }
      }
      if (!t) return;

      // Fill form inputs with task values
      titleElement.value = t.title;
      descriptionElement.value = t.description;
      deadlineElement.value = t.deadline;
      priorityElement.value = String(t.priority);

      submitBtn.textContent = "Save Task";
      cancelEditBtn.style.display = "inline";
      titleElement.focus();
    });

    /* ----- Assemble list item ----- */
    li.appendChild(titleLine);
    li.appendChild(deadlineLine);
    li.appendChild(priorityLine);
    li.appendChild(descriptionLine);
    li.appendChild(completedLine);
    li.appendChild(deleteBtn);
    li.appendChild(editBtn);

    taskList.appendChild(li);
  }

  /* ----- Empty state message ----- */
  if (taskList.children.length === 0) {
    const empty = document.createElement("li");
    empty.textContent = (tasks.length === 0)
      ? "No tasks yet. Add one above!"
      : "No tasks match your filter.";
    taskList.appendChild(empty);
  }

  /* ----- Update stats after rendering ----- */
  updateStats(visibleCount);
}


/* =========================
   13) INITIAL RUN
   Set default filter UI + render tasks on page load.
   ========================= */
setActiveFilterButton();
renderTasks();
