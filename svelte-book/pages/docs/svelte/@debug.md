---
type: Web Page
title: '{@debug ...} • Svelte Docs'
description: '{@debug ...} • Svelte documentation'
resource: https://svelte.dev/docs/svelte/@debug
timestamp: '2026-07-07T10:59:37.245126+00:00'
---

# {@debug ...}

The `{@debug ...}` tag offers an alternative to `console.log(...)`. It logs the values of specific variables whenever they change, and pauses code execution if you have devtools open.

```
<script>
	let user = {
		firstname: 'Ada',
		lastname: 'Lovelace'
	};
</script>
{@debug user}
<h1>Hello {user.firstname}!</h1>
```
`{@debug ...}` accepts a comma-separated list of variable names (not arbitrary expressions).

```
<!-- Compiles -->
{@debug user}
{@debug user1, user2, user3}
<!-- WON'T compile -->
{@debug user.firstname}
{@debug myArray[0]}
{@debug !isReady}
{@debug typeof user === 'object'}
```
The `{@debug}` tag without any arguments will insert a `debugger` statement that gets triggered when *any* state changes, as opposed to the specified variables.

Edit this page on GitHub llms.txt

previous next

# Citations

1. Source page: https://svelte.dev/docs/svelte/@debug
