---
type: Web Page
title: $props • Svelte Docs
description: $props • Svelte documentation
resource: https://svelte.dev/docs/svelte/$props
timestamp: '2026-07-07T10:59:37.245126+00:00'
---

# $props

The inputs to a component are referred to as *props*, which is short for *properties*. You pass props to components just like you pass attributes to elements:

```
<script>
	import MyComponent from './MyComponent.svelte';
</script>
<MyComponent adjective="cool" />
```
```
<script lang="ts">
	import MyComponent from './MyComponent.svelte';
</script>
<MyComponent adjective="cool" />
```
On the other side, inside `MyComponent.svelte`, we can receive props with the `$props` rune...

```
<script>
	let props = $props();
</script>
<p>this component is {props.adjective}</p>
```
```
<script lang="ts">
	let props = $props();
</script>
<p>this component is {props.adjective}</p>
```
...though more commonly, you'll *destructure* your props:

```
<script>
	let { adjective } = $props();
</script>
<p>this component is {adjective}</p>
```
```
<script lang="ts">
	let { adjective } = $props();
</script>
<p>this component is {adjective}</p>
```
## Fallback values

Destructuring allows us to declare fallback values, which are used if the parent component does not set a given prop (or the value is `undefined`):

`let { ``let adjective: any`adjective = 'happy' } = ```
function $props(): any
namespace $props
```

Declares the props that a component accepts. Example:

`let { optionalProp = 42, requiredProp, bindableProp = $bindable() }: { optionalProp?: number; requiredProps: string; bindableProp: boolean } = $props();`

$props();Fallback values are not turned into reactive state proxies (see Updating props for more info)

## Renaming props

We can also use the destructuring assignment to rename props, which is necessary if they're invalid identifiers, or a JavaScript keyword like `super`:

`let { super: ``let trouper: any`trouper = 'lights are gonna find me' } = ```
function $props(): any
namespace $props
```

Declares the props that a component accepts. Example:

`let { optionalProp = 42, requiredProp, bindableProp = $bindable() }: { optionalProp?: number; requiredProps: string; bindableProp: boolean } = $props();`

$props();## Rest props

Finally, we can use a *rest property* to get, well, the rest of the props:

`let { ``let a: any`a, `let b: any`b, `let c: any`c, ...`let others: any`others } = ```
function $props(): any
namespace $props
```

Declares the props that a component accepts. Example:

`let { optionalProp = 42, requiredProp, bindableProp = $bindable() }: { optionalProp?: number; requiredProps: string; bindableProp: boolean } = $props();`

$props();## Updating props

References to a prop inside a component update when the prop itself updates — when `count` changes in `App.svelte`, it will also change inside `Child.svelte`. But the child component is able to temporarily override the prop value, which can be useful for unsaved ephemeral state:

```
<script>
	import Child from './Child.svelte';
	let count = $state(0);
</script>
<button onclick={() => (count += 1)}>
	clicks (parent): {count}
</button>
<Child {count} />
```
```
<script lang="ts">
	import Child from './Child.svelte';
	let count = $state(0);
</script>
<button onclick={() => (count += 1)}>
	clicks (parent): {count}
</button>
<Child {count} />
```
```
<script>
	let { count } = $props();
</script>
<button onclick={() => (count += 1)}>
	clicks (child): {count}
</button>
```
```
<script lang="ts">
	let { count } = $props();
</script>
<button onclick={() => (count += 1)}>
	clicks (child): {count}
</button>
```
While you can temporarily *reassign* props, you should not *mutate* props unless they are bindable.

If the prop is a regular object, the mutation will have no effect:

```
<script>
	import Child from './Child.svelte';
</script>
<Child object={{ count: 0 }} />
```
```
<script lang="ts">
	import Child from './Child.svelte';
</script>
<Child object={{ count: 0 }} />
```
```
<script>
	let { object } = $props();
</script>
<button onclick={() => {
	// has no effect
	object.count += 1
}}>
	clicks: {object.count}
</button>
```
```
<script lang="ts">
	let { object } = $props();
</script>
<button onclick={() => {
	// has no effect
	object.count += 1
}}>
	clicks: {object.count}
</button>
```
If the prop is a reactive state proxy, however, then mutations *will* have an effect but you will see an `ownership_invalid_mutation` warning, because the component is mutating state that does not 'belong' to it:

```
<script>
	import Child from './Child.svelte';
	let object = $state({count: 0});
</script>
<Child {object} />
```
```
<script lang="ts">
	import Child from './Child.svelte';
	let object = $state({count: 0});
</script>
<Child {object} />
```
```
<script>
	let { object } = $props();
</script>
<button onclick={() => {
	// will cause the count below to update,
	// but with a warning. Don't mutate
	// objects you don't own!
	object.count += 1
}}>
	clicks: {object.count}
</button>
```
```
<script lang="ts">
	let { object } = $props();
</script>
<button onclick={() => {
	// will cause the count below to update,
	// but with a warning. Don't mutate
	// objects you don't own!
	object.count += 1
}}>
	clicks: {object.count}
</button>
```
The fallback value of a prop not declared with `$bindable` is left untouched — it is not turned into a reactive state proxy — meaning mutations will not cause updates:

```
<script>
	import Child from './Child.svelte';
</script>
<Child />
```
```
<script lang="ts">
	import Child from './Child.svelte';
</script>
<Child />
```
```
<script>
	let { object = { count: 0 } } = $props();
</script>
<button onclick={() => {
	// has no effect if the fallback value is used
	object.count += 1
}}>
	clicks: {object.count}
</button>
```
```
<script lang="ts">
	let { object = { count: 0 } } = $props();
</script>
<button onclick={() => {
	// has no effect if the fallback value is used
	object.count += 1
}}>
	clicks: {object.count}
</button>
```
In summary: don't mutate props. Either use callback props to communicate changes, or — if parent and child should share the same object — use the `$bindable` rune.

## Type safety

You can add type safety to your components by annotating your props, as you would with any other variable declaration. In TypeScript that might look like this...

```
<script lang="ts">
	let { adjective }: { adjective: string } = $props();
</script>
```
...while in JSDoc you can do this:

```
<script>
	/** @type {{ adjective: string }} */
	let { adjective } = $props();
</script>
```
You can, of course, separate the type declaration from the annotation:

```
<script lang="ts">
	interface Props {
		adjective: string;
	}
	let { adjective }: Props = $props();
</script>
```
Interfaces for native DOM elements are provided in the

`svelte/elements`module (see Typing wrapper components)

If your component exposes snippet props like `children`, these should be typed using the `Snippet` interface imported from `'svelte'` — see Typing snippets for examples.

Adding types is recommended, as it ensures that people using your component can easily discover which props they should provide.

## $props.id()

This rune, added in version 5.20.0, generates an ID that is unique to the current component instance. When hydrating a server-rendered component, the value will be consistent between server and client.

This is useful for linking elements via attributes like `for` and `aria-labelledby`.

```
<script>
	const uid = $props.id();
</script>
<form>
	<label for="{uid}-firstname">First Name: </label>
	<input id="{uid}-firstname" type="text" />
	<label for="{uid}-lastname">Last Name: </label>
	<input id="{uid}-lastname" type="text" />
</form>
```

# Citations

1. Source page: https://svelte.dev/docs/svelte/$props
