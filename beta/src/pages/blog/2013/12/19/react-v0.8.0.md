---
title: 'React v0.8'
author: [zpao]
---

I'll start by answering the obvious question:

> What happened to 0.6 and 0.7?

It's become increasingly obvious since our launch in May that people want to use React on the server. With the server-side rendering abilities, that's a perfect fit. However using the same copy of React on the server and then packaging it up for the client is surprisingly a harder problem. People have been using our `react-tools` module which includes React, but when browserifying that ends up packaging all of `esprima` and some other dependencies that aren't needed on the client. So we wanted to make this whole experience better.

We talked with [Jeff Barczewski][jeff] who was the owner of the `react` module on npm. He was kind enough to transition ownership to us and release his package under a different name: `autoflow`. I encourage you to [check it out][autoflow] if you're writing a lot of asynchronous code. In order to not break all of `react`'s current users of 0.7.x, we decided to bump our version to 0.8 and skip the issue entirely. We're also including a warning if you use our `react` module like you would use the previous package.

In order to make the transition to 0.8 for our current users as painless as possible, we decided to make 0.8 primarily a bug fix release on top of 0.5. No public APIs were changed (even if they were already marked as deprecated). We haven't added any of the new features we have in master, though we did take the opportunity to pull in some improvements to internals.

We hope that by releasing `react` on npm, we will enable a new set of uses that have been otherwise difficult. All feedback is welcome!

## Changelog {#changelog}

### React {#react}

- Added support for more attributes:
  - `rows` & `cols` for `<textarea>`
  - `defer` & `async` for `<script>`
  - `loop` for `<audio>` & `<video>`
  - `autoCorrect` for form fields (a non-standard attribute only supported by mobile WebKit)
- Improved error messages
- Fixed Selection events in IE11
- Added `onContextMenu` events

### React with Addons {#react-with-addons}

- Fixed bugs with TransitionGroup when children were undefined
- Added support for `onTransition`

### react-tools {#react-tools}

- Upgraded `jstransform` and `esprima-fb`

### JSXTransformer {#jsxtransformer}

- Added support for use in IE8
- Upgraded browserify, which reduced file size by ~65KB (16KB gzipped)

[jeff]: https://github.com/jeffbski
[autoflow]: https://github.com/jeffbski/autoflow
