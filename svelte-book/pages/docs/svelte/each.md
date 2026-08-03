---
type: Web Page
title: '{#each ...} • Svelte Docs'
description: '{#each ...} • Svelte documentation'
resource: https://svelte.dev/docs/svelte/each
timestamp: '2026-08-03T08:54:23.898986+00:00'
---

# {#each ...}

`{#each expression as name}...{/each}``{#each expression as name, index}...{/each}`
Iterating over values can be done with an each block. The values in question can be arrays, array-like objects (i.e. anything with a `length` property), or iterables like `Map` and `Set`. (Internally, they are converted to arrays with [`Array.from`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/from).)

If the value is `null` or `undefined`, it is treated the same as an empty array (which will cause [else blocks](#Else-blocks) to be rendered, where applicable).

```
<h1>Shopping list</h1>
<ul>
	{#each items as item}
		<li>{item.name} x {item.qty}</li>
	{/each}
</ul>
```
An each block can also specify an *index*, equivalent to the second argument in an `array.map(...)` callback:

```
{#each items as item, i}
	<li>{i + 1}: {item.name} x {item.qty}</li>
{/each}
```
## Keyed each blocks

`{#each expression as name (key)}...{/each}``{#each expression as name, index (key)}...{/each}`
If a *key* expression is provided — which must uniquely identify each list item — Svelte will use it to intelligently update the list when data changes by inserting, moving and deleting items, rather than adding or removing items at the end and updating the state in the middle.

The key can be any object, but strings and numbers are recommended since they allow identity to persist when the objects themselves change.

```
{#each items as item (item.id)}
	<li>{item.name} x {item.qty}</li>
{/each}
<!-- or with additional index value -->
{#each items as item, i (item.id)}
	<li>{i + 1}: {item.name} x {item.qty}</li>
{/each}
```
You can freely use destructuring and rest patterns in each blocks.

```
{#each items as { id, name, qty }, i (id)}
	<li>{i + 1}: {name} x {qty}</li>
{/each}
{#each objects as { id, ...rest }}
	<li><span>{id}</span><MyComponent {...rest} /></li>
{/each}
{#each items as [id, ...rest]}
	<li><span>{id}</span><MyComponent values={rest} /></li>
{/each}
```
## Each blocks without an item

`{#each expression}...{/each}``{#each expression, index}...{/each}`
In case you just want to render something `n` times, you can omit the `as` part:

```
<div class="chess-board">
	{#each { length: 8 }, rank}
		{#each { length: 8 }, file}
			<div class:black={(rank + file) % 2 === 1}></div>
		{/each}
	{/each}
</div>
<style>
	.chess-board {
		display: grid;
		grid-template-columns: repeat(8, 1fr);
		grid-template-rows: repeat(8, 1fr);
		border: 1px solid black;
		aspect-ratio: 1;
		.black {
			background: black;
		}
	}
</style>
```
## Else blocks

`{#each expression as name}...{:else}...{/each}`
An each block can also have an `{:else}` clause, which is rendered if the list is empty.

```
{#each todos as todo}
	<p>{todo.text}</p>
{:else}
	<p>No tasks today!</p>
{/each}
```
 [Edit this page on GitHub](https://github.com/sveltejs/svelte/edit/main/documentation/docs/03-template-syntax/03-each.md)  [llms.txt](/docs/svelte/each/llms.txt)

# Citations

1. Source page: https://svelte.dev/docs/svelte/each
