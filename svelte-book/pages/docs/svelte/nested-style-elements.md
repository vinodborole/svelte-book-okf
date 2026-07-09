---
type: Web Page
title: Nested <style> elements • Svelte Docs
description: Nested <style> elements • Svelte documentation
resource: https://svelte.dev/docs/svelte/nested-style-elements
timestamp: '2026-07-09T12:17:00.027378+00:00'
---

# Nested <style> elements

There can only be one top-level `<style>` tag per component.

However, it is possible to have a `<style>` tag nested inside other elements or logic blocks.

In that case, the `<style>` tag will be inserted as-is into the DOM; no scoping or processing will be done on the `<style>` tag.

```
<div>
	<style>
		/* this style tag will be inserted as-is */
		div {
			/* this will apply to all `<div>` elements in the DOM */
			color: red;
		}
	</style>
</div>
```
[ Edit this page on GitHub](https://github.com/sveltejs/svelte/edit/main/documentation/docs/04-styling/04-nested-style-elements.md) [ llms.txt](/docs/svelte/nested-style-elements/llms.txt)

previous next

# Citations

1. Source page: https://svelte.dev/docs/svelte/nested-style-elements
