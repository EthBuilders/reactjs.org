---
title: 'React v0.14.4'
author: [sophiebits]
---

Happy December! We have a minor point release today. It has just a few small bug fixes.

The release is now available for download:

- **React**  
  Dev build with warnings: <https://fb.me/react-0.14.4.js>  
  Minified build for production: <https://fb.me/react-0.14.4.min.js>
- **React with Add-Ons**  
  Dev build with warnings: <https://fb.me/react-with-addons-0.14.4.js>  
  Minified build for production: <https://fb.me/react-with-addons-0.14.4.min.js>
- **React DOM** (include React in the page before React DOM)  
  Dev build with warnings: <https://fb.me/react-dom-0.14.4.js>  
  Minified build for production: <https://fb.me/react-dom-0.14.4.min.js>
- **React DOM Server** (include React in the page before React DOM Server)  
  Dev build with warnings: <https://fb.me/react-dom-server-0.14.4.js>  
  Minified build for production: <https://fb.me/react-dom-server-0.14.4.min.js>

We've also published version `0.14.4` of the `react`, `react-dom`, and addons packages on npm and the `react` package on bower.

---

## Changelog {#changelog}

### React {#react}

- Minor internal changes for better compatibility with React Native

### React DOM {#react-dom}

- The `autoCapitalize` and `autoCorrect` props are now set as attributes in the DOM instead of properties to improve cross-browser compatibility
- Fixed bug with controlled `<select>` elements not handling updates properly

### React Perf Add-on {#react-perf-add-on}

- Some DOM operation names have been updated for clarity in the output of `.printDOM()`
