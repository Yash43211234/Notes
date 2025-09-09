# 31. What are Portals in React?
- Portals allow rendering a component’s children into a **different DOM node** outside the root.  
- Useful for modals, tooltips, popups.  

### Example:
```javascript
ReactDOM.createPortal(
  <div>Portal Content</div>,
  document.getElementById("portal-root")
);
```

### 32. What is Context in React?
- A way to **share data globally** without prop drilling.  
- Provides and consumes data using:  
  - **`Context.Provider`**  
  - **`Context.Consumer`** or **`useContext` hook**  

### 33. Example of Context API Usage

```jsx
// Create context
const ThemeContext = React.createContext();

// Provider
function App() {
  return (
    <ThemeContext.Provider value="dark">
      <Child />
    </ThemeContext.Provider>
  );
}

// Consumer with useContext
function Child() {
  const theme = React.useContext(ThemeContext);
  return <h1>Theme is {theme}</h1>;
}
```
### 34. Purpose of Callback in setState()
- `setState` is **asynchronous**.  
- The **callback ensures** that code runs **after the state update and re-render**.  

**Example:**
```jsx
this.setState({ count: this.state.count + 1 }, () => {
  console.log("Updated Count:", this.state.count);
});
```
### 35. Custom Hook for Counter

**Custom Hook:**
```jsx
function useCounter(initial = 0) {
  const [count, setCount] = React.useState(initial);

  const increment = () => setCount(c => c + 1);
  const decrement = () => setCount(c => c - 1);

  return { count, increment, decrement };
}
```

```jsx
function Counter() {
  const { count, increment, decrement } = useCounter(0);

  return (
    <>
      <h1>{count}</h1>
      <button onClick={increment}>+</button>
      <button onClick={decrement}>-</button>
    </>
  );
}
```
### 36. Lifecycle Methods Replaced by useEffect

In **functional components**, `useEffect` replaces several lifecycle methods:

- **`componentDidMount`** → `useEffect(() => { ... }, [])`
- **`componentDidUpdate`** → `useEffect(() => { ... }, [deps])`
- **`componentWillUnmount`** → Cleanup function inside `useEffect`

**Example:**
```jsx
useEffect(() => {
  console.log("Mounted or Updated");

  return () => {
    console.log("Cleanup before unmount");
  };
}, [deps]);
```

### 37. What is StrictMode in React?
- A **tool for highlighting potential problems** in a React app.  
- Helps detect:  
  - Unsafe lifecycle methods  
  - Unexpected side effects  
  - Deprecated APIs  
- Does **not render any visible UI** (only runs checks in development mode).  

**Example:**
```jsx
<React.StrictMode>
  <App />
</React.StrictMode>
```

### 38. Ways to Pass Data from Child to Parent
1. **Using Callback Functions**  
   - Parent passes a function as a prop to child.  
   - Child calls the function to send data back.  

2. **Using Refs**  
   - Parent creates a `ref` and passes it to child.  
   - Child updates/accesses the ref value which parent can read.  

3. **Using Context API or State Management Libraries**  
   - Share data globally via **Context API**, **Redux**, **Zustand**, etc.  

### 39. Example: Child → Parent (Callback Function)

```jsx
function Parent() {
  const handleData = (data) => {
    console.log("Received:", data);
  };

  return <Child sendData={handleData} />;
}

function Child({ sendData }) {
  return (
    <button onClick={() => sendData("Hello Parent")}>
      Send Data
    </button>
  );
}
```
### 40. Example: Child → Parent (useRef)

```jsx
function Parent() {
  const childRef = React.useRef();

  const getData = () => {
    alert(childRef.current.value);
  };

  return (
    <>
      <Child ref={childRef} />
      <button onClick={getData}>Get Data</button>
    </>
  );
}

const Child = React.forwardRef((props, ref) => (
  <input ref={ref} placeholder="Enter text" />
));
```