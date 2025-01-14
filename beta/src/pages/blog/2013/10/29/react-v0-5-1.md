---
title: 'React v0.5.1'
author: [zpao]
---

This release focuses on fixing some small bugs that have been uncovered over the past two weeks. I would like to thank everybody involved, specifically members of the community who fixed half of the issues found. Thanks to [Sophie Alpert][1], [Andrey Popp][2], and [Laurence Rowe][3] for their contributions!

## Changelog {#changelog}

### React {#react}

- Fixed bug with `<input type="range">` and selection events.
- Fixed bug with selection and focus.
- Made it possible to unmount components from the document root.
- Fixed bug for `disabled` attribute handling on non-`<input>` elements.

### React with Addons {#react-with-addons}

- Fixed bug with transition and animation event detection.

[1]: https://github.com/sophiebits
[2]: https://github.com/andreypopp
[3]: https://github.com/lrowe
