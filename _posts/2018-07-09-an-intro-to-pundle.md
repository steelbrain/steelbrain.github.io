---
published: true
title: An Intro to Pundle
layout: post
---

[Pundle][pundle-gh] (Peaceful Bundle) is a next generation module bundler. It allows you to use Node.js style require statements in the browser and supports splitting out of the box with [`import()`][import-rfc] syntax. It uses worker processes to parallelize the work as much as possible, that combined with a file system transform cache delivers amazing performance on recurrent builds.

You can read how it works in this series of posts:

- [How imports are handled in Pundle](/2018/07/09/how-imports-are-handled-in-pundle.html)
- [How HMR in Pundle Works](/2018/07/09/how-hmr-in-pundle-works.html)

---

This series of posts is a Work-in-Progress and would be updated as Pundle furthers it's path towards release.

[pundle-gh]: https://github.com/steelbrain/pundle
[import-rfc]: https://github.com/tc39/proposal-dynamic-import
