---
title: 'React v0.5'
author: [zpao]
---

This release is the result of several months of hard work from members of the team and the community. While there are no groundbreaking changes in core, we've worked hard to improve performance and memory usage. We've also worked hard to make sure we are being consistent in our usage of DOM properties.

The biggest change you'll notice as a developer is that we no longer support `class` in JSX as a way to provide CSS classes. Since this prop was being converted to `className` at the transform step, it caused some confusion when trying to access it in composite components. As a result we decided to make our DOM properties mirror their counterparts in the JS DOM API. There are [a few exceptions](https://github.com/facebook/react/blob/master/src/dom/DefaultDOMPropertyConfig.js#L156) where we deviate slightly in an attempt to be consistent internally.

The other major change in v0.5 is that we've added an additional build - `react-with-addons` - which adds support for some extras that we've been working on including animations and two-way binding. [Read more about these addons in the docs](/docs/addons.html).

## Thanks to Our Community {#thanks-to-our-community}

We added _22 new people_ to the list of authors since we launched React v0.4.1 nearly 3 months ago. With a total of 48 names in our `AUTHORS` file, that means we've nearly doubled the number of contributors in that time period. We've seen the number of people contributing to discussion on IRC, mailing lists, Stack Overflow, and GitHub continue rising. We've also had people tell us about talks they've given in their local community about React.

It's been awesome to see the things that people are building with React, and we can't wait to see what you come up with next!

## Changelog {#changelog}

### React {#react}

- Memory usage improvements - reduced allocations in core which will help with GC pauses
- Performance improvements - in addition to speeding things up, we made some tweaks to stay out of slow path code in V8 and Nitro.
- Standardized prop -> DOM attribute process. This previously resulting in additional type checking and overhead as well as confusing cases for users. Now we will always convert your value to a string before inserting it into the DOM.
- Support for Selection events.
- Support for [Composition events](https://developer.mozilla.org/en-US/docs/Web/API/CompositionEvent).
- Support for additional DOM properties (`charSet`, `content`, `form`, `httpEquiv`, `rowSpan`, `autoCapitalize`).
- Support for additional SVG properties (`rx`, `ry`).
- Support for using `getInitialState` and `getDefaultProps` in mixins.
- Support mounting into iframes.
- Bug fixes for controlled form components.
- Bug fixes for SVG element creation.
- Added `React.version`.
- Added `React.isValidClass` - Used to determine if a value is a valid component constructor.
- Removed `React.autoBind` - This was deprecated in v0.4 and now properly removed.
- Renamed `React.unmountAndReleaseReactRootNode` to `React.unmountComponentAtNode`.
- Began laying down work for refined performance analysis.
- Better support for server-side rendering - [react-page](https://github.com/facebook/react-page) has helped improve the stability for server-side rendering.
- Made it possible to use React in environments enforcing a strict [Content Security Policy](https://developer.mozilla.org/en-US/docs/Security/CSP/Introducing_Content_Security_Policy). This also makes it possible to use React to build Chrome extensions.

### React with Addons (New!) {#react-with-addons-new}

- Introduced a separate build with several "addons" which we think can help improve the React experience. We plan to deprecate this in the long-term, instead shipping each as standalone pieces. [Read more in the docs](/docs/addons.html).

### JSX {#jsx}

- No longer transform `class` to `className` as part of the transform! This is a breaking change - if you were using `class`, you _must_ change this to `className` or your components will be visually broken.
- Added warnings to the in-browser transformer to make it clear it is not intended for production use.
- Improved compatibility for Windows
- Improved support for maintaining line numbers when transforming.
