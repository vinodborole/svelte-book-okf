---
type: Web Page
title: <svelte:component> • Svelte Docs
description: <svelte:component> • Svelte documentation
resource: https://svelte.dev/docs/svelte/legacy-svelte-component
timestamp: '2026-07-07T10:59:37.245126+00:00'
---

# <svelte:component>

In runes mode, `<MyComponent>` will re-render if the value of `MyComponent` changes. See the Svelte 5 migration guide for an example.

In legacy mode, it won't — we must use `<svelte:component>`, which destroys and recreates the component instance when the value of its `this` expression changes:

`<svelte:component this={MyComponent} />`If `this` is falsy, no component is rendered.

Edit this page on GitHub llms.txt

previous next

# Citations

1. Source page: https://svelte.dev/docs/svelte/legacy-svelte-component
