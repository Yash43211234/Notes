# 41. How do you optimize your React application?
- Use **React.memo** / **PureComponent** to avoid unnecessary re-renders.  
- Use **useMemo** and **useCallback** for expensive calculations and functions.  
- Implement **Code Splitting & Lazy Loading**.  
- Use **Pagination / Infinite Scroll** for large lists.  
- Keep state local where possible.  
- Avoid inline functions inside JSX (when performance critical).  

---

# 42. How would you consume a RESTful JSON API in React?
Using **fetch** or **axios** inside `useEffect`.

### Example:
```javascript
function Users() {
  const [users, setUsers] = React.useState([]);

  React.useEffect(() => {
    fetch("https://jsonplaceholder.typicode.com/users")
      .then(res => res.json())
      .then(data => setUsers(data));
  }, []);

  return users.map(u => <p key={u.id}>{u.name}</p>);
}
```
### 43. Different Design Patterns in React

1. **Container & Presentational Components**  
   - *Container Components*: Handle logic, state, and data fetching.  
   - *Presentational Components*: Handle UI rendering only.  
   - Example: `UserContainer` fetches data, `UserCard` displays it.

2. **Higher-Order Components (HOC)**  
   - A function that takes a component and returns a new component.  
   - Used for code reusability (auth checks, theming, logging).  
   - Example: `withAuth(Component)`.

3. **Render Props**  
   - A technique where a component takes a function as a prop to determine what to render.  
   - Example:  
     ```jsx
     <DataFetcher render={(data) => <List items={data} />} />
     ```

4. **Custom Hooks**  
   - Encapsulate reusable logic in a function starting with `use`.  
   - Example: `useFetch()`, `useAuth()`.

5. **Compound Components**  
   - Multiple components working together for flexibility.  
   - Example: `Modal.Header`, `Modal.Body`, `Modal.Footer`.

6. **Controlled vs Uncontrolled Components**  
   - **Controlled**: State is managed by React (`value` and `onChange`).  
   - **Uncontrolled**: State is managed by the DOM (`ref`).  
   - Example:  
     ```jsx
     <input value={name} onChange={(e) => setName(e.target.value)} /> // controlled
     <input ref={inputRef} /> // uncontrolled
     ```

### 44. Context API vs Redux

| Feature       | Context API (React)      | Redux (State Management)             |
|---------------|--------------------------|---------------------------------------|
| **Complexity** | Simple, built-in         | More complex, requires setup          |
| **Use Case**   | Small/medium apps        | Large apps with complex state         |
| **Performance**| Can cause unnecessary re-renders | Optimized with middleware & selectors |
| **Tools**      | Only React (no extra lib) | Redux DevTools, middleware (Thunk, Saga) |
| **Learning Curve** | Easy to learn        | Steeper learning curve                |
| **Data Flow**  | Top-down (via Provider)  | Centralized global store              |
| **Best For**   | Theme, auth, user prefs  | Enterprise apps, multi-source data     |

### 45. PropTypes in React (Validation)

`prop-types` package is used to **validate props** in React components.  
It helps catch bugs by ensuring props have the correct type.

#### Example:
```jsx
import PropTypes from "prop-types";

function User({ name, age }) {
  return <h1>{name} - {age}</h1>;
}

User.propTypes = {
  name: PropTypes.string.isRequired,  // must be string
  age: PropTypes.number               // optional, must be number
};
```

### 46. What are React Mixins?
- **Old React (pre ES6)** way to reuse functionality across components.  
- Used with `createReactClass`.  
- ❌ Now deprecated and replaced by **HOCs** and **Hooks**.  

---

### 47. Different Hooks in React
- **useState** – Manage state in functional components.  
- **useEffect** – Handle side effects (API calls, subscriptions, timers).  
- **useContext** – Consume context values without prop drilling.  
- **useRef** – Access DOM elements and store persistent values.  
- **useMemo** – Memoize values to avoid recalculations.  
- **useCallback** – Memoize functions to prevent unnecessary re-renders.  
- **useReducer** – Manage complex state logic (alternative to useState).  
- **useLayoutEffect** – Run effects **synchronously after DOM mutations**.  
- **Custom Hooks** – User-defined hooks to encapsulate logic.  

### 48. What are Render Props in React?
- A **technique** where a component’s **prop is a function** that controls rendering.  
- Useful for sharing logic between components.  

**Example:**
```jsx
function DataProvider({ render }) {
  const [data] = React.useState("Hello");
  return render(data);
}

// Usage
<DataProvider render={(data) => <h1>{data}</h1>} />
```

### 49. Types of Exports and Imports

#### 1. **Default Export**
- Only **one default export** per file.  
- Imported without curly braces.  

**Example:**
```jsx
// App.js
export default function App() {}

// Import
import App from "./App";
```

### 2. **Named Export**

- Allows multiple exports per file.
- Imported using curly braces.

**Example:**

```js
// math.js
export const add = () => {};
export const subtract = () => {};

// Import
import { add, subtract } from "./math";
```

### 50. `createElement` vs `cloneElement`

#### 1. **React.createElement**
- Creates a **new React element**.  
- Commonly used under the hood when using JSX.  

**Example:**
```jsx
const element = React.createElement("h1", null, "Hello");
```

### 51. When to use `useState` vs `useReducer`

#### **useState**
- Best for **simple local state**.  
- Examples: counters, toggles, form inputs.  

```jsx
const [count, setCount] = useState(0);
```

#### useReducer

- Best for complex state logic with multiple sub-values or actions.
- Follows a reducer pattern similar to Redux.

```js
function reducer(state, action) {
  switch (action.type) {
    case "increment": return { count: state.count + 1 };
    case "decrement": return { count: state.count - 1 };
    default: return state;
  }
}

const [state, dispatch] = useReducer(reducer, { count: 0 });
```

### 52. What are Protected Routes in React?

- **Protected Routes** are routes that require **authentication** before access.  
- Commonly used in apps with login systems to restrict access to certain pages.  

#### Example:
```jsx
import { Navigate } from "react-router-dom";

function PrivateRoute({ children }) {
  const isAuth = localStorage.getItem("token");
  return isAuth ? children : <Navigate to="/login" />;
}
```

### 53. Does React Router support a Context Menu?

- **React Router does not directly support context menus.**  
- But you can implement it manually using:  
  - `onContextMenu` (right-click event).  
  - A custom context menu component.  
  - `useNavigate` from React Router to navigate programmatically.  

#### Example:
```jsx
import { useNavigate } from "react-router-dom";

function MyComponent() {
  const navigate = useNavigate();

  const handleRightClick = (e) => {
    e.preventDefault(); // Prevent default browser context menu
    navigate("/custom-path"); // Navigate on right-click
  };

  return <div onContextMenu={handleRightClick}>Right Click Me</div>;
}
```
