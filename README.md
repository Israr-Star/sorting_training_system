# Vue 3 Sorting Game

This project is a sorting game built with Vue 3, Vite, and Tailwind CSS. The goal is to sort a table of people by the number of potatoes they have in descending order using drag-and-drop functionality. A timer tracks the user's speed, and a success message is displayed upon correct sorting.

## Getting Started

### Prerequisites

Ensure you have the following installed:

- [Node.js](https://nodejs.org/) (v16 or later recommended)
- [npm](https://www.npmjs.com/) or [yarn](https://yarnpkg.com/)

### Installation

1. Clone the repository:
   ```sh
   git clone https://github.com/Israr-Star/sorting_training_system
   cd sorting_training_system
   ```
2. Install dependencies:
   ```sh
   npm install  # or yarn install
   ```
3. Start the development server:
   ```sh
   npm run dev  # or yarn dev
   ```
4. Open the application in your browser at `http://localhost:5173` (default Vite port).

## How It Works

1. **Start Sorting:** Click the "Start Sorting" button to open a modal.
2. **Enter a Number:** Input a number between 20 and 100 to specify how many people will be added to the list.
3. **Generate Entries:** Click "Start" to generate random people with:
   - A unique number of potatoes (each entry has a different amount).
   - A random name.
   - A randomly generated email.
     The timer starts automatically when the table is populated.
4. **Sorting:** Drag and drop the table rows to arrange them in descending order based on the potato count.
5. **Win Condition:** Once the list is correctly sorted, the timer stops, and a success message displays the user's score in details.
6. **After Sort:** Table items will no longer be draggable. Clicking on "Start Sorting" will show a confirmation asking if the user wants to sort again. Clicking "OK" will unsort the table and the sorting process will start again as before.

## Technologies Used

- **Vue 3** (Composition API)
- **Vite** (for fast development and build processes)
- **Tailwind CSS** (for styling)
- **Vue Draggable** (for drag-and-drop functionality)

## Development Commands

- Start Development Server:
  ```sh
  npm run dev
  ```
- Build for Production:
  ```sh
  npm run build
  ```
- Preview Production Build:
  ```sh
  npm run preview
  ```
