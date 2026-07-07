---
type: Web Page
title: '{#key ...} • Svelte Docs'
description: '{#key ...} • Svelte documentation'
resource: https://svelte.dev/docs/svelte/key
timestamp: '2026-07-07T10:59:37.245126+00:00'
---

# {#key ...}

`{#key expression}...{/key}`Key blocks destroy and recreate their contents when the value of an expression changes. When used around components, this will cause them to be reinstantiated and reinitialised:

```
{#key value}
	<Component />
{/key}
```
It's also useful if you want a transition to play whenever a value changes:

```
{#key value}
	<div transition:fade>{value}</div>
{/key}
```
Edit this page on GitHub llms.txt

previous next

# Citations

1. Source page: https://svelte.dev/docs/svelte/key
