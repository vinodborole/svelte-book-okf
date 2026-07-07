---
type: Web Page
title: '{@html ...} • Svelte Docs'
description: '{@html ...} • Svelte documentation'
resource: https://svelte.dev/docs/svelte/@html
timestamp: '2026-07-07T10:59:37.245126+00:00'
---

# {@html ...}

To inject raw HTML into your component, use the `{@html ...}` tag:

```
<article>
	{@html content}
</article>
```
Make sure that you either escape the passed string or only populate it with values that are under your control in order to prevent XSS attacks. Never render unsanitized content.

The expression should be valid standalone HTML — this will not work, because `</div>` is not valid HTML:

`{@html '<div>'}content{@html '</div>'}`It also will not compile Svelte code.

## Styling

Content rendered this way is 'invisible' to Svelte and as such will not receive scoped styles. In other words, this will not work, and the `a` and `img` styles will be regarded as unused:

```
<article>
	{@html content}
</article>
<style>
	article {
		a { color: hotpink }
		img { width: 100% }
	}
</style>
```
Instead, use the `:global` modifier to target everything inside the `<article>`:

```
<style>
	article :global {
		a { color: hotpink }
		img { width: 100% }
	}
</style>
```
Edit this page on GitHub llms.txt

previous next

# Citations

1. Source page: https://svelte.dev/docs/svelte/@html
