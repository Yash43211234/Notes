# React Notes

## 1. What is React?
- React is a **JavaScript library** for building **user interfaces**.
- Developed and maintained by **Meta (Facebook)**.
- Helps in creating **Single Page Applications (SPA)**.
- Uses a **component-based architecture**.

Example:
```javascript
function App() {
  return <h1>Hello React!</h1>;
}
```

## 2. What is useMemo?

- **useMemo** is a React Hook.

- It memoizes the result of an expensive calculation.

- **Recomputes** only when dependencies change.

- Improves performance.

Example:

```js
import { useMemo } from "react";

function Example({ a, b }) {
  const result = useMemo(() => a + b, [a, b]);
  return <p>Result: {result}</p>;
}

```

## 3. Features of React

- **JSX** – HTML-like syntax inside JavaScript.

- **Virtual DOM** – fast updates.

- **Component-based** – reusable building blocks.

- **Unidirectional data flow** – parent → child.

- **Hooks** – state & lifecycle in functional components.

- **Cross-platform** – React Native for mobile.

## 4. What is JSX?

- JSX stands for **JavaScript XML**.

- Allows writing HTML-like syntax inside JS.

- Makes UI code **declarative and readable**.

Example:
```js
const element = <h1>Welcome to JSX!</h1>;
```

## 5. What is DOM?

- **DOM (Document Object Model)** represents a web page as a tree structure.

- Allows **JavaScript** to update content and styling dynamically.

Example:

```js
// Vanilla JS
document.getElementById("demo").innerHTML = "Hello World";
```

## 6. What is Virtual DOM?

- A **virtual representation** of the real DOM.

- React compares Virtual DOM with Real DOM **(diffing algorithm)**.

- Updates **only changed parts**, improving performance.

Example:

```js
function App() {
  return <p>{new Date().toLocaleTimeString()}</p>;
}

(React updates only the <p> instead of re-rendering the whole page)

```

## 7. Component Life Cycle of React Class Component

Three main phases:

- Mounting Phase

**constructor(), render(), componentDidMount()**

- Updating Phase

**shouldComponentUpdate(), render(), componentDidUpdate()**

- Unmounting Phase

**componentWillUnmount()**

Example:

```js
class MyComponent extends React.Component {
  componentDidMount() {
    console.log("Mounted!");
  }
  componentWillUnmount() {
    console.log("Unmounted!");
  }
  render() {
    return <h1>Hello Lifecycle</h1>;
  }
}
```

## 8. What are Fragments in React?

- Used to group elements without adding extra DOM nodes.

- Shorthand: **<> ... </>**.

Example:

```js

return (
  <>
    <h2>Title</h2>
    <p>Content here</p>
  </>
);

```

## 9. What are Props in React?

- Props = Properties.

- Passed from parent to child.

- *Immutable* in child.

- Help make components reusable.

Example:

```js
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

<Welcome name="Yashwant" />
```

## 10. What are Synthetic Events in React?

- React’s wrapper around native browser events.

- Ensures **cross-browser compatibility**.

- Works like normal events but optimized.

Example:

```js
function Button() {
  return (
    <button onClick={(e) => alert("Clicked! Event type: " + e.type)}>
      Click Me
    </button>
  );
}
```