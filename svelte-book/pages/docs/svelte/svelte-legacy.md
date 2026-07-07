---
type: Web Page
title: svelte/legacy • Svelte Docs
description: svelte/legacy • Svelte documentation
resource: https://svelte.dev/docs/svelte/svelte-legacy
timestamp: '2026-07-07T10:59:37.245126+00:00'
---

# svelte/legacy 

 This module provides various functions for use during the migration, since some features can't be replaced one to one with new features. All imports are marked as deprecated and should be migrated away from over time.

```
import {
	
```
`function asClassComponent<Props extends Record<string, any>, Exports extends Record<string, any>, Events extends Record<string, any>, Slots extends Record<string, any>>(component: SvelteComponent<Props, Events, Slots> | Component<Props>): ComponentType<SvelteComponent<Props, Events, Slots> & Exports>`Takes the component function and returns a Svelte 4 compatible component constructor.

asClassComponent,
	`function createBubbler(): (type: string) => (event: Event) => boolean`Function to create a `bubble` function that mimic the behavior of `on:click` without handler available in svelte 4.

createBubbler,
	```
function createClassComponent<Props extends Record<string, any>, Exports extends Record<string, any>, Events extends Record<string, any>, Slots extends Record<string, any>>(options: ComponentConstructorOptions<Props> & {
    component: ComponentType<SvelteComponent<Props, Events, Slots>> | Component<Props>;
}): SvelteComponent<Props, Events, Slots> & Exports
```

Takes the same options as a Svelte 4 component and the component function and returns a Svelte 4 compatible component.

createClassComponent,
	`function handlers(...handlers: EventListener[]): EventListener`Function to mimic the multiple listeners available in svelte 4

run,
	`function self(fn: (event: Event, ...args: Array<unknown>) => void): (event: Event, ...args: unknown[]) => void`Substitute for the `self` event modifier

self,
	`function stopImmediatePropagation(fn: (event: Event, ...args: Array<unknown>) => void): (event: Event, ...args: unknown[]) => void`Substitute for the `stopImmediatePropagation` event modifier

stopImmediatePropagation,
	`function stopPropagation(fn: (event: Event, ...args: Array<unknown>) => void): (event: Event, ...args: unknown[]) => void`Substitute for the `stopPropagation` event modifier

stopPropagation,
	`function trusted(fn: (event: Event, ...args: Array<unknown>) => void): (event: Event, ...args: unknown[]) => void`Substitute for the `trusted` event modifier

trusted
} from 'svelte/legacy';## asClassComponent

Use this only as a temporary solution to migrate your imperative component code to Svelte 5.

Takes the component function and returns a Svelte 4 compatible component constructor.

```
function asClassComponent<
	Props extends Record<string, any>,
	Exports extends Record<string, any>,
	Events extends Record<string, any>,
	Slots extends Record<string, any>
>(
	component:
		| SvelteComponent<Props, Events, Slots>
		| Component<Props>
): ComponentType<
	SvelteComponent<Props, Events, Slots> & Exports
>;
```
## createBubbler

Use this only as a temporary solution to migrate your automatically delegated events in Svelte 5.

Function to create a `bubble` function that mimic the behavior of `on:click` without handler available in svelte 4.

```
function createBubbler(): (
	type: string
) => (event: Event) => boolean;
```
## createClassComponent

Use this only as a temporary solution to migrate your imperative component code to Svelte 5.

Takes the same options as a Svelte 4 component and the component function and returns a Svelte 4 compatible component.

```
function createClassComponent<
	Props extends Record<string, any>,
	Exports extends Record<string, any>,
	Events extends Record<string, any>,
	Slots extends Record<string, any>
>(
	options: ComponentConstructorOptions<Props> & {
		component:
			| ComponentType<SvelteComponent<Props, Events, Slots>>
			| Component<Props>;
	}
): SvelteComponent<Props, Events, Slots> & Exports;
```
## handlers

Function to mimic the multiple listeners available in svelte 4

```
function handlers(
	...handlers: EventListener[]
): EventListener;
```
## nonpassive

Substitute for the `nonpassive` event modifier, implemented as an action

```
function nonpassive(
	node: HTMLElement,
	[event, handler]: [
		event: string,
		handler: () => EventListener
	]
): void;
```
## once

Substitute for the `once` event modifier

```
function once(
	fn: (event: Event, ...args: Array<unknown>) => void
): (event: Event, ...args: unknown[]) => void;
```
## passive

Substitute for the `passive` event modifier, implemented as an action

```
function passive(
	node: HTMLElement,
	[event, handler]: [
		event: string,
		handler: () => EventListener
	]
): void;
```
## preventDefault

Substitute for the `preventDefault` event modifier

```
function preventDefault(
	fn: (event: Event, ...args: Array<unknown>) => void
): (event: Event, ...args: unknown[]) => void;
```
## run

Use this only as a temporary solution to migrate your component code to Svelte 5.

Runs the given function once immediately on the server, and works like `$effect.pre` on the client.

`function run(fn: () => void | (() => void)): void;`## self

Substitute for the `self` event modifier

```
function self(
	fn: (event: Event, ...args: Array<unknown>) => void
): (event: Event, ...args: unknown[]) => void;
```
## stopImmediatePropagation

Substitute for the `stopImmediatePropagation` event modifier

```
function stopImmediatePropagation(
	fn: (event: Event, ...args: Array<unknown>) => void
): (event: Event, ...args: unknown[]) => void;
```
## stopPropagation

Substitute for the `stopPropagation` event modifier

```
function stopPropagation(
	fn: (event: Event, ...args: Array<unknown>) => void
): (event: Event, ...args: unknown[]) => void;
```
## trusted

Substitute for the `trusted` event modifier

```
function trusted(
	fn: (event: Event, ...args: Array<unknown>) => void
): (event: Event, ...args: unknown[]) => void;
```
## LegacyComponentType

Support using the component as both a class and function during the transition period

```
type LegacyComponentType = {
	new (o: ComponentConstructorOptions): SvelteComponent;
	(
		...args: Parameters<Component<Record<string, any>>>
	): ReturnType<
		Component<Record<string, any>, Record<string, any>>
	>;
};
```
Edit this page on GitHub llms.txt

# Citations

1. Source page: https://svelte.dev/docs/svelte/svelte-legacy
