---
type: Web Page
title: $host • Svelte Docs
description: $host • Svelte documentation
resource: https://svelte.dev/docs/svelte/$host
timestamp: '2026-07-07T10:59:37.245126+00:00'
---

# $host

When compiling a component as a custom element, the `$host` rune provides access to the host element, allowing you to (for example) dispatch custom events (demo):

Stepper

```
<svelte:options customElement="my-stepper" />
<script>
	function dispatch(type) {
		$host().dispatchEvent(new CustomEvent(type));
	}
</script>
<button onclick={() => dispatch('decrement')}>decrement</button>
<button onclick={() => dispatch('increment')}>increment</button>
```
```
<svelte:options customElement="my-stepper" />
<script lang="ts">
	function dispatch(type) {
		$host().dispatchEvent(new CustomEvent(type));
	}
</script>
<button onclick={() => dispatch('decrement')}>decrement</button>
<button onclick={() => dispatch('increment')}>increment</button>
```
App

```
<script>
	import './Stepper.svelte';
	let count = $state(0);
</script>
<my-stepper
	ondecrement={() => count -= 1}
	onincrement={() => count += 1}
></my-stepper>
<p>count: {count}</p>
```
```
<script lang="ts">
	import './Stepper.svelte';
	let count = $state(0);
</script>
<my-stepper
	ondecrement={() => count -= 1}
	onincrement={() => count += 1}
></my-stepper>
<p>count: {count}</p>
```
Edit this page on GitHub llms.txt

previous next

# Citations

1. Source page: https://svelte.dev/docs/svelte/$host
