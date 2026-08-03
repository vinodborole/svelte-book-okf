---
type: Web Page
title: <svelte:fragment> • Svelte Docs
description: <svelte:fragment> • Svelte documentation
resource: https://svelte.dev/docs/svelte/legacy-svelte-fragment
timestamp: '2026-08-03T08:54:23.898986+00:00'
---

# <svelte:fragment>

The `<svelte:fragment>` element allows you to place content in a [named slot](legacy-slots) without wrapping it in a container DOM element. This keeps the flow layout of your document intact.

Widget

```
<div>
	<slot name="header">No header was provided</slot>
	<p>Some content between header and footer</p>
	<slot name="footer" />
</div>
```
App

```
<script>
	import Widget from './Widget.svelte';
</script>
<Widget>
	<h1 slot="header">Hello</h1>
	<svelte:fragment slot="footer">
		<p>All rights reserved.</p>
		<p>Copyright (c) 2019 Svelte Industries</p>
	</svelte:fragment>
</Widget>
```
```
<script lang="ts">
	import Widget from './Widget.svelte';
</script>
<Widget>
	<h1 slot="header">Hello</h1>
	<svelte:fragment slot="footer">
		<p>All rights reserved.</p>
		<p>Copyright (c) 2019 Svelte Industries</p>
	</svelte:fragment>
</Widget>
```
In Svelte 5+, this concept is obsolete, as snippets don't create a wrapping element

 [Edit this page on GitHub](https://github.com/sveltejs/svelte/edit/main/documentation/docs/99-legacy/22-legacy-svelte-fragment.md)  [llms.txt](/docs/svelte/legacy-svelte-fragment/llms.txt)

previous next

# Citations

1. Source page: https://svelte.dev/docs/svelte/legacy-svelte-fragment
