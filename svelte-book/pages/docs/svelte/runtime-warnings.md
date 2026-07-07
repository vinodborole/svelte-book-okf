---
type: Web Page
title: Runtime warnings • Svelte Docs
description: Runtime warnings • Svelte documentation
resource: https://svelte.dev/docs/svelte/runtime-warnings
timestamp: '2026-07-07T10:59:37.245126+00:00'
---

# Runtime warnings

## Client warnings

### assignment_value_stale

`Assignment to `%property%` property (%location%) will evaluate to the right-hand side, not the value of `%property%` following the assignment. This may result in unexpected behaviour.`Given a case like this...

```
<script>
	let object = $state({ array: null });
	function add() {
		(object.array ??= []).push(object.array.length);
	}
</script>
<button onclick={add}>add</button>
<p>items: {JSON.stringify(object.items)}</p>
```
...the array being pushed to when the button is first clicked is the `[]` on the right-hand side of the assignment, but the resulting value of `object.array` is an empty state proxy. As a result, the pushed value will be discarded.

You can fix this by separating it into two statements:

`function ``function add(): void`add() {
	```
let object: {
    array: number[];
}
```

`array: number[]`array ??= [];
	```
let object: {
    array: number[];
}
```

`array: number[]`array.`Array<number>.push(...items: number[]): number`Appends new elements to the end of an array, and returns the new length of the array.

push(```
let object: {
    array: number[];
}
```

`array: number[]`array.`Array<number>.length: number`Gets or sets the length of the array. This is a number one higher than the highest index in the array.

length);
}### await_reactivity_loss

`Detected reactivity loss when reading `%name%`. This happens when state is read in an async function after an earlier `await``Svelte's signal-based reactivity works by tracking which bits of state are read when a template or `$derived(...)` expression executes. If an expression contains an `await`, Svelte transforms it such that any state *after* the `await` is also tracked — in other words, in a case like this...

`let ``let total: number`total = ```
function $derived<number>(expression: number): number
namespace $derived
```

Declares derived state, i.e. one that depends on other state variables.
The expression inside `$derived(...)` should be free of side-effects.

Example:

`let double = $derived(count * 2);`

$derived(await `let a: Promise<number>`a + `let b: number`b);...both `a` and `b` are tracked, even though `b` is only read once `a` has resolved, after the initial execution.

This does *not* apply to an `await` that is not 'visible' inside the expression. In a case like this...

`async function ``function sum(): Promise<number>`sum() {
	return await `let a: Promise<number>`a + `let b: number`b;
}
let `let total: number`total = ```
function $derived<number>(expression: number): number
namespace $derived
```

Declares derived state, i.e. one that depends on other state variables.
The expression inside `$derived(...)` should be free of side-effects.

Example:

`let double = $derived(count * 2);`

$derived(await `function sum(): Promise<number>`sum());...`total` will depend on `a` (which is read immediately) but not `b` (which is not). The solution is to pass the values into the function:

```
/**
 * @param {Promise<number>} a
 * @param {number} b
 */
async function 
```
`function sum(a: Promise<number>, b: number): Promise<number>`sum(`a: Promise<number>`a, `b: number`b) {
	return await `a: Promise<number>`a + `b: number`b;
}
let `let total: number`total = ```
function $derived<number>(expression: number): number
namespace $derived
```

Declares derived state, i.e. one that depends on other state variables.
The expression inside `$derived(...)` should be free of side-effects.

Example:

`let double = $derived(count * 2);`

$derived(await `function sum(a: Promise<number>, b: number): Promise<number>`sum(`let a: Promise<number>`a, `let b: number`b));### await_waterfall

`An async derived, `%name%` (%location%) was not read immediately after it resolved. This often indicates an unnecessary waterfall, which can slow down your app`In a case like this...

`let ``let a: number`a = ```
function $derived<number>(expression: number): number
namespace $derived
```

Declares derived state, i.e. one that depends on other state variables.
The expression inside `$derived(...)` should be free of side-effects.

Example:

`let double = $derived(count * 2);`

$derived(await `function one(): Promise<number>`one());
let `let b: number`b = ```
function $derived<number>(expression: number): number
namespace $derived
```

Declares derived state, i.e. one that depends on other state variables.
The expression inside `$derived(...)` should be free of side-effects.

Example:

`let double = $derived(count * 2);`

$derived(await `function two(): Promise<number>`two());...the second `$derived` will not be created until the first one has resolved. Since `await two()` does not depend on the value of `a`, this delay, often described as a 'waterfall', is unnecessary.

(Note that if the values of `await one()` and `await two()` subsequently change, they can do so concurrently — the waterfall only occurs when the deriveds are first created.)

You can solve this by creating the promises first and *then* awaiting them:

`let ``let aPromise: Promise<number>`aPromise = ```
function $derived<Promise<number>>(expression: Promise<number>): Promise<number>
namespace $derived
```

Declares derived state, i.e. one that depends on other state variables.
The expression inside `$derived(...)` should be free of side-effects.

Example:

`let double = $derived(count * 2);`

$derived(`function one(): Promise<number>`one());
let `let bPromise: Promise<number>`bPromise = ```
function $derived<Promise<number>>(expression: Promise<number>): Promise<number>
namespace $derived
```

Declares derived state, i.e. one that depends on other state variables.
The expression inside `$derived(...)` should be free of side-effects.

Example:

`let double = $derived(count * 2);`

$derived(`function two(): Promise<number>`two());
let `let a: number`a = ```
function $derived<number>(expression: number): number
namespace $derived
```

Declares derived state, i.e. one that depends on other state variables.
The expression inside `$derived(...)` should be free of side-effects.

Example:

`let double = $derived(count * 2);`

$derived(await `let aPromise: Promise<number>`aPromise);
let `let b: number`b = ```
function $derived<number>(expression: number): number
namespace $derived
```

Declares derived state, i.e. one that depends on other state variables.
The expression inside `$derived(...)` should be free of side-effects.

Example:

`let double = $derived(count * 2);`

$derived(await `let bPromise: Promise<number>`bPromise);### binding_property_non_reactive

``%binding%` is binding to a non-reactive property```%binding%` (%location%) is binding to a non-reactive property`### console_log_state

`Your `console.%method%` contained `$state` proxies. Consider using `$inspect(...)` or `$state.snapshot(...)` instead`When logging a proxy, browser devtools will log the proxy itself rather than the value it represents. In the case of Svelte, the 'target' of a `$state` proxy might not resemble its current value, which can be confusing.

The easiest way to log a value as it changes over time is to use the `$inspect` rune. Alternatively, to log things on a one-off basis (for example, inside an event handler) you can use `$state.snapshot` to take a snapshot of the current value.

### derived_inert

`Reading a derived belonging to a now-destroyed effect may result in stale values`A `$derived` value created inside an effect will stop updating when the effect is destroyed. You should create the `$derived` outside the effect, or inside an `$effect.root`.

### event_handler_invalid

`%handler% should be a function. Did you mean to %suggestion%?`### hydratable_missing_but_expected

`Expected to find a hydratable with key `%key%` during hydration, but did not.`This can happen if you render a hydratable on the client that was not rendered on the server, and means that it was forced to fall back to running its function blockingly during hydration. This is bad for performance, as it blocks hydration until the asynchronous work completes.

```
<script>
  import { hydratable } from 'svelte';
	if (BROWSER) {
		// bad! nothing can become interactive until this asynchronous work is done
		await hydratable('foo', get_slow_random_number);
	}
</script>
```
### hydration_attribute_changed

`The `%attribute%` attribute on `%html%` changed its value between server and client renders. The client value, `%value%`, will be ignored in favour of the server value`Certain attributes like `src` on an `<img>` element will not be repaired during hydration, i.e. the server value will be kept. That's because updating these attributes can cause the image to be refetched (or in the case of an `<iframe>`, for the frame to be reloaded), even if they resolve to the same resource.

To fix this, either silence the warning with a `svelte-ignore` comment, or ensure that the value stays the same between server and client. If you really need the value to change on hydration, you can force an update like this:

```
<script>
	let { src } = $props();
	if (typeof window !== 'undefined') {
		// stash the value...
		const initial = src;
		// unset it...
		src = undefined;
		$effect(() => {
			// ...and reset after we've mounted
			src = initial;
		});
	}
</script>
<img {src} />
```
### hydration_html_changed

`The value of an `{@html ...}` block changed between server and client renders. The client value will be ignored in favour of the server value``The value of an `{@html ...}` block %location% changed between server and client renders. The client value will be ignored in favour of the server value`If the `{@html ...}` value changes between the server and the client, it will not be repaired during hydration, i.e. the server value will be kept. That's because change detection during hydration is expensive and usually unnecessary.

To fix this, either silence the warning with a `svelte-ignore` comment, or ensure that the value stays the same between server and client. If you really need the value to change on hydration, you can force an update like this:

```
<script>
	let { markup } = $props();
	if (typeof window !== 'undefined') {
		// stash the value...
		const initial = markup;
		// unset it...
		markup = undefined;
		$effect(() => {
			// ...and reset after we've mounted
			markup = initial;
		});
	}
</script>
{@html markup}
```
### hydration_mismatch

`Hydration failed because the initial UI does not match what was rendered on the server``Hydration failed because the initial UI does not match what was rendered on the server. The error occurred near %location%`This warning is thrown when Svelte encounters an error while hydrating the HTML from the server. During hydration, Svelte walks the DOM, expecting a certain structure. If that structure is different (for example because the HTML was repaired by the DOM because of invalid HTML), then Svelte will run into issues, resulting in this warning.

During development, this error is often preceded by a `console.error` detailing the offending HTML, which needs fixing.

### invalid_raw_snippet_render

`The `render` function passed to `createRawSnippet` should return HTML for a single element`### legacy_recursive_reactive_block

`Detected a migrated `$:` reactive block in `%filename%` that both accesses and updates the same reactive value. This may cause recursive updates when converted to an `$effect`.`### lifecycle_double_unmount

`Tried to unmount a component that was not mounted`### ownership_invalid_binding

`%parent% passed property `%prop%` to %child% with `bind:`, but its parent component %owner% did not declare `%prop%` as a binding. Consider creating a binding between %owner% and %parent% (e.g. `bind:%prop%={...}` instead of `%prop%={...}`)`Consider three components `GrandParent`, `Parent` and `Child`. If you do `<GrandParent bind:value>`, inside `GrandParent` pass on the variable via `<Parent {value} />` (note the missing `bind:`) and then do `<Child bind:value>` inside `Parent`, this warning is thrown.

To fix it, `bind:` to the value instead of just passing a property (i.e. in this example do `<Parent bind:value />`).

### ownership_invalid_mutation

`Mutating unbound props (`%name%`, at %location%) is strongly discouraged. Consider using `bind:%prop%={...}` in %parent% (or using a callback) instead`Consider the following code:

```
<script>
	import Child from './Child.svelte';
	let person = $state({ name: 'Florida', surname: 'Man' });
</script>
<Child {person} />
```
```
<script lang="ts">
	import Child from './Child.svelte';
	let person = $state({ name: 'Florida', surname: 'Man' });
</script>
<Child {person} />
```
```
<script>
	let { person } = $props();
</script>
<input bind:value={person.name}>
<input bind:value={person.surname}>
```
```
<script lang="ts">
	let { person } = $props();
</script>
<input bind:value={person.name}>
<input bind:value={person.surname}>
```
`Child` is mutating `person` which is owned by `App` without being explicitly "allowed" to do so. This is strongly discouraged since it can create code that is hard to reason about at scale ("who mutated this value?"), hence the warning.

To fix it, either create callback props to communicate changes, or mark `person` as `$bindable`.

### select_multiple_invalid_value

`The `value` property of a `<select multiple>` element should be an array, but it received a non-array value. The selection will be kept as is.`When using `<select multiple value={...}>`, Svelte will mark all selected `<option>` elements as selected by iterating over the array passed to `value`. If `value` is not an array, Svelte will emit this warning and keep the selected options as they are.

To silence the warning, ensure that `value`:

- is an array for an explicit selection
- is `null`or`undefined`to keep the selection as is

### state_proxy_equality_mismatch

`Reactive `$state(...)` proxies and the values they proxy have different identities. Because of this, comparisons with `%operator%` will produce unexpected results``$state(...)` creates a proxy of the value it is passed. The proxy and the value have different identities, meaning equality checks will always return `false`:

```
<script>
	let value = { foo: 'bar' };
	let proxy = $state(value);
	value === proxy; // always false
</script>
```
To resolve this, ensure you're comparing values where both values were created with `$state(...)`, or neither were. Note that `$state.raw(...)` will *not* create a state proxy.

### state_proxy_unmount

`Tried to unmount a state proxy, rather than a component``unmount` was called with a state proxy:

`let ````
let component: {
    $on?(type: string, callback: (e: any) => void): () => void;
    $set?(props: Partial<Record<string, any>>): void;
} & Record<string, any>
```

```
function $state<{
    $on?(type: string, callback: (e: any) => void): () => void;
    $set?(props: Partial<Record<string, any>>): void;
} & Record<string, any>>(initial: {
    $on?(type: string, callback: (e: any) => void): () => void;
    $set?(props: Partial<Record<string, any>>): void;
} & Record<string, any>): {
    $on?(type: string, callback: (e: any) => void): () => void;
    $set?(props: Partial<Record<string, any>>): void;
} & Record<string, any> (+1 overload)
namespace $state
```

Declares reactive state.

Example:

`let count = $state(0);`

$state(```
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

mount(`const Component: LegacyComponentType`Component, { `target: Document | Element | ShadowRoot`Target element where the component will be mounted.

target }));
// later...
```
function unmount(component: Record<string, any>, options?: {
    outro?: boolean;
} | undefined): Promise<void>
```

Unmounts a component that was previously mounted using `mount` or `hydrate`.

Since 5.13.0, if `options.outro` is `true`, transitions will play before the component is removed from the DOM.

Returns a `Promise` that resolves after transitions have completed if `options.outro` is true, or immediately otherwise (prior to 5.13.0, returns `void`).

```
import { mount, unmount } from 'svelte';
import App from './App.svelte';
const app = mount(App, { target: document.body });
// later...
unmount(app, { outro: true });
```

unmount(```
let component: {
    $on?(type: string, callback: (e: any) => void): () => void;
    $set?(props: Partial<Record<string, any>>): void;
} & Record<string, any>
```

Avoid using `$state` here. If `component` *does* need to be reactive for some reason, use `$state.raw` instead.

### svelte_boundary_reset_noop

`A `<svelte:boundary>` `reset` function only resets the boundary the first time it is called`When an error occurs while rendering the contents of a `<svelte:boundary>`, the `onerror` handler is called with the error plus a `reset` function that attempts to re-render the contents.

This `reset` function should only be called once. After that, it has no effect — in a case like this, where a reference to `reset` is stored outside the boundary, clicking the button while `<Contents />` is rendered will *not* cause the contents to be rendered again.

```
<script>
	let reset;
</script>
<button onclick={reset}>reset</button>
<svelte:boundary onerror={(e, r) => (reset = r)}>
	<!-- contents -->
	{#snippet failed(e)}
		<p>oops! {e.message}</p>
	{/snippet}
</svelte:boundary>
```
### transition_slide_display

`The `slide` transition does not work correctly for elements with `display: %value%``The slide transition works by animating the `height` of the element, which requires a `display` style like `block`, `flex` or `grid`. It does not work for:

- `display: inline`(which is the default for elements like- `<span>`), and its variants like- `inline-block`,- `inline-flex`and- `inline-grid`
- `display: table`and- `table-[name]`, which are the defaults for elements like- `<table>`and- `<tr>`
- `display: contents`

## Shared warnings

### dynamic_void_element_content

``<svelte:element this="%tag%">` is a void element — it cannot have content`Elements such as `<input>` cannot have content, any children passed to these elements will be ignored.

### state_snapshot_uncloneable

`Value cannot be cloned with `$state.snapshot` — the original value was returned````
The following properties cannot be cloned with `$state.snapshot` — the return value contains the originals:
%properties%
```
`$state.snapshot` tries to clone the given value in order to return a reference that no longer changes. Certain objects may not be cloneable, in which case the original value is returned. In the following example, `property` is cloned, but `window` is not, because DOM elements are uncloneable:

`const ````
const object: {
    property: string;
    window: Window & typeof globalThis;
}
```

```
function $state<{
    property: string;
    window: Window & typeof globalThis;
}>(initial: {
    property: string;
    window: Window & typeof globalThis;
}): {
    property: string;
    window: Window & typeof globalThis;
} (+1 overload)
namespace $state
```

Declares reactive state.

Example:

`let count = $state(0);`

$state({ `property: string`property: 'this is cloneable', `window: Window & typeof globalThis`window })
const ```
const snapshot: {
    property: string;
    window: {
        [x: number]: {
            [x: number]: ...;
            readonly clientInformation: {
                readonly clipboard: {
                    read: {};
                    readText: {};
                    write: {};
                    writeText: {};
                    addEventListener: {};
                    dispatchEvent: {};
                    removeEventListener: {};
                };
                readonly credentials: {
                    create: {};
                    get: {};
                    preventSilentAccess: {};
                    store: {};
                };
                readonly doNotTrack: string | null;
                readonly geolocation: {
                    clearWatch: {};
                    getCurrentPosition: {};
                    watchPosition: {};
                };
                readonly login: {
                    setStatus: {};
                };
                readonly maxTouchPoints: number;
                readonly mediaCapabilities: {
                    decodingInfo: {};
                    encodingInfo: {};
                };
                readonly mediaDevices: {
                    ondevicechange: {} | null;
                    ... 6 more ...;
                    dispatchEvent: {};
                };
                ... 35 more ...;
                readonly storage: {
                    ...;
                };
            };
            ... 215 more ...;
            readonly sessionStorage: {
                ...;
            };
        };
        ... 955 more ...;
        undefined: undefined;
    };
}
```

```
namespace $state
function $state<T>(initial: T): T (+1 overload)
```

Declares reactive state.

Example:

`let count = $state(0);`

$state.```
function $state.snapshot<{
    property: string;
    window: Window & typeof globalThis;
}>(state: {
    property: string;
    window: Window & typeof globalThis;
}): {
    property: string;
    window: {
        [x: number]: {
            [x: number]: ...;
            readonly clientInformation: {
                readonly clipboard: {
                    read: {};
                    readText: {};
                    write: {};
                    writeText: {};
                    addEventListener: {};
                    dispatchEvent: {};
                    removeEventListener: {};
                };
                readonly credentials: {
                    create: {};
                    get: {};
                    preventSilentAccess: {};
                    store: {};
                };
                readonly doNotTrack: string | null;
                readonly geolocation: {
                    clearWatch: {};
                    getCurrentPosition: {};
                    watchPosition: {};
                };
                readonly login: {
                    setStatus: {};
                };
                ... 38 more ...;
                readonly storage: {
                    ...;
                };
            };
            ... 215 more ...;
            readonly sessionStorage: {
                ...;
            };
        };
        ... 955 more ...;
        undefined: undefined;
    };
}
```

To take a static snapshot of a deeply reactive `$state` proxy, use `$state.snapshot`:

Example:

```
<script>
  let counter = $state({ count: 0 });
  function onclick() {
	// Will log `{ count: ... }` rather than `Proxy { ... }`
	console.log($state.snapshot(counter));
  };
</script>
```

If `state` has a `toJSON` method, the snapshot will clone the value returned from `toJSON` instead of the original object.

snapshot(```
const object: {
    property: string;
    window: Window & typeof globalThis;
}
```

Edit this page on GitHub llms.txt

# Citations

1. Source page: https://svelte.dev/docs/svelte/runtime-warnings
