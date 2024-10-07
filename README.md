# TODO App

## Overview

The **TODO App** is a simple task management application built using Vue.js. It allows users to categorize tasks, add due dates, mark tasks as completed, and delete tasks.

<img src="https://github.com/AreebaSattar/Todo-App-VueJs/blob/main/app/photo5.PNG?raw=true" width="1000">

## Features

- **Task Creation:** Add tasks with a category and a due date/time.
- **Task Completion:** Mark tasks as completed or not completed.
- **Task Deletion:** Remove tasks from the list.
- **Task Overview:** Displays the number of pending and completed tasks.
- **Responsive UI:** A clean, responsive user interface built with Tailwind CSS.

## Technologies Used

- **Vue.js**: A progressive JavaScript framework for building user interfaces.
- **Tailwind CSS**: A utility-first CSS framework for styling the app.
- **vue-datepicker-next**: A Vue.js component to select and manage dates.

## Project Setup

1. Clone the repository:
   ```bash
   git clone <repository-url>
   cd <repository-folder>
2. Install dependencies:
   ```bash
   npm install
3. Start the development server:
   ```bash
   npm run dev
3. Build the project for production:
   ```bash
   npm run build
   
## Usage

- **Add a Task**: Use the form at the top to select a category, add a task description, and choose a due date/time. Click the "+" button to add the task to the list.
- **Complete a Task**: Click the checkmark icon next to a task to mark it as completed.
- **Undo Completion**: Click the undo icon to revert a completed task to pending.
- **Delete a Task**: Click the trash icon to remove a task from the list.
- **Task Overview**: The app will show the number of pending and completed tasks at the top.

## Components

### App Layout

- **Form for Adding Tasks:** Allows users to add tasks with categories and due dates.
- **Task Table:** Displays all tasks, including details like task description, category, start time, and available actions (mark complete, undo, delete).
- **Task Statistics:** Shows how many tasks are pending and completed.

### Key Vue.js Concepts Used

- **Reactivity:** Used `ref` and `computed` to manage the state of tasks.
- **Methods:** Functions to add, complete, undo, and remove tasks.
- **Date Formatting:** Used JavaScript `Date` object to format the task start time.

## Dependencies

- **vue-datepicker-next:** For date and time selection.
- **Tailwind CSS:** For styling.

Install Tailwind CSS and Vue Date Picker by following the setup guides.

## Future Improvements

- **Data Persistence:** Implement local storage or database integration to save tasks between sessions.
- **Task Editing:** Allow users to edit existing tasks.
- **Filtering:** Add functionality to filter tasks based on their category or completion status.

   
