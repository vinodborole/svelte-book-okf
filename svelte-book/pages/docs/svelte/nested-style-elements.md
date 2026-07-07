---
type: Web Page
title: Nested <style> elements • Svelte Docs
description: Nested <style> elements • Svelte documentation
resource: https://svelte.dev/docs/svelte/nested-style-elements
timestamp: '2026-07-07T10:59:37.245126+00:00'
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
Edit this page on GitHub llms.txt

previous next

# Citations

1. Source page: https://svelte.dev/docs/svelte/nested-style-elements
