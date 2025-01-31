---
title: React v0.11.1
author: [zpao]
---

Today we're releasing React v0.11.1 to address a few small issues. Thanks to everybody who has reported them as they've begun upgrading.

The first of these is the most major and resulted in a regression with the use of `setState` inside `componentWillMount` when using React on the server. These `setState` calls are batched into the initial render. A change we made to our batching code resulted in this path hitting DOM specific code when run server-side, in turn throwing an error as `document` is not defined.

There are several fixes we're including in v0.11.1 that are focused around the newly supported `event.getModifierState()` function. We made some adjustments to improve this cross-browser standardization.

The final fix we're including is to better support a workaround for some IE8 behavior. The edge-case bug we're fixing was also present in v0.9 and v0.10, so while it wasn't a short-term regression, we wanted to make sure we support IE8 to the best of our abilities.

We'd also like to call out a couple additional breaking changes that we failed to originally mention in the release notes for v0.11. We updated that blog post and the changelog, so we encourage you to go read about the changes around [Descriptors](/blog/2014/07/17/react-v0.11.html#descriptors) and [Prop Type Validation](/blog/2014/07/17/react-v0.11.html#prop-type-validation).

The release is available for download from the CDN:

- **React**  
  Dev build with warnings: <https://fb.me/react-0.11.1.js>  
  Minified build for production: <https://fb.me/react-0.11.1.min.js>
- **React with Add-Ons**  
  Dev build with warnings: <https://fb.me/react-with-addons-0.11.1.js>  
  Minified build for production: <https://fb.me/react-with-addons-0.11.1.min.js>
- **In-Browser JSX transformer**  
  <https://fb.me/JSXTransformer-0.11.1.js>

We've also published version `0.11.1` of the `react` and `react-tools` packages on npm and the `react` package on bower.

Please try these builds out and [file an issue on GitHub](https://github.com/facebook/react/issues/new) if you see anything awry.

## Changelog {#changelog}

### React Core {#react-core}

#### Bug Fixes {#bug-fixes}

- `setState` can be called inside `componentWillMount` in non-DOM environments
- `SyntheticMouseEvent.getEventModifierState` correctly renamed to `getModifierState`
- `getModifierState` correctly returns a `boolean`
- `getModifierState` is now correctly case sensitive
- Empty Text node used in IE8 `innerHTML` workaround is now removed, fixing rerendering in certain cases

### JSXTransformer {#jsxtransformer}

- Fix duplicate variable declaration (caused issues in some browsers)
