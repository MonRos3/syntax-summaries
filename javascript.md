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
