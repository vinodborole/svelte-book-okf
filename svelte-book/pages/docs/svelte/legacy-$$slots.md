---
type: Web Page
title: $$slots • Svelte Docs
description: $$slots • Svelte documentation
resource: https://svelte.dev/docs/svelte/legacy-$$slots
timestamp: '2026-07-07T10:59:37.245126+00:00'
---

# $$slots

In runes mode, we know which snippets were provided to a component, as they're just normal props.

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
Edit this page on GitHub llms.txt

previous next

# Citations

1. Source page: https://svelte.dev/docs/svelte/legacy-$$slots
