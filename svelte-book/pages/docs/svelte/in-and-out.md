---
type: Web Page
title: 'in: and out: • Svelte Docs'
description: 'in: and out: • Svelte documentation'
resource: https://svelte.dev/docs/svelte/in-and-out
timestamp: '2026-07-09T12:17:00.027378+00:00'
---

# in: and out:

The `in:` and `out:` directives are identical to [ transition:](transition), except that the resulting transitions are not bidirectional — an 

`in` transition will continue to 'play' alongside the `out` transition, rather than reversing, if the block is outroed while the transition is in progress. If an out transition is aborted, transitions will restart from scratch.```
<script>
  import { fade, fly } from 'svelte/transition';
  let visible = $state(false);
</script>
<label>
  <input type="checkbox" bind:checked={visible}>
  visible
</label>
{#if visible}
	<div in:fly={{ y: 200 }} out:fade>flies in, fades out</div>
{/if}
```
[ Edit this page on GitHub](https://github.com/sveltejs/svelte/edit/main/documentation/docs/03-template-syntax/15-in-and-out.md) [ llms.txt](/docs/svelte/in-and-out/llms.txt)

previous next

# Citations

1. Source page: https://svelte.dev/docs/svelte/in-and-out
