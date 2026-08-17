---
type: Web Page
title: Context • Svelte Docs
description: Context • Svelte documentation
resource: https://svelte.dev/docs/svelte/context
timestamp: '2026-08-17T06:25:40.913234+00:00'
---

# Context

Context allows components to access values owned by parent components without passing them down as props (potentially through many layers of intermediate components, known as ‘prop-drilling’).

By creating a `[get, set]` pair of functions with `createContext`, you can set the context in a parent component and get it in a child component:

```
<script>
	import Parent from './Parent.svelte';
	import Child from './Child.svelte';
</script>
<Parent>
	<Child />
</Parent>
```
```
<script lang="ts">
	import Parent from './Parent.svelte';
	import Child from './Child.svelte';
</script>
<Parent>
	<Child />
</Parent>
```
```
<script>
	import { setUserContext } from './context';
	let { children } = $props();
	setUserContext({ name: 'world' });
</script>
{@render children()}
```
```
<script lang="ts">
	import { setUserContext } from './context';
	let { children } = $props();
	setUserContext({ name: 'world' });
</script>
{@render children()}
```
```
<script>
	import { getUserContext } from './context';
	const user = getUserContext();
</script>
<h1>hello {user.name}, inside Child.svelte</h1>
```
```
<script lang="ts">
	import { getUserContext } from './context';
	const user = getUserContext();
</script>
<h1>hello {user.name}, inside Child.svelte</h1>
```
`import {` `function createContext<T>(): [() => T, (context: T) => T]`
Returns a `[get, set]` pair of functions for working with context in a type-safe way.

`get` will throw an error if no parent component called `set`.

createContext } from 'svelte';
interface User {
	`User.name: string`name: string;
}
export const [`const getUserContext: () => User`getUserContext, `const setUserContext: (context: User) => User`setUserContext] = `createContext<User>(): [() => User, (context: User) => User]`
Returns a `[get, set]` pair of functions for working with context in a type-safe way.

`get` will throw an error if no parent component called `set`.

createContext<User>();
 `createContext` was added in version 5.40. If you are using an earlier version of Svelte, you must use `setContext` and `getContext` instead.

This is particularly useful when `Parent.svelte` is not directly aware of `Child.svelte`, but instead renders it as part of a `children` [snippet](snippet) as shown above.

## setContext and getContext

As an alternative to `createContext`, you can use `setContext` and `getContext` directly. The parent component sets context with `setContext(key, value)`...

```
<script>
	import { setContext } from 'svelte';
	setContext('my-context', 'hello from Parent.svelte');
</script>
```
```
<script lang="ts">
	import { setContext } from 'svelte';
	setContext('my-context', 'hello from Parent.svelte');
</script>
```
...and the child retrieves it with `getContext`:

```
<script>
	import { getContext } from 'svelte';
	const message = getContext('my-context');
</script>
<h1>{message}, inside Child.svelte</h1>
```
```
<script lang="ts">
	import { getContext } from 'svelte';
	const message = getContext('my-context');
</script>
<h1>{message}, inside Child.svelte</h1>
```
The key (`'my-context'`, in the example above) and the context itself can be any JavaScript value.

 `createContext` is preferred since it provides better type safety and makes it unnecessary to use keys.

In addition to [`setContext`](svelte#setContext) and [`getContext`](svelte#getContext), Svelte exposes [`hasContext`](svelte#hasContext) and [`getAllContexts`](svelte#getAllContexts) functions.

## Using context with state

You can store reactive state in context...

```
<script>
	import { setCounter } from './context.ts';
	import Child from './Child.svelte';
	let counter = $state({
		count: 0
	});
	setCounter(counter);
</script>
<button onclick={() => counter.count += 1}>
	increment
</button>
<Child />
<Child />
<Child />
<button onclick={() => counter.count = 0}>
	reset
</button>
```
```
<script lang="ts">
	import { setCounter } from './context.ts';
	import Child from './Child.svelte';
	let counter = $state({
		count: 0
	});
	setCounter(counter);
</script>
<button onclick={() => counter.count += 1}>
	increment
</button>
<Child />
<Child />
<Child />
<button onclick={() => counter.count = 0}>
	reset
</button>
```
```
<script>
	import { getCounter } from './context.ts';
	const counter = getCounter();
</script>
<p>{counter.count}</p>
```
```
<script lang="ts">
	import { getCounter } from './context.ts';
	const counter = getCounter();
</script>
<p>{counter.count}</p>
```
`import {` `function createContext<T>(): [() => T, (context: T) => T]`
Returns a `[get, set]` pair of functions for working with context in a type-safe way.

`get` will throw an error if no parent component called `set`.

createContext } from 'svelte';
interface Counter {
	`Counter.count: number`count: number;
}
export const [`const getCounter: () => Counter`getCounter, `const setCounter: (context: Counter) => Counter`setCounter] = `createContext<Counter>(): [() => Counter, (context: Counter) => Counter]`
Returns a `[get, set]` pair of functions for working with context in a type-safe way.

`get` will throw an error if no parent component called `set`.

createContext<Counter>();
...though note that if you *reassign* `counter` instead of updating it, you will ‘break the link’ — in other words instead of this...

```
<button onclick={() => counter = { count: 0 } }>
	reset
</button>
```
...you must do this:

```
<button onclick={() => counter.count = 0}>
	reset
</button>
```
Svelte will warn you if you get it wrong.

Similarly, to pass primitive values through context, use functions as described in [Passing state into functions]($state#Passing-state-into-functions).

## Component testing

When writing [component tests](testing#Unit-and-component-tests-with-Vitest-Component-testing), it can be useful to create a wrapper component that sets the context in order to check the behaviour of a component that uses it. As of version 5.49, you can do this sort of thing:

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
import { `const expect: ExpectStatic`expect, `const test: TestAPI`
Defines a test case with a given name and test function. The test function can optionally be configured with test options.

test } from 'vitest';
import { `import setUserContext`setUserContext } from './context';
import ```
type MyComponent = SvelteComponent<Record<string, any>, any, any>
const MyComponent: LegacyComponentType
```

`test<object>(name: string | Function, fn?: TestFunction<object> | undefined, options?: number): void (+1 overload)`
Defines a test case with a given name and test function. The test function can optionally be configured with test options.

test('MyComponent', () => {
	function ```
function (local function) Wrapper(...args: any[]): {
    $on?(type: string, callback: (e: any) => void): () => void;
    $set?(props: Partial<Record<string, any>>): void;
} & Record<string, any>
```

`args: any[]`args) {
		`import setUserContext`setUserContext({ `name: string`name: 'Bob' });
		return `function MyComponent(internals: Brand<"ComponentInternals">, props: Record<string, any>): ReturnType<Component<Record<string, any>, Record<string, any>>>`MyComponent(...`args: any[]`args);
	}
	const ```
const component: {
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

mount(
```
function (local function) Wrapper(...args: any[]): {
    $on?(type: string, callback: (e: any) => void): () => void;
    $set?(props: Partial<Record<string, any>>): void;
} & Record<string, any>
```

`target: Document | Element | ShadowRoot`
Target element where the component will be mounted.

target: `var document: Document`
**`window.document`** returns a reference to the document contained in the window.

document.`Document.body: HTMLElement`
The **`Document.body`** property represents the 

 or body
	});
	`expect<string>(actual: string, message?: string): Assertion<string> (+1 overload)`expect(`var document: Document`
**`window.document`** returns a reference to the document contained in the window.

document.`Document.body: HTMLElement`
The **`Document.body`** property represents the 

 or body.`Element.innerHTML: string`
The **`innerHTML`** property of the Element interface gets or sets the HTML or XML markup contained within the element, omitting any shadow roots in both cases.

innerHTML).`JestAssertion<string>.toBe: <string>(expected: string) => void`
Checks that a value is what you expect. It calls `Object.is` to compare values.
Don’t use `toBe` with floating-point numbers.

toBe('<h1>Hello Bob!</h1>');
	
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
const component: {
    $on?(type: string, callback: (e: any) => void): () => void;
    $set?(props: Partial<Record<string, any>>): void;
} & Record<string, any>
```

This approach also works with [`hydrate`](imperative-component-api#hydrate) and [`render`](imperative-component-api#render).

## Replacing global state

When you have state shared by many different components, you might be tempted to put it in its own module and just import it wherever it’s needed:

`export const` ```
const myGlobalState: {
    user: {};
}
```

```
function $state<{
    user: {};
}>(initial: {
    user: {};
}): {
    user: {};
} (+1 overload)
namespace $state
```

Declares reactive state.

Example:

`let count = $state(0);`

$state({
	`user: {}`user: {
		// ...
	}
	// ...
});
In many cases this is perfectly fine, but there is a risk: if you mutate the state during server-side rendering (which is discouraged, but entirely possible!)...

```
<script>
	import { myGlobalState } from './state.svelte.js';
	let { data } = $props();
	if (data.user) {
		myGlobalState.user = data.user;
	}
</script>
```
```
<script lang="ts">
	import { myGlobalState } from './state.svelte.js';
	let { data } = $props();
	if (data.user) {
		myGlobalState.user = data.user;
	}
</script>
```
...then the data may be accessible by the *next* user. Context solves this problem because it is not shared between requests.

 [Edit this page on GitHub](https://github.com/sveltejs/svelte/edit/main/documentation/docs/06-runtime/02-context.md)  [llms.txt](/docs/svelte/context/llms.txt)

# Citations

1. Source page: https://svelte.dev/docs/svelte/context
