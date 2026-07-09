---
type: Web Page
title: $inspect • Svelte Docs
description: $inspect • Svelte documentation
resource: https://svelte.dev/docs/svelte/$inspect
timestamp: '2026-07-09T12:17:00.027378+00:00'
---

# $inspect

`$inspect`only works during development. In a production build it becomes a noop.

The `$inspect` rune is roughly equivalent to `console.log`, with the exception that it will re-run whenever its argument changes. `$inspect` tracks reactive state deeply, meaning that updating something inside an object or array using fine-grained reactivity will cause it to re-fire:

```
<script>
	let count = $state(0);
	let message = $state('hello');
	$inspect(count, message); // will console.log when `count` or `message` change
</script>
<button onclick={() => count++}>Increment</button>
<input bind:value={message} />
```
```
<script lang="ts">
	let count = $state(0);
	let message = $state('hello');
	$inspect(count, message); // will console.log when `count` or `message` change
</script>
<button onclick={() => count++}>Increment</button>
<input bind:value={message} />
```
On updates, a stack trace will be printed, making it easy to find the origin of a state change (unless you're in the playground, due to technical limitations).

## $inspect(...).with

`$inspect(...)` returns an object with a `with` method, which you can invoke with a callback that will then be invoked instead of `console.log`. The first argument to the callback is either `"init"` or `"update"`; subsequent arguments are the values passed to `$inspect`:

```
<script>
	let count = $state(0);
	$inspect(count).with((type, count) => {
		if (type === 'update') {
			debugger; // or `console.trace`, or whatever you want
		}
	});
</script>
<button onclick={() => count++}>Increment</button>
```
```
<script lang="ts">
	let count = $state(0);
	$inspect(count).with((type, count) => {
		if (type === 'update') {
			debugger; // or `console.trace`, or whatever you want
		}
	});
</script>
<button onclick={() => count++}>Increment</button>
```
## $inspect.trace(...)

This rune, added in 5.14, causes the surrounding function to be *traced* in development. Any time the function re-runs as part of an [effect]($effect) or a [derived]($derived), information will be printed to the console about which pieces of reactive state caused the effect to fire.

```
<script>
	import { doSomeWork } from './elsewhere';
	$effect(() => {
		// $inspect.trace must be the first statement of a function body
		$inspect.trace();
		doSomeWork();
	});
</script>
```
`$inspect.trace` takes an optional first argument which will be used as the label.

# Citations

1. Source page: https://svelte.dev/docs/svelte/$inspect
