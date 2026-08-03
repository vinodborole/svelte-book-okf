---
type: Web Page
title: '{let/const ...} • Svelte Docs'
description: '{let/const ...} • Svelte documentation'
resource: https://svelte.dev/docs/svelte/declaration-tags
timestamp: '2026-08-03T08:54:23.898986+00:00'
---

# {let/const ...} 

 Declaration tags define local variables inside markup with `const` or `let`:

```
<script>
	let boxes = [{ width: 10, height: 10 }, { width: 15, height: 15 }];
</script>
{#each boxes as box}
	{const area = box.width * box.height}
	{const label = `${box.width} ⨉ ${box.height} = ${area}`}
	<p>{label}</p>
{/each}
```
```
<script lang="ts">
	let boxes = [{ width: 10, height: 10 }, { width: 15, height: 15 }];
</script>
{#each boxes as box}
	{const area = box.width * box.height}
	{const label = `${box.width} ⨉ ${box.height} = ${area}`}
	<p>{label}</p>
{/each}
```
Declaration tags are available since Svelte 5.56.

 The [`{@const ...}`](@const) syntax is considered legacy — use declaration tags instead.

When values should be reactive, you can use `$state` and `$derived`:

```
<script>
	let user = $state({ name: 'Svelte' });
	let editing = $state(false);
</script>
<p>Hello {user.name}</p>
<button onclick={() => editing = true}>edit name</button>
{#if editing}
	{let name = $state(user.name)}
	{const greeting = $derived(`Hello ${name}`)}
	<hr>
	<input bind:value={name} />
	<p>{greeting}</p>
	<button onclick={() => {
		user.name = name;
		editing = false;
	}}>save</button>
{/if}
```
```
<script lang="ts">
	let user = $state({ name: 'Svelte' });
	let editing = $state(false);
</script>
<p>Hello {user.name}</p>
<button onclick={() => editing = true}>edit name</button>
{#if editing}
	{let name = $state(user.name)}
	{const greeting = $derived(`Hello ${name}`)}
	<hr>
	<input bind:value={name} />
	<p>{greeting}</p>
	<button onclick={() => {
		user.name = name;
		editing = false;
	}}>save</button>
{/if}
```
Declaration tags can be used anywhere inside the component. They can reference values declared outside themselves (for example in the `<script>` tag or in `{#each ...}` blocks) and are 'visible' to everything in the same lexical scope (i.e. siblings, and children of those siblings):

```
{const hello = 'hello'}
{hello} <!-- 'hello' -->
<div>
	{const hello = 'hi'}
	{hello} <!-- 'hi' -->
	<div>
		{hello} <!-- 'hi' -->
	</div>
</div>
{hello} <!-- 'hello' -->
```
 [Edit this page on GitHub](https://github.com/sveltejs/svelte/edit/main/documentation/docs/03-template-syntax/11-declaration-tags.md)  [llms.txt](/docs/svelte/declaration-tags/llms.txt)

previous next

# Citations

1. Source page: https://svelte.dev/docs/svelte/declaration-tags
