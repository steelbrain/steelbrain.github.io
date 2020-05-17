---
published: true
title: What I don't like about Node.js
layout: post
---

[Node.js][] is a JavaScript runtime built on Chrome's V8 JavaScript engine. I have been working with Node.js for many years and for the most part, it has been a pleasant and productive experience. The prototyping speed and ability to scale that same quickly written and not particularly optimized code is amazing. It often falls short when you do try to optimize tho, you hit the architectural limitations faster than you expect to.

Please keep in mind that this rant is a product representing its time, so if you are reading this in the future, It may no longer be true, or I would hope so.

My personal experience with the short comings of Node.js comes as a result of trying to write a *fast* module bundler in Node.js. In case you don't know, a module bundler like [Webpack][], [Rollup][], [Parcel][] or my own (now deprecated) [Pundle][] is a piece of software that takes your program and its dependencies and bundles them up into a single file or sometimes chunks often to be consumed by browsers. Module bundlers are what let you `require(...)` or `import(...)` dependencies in the browser without the hassle of writing all those `<script ...>` tags by hand (and having to maintain the order of dependencies). You can configure them to do much more than that but that's the gist of it.

For a module bundler to become widely successful, it has to be configurable, work well and be reasonably fast. Now the configurability and being reasonably fast are difficult to achive together as I have come to learn through experience. For example, if you control all the steps in the pipeline, you only have to parse the file once and continue to work on AST from then onwards. Making it configurable means that each step much pass on the resultant string or buffer to the next step. Most module bundlers of current time work this around by manipulating strings directly using [magic-string][] or something similar to it. Using it allows you to infer trivial things and replace imports with internal references. Making the pipeline configurable however means that someone could put Babel transpilation or Terser minification in there, so your direct-string-manipulation isn't going to stop parsing and re-parsing.

Another thing that makes this very difficult, if not impossible to scale with the number of cores is the fact that you cannot share objects between threads in Node.js. IPC in Node.js is quite expensive, expensive enough that you have to architect your module bundler so that one process does nothing but task the others and even then, it ends up being bottle-necked because of IPC overhead of serializing and unserializing these thousands of files and their state at different steps in the pipeline, not to mention that if you want to avoid re-parsing the file, AST is much much bigger than the source and you **require** most metadata of all the files in a bundle to generate a source map. Node.js only recently got proper multi threading support via [`worker_threads`][], but even that does not allow sharing actual objects, only transferring ownership of Buffers.

The source of lack of ability to transfer objects instead of Buffers, per my unverified source is that v8 locks the entire virtual machine to all threads when you try to call something in parallel. So your module bundler is limited by the fundamental limitations of the v8 engine. It's like trying to run a horse race with only one horse. You cannot work around it.

[JavascriptCore][] (the JS engine used inside Safari) does not however lock the entire virtual machine but only the specific execution context. There was an attempt by [@voodooattack][] to create a runtime on top of it to rival (if not compliment) Node.js. It is called [Nexus.js][] and available on Github. It supports [Concurrent Variable Access][] among other cool things but sadly hasn't gotten the love it deserved. Most Module Bundlers, if they were just ported to Nexus.js with no changes other than to remove their current worker pooling implementations would run many many times faster.

Alas.

Further reading:

- [Locking in Webkit - Webkit Blog](https://webkit.org/blog/6161/locking-in-webkit/)

[Node.js]:https://nodejs.org/en/
[Webpack]:https://webpack.js.org/
[Rollup]:https://rollupjs.org/
[Parcel]:https://parceljs.org/
[Pundle]:https://github.com/steelbrain/pundle
[magic-string]:https://github.com/Rich-Harris/magic-string
[`worker_threads`]:https://nodejs.org/api/worker_threads.html
[JavascriptCore]:https://developer.apple.com/documentation/javascriptcore
[@voodooattack]:https://github.com/voodooattack
[Nexus.js]:https://github.com/voodooattack/nexusjs
[Concurrent Variable Access]:https://www.nexusjs.com/architecture/#concurrent-variable-access
