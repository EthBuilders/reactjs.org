---
title: React v0.10 RC
author: [zpao]
---

[v0.9 has only been out for a month](/blog/2014/02/20/react-v0.9.html), but we’re getting ready to push out v0.10 already. Unlike v0.9 which took a long time, we don't have a long list of changes to talk about.

The release candidate is available for download from the CDN:

- **React**  
  Dev build with warnings: <https://fb.me/react-0.10.0-rc1.js>  
  Minified build for production: <https://fb.me/react-0.10.0-rc1.min.js>
- **React with Add-Ons**  
  Dev build with warnings: <https://fb.me/react-with-addons-0.10.0-rc1.js>  
  Minified build for production: <https://fb.me/react-with-addons-0.10.0-rc1.min.js>
- **In-Browser JSX transformer**  
  <https://fb.me/JSXTransformer-0.10.0-rc1.js>

We've also published version `0.10.0-rc1` of the `react` and `react-tools` packages on npm and the `react` package on bower.

Please try these builds out and [file an issue on GitHub](https://github.com/facebook/react/issues/new) if you see anything awry.

## Clone On Mount {#clone-on-mount}

The main purpose of this release is to provide a smooth upgrade path as we evolve some of the implementation of core. In v0.9 we started warning in cases where you called methods on unmounted components. This is part of an effort to enforce the idea that the return value of a component (`React.DOM.div()`, `MyComponent()`) is in fact not a reference to the component instance React uses in the virtual DOM. The return value is instead a light-weight object that React knows how to use. Since the return value currently is a reference to the same object React uses internally, we need to make this transition in stages as many people have come to depend on this implementation detail.

In 0.10, we’re adding more warnings to catch a similar set of patterns. When a component is mounted we clone it and use that object for our internal representation. This allows us to capture calls you think you’re making to a mounted component. We’ll forward them on to the right object, but also warn you that this is breaking. See “Access to the Mounted Instance” on [this page](https://fb.me/react-warning-descriptors). Most of the time you can solve your pattern by using refs.

Storing a reference to your top level component is a pattern touched upon on that page, but another examples that demonstrates what we see a lot of:

```js
// This is a common pattern. However instance here really refers to a
// "descriptor", not necessarily the mounted instance.
var instance = <MyComponent/>;
React.renderComponent(instance);
// ...
instance.setProps(...);

// The change here is very simple. The return value of renderComponent will be
// the mounted instance.
var instance = React.renderComponent(<MyComponent/>)
// ...
instance.setProps(...);
```

These warnings and method forwarding are only enabled in the development build. The production builds continue to work as they did in v0.9. We strongly encourage you to use the development builds to catch these warnings and fix the call sites.

The plan for v0.11 is that we will go fully to "descriptors". Method calls on the return value of `MyComponent()` will fail hard.

## Changelog {#changelog}

### React Core {#react-core}

#### New Features {#new-features}

- Added warnings to help migrate towards descriptors
- Made it possible to server render without React-related markup (`data-reactid`, `data-react-checksum`). This DOM will not be mountable by React. [Read the docs for `React.renderComponentToStaticMarkup`](/docs/top-level-api.html#react.rendercomponenttostaticmarkup)
- Added support for more attributes:
  - `srcSet` for `<img>` to specify images at different pixel ratios
  - `textAnchor` for SVG

#### Bug Fixes {#bug-fixes}

- Ensure all void elements don’t insert a closing tag into the markup.
- Ensure `className={false}` behaves consistently
- Ensure `this.refs` is defined, even if no refs are specified.

### Addons {#addons}

- `update` function to deal with immutable data. [Read the docs](/docs/update.html)

### react-tools {#react-tools}

- Added an option argument to `transform` function. The only option supported is `harmony`, which behaves the same as `jsx --harmony` on the command line. This uses the ES6 transforms from [jstransform](https://github.com/facebook/jstransform).
