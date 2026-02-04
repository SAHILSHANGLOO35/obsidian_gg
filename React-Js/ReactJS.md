## 1. What is Babel?

- **Babel** is a JavaScript compiler.
- It translates other JavaScript-like languages (such as JSX) into plain **JavaScript**, which browsers understand.

---

## 2. Why do we need Babel?

- When using **React**, we don’t write plain JavaScript only.
- We use an enhanced syntax called **JSX (JavaScript XML)**.
- JSX looks like HTML written inside JavaScript.

Example:

```jsx
const element = <h1>Hello World</h1>;
```

---

## 3. Problem with JSX

- Browsers **do not understand JSX**.
- Browsers understand **only normal JavaScript**.
- So JSX must be **translated (compiled)** into JavaScript.

### Solution: Babel

We use an external JavaScript library called **Babel**.

### Steps:

1. **Load Babel as an external library**

```html
<script src=""></script>
```

2. **Tell Babel to translate JSX** by using the `text/babel` type

```html
<script type="text/babel"></script>
```

---

> **React = an external library that helps us create websites more easily.**

---

## 4. How React helps us create websites easier

- More natural way to write UI
- Easier error detection
- Allows inserting JavaScript directly inside UI elements

---

## 5. State

- **State** is data connected to the UI.
- It stores data that **changes over time**.
- When state updates, React **automatically updates the HTML**.

### `useState`

- `React.useState()` returns an array:
	1. **Current value** → `array[0]`
	2. **Updater function** → `array[1]`
- React updates the UI **only when the updater function is used**.

---

## Spread Operator (`...`) in JavaScript

- It copies values from an existing array/object into a new one.

Example:

```js
const newArray = [...oldArray];
```

---

## `onChange`

- Runs a function when the value of an `<input>` element changes.

---

## CSS Tip

- By default, the `<body>` element has **8px margin** on all sides.

---

## 6. Hooks

- **Hooks** allow us to use React features inside functional components.

---

### `useEffect`

- Runs code **after a component is created or updated**.

```js
useEffect(() => {
  // side-effect code
}, []);
```

#### Dependency Array:

- `[]` → runs **only once** (after first render)
- `[chatMessages]` → runs **every time `chatMessages` changes**

---

### `useRef`

- A **container** with special React behavior.
- Can store:
	- DOM elements
	- Mutable values

#### Use cases:

- Accessing DOM elements
- Storing mutable values
- Avoiding unnecessary re-renders

---

### Rule of Thumb

- Use `useState` → when data affects rendering
- Use `useRef` → when data should **not** trigger re-render

---

## SPA Routing & Links

- Normal `<a>` tags **reload the page**.
- Page reloads make sense when navigating between **multiple HTML files**.
- In **Single Page Applications (SPA)**, page reloads are unnecessary.

### React Router

- React Router provides `<Link />` component.
- `<Link />` navigates between pages **without reloading** the page.

---

## Strict Mode

- `StrictMode` runs **only in development**.
- It intentionally renders components **twice** to help detect bugs early.