# react-guide
Documenting the things which make us cofuse when we start learning react newly.
# React + Vite Startup Flow (Beginner Notes)

## 1. What happens when I create a React project using Vite?

Command:

```bash
npm create vite@latest my-app -- --template react
```

This creates a project structure:

```text
my-app/
├── node_modules/
├── public/
├── src/
│   ├── assets/
│   ├── App.jsx
│   └── main.jsx
├── index.html
├── package.json
├── package-lock.json
├── vite.config.js
└── .gitignore
```

---

# 2. Purpose of Each Important File

## index.html

```html
<body>
  <div id="root"></div>
</body>
```

Purpose:

* The only HTML page Vite serves.
* Contains the container where React will be displayed.

Think of it as:

```text
Empty Room
┌───────────────┐
│               │
└───────────────┘
```

The room is the root div.

---

## main.jsx

```jsx
import ReactDOM from "react-dom/client";
import App from "./App.jsx";

ReactDOM.createRoot(
  document.getElementById("root")
).render(<App />);
```

Purpose:

* Entry point of the React application.
* Connects React to the HTML page.
* Tells React which component to render first.

---

## App.jsx

```jsx
function App() {
  return <h1>Hello React</h1>;
}

export default App;
```

Purpose:

* Main component of the application.
* Usually contains the entire UI structure.

---

# 3. What is document?

In JavaScript:

```js
document
```

represents the entire HTML page loaded in the browser.

Example:

```html
<html>
<body>
  <div id="root"></div>
</body>
</html>
```

JavaScript sees this page through the document object.

Think:

```text
document
│
├── html
│
└── body
     │
     └── div#root
```

---

# 4. What does getElementById() do?

Code:

```js
document.getElementById("root")
```

Meaning:

"Find the HTML element whose id is root."

Result:

```html
<div id="root"></div>
```

Think:

```js
const htmlRoot =
document.getElementById("root");
```

Now htmlRoot refers to that div.

---

# 5. What is the HTML Root?

HTML Root:

```html
<div id="root"></div>
```

This is a normal DOM element.

Browser creates it.

React does not create it.

It already exists in index.html.

---

# 6. What is createRoot()?

Code:

```js
createRoot(htmlRoot)
```

Purpose:

Creates a React Root.

Important:

React Root is NOT another HTML element.

It is a JavaScript object managed by React.

Think:

```js
const reactRoot =
createRoot(htmlRoot);
```

Meaning:

"React, take control of this HTML div."

---

# 7. HTML Root vs React Root

HTML Root

```html
<div id="root"></div>
```

* Real DOM element
* Created by browser
* Exists in HTML

React Root

```js
const reactRoot =
createRoot(htmlRoot);
```

* JavaScript object
* Created by React
* Controls rendering inside the HTML Root

---

# 8. What does render() do?

Code:

```js
reactRoot.render(<App />);
```

Meaning:

"Display the App component inside the React Root."

React executes:

```jsx
<App />
```

which becomes:

```html
<h1>Hello React</h1>
```

and inserts it into:

```html
<div id="root">
  <h1>Hello React</h1>
</div>
```

---

# 9. Complete Flow

Step 1

Browser loads:

```html
<div id="root"></div>
```

↓

Step 2

JavaScript runs:

```js
document.getElementById("root")
```

↓

Gets:

```html
<div id="root"></div>
```

↓

Step 3

```js
createRoot(...)
```

↓

Creates React Root

↓

Step 4

```js
render(<App />)
```

↓

Renders App component

↓

Final Output

```html
<div id="root">
  <h1>Hello React</h1>
</div>
```

---

# 10. What does npm run dev do?

In package.json:

```json
{
  "scripts": {
    "dev": "vite"
  }
}
```

Command:

```bash
npm run dev
```

Meaning:

1. npm looks inside package.json
2. Finds the script named dev
3. Executes:

```bash
vite
```

---

# 11. What does Vite do?

Vite:

* Starts development server
* Loads index.html
* Loads React files
* Rebuilds automatically on changes
* Refreshes browser instantly

Output:

```text
http://localhost:5173
```

Open this URL to see your React app.

---

# 12. Final Mental Model

```text
npm run dev
        │
        ▼
     Vite
        │
        ▼
   index.html
        │
        ▼
<div id="root">
        │
        ▼
document.getElementById("root")
        │
        ▼
createRoot()
        │
        ▼
React Root Created
        │
        ▼
render(<App />)
        │
        ▼
App Component
        │
        ▼
Displayed in Browser
```

Remember:

HTML Root = Browser's container

React Root = React's controller

render(<App />) = Put App inside the container
