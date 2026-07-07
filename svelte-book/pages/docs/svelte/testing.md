---
type: Web Page
title: Testing • Svelte Docs
description: Testing • Svelte documentation
resource: https://svelte.dev/docs/svelte/testing
timestamp: '2026-07-07T10:59:37.245126+00:00'
---

# Testing

Testing helps you write and maintain your code and guard against regressions. Testing frameworks help you with that, allowing you to describe assertions or expectations about how your code should behave. Svelte is unopinionated about which testing framework you use — you can write unit tests, integration tests, and end-to-end tests using solutions like Vitest, Jasmine, Cypress and Playwright.

## Unit and component tests with Vitest

Unit tests allow you to test small isolated parts of your code. Integration tests allow you to test parts of your application to see if they work together. If you're using Vite (including via SvelteKit), we recommend using Vitest. You can use the Svelte CLI to setup Vitest either during project creation or later on.

To setup Vitest manually, first install it:

`npm install -D vitest`Then adjust your `vite.config.js`:

`import { ``function defineConfig(config: UserConfig): UserConfig (+4 overloads)`defineConfig } from 'vitest/config';
export default `function defineConfig(config: UserConfig): UserConfig (+4 overloads)`defineConfig({
	// ...
	// Tell Vitest to use the `browser` entry points in `package.json` files, even though it's running in Node
	`resolve?: AllResolveOptions | undefined`resolve: `var process: NodeJS.Process`process.`NodeJS.Process.env: NodeJS.ProcessEnv`The `process.env` property returns an object containing the user environment.
See `environ(7)`.

An example of this object looks like:

```
{
  TERM: 'xterm-256color',
  SHELL: '/usr/local/bin/bash',
  USER: 'maciej',
  PATH: '~/.bin/:/usr/bin:/bin:/usr/sbin:/sbin:/usr/local/bin',
  PWD: '/Users/maciej',
  EDITOR: 'vim',
  SHLVL: '1',
  HOME: '/Users/maciej',
  LOGNAME: 'maciej',
  _: '/usr/local/bin/node'
}
```

It is possible to modify this object, but such modifications will not be
reflected outside the Node.js process, or (unless explicitly requested)
to other `Worker` threads.
In other words, the following example would not work:

`node -e 'process.env.foo = "bar"' && echo $foo`

While the following will:

```
import { env } from 'node:process';
env.foo = 'bar';
console.log(env.foo);
```

Assigning a property on `process.env` will implicitly convert the value
to a string. **This behavior is deprecated.** Future versions of Node.js may
throw an error when the value is not a string, number, or boolean.

```
import { env } from 'node:process';
env.test = null;
console.log(env.test);
// => 'null'
env.test = undefined;
console.log(env.test);
// => 'undefined'
```

Use `delete` to delete a property from `process.env`.

```
import { env } from 'node:process';
env.TEST = 1;
delete env.TEST;
console.log(env.TEST);
// => undefined
```

On Windows operating systems, environment variables are case-insensitive.

```
import { env } from 'node:process';
env.TEST = 1;
console.log(env.test);
// => 1
```

Unless explicitly specified when creating a `Worker` instance,
each `Worker` thread has its own copy of `process.env`, based on its
parent thread's `process.env`, or whatever was specified as the `env` option
to the `Worker` constructor. Changes to `process.env` will not be visible
across `Worker` threads, and only the main thread can make changes that
are visible to the operating system or to native add-ons. On Windows, a copy of `process.env` on a `Worker` instance operates in a case-sensitive manner
unlike the main thread.

env.`string | undefined`VITEST
		? {
				`EnvironmentResolveOptions.conditions?: string[] | undefined`conditions: ['browser']
			}
		: `var undefined`undefined
});If loading the browser version of all your packages is undesirable, because (for example) you also test backend libraries, you may need to resort to an alias configuration

You can now write unit tests for code inside your `.js/.ts` files:

```
import { flushSync } from 'svelte';
import { expect, test } from 'vitest';
import { multiplier } from './multiplier.svelte.js';
test('Multiplier', () => {
	let double = multiplier(0, 2);
	expect(double.value).toEqual(0);
	double.set(5);
	expect(double.value).toEqual(10);
});
```
```
/**
 * @param {number} initial
 * @param {number} k
 */
export function 
```
```
function multiplier(initial: number, k: number): {
    readonly value: number;
    set: (c: number) => void;
}
```

`initial: number`initial, `k: number`k) {
	let `let count: number`count = ```
function $state<number>(initial: number): number (+1 overload)
namespace $state
```

Declares reactive state.

Example:

`let count = $state(0);`

$state(`initial: number`initial);
	return {
		get `value: number`value() {
			return `let count: number`count * `k: number`k;
		},
		/** @param {number} c */
		`set: (c: number) => void`set: (`c: number`c) => {
			`let count: number`count = `c: number`c;
		}
	};
}`export function ````
function multiplier(initial: number, k: number): {
    readonly value: number;
    set: (c: number) => void;
}
```

`initial: number`initial: number, `k: number`k: number) {
	let `let count: number`count = ```
function $state<number>(initial: number): number (+1 overload)
namespace $state
```

Declares reactive state.

Example:

`let count = $state(0);`

$state(`initial: number`initial);
	return {
		get `value: number`value() {
			return `let count: number`count * `k: number`k;
		},
		`set: (c: number) => void`set: (`c: number`c: number) => {
			`let count: number`count = `c: number`c;
		}
	};
}### Using runes inside your test files

Since Vitest processes your test files the same way as your source files, you can use runes inside your tests as long as the filename includes `.svelte`:

```
import { flushSync } from 'svelte';
import { expect, test } from 'vitest';
import { multiplier } from './multiplier.svelte.js';
test('Multiplier', () => {
	let count = $state(0);
	let double = multiplier(() => count, 2);
	expect(double.value).toEqual(0);
	count = 5;
	expect(double.value).toEqual(10);
});
```
```
/**
 * @param {() => number} getCount
 * @param {number} k
 */
export function 
```
```
function multiplier(getCount: () => number, k: number): {
    readonly value: number;
}
```

`getCount: () => number`getCount, `k: number`k) {
	return {
		get `value: number`value() {
			return `getCount: () => number`getCount() * `k: number`k;
		}
	};
}`export function ````
function multiplier(getCount: () => number, k: number): {
    readonly value: number;
}
```

`getCount: () => number`getCount: () => number, `k: number`k: number) {
	return {
		get `value: number`value() {
			return `getCount: () => number`getCount() * `k: number`k;
		}
	};
}If the code being tested uses effects, you need to wrap the test inside `$effect.root`:

```
import { flushSync } from 'svelte';
import { expect, test } from 'vitest';
import { logger } from './logger.svelte.js';
test('Effect', () => {
	const cleanup = $effect.root(() => {
		let count = $state(0);
		// logger uses an $effect to log updates of its input
		let log = logger(() => count);
		// effects normally run after a microtask,
		// use flushSync to execute all pending effects synchronously
		flushSync();
		expect(log).toEqual([0]);
		count = 1;
		flushSync();
		expect(log).toEqual([0, 1]);
	});
	cleanup();
});
```
```
/**
 * @param {() => any} getValue
 */
export function 
```
`function logger(getValue: () => any): any[]`logger(`getValue: () => any`getValue) {
	/** @type {any[]} */
	let `let log: any[]`log = [];
	```
function $effect(fn: () => void | (() => void)): void
namespace $effect
```

Runs code when a component is mounted to the DOM, and then whenever its dependencies change, i.e. `$state` or `$derived` values.
The timing of the execution is after the DOM has been updated.

Example:

`$effect(() => console.log('The count is now ' + count));`

If you return a function from the effect, it will be called right before the effect is run again, or when the component is unmounted.

Does not run during server-side rendering.

$effect(() => {
		`let log: any[]`log.`Array<any>.push(...items: any[]): number`Appends new elements to the end of an array, and returns the new length of the array.

push(`getValue: () => any`getValue());
	});
	return `let log: any[]`log;
}`export function ``function logger(getValue: () => any): any[]`logger(`getValue: () => any`getValue: () => any) {
	let `let log: any[]`log: any[] = [];
	```
function $effect(fn: () => void | (() => void)): void
namespace $effect
```

Runs code when a component is mounted to the DOM, and then whenever its dependencies change, i.e. `$state` or `$derived` values.
The timing of the execution is after the DOM has been updated.

Example:

`$effect(() => console.log('The count is now ' + count));`

If you return a function from the effect, it will be called right before the effect is run again, or when the component is unmounted.

Does not run during server-side rendering.

$effect(() => {
		`let log: any[]`log.`Array<any>.push(...items: any[]): number`Appends new elements to the end of an array, and returns the new length of the array.

push(`getValue: () => any`getValue());
	});
	return `let log: any[]`log;
}### Component testing

It is possible to test your components in isolation, which allows you to render them in a browser (real or simulated), simulate behavior, and make assertions, without spinning up your whole app.

Before writing component tests, think about whether you actually need to test the component, or if it's more about the logic

insidethe component. If so, consider extracting out that logic to test it in isolation, without the overhead of a component.

To get started, install jsdom (a library that shims DOM APIs):

`npm install -D jsdom`Then adjust your `vite.config.js`:

`import { ``function defineConfig(config: UserConfig): UserConfig (+4 overloads)`defineConfig } from 'vitest/config';
export default `function defineConfig(config: UserConfig): UserConfig (+4 overloads)`defineConfig({
	`UserConfig.plugins?: PluginOption[] | undefined`Array of vite plugins to use.

plugins: [
		/* ... */
	],
	`UserConfig.test?: InlineConfig | undefined`Options for Vitest

test: {
		// If you are testing components client-side, you need to set up a DOM environment.
		// If not all your files should have this environment, you can use a
		// `// @vitest-environment jsdom` comment at the top of the test files instead.
		`InlineConfig.environment?: VitestEnvironment | undefined`Running environment

Supports 'node', 'jsdom', 'happy-dom', 'edge-runtime'

If used unsupported string, will try to load the package `vitest-environment-${env}`

environment: 'jsdom'
	},
	// Tell Vitest to use the `browser` entry points in `package.json` files, even though it's running in Node
	`resolve?: AllResolveOptions | undefined`resolve: `var process: NodeJS.Process`process.`NodeJS.Process.env: NodeJS.ProcessEnv`The `process.env` property returns an object containing the user environment.
See `environ(7)`.

An example of this object looks like:

```
{
  TERM: 'xterm-256color',
  SHELL: '/usr/local/bin/bash',
  USER: 'maciej',
  PATH: '~/.bin/:/usr/bin:/bin:/usr/sbin:/sbin:/usr/local/bin',
  PWD: '/Users/maciej',
  EDITOR: 'vim',
  SHLVL: '1',
  HOME: '/Users/maciej',
  LOGNAME: 'maciej',
  _: '/usr/local/bin/node'
}
```

It is possible to modify this object, but such modifications will not be
reflected outside the Node.js process, or (unless explicitly requested)
to other `Worker` threads.
In other words, the following example would not work:

`node -e 'process.env.foo = "bar"' && echo $foo`

While the following will:

```
import { env } from 'node:process';
env.foo = 'bar';
console.log(env.foo);
```

Assigning a property on `process.env` will implicitly convert the value
to a string. **This behavior is deprecated.** Future versions of Node.js may
throw an error when the value is not a string, number, or boolean.

```
import { env } from 'node:process';
env.test = null;
console.log(env.test);
// => 'null'
env.test = undefined;
console.log(env.test);
// => 'undefined'
```

Use `delete` to delete a property from `process.env`.

```
import { env } from 'node:process';
env.TEST = 1;
delete env.TEST;
console.log(env.TEST);
// => undefined
```

On Windows operating systems, environment variables are case-insensitive.

```
import { env } from 'node:process';
env.TEST = 1;
console.log(env.test);
// => 1
```

Unless explicitly specified when creating a `Worker` instance,
each `Worker` thread has its own copy of `process.env`, based on its
parent thread's `process.env`, or whatever was specified as the `env` option
to the `Worker` constructor. Changes to `process.env` will not be visible
across `Worker` threads, and only the main thread can make changes that
are visible to the operating system or to native add-ons. On Windows, a copy of `process.env` on a `Worker` instance operates in a case-sensitive manner
unlike the main thread.

env.`string | undefined`VITEST
		? {
				`EnvironmentResolveOptions.conditions?: string[] | undefined`conditions: ['browser']
			}
		: `var undefined`undefined
});After that, you can create a test file in which you import the component to test, interact with it programmatically and write expectations about the results:

`import { ``function flushSync<T = void>(fn?: (() => T) | undefined): T`Synchronously flush any pending updates.
Returns void if no callback is provided, otherwise returns the result of calling the callback.

flushSync, `function mount<Props extends Record<string, any>, Exports extends Record<string, any>>(component: ComponentType<SvelteComponent<Props>> | Component<Props, Exports, any>, options: MountOptions<Props>): Exports`Mounts a component to the given target and returns the exports and potentially the props (if compiled with `accessors: true`) of the component.
Transitions will play during the initial render unless the `intro` option is set to `false`.

mount, ```
function unmount(component: Record<string, any>, options?: {
    outro?: boolean;
} | undefined): Promise<void>
```

Unmounts a component that was previously mounted using `mount` or `hydrate`.

Since 5.13.0, if `options.outro` is `true`, transitions will play before the component is removed from the DOM.

Returns a `Promise` that resolves after transitions have completed if `options.outro` is true, or immediately otherwise (prior to 5.13.0, returns `void`).

```
import { mount, unmount } from 'svelte';
import App from './App.svelte';
const app = mount(App, { target: document.body });
// later...
unmount(app, { outro: true });
```

unmount } from 'svelte';
import { `const expect: ExpectStatic`expect, `const test: TestAPI`Defines a test case with a given name and test function. The test function can optionally be configured with test options.

test } from 'vitest';
import ```
type Component = SvelteComponent<Record<string, any>, any, any>
const Component: LegacyComponentType
```

`test<object>(name: string | Function, fn?: TestFunction<object> | undefined, options?: number): void (+1 overload)`Defines a test case with a given name and test function. The test function can optionally be configured with test options.

test('Component', () => {
	// Instantiate the component using Svelte's `mount` API
	const ```
const component: {
    $on?(type: string, callback: (e: any) => void): () => void;
    $set?(props: Partial<Record<string, any>>): void;
} & Record<string, any>
```

```
mount<Record<string, any>, {
    $on?(type: string, callback: (e: any) => void): () => void;
    $set?(props: Partial<Record<string, any>>): void;
} & Record<string, any>>(component: ComponentType<SvelteComponent<Record<string, any>, any, any>> | Component<Record<string, any>, {
    $on?(type: string, callback: (e: any) => void): () => void;
    $set?(props: Partial<Record<string, any>>): void;
} & Record<string, any>, any>, options: MountOptions<...>): {
    $on?(type: string, callback: (e: any) => void): () => void;
    $set?(props: Partial<Record<string, any>>): void;
} & Record<...>
```

Mounts a component to the given target and returns the exports and potentially the props (if compiled with `accessors: true`) of the component.
Transitions will play during the initial render unless the `intro` option is set to `false`.

mount(`const Component: LegacyComponentType`Component, {
		`target: Document | Element | ShadowRoot`Target element where the component will be mounted.

target: `var document: Document``window.document`

document.`Document.body: HTMLElement`The `Document.body``null` if no such element exists.

body, // `document` exists because of jsdom
		`props?: Record<string, any> | undefined`Component properties.

props: { `initial: number`initial: 0 }
	});
	`expect<string>(actual: string, message?: string): Assertion<string> (+1 overload)`expect(`var document: Document``window.document`

document.`Document.body: HTMLElement`The `Document.body``null` if no such element exists.

body.`Element.innerHTML: string`The `innerHTML`

innerHTML).`JestAssertion<string>.toBe: <string>(expected: string) => void`Checks that a value is what you expect. It calls `Object.is` to compare values.
Don't use `toBe` with floating-point numbers.

toBe('<button>0</button>');
	// Click the button, then flush the changes so you can synchronously write expectations
	`var document: Document``window.document`

document.`Document.body: HTMLElement`The `Document.body``null` if no such element exists.

body.`ParentNode.querySelector<"button">(selectors: "button"): HTMLButtonElement | null (+4 overloads)`Returns the first element that is a descendant of node that matches selectors.

querySelector('button')?.`HTMLElement.click(): void`The `HTMLElement.click()`

click();
	`flushSync<void>(fn?: (() => void) | undefined): void`Synchronously flush any pending updates.
Returns void if no callback is provided, otherwise returns the result of calling the callback.

flushSync();
	`expect<string>(actual: string, message?: string): Assertion<string> (+1 overload)`expect(`var document: Document``window.document`

document.`Document.body: HTMLElement`The `Document.body``null` if no such element exists.

body.`Element.innerHTML: string`The `innerHTML`

innerHTML).`JestAssertion<string>.toBe: <string>(expected: string) => void`Checks that a value is what you expect. It calls `Object.is` to compare values.
Don't use `toBe` with floating-point numbers.

toBe('<button>1</button>');
	// Remove the component from the DOM
	```
function unmount(component: Record<string, any>, options?: {
    outro?: boolean;
} | undefined): Promise<void>
```

Unmounts a component that was previously mounted using `mount` or `hydrate`.

Since 5.13.0, if `options.outro` is `true`, transitions will play before the component is removed from the DOM.

Returns a `Promise` that resolves after transitions have completed if `options.outro` is true, or immediately otherwise (prior to 5.13.0, returns `void`).

```
import { mount, unmount } from 'svelte';
import App from './App.svelte';
const app = mount(App, { target: document.body });
// later...
unmount(app, { outro: true });
```

unmount(```
const component: {
    $on?(type: string, callback: (e: any) => void): () => void;
    $set?(props: Partial<Record<string, any>>): void;
} & Record<string, any>
```

While the process is very straightforward, it is also low level and somewhat brittle, as the precise structure of your component may change frequently. Tools like @testing-library/svelte can help streamline your tests. The above test could be rewritten like this:

`import { ``function render<C extends Component<any, any, string> | SvelteComponent<any, any, any>, Q extends Queries = typeof import("/vercel/path0/node_modules/.pnpm/@testing-library+dom@10.4.1/node_modules/@testing-library/dom/types/queries")>(Component: ComponentImport<C>, options?: ComponentOptions<C>, renderOptions?: RenderOptions<Q>): RenderResult<C, Q>`Render a component into the document.

render, `const screen: Screen<typeof import("/vercel/path0/node_modules/.pnpm/@testing-library+dom@10.4.1/node_modules/@testing-library/dom/types/queries")>`screen } from '@testing-library/svelte';
import ```
const userEvent: {
    readonly setup: typeof setupMain;
    readonly clear: typeof clear;
    readonly click: typeof click;
    readonly copy: typeof copy;
    readonly cut: typeof cut;
    readonly dblClick: typeof dblClick;
    readonly deselectOptions: typeof deselectOptions;
    readonly hover: typeof hover;
    readonly keyboard: typeof keyboard;
    ... 7 more ...;
    readonly tab: typeof tab;
}
```

`const expect: ExpectStatic`expect, `const test: TestAPI`Defines a test case with a given name and test function. The test function can optionally be configured with test options.

test } from 'vitest';
import ```
type Component = SvelteComponent<Record<string, any>, any, any>
const Component: LegacyComponentType
```

`test<object>(name: string | Function, fn?: TestFunction<object> | undefined, options?: number): void (+1 overload)`Defines a test case with a given name and test function. The test function can optionally be configured with test options.

test('Component', async () => {
	const `const user: UserEvent`user = ```
const userEvent: {
    readonly setup: typeof setupMain;
    readonly clear: typeof clear;
    readonly click: typeof click;
    readonly copy: typeof copy;
    readonly cut: typeof cut;
    readonly dblClick: typeof dblClick;
    readonly deselectOptions: typeof deselectOptions;
    readonly hover: typeof hover;
    readonly keyboard: typeof keyboard;
    ... 7 more ...;
    readonly tab: typeof tab;
}
```

`setup: (options?: Options) => UserEvent`Start a "session" with userEvent.
All APIs returned by this function share an input device state and a default configuration.

setup();
	`render<SvelteComponent<Record<string, any>, any, any>, typeof import("/vercel/path0/node_modules/.pnpm/@testing-library+dom@10.4.1/node_modules/@testing-library/dom/types/queries")>(Component: ComponentImport<SvelteComponent<Record<string, any>, any, any>>, options?: ComponentOptions<SvelteComponent<Record<string, any>, any, any>> | undefined, renderOptions?: RenderOptions<typeof import("/vercel/path0/node_modules/.pnpm/@testing-library+dom@10.4.1/node_modules/@testing-library/dom/types/queries")> | undefined): RenderResult<...>`Render a component into the document.

render(`const Component: LegacyComponentType`Component);
	const `const button: HTMLElement`button = `const screen: Screen<typeof import("/vercel/path0/node_modules/.pnpm/@testing-library+dom@10.4.1/node_modules/@testing-library/dom/types/queries")>`screen.`getByRole<HTMLElement>(role: ByRoleMatcher, options?: ByRoleOptions | undefined): HTMLElement (+1 overload)`getByRole('button');
	`expect<HTMLElement>(actual: HTMLElement, message?: string): Assertion<HTMLElement> (+1 overload)`expect(`const button: HTMLElement`button).toHaveTextContent(0);
	await `const user: UserEvent`user.`click: (element: Element) => Promise<void>`click(`const button: HTMLElement`button);
	`expect<HTMLElement>(actual: HTMLElement, message?: string): Assertion<HTMLElement> (+1 overload)`expect(`const button: HTMLElement`button).toHaveTextContent(1);
});When writing component tests that involve two-way bindings, context or snippet props, it's best to create a wrapper component for your specific test and interact with that. `@testing-library/svelte` contains some examples.

## Component tests with Storybook

Storybook is a tool for developing and documenting UI components, and it can also be used to test your components. They're run with Vitest's browser mode, which renders your components in a real browser for the most realistic testing environment.

To get started, first install Storybook (using Svelte's CLI) in your project via `npx sv add storybook` and choose the recommended configuration that includes testing features. If you're already using Storybook, and for more information on Storybook's testing capabilities, follow the Storybook testing docs to get started.

You can create stories for component variations and test interactions with the play function, which allows you to simulate behavior and make assertions using the Testing Library and Vitest APIs. Here's an example of two stories that can be tested, one that renders an empty LoginForm component and one that simulates a user filling out the form:

```
<script module>
	import { defineMeta } from '@storybook/addon-svelte-csf';
	import { expect, fn } from 'storybook/test';
	import LoginForm from './LoginForm.svelte';
	const { Story } = defineMeta({
		component: LoginForm,
		args: {
			// Pass a mock function to the `onSubmit` prop
			onSubmit: fn(),
		}
	});
</script>
<Story name="Empty Form" />
<Story
	name="Filled Form"
	play={async ({ args, canvas, userEvent }) => {
		// Simulate a user filling out the form
		await userEvent.type(canvas.getByTestId('email'), 'email@provider.com');
		await userEvent.type(canvas.getByTestId('password'), 'a-random-password');
		await userEvent.click(canvas.getByRole('button'));
		// Run assertions
		await expect(args.onSubmit).toHaveBeenCalledTimes(1);
		await expect(canvas.getByText('You’re in!')).toBeInTheDocument();
	}}
/>
```
## End-to-end tests with Playwright

E2E (short for 'end to end') tests allow you to test your full application through the eyes of the user. This section uses Playwright as an example, but you can also use other solutions like Cypress or NightwatchJS.

You can use the Svelte CLI to setup Playwright either during project creation or later on. You can also set it up with `npm init playwright`. Additionally, you may also want to install an IDE plugin such as the VS Code extension to be able to execute tests from inside your IDE.

If you've run `npm init playwright` or are not using Vite, you may need to adjust the Playwright config to tell Playwright what to do before running the tests — mainly starting your application at a certain port. For example:

`const ````
const config: {
    webServer: {
        command: string;
        port: number;
    };
    testDir: string;
    testMatch: RegExp;
}
```

```
webServer: {
    command: string;
    port: number;
}
```

`command: string`command: 'npm run build && npm run preview',
		`port: number`port: 4173
	},
	`testDir: string`testDir: 'tests',
	`testMatch: RegExp`testMatch: /(.+\.)?(test|spec)\.[jt]s/
};
export default ```
const config: {
    webServer: {
        command: string;
        port: number;
    };
    testDir: string;
    testMatch: RegExp;
}
```

You can now start writing tests. These are totally unaware of Svelte as a framework, so you mainly interact with the DOM and write assertions.

`import { ``import expect`expect, `import test`test } from '@playwright/test';
`import test`test('home page has expected h1', async ({ page }) => {
	await `page: any`page.goto('/');
	await `import expect`expect(`page: any`page.locator('h1')).toBeVisible();
});Edit this page on GitHub llms.txt

# Citations

1. Source page: https://svelte.dev/docs/svelte/testing
