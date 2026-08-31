---
type: Web Page
title: svelte/server • Svelte Docs
description: svelte/server • Svelte documentation
resource: https://svelte.dev/docs/svelte/svelte-server
timestamp: '2026-08-31T11:55:22.502440+00:00'
---

# svelte/server 

 `import {` ```
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
## render

Only available on the server and when compiling with the `server` option.
Takes a component and returns an object with `body` and `head` properties on it, which you can use to populate the HTML when server-rendering your app.

```
function render<
	Comp extends SvelteComponent<any> | Component<any>,
	Props extends ComponentProps<Comp> = ComponentProps<Comp>
>(
	...args: {} extends Props
		? [
				component: Comp extends SvelteComponent<any>
					? ComponentType<Comp>
					: Comp,
				options?: {
					props?: Omit<Props, '$$slots' | '$$events'>;
					context?: Map<any, any>;
					idPrefix?: string;
					csp?: Csp;
					transformError?: (
						error: unknown
					) => unknown | Promise<unknown>;
				}
			]
		: [
				component: Comp extends SvelteComponent<any>
					? ComponentType<Comp>
					: Comp,
				options: {
					props: Omit<Props, '$$slots' | '$$events'>;
					context?: Map<any, any>;
					idPrefix?: string;
					csp?: Csp;
					transformError?: (
						error: unknown
					) => unknown | Promise<unknown>;
				}
			]
): RenderOutput;
```
## Csp

`type Csp = { nonce?: string; hash?: boolean };`
## RenderOutput

```
type RenderOutput = SyncRenderOutput &
	PromiseLike<SyncRenderOutput>;
```
## Sha256Source

``type Sha256Source = `sha256-${string}`;``
## SyncRenderOutput

`interface SyncRenderOutput {…}``head: string;`
HTML that goes into the `<head>`

`html: string;`
- deprecated use `body` instead

`body: string;`
HTML that goes somewhere into the `<body>`

```
hashes: {
	script: Sha256Source[];
};
```
 [Edit this page on GitHub](https://github.com/sveltejs/svelte/edit/main/documentation/docs/98-reference/21-svelte-server.md)  [llms.txt](/docs/svelte/svelte-server/llms.txt)

previous next

# Citations

1. Source page: https://svelte.dev/docs/svelte/svelte-server
