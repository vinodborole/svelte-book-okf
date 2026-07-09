---
type: Web Page
title: <svelte:component> • Svelte Docs
description: <svelte:component> • Svelte documentation
resource: https://svelte.dev/docs/svelte/legacy-svelte-component
timestamp: '2026-07-09T12:17:00.027378+00:00'
---

# <svelte:component>

In runes mode, `<MyComponent>` will re-render if the value of `MyComponent` changes. See the [Svelte 5 migration guide](/docs/svelte/v5-migration-guide#svelte:component-is-no-longer-necessary) for an example.

In legacy mode, it won't — we must use `<svelte:component>`, which destroys and recreates the component instance when the value of its `this` expression changes:

`<svelte:component this={MyComponent} />`If `this` is falsy, no component is rendered.

[ Edit this page on GitHub](https://github.com/sveltejs/svelte/edit/main/documentation/docs/99-legacy/30-legacy-svelte-component.md) [ llms.txt](/docs/svelte/legacy-svelte-component/llms.txt)

previous next

# Citations

1. Source page: https://svelte.dev/docs/svelte/legacy-svelte-component
