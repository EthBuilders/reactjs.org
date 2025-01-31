---
title: 'React v0.13 RC'
author: [zpao]
date: 2015-02-24 14:00
---

Over the weekend we pushed out our first (and hopefully only) release candidate for React v0.13!

We've talked a little bit about the changes that are coming. The splashiest of these changes is support for ES6 Classes. You can read more about this in [our beta announcement](/blog/2015/01/27/react-v0.13.0-beta-1.html). We're really excited about this! Sebastian also posted earlier this morning about [some of the other changes coming focused around ReactElement](/blog/2015/02/24/streamlining-react-elements.html). The changes we've been working on there will hopefully enable lots of improvements to performance and developer experience.

The release candidate is available for download:

- **React**  
  Dev build with warnings: <https://fb.me/react-0.13.0-rc1.js>  
  Minified build for production: <https://fb.me/react-0.13.0-rc1.min.js>
- **React with Add-Ons**  
  Dev build with warnings: <https://fb.me/react-with-addons-0.13.0-rc1.js>  
  Minified build for production: <https://fb.me/react-with-addons-0.13.0-rc1.min.js>
- **In-Browser JSX transformer**  
  <https://fb.me/JSXTransformer-0.13.0-rc1.js>

We've also published version `0.13.0-rc1` of the `react` and `react-tools` packages on npm and the `react` package on bower.

---

## Changelog {#changelog}

### React Core {#react-core}

#### Breaking Changes {#breaking-changes}

- Mutating `props` after an element is created is deprecated and will cause warnings in development mode; future versions of React will incorporate performance optimizations assuming that props aren't mutated
- Static methods (defined in `statics`) are no longer autobound to the component class
- `ref` resolution order has changed slightly such that a ref to a component is available immediately after its `componentDidMount` method is called; this change should be observable only if your component calls a parent component's callback within your `componentDidMount`, which is an anti-pattern and should be avoided regardless
- Calls to `setState` in life-cycle methods are now always batched and therefore asynchronous. Previously the first call on the first mount was synchronous.
- `setState` and `forceUpdate` on an unmounted component now warns instead of throwing. That avoids a possible race condition with Promises.
- Access to most internal properties has been completely removed, including `this._pendingState` and `this._rootNodeID`.

#### New Features {#new-features}

- Support for using ES6 classes to build React components; see the [v0.13.0 beta 1 notes](/blog/2015/01/27/react-v0.13.0-beta-1.html) for details
- Added new top-level API `React.findDOMNode(component)`, which should be used in place of `component.getDOMNode()`. The base class for ES6-based components will not have `getDOMNode`. This change will enable some more patterns moving forward.
- New `ref` style, allowing a callback to be used in place of a name: `<Photo ref={(c) => this._photo = c} />` allows you to reference the component with `this._photo` (as opposed to `ref="photo"` which gives `this.refs.photo`)
- `this.setState()` can now take a function as the first argument for transactional state updates, such as `this.setState((state, props) => ({count: state.count + 1}));` -- this means that you no longer need to use `this._pendingState`, which is now gone.
- Support for iterators and immutable-js sequences as children

#### Deprecations {#deprecations}

- `ComponentClass.type` is deprecated. Just use `ComponentClass` (usually as `element.type === ComponentClass`)
- Some methods that are available on `createClass`-based components are removed or deprecated from ES6 classes (for example, `getDOMNode`, `setProps`, `replaceState`).

### React with Add-Ons {#react-with-add-ons}

#### Deprecations {#deprecations-1}

- `React.addons.classSet` is now deprecated. This functionality can be replaced with several freely available modules. [classnames](https://www.npmjs.com/package/classnames) is one such module.

### React Tools {#react-tools}

#### Breaking Changes {#breaking-changes-1}

- When transforming ES6 syntax, `class` methods are no longer enumerable by default, which requires `Object.defineProperty`; if you support browsers such as IE8, you can pass `--target es3` to mirror the old behavior

#### New Features {#new-features-1}

- `--target` option is available on the jsx command, allowing users to specify and ECMAScript version to target.
  - `es5` is the default.
  - `es3` restored the previous default behavior. An additional transform is added here to ensure the use of reserved words as properties is safe (eg `this.static` will become `this['static']` for IE8 compatibility).
- The transform for the call spread operator has also been enabled.

### JSX {#jsx}

#### Breaking Changes {#breaking-changes-2}

- A change was made to how some JSX was parsed, specifically around the use of `>` or `}` when inside an element. Previously it would be treated as a string but now it will be treated as a parse error. We will be releasing a standalone executable to find and fix potential issues in your JSX code.
