---
type: Web Page
title: $$slots • Svelte Docs
description: $$slots • Svelte documentation
resource: https://svelte.dev/docs/svelte/legacy-$$slots
timestamp: '2026-08-17T06:25:40.913234+00:00'
---

# $$slots

In runes mode, we know which [snippets](snippet) were provided to a component, as they’re just normal props.

In legacy mode, the way to know if content was provided for a given slot is with the `$$slots` object, whose keys are the names of the slots passed into the component by the parent.

Card

```
<div>
	<slot name="title" />
	{#if $$slots.description}
		<!-- This <hr> and slot will render only if `slot="description"` is provided. -->
		<hr />
		<slot name="description" />
	{/if}
</div>
```
App

```
<Card>
	<h1 slot="title">Blog Post Title</h1>
	<!-- No slot named "description" was provided so the optional slot will not be rendered. -->
</Card>
```
 [Edit this page on GitHub](https://github.com/sveltejs/svelte/edit/main/documentation/docs/99-legacy/21-legacy-$$slots.md)  [llms.txt](/docs/svelte/legacy-$$slots/llms.txt)

previous next

# Citations

1. Source page: https://svelte.dev/docs/svelte/legacy-$$slots
