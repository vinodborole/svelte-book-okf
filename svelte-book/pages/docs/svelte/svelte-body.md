---
type: Web Page
title: <svelte:body> • Svelte Docs
description: <svelte:body> • Svelte documentation
resource: https://svelte.dev/docs/svelte/svelte-body
timestamp: '2026-07-07T10:59:37.245126+00:00'
---

# <svelte:body>

`<svelte:body onevent={handler} />`Similarly to `<svelte:window>`, this element allows you to add listeners to events on `document.body`, such as `mouseenter` and `mouseleave`, which don't fire on `window`. It also lets you use actions on the `<body>` element.

As with `<svelte:window>` and `<svelte:document>`, this element may only appear at the top level of your component and must never be inside a block or element.

`<svelte:body onmouseenter={handleMouseenter} onmouseleave={handleMouseleave} use:someAction />`Edit this page on GitHub llms.txt

previous next

# Citations

1. Source page: https://svelte.dev/docs/svelte/svelte-body
