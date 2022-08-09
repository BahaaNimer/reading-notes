# useState Hook

## what is a Hook?

Hooks are functions that let you “hook into” React state and lifecycle features from function components.

Hooks don’t work inside classes — they let you use React without classes.

React provides a few built-in Hooks like useState.

You can also create your own Hooks to reuse stateful behavior between different components.

## Rules of Hooks

- Only call Hooks `at the top level`. Don’t call Hooks inside loops, conditions, or nested functions.

- Only call Hooks `from React function components`. Don’t call Hooks from regular JavaScript functions. (There is just one other valid place to call Hooks — your own custom Hooks.

## Building Your Own Hooks

Sometimes, we want to reuse some stateful logic between components. Traditionally, there were two popular solutions to this problem: `higher-order components` and `render props`. Custom Hooks let you do this, but without adding more components to your tree.

You can write custom Hooks that cover a wide range of use cases like form handling, animation, declarative subscriptions, timers, etc.

## Example of using state hook

```js
import React, { useState } from 'react';

function Example() {
  // Declare a new state variable, which we'll call "count"
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
}
```

## Equivalent Class Example

```js
class Example extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0,
    };
  }

  render() {
    return (
      <div>
        <p>You clicked {this.state.count} times</p>
        <button onClick={() => this.setState({ count: this.state.count + 1 })}>
          Click me
        </button>
      </div>
    );
  }
}
```

## Hooks and Function Components

Function components in React look like this:

```js
const Example = (props) => {
  // You can use Hooks here!
  return <div />;
};
```

Or this

```js
function Example(props) {
  // You can use Hooks here!
  return <div />;
}
```

> Hooks don’t work inside classes.

## When would I use a Hook?

If you write a function component and realize you need to add some state to it, previously you had to convert it to a class. Now you can use a Hook inside the existing function component

## What does calling useState do?

It declares a “state variable”. Our variable is called `count` but we could call it anything else, like banana. This is a way to “preserve” some values between the function calls — `useState` is a new way to use the exact same capabilities that `this.state` provides in a class. Normally, variables “disappear” when the function exits but state variables are preserved by React.

## What do we pass to useState as an argument?

The only argument to the `useState()` Hook is the initial state. Unlike with classes, the state doesn’t have to be an object. We can keep a number or a string if that’s all we need. In our example, we just want a number for how many times the user clicked, so pass 0 as initial state for our variable. (If we wanted to store two different values in state, we would call `useState()` twice.)

## What does useState return?

It returns a pair of values: the current state and a function that updates it. This is why we write `const [count, setCount] = useState()`. This is similar to `this.state.count` and `this.setState` in a class, except you get them in a pair.

```js
import React, { useState } from 'react';

function Example() {
  // Declare a new state variable, which we'll call "count"
  const [count, setCount] = useState(0);
}
```

We declare a state variable called count, and set it to 0. React will remember its current value between re-renders, and provide the most recent one to our function. If we want to update the current count, we can call setCount.

## Reading State

```js
<p>You clicked {count} times</p>
```

## Updating State

```js
<button onClick={() => setCount(count + 1)}>Click me</button>
```

## Final code to recap

```js
 1:  import React, { useState } from 'react';
 2:
 3:  function Example() {
 4:    const [count, setCount] = useState(0);
 5:
 6:    return (
 7:      <div>
 8:        <p>You clicked {count} times</p>
 9:        <button onClick={() => setCount(count + 1)}>
10:         Click me
11:        </button>
12:      </div>
13:    );
14:  }
```

- Line 1: We import the useState Hook from React. It lets us keep local state in a function component.

- Line 4: Inside the Example component, we declare a new state variable by calling the useState Hook. It returns a pair of values, to which we give names. We’re calling our variable count because it holds the number of button clicks. We initialize it to zero by passing 0 as the only useState argument. The second returned item is itself a function. It lets us update the count so we’ll name it setCount.

- Line 9: When the user clicks, we call setCount with a new value. React will then re-render the Example component, passing the new count value to it.

## Using Multiple State Variables

```js
function ExampleWithManyStates() {
  // Declare multiple state variables!
  const [age, setAge] = useState(42);
  const [fruit, setFruit] = useState('banana');
  const [todos, setTodos] = useState([{ text: 'Learn Hooks' }]);
}
```
