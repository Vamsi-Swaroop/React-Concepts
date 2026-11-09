## What is React?
React is a Javascript Library which is used to build frontend applications by the means of dynamic reusable UI components.

## What is JSX, Component, props?
 JSX stands for JavaScript XML which is similar to HTML like structure. It is an extension to build HTML structures directly rendered on the screen.
 Component is the building block of React application. It is independent, reusable and basic structures of React.
 Props is a shortcut for properties.They are used to pass data from parent component to child component.The child can not modify the data of the props, it shuld use the data as is.

 ## What is babel and what role it plays in the React?
Babel is a tool that is used to convert JSX and modren javascript to a Browser compatible code such that it runs in all environments.

## What is difference between Virtual DOM & Real DOM?
Virtual DOM is light weight representation of the DOM by React. The DOm that is present on browser is termed as Real DOM.Virtual DOM works by creating an in-memory representation of the Real DOM, allowing developers to make changes without directly affecting the actual page.

## What is a bundler?
A budnler is a tool that can combine all individual files (JavaScript, CSS files) and optimses into lesser files for the efficient understanding of the browser.

## Why we are not using Create React App, but the vite for the React projects?
Create-React-App is the older way of creating a react app. It has been deprecated due to its sluggishness, in the place of it we can create react application by using Vite.

## Folder Structure and BoilerPlate code of React
React project will have the following Folders and files by default:
  1. Node Modules Folder: This contains all external libraries installed in the project.
  2. App.css : It contains styling that is confined to the React Application.
  3. Index.css : Contains styling that is globally applicable.
  4. main.jsx : This file connects react to the actual DOM element.
  5. index.html: It is the main html file that the browser loads by default.
  6. package.json: It contains project information, dependencies and scripts.It allows minor updates and patch updates if required.
  7. package-lock.json: It contains exact dependencies used by the projects.
  8. App.jsx : This is the main component or root UI component for the React App.

## Diff. between Class & Functional components
React offers two types of components class based components and functional components.We can directly return JSX from function based components, where as in class based componets we use constructor and requires a render method.

## What are hooks in React?
Hooks are special functions that  allow us to use react properties such as state, lifr cycle based behaviour.

## Basic Hooks: useState, useEffect, useRef

Some of the basic hooks in React are:

1. **useState:**

   `useState` is a React hook that allows functional components to manage state. It returns two values: the current state and a function to update the state.

   Example:
   ```jsx
   import { useState } from 'react';

   const Counter = () => {
       const [count, setCount] = useState(0);

       return (
           <>
               <h2>Count: {count}</h2>
               <button onClick={() => setCount(count + 1)}>
                   Increment
               </button>
           </>
       );
   };

   export default Counter;
   ```

2. **useEffect:**

   `useEffect` is used to perform side effects in functional components. Side effects include fetching data from APIs, setting up subscriptions, and updating document-related information.

   Example:
   ```jsx
   import { useEffect } from 'react';

   useEffect(() => {
       console.log('Component mounted');

       return () => {
           console.log('Component unmounted');
       };
   }, []);
   ```

   The empty dependency array ensures that the effect runs after the component's initial render. The cleanup function runs when the component is unmounted.

3. **useRef:**

   `useRef` is a React hook that allows us to store a mutable value that persists between renders without triggering a re-render when its value changes. It is also commonly used to access DOM elements directly.

   Example:
   ```jsx
   import { useRef } from 'react';

   const InputComponent = () => {
       const inputRef = useRef(null);

       const handleFocus = () => {
           inputRef.current.focus();
       };

       return (
           <>
               <input ref={inputRef} />
               <button onClick={handleFocus}>Focus Input</button>
           </>
       );
   };

   export default InputComponent;
   ```

## How to pass the data from one component to another component?

In React, data is generally passed from a parent component to a child component using **props**.

Example:

```jsx
const Child = ({ name }) => {
    return <h2>Hello, {name}!</h2>;
};

const Parent = () => {
    return <Child name="React Developer" />;
};

export default Parent;
```

In this example, the Parent component passes the `name` value to the Child component through props.

If a child component needs to communicate with its parent, we can pass a callback function as a prop. The child can invoke this function to send information back to the parent.

Example:

```jsx
const Child = ({ onSend }) => {
    return (
        <button onClick={() => onSend('Hello Parent!')}>
            Send Message
        </button>
    );
};

const Parent = () => {
    const handleMessage = (message) => {
        console.log(message);
    };

    return <Child onSend={handleMessage} />;
};

export default Parent;
```

## What is lifting state up?

Lifting state up is a concept in React where we move the state from a child component to its nearest common parent component when multiple components need to access or share the same data.

This helps maintain a single source of truth and keeps the data synchronized between components.

Example:

```jsx
import { useState } from 'react';

const ChildOne = ({ count, onIncrement }) => {
    return (
        <button onClick={onIncrement}>
            Increment: {count}
        </button>
    );
};

const ChildTwo = ({ count }) => {
    return <h2>Current Count: {count}</h2>;
};

const Parent = () => {
    const [count, setCount] = useState(0);

    return (
        <>
            <ChildOne
                count={count}
                onIncrement={() => setCount(count + 1)}
            />
            <ChildTwo count={count} />
        </>
    );
};

export default Parent;
```

In this example, the state is maintained in the Parent component and passed to both ChildOne and ChildTwo through props.

When ChildOne updates the state using the callback function, ChildTwo automatically receives the updated value.

## How to use event listeners in the component?

React provides event handling through JSX attributes. We can handle user interactions such as clicks, input changes, form submissions, and keyboard events using event handlers.

React uses camelCase naming conventions for event handlers, such as `onClick`, `onChange`, and `onSubmit`.

Example:

```jsx
const EventComponent = () => {

    const handleClick = () => {
        alert('Button clicked!');
    };

    const handleChange = (event) => {
        console.log(event.target.value);
    };

    return (
        <>
            <button onClick={handleClick}>
                Click Me
            </button>

            <input
                type="text"
                onChange={handleChange}
                placeholder="Enter your name"
            />
        </>
    );
};

export default EventComponent;
```

In this example:

1. `onClick` handles the button click event.
2. `onChange` handles changes in the input field.
3. The event object provides information about the event, including the target element and its value.

Unlike traditional JavaScript, where we often use `addEventListener()`, React generally handles events directly through JSX event attributes.
