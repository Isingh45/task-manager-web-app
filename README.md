# Task Manager Web Application

## Overview
A browser-based task management application built with HTML, CSS, and vanilla JavaScript[cite: 8]. The app allows users to create tasks with deadlines and priorities, mark tasks as completed, and manage tasks using filtering, sorting, and persistent storage[cite: 8]. The underlying execution engine is designed with a framework-free, resource-conscious mindset to achieve low overhead and high performance[cite: 3, 8].

## Features
* **Add, Edit, and Delete Tasks (CRUD):** Full runtime data lifecycle management supporting dynamic creation, retrieval, input redirection for structural modifications, and memory-safe deletion of records[cite: 8, 9].
* **Mark Tasks as Completed:** Direct state mutation via checkbox inputs, serving as the system's operational switch[cite: 8, 9].
* **Filter Tasks by Status:** Real-time array filtering to isolate records by their status indices (All / Completed / Incomplete)[cite: 8, 9].
* **Filter Tasks by Priority:** Dynamic matrix filtering sorting entries by specific urgency weights (Low / Medium / High)[cite: 8, 9].
* **Automatic Task Sorting:** A deterministic multi-tiered sorting routine evaluating three operational constraint layers simultaneously: Incomplete tasks first $\rightarrow$ Earlier deadlines chronologically $\rightarrow$ Higher priority metrics first[cite: 8, 9].
* **Visual Indicators for Overdue/Due Today:** Time-critical date-parsing helper logic that cross-references the client system clock to dynamically update UI style classes for temporal state transitions[cite: 8, 9].
* **Telemetry Statistics Bar:** A continuous live calculation array displaying system-wide telemetry: total registered tasks, filtered visible nodes, and full completion counts[cite: 8, 9].
* **Persistent Storage:** Custom data retention handling that serializes core state memory into JSON strings for non-volatile browser `localStorage` persistence across power and session cycles[cite: 8, 9].

## Technologies Used
* **HTML5:** Semantic DOM element layouts and clean structural form groupings[cite: 8, 10].
* **CSS3:** Custom component layouts, visible keyboard navigation focus rings, and visual operational state indicators[cite: 8].
* **JavaScript (Vanilla JS):** Core execution engine, deterministic state logic, data pipelines, and hardware-style display-refresh rendering[cite: 8, 9].
* **Browser localStorage API:** Non-volatile local storage configuration for stateless data preservation[cite: 8, 9].

## How to Run
1. Download or clone the repository instance locally[cite: 8].
2. Open the `index.html` file directly in any modern web browser interface[cite: 8, 10].
3. Start managing tasks securely with zero build tools or compiler installations required[cite: 8, 9].

## What I Learned
* **Deterministic Application State Management:** Architected a strict "Single Source of Truth" data pattern where user inputs exclusively mutate a central data array, keeping memory states perfectly synchronized[cite: 8, 9].
* **Dependency-Free DOM Manipulation:** Rebuilt user interfaces from scratch using raw native web APIs, avoiding virtual-DOM framework overhead to guarantee a minimal footprint and fast loading speeds[cite: 8, 9].
* **Non-Volatile Data Persistence:** Implemented robust object serialization and parsing to manage state boundaries and local data retention routines[cite: 8, 9].
* **Structuring Maintainable Codebases:** Developed decoupled, modular JavaScript logic separating structural layout definitions from dynamic behavioral execution scripts[cite: 8, 9].

## Future Improvements
* **Search Functionality:** Implementing high-performance algorithmic string-matching routines to query the data structure array in real time[cite: 8, 9].
* **Improved UI/UX Styling:** Expanding responsive design properties and implementing a unified low-power dark-mode design matrix[cite: 8].
* **Optional Backend Integration:** Engineering full RESTful API endpoints and a relational data engine to transition from local file storage to scalable server-side systems[cite: 8].
