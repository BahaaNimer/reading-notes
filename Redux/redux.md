# What is Redux?

Redux is a predictable state container for JavaScript apps.

It helps you write applications that behave consistently…

Redux takes away some of the hassles faced with state management in large applications. It provides you with a great developer experience, and makes sure that the testability of your app isn’t sacrificed for any of those.

As you develop React applications, you may find that keeping all your state in a top-level component is no longer sufficient for you.

You may also have a lot of data changing in your application over time.

Redux helps solve these kinds of problems. Mind you, it isn’t the only solution out there.

## Why use Redux?

In larger apps with a lot of moving pieces, state management becomes a huge concern. Redux ticks that off quite well without performance concerns or trading off testability.

One other reason a lot of developers love Redux is the developer experience that comes with it. A lot of other tools have begun to do similar things, but big credits to Redux.

Some of the nice things you get with using Redux include logging, hot reloading, time travel, universal apps, record and replay — all without doing so much on your end as the developer. These things will likely sound fancy until you use them and see for yourself.

## Redux principle

### Redux principle #1

![redux](./assets/Understanding-Redux-The-World%E2%80%99s-Easiest-Guide-to-Beginning-Redux.png)

### Redux principle #2

State is read-only:

The only way to change the state is to emit an action, an object describing what happened.

![redux2](<./assets/Understanding-Redux-The-World%E2%80%99s-Easiest-Guide-to-Beginning-Redux%20(1).png>)

### Redux principle #3

To specify how the state tree is transformed by actions, you write pure reducers.

![redux3](<./assets/Understanding-Redux-The-World%E2%80%99s-Easiest-Guide-to-Beginning-Redux%20(2).png>)

The most important Redux actors are: the `store`, the `reducer` and an `action`.

## References

[eggHead](https://egghead.io/lessons/react-redux-describing-state-changes-with-actions)

[freeCodeCamp](https://www.freecodecamp.org/news/understanding-redux-the-worlds-easiest-guide-to-beginning-redux-c695f45546f6)
