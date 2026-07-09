---
type: Web Page
title: Browser support • Svelte Docs
description: Browser support • Svelte documentation
resource: https://svelte.dev/docs/svelte/browser-support
timestamp: '2026-07-09T12:17:00.027378+00:00'
---

# Browser support

The table below shows the minimum browser versions Svelte is expected to work in, derived from the browser APIs used by Svelte's internal code.

| Browser | Minimum version | 
|---|---|
| Chrome/Edge | 87 | 
| Firefox | 83 | 
| Safari | 14 | 
| Opera | 73 | 
| Opera (Android) | 62 | 
| Samsung Internet | 14.0 | 
| Android WebView | 87 | 
| Internet Explorer | not supported | 

This equates to a

[Baseline](https://web-platform-dx.github.io/baseline/)target of 2020.

This table only covers Svelte itself. It does not include [SvelteKit](/docs/kit), other Svelte libraries, or your own code.

## Exceptions

A few Svelte features require a higher minimum browser version. You'll only need to take the following table into consideration if you use these specific features.

| Feature | Chrome/Edge | Firefox | Safari | 
|---|---|---|---|
| `$state.snapshot` | 98 | 94 | 15.4 | 
| `bind:devicePixelContentBoxSize` | — | 93 | not supported | 
| `flip`from`svelte/animate` | — | 126 | — | 

[ Edit this page on GitHub](https://github.com/sveltejs/svelte/edit/main/documentation/docs/07-misc/05-browser-support.md) [ llms.txt](/docs/svelte/browser-support/llms.txt)

previous next

# Citations

1. Source page: https://svelte.dev/docs/svelte/browser-support
