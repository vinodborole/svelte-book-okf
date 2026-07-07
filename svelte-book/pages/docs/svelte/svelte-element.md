---
type: Web Page
title: <svelte:element> • Svelte Docs
description: <svelte:element> • Svelte documentation
resource: https://svelte.dev/docs/svelte/svelte-element
timestamp: '2026-07-07T10:59:37.245126+00:00'
---

# <svelte:element>

`<svelte:element this={expression} />`The `<svelte:element>` element lets you render an element that is unknown at author time, for example because it comes from a CMS. Any properties and event listeners present will be applied to the element.

The only supported binding is `bind:this`, since Svelte's built-in bindings do not work with generic elements.

If `this` has a nullish value, the element and its children will not be rendered.

If `this` is the name of a void element (e.g., `br`) and `<svelte:element>` has child elements, a runtime error will be thrown in development mode:

```
<script>
	let tag = $state('hr');
</script>
<svelte:element this={tag}>
	This text cannot appear inside an hr element
</svelte:element>
```
Svelte tries its best to infer the correct namespace from the element's surroundings, but it's not always possible. You can make it explicit with an `xmlns` attribute:

`<svelte:element this={tag} xmlns="http://www.w3.org/2000/svg" />``this` needs to be a valid DOM element tag, things like `#text` or `svelte:head` will not work.

Edit this page on GitHub llms.txt

# Citations

1. Source page: https://svelte.dev/docs/svelte/svelte-element
