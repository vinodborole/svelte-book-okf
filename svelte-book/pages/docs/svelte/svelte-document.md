---
type: Web Page
title: <svelte:document> • Svelte Docs
description: <svelte:document> • Svelte documentation
resource: https://svelte.dev/docs/svelte/svelte-document
timestamp: '2026-07-09T12:17:00.027378+00:00'
---

# <svelte:document>

`<svelte:document onevent={handler} />``<svelte:document bind:prop={value} />`Similarly to `<svelte:window>`, this element allows you to add listeners to events on `document`, such as `visibilitychange`, which don't fire on `window`. It also lets you use [attachments](@attach) on `document`.

As with `<svelte:window>`, this element may only appear the top level of your component and must never be inside a block or element.

`<svelte:document onvisibilitychange={handleVisibilityChange} {@attach someAttachment} />`You can also bind to the following properties:

- `activeElement`
- `fullscreenElement`
- `pointerLockElement`
- `visibilityState`

All are readonly.

[ Edit this page on GitHub](https://github.com/sveltejs/svelte/edit/main/documentation/docs/05-special-elements/03-svelte-document.md) [ llms.txt](/docs/svelte/svelte-document/llms.txt)

previous next

# Citations

1. Source page: https://svelte.dev/docs/svelte/svelte-document
