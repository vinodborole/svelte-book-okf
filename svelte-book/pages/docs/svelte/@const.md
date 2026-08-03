---
type: Web Page
title: '{@const ...} • Svelte Docs'
description: '{@const ...} • Svelte documentation'
resource: https://svelte.dev/docs/svelte/@const
timestamp: '2026-08-03T08:54:23.898986+00:00'
---

# {@const ...}

 `{@const x = y}` is legacy syntax — use [`{const x = $derived(y)}`](declaration-tags) instead

The `{@const ...}` tag defines a local constant.

```
{#each boxes as box}
	{@const area = box.width * box.height}
	{box.width} * {box.height} = {area}
{/each}
```
`{@const}` is only allowed as an immediate child of a block — `{#if ...}`, `{#each ...}`, `{#snippet ...}` and so on — a `<Component />` or a `<svelte:boundary>`.

 [Edit this page on GitHub](https://github.com/sveltejs/svelte/edit/main/documentation/docs/03-template-syntax/10-@const.md)  [llms.txt](/docs/svelte/@const/llms.txt)

previous next

# Citations

1. Source page: https://svelte.dev/docs/svelte/@const
