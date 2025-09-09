# 21. What are Error Boundaries?
- Special React components that **catch JavaScript errors** in their child component tree.  
- Prevents the whole app from crashing.  
- Implemented using `componentDidCatch` and `getDerivedStateFromError`.  

### Example:
```javascript
class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError() {
    return { hasError: true };
  }

  componentDidCatch(error, info) {
    console.log(error, info);
  }

  render() {
    if (this.state.hasError) {
      return <h2>Something went wrong.</h2>;
    }
    return this.props.children;
  }
}
```

### 22. What are Higher Order Components (HOC)?
- A **Higher Order Component (HOC)** is a function that takes a component and returns a new component.  
- Used for:  
  - **Code reuse**  
  - **Logic sharing**  
  - **Cross-cutting concerns**  

**Example:**
```jsx
function withLogger(WrappedComponent) {
  return function(props) {
    console.log("Props:", props);
    return <WrappedComponent {...props} />;
  };
}
```

### 23. Controlled vs Uncontrolled Components

| Feature        | Controlled Component (with state) | Uncontrolled Component (with ref) |
|----------------|-----------------------------------|-----------------------------------|
| **Data Handling** | Controlled by React state          | Controlled by DOM                  |
| **Access Value**  | `state`                           | `ref.current.value`                |
| **Use Case**      | Forms with validation             | Simple inputs                      |

---

**Example**

✅ **Controlled Component:**
```jsx
const [value, setValue] = useState("");
<input value={value} onChange={(e) => setValue(e.target.value)} />
```

✅ **Uncontrolled Component:**

```jsx
const inputRef = useRef();
<input ref={inputRef} />
<button onClick={() => console.log(inputRef.current.value)}>Get</button>
```

### 24. What is useCallback?
- A **hook that memoizes a function**.  
- Prevents unnecessary re-creation of functions during re-renders.  

**Example:**
```jsx
const handleClick = useCallback(() => {
  console.log("Clicked!");
}, []);
```

### 25. useMemo vs useCallback

| Feature       | useMemo                              | useCallback                    |
|---------------|--------------------------------------|--------------------------------|
| **Purpose**   | Memoizes **values** (result of function) | Memoizes **functions**          |
| **Returns**   | Cached **value**                     | Cached **function**             |
| **Use Case**  | Expensive calculations               | Prevent re-creating handlers    |

### 26. What are Keys in React?
- **Keys** are unique identifiers used in lists to help React identify elements.  
- They improve performance during the **reconciliation** process by letting React know which items changed, were added, or removed.  

**Example:**
```jsx
{items.map(item => (
  <li key={item.id}>{item.name}</li>
))}
```

### 27. What is Lazy Loading in React?
- **Lazy Loading** means loading components only when they are needed.  
- Helps in **improving performance** and **reducing bundle size**.  

**Example:**
```jsx
const LazyComp = React.lazy(() => import("./LazyComp"));
```
### ✅ Usually used with <Suspense> for fallback UI:

```js
<Suspense fallback={<div>Loading...</div>}>
  <LazyComp />
</Suspense>
```
### 28. What is Suspense in React?
- **Suspense** is a React component used with **lazy loading** (or other async operations) to show a **fallback UI** while waiting for the component to load.  

**Example:**
```jsx
<Suspense fallback={<div>Loading...</div>}>
  <LazyComp />
</Suspense>
```
### 29. What are Custom Hooks?
- **Custom Hooks** are user-defined hooks that allow you to **reuse logic across components**.  
- By convention, their name must start with **`use`**.  

**Example:**
```jsx
function useCounter() {
  const [count, setCount] = useState(0);
  const increment = () => setCount(c => c + 1);
  return { count, increment };
}
```

### 30. What is useReducer Hook?
- **useReducer** is an alternative to `useState` for handling **complex state logic**.  
- It follows the **Redux-like reducer pattern** (state + actions).  

**Example:**
```jsx
function reducer(state, action) {
  switch (action.type) {
    case "increment":
      return { count: state.count + 1 };
    default:
      return state;
  }
}

const [state, dispatch] = useReducer(reducer, { count: 0 });
```