---
title: 'React v0.14.3'
author: [zpao]
---

It's time for another installment of React patch releases! We didn't break anything in v0.14.2 but we do have a couple of other bugs we're fixing. The biggest change in this release is actually an addition of a new built file. We heard from a number of people that they still need the ability to use React to render to a string on the client. While the use cases are not common and there are other ways to achieve this, we decided that it's still valuable to support. So we're now building `react-dom-server.js`, which will be shipped to Bower and in the `dist/` directory of the `react-dom` package on npm. This file works the same way as `react-dom.js` and therefore requires that the primary React build has already been included on the page.

The release is now available for download:

- **React**  
  Dev build with warnings: <https://fb.me/react-0.14.3.js>  
  Minified build for production: <https://fb.me/react-0.14.3.min.js>
- **React with Add-Ons**  
  Dev build with warnings: <https://fb.me/react-with-addons-0.14.3.js>  
  Minified build for production: <https://fb.me/react-with-addons-0.14.3.min.js>
- **React DOM** (include React in the page before React DOM)  
  Dev build with warnings: <https://fb.me/react-dom-0.14.3.js>  
  Minified build for production: <https://fb.me/react-dom-0.14.3.min.js>
- **React DOM Server** (include React in the page before React DOM Server)  
  Dev build with warnings: <https://fb.me/react-dom-server-0.14.3.js>  
  Minified build for production: <https://fb.me/react-dom-server-0.14.3.min.js>

We've also published version `0.14.3` of the `react`, `react-dom`, and addons packages on npm and the `react` package on bower.

---

## Changelog {#changelog}

### React DOM {#react-dom}

- Added support for `nonce` attribute for `<script>` and `<style>` elements
- Added support for `reversed` attribute for `<ol>` elements

### React TestUtils Add-on {#react-testutils-add-on}

- Fixed bug with shallow rendering and function refs

### React CSSTransitionGroup Add-on {#react-csstransitiongroup-add-on}

- Fixed bug resulting in timeouts firing incorrectly when mounting and unmounting rapidly

### React on Bower {#react-on-bower}

- Added `react-dom-server.js` to expose `renderToString` and `renderToStaticMarkup` for usage in the browser
