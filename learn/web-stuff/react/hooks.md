# Hooks

## Overview

Hooks are function which we can use to hook into React features.

React hooks can be only used with functional components. 

The execution order of the hooks should always be same. Meaning it cannot be inside conditional statements, loops or nested functions. Only Call Hooks at the Top Level. [`eslint-plugin-react-hooks`](https://www.npmjs.com/package/eslint-plugin-react-hooks)

## useState

`useState(DEFAULT_STATE_VALUE): [CURRENT_STATE_VALUE, STATE_UPDATING_FUNCTION()]`

Takes in a default value & returns array containing current state value & a function which can be used to update the state. Every time there is new state the component is re-rendered.

```text
import React, { useState } from 'react';

function TestApp() {
    const [count, setCount] = useState(0)
    
    function updateCount() {
        setCount(5);
    }
    
    return {
        <button onClick={updateCount}>Update Count</button>
    }
}
```

#### **Using previous state**

_**Note**: if we are using previous value of the state to make changes on state, we should pass in function parameter to update the state._

```text
// Don't do
function updateCount() {
    setCount(count + 5);
}

// Do
function updateCount() {
    setCount(previousCount => previousCount + 5);
}

This is required because if setCount is called in different place or called more than once.
Then the count value passed in would be same.

function updateCount() {
    setCount(count + 5); // count = 0, Results: 5
    setCount(count + 5); // count = 0, Results: 5
}
```

#### Initial State

useState can also take in a normal default value or a function that returns the value. The difference being that a normal default value will be updated/ran every time the component re-renders. This is why it is always better to pass in default value as a function if the generation of the value need higher computational usage. 

```text
function initialFn() {
    console.log("Rendered");
    return 5;
}

//Called in every re-render.
const [count, setCount] = useState(initialFn()); 

//Called only in first reendering.
const [count, setCount] = useState(() => initialFn()); 
```

#### Object state

One thing to note about state from class component state is that when we update the state of an object there is no auto merging happening which means the new state will override all the value of old state.

```text
const objectCount, setObjectCount] = useState({ count: 5, name: 'madan'})

//This new state will override the old state which means the name property will dissapear too as there is no auto merging.
setObjectCount(prevState => { return { count: prevState + 5 } } )

//We will use speard operator to get old state value & update count with new value then update the state with all the property.
setObjectCount(prevState => { return { ...prevState, count: prevState + 5 } } )
```

## useEffect

`useEffect(() => { FUNCTIONS_TO_RUN_ON_RENDER }, OPTIONAL_STATE_ARRAY_TO_WATCH)`

useEffect are useful when trying to create some side effect in the site or make some API request. 

They run on every render \(after render / DOM has been updated\). 

However, we can pass in the state name as second argument which will then cause it to execute only when the state value changes from the list of second argument. 

we can also pass in empty array which means it will only run on first mount/render. 

```text
//Runs on each render
useEffect(() => {
    console.log("ran effect")
})

//Runs only when the state changes for the variable in the list
useEffect(() => {
    console.log("ran effect")
}, [count, name])

//Runs on first render/mount only
useEffect(() => {
    console.log("ran effect")
}, [])
```

#### Clean ups with useEffect

Once our component is unmounted/removed/stateChanges, we can run a function to clean up anything we had setup in useEffect. This can be done with useEffect return function. This cleanup function will be ran every-time we run useEffect to clean up previous changes. 

```text
useEffect(() => {
    // add listener to an element
    button.addEventListener('onclick', handleOnClick);
    
    //Clean up by removing event listener
    return () => {
        button.removeEventListener('onclick', handleOnClick)
    }
}, []) // run on mount only
```

## Custom Hook

Custom hook are functions with name that starts with `use` & can call other hooks. 

Custom hooks are useful when we have more than one hook/functions that share the logics.

Custom hooks functions has not specific signature, meaning it can take in any arguments & return anything.

```text
// Custom hook
function useUserStatus(userId) {
    const [userStatus, setUserStatus] = useState(null);
    // ... some logic to get/update status
    return userStatus;
}

// Using custom hook like normal hook inside React Component
function UserProfile(userId) {
    const userStatus = useUserStatus(userId);
    return (<div>Status: {userStatus}</div>);
}
```

## useContext

`useContext` allow us to access the value from component without passing  props from direct parent component and avoid cuber-some task of passing props to share with child's.

we can create custom context using `React.createContext`

`useContext` then takes in this context object and returns the current value of that context. 

we can use this hook by wrapping any parent up the component we use this hook with `ExampleContext.Provider` .

This `value` is determined from the closest provider above the calling component.

component using useContext will always re-render when context value is changed.

```text
const GlobalContext = React.createContext();

//Compoent with Context Provider wrapped up
function Test () {
    return (
        <GlobalContext.Provider value="Madan">
            <CustomComponents />
        </GlobalContext.Provider>
    );
}

//Somewhere deep in the CustomComponents component tree
function DeepCompoent() {
    const contextValue = useContext(GlobalContext);
    return (<h1>{{ contextValue.value }}</h1>);
}
```

## useReducer

Similar to `useState` / `Redux` we can use reducer hook to  reduce our state.

```text
//Reducer that has logic to handle different action, takes in previousState & action.
const reducer = (state, action) => newState;

//Takes in reducer, initialState & init(initialState)
const [state, dispatch] = useReducer(reducer, initialState, init);

//We can then call the dispatch function to update the state
dispatch({ type: 'updateAction'})
```

#### Initialise useReducer

1. We can initialise reducer using just reducer & initialState.
2. We can use pass 3rd parameter \(init\) function that takes in initialState as argument then lazy load the initialState from \(init\) function. `useReducer((prevS, action) => newS , initialS, (initialS) => initialS)`

Reducer dispatch is also useful when trying to avoid deep nested callbacks. With context, we can pass down the `dispatch` function from `useReducer`

```text
const GlobalContext = React.createContext();

function App() {
    const [state, dispatch] = useReducer(reducer, initialState);
    return (
        <GlobalContext.Provider value={dispatch}>
            <SomeComponents />
        </GlobalContext.Provider>
    );
}

function SomeComponents() {
    const dispatch = useContext(GlobalContext);
    return (
        <button onClick={dispatch({type: 'updateState', extra: 'data'})}>Ok</button>
    );
}

```

