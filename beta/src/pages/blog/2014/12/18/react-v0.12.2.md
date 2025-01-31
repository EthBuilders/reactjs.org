---
title: React v0.12.2
author: [zpao]
---

We just shipped React v0.12.2, bringing the 0.12 branch up to date with a few small fixes that landed in master over the past 2 months.

You may have noticed that we did not do an announcement for v0.12.1. That release was snuck out in anticipation of [Flow](http://flowtype.org/), with only transform-related changes. Namely we added a flag to the `jsx` executable which allowed you to safely transform Flow-based code to vanilla JS. If you didn't update for that release, you can safely skip it and move directly to v0.12.2.

The release is available for download from the CDN:

- **React**  
  Dev build with warnings: <https://fb.me/react-0.12.2.js>  
  Minified build for production: <https://fb.me/react-0.12.2.min.js>
- **React with Add-Ons**  
  Dev build with warnings: <https://fb.me/react-with-addons-0.12.2.js>  
  Minified build for production: <https://fb.me/react-with-addons-0.12.2.min.js>
- **In-Browser JSX transformer**  
  <https://fb.me/JSXTransformer-0.12.2.js>

We've also published version `0.12.2` of the `react` and `react-tools` packages on npm and the `react` package on bower. `0.12.1` is also available in the same locations if need those.

Please try these builds out and [file an issue on GitHub](https://github.com/facebook/react/issues/new) if you see anything awry.

## Changelog {#changelog}

### React Core {#react-core}

- Added support for more HTML attributes: `formAction`, `formEncType`, `formMethod`, `formTarget`, `marginHeight`, `marginWidth`
- Added `strokeOpacity` to the list of unitless CSS properties
- Removed trailing commas (allows npm module to be bundled and used in IE8)
- Fixed bug resulting in error when passing `undefined` to `React.createElement` - now there is a useful warning

### React Tools {#react-tools}

- JSX-related transforms now always use double quotes for props and `displayName`
