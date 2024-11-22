# react-notes
A place for my React learning notes.
## What is JSX?
JSX stands for JavaScript XML. It is a syntax extension for JavaScript that looks similar to HTML but is used within JavaScript code.
JSX allows you to write HTML tags within JavaScript code. React then takes this JSX code and converts it into JavaScript that the browser can understand.

**function HelloWorld() {
  return <h1>Hello, world!</h1>;
}**
This JSX will be compiled into JavaScript code like this:
**function HelloWorld() {
  return React.createElement('h1', null, 'Hello, world!');
}**
In JSX, you can only return one single element from a component. If you want to return multiple elements, you have to wrap them in a parent element.
**function MyComponent() {
  return (
    <div>
      <h1>Hello</h1>
      <p>World</p>
    </div>
  );
}**

## Expressions in JSX
We can embed JavaScript expressions directly in JSX by wrapping them in curly braces {}.
**function Greeting() {
  const name = 'John';
  return <h1>Hello, {name}!</h1>;
}**

## Why Use JSX?
**Readability:** It allows you to write HTML-like code in JavaScript, which makes the code more readable and familiar.
**Performance:** JSX is compiled to React.createElement() calls that optimize rendering and performance.
**Integration:** JSX can easily be integrated with JavaScript, making it more flexible to add dynamic content and interactivity.

## Example
**function App() {
  let count = 0;  // Regular JavaScript variable to track the count
  const increment = () => {
    count += 1;  // Increment the count
    document.getElementById("countDisplay").innerText = `Current Count: ${count}`;  // Update the displayed count
  };
  return (
    <div>
      <h1>Simple Counter Example</h1>
      <p>Click the button to increase the count:</p>
      <button onClick={increment}>Increment</button>
      <p id="countDisplay">Current Count: {count}</p>
    </div>
  );
}
export default App;**

## Functional Components
Functional components are simple JavaScript functions that return JSX. They are used to create components in React and are the most commonly used type of component today.

Basic Syntax of Functional Components:
**function Greeting() {
  return <h1>Hello, welcome to React!</h1>;
}
export default Greeting;**

We can then use this component in other components by importing and rendering it inside JSX
import Greeting from './Greeting'; // Import the component

**function App() {
  return (
    <div>
      <Greeting />
    </div>
  );
}
export default App;**

## Class Components
Class components are older and use the class syntax to define components. They were once the standard for creating components that had internal state or lifecycle methods, but nowadays, functional components with hooks are preferred.

Basic Syntax of Class Components:
**import React, { Component } from 'react';
class Greeting extends Component {
  render() {
    return <h1>Hello, welcome to React!</h1>;
  }
}
export default Greeting;**

## Key Differences Between Functional and Class Components:
## Syntax:
Functional components are simpler and written as functions.
Class components are written using ES6 classes.

## State:
Class components can have state and lifecycle methods.
In functional components, state and lifecycle methods are handled using hooks like useState and useEffect (which we haven't covered yet).

## Usage:
Functional components are generally preferred because they are simpler and easier to understand.
Class components are used in older codebases but are being replaced by functional components with hooks.

## Props: Passing Data Between Components
In React, props (short for "properties") are used to pass data from a parent component to a child component. Props are read-only, meaning they cannot be modified by the child component that receives them.

## Example
## Parent Component (App.jsx)

**import React from 'react';
import Greeting from './Greeting';
function App() {
  const userName = "John"; // Data to pass as a prop
  return (
    <div>
      <Greeting name={userName} />
    </div>
  );
}
export default App;**

## Child Component (Greeting.jsx)
**import React from 'react';
function Greeting(props) {
  return (
    <div>
      <h1>Hello, {props.name}!</h1>
      <p>Welcome to learning React with props.</p>
    </div>
  );
}
export default Greeting;**

## State in React
State is a special object in React that holds information about a component. This data can change over time, and React re-renders the component whenever the state updates, ensuring the UI stays in sync with the data.

## Example

**import React, { useState } from 'react';
function Counter() {
  // Step 1: Declare a state variable called 'count' with an initial value of 0
  const [count, setCount] = useState(0);
  // Step 2: Define a function to update the state
  const increment = () => {
    setCount(count + 1); // Update the state with the new value
  };
  return (
    <div>
      <h1>Counter: {count}</h1>
      <button onClick={increment}>Increment</button>
    </div>
  );
}
export default Counter;**

Code Explanation:
State Declaration:
const [count, setCount] = useState(0);

count starts at 0.
setCount is a function used to update the count.
Updating State:

When the Increment button is clicked, the increment function runs.
setCount(count + 1) updates the state to count + 1.
Dynamic Rendering:

When count changes, React automatically re-renders the component to display the new value.

## Another Example: Dynamic List of Items

**import React, { useState } from "react";
function App() {
  const [items, setItems] = useState([]); // State to hold the list of items
  const [inputValue, setInputValue] = useState(""); // State to hold the input value
  const handleAddItem = () => {
    if (inputValue.trim() !== "") {
      setItems([...items, inputValue]); // Add the new item to the list
      setInputValue(""); // Clear the input field
    }
  };
  return (
    <div>
      <h1>Dynamic List</h1>
      <input
        type="text"
        placeholder="Enter an item"
        value={inputValue}
        onChange={(e) => setInputValue(e.target.value)} // Update input value
      />
      <button onClick={handleAddItem}>Add Item</button>
      <ul>
        {items.map((item, index) => (
          <li key={index}>{item}</li> // Render each item in the list
        ))}
      </ul>
    </div>
  );
}
export default App;**

What Happens Here:
State Variables:

items: An array to hold the list of items.
inputValue: Tracks the value of the input field.
Updating Input:

The onChange event updates inputValue whenever the user types something in the input field.
Adding Items:

When the "Add Item" button is clicked, the handleAddItem function:
Adds the current inputValue to the items array.
Clears the inputValue to reset the input field.
Rendering Items:

Each item in the items array is rendered as a list item (<li>) inside the <ul>

## Event Handling in React
In React, event handling means detecting and responding to user interactions such as clicks, key presses, mouse movements, or form submissions. React uses a synthetic event system, which ensures events work consistently across all browsers.


Event Handling in React
In React, event handling means detecting and responding to user interactions such as clicks, key presses, mouse movements, or form submissions. React uses a synthetic event system, which ensures events work consistently across all browsers.

# How It Works
Events are written as camelCase: Instead of writing onclick, React uses onClick.
Pass a function as the event handler: The event handler is the code that should run when the event happens.
Event object: React provides an event object (e) to access details about the event.

**function App() {
  const handleSubmit = (e) => {
    // Prevent the page from refreshing on form submission
    e.preventDefault();
    alert("Form submitted successfully!");
  };
  return (
    <div>
      <h1>Form Submission Example</h1>
      <form onSubmit={handleSubmit}>
        <label htmlFor="name">Enter your name:</label>
        <input type="text" id="name" />
        <button type="submit">Submit</button>
      </form>
    </div>
  );
}
export default App;**

## Component Lifecycle (Class Components)
A component lifecycle refers to the series of events that happen from the creation to the destruction of a component. This lifecycle can be broken down into three main phases:

**Mounting:** The component is being created and inserted into the DOM.
**Updating:** The component is being re-rendered due to changes in state or props.
**Unmounting:** The component is being removed from the DOM.
Each of these phases has lifecycle methods that you can override to run code at specific points in the component's life.

**import React, { Component } from 'react';
class LifecycleExample extends Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0,
      data: null,
    };
    console.log('Constructor: Component is being created');
  }
  // 1. componentDidMount - Called after the component is mounted (rendered) to the DOM
  componentDidMount() {
    console.log('componentDidMount: Component has been mounted');
    // Simulating data fetching
    setTimeout(() => {
      this.setState({ data: 'Fetched Data' });
    }, 2000);
  }
  // 2. componentDidUpdate - Called after the component is updated (re-rendered)
  componentDidUpdate(prevProps, prevState) {
    console.log('componentDidUpdate: Component has been updated');
    if (this.state.count !== prevState.count) {
      console.log(`Count has changed to: ${this.state.count}`);
    }
    if (this.state.data !== prevState.data) {
      console.log('Data has been updated: ', this.state.data);
    }
  }
  // 3. componentWillUnmount - Called before the component is unmounted (removed from the DOM)
  componentWillUnmount() {
    console.log('componentWillUnmount: Component is about to be removed');
    // Cleanup operations like cancelling API calls, clearing timeouts, etc.
  }
  handleClick = () => {
    this.setState((prevState) => ({ count: prevState.count + 1 }));
  };
  render() {
    console.log('render: Component is being rendered');
    return (
      <div>
        <h1>React Lifecycle Example</h1>
        <p>Count: {this.state.count}</p>
        <button onClick={this.handleClick}>Increment Count</button>
        {this.state.data ? <p>{this.state.data}</p> : <p>Loading data...</p>}
      </div>
    );
  }
}
export default LifecycleExample;**

# Explanation of the Code:
**Constructor:** This is where we initialize the state and bind methods. We also log when the component is being created.

**componentDidMount:** Once the component is mounted to the DOM, we simulate an API call with setTimeout to fetch data. After 2 seconds, the state is updated with some fetched data, triggering a re-render.

**componentDidUpdate:** This method is called after any update (like state changes or prop changes). We check if the state has changed, and if so, log the new state or data.

**componentWillUnmount:** This method is called right before the component is removed from the DOM. It’s a place where you clean up resources, such as canceling timers, removing event listeners, or aborting API calls.

**handleClick:** This method updates the count state whenever the button is clicked.

# What Happens in the App:
When the component is first rendered, it will show the count and a "Loading data..." message.
After 2 seconds, the data will change to "Fetched Data", simulating an API call.
Every time the button is clicked, the count will increase, and the component will re-render.

##  useEffect
useEffect is a hook that allows you to perform side effects in a component, such as fetching data, directly interacting with the DOM, or setting up subscriptions.
Executes after the component renders.
Can depend on specific variables (dependency array).
Replaces lifecycle methods like componentDidMount, componentDidUpdate, and componentWillUnmount.

**import React, { useState, useEffect } from 'react';
function FetchData() {
  // Step 1: Initialize state for data
  const [data, setData] = useState([]);
  const [loading, setLoading] = useState(true);
  // Step 2: Fetch data when component mounts
  useEffect(() => {
    fetch('https://jsonplaceholder.typicode.com/posts')
      .then(response => response.json())
      .then(json => {
        setData(json);
        setLoading(false);
      });
  }, []); // Empty dependency array: Runs only once when the component mounts
  return (
    <div>
      <h1>Data from API</h1>
      {loading ? (
        <p>Loading...</p>
      ) : (
        <ul>
          {data.slice(0, 5).map(post => (
            <li key={post.id}>{post.title}</li>
          ))}
        </ul>
      )}
    </div>
  );
}
export default FetchData;**

## useContext
useContext is a hook that allows components to access and share data from React’s Context API without passing props manually through every component in the tree.

**import React, { useContext } from 'react';
// Step 1: Create Context
const ThemeContext = React.createContext();
function ThemeProvider({ children }) {
  const theme = "dark"; // Value to share globally
  return (
    <ThemeContext.Provider value={theme}>
      {children}
    </ThemeContext.Provider>
  );
}
function ThemedButton() {
  // Step 2: Use Context in a component
  const theme = useContext(ThemeContext);
  return (
    <button style={{ background: theme === "dark" ? "#333" : "#fff", color: theme === "dark" ? "#fff" : "#000" }}>
      I am a {theme} button
    </button>
  );
}
function App() {
  return (
    <ThemeProvider>
      <ThemedButton />
    </ThemeProvider>
  );
}
export default App;**

Explanation:
Theme Context:

ThemeContext is a shared context created using React.createContext.
Provider:

ThemeProvider wraps all components that need access to the theme value.
Provides the value "dark" globally.
Consumer:

useContext accesses the theme in ThemedButton.
Styles the button based on the theme value.

## Summary of Hooks:
Hook	    Purpose	                        Example Use Case
useState	Manage local component state.    	Tracking a counter, form inputs.
useEffect	Perform side effects (like data fetching or cleanup).	API calls, event listeners.
useContext	Share data globally without prop drilling.	Theme, user authentication.

## useReducer
At a very basic level, useReducer is a React Hook used to manage complex state in your application.

Think of it as an alternative to useState when:

You have multiple state values that are connected.
Updating state becomes hard to manage with useState.

It works like a mini-state machine:
State: Represents the current data of your app (e.g., counter value, user info).
Action: Describes what you want to do to the state (e.g., increase counter, update name).
Reducer Function: A function that decides how the state should change based on the action.

**import React, { useReducer } from "react";
// 1. Define the reducer function
function counterReducer(state, action) {
  switch (action.type) {
    case "increment":
      return { count: state.count + 1 }; // Increase count
    case "decrement":
      return { count: state.count - 1 }; // Decrease count
    case "reset":
      return { count: 0 }; // Reset count to 0
    default:
      return state; // Return current state for unknown actions
  }
}
function Counter() {
  // 2. Set up useReducer with initial state and reducer function
  const initialState = { count: 0 };
  const [state, dispatch] = useReducer(counterReducer, initialState);
  return (
    <div>
      <h1>Counter: {state.count}</h1>
      <button onClick={() => dispatch({ type: "increment" })}>Increment</button>
      <button onClick={() => dispatch({ type: "decrement" })}>Decrement</button>
      <button onClick={() => dispatch({ type: "reset" })}>Reset</button>
    </div>
  );
}
export default Counter;**

## How This Works
# Reducer Function:

counterReducer is the logic that decides how the state changes for each action.
It takes:
state: Current state, e.g., { count: 0 }.
action: An object describing what to do, e.g., { type: 'increment' }.
Initial State:

The counter starts at { count: 0 }.
Dispatch:

dispatch is used to send an action to the reducer.
For example:
dispatch({ type: "increment" }) increases the counter.
Actions:

Each type in the action object triggers a specific change in state:
"increment" adds 1.
"decrement" subtracts 1.
"reset" resets the counter to 0.

## useMemo
useMemo is a React Hook that helps optimize your app by memorizing the result of a calculation so that it doesn’t get recomputed unnecessarily.
Use it to optimize performance when you have:
Expensive calculations that take time to compute.
Values derived from props or state that don’t change frequently.
Situations where recalculating would cause unnecessary re-renders.

**import React, { useState, useMemo } from 'react';
function ExpensiveCalculation() {
  const [count, setCount] = useState(0);
  const [number, setNumber] = useState(5);
  // Expensive function to calculate a factorial
  const calculateFactorial = (n) => {
    console.log('Calculating factorial...');
    if (n <= 0) return 1;
    return n * calculateFactorial(n - 1);
  };
  // useMemo to memoize the result of the calculation
  const factorial = useMemo(() => calculateFactorial(number), [number]);
  return (
    <div>
      <h1>useMemo Example</h1>
      <div>
        <p>Factorial of {number}: {factorial}</p>
        <button onClick={() => setNumber((prev) => prev + 1)}>Increase Number</button>
        <button onClick={() => setNumber((prev) => prev - 1)}>Decrease Number</button>
      </div>
      <div>
        <p>Count: {count}</p>
        <button onClick={() => setCount((prev) => prev + 1)}>Increase Count</button>
      </div>
    </div>
  );
}
export default ExpensiveCalculation;**

# How it Works:

# Without useMemo:
The factorial calculation (calculateFactorial) runs every time the component re-renders, even when the count changes.
This wastes resources.

# With useMemo:
The calculation only runs when number changes, not when count changes.
The result of the factorial calculation is stored (memoized) and reused.

## What is Routing in React?
Routing allows you to create multiple "pages" in your React app, enabling users to navigate between them without reloading the whole page. React Router is the library we use to handle this.

Key Concepts:
1. BrowserRouter
It acts as the parent component that enables routing in your React app.
It manages the history of your routes (URLs).
2. Route
A Route defines what to render when the app's URL matches a specific path.
3. Link
It is used to create navigation links (like buttons or text) to other pages.
Works like an anchor tag (<a>), but avoids full-page reloads.
4. useParams
A hook to extract dynamic values (parameters) from the URL.
Useful for showing specific data based on the URL.

Where to Use Routing?
Whenever your app needs navigation between different pages like:

Home
About
Profile (with dynamic user IDs)

Install React Router - npm install react-router-dom

# Note: create Home.jsx, About.jsx, Profile.jsx

**import React from 'react';
import { BrowserRouter as Router, Routes, Route, Link } from 'react-router-dom';
import Home from './components/Home';
import About from './components/About';
import Profile from './components/Profile';
const App = () => {
  return (
    <Router>
      <nav>
        <Link to="/">Home</Link> | <Link to="/about">About</Link> | <Link to="/profile/1">Profile</Link>
      </nav>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
        <Route path="/profile/:userId" element={<Profile />} />
      </Routes>
    </Router>
  );
};
export default App;**

## What is API Integration?

API (Application Programming Interface) Integration is the process of connecting your application to a backend server or third-party services to fetch or send data.

**Fetching Data:** This means requesting data from a server using a URL.
**Handling Errors:** Sometimes the request might fail (due to a server issue or bad internet connection). You need to handle such errors in your app.
**Handling Loading:** While waiting for the data to load, you can show a loading spinner or message to the user.

**import React, { useState, useEffect } from 'react';
function FetchDataExample() {
  // States to manage data, loading, and error
  const [data, setData] = useState(null);  // To store fetched data
  const [loading, setLoading] = useState(true);  // To track loading state
  const [error, setError] = useState(null);  // To store error message
  // Use useEffect to fetch data when component is mounted
  useEffect(() => {
    // Fetch data from an API (example: JSONPlaceholder)
    fetch('https://jsonplaceholder.typicode.com/posts')
      .then(response => {
        // Check if the response is successful
        if (!response.ok) {
          throw new Error('Something went wrong!');
        }
        return response.json(); // Parse the JSON data
      })
      .then(fetchedData => {
        setData(fetchedData); // Save data to state
        setLoading(false); // Set loading to false
      })
      .catch(err => {
        setError(err.message); // Handle any error
        setLoading(false); // Set loading to false even if there is an error
      });
  }, []); // Empty dependency array ensures this runs only once (on mount)
  // Return loading, error or data
  if (loading) {
    return <div>Loading...</div>; // Show loading message
  }
  if (error) {
    return <div>Error: {error}</div>; // Show error message if there's an error
  }
  return (
    <div>
      <h1>Fetched Data:</h1>
      <ul>
        {data.map(item => (
          <li key={item.id}>
            <h3>{item.title}</h3>
            <p>{item.body}</p>
          </li>
        ))}
      </ul>
    </div>
  );
}
export default FetchDataExample;**

## Conditional Rendering in React:
Conditional rendering allows you to display different content or components based on certain conditions. It's like saying: "If this condition is true, show this part of the UI, otherwise show something else."

**import React, { useContext } from 'react';
import { ThemeContext } from './ThemeContext';
function ThemeToggler() {
  const { theme, toggleTheme } = useContext(ThemeContext);
  return (
    <div>
      <p>Current Theme: {theme}</p>
      <button onClick={toggleTheme}>
        Switch to {theme === 'light' ? 'dark' : 'light'} mode
      </button>
    </div>
  );
}
export default ThemeToggler;**




