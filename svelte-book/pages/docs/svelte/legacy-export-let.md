---
type: Web Page
title: export let • Svelte Docs
description: export let • Svelte documentation
resource: https://svelte.dev/docs/svelte/legacy-export-let
timestamp: '2026-07-09T12:17:00.027378+00:00'
---

# export let

In runes mode, [component props](basic-markup#Component-props) are declared with the [ $props]($props) rune, allowing parent components to pass in data.

In legacy mode, props are marked with the `export` keyword, and can have a default value:

```
<script>
	export let foo;
	export let bar = 'default value';
	// Values that are passed in as props
	// are immediately available
	console.log({ foo });
</script>
```
The default value is used if it would otherwise be `undefined` when the component is created.

Unlike in runes mode, if the parent component changes a prop from a defined value to

`undefined`, it does not revert to the initial value.

Props without default values are considered *required*, and Svelte will print a warning during development if no value is provided, which you can squelch by specifying `undefined` as the default value:

`export let ``let foo: undefined`foo = `var undefined`undefined;## Component exports

An exported `const`, `class` or `function` declaration is *not* considered a prop — instead, it becomes part of the component's API:

```
<script>
	export function greet(name) {
		alert(`hello ${name}!`);
	}
</script>
```
```
<script lang="ts">
	export function greet(name) {
		alert(`hello ${name}!`);
	}
</script>
```
```
<script>
	import Greeter from './Greeter.svelte';
	let greeter;
</script>
<Greeter bind:this={greeter} />
<button on:click={() => greeter.greet('world')}>
	greet
</button>
```
```
<script lang="ts">
	import Greeter from './Greeter.svelte';
	let greeter;
</script>
<Greeter bind:this={greeter} />
<button on:click={() => greeter.greet('world')}>
	greet
</button>
```
## Renaming props

The `export` keyword can appear separately from the declaration. This is useful for renaming props, for example in the case of a reserved word:

```
<script>
	/** @type {string} */
	let className;
	// creates a `class` property, even
	// though it is a reserved word
	export { className as class };
</script>
```
```
<script lang="ts">
	let className: string;
	// creates a `class` property, even
	// though it is a reserved word
	export { className as class };
</script>
```
[ Edit this page on GitHub](https://github.com/sveltejs/svelte/edit/main/documentation/docs/99-legacy/03-legacy-export-let.md) [ llms.txt](/docs/svelte/legacy-export-let/llms.txt)

# Citations

1. Source page: https://svelte.dev/docs/svelte/legacy-export-let
