# Event-Driven Programming in Node.js

Event-Driven Programming is a logical pattern that we can choose to confine our programming within to avoid issues of complexity and collision.

- An Event Handler is a callback function that will be called when an event is triggered.

- A Main Loop listens for event triggers and calls the associated event handler for that event.

## EventEmitter

Node.js natively provides us with a useful module called EventEmitter that allows us to get started incorporating Event-Driven Programming in our project right away.

We access the EventEmitter class through the events module.

```js
const EventEmitter = require('events').EventEmitter;
const myEventEmitter = new EventEmitter();
```

> Now we can get started with Event-Driven Programming in Node.

Example:

```js
const EventEmitter = require('events').EventEmitter;
const chatRoomEvents = new EventEmitter();

function userJoined(username) {
  // Assuming we already have a function to alert all users.
  alertAllUsers('User ' + username + ' has joined the chat.');
}

// Run the userJoined function when a 'userJoined' event is triggered.
chatRoomEvents.on('userJoined', userJoined);
```

The next step would be to make sure that our chat room triggers a userJoined event whenever someone logs in so that our event handler is called.

```js
function login(username) {
  chatRoomEvents.emit('userJoined', username);
}
```

## Removing Listeners

The orignal code will be like this:

```js
const EventEmitter = require('events').EventEmitter;
const chatRoomEvents = new EventEmitter();

function userJoined(username) {
  chatRoomEvents.on('message', function (message) {
    document.write(message);
  });
}

chatRoomEvents.on('userJoined', userJoined);
```

So we can rewrite the code like this:

```js
const EventEmitter = require('events').EventEmitter;
const chatRoomEvents = new EventEmitter();

function displayMessage(message) {
  document.write(message);
}

function userJoined(username) {
  chatRoomEvents.on('message', displayMessage);
}

chatRoomEvents.on('userJoined', userJoined);
```

Now if we want to remove the displayMessage function from the message event’s list of handlers:

```js
chatRoomEvents.removeListener('message', displayMessage);
```

## Object Oriented Programming + Event-Driven Programming

Example:

```js
class Food {
  constructor(name) {
    this.name = name;
  }

  becomeEaten() {
    return 'I have been eaten.';
  }
}

var bacon = new Food('bacon');

class gator {
  eat() {
    bacon.becomeEaten();
  }
}
```

In this example, our gator had to access the methods inside of Food in order to eat. This is a lot of work for our lazy gator so we’re going to make things easier for him.

```js
const EventEmitter = require('events').EventEmitter;
const myGatorEvents = new EventEmitter();

class Food {
  constructor(name) {
    this.name = name;
    // Become eaten when gator emits 'gatorEat'
    myGatorEvents.on('gatorEat', this.becomeEaten);
  }

  becomeEaten() {
    return 'I have been eaten.';
  }
}

var bacon = new Food('bacon');

const gator = {
  eat() {
    myGatorEvents.emit('gatorEat');
  },
};
```

Now all our gator has to do is just say gatorEat and the EventEmitter takes care of the rest.

[Node.js v18.4.0 documentation](https://nodejs.org/api/events.html)

> For EventEmitter, EventTarget and NodeEventTarget.
