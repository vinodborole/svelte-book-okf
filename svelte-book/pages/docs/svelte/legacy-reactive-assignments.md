---
type: Web Page
title: 'Reactive $: statements • Svelte Docs'
description: 'Reactive $: statements • Svelte documentation'
resource: https://svelte.dev/docs/svelte/legacy-reactive-assignments
timestamp: '2026-07-07T10:59:37.245126+00:00'
---

# Reactive $: statements

In runes mode, reactions to state updates are handled with the `$derived` and `$effect` runes.

In legacy mode, any top-level statement (i.e. not inside a block or a function) can be made reactive by prefixing it with a `$:` label. These statements run after other code in the `<script>` and before the component markup is rendered, then whenever the values that they depend on change.

```
<script>
	let a = 1;
	let b = 2;
	// this is a 'reactive statement', and it will re-run
	// when `a`, `b` or `sum` change
	$: console.log(`${a} + ${b} = ${sum}`);
	// this is a 'reactive assignment' — `sum` will be
	// recalculated when `a` or `b` change. It is
	// not necessary to declare `sum` separately
	$: sum = a + b;
</script>
```
Statements are ordered *topologically* by their dependencies and their assignments: since the `console.log` statement depends on `sum`, `sum` is calculated first even though it appears later in the source.

Multiple statements can be combined by putting them in a block:

```
$: {
	// recalculate `total` when `items` changes
	total = 0;
	for (const 
```
`const item: any`item of items) {
		total += `const item: any`item.value;
	}
}The left-hand side of a reactive assignments can be an identifier, or it can be a destructuring assignment:

`$: ({ ``larry: any`larry, `moe: any`moe, `curly: any`curly } = stooges);## Understanding dependencies

The dependencies of a `$:` statement are determined at compile time — they are whichever variables are referenced (but not assigned to) inside the statement.

In other words, a statement like this will *not* re-run when `count` changes, because the compiler cannot 'see' the dependency:

`let ``let count: number`count = 0;
let `let double: () => number`double = () => `let count: number`count * 2;
$: doubled = `let double: () => number`double();Similarly, topological ordering will fail if dependencies are referenced indirectly: `z` will never update, because `y` is not considered 'dirty' when the update occurs. Moving `$: z = y` below `$: setY(x)` will fix it:

```
<script>
	let x = 0;
	let y = 0;
	$: z = y;
	$: setY(x);
	function setY(value) {
		y = value;
	}
</script>
```
## Browser-only code

Reactive statements run during server-side rendering as well as in the browser. This means that any code that should only run in the browser must be wrapped in an `if` block:

```
$: if (browser) {
	
```
`var document: Document``window.document`

document.`Document.title: string`The `document.title`

title = title;
}Edit this page on GitHub llms.txt

# Citations

1. Source page: https://svelte.dev/docs/svelte/legacy-reactive-assignments
