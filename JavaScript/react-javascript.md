# REACT JS COMMANDS

## CREATING A NEW APP

```bash
npx create-react-app my-app-name
```

```bash
cd my-app
```

- don't forget to create virtualenv

```bash
npm start
```

## FUNCTIONS

TWO WAYS TO DEFINE A FUNCTION

1 - Declaration

```javascript
test();

function test() {}
```

2 - Expression

```javascript
const test = () => {
  console.log("Hello World");
};

test();
```

## REST OPERATOR

Use when you need an indefinite number of operators

```javascript
function test3(firstArgument, ...otherArguments) {
  console.log(firstArgument);
  console.log(otherArguments);
}

test3("Peter", "Max", "Claudia", "Michael", "Brandon", "Stevie");
```

## SPREAD OPERATOR

```javascript
const fruits = ["mango", "pineapple"];
const moreFruits = ["banana", "blueberry", "watermelon"];

//creates a NEW array [not modifying existing]
const allFruits = [...fruits, ...moreFruits];

console.log(allFruits);

//creates a NEW array [not modifying existing]

const faveFruits = [...fruits, "strawberry", "raspberry"];

console.log(faveFruits);
```

## COMPONENTS

State = manage component data

component re-renders; variables don’t do that!

Two parts: getting and setting

## PROPS

Props = passing data to components
[property]

- used to pass data, event handlers, and functions to components
- you can pass props to nested components [“prop drilling”]

Two parts: create a property inside of component ;

Redux can create a single state for the entire application

## ROUTER

Router = navigation between components

- use routes to configure the routing
- use link to navigate the user

npm i react-router-dom

```js

```

## REDUCER

Reducer = manages state in a centralized way

- clear separation between UI and State Logic
- Components: what should happen; Reducer: how it’s done
- separates logic from user actions
- information gets passed to the reducer in the payload

state.js:

```js
import { useState } from "react";

export default function App() {

const [movies, setMovies] = useState([]);

...
    const loadedMovies = ...;
    setMovies
...

return (
    <div>{movies.length}</div>
);

}
```

reducer.js

```js
import { useReducer } from "react";

const [state, dispatch] = useReducer(ticketReducer, initialState);

export default function ticketReducer(state, action) {
  switch (action.type) {
    case "ADD TICKET":
      return { ...state, tickets: [...state.tickets, action.payload] };

    //other actions

    default:
      return state;
  }
}

// Any component that has access to the dispatch function of the reducer

const handleSubmit = (e) => {
  const ticketData = {
    title,
    description,
    priority,
  };

  dispatch({
    type: "ADD_TICKET",
    payload: ticketData,
  });
};
```

## ContextAPI

ContextAPI = global state management without prop drilling

- share state via provider in across the component tree
- too much prop drilling makes your code messy and harder to maintain
- contextAPI easily share state across multiple components

Use context: if you have info that needs to get shared across MULTIPLE components that are a part of DIFFERENT logics.

    ex:
    - current logged in user
    - cart items
    - theme settings
    - app notifications

```js
import { createContext } from "react";

const UserContext = createContext({username: "Guest"})

// use [previously created] context

import {useContext} from "react";
import {UserContext} from ...

const user = useContext(UserContext);

// wrap UserContext.Provider around every component that needs it

const user = {username: "Admin"}
<UserContext.Provider value={user}>
    <ComponentA></ComponentA>
    <ComponentB></ComponentB> //uses ComponentC
</UserContext.Provider>
```
