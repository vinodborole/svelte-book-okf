---
type: Web Page
title: $$props and $$restProps • Svelte Docs
description: $$props and $$restProps • Svelte documentation
resource: https://svelte.dev/docs/svelte/legacy-$$props-and-$$restProps
timestamp: '2026-08-03T08:54:23.898986+00:00'
---

# $$props and $$restProps

In runes mode, getting an object containing all the props that were passed in is easy, using the [`$props`]($props) rune.

In legacy mode, we use `$$props` and `$$restProps`:

- `$$props` contains all the props that were passed in, including ones that are not individually declared with the`export` keyword
- `$$restProps` contains all the props that were passed in*except* the ones that were individually declared

For example, a `<Button>` component might need to pass along all its props to its own `<button>` element, except the `variant` prop:

```
<script>
	export let variant;
</script>
<button {...$$restProps} class="variant-{variant} {$$props.class ?? ''}">
	click me
</button>
<style>
	.variant-danger {
		background: red;
	}
</style>
```
In Svelte 3/4 using `$$props` and `$$restProps` creates a modest performance penalty, so they should only be used when needed.

 [Edit this page on GitHub](https://github.com/sveltejs/svelte/edit/main/documentation/docs/99-legacy/04-legacy-$$props-and-$$restProps.md)  [llms.txt](/docs/svelte/legacy-$$props-and-$$restProps/llms.txt)

previous next

# Citations

1. Source page: https://svelte.dev/docs/svelte/legacy-$$props-and-$$restProps
