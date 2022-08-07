# React

React is a JavaScript library

Simple Example

```js
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<h1>Hello, world!</h1>);
```

## Introducing JSX

```js
const element = <h1>Hello, world!</h1>;
```

It is called `JSX`, and it is a syntax extension to JavaScript.

`JSX` may remind you of a template language, but it comes with the full power of JavaScript.

> JSX produces React “elements”.

## Why JSX?

Instead of artificially separating technologies by putting markup and logic in separate files, React separates concerns with loosely coupled units called `“components”` that contain both.

React doesn’t require using `JSX`, but most people find it helpful as a visual aid when working with UI inside the JavaScript code.

It also allows React to show more useful error and warning messages.

### Embedding Expressions in JSX

```js
const name = 'Josh Perez';
const element = <h1>Hello, {name}</h1>;
```

> You can put any valid JavaScript expression inside the curly braces in JSX.

```js
function formatName(user) {
  return user.firstName + ' ' + user.lastName;
}

const user = {
  firstName: 'Harper',
  lastName: 'Perez',
};

const element = <h1>Hello, {formatName(user)}!</h1>;
```

Also recommend wrapping it in parentheses to avoid the pitfalls of `automatic semicolon insertion`.

### JSX is an Expression Too

After compilation, `JSX` expressions become regular JavaScript function calls and evaluate to JavaScript objects.

This means that you can use `JSX` inside of `if` statements and `for` loops, assign it to variables, accept it as arguments, and return it from functions:

```js
function getGreeting(user) {
  if (user) {
    return <h1>Hello, {formatName(user)}!</h1>;
  }
  return <h1>Hello, Stranger.</h1>;
}
```

### Specifying Attributes with JSX

You may use quotes to specify string literals as attributes:

```js
const element = <a href='https://www.reactjs.org'> link </a>;
```

You may also use curly braces to embed a JavaScript expression in an attribute:

```js
const element = <img src={user.avatarUrl}></img>;
```

Don’t put quotes around curly braces when embedding a JavaScript expression in an attribute. You should either use quotes (for string values) or curly braces (for expressions), but not both in the same attribute.

### Specifying Children with JSX

If a tag is empty, you may close it immediately with `/>`, like XML:

```js
const element = <img src={user.avatarUrl} />;
```

`JSX` tags may contain children:

```js
const element = (
  <div>
    <h1>Hello!</h1>
    <h2>Good to see you here.</h2>
  </div>
);
```

### JSX Prevents Injection Attacks

It is safe to embed user input in `JSX`:

```js
const title = response.potentiallyMaliciousInput;
// This is safe:
const element = <h1>{title}</h1>;
```

By default, React DOM escapes any values embedded in `JSX` before rendering them. Thus it ensures that you can never inject anything that’s not explicitly written in your application. Everything is converted to a string before being rendered. This helps prevent `XSS` (cross-site-scripting) attacks.

### JSX Represents Objects

Babel compiles `JSX` down to `React.createElement()` calls.

These two examples are identical:

```js
const element = <h1 className='greeting'>Hello, world!</h1>;
```

```js
const element = React.createElement(
  'h1',
  { className: 'greeting' },
  'Hello, world!'
);
```

`React.createElement()` performs a few checks to help you write bug-free code but essentially it creates an object like this:

```js
// Note: this structure is simplified
const element = {
  type: 'h1',
  props: {
    className: 'greeting',
    children: 'Hello, world!',
  },
};
```

> These objects are called `“React elements”`.

You can think of them as descriptions of what you want to see on the screen.

React reads these objects and uses them to construct the DOM and keep it up to date.

## Rendering Elements

Elements are the smallest building blocks of React apps.

An element describes what you want to see on the screen:

```js
const element = <h1>Hello, world</h1>;
```

Unlike browser DOM elements, React elements are plain objects, and are cheap to create. React DOM takes care of updating the DOM to match the React elements.

### Rendering an Element into the DOM

```js
<div id='root'></div>
```

We call this a `“root”` DOM node because everything inside it will be managed by React DOM.

To render a React element, first pass the DOM element to `ReactDOM.createRoot()`, then pass the React element to `root.render()`:

```js
const root = ReactDOM.createRoot(document.getElementById('root'));
const element = <h1>Hello, world</h1>;
root.render(element);
```

> It displays “Hello, world” on the page.

### Updating the Rendered Element

> React elements are immutable.

Once you create an element, you can’t change its children or attributes. An element is like a single frame in a movie: it represents the UI at a certain point in time.

Example:

```js
const root = ReactDOM.createRoot(document.getElementById('root'));

function tick() {
  const element = (
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {new Date().toLocaleTimeString()}.</h2>
    </div>
  );
  root.render(element);
}

setInterval(tick, 1000);
```

It calls `root.render()` every second from a `setInterval()` callback.

### React Only Updates What’s Necessary

React DOM compares the element and its children to the previous one, and only applies the DOM updates necessary to bring the DOM to the desired state.

> Only the text node whose contents have changed gets updated by React DOM.
