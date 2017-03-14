---
published: true
title: Atom Linter v2 Released
layout: post
---

It has been almost two years since the v1.0 of the [`linter`][] package for Atom was released to the general public. Since then, we have come a long way. Linter is the second most downloaded Atom package right now with over 2.7 million downloads. Thank you for being a part of it 🙇.

Linter v2 has been in the oven for more than a year and I'm excited to announce it's release to you today.

## Separate UI package

Starting from v2, Linter has support for pluggable UI providers. The default UI has been moved to [`linter-ui-default`][]. This opens ways for users to swap out UIs for Linter at will.

## Linter Panel

The Linter Panel is now a table with sortable columns. You can configure it to represent the current file or the entire project.

![Linter UI Default Panel](https://cloud.githubusercontent.com/assets/4278113/23875411/29906274-085b-11e7-88f9-a1c05a18d7eb.gif)

## Linter Status

The Linter Status, after much feedback, now includes three separate counts for `Error`s, `Warning`s and `Info`s. You can configure it to toggle the panel or jump to the error of the specific type when clicked. Just like the Linter Panel, you can configure Linter Status to represent the current file or the entire project.

<img alt="Linter UI Default Status" src="https://cloud.githubusercontent.com/assets/4278113/23875588/e4580544-085b-11e7-84c7-df6cc9725b0f.gif" />

## Busy Signal Integration

The new Linter UI now includes busy signal integration so you know which Linter provider is being excuted on which file.

<img alt="Linter UI Default Busy Signal" height="200" src="https://cloud.githubusercontent.com/assets/4278113/23875763/5c738c6a-085c-11e7-8d72-5b73f9306650.gif" />

## Intentions Integration

Linter now fully integrates with the [`intentions`][] package. This allows providers to use `solutions` in v2 and `fix` in v1 to allow the users to fix the issue without leaving the comfort of their Atom Editor.

<img alt="Linter UI Default Intentions" src="https://cloud.githubusercontent.com/assets/4278113/23875866/cdd051fe-085c-11e7-81c9-89fa59456891.gif" />

## Toggling Linter Providers

Linter v2 now includes commands to toggle linter providers from the command pallete.

<img alt="Linter Toggle Providers" src="https://cloud.githubusercontent.com/assets/4278113/23630039/56e760a4-02db-11e7-9b9b-0d8321a4ac4c.gif" />

## Tooltip Enhancements

We all know how intrusive tooltips can become when they follow your keyboard, therefore in v2 We've added an option for them to follow your mouse. This provides a much more comfortable Linter experience.

<img alt="Linter UI Default following Mouse" src="https://cloud.githubusercontent.com/assets/4278113/23876163/ebec18ca-085d-11e7-9137-b7a2c6ff6a14.gif" />
<img alt="Linter UI Default Follows Keyboard" src="https://cloud.githubusercontent.com/assets/4278113/23876225/3f5d8a98-085e-11e7-8c4f-171b8aa46367.gif" />

## TreeView Decoration

Linter v2 now decorates your TreeView. This is especially useful when combined with Project-Scoped linters like [`flow-ide`][] as it gives you the status of your entire project in just one look.

<img alt="Linter UI Default Tree View" height="500" src="https://cloud.githubusercontent.com/assets/4278113/23876314/b29a88a8-085e-11e7-98ef-33e57fbf12c9.gif" />

## Upgrading to Linter v2

If you are a package maintainer, we've prepared [migration docs](https://github.com/steelbrain/linter/tree/master/docs#migration-guides) for you. They are not perfect but we're open to contributions!

## Closing Thoughts

You can see [Linter v2 in Action](https://www.youtube.com/watch?v=Ek7p49sf8Eo) in the demo video.

This release is really exciting for me. I want to thank [Landon Abney](https://github.com/Arcanemagus) for his continued involvement in the Linter Project and for maintaining dozens of repositories in the [AtomLinter](https://github.com/AtomLinter) org. Thanks to everyone who has ever contributed to the Linter Project, and the users for providing useful bug reports. Peace out 👋 ☮.


[`linter`]:https://atom.io/packages/linter
[`linter-ui-default`]:https://atom.io/packages/linter-ui-default
[`intentions`]:https://atom.io/packages/intentions
[`flow-ide`]:https://atom.io/packages/flow-ide
