# Browser components

Register independent DOM enhancements by selector with `build()`; use `HasPlugins` and `Plugin<T>` for ordered optional
extensions around a stable host API.

`build()` handles matching elements in `document.body` and later insertions; it can also register prioritised listeners.
Put registrations in an explicit browser build module imported by the browser entry or a template dependency.
Use semantic selectors and guard repeated activation when components do not already do so.
Load heavy or optional behaviour inside the callback. Browser subpath imports use explicit `.js` extensions.
Keep structure in HTML, behaviour in TypeScript and visual state in SCSS, sharing documented classes and attributes.

## Plugins and navigation

A host extends `HasPlugins<Host>`, accepts `Partial<Options<Host>>`, establishes its base state, then calls
`constructPlugins()` and `initPlugins()`.
A plugin extends `Plugin<Host, PluginOptions>` and receives its host as `of`.
Put wrappers and listeners in `init()` unless an earlier lifecycle is defined.

When wrapping a method, save the previous method, preserve its host receiver, return value and asynchronous behaviour.
Use a normal function when dynamic `this` is needed. Each plugin wraps earlier behaviour, so configure order explicitly.
Pass classes for default options and instances for configured options; define listener/style cleanup.

Extend `XTarget` policies with its plugins rather than building another navigation pipeline.
Check initial DOM, dynamic insertion, reinsertion and failed fetches; preserve native links/forms without JavaScript.

References: `build/build.ts`, `plugin/plugin.ts`, `xtarget/src/xtarget.ts`, `list/src/front/build.ts`.
