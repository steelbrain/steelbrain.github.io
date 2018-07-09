---
published: false
title: How imports are handled in Pundle
layout: post
---

This post is a part of the series ["An Intro to Pundle"][pundle-intro].

---

Imports are a way of sharing bindings between modules. They help keep the code modular and maintainable as the size of the codebase grows as well as sharing it with other people trying to solve similar problems (think [npmjs][]).

In Javascript runtimes like V8 (heart of Chrome browser and Node.js) you can import JS files into JS files but not for example CSS files into JS files. Being able to import CSS into JS would help majorly modularize the code as well as help avoid any conflicts on the global namespace.

Interoperability between asset types as different as JS and CSS (compared to say JS and WASM) require a lot of decisions that are better done by the bundler instead of runtime. For example, to use the contents of the asset or to a path pointing at it because the size of the asset is too big (think 150kb+ of blob wouldn't make sense in a JS bundle).

While other module bundlers try to hard-code how the bridges work in the core, Pundle takes a different approach. Pundle's file resolver allows users to specify completely arbitrary "format"s to use for each extension. Pundle enforces "chunk"s to have the same format throughout so when you import a css file or a golang file or any other non-js format file, It'll be force loaded as `js` as to allow the processors to provide "bridge" code.

While providing the bridge code the transformers can add the import as a chunk dependency and return path to it, return it in base64 blob etc. For css this lets us do interesting things like return the [css modules object][css-modules] to the requiring module or insert as a JS blob that accepts HMR.

For example, here's what happens when your import `./index.js` imports an `./index.css`

- Resolve `./index.js` relative to project root
- Resolved to `project/index.js` with format `js`
- Process `project/index.js` as `js` and scan for imports
- Resolve `./index.css` relative to `./index.js`
- Resolved to `project/index.css` with format `css`
- Process `project/index.css` as `js` and scan for imports (notice how we're processing as `js`)
  - If the file contains with `.module` before its extension like (`.module.css`), return its module mapping back to JS
  - If HMR and Development are turned on, put the raw contents as blob to create a style tag to be replaced on HMR later
    - Otherwise add `project/index.css` with format `css` as an external dependency of the file

This process depending on your configuration would either embed the css in JS file or add it as an external dependency (while also resolving its imports and adding them as dependencies recursively). This allows Pundle to maintain multiple versions of the same file with different formats. This allows for an unprecedented level of customizable interoperability between different formats.

[pundle-intro]: /2018/07/09/an-intro-to-pundle.html
[npmjs]: https://docs.npmjs.com/getting-started/what-is-npm
[css-modules]: https://github.com/css-modules/css-modules
