---
id: displaying-data
title: Displaying Data
permalink: docs/displaying-data.html
prev: why-react.html
next: jsx-in-depth.html
---

The most basic thing you can do with a UI is display some data. React makes it easy to display data and automatically keeps the interface up-to-date when the data changes.

## Getting Started

Let's look at a really simple example. Create a `hello-react.html` file with the following code:

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>Hello React</title>
    <script src="https://unpkg.com/react@{{site.react_version}}/dist/react.js"></script>
    <script src="https://unpkg.com/react-dom@{{site.react_version}}/dist/react-dom.js"></script>
    <script src="https://unpkg.com/babel-core@5.8.38/browser.min.js"></script>
  </head>
  <body>
    <div id="example"></div>
    <script type="text/babel">

      // ** Your code goes here! **

    </script>
  </body>
</html>
```

For the rest of the documentation, we'll just focus on the JavaScript code and assume it's inserted into a template like the one above. Replace the placeholder comment above with the following JSX:

```javascript
class HelloWorld extends React.Component {
  render() {
    return (
      <p>
        Hello, <input type="text" placeholder="Your name here" />!
        It is {this.props.date.toTimeString()}
      </p>
    );
  }
}

function tick() {
  ReactDOM.render(
    <HelloWorld date={new Date()} />,
    document.getElementById('example')
  );
}

setInterval(tick, 500);
```

## Reactive Updates

Open `hello-react.html` in a web browser and type your name into the text field. Notice that React is only changing the time string in the UI — any input you put in the text field remains, even though you haven't written any code to manage this behavior. React figures it out for you and does the right thing.

The way we are able to figure this out is that React does not manipulate the DOM unless it needs to. **It uses a fast, internal mock DOM to perform diffs and computes the most efficient DOM mutation for you.**

The inputs to this component are called `props` — short for "properties". They're passed as attributes in JSX syntax. You should think of these as immutable within the component, that is, **never write to `this.props`**.

## Components are Just Like Functions

React components are very simple. You can think of them as simple functions that take in `props` and `state` (discussed later) and render HTML. With this in mind, components are easy to reason about.

> Note:
>
> **One limitation**: React components can only render a single root node. If you want to return multiple nodes they *must* be wrapped in a single root.

## JSX Syntax

We strongly believe that components are the right way to separate concerns rather than "templates" and "display logic." We think that markup and the code that generates it are intimately tied together. Additionally, display logic is often very complex and using template languages to express it becomes cumbersome.

We've found that the best solution for this problem is to generate HTML and component trees directly from the JavaScript code such that you can use all of the expressive power of a real programming language to build UIs.

In order to make this easier, we've added a very simple, **optional** HTML-like syntax to create these React tree nodes.

**JSX lets you create JavaScript objects using HTML syntax.** To generate a link in React using pure JavaScript you'd write:

`React.createElement('a', {href: 'https://facebook.github.io/react/'}, 'Hello!')`

With JSX this becomes:

`<a href="https://facebook.github.io/react/">Hello!</a>`

We've found this has made building React apps easier and designers tend to prefer the syntax, but everyone has their own workflow, so **JSX is not required to use React.**

JSX is very small. To learn more about it, see [JSX in depth](/react/docs/jsx-in-depth.html). Or see the transform in action in [the Babel REPL](https://babeljs.io/repl/).

JSX is similar to HTML, but not exactly the same. See [JSX gotchas](/react/docs/jsx-gotchas.html) for some key differences.

[Babel exposes a number of ways to get started using JSX](http://babeljs.io/docs/setup/), ranging from command line tools to Ruby on Rails integrations. Choose the tool that works best for you.

## React without JSX

JSX is completely optional; you don't have to use JSX with React. You can create React elements in plain JavaScript using `React.createElement`, which takes a tag name or component, a properties object, and variable number of optional child arguments.

```javascript
var child1 = React.createElement('li', null, 'First Text Content');
var child2 = React.createElement('li', null, 'Second Text Content');
var root = React.createElement('ul', { className: 'my-list' }, child1, child2);
ReactDOM.render(root, document.getElementById('example'));
```

For convenience, you can create short-hand factory functions to create elements from custom components.

```javascript
var Factory = React.createFactory(ComponentClass);
...
var root = Factory({ custom: 'prop' });
ReactDOM.render(root, document.getElementById('example'));
```

React already has built-in factories for common HTML tags:

```javascript
var root = React.DOM.ul({ className: 'my-list' },
             React.DOM.li(null, 'Text Content')
           );
```
