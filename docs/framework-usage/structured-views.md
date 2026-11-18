# Structured business views

Use an `<article>` for a structured view of business objects or an action on them, wherever it appears:
in `main`, a modal, a form or another view. Keep the same header, content and optional footer structure.
Notifications, navigation, inline references and other compact supporting elements may use smaller markup.

The standard edit view uses `<form>` as its article-equivalent root, with exactly the same structure.
Use this form root when the whole view is one submission; use articles for structured views within a larger form.
Never nest forms. A list uses an article containing its search/selection form.

Follow [templates and targets](../framework-changes/architecture/html-templates-and-targets.md) for expressions,
translation, URLs, fragment syntax, assets and HTML validation.

## Structure and identity

- Put the view directly inside its destination. In `main`, use `main > article` or `main > form`;
  an extra wrapper prevents the standard panel layout from matching.
- Put `<header>` first, containing `<h2>` and, when needed, `<ul class="general actions">`.
  Keep the heading even when the application hides it: the framework uses top-level headings for the breadcrumb.
  Keep the document `<title>` consistent with it.
- Use one direct child for the content: a property list, table container, form or wrapper around several sections.
  An optional direct `<footer>` follows it. Do not put several content siblings beside the header/footer:
  `article.css` assigns them all to the same grid area, causing overlap.
- Put `data-action`, `data-class` and `data-route` on the article or equivalent form root.
  They identify the view's operation, business class and addressed business route, respectively.
  `data-class` is the reflected class name, not its display label. `data-route` excludes the action suffix;
  use the object's route for an object view and the type's route for a collection.
  Add `data-id="{?id}"` for an identified object; omit it for a new object or collection.
- Keep action names consistent with routes, CSS and action definitions. Use additional `data-*` attributes only
  when the owning component consumes them.

`ux-core/css/article.css` supplies the header/content/footer grid and content scrolling for `main > article` and
`main > form`. Its grid selectors do not match modal or nested views. Preserve the structure there and use the
owning component's layout; provide scoped CSS if it needs equivalent sizing or scrolling.
Do not insert another `<main>` into a modal to obtain those styles.

## Properties, actions and forms

The action passes the business object or a small named view model to `htmlTemplateResponse`.
For an object context, use `{%name}`, `{@route}` and `<!--%orderedProperties-->`.
For a view model, enter its object block before using object reflection; collections use their explicit type/columns.
`{.actions}` and `{.action}` access the enclosing action context from the root object;
each loop changes the current context. Keep business decisions in the action.

- Object properties: `<ul class="object properties">`, with one `<li data-property="{name}">` per property.
  For display, use `<label>{@display}</label>{outputMandatoryContainer}`.
  For editing, use `{edit}`, which supplies the field markup and labels through the configured transformers.
  For selected fields, use reflected properties such as `{%property.name.edit}` rather than rebuilding widgets.
- Actions: one `<li class="{action}">{{template}}</li>` per configured action in `ul.general.actions`.
  Reuse action templates, captions, destinations and icon styles. Put selection actions in `ul.selection.actions`
  within the selection form, normally in its footer. Buttons that do not submit must have `type="button"`.
- Forms: declare `action="app://(...)"`, `method="post"` for a mutation, and the response `target`.
  Use `target="main"` for a view response and `target="#notifications:prepend"` for notification feedback.
  A submit control may override these with `formaction` and `formtarget`.
  Follow standard edit forms with `autocomplete="off"` and conditional `enctype="multipart/form-data"`
  when file properties are present. Add `data-allow-new` only when related-object creation is intended.
- Lists: preserve the standard search/selection form, `table.objects`, column/filter metadata, feed include and
  selection controls when using the list components. Start from `list/src/list.html` and `feed.html`;
  copying just the visible table loses their browser contracts.

## Template for main

This object-view example is located at `app/customer/output.html`; adjust asset paths to the template's location.
Declare the styles the view uses, including `app.css`, `article.css`, action-bar styles and property/action styles.
Declare any view-specific browser build module in the head, as described in
[browser components](../framework-changes/architecture/browser-components.md).

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <link href="../../node_modules/@itrocks/ux-core/css/app.css" rel="stylesheet">
  <link href="../../node_modules/@itrocks/ux-core/css/article.css" rel="stylesheet">
  <link href="../../node_modules/@itrocks/action-bar/action.css" rel="stylesheet">
  <link href="../../node_modules/@itrocks/output/css/output.css" rel="stylesheet">
  <title>{@output.ucFirst}</title>
</head>
<body>
<main>
<!--BEGIN-->
  <!--#main-->
  <article data-action="output" data-class="{%name}" data-id="{?id}" data-route="{@route}">
    <header>
      <h2>{@output.ucFirst}</h2>
      <ul class="general actions">
        <li class="close"><a href="app://(@typeRoute)/list" target="main">Close</a></li>
        <!--.actions-->
        <li class="{action}">{{template}}</li>
        <!--end-->
      </ul>
    </header>
    <ul class="object properties">
      <!--%orderedProperties-->
      <li data-property="{name}"><label>{@display}</label>{outputMandatoryContainer}</li>
      <!--end-->
    </ul>
  </article>
  <!--#end-->
<!--END-->
</main>
</body>
</html>
```

Keep the document shell and `<main>` outside `BEGIN`/`END`: only the article enters the existing destination.
The application container owns navigation, breadcrumb, notifications, base URL and import map.
Use `<!--#main-->` for a response explicitly destined for `main`, as in the standard CRUD views.
For a view reusable in a modal or another target, omit that target block and its `<!--#end-->`:
the caller's `target` then chooses the destination. Keep `BEGIN`/`END` around the view in either case.
A notification response targets `#notifications:prepend` and contains notification items, not another business article.

## Edit variant

Keep the preceding document/fragment shell, link `edit/css/edit.css` and `save/css/action.css` as well,
and replace the article with this form. Set the document title to `{.action.ucFirst} {@output}`.
This follows the standard edit/new contract; the save response supplies notification feedback.

```html
<form action="app://(@route)/save" autocomplete="off" method="post" target="#notifications:prepend"
  data-action="edit" data-class="{%name}" data-id="{?id}" data-route="{@route}"
  data-if="{%hasFileProperty}" enctype="multipart/form-data" data-end>
  <header>
    <h2>{.action.ucFirst} {@output}</h2>
    <ul class="general actions">
      <li class="close"><a href="app://(@route)" target="main">Close</a></li>
      <li class="save"><input type="submit" value="Save"></li>
      <!--id?-->
      <!--.actions-->
      <li class="{action}">{{template}}</li>
      <!--end-->
      <!--end-->
    </ul>
  </header>
  <ul class="object properties">
    <!--%orderedProperties-->
    <li data-property="{name}">{edit}</li>
    <!--end-->
  </ul>
</form>
```

Check resolved HTML and the inserted DOM using the
[validation rules](../framework-changes/architecture/html-templates-and-targets.md#authoring-and-validation).
Verify direct navigation and partial insertion, heading/breadcrumb, content scrolling, action destinations,
form submission and first-use asset loading. Check the actual modal/nested context when applicable.

Reference implementations, relative to `node_modules/@itrocks/`: `output/src/output.html`, `edit/src/edit.html`,
`list/src/list.html`, `list/src/feed.html`, `save/src/save.html`, `home/src/container.html`,
`ux-core/css/article.css` and `action/cjs/action.html`.
