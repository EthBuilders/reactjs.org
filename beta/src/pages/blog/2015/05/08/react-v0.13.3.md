---
title: 'React v0.13.3'
author: [zpao]
---

Today we're sharing another patch release in the v0.13 branch. There are only a few small changes, with a couple to address some issues that arose around that undocumented feature so many of you are already using: `context`. We also improved developer ergonomics just a little bit, making some warnings better.

The release is now available for download:

- **React**  
  Dev build with warnings: <https://fb.me/react-0.13.3.js>  
  Minified build for production: <https://fb.me/react-0.13.3.min.js>
- **React with Add-Ons**  
  Dev build with warnings: <https://fb.me/react-with-addons-0.13.3.js>  
  Minified build for production: <https://fb.me/react-with-addons-0.13.3.min.js>
- **In-Browser JSX transformer**  
  <https://fb.me/JSXTransformer-0.13.3.js>

We've also published version `0.13.3` of the `react` and `react-tools` packages on npm and the `react` package on bower.

---

## Changelog {#changelog}

### React Core {#react-core}

#### New Features {#new-features}

- Added `clipPath` element and attribute for SVG
- Improved warnings for deprecated methods in plain JS classes

#### Bug Fixes {#bug-fixes}

- Loosened `dangerouslySetInnerHTML` restrictions so `{__html: undefined}` will no longer throw
- Fixed extraneous context warning with non-pure `getChildContext`
- Ensure `replaceState(obj)` retains prototype of `obj`

### React with Add-ons {#react-with-add-ons}

### Bug Fixes {#bug-fixes-1}

- Test Utils: Ensure that shallow rendering works when components define `contextTypes`
