---
type: Web Page
title: await • Svelte Docs
description: await • Svelte documentation
resource: https://svelte.dev/docs/svelte/await-expressions
timestamp: '2026-07-07T10:59:37.245126+00:00'
---

# await

As of Svelte 5.36, you can use the `await` keyword inside your components in three places where it was previously unavailable:

- at the top level of your component's `<script>`
- inside `$derived(...)`declarations
- inside your markup

This feature is currently experimental, and you must opt in by adding the `experimental.async` option wherever you configure Svelte, usually `svelte.config.js`:

```
export default {
	
```
```
compilerOptions: {
    experimental: {
        async: boolean;
    };
}
```

```
experimental: {
    async: boolean;
}
```

`async: boolean`async: true
		}
	}
};The experimental flag will be removed in Svelte 6.

## Synchronized updates

When an `await` expression depends on a particular piece of state, changes to that state will not be reflected in the UI until the asynchronous work has completed, so that the UI is not left in an inconsistent state. In other words, in an example like this...

```
<script>
	let a = $state(1);
	let b = $state(2);
	async function add(a, b) {
		await new Promise((f) => setTimeout(f, 500)); // artificial delay
		return a + b;
	}
</script>
<input type="number" bind:value={a}>
<input type="number" bind:value={b}>
<p>{a} + {b} = {await add(a, b)}</p>
```
```
<script lang="ts">
	let a = $state(1);
	let b = $state(2);
	async function add(a, b) {
		await new Promise((f) => setTimeout(f, 500)); // artificial delay
		return a + b;
	}
</script>
<input type="number" bind:value={a}>
<input type="number" bind:value={b}>
<p>{a} + {b} = {await add(a, b)}</p>
```
...if you increment `a`, the contents of the `<p>` will *not* immediately update to read this —

`<p>2 + 2 = 3</p>`— instead, the text will update to `2 + 2 = 4` when `add(a, b)` resolves.

Updates can overlap — a fast update will be reflected in the UI while an earlier slow update is still ongoing.

## Concurrency

Svelte will do as much asynchronous work as it can in parallel. For example if you have two `await` expressions in your markup...

```
<p>{await one(x)}</p>
<p>{await two(y)}</p>
```
...both functions will run at the same time, as they are independent expressions, even though they are *visually* sequential.

This does not apply to sequential `await` expressions inside your `<script>` or inside async functions — these run like any other asynchronous JavaScript. An exception is that independent `$derived` expressions will update independently, even though they will run sequentially when they are first created:

```
// `b` will not be created until `a` has resolved,
// but once created they will update independently
// even if `x` and `y` update simultaneously
let 
```
`let a: number`a = ```
function $derived<number>(expression: number): number
namespace $derived
```

Declares derived state, i.e. one that depends on other state variables.
The expression inside `$derived(...)` should be free of side-effects.

Example:

`let double = $derived(count * 2);`

$derived(await `function one(x: number): Promise<number>`one(`let x: number`x));
let `let b: number`b = ```
function $derived<number>(expression: number): number
namespace $derived
```

Declares derived state, i.e. one that depends on other state variables.
The expression inside `$derived(...)` should be free of side-effects.

Example:

`let double = $derived(count * 2);`

$derived(await `function two(y: number): Promise<number>`two(`let y: number`y));If you write code like this, expect Svelte to give you an

`await_waterfall`warning

## Indicating loading states

To render placeholder UI, you can wrap content in a `<svelte:boundary>` with a `pending` snippet. This will be shown when the boundary is first created, but not for subsequent updates, which are globally coordinated.

After the contents of a boundary have resolved for the first time and have replaced the `pending` snippet, you can detect subsequent async work with `$effect.pending()`. This is what you would use to display a "we're asynchronously validating your input" spinner next to a form field, for example.

You can also use `settled()` to get a promise that resolves when the current update is complete:

`import { ``function tick(): Promise<void>`Returns a promise that resolves once any pending state changes have been applied.

tick, `function settled(): Promise<void>`Returns a promise that resolves once any state changes, and asynchronous work resulting from them,
have resolved and the DOM has been updated

settled } from 'svelte';
async function `function onclick(): Promise<void>`onclick() {
	`let updating: boolean`updating = true;
	// without this, the change to `updating` will be
	// grouped with the other changes, meaning it
	// won't be reflected in the UI
	await `function tick(): Promise<void>`Returns a promise that resolves once any pending state changes have been applied.

tick();
	`let color: string`color = 'octarine';
	`let answer: number`answer = 42;
	await `function settled(): Promise<void>`Returns a promise that resolves once any state changes, and asynchronous work resulting from them,
have resolved and the DOM has been updated

settled();
	// any updates affected by `color` or `answer`
	// have now been applied
	`let updating: boolean`updating = false;
}## Error handling

Errors in `await` expressions will bubble to the nearest error boundary.

## Server-side rendering

Svelte supports asynchronous server-side rendering (SSR) with the `render(...)` API. To use it, simply await the return value:

`import { ````
function render<Comp extends SvelteComponent<any> | Component<any>, Props extends ComponentProps<Comp> = ComponentProps<Comp>>(...args: {} extends Props ? [component: Comp extends SvelteComponent<any> ? ComponentType<Comp> : Comp, options?: {
    props?: Omit<Props, "$$slots" | "$$events">;
    context?: Map<any, any>;
    idPrefix?: string;
    csp?: Csp;
    transformError?: (error: unknown) => unknown | Promise<unknown>;
}] : [component: Comp extends SvelteComponent<any> ? ComponentType<Comp> : Comp, options: {
    props: Omit<Props, "$$slots" | "$$events">;
    context?: Map<any, any>;
    idPrefix?: string;
    csp?: Csp;
    transformError?: (error: unknown) => unknown | Promise<unknown>;
}]): RenderOutput
```

Only available on the server and when compiling with the `server` option.
Takes a component and returns an object with `body` and `head` properties on it, which you can use to populate the HTML when server-rendering your app.

render } from 'svelte/server';
import ```
type App = SvelteComponent<Record<string, any>, any, any>
const App: LegacyComponentType
```

`const head: string`HTML that goes into the `<head>`

head, `const body: string`HTML that goes somewhere into the `<body>`

body } = await ```
render<SvelteComponent<Record<string, any>, any, any>, Record<string, any>>(component: ComponentType<SvelteComponent<Record<string, any>, any, any>>, options?: {
    props?: Omit<Record<string, any>, "$$slots" | "$$events"> | undefined;
    context?: Map<any, any>;
    idPrefix?: string;
    csp?: Csp;
    transformError?: ((error: unknown) => unknown | Promise<unknown>) | undefined;
} | undefined): RenderOutput
```

Only available on the server and when compiling with the `server` option.
Takes a component and returns an object with `body` and `head` properties on it, which you can use to populate the HTML when server-rendering your app.

render(`const App: LegacyComponentType`App);If you're using a framework like SvelteKit, this is done on your behalf.

If a `<svelte:boundary>` with a `pending` snippet is encountered during SSR, that snippet will be rendered while the rest of the content is ignored. All `await` expressions encountered outside boundaries with `pending` snippets will resolve and render their contents prior to `await render(...)` returning.

In the future, we plan to add a streaming implementation that renders the content in the background.

## Forking

The `fork(...)` API, added in 5.42, makes it possible to run `await` expressions that you *expect* to happen in the near future. This is mainly intended for frameworks like SvelteKit to implement preloading when (for example) users signal an intent to navigate.

```
<script>
	import { fork } from 'svelte';
	import Menu from './Menu.svelte';
	let open = $state(false);
	/** @type {import('svelte').Fork | null} */
	let pending = null;
	function preload() {
		pending ??= fork(() => {
			open = true;
		});
	}
	function discard() {
		pending?.discard();
		pending = null;
	}
</script>
<button
	onfocusin={preload}
	onfocusout={discard}
	onpointerenter={preload}
	onpointerleave={discard}
	onclick={() => {
		pending?.commit();
		pending = null;
		// in case `pending` didn't exist
		// (if it did, this is a no-op)
		open = true;
	}}
>open menu</button>
{#if open}
	<!-- any async work inside this component will start
	     as soon as the fork is created -->
	<Menu onclose={() => open = false} />
{/if}
```
## Caveats

As an experimental feature, the details of how `await` is handled (and related APIs like `$effect.pending()`) are subject to breaking changes outside of a semver major release, though we intend to keep such changes to a bare minimum.

## Breaking changes

Effects run in a slightly different order when the `experimental.async` option is `true`. Specifically, *block* effects like `{#if ...}` and `{#each ...}` now run before an `$effect.pre` or `beforeUpdate` in the same component, which means that in very rare situations it is possible to update a block that should no longer exist, but only if you update state inside an effect, which you should avoid.

Edit this page on GitHub llms.txt

# Citations

1. Source page: https://svelte.dev/docs/svelte/await-expressions
