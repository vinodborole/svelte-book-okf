---
type: Web Page
title: svelte/animate • Svelte Docs
description: svelte/animate • Svelte documentation
resource: https://svelte.dev/docs/svelte/svelte-animate
timestamp: '2026-07-07T10:59:37.245126+00:00'
---

# svelte/animate 

 `import { ````
function flip(node: Element, { from, to }: {
    from: DOMRect;
    to: DOMRect;
}, params?: FlipParams): AnimationConfig
```

The flip function calculates the start and end position of an element and animates between them, translating the x and y values.
`flip` stands for First, Last, Invert, Play.

flip } from 'svelte/animate';## flip

The flip function calculates the start and end position of an element and animates between them, translating the x and y values.
`flip` stands for First, Last, Invert, Play.

```
function flip(
	node: Element,
	{
		from,
		to
	}: {
		from: DOMRect;
		to: DOMRect;
	},
	params?: FlipParams
): AnimationConfig;
```
## AnimationConfig

`interface AnimationConfig {…}``delay?: number;``duration?: number;``easing?: (t: number) => number;``css?: (t: number, u: number) => string;``tick?: (t: number, u: number) => void;`## FlipParams

`interface FlipParams {…}``delay?: number;``duration?: number | ((len: number) => number);``easing?: (t: number) => number;`Edit this page on GitHub llms.txt

previous next

# Citations

1. Source page: https://svelte.dev/docs/svelte/svelte-animate
