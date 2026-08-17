---
type: Web Page
title: '{@render ...} • Svelte Docs'
description: '{@render ...} • Svelte documentation'
resource: https://svelte.dev/docs/svelte/@render
timestamp: '2026-08-17T06:25:40.913234+00:00'
---

# {@render ...}

To render a [snippet](snippet), use a `{@render ...}` tag.

```
{#snippet sum(a, b)}
	<p>{a} + {b} = {a + b}</p>
{/snippet}
{@render sum(1, 2)}
{@render sum(3, 4)}
{@render sum(5, 6)}
```
The expression can be an identifier like `sum`, or an arbitrary JavaScript expression:

`{@render (cool ? coolSnippet : lameSnippet)()}`
## Optional snippets

If the snippet is potentially undefined — for example, because it’s an incoming prop — then you can use optional chaining to only render it when it *is* defined:

`{@render children?.()}`
Alternatively, use an [`{#if ...}`](if) block with an `:else` clause to render fallback content:

```
{#if children}
	{@render children()}
{:else}
	<p>fallback content</p>
{/if}
```
 [Edit this page on GitHub](https://github.com/sveltejs/svelte/edit/main/documentation/docs/03-template-syntax/07-@render.md)  [llms.txt](/docs/svelte/@render/llms.txt)

previous next

# Citations

1. Source page: https://svelte.dev/docs/svelte/@render
