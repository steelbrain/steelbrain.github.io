---
published: true
title: How I debug Node.js
layout: post
---
[Node.js][] is a server side runtime for Javascript apps. Being a server sided runtime, it doesn't have a GUI. Therefore it's abilities to provide an easy to use debugging interface are limited.

### Why I don't like Popular Options

There are several ways of debugging Node.js, here are few of the reasons why I don't like the most popular ones

#### Builtin CLI debugger

0. It doesn't have a GUI of course
0. It's slow and even hangs at times
0. You have to remember it's commands
0. Debugging complex problems is nearly impossible if not impossible

#### [node-inspector][]

0. It shows ES6 Maps and Sets as `null`
0. It shows objects as empty randomly
0. It is generally slow
0. It's *very* unstable

#### IDE Debuggers

0. The IDEs are costy
0. Each has their own UI
0. They are hard to setup
0. They lack advance features

### Electron to the rescue

[Electron][] is an open source project by GitHub, it is basically Chromium + Node.js. It has the best of both worlds, node's `require`, `global`s and all the other APIs along with Chromium Dev Tools.

I have written a small wrapper around Electron to allow for quick Node.js debugging. It's called [DeNode], short for Debug Node.
You can install it using npm

```sh
npm install -g denode
```

It registers itself as `denode` bin, it accepts an optional file path of the node module to execute on boot.

```sh
denode
denode ./index
denode `which browserify`
```

#### What's awesome about this?

0. You can click and expand on deep nested objects
0. You can profile your apps for memory leaks and CPU time
0. You can set breakpoints on the fly
0. You can update running code from dev tools
0. You can compile your files with babel and debug without banging your head in a wall using sourcemaps
0. Basically, all the awesomeness of Chromium Dev Tools

#### What's the side effect?

0. Not having the ability to execute it over a network or VM, theoretically you could do X forwarding but it would get too slow and painful

---

That's what I use to debug my Node.js app, let me know what you think of it in the comments below.

[Node.js]:https://nodejs.org/en/
[node-inspector]:https://www.npmjs.com/package/node-inspector
[Electron]:http://electron.atom.io/
[DeNode]:https://github.com/steelbrain/denode
