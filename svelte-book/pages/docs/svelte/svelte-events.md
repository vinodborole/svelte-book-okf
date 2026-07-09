---
type: Web Page
title: svelte/events • Svelte Docs
description: svelte/events • Svelte documentation
resource: https://svelte.dev/docs/svelte/svelte-events
timestamp: '2026-07-09T12:17:00.027378+00:00'
---

# svelte/events 

 `import { ````
function on<Type extends keyof WindowEventMap>(window: Window, type: Type, handler: (this: Window, event: WindowEventMap[Type] & {
    currentTarget: Window;
}) => any, options?: AddEventListenerOptions | undefined): () => void (+4 overloads)
```

Attaches an event handler to the window and returns a function that removes the handler. Using this
rather than `addEventListener` will preserve the correct order relative to handlers added declaratively
(with attributes like `onclick`), which use event delegation for performance reasons

on } from 'svelte/events';## on

Attaches an event handler to the window and returns a function that removes the handler. Using this
rather than `addEventListener` will preserve the correct order relative to handlers added declaratively
(with attributes like `onclick`), which use event delegation for performance reasons

```
function on<Type extends keyof WindowEventMap>(
	window: Window,
	type: Type,
	handler: (
		this: Window,
		event: WindowEventMap[Type] & { currentTarget: Window }
	) => any,
	options?: AddEventListenerOptions | undefined
): () => void;
```
```
function on<Type extends keyof DocumentEventMap>(
	document: Document,
	type: Type,
	handler: (
		this: Document,
		event: DocumentEventMap[Type] & {
			currentTarget: Document;
		}
	) => any,
	options?: AddEventListenerOptions | undefined
): () => void;
```
```
function on<
	Element extends HTMLElement,
	Type extends keyof HTMLElementEventMap
>(
	element: Element,
	type: Type,
	handler: (
		this: Element,
		event: HTMLElementEventMap[Type] & {
			currentTarget: Element;
		}
	) => any,
	options?: AddEventListenerOptions | undefined
): () => void;
```
```
function on<
	Element extends MediaQueryList,
	Type extends keyof MediaQueryListEventMap
>(
	element: Element,
	type: Type,
	handler: (
		this: Element,
		event: MediaQueryListEventMap[Type] & {
			currentTarget: Element;
		}
	) => any,
	options?: AddEventListenerOptions | undefined
): () => void;
```
```
function on(
	element: EventTarget,
	type: string,
	handler: EventListener,
	options?: AddEventListenerOptions | undefined
): () => void;
```
[ Edit this page on GitHub](https://github.com/sveltejs/svelte/edit/main/documentation/docs/98-reference/21-svelte-events.md) [ llms.txt](/docs/svelte/svelte-events/llms.txt)

previous next

# Citations

1. Source page: https://svelte.dev/docs/svelte/svelte-events
