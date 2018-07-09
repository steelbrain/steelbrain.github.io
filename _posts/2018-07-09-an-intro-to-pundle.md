---
published: false
title: An Intro to Pundle
layout: post
---

[Pundle][pundle-gh] is a next generation module bundler. It allows you to use Node.js style require statements in the browser along with supporting splitting out of the box with [`import()`][import-rfc] syntax. It uses worker processes to parallelize the work as much as possible, that combined with a file system transform cache delivers amazing performance on recurrent builds.

Here's links to the posts in this series where I try to explain how Pundle works:

[pundle-gh]: https://github.com/steelbrain/pundle
[import-rfc]: https://github.com/tc39/proposal-dynamic-import
