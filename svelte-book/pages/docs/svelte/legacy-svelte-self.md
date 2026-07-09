---
type: Web Page
title: <svelte:self> • Svelte Docs
description: <svelte:self> • Svelte documentation
resource: https://svelte.dev/docs/svelte/legacy-svelte-self
timestamp: '2026-07-09T12:17:00.027378+00:00'
---

# <svelte:self>

The `<svelte:self>` element allows a component to include itself, recursively.

It cannot appear at the top level of your markup; it must be inside an if or each block or passed to a component's slot to prevent an infinite loop.

```
<script>
	export let count;
</script>
{#if count > 0}
	<p>counting down... {count}</p>
	<svelte:self count={count - 1} />
{:else}
	<p>lift-off!</p>
{/if}
```
This concept is obsolete, as components can import themselves:

App`<script> import Self from './App.svelte' export let count; </script> {#if count > 0} <p>counting down... {count}</p> <Self count={count - 1} /> {:else} <p>lift-off!</p> {/if}``<script lang="ts"> import Self from './App.svelte' export let count; </script> {#if count > 0} <p>counting down... {count}</p> <Self count={count - 1} /> {:else} <p>lift-off!</p> {/if}`

[ Edit this page on GitHub](https://github.com/sveltejs/svelte/edit/main/documentation/docs/99-legacy/31-legacy-svelte-self.md) [ llms.txt](/docs/svelte/legacy-svelte-self/llms.txt)

previous next

# Citations

1. Source page: https://svelte.dev/docs/svelte/legacy-svelte-self
