---
type: Web Page
title: Getting started • Svelte Docs
description: Getting started • Svelte documentation
resource: https://svelte.dev/docs/svelte/getting-started
timestamp: '2026-07-07T10:59:37.245126+00:00'
---

# Getting started

We recommend using SvelteKit, which lets you build almost anything. It's the official application framework from the Svelte team and powered by Vite. Create a new project with:

```
npx sv create myapp
cd myapp
npm install
npm run dev
```
Don't worry if you don't know Svelte yet! You can ignore all the nice features SvelteKit brings on top for now and dive into it later.

## Alternatives to SvelteKit

You can also use Svelte directly with Vite via vite-plugin-svelte by running `npm create vite@latest` and selecting the `svelte` option (or, if working with an existing project, adding the plugin to your `vite.config.js` file). With this, `npm run build` will generate HTML, JS, and CSS files inside the `dist` directory. In most cases, you will probably need to choose a routing library as well.

Vite is often used in standalone mode to build single page apps (SPAs), which you can also build with SvelteKit.

There are also plugins for other bundlers, but we recommend Vite.

## Editor tooling

The Svelte team maintains a VS Code extension, and there are integrations with various other editors and tools as well.

You can also check your code from the command line using `npx sv check`.

## Getting help

Don't be shy about asking for help in the Discord chatroom! You can also find answers on Stack Overflow.

Edit this page on GitHub llms.txt

# Citations

1. Source page: https://svelte.dev/docs/svelte/getting-started
