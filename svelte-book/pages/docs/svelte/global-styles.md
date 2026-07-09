---
type: Web Page
title: Global styles • Svelte Docs
description: Global styles • Svelte documentation
resource: https://svelte.dev/docs/svelte/global-styles
timestamp: '2026-07-09T12:17:00.027378+00:00'
---

# Global styles

## :global(...)

To apply styles to a single selector globally, use the `:global(...)` modifier:

```
<style>
	:global(body) {
		/* applies to <body> */
		margin: 0;
	}
	div :global(strong) {
		/* applies to all <strong> elements, in any component,
		   that are inside <div> elements belonging
		   to this component */
		color: goldenrod;
	}
	p:global(.big.red) {
		/* applies to all <p> elements belonging to this component
		   with `class="big red"`, even if it is applied
		   programmatically (for example by a library) */
	}
</style>
```
If you want to make @keyframes that are accessible globally, you need to prepend your keyframe names with `-global-`.

The `-global-` part will be removed when compiled, and the keyframe will then be referenced using just `my-animation-name` elsewhere in your code.

```
<style>
	@keyframes -global-my-animation-name {
		/* code goes here */
	}
</style>
```
## :global

To apply styles to a group of selectors globally, create a `:global {...}` block:

```
<style>
	:global {
		/* applies to every <div> in your application */
		div { ... }
		/* applies to every <p> in your application */
		p { ... }
	}
	.a :global {
		/* applies to every `.b .c .d` element, in any component,
		   that is inside an `.a` element in this component */
		.b .c .d {...}
	}
</style>
```
The second example above could also be written as an equivalent

`.a :global .b .c .d`selector, where everything after the`:global`is unscoped, though the nested form is preferred.

[ Edit this page on GitHub](https://github.com/sveltejs/svelte/edit/main/documentation/docs/04-styling/02-global-styles.md) [ llms.txt](/docs/svelte/global-styles/llms.txt)

previous next

# Citations

1. Source page: https://svelte.dev/docs/svelte/global-styles
