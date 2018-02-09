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

Having to do `sudo` for npm is bad for a lot of reasons, for examples the directories/files it creates while running as sudo will be owned by root and you won't get to modify them afterwords.

### How I do it

I use the [n][] Node.js version manager by TJ Holowaychuk.
Here's it's pros and cons in comparison

#### Things awesome about n

0. Zero overhead ([unlike NVM][nvm-slow])
0. Works on any POSIX environment
0. Never asks for or requires sudo
0. Can download *any* Node.js version
0. Installs modules in `~/n` (configurable) so they are isolated per user

#### Possible downsides of n

0. Too easy if you are a [real programmer][xkcd-joke] 😁

### How you can too

You should uninstall the currently installed Node.js/NPM before anything else and then execute these in order

```
curl -L https://git.io/n-install | bash
# Press y in the prompt or configure the directory if you want
# Then restart your shell to update it's $PATH and be able to use n/node/npm/npx
exec $SHELL
```

That's it fellaws, now you have an isolated, working Node.js setup. If you went with the defaults you should now have an `n` directory in your home directory. That's where your Node.js will live in from now on

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

or say you want to download Node.js v8.9.4 do

```
n 4.4.1
```

If you want to access the list of installed versions and select between them, do

```
n
```

You can find more about [n][] in it's README.

**Note**: When switching between shells, remember to also include the line inserted by `n-install` in your shell's config file such as `~/.bash_profile`, `~/.bashrc` or `~/.zshrc`.

That's all for now folks, happy coding!

[n]:https://github.com/tj/n
[semver]:https://semver.org/
[Node.js]:https://nodejs.org/en/
[nvm-slow]:https://broken-by.me/lazy-load-nvm/
[xkcd-joke]:https://xkcd.com/378/
