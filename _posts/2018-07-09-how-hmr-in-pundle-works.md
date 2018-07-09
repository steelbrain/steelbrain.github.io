---
published: false
title: How HMR in Pundle works
layout: post
---

This post is a part of the series ["An Intro to Pundle"][pundle-intro].

---

HMR (Hot Module Replacement) is a way to apply changes to parts of the app while it's still running allowing developers to quickly test new changes and be more productive. Webpack has a [great introduction to HMR][hmr-webpack]. I recommend you read it before reading through the rest of the post.

Here are some of the interesting things about Pundle's implementation of HMR

#### Determining HMR server path:

Both Webpack and Parcel use [WebSockets][ws] to deliver HMR to the clients. These can be a bit hard to develop / maintain because to handle WebSocket connections on the server side you have to either listen on a separate port for HMR (if source is on https, then you have to have https on that one too) or you have to provide the server object to the WebSocket libs (which means it cannot be an express middleware).

That leads to extra moving parts in the config, `hmrHost` or `hmrPath`. Pundle solves this by getting rid of WebSockets and using `fetch()` streaming instead. Fetch streaming works on normal HTTP requests so it can be done in an express middleware and does not need any third party library. Pundle instead uses `document.currentScript` + `.hmr.pundle` and then handles it as a route on the server.

Because this is for HMR, you don't have to worry about supporting fetch streaming in older browsers as your development testing ones should be up to date.

#### Compiling and applying changes

While Webpack uses a poll mechanism to determine if files have changed on the server side, Pundle makes the server do the heavy lifting. It writes to an internal list of pending http fetch requests. Pundle's architecture allows it to generate individual files as temporary chunks, meaning that even if your bundle is 100mbs in size, only changed files would be transformed and sent to the client. This gives Pundle `O(nFilesChanged)` instead of `O(nFilesTotal)` time complexity for HMR.

Pundle also only regenerates a full bundle (ie joining all the transformed files together) only when it receives the next non-HMR request meaning that if you keep saving your files without refreshing, your CPU cycles won't be wasted.

---

If you would like to read the source code of the HMR client (at the time of writing this post), You can [hmr-client on Github](https://github.com/steelbrain/pundle/blob/192131782c9c76180cc6824cd1094955b3521e0f/packages/pundle-dev-middleware/src/client/hmr-client.js)

[pundle-intro]: /2018/07/09/an-intro-to-pundle.html
[hmr-webpack]: https://webpack.js.org/concepts/hot-module-replacement/
[ws]: https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API
