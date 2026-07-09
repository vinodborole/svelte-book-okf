---
type: Web Page
title: <svelte:body> • Svelte Docs
description: <svelte:body> • Svelte documentation
resource: https://svelte.dev/docs/svelte/svelte-body
timestamp: '2026-07-09T12:17:00.027378+00:00'
---

# <svelte:body>

`<svelte:body onevent={handler} />`Similarly to `<svelte:window>`, this element allows you to add listeners to events on `document.body`, such as `mouseenter` and `mouseleave`, which don't fire on `window`. It also lets you use [actions](use) on the `<body>` element.

As with `<svelte:window>` and `<svelte:document>`, this element may only appear at the top level of your component and must never be inside a block or element.

`<svelte:body onmouseenter={handleMouseenter} onmouseleave={handleMouseleave} use:someAction />`[ Edit this page on GitHub](https://github.com/sveltejs/svelte/edit/main/documentation/docs/05-special-elements/04-svelte-body.md) [ llms.txt](/docs/svelte/svelte-body/llms.txt)

previous next

# Citations

1. Source page: https://svelte.dev/docs/svelte/svelte-body
