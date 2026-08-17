---
type: Web Page
title: Imperative component API • Svelte Docs
description: Imperative component API • Svelte documentation
resource: https://svelte.dev/docs/svelte/imperative-component-api
timestamp: '2026-08-17T06:25:40.913234+00:00'
---

# Imperative component API

Every Svelte application starts by imperatively creating a root component. On the client this component is mounted to a specific element. On the server, you want to get back a string of HTML instead which you can render. The following functions help you achieve those tasks.

## mount

Instantiates a component and mounts it to the given target:

`import {` `function mount<Props extends Record<string, any>, Exports extends Record<string, any>>(component: ComponentType<SvelteComponent<Props>> | Component<Props, Exports, any>, options: MountOptions<Props>): Exports`
Mounts a component to the given target and returns the exports and potentially the props (if compiled with `accessors: true`) of the component.
Transitions will play during the initial render unless the `intro` option is set to `false`.

mount } from 'svelte';
import ```
type App = SvelteComponent<Record<string, any>, any, any>
const App: LegacyComponentType
```

```
const app: {
    $on?(type: string, callback: (e: any) => void): () => void;
    $set?(props: Partial<Record<string, any>>): void;
} & Record<string, any>
```

```
mount<Record<string, any>, {
    $on?(type: string, callback: (e: any) => void): () => void;
    $set?(props: Partial<Record<string, any>>): void;
} & Record<string, any>>(component: ComponentType<SvelteComponent<Record<string, any>, any, any>> | Component<Record<string, any>, {
    $on?(type: string, callback: (e: any) => void): () => void;
    $set?(props: Partial<Record<string, any>>): void;
} & Record<string, any>, any>, options: MountOptions<...>): {
    $on?(type: string, callback: (e: any) => void): () => void;
    $set?(props: Partial<Record<string, any>>): void;
} & Record<...>
```

Mounts a component to the given target and returns the exports and potentially the props (if compiled with `accessors: true`) of the component.
Transitions will play during the initial render unless the `intro` option is set to `false`.

mount(`const App: LegacyComponentType`App, {
	`target: Document | Element | ShadowRoot`
Target element where the component will be mounted.

target: `var document: Document`
**`window.document`** returns a reference to the document contained in the window.

document.`ParentNode.querySelector<Element>(selectors: string): Element | null (+4 overloads)`
Returns the first element that is a descendant of node that matches selectors.

querySelector('#app'),
	`props?: Record<string, any> | undefined`
Component properties.

props: { `some: string`some: 'property' }
});
You can mount multiple components per page, and you can also mount from within your application, for example when creating a tooltip component and attaching it to the hovered element.

Note that unlike calling `new App(...)` in Svelte 4, things like effects (including `onMount` callbacks, and action functions) will not run during `mount`. If you need to force pending effects to run (in the context of a test, for example) you can do so with `flushSync()`.

## unmount

Unmounts a component that was previously created with [`mount`](#mount) or [`hydrate`](#hydrate).

If `options.outro` is `true`, [transitions](transition) will play before the component is removed from the DOM:

`import {` `function mount<Props extends Record<string, any>, Exports extends Record<string, any>>(component: ComponentType<SvelteComponent<Props>> | Component<Props, Exports, any>, options: MountOptions<Props>): Exports`
Mounts a component to the given target and returns the exports and potentially the props (if compiled with `accessors: true`) of the component.
Transitions will play during the initial render unless the `intro` option is set to `false`.

mount, ```
function unmount(component: Record<string, any>, options?: {
    outro?: boolean;
} | undefined): Promise<void>
```

Unmounts a component that was previously mounted using `mount` or `hydrate`.

Since 5.13.0, if `options.outro` is `true`, [transitions](https://svelte.dev/docs/svelte/transition) will play before the component is removed from the DOM.

Returns a `Promise` that resolves after transitions have completed if `options.outro` is true, or immediately otherwise (prior to 5.13.0, returns `void`).

```
import { mount, unmount } from 'svelte';
import App from './App.svelte';
const app = mount(App, { target: document.body });
// later...
unmount(app, { outro: true });
```

unmount } from 'svelte';
import ```
type App = SvelteComponent<Record<string, any>, any, any>
const App: LegacyComponentType
```

```
const app: {
    $on?(type: string, callback: (e: any) => void): () => void;
    $set?(props: Partial<Record<string, any>>): void;
} & Record<string, any>
```

```
mount<Record<string, any>, {
    $on?(type: string, callback: (e: any) => void): () => void;
    $set?(props: Partial<Record<string, any>>): void;
} & Record<string, any>>(component: ComponentType<SvelteComponent<Record<string, any>, any, any>> | Component<Record<string, any>, {
    $on?(type: string, callback: (e: any) => void): () => void;
    $set?(props: Partial<Record<string, any>>): void;
} & Record<string, any>, any>, options: MountOptions<...>): {
    $on?(type: string, callback: (e: any) => void): () => void;
    $set?(props: Partial<Record<string, any>>): void;
} & Record<...>
```

Mounts a component to the given target and returns the exports and potentially the props (if compiled with `accessors: true`) of the component.
Transitions will play during the initial render unless the `intro` option is set to `false`.

mount(`const App: LegacyComponentType`App, { `target: Document | Element | ShadowRoot`
Target element where the component will be mounted.

target: `var document: Document`
**`window.document`** returns a reference to the document contained in the window.

document.`Document.body: HTMLElement`
The **`Document.body`** property represents the 

 or body });
// later
```
function unmount(component: Record<string, any>, options?: {
    outro?: boolean;
} | undefined): Promise<void>
```

Unmounts a component that was previously mounted using `mount` or `hydrate`.

Since 5.13.0, if `options.outro` is `true`, [transitions](https://svelte.dev/docs/svelte/transition) will play before the component is removed from the DOM.

Returns a `Promise` that resolves after transitions have completed if `options.outro` is true, or immediately otherwise (prior to 5.13.0, returns `void`).

```
import { mount, unmount } from 'svelte';
import App from './App.svelte';
const app = mount(App, { target: document.body });
// later...
unmount(app, { outro: true });
```

unmount(
```
const app: {
    $on?(type: string, callback: (e: any) => void): () => void;
    $set?(props: Partial<Record<string, any>>): void;
} & Record<string, any>
```

`outro?: boolean | undefined`outro: true });
Returns a `Promise` that resolves after transitions have completed if `options.outro` is true, or immediately otherwise.

## render

Only available on the server and when compiling with the `server` option. Takes a component and returns an object with `body` and `head` properties on it, which you can use to populate the HTML when server-rendering your app:

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
import ```
type App = SvelteComponent<Record<string, any>, any, any>
const App: LegacyComponentType
```

`const result: RenderOutput`result = ```
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

render(`const App: LegacyComponentType`App, {
	`props?: Omit<Record<string, any>, "$$slots" | "$$events"> | undefined`props: { `some: string`some: 'property' }
});
`const result: RenderOutput`result.`SyncRenderOutput.body: string`
HTML that goes somewhere into the `<body>`

body; // HTML for somewhere in this <body> tag
`const result: RenderOutput`result.`SyncRenderOutput.head: string`
HTML that goes into the `<head>`

head; // HTML for somewhere in this <head> tag
## hydrate

Like `mount`, but will reuse up any HTML rendered by Svelte’s SSR output (from the [`render`](#render) function) inside the target and make it interactive:

`import {` ```
function hydrate<Props extends Record<string, any>, Exports extends Record<string, any>>(component: ComponentType<SvelteComponent<Props>> | Component<Props, Exports, any>, options: {} extends Props ? {
    target: Document | Element | ShadowRoot;
    props?: Props;
    events?: Record<string, (e: any) => any>;
    context?: Map<any, any>;
    intro?: boolean;
    recover?: boolean;
    transformError?: (error: unknown) => unknown;
} : {
    target: Document | Element | ShadowRoot;
    props: Props;
    events?: Record<string, (e: any) => any>;
    context?: Map<any, any>;
    intro?: boolean;
    recover?: boolean;
    transformError?: (error: unknown) => unknown;
}): Exports
```

Hydrates a component on the given target and returns the exports and potentially the props (if compiled with `accessors: true`) of the component

hydrate } from 'svelte';
import ```
type App = SvelteComponent<Record<string, any>, any, any>
const App: LegacyComponentType
```

```
const app: {
    $on?(type: string, callback: (e: any) => void): () => void;
    $set?(props: Partial<Record<string, any>>): void;
} & Record<string, any>
```

```
hydrate<Record<string, any>, {
    $on?(type: string, callback: (e: any) => void): () => void;
    $set?(props: Partial<Record<string, any>>): void;
} & Record<string, any>>(component: ComponentType<SvelteComponent<Record<string, any>, any, any>> | Component<Record<string, any>, {
    $on?(type: string, callback: (e: any) => void): () => void;
    $set?(props: Partial<Record<string, any>>): void;
} & Record<string, any>, any>, options: {
    ...;
}): {
    $on?(type: string, callback: (e: any) => void): () => void;
    $set?(props: Partial<Record<string, any>>): void;
} & Record<...>
```

Hydrates a component on the given target and returns the exports and potentially the props (if compiled with `accessors: true`) of the component

hydrate(`const App: LegacyComponentType`App, {
	`target: Document | Element | ShadowRoot`target: `var document: Document`
**`window.document`** returns a reference to the document contained in the window.

document.`ParentNode.querySelector<Element>(selectors: string): Element | null (+4 overloads)`
Returns the first element that is a descendant of node that matches selectors.

querySelector('#app'),
	`props?: Record<string, any> | undefined`props: { `some: string`some: 'property' }
});
As with `mount`, effects will not run during `hydrate` — use `flushSync()` immediately afterwards if you need them to.

 [Edit this page on GitHub](https://github.com/sveltejs/svelte/edit/main/documentation/docs/06-runtime/04-imperative-component-api.md)  [llms.txt](/docs/svelte/imperative-component-api/llms.txt)

# Citations

1. Source page: https://svelte.dev/docs/svelte/imperative-component-api
