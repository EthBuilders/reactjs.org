---
title: React v0.13.0 Beta 1
author: [sebmarkbage]
---

React 0.13 has a lot of nice features but there is one particular feature that I'm really excited about. I couldn't wait for React.js Conf to start tomorrow morning.

Maybe you're like me and staying up late excited about the conference, or maybe you weren't one of the lucky ones to get a ticket. Either way I figured I'd give you all something to play with until then.

We just published a beta version of React v0.13.0 to [npm](https://www.npmjs.com/package/react)! You can install it with `npm install react@0.13.0-beta.1`. Since this is a pre-release, we don't have proper release notes ready.

So what is that one feature I'm so excited about that I just couldn't wait to share?

## Plain JavaScript Classes!! {#plain-javascript-classes}

JavaScript originally didn't have a built-in class system. Every popular framework built their own, and so did we. This means that you have a learn slightly different semantics for each framework.

We figured that we're not in the business of designing a class system. We just want to use whatever is the idiomatic JavaScript way of creating classes.

In React 0.13.0 you no longer need to use `React.createClass` to create React components. If you have a transpiler you can use ES6 classes today. You can use the transpiler we ship with `react-tools` by making use of the harmony option: `jsx --harmony`.

### ES6 Classes {#es6-classes}

```javascript
class HelloMessage extends React.Component {
  render() {
    return <div>Hello {this.props.name}</div>;
  }
}

React.render(<HelloMessage name="Sebastian" />, mountNode);
```

The API is mostly what you would expect, with the exception of `getInitialState`. We figured that the idiomatic way to specify class state is to just use a simple instance property. Likewise `getDefaultProps` and `propTypes` are really just properties on the constructor.

```javascript
export class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = {count: props.initialCount};
  }
  tick() {
    this.setState({count: this.state.count + 1});
  }
  render() {
    return <div onClick={this.tick.bind(this)}>Clicks: {this.state.count}</div>;
  }
}
Counter.propTypes = {initialCount: React.PropTypes.number};
Counter.defaultProps = {initialCount: 0};
```

### ES7+ Property Initializers {#es7-property-initializers}

Wait, assigning to properties seems like a very imperative way of defining classes! You're right, however, we designed it this way because it's idiomatic. We fully expect a more declarative syntax for property initialization to arrive in future version of JavaScript. It might look something like this:

```javascript
// Future Version
export class Counter extends React.Component {
  static propTypes = {initialCount: React.PropTypes.number};
  static defaultProps = {initialCount: 0};
  state = {count: this.props.initialCount};
  tick() {
    this.setState({count: this.state.count + 1});
  }
  render() {
    return <div onClick={this.tick.bind(this)}>Clicks: {this.state.count}</div>;
  }
}
```

This was inspired by TypeScript's property initializers.

### Autobinding {#autobinding}

`React.createClass` has a built-in magic feature that bound all methods to `this` automatically for you. This can be a little confusing for JavaScript developers that are not used to this feature in other classes, or it can be confusing when they move from React to other classes.

Therefore we decided not to have this built-in into React's class model. You can still explicitly prebind methods in your constructor if you want.

```javascript
class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.tick = this.tick.bind(this);
  }
  tick() {
    ...
  }
  ...
}
```

However, when we have the future property initializers, there is a neat trick that you can use to accomplish this syntactically:

```javascript
class Counter extends React.Component {
  tick = () => {
    ...
  }
  ...
}
```

### Mixins {#mixins}

Unfortunately, we will not launch any mixin support for ES6 classes in React. That would defeat the purpose of only using idiomatic JavaScript concepts.

There is no standard and universal way to define mixins in JavaScript. In fact, several features to support mixins were dropped from ES6 today. There are a lot of libraries with different semantics. We think that there should be one way of defining mixins that you can use for any JavaScript class. React just making another doesn't help that effort.

Therefore, we will keep working with the larger JS community to create a standard for mixins. We will also start designing a new compositional API that will help make common tasks easier to do without mixins. E.g. first-class subscriptions to any kind of Flux store.

Luckily, if you want to keep using mixins, you can just keep using `React.createClass`.

> **Note:**
>
> The classic `React.createClass` style of creating classes will continue to work just fine.

## Other Languages! {#other-languages}

Since these classes are just plain old JavaScript classes, you can use other languages that compile to JavaScript classes, such as TypeScript.

You can also use CoffeeScript classes:

```coffeescript
div = React.createFactory 'div'

class Counter extends React.Component
  @propTypes = initialCount: React.PropTypes.number
  @defaultProps = initialCount: 0

  constructor: (props) ->
    super props
    @state = count: props.initialCount

  tick: =>
    @setState count: @state.count + 1

  render: ->
    div onClick: @tick,
      'Clicks: '
      @state.count
```

You can even use the old ES3 module pattern if you want:

```javascript
function MyComponent(initialProps) {
  return {
    state: {value: initialProps.initialValue},
    render: function () {
      return <span className={this.state.value} />;
    },
  };
}
```
