---
title: "React Calculator App"
date: 2024-11-28
draft: false
hideToc: true
tags: ["Frontend", "React", "Components", "Hooks", "useState", "useRef", "JavaScript", "preventDefault()"]
---

# Greetings
Hello from a pationate beginner to front-end development!<br>
I hope that this post finds you healthy and well, you are having a good day and you are working towards your goals.

In case you are having a bad day, the only advice that I can give you is, control the things that are in your sphere of influence and accept everything else. If you are in a dark place, be the light!
May God help you overcome your battles as He overcame the world!

# React Calculator App
## Intro
As part of my journey to front-end development and actively pursuing the Meta's Front End Developer Professional Certificate offered on Coursera, at the end of the *React Basics* course, a calculator application should have been completed.

It is pretty straightforward so let's start explaining a couple of things.

## React Hooks
### `useState` React Hook
When a component needs to keep track its state then the `useState` hook can be used.<br> The state is being tracked in the `state` variable and the component's state can be changed by using the `setState` function. These data are returned by the hook:
```JavaScript
const [state, setState] = useState(initialState)
```
> `initialState` can be any valid JavaScript type, even functions.
> For more information refer to React's documentation about [useState](https://react.dev/reference/react/useState) hook.

### `useRef` React Hook
According to React's documentation, `useRef` hook lets you reference a value that is not needed for rendering.<br/>
In other words, the hook can be used to persist or preserve values between re-renders.<br/>
```JavaScript
const ref = useRef(initialValue);
```

The question that may arise is <u>*what is a re-render in React?*</u><br/>

When using React, we are constructing a Single-Page Application (SPA). The nature of an SPA is to update only the portion of the page that needs to be updated instead of loading the whole web page anew.<br/>

Therefore, there are two stages that care about:
- **Initial render**, which happens when a component is rendered for the first time on the viewport.
- **Re-render**, which involves any subsequent render of a component which has already passed through the initial render stage.

Finally, the `useRef` hook returns an object with only one property, `current`.
> For more information refer to React's documentation about [useRef](https://react.dev/reference/react/useRef)

## `App` Component
```JavaScript
import {
  useState,
  useRef
} from "react"; 

import "./App.css";

function App() { 
  const inputRef = useRef(null); 
  const resultRef = useRef(null); 
  const [result, setResult] = useState(0); 
 
  function plus(e) { 
    e.preventDefault(); 
    setResult( (result) => result + Number(inputRef.current.value) ); 
  };
 
  function minus(e) { 
  	e.preventDefault();
    setResult( (result) => result - Number(inputRef.current.value)  );
  };
 
  function times(e) { 
    e.preventDefault();
    setResult( (result) => result * Number(inputRef.current.value) );
  }; 
 
  function divide(e) { 
    e.preventDefault();
    setResult( (result) => result / Number(inputRef.current.value) );
  };
 
  function resetInput(e) { 
    e.preventDefault();
    inputRef.current.value = "";
  }; 
 
  function resetResult(e) { 
  	e.preventDefault();
    setResult(0);
  }; 
 
  return ( 
    <div className="App"> 
      <div> 
        <h1>Simplest Working Calculator</h1> 
      </div> 
      <form> 
        <p ref={resultRef}> 
          { result }
        </p> 
        <input
          pattern="[0-9]" 
          ref={inputRef} 
          type="number" 
          placeholder="Type a number" 
        /> 
        <button onClick={ plus }>add</button> 
        <button onClick={ minus }>subtract</button>
        <button onClick={ times }>Multiply</button>
        <button onClick={ divide }>Divide</button>
        <button onClick={ resetInput }>Reset Input</button>
        <button onClick={ resetResult }>Reset Result</button>
      </form> 
    </div> 
  ); 
} 
 
export default App;
```
### Used React Hooks
```JavaScript
const inputRef = useRef(null); 
const resultRef = useRef(null); 
const [result, setResult] = useState(0);
```
Two reference objects have been created using the `useRef` React hook whose initial value is `null`.<br/>
Then the `useState` React hook is used to keep track of the `App` component's state which is stored in the state variable `result`.<br/>
> Observe how the reference objects are bind to the proper DOM elements using the `ref` attribute and passing the reference object in a JSX expression. React will set the `current` property of the reference objects to the DOM node.

### Mathematical Expressions
For the sake of simplicity, let's focus on the addition functionality:
```JavaScript
function plus(e) { 
    e.preventDefault(); 
    setResult( (result) => result + Number(inputRef.current.value) ); 
  };
```
First, the `preventDefault()` method will be analyzed.<br/>
As the MDN Web Docs mentions, the `preventDefault()` method tells the user agent that if the event does not get explicitly handled, its default action should not be taken as it normally would be. In other words, it cancels an event if it is cancelable. Therefore, this statement instructs the browser to avert the button from submitting the form.<br/>

*Do you recall that the reference object's `current` property holds the DOM object?*<br/>
Well, since we have a reference to the `<input>` element, like we would have if we have used the `document.querySelector()` method, we can acquire the value that the user put into the field by accessing the `value` property.<br/>

Finally, the `setResult` function accepts a callback function that calculates the new state from the previous state. The `result` in the parentheses is the pending state or current state, whereas the statement on the right of the arrow (`=>`) is the next state.
# References
- [Refine - Understanding the React useRef Hook](https://refine.dev/blog/react-useref-hook-and-ref/)
- [React - useRef Hook](https://react.dev/reference/react/useRef)
- [React - useState Hook](https://react.dev/reference/react/useState)
- [React -  State as a Snapshot](https://react.dev/learn/state-as-a-snapshot)
- [Dev - Re-render in React](https://dev.to/adevnadia/react-re-renders-guide-why-components-re-render-4ml#:~:text=Re%2Drender%20happens%20when%20React,request%20or%20some%20subscription%20model.)
- [MDN - preventDefault()](https://developer.mozilla.org/en-US/docs/Web/API/Event/preventDefault)
- [W3Schools - preventDefault()](https://www.w3schools.com/jsref/event_preventdefault.asp)