---
title: 'React v0.13.2'
author: [zpao]
---

Yesterday the [React Native team shipped v0.4](/blog/2015/04/17/react-native-v0.4.html). Those of us working on the web team just a few feet away couldn't just be shown up like that so we're shipping v0.13.2 today as well! This is a bug fix release to address a few things while we continue to work towards v0.14.

The release is now available for download:

- **React**  
  Dev build with warnings: <https://fb.me/react-0.13.2.js>  
  Minified build for production: <https://fb.me/react-0.13.2.min.js>
- **React with Add-Ons**  
  Dev build with warnings: <https://fb.me/react-with-addons-0.13.2.js>  
  Minified build for production: <https://fb.me/react-with-addons-0.13.2.min.js>
- **In-Browser JSX transformer**  
  <https://fb.me/JSXTransformer-0.13.2.js>

We've also published version `0.13.2` of the `react` and `react-tools` packages on npm and the `react` package on bower.

---

## Changelog {#changelog}

### React Core {#react-core}

#### New Features {#new-features}

- Added `strokeDashoffset`, `flexPositive`, `flexNegative` to the list of unitless CSS properties
- Added support for more DOM properties:
  - `scoped` - for `<style>` elements
  - `high`, `low`, `optimum` - for `<meter>` elements
  - `unselectable` - IE-specific property to prevent user selection

#### Bug Fixes {#bug-fixes}

- Fixed a case where re-rendering after rendering null didn't properly pass context
- Fixed a case where re-rendering after rendering with `style={null}` didn't properly update `style`
- Update `uglify` dependency to prevent a bug in IE8
- Improved warnings

### React with Add-Ons {#react-with-add-ons}

#### Bug Fixes {#bug-fixes-1}

- Immutabilty Helpers: Ensure it supports `hasOwnProperty` as an object key

### React Tools {#react-tools}

- Improve documentation for new options
