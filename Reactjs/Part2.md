# Difference between package.json and package-lock.json

## package.json
- Contains **basic info** about the project.  
- Lists **dependencies and versions** (can be flexible like `^1.2.0`).  
- Used to **install project dependencies**.  

## package-lock.json
- Records the **exact version** of every installed package.  
- Ensures **consistency across environments**.  
- Automatically generated when **`npm install`** is run.  

# Difference between Client-Side Rendering (CSR) and Server-Side Rendering (SSR)

| Feature       | CSR (Client-Side Rendering)                  | SSR (Server-Side Rendering)                |
|---------------|-----------------------------------------------|--------------------------------------------|
| **Rendering** | Done in the **browser** using JavaScript     | Done on the **server** before sending HTML |
| **Speed (First Load)** | Slower initial load (needs JS)             | Faster initial load (ready HTML)           |
| **SEO**       | Harder (bots need to execute JavaScript)     | Better for SEO (HTML is ready)             |
| **Interactivity** | Very fast after load                         | Slightly slower than CSR                   |

# 13. What is State in ReactJS?

- State is a **built-in object** that holds data about a component.  
- It is **mutable** (can change over time).  
- When **state changes**, the component **re-renders** to update the UI.  

## Example:
```javascript
import React, { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increase</button>
    </div>
  );
}
```
# 14. What are Props?

- Props are **inputs to components**.  
- Passed from **parent → child**.  
- **Read-only** (cannot be modified by the child component).  

## Example:
```javascript
function Greeting({ name }) {
  return <h1>Hello, {name}</h1>;
}

// Usage
<Greeting name="Yashwant" />
```

# 15. Difference between State and Props

| Feature      | State                              | Props                               |
|--------------|------------------------------------|-------------------------------------|
| **Mutability** | Mutable (can change over time)     | Immutable (read-only)               |
| **Ownership**  | Managed inside the component       | Passed from parent to child         |
| **Usage**      | Stores component’s internal data   | Used for communication between components |

# 16. What is Props Drilling?

- **Props Drilling** happens when props are passed from **parent → child → grandchild**,  
  even if the intermediate components don’t use them.  
- It makes code harder to manage as the app grows.

## Example:
```javascript
// Parent component
function Parent() {
  return <Child data="Some Info" />;
}

// Child component (just passes down the prop)
function Child({ data }) {
  return <GrandChild data={data} />;
}

// Grandchild component (actually uses the prop)
function GrandChild({ data }) {
  return <h2>{data}</h2>;
}
```

# 17. Disadvantages of Props Drilling & How to Avoid

## Disadvantages
- Hard to manage in **large applications**.  
- Creates **unnecessary prop chains** (passing props through many components that don’t use them).  
- Makes components **less reusable** and tightly coupled.  

## How to Avoid
- Use **Context API** for global state sharing.  
- Use **state management libraries** like:
  - Redux  
  - Zustand  
  - Recoil  

  # 18. What are Pure Components in React?

- A **Pure Component** renders only when **props or state change**.  
- Prevents **unnecessary re-renders**, which improves **performance**.  
- Implemented using:
  - `React.PureComponent` (for class components)  
  - `React.memo` (for functional components)  

## Example with React.memo (Functional Component)
```javascript
const MyComponent = React.memo(function(props) {
  return <div>{props.value}</div>;
});
```

### Example with React.PureComponent (Class Component)

```js
import React from "react";

class MyPureComponent extends React.PureComponent {
  render() {
    return <h1>{this.props.name}</h1>;
  }
}

```

# 19. What are Refs in React?

- **Refs** provide direct access to **DOM elements** or **React elements**.  
- They are used for:
  - Setting **focus**  
  - Running **animations**  
  - Integrating with **third-party libraries**  

## Example with useRef (Functional Component)
```javascript
import React, { useRef } from "react";

function InputBox() {
  const inputRef = useRef(null);

  return (
    <>
      <input ref={inputRef} />
      <button onClick={() => inputRef.current.focus()}>
        Focus
      </button>
    </>
  );
}
```

# 20. What is Forward Ref?

- **Forward Ref** allows a component to **pass a ref to its child**.  
- It is useful when the **parent wants direct control** over a child’s DOM element.  

## Example
```javascript
import React, { useRef } from "react";

const Child = React.forwardRef((props, ref) => (
  <input ref={ref} {...props} />
));

function Parent() {
  const inputRef = useRef();

  return (
    <>
      <Child ref={inputRef} />
      <button onClick={() => inputRef.current.focus()}>
        Focus Child
      </button>
    </>
  );
}
```
