---
type: Web Page
title: '{#snippet ...} • Svelte Docs'
description: '{#snippet ...} • Svelte documentation'
resource: https://svelte.dev/docs/svelte/snippet
timestamp: '2026-08-17T06:25:40.913234+00:00'
---

# {#snippet ...}

`{#snippet name()}...{/snippet}``{#snippet name(param1, param2, paramN)}...{/snippet}`
Snippets, and [render tags](@render), are a way to create reusable chunks of markup inside your components. Instead of writing duplicative code like [this](/playground/untitled#H4sIAAAAAAAAE5VUYW-kIBD9K8Tmsm2yXXRzvQ-s3eR-R-0HqqOQKhAZb9sz_vdDkV1t000vRmHewMx7w2AflbIGG7GnPlK8gYhFv42JthG-m9Gwf6BGcLbVXZuPSGrzVho8ZirDGpDIhldgySN5GpEMez9kaNuckY1ANJZRamRuu2ZnhEZt6a84pvs43mzD4pMsUDDi8DMkQFYCGdkvsJwblFq5uCik9bmJ4JZwUkv1eoknWigX2eGNN6aGXa6bjV8ybP-X7sM36T58SVcrIIV2xVIaA41xeD5kKqWXuqpUJEefOqVuOkL9DfBchGrzWfu0vb-RpTd3o-zBR045Ga3HfuE5BmJpKauuhbPtENlUF2sqR9jqpsPSxWsMrlngyj3VJiyYjJXb1-lMa7IWC-iSk2M5Zzh-SJjShe-siq5kpZRPs55BbSGU5YPyte4vVV_VfFXxVb10dSLf17pS2lM5HnpPxw4Zpv6x-F57p0jI3OKlVnhv5V9wPQrNYQQ9D_f6aGHlC89fq1Z3qmDkJCTCweOGF4VUFSPJvD_DhreVdA0eu8ehJJ5x91dBaBkpWm3ureCFPt3uzRv56d4kdp-2euG38XZ6dsnd3ZmPG9yRBCrzRUvi-MccOdwz3qE-fOZ7AwAhlrtTUx3c76vRhSwlFBHDtoPhefgHX3dM0PkEAAA=)...

```
{#each images as image}
	{#if image.href}
		<a href={image.href}>
			<figure>
				<img src={image.src} alt={image.caption} width={image.width} height={image.height} />
				<figcaption>{image.caption}</figcaption>
			</figure>
		</a>
	{:else}
		<figure>
			<img src={image.src} alt={image.caption} width={image.width} height={image.height} />
			<figcaption>{image.caption}</figcaption>
		</figure>
	{/if}
{/each}
```
...you can write [this](/playground/untitled#H4sIAAAAAAAAE5VUYW-bMBD9KxbRlERKY4jWfSA02n5H6QcXDmwVbMs-lnaI_z6D7TTt1moTAnPvzvfenQ_GpBEd2CS_HxPJekjy5IfWyS7BFz0b9id0CM62ajDVjBS2MkLjqZQldoBE9KwFS-7I_YyUOPqlRGuqnKw5orY5pVpUduj3mitUln5LU3pI0_UuBp9FjTwnDr9AHETLMSeHK6xiGoWSLi9yYT034cwSRjohn17zcQPNFTs8s153sK9Uv_Yh0-5_5d7-o9zbD-UqCaRWrllSYZQxLw_HUhb0ta-y4NnJUxfUvc7QuLJSaO0a3oh2MLBZat8u-wsPnXzKQvTtVVF34xK5d69ThFmHEQ4SpzeVRediTG8rjD5vBSeN3E5JyHh6R1DQK9-iml5kjzQUN_lSgVU8DhYLx7wwjSvRkMDvTjiwF4zM1kXZ7DlF1eN3A7IG85e-zRrYEjjm0FkI4Cc7Ripm0pHOChexhcWXzreeZyRMU6Mk3ljxC9w4QH-cQZ_b3T5pjHxk1VNr1CDrnJy5QDh6XLO6FrLNSRb2l9gz0wo3S6m7HErSgLsPGMHkpDZK31jOanXeHPQz-eruLHUP0z6yTbpbrn223V70uMXNSpQSZjpL0y8hcxxpNqA6_ql3BQAxlxvfpQ_uT9GrWjQC6iRHM8D0MP0GQsIi92QEAAA=):

```
{#snippet figure(image)}
	<figure>
		<img src={image.src} alt={image.caption} width={image.width} height={image.height} />
		<figcaption>{image.caption}</figcaption>
	</figure>
{/snippet}
{#each images as image}
	{#if image.href}
		<a href={image.href}>
			{@render figure(image)}
		</a>
	{:else}
		{@render figure(image)}
	{/if}
{/each}
```
Like function declarations, snippets can have an arbitrary number of parameters, which can have default values, and you can destructure each parameter. You cannot use rest parameters, however.

## Snippet scope

Snippets can be declared anywhere inside your component. They can reference values declared outside themselves, for example in the `<script>` tag or in `{#each ...}` blocks...

```
<script>
	let { message = `it's great to see you!` } = $props();
</script>
{#snippet hello(name)}
	<p>hello {name}! {message}!</p>
{/snippet}
{@render hello('alice')}
{@render hello('bob')}
```
```
<script lang="ts">
	let { message = `it's great to see you!` } = $props();
</script>
{#snippet hello(name)}
	<p>hello {name}! {message}!</p>
{/snippet}
{@render hello('alice')}
{@render hello('bob')}
```
...and they are ‘visible’ to everything in the same lexical scope (i.e. siblings, and children of those siblings):

```
<div>
	{#snippet x()}
		{#snippet y()}...{/snippet}
		<!-- this is fine -->
		{@render y()}
	{/snippet}
	<!-- this will error, as `y` is not in scope -->
	{@render y()}
</div>
<!-- this will also error, as `x` is not in scope -->
{@render x()}
```
Snippets can reference themselves and each other:

```
{#snippet blastoff()}
	<span>🚀</span>
{/snippet}
{#snippet countdown(n)}
	{#if n > 0}
		<span>{n}...</span>
		{@render countdown(n - 1)}
	{:else}
		{@render blastoff()}
	{/if}
{/snippet}
{@render countdown(10)}
```
## Passing snippets to components

### Explicit props

Within the template, snippets are values just like any other. As such, they can be passed to components as props:

```
<script>
	import Table from './Table.svelte';
	const fruits = [
		{ name: 'apples', qty: 5, price: 2 },
		{ name: 'bananas', qty: 10, price: 1 },
		{ name: 'cherries', qty: 20, price: 0.5 }
	];
</script>
{#snippet header()}
	<th>fruit</th>
	<th>qty</th>
	<th>price</th>
	<th>total</th>
{/snippet}
{#snippet row(d)}
	<td>{d.name}</td>
	<td>{d.qty}</td>
	<td>{d.price}</td>
	<td>{d.qty * d.price}</td>
{/snippet}
<Table data={fruits} {header} {row} />
```
```
<script lang="ts">
	import Table from './Table.svelte';
	const fruits = [
		{ name: 'apples', qty: 5, price: 2 },
		{ name: 'bananas', qty: 10, price: 1 },
		{ name: 'cherries', qty: 20, price: 0.5 }
	];
</script>
{#snippet header()}
	<th>fruit</th>
	<th>qty</th>
	<th>price</th>
	<th>total</th>
{/snippet}
{#snippet row(d)}
	<td>{d.name}</td>
	<td>{d.qty}</td>
	<td>{d.price}</td>
	<td>{d.qty * d.price}</td>
{/snippet}
<Table data={fruits} {header} {row} />
```
```
<script>
	let { data, header, row } = $props();
</script>
<table>
	{#if header}
		<thead>
			<tr>{@render header()}</tr>
		</thead>
	{/if}
	<tbody>
		{#each data as d}
			<tr>{@render row(d)}</tr>
		{/each}
	</tbody>
</table>
<style>
	table {
		text-align: left;
		border-spacing: 0;
	}
	tbody tr:nth-child(2n+1) {
		background: ButtonFace;
	}
	table :global(th), table :global(td) {
		padding: 0.5em;
	}
</style>
```
```
<script lang="ts">
	let { data, header, row } = $props();
</script>
<table>
	{#if header}
		<thead>
			<tr>{@render header()}</tr>
		</thead>
	{/if}
	<tbody>
		{#each data as d}
			<tr>{@render row(d)}</tr>
		{/each}
	</tbody>
</table>
<style>
	table {
		text-align: left;
		border-spacing: 0;
	}
	tbody tr:nth-child(2n+1) {
		background: ButtonFace;
	}
	table :global(th), table :global(td) {
		padding: 0.5em;
	}
</style>
```
Think about it like passing content instead of data to a component. The concept is similar to slots in web components.

### Implicit props

As an authoring convenience, snippets declared directly *inside* a component implicitly become props *on* the component:

```
<script>
	import Table from './Table.svelte';
	const fruits = [
		{ name: 'apples', qty: 5, price: 2 },
		{ name: 'bananas', qty: 10, price: 1 },
		{ name: 'cherries', qty: 20, price: 0.5 }
	];
</script>
<Table data={fruits}>
	{#snippet header()}
		<th>fruit</th>
		<th>qty</th>
		<th>price</th>
		<th>total</th>
	{/snippet}
	{#snippet row(d)}
		<td>{d.name}</td>
		<td>{d.qty}</td>
		<td>{d.price}</td>
		<td>{d.qty * d.price}</td>
	{/snippet}
</Table>
```
```
<script lang="ts">
	import Table from './Table.svelte';
	const fruits = [
		{ name: 'apples', qty: 5, price: 2 },
		{ name: 'bananas', qty: 10, price: 1 },
		{ name: 'cherries', qty: 20, price: 0.5 }
	];
</script>
<Table data={fruits}>
	{#snippet header()}
		<th>fruit</th>
		<th>qty</th>
		<th>price</th>
		<th>total</th>
	{/snippet}
	{#snippet row(d)}
		<td>{d.name}</td>
		<td>{d.qty}</td>
		<td>{d.price}</td>
		<td>{d.qty * d.price}</td>
	{/snippet}
</Table>
```
```
<script>
	let { data, header, row } = $props();
</script>
<table>
	{#if header}
		<thead>
			<tr>{@render header()}</tr>
		</thead>
	{/if}
	<tbody>
		{#each data as d}
			<tr>{@render row(d)}</tr>
		{/each}
	</tbody>
</table>
<style>
	table {
		text-align: left;
		border-spacing: 0;
	}
	tbody tr:nth-child(2n+1) {
		background: ButtonFace;
	}
	table :global(th), table :global(td) {
		padding: 0.5em;
	}
</style>
```
```
<script lang="ts">
	let { data, header, row } = $props();
</script>
<table>
	{#if header}
		<thead>
			<tr>{@render header()}</tr>
		</thead>
	{/if}
	<tbody>
		{#each data as d}
			<tr>{@render row(d)}</tr>
		{/each}
	</tbody>
</table>
<style>
	table {
		text-align: left;
		border-spacing: 0;
	}
	tbody tr:nth-child(2n+1) {
		background: ButtonFace;
	}
	table :global(th), table :global(td) {
		padding: 0.5em;
	}
</style>
```
### Implicit children snippet

Any content inside the component tags that is *not* a snippet declaration implicitly becomes part of the `children` snippet:

```
<script>
	import Button from './Button.svelte';
</script>
<Button>click me</Button>
```
```
<script lang="ts">
	import Button from './Button.svelte';
</script>
<Button>click me</Button>
```
```
<script>
	let { children } = $props();
</script>
<!-- result will be <button>click me</button> -->
<button>{@render children()}</button>
```
```
<script lang="ts">
	let { children } = $props();
</script>
<!-- result will be <button>click me</button> -->
<button>{@render children()}</button>
```
 Note that you cannot have a prop called `children` if you also have content inside the component — for this reason, you should avoid having props with that name

### Optional snippet props

You can declare snippet props as being optional. You can either use optional chaining to not render anything if the snippet isn’t set...

```
<script>
	let { children } = $props();
</script>
{@render children?.()}
```
...or use an `#if` block to render fallback content:

```
<script>
	let { children } = $props();
</script>
{#if children}
	{@render children()}
{:else}
	fallback content
{/if}
```
## Typing snippets

Snippets implement the `Snippet` interface imported from `'svelte'`:

```
<script lang="ts">
	import type { Snippet } from 'svelte';
	interface Props {
		data: any[];
		children: Snippet;
		row: Snippet<[any]>;
	}
	let { data, children, row }: Props = $props();
</script>
```
With this change, red squigglies will appear if you try and use the component without providing a `data` prop and a `row` snippet. Notice that the type argument provided to `Snippet` is a tuple, since snippets can have multiple parameters.

We can tighten things up further by declaring a generic, so that `data` and `row` refer to the same type:

```
<script lang="ts" generics="T">
	import type { Snippet } from 'svelte';
	let {
		data,
		children,
		row
	}: {
		data: T[];
		children: Snippet;
		row: Snippet<[T]>;
	} = $props();
</script>
```
## Exporting snippets

Snippets declared at the top level of a `.svelte` file can be exported from a `<script module>` for use in other components, provided they don’t reference any declarations in a non-module `<script>` (whether directly or indirectly, via other snippets):

```
<script>
	import { add } from './snippets.svelte';
</script>
{@render add(1, 2)}
```
```
<script lang="ts">
	import { add } from './snippets.svelte';
</script>
{@render add(1, 2)}
```
```
<script module>
	export { add };
</script>
{#snippet add(a, b)}
	{a} + {b} = {a + b}
{/snippet}
```
This requires Svelte 5.5.0 or newer

## Programmatic snippets

Snippets can be created programmatically with the [`createRawSnippet`](svelte#createRawSnippet) API. This is intended for advanced use cases.

## Snippets and slots

In Svelte 4, content can be passed to components using [slots](legacy-slots). Snippets are more powerful and flexible, and so slots have been deprecated in Svelte 5.

 [Edit this page on GitHub](https://github.com/sveltejs/svelte/edit/main/documentation/docs/03-template-syntax/06-snippet.md)  [llms.txt](/docs/svelte/snippet/llms.txt)

# Citations

1. Source page: https://svelte.dev/docs/svelte/snippet
