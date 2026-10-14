# SCSS and assets

Put shared layout and element defaults in `ux-core`; feature structure, state and icons belong to the package owning
the corresponding HTML or browser behaviour.

Use stable semantic elements, feature classes, action names and `data-*` attributes.
Nest by DOM ownership and use direct-child selectors where structure is contractual; avoid leaking styles into includes.
Represent interactive state with classes or attributes toggled by TypeScript, such as `.visible` or `[data-sort]`.
Do not rely on temporary wrappers present only during partial navigation.

Compose reusable partials with Sass `@use`. Each standalone template links the styles it needs so inserted fragments
can load them through head processing. Reuse existing breakpoints and containers for shared layout changes.

Action icons use `.action.save, ul.actions > li.save` with `background-image: url('save.svg')`.
Keep the action name consistent across routes, templates, selectors and asset filenames.
Resolve asset URLs against compiled CSS and copy assets to the matching published location.
Check `url(...)` and `@use` paths, plus full-page and fragment rendering.

References: `ux-core/css/app.scss`, `action-bar/action.scss`, `list/src/list.scss`, `save/src/action.scss`.
