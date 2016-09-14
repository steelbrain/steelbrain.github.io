---
published: true
title: How I manage multiple Node.js versions
layout: post
---
[Node.js][] is a lightweight Javascript runtime. It follows the [Semantic Versioning][semver] scheme so every major release has multiple API breaking changes. We change our Node.js version to make a certain app work or to upgrade to the latest version.

### Why I don't like Popular Options

After evaluating different popular options including NVM, Ubuntu Repos, Ubuntu PPAs, OSX Homebrew and OSX Macports I experienced a lot of issues with them including

0. They are OS specific
0. You cannot install specific Node.js versions
0. They can cause conflicts when more than one users try to run different versions of same global modules
0. You have to use `sudo` when installing global modules or linking local ones (except for homebrew)

I am a security conscious person, I would do anything to avoid using that `sudo` before installing modules from people I don't even know. If you don't share the same fear, read this [Package install scripts vulnerability][npm-vuln] post by npm and you will.

### How I do it

I use the [n][] Node.js version manager by TJ Holowaychuk.
Here's it's pros and cons in comparison

#### Things awesome about n

0. Zero overhead ([unlike NVM][nvm-slow])
0. Works on any POSIX environment
0. Never asks for or requires sudo
0. Can download *any* Node.js version
0. Installs modules in `~/n` so they are isolated per user

#### Possible downsides of n

0. Too easy if you are a [real programmer][xkcd-joke] 😁

### How you can too

There's two different ways to install Node.js, the easy way is when you already have Node.js installed. The hard way assumes nothing!

#### The easy way

The easy way makes use of npm global scripts and is pretty simple.

```
npm install -g n
```

#### The hard way

The hard way makes use of [`n-install`](https://github.com/mklement0/n-install). It installs Node.js in your `~/n` directory and does **not** uninstall or remove any previous versions. The first thing you should do is uninstall any installed version of Node.js.

You can skip the removal steps if you do not have Node.js installed already.

```
# If you use ubuntu
sudo apt-get remove --purge nodejs
# If you use homebrew
brew uninstall node
# If yu use macports
sudo port uninstall nodejs
# If you use nvm
LINK="https://github.com/creationix/nvm/issues/298"
xdg-open $LINK || open $LINK
```

Then to make sure, garbage collect the global `node_modules` directory

```
sudo rm -rf /usr/local/lib/node_modules
sudo rm -rf /usr/lib/node_modules
```

Now run the magical `n-install` script and it'll set it up for you

```
curl -L -o /tmp/n-install-script https://git.io/n-install
bash /tmp/n-install-script -y
exec $SHELL # To re-initialize the PATH variable
```

That's it fellaws, now you have an isolated, working Node.js setup.

### Basic Usage

n is a bash script so it's lightweight/minimal but still includes all the necessary features.

To upgrade to the latest version of Node.js do

```
n latest
```

or to install the lts version do

```
n lts
```

or say you want to download Node.js v4.4.1 do

```
n 4.4.1
```

If you want to access the list of installed versions and select between them, do

```
n
```

You can find more about [n][] in it's README.

**Note**: When switching between shells, remember to also include the line inserted by `n-install` in your `~/.bashrc` or `~/.zshrc` into your new shell configuration.

That's all for now folks, happy coding!

[n]:https://github.com/tj/n
[semver]:http://semver.org/
[Node.js]:https://nodejs.org/en/
[npm-vuln]:http://blog.npmjs.org/post/141702881055/package-install-scripts-vulnerability
[nvm-slow]:http://broken-by.me/lazy-load-nvm/
[xkcd-joke]:https://xkcd.com/378/
