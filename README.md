# Task Manager Web Application

## Overview
A browser-based task management application built with HTML, CSS, and vanilla JavaScript. The app allows users to create tasks with deadlines and priorities, mark tasks as completed, and manage tasks using filtering, sorting, and persistent storage. The underlying execution engine is built using a lightweight, framework-free architecture that emphasizes simplicity, maintainability, and efficient client-side execution.


## Features
- **Add, Edit, and Delete Tasks (CRUD):** Supports complete task lifecycle management, allowing users to create, update, and remove tasks while maintaining a synchronized application state.

- **Mark Tasks as Completed:** Direct state mutation via checkbox inputs, serving as the system's operational switch.

- **Filter Tasks by Status:** Real-time array filtering to isolate records by their status indices (All / Completed / Incomplete).

- **Filter Tasks by Priority:** Dynamic matrix filtering sorting entries by specific urgency weights (Low / Medium / High).

- **Automatic Task Sorting:** A deterministic multi-tiered sorting routine evaluating three operational constraint layers simultaneously: Incomplete tasks first → Earlier deadlines chronologically → Higher priority metrics first.

- **Visual Indicators for Overdue/Due Today:** Time-critical date-parsing helper logic that cross-references the client system clock to dynamically update UI style classes for temporal state transitions.

- **Telemetry Statistics Bar:** A continuous live calculation array displaying system-wide telemetry: total registered tasks, filtered visible nodes, and full completion counts.

- **Persistent Storage:** Serializes application data into JSON and stores it using the browser's localStorage API, allowing tasks to persist across page refreshes and browser sessions.

## Technologies Used
* **HTML5:** Semantic DOM element layouts and clean structural form groupings.
* **CSS3:** Custom component layouts, visible keyboard navigation focus rings, and visual operational state indicators.
* **JavaScript (Vanilla JS):** Core execution engine, deterministic state logic, data pipelines, and hardware-style display-refresh rendering.
* **Browser localStorage API:** Non-volatile local storage configuration for stateless data preservation.

## How to Run
1. Download or clone the repository instance locally.
2. Open the index.html file directly in any modern web browser interface.
3. Start managing tasks securely with zero build tools or compiler installations required.

## What I Learned
* **Deterministic Application State Management:** Architected a strict "Single Source of Truth" data pattern where user inputs exclusively mutate a central data array, keeping memory states perfectly synchronized.
* **Dependency-Free DOM Manipulation:** Rebuilt user interfaces from scratch using raw native web APIs, avoiding virtual-DOM framework overhead to guarantee a minimal footprint and fast loading speeds.
* **Non-Volatile Data Persistence:** Implemented robust object serialization and parsing to manage state boundaries and local data retention routines.
* **Structuring Maintainable Codebases:** Developed decoupled, modular JavaScript logic separating structural layout definitions from dynamic behavioral execution scripts.

## Future Improvements
* **Search Functionality:** Implementing high-performance algorithmic string-matching routines to query the data structure array in real time.
* **Improved UI/UX Styling:** Expanding responsive design properties and implementing a unified low-power dark-mode design matrix.
* **Optional Backend Integration:** Engineering full RESTful API endpoints and a relational data engine to transition from local file storage to scalable server-side systems.
