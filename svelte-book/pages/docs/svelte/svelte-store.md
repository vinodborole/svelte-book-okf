---
type: Web Page
title: svelte/store • Svelte Docs
description: svelte/store • Svelte documentation
resource: https://svelte.dev/docs/svelte/svelte-store
timestamp: '2026-07-09T12:17:00.027378+00:00'
---

# svelte/store 

 ```
import {
	
```
`function derived<S extends Stores, T>(stores: S, fn: (values: StoresValues<S>, set: (value: T) => void, update: (fn: Updater<T>) => void) => Unsubscriber | void, initial_value?: T | undefined): Readable<T> (+1 overload)`Derived value store by synchronizing one or more readable stores and
applying an aggregation function over its input values.

derived,
	```
function fromStore<V>(store: Writable<V>): {
    current: V;
} (+1 overload)
```

`function get<T>(store: Readable<T>): T`Get the current value from a store by subscribing and immediately unsubscribing.

get,
	`function readable<T>(value?: T | undefined, start?: StartStopNotifier<T> | undefined): Readable<T>`Creates a `Readable` store that allows reading by subscription.

readable,
	`function readonly<T>(store: Readable<T>): Readable<T>`Takes a store and returns a new one derived from the old one that is readable.

readonly,
	`function toStore<V>(get: () => V, set: (v: V) => void): Writable<V> (+1 overload)`toStore,
	`function writable<T>(value?: T | undefined, start?: StartStopNotifier<T> | undefined): Writable<T>`Create a `Writable` store that allows both updating and reading by subscription.

writable
} from 'svelte/store';## derived

Derived value store by synchronizing one or more readable stores and applying an aggregation function over its input values.

```
function derived<S extends Stores, T>(
	stores: S,
	fn: (
		values: StoresValues<S>,
		set: (value: T) => void,
		update: (fn: Updater<T>) => void
	) => Unsubscriber | void,
	initial_value?: T | undefined
): Readable<T>;
```
```
function derived<S extends Stores, T>(
	stores: S,
	fn: (values: StoresValues<S>) => T,
	initial_value?: T | undefined
): Readable<T>;
```
## fromStore

```
function fromStore<V>(store: Writable<V>): {
	current: V;
};
```
```
function fromStore<V>(store: Readable<V>): {
	readonly current: V;
};
```
## get

Get the current value from a store by subscribing and immediately unsubscribing.

`function get<T>(store: Readable<T>): T;`## readable

Creates a `Readable` store that allows reading by subscription.

```
function readable<T>(
	value?: T | undefined,
	start?: StartStopNotifier<T> | undefined
): Readable<T>;
```
## readonly

Takes a store and returns a new one derived from the old one that is readable.

`function readonly<T>(store: Readable<T>): Readable<T>;`## toStore

```
function toStore<V>(
	get: () => V,
	set: (v: V) => void
): Writable<V>;
```
`function toStore<V>(get: () => V): Readable<V>;`## writable

Create a `Writable` store that allows both updating and reading by subscription.

```
function writable<T>(
	value?: T | undefined,
	start?: StartStopNotifier<T> | undefined
): Writable<T>;
```
## Readable

Readable interface for subscribing.

`interface Readable<T> {…}``subscribe(this: void, run: Subscriber<T>, invalidate?: () => void): Unsubscriber;`- `run`subscription callback
- `invalidate`cleanup callback

Subscribe on value changes.

## StartStopNotifier

Start and stop notification callbacks. This function is called when the first subscriber subscribes.

```
type StartStopNotifier<T> = (
	set: (value: T) => void,
	update: (fn: Updater<T>) => void
) => void | (() => void);
```
## Subscriber

Callback to inform of a value updates.

`type Subscriber<T> = (value: T) => void;`## Unsubscriber

Unsubscribes from value updates.

`type Unsubscriber = () => void;`## Updater

Callback to update a value.

`type Updater<T> = (value: T) => T;`## Writable

Writable interface for both updating and subscribing.

`interface Writable<T> extends Readable<T> {…}``set(this: void, value: T): void;`- `value`to set

Set value and inform subscribers.

`update(this: void, updater: Updater<T>): void;`- `updater`callback

Update value using callback and inform subscribers.

[ Edit this page on GitHub](https://github.com/sveltejs/svelte/edit/main/documentation/docs/98-reference/21-svelte-store.md) [ llms.txt](/docs/svelte/svelte-store/llms.txt)

# Citations

1. Source page: https://svelte.dev/docs/svelte/svelte-store
