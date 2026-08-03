---
type: Web Page
title: Custom properties • Svelte Docs
description: Custom properties • Svelte documentation
resource: https://svelte.dev/docs/svelte/custom-properties
timestamp: '2026-08-03T08:54:23.898986+00:00'
---

# Custom properties

You can pass CSS custom properties — both static and dynamic — to components:

```
<Slider
	bind:value
	min={0}
	max={100}
	--track-color="black"
	--thumb-color="rgb({r} {g} {b})"
/>
```
The above code essentially desugars to this:

```
<svelte-css-wrapper style="display: contents; --track-color: black; --thumb-color: rgb({r} {g} {b})">
	<Slider
		bind:value
		min={0}
		max={100}
	/>
</svelte-css-wrapper>
```
For an SVG element, it would use `<g>` instead:

```
<g style="--track-color: black; --thumb-color: rgb({r} {g} {b})">
	<Slider
		bind:value
		min={0}
		max={100}
	/>
</g>
```
Inside the component, we can read these custom properties (and provide fallback values) using [`var(...)`](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_custom_properties):

```
<style>
	.track {
		background: var(--track-color, #aaa);
	}
	.thumb {
		background: var(--thumb-color, blue);
	}
</style>
```
You don't *have* to specify the values directly on the component; as long as the custom properties are defined on a parent element, the component can use them. It's common to define custom properties on the `:root` element in a global stylesheet so that they apply to your entire application.

 While the extra element will not affect layout, it *will* affect any CSS selectors that (for example) use the `>` combinator to target an element directly inside the component's container.

 [Edit this page on GitHub](https://github.com/sveltejs/svelte/edit/main/documentation/docs/04-styling/03-custom-properties.md)  [llms.txt](/docs/svelte/custom-properties/llms.txt)

# Citations

1. Source page: https://svelte.dev/docs/svelte/custom-properties
