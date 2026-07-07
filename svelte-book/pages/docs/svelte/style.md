---
type: Web Page
title: 'style: • Svelte Docs'
description: 'style: • Svelte documentation'
resource: https://svelte.dev/docs/svelte/style
timestamp: '2026-07-07T10:59:37.245126+00:00'
---

# style:

The `style:` directive provides a shorthand for setting multiple styles on an element.

```
<!-- These are equivalent -->
<div style:color="red">...</div>
<div style="color: red;">...</div>
```
The value can contain arbitrary expressions:

`<div style:color={myColor}>...</div>`The shorthand form is allowed:

`<div style:color>...</div>`Multiple styles can be set on a single element:

`<div style:color style:width="12rem" style:background-color={darkMode ? 'black' : 'white'}>...</div>`To mark a style as important, use the `|important` modifier:

`<div style:color|important="red">...</div>`When `style:` directives are combined with `style` attributes, the directives will take precedence,
even over `!important` properties:

```
<div style:color="red" style="color: blue">This will be red</div>
<div style:color="red" style="color: blue !important">This will still be red</div>
```
You can set CSS custom properties:

`<div style:--columns={columns}>...</div>`

# Citations

1. Source page: https://svelte.dev/docs/svelte/style
