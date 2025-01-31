---
title: 'React v0.3.3'
author: [zpao]
---

We have a ton of great stuff coming in v0.4, but in the meantime we're releasing v0.3.3. This release addresses some small issues people were having and simplifies our tools to make them easier to use.

## react-tools {#react-tools}

- Upgrade Commoner so `require` statements are no longer relativized when passing through the transformer. This was a feature needed when building React, but doesn't translate well for other consumers of `bin/jsx`.
- Upgraded our dependencies on Commoner and Recast so they use a different directory for their cache.
- Freeze our esprima dependency.

## React {#react}

- Allow reusing the same DOM node to render different components. e.g. `React.renderComponent(<div/>, domNode); React.renderComponent(<span/>, domNode);` will work now.

## JSXTransformer {#jsxtransformer}

- Improved the in-browser transformer so that transformed scripts will execute in the expected scope. The allows components to be defined and used from separate files.
