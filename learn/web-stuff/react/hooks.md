# Hooks

### Overview

React hooks can be only used with functional components. 

The execution order of the hooks should always be same. Meaning it cannot be inside conditional statements.

### useState

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

