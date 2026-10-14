# Transformations and views

Use the transformer registry for property representation changes; use view metadata to select presentation.

Selection uses format (`HTML`, `SQL`, etc.) and direction (`EDIT`, `INPUT`, `OUTPUT`, `READ`, `SAVE`).
Precedence: property → property type → `ALL`, with empty format/direction fallbacks.
Type lookup supports canonical types, domain types, collections and base types.

Register with `@Transform`, `setPropertyTransformer` or `setPropertyTypeTransformer`.
Use a type transformer for a shared rule and a property transformer for an exceptional field.
Return `IGNORE` to leave a property untouched; `undefined` is a legitimate transformed value.

- Form → domain: `HTML`/`INPUT` through `dataToObject`.
- Domain → edit/display: `HTML`/`EDIT` or `HTML`/`OUTPUT` through framework `ReflectProperty`.
- Row → domain: `SQL`/`READ`.
- Domain → database: `SQL`/`SAVE`.

Prefer pure transformers. Bind collaborators and register shared transformers during bootstrap.
Format-level post-processing is for rules shared by every transformer in that format.
Check precedence, asynchronous and optional values, collections and `IGNORE` when changing resolution.

`@Display` names classes/properties; `@DisplayOrder` orders detail fields; `@List` selects collection fields;
`@Representative` identifies objects in links and summaries. Defaults are inherited and reflection-based.
Templates consume reflected metadata and decorated helpers instead of rebuilding labels or formatting.

References: `transformer/src/transformer.ts`, `data-to-object/src/data-to-object.ts`,
`framework/src/reflect-property.ts`, `class-view/src/representative.ts`.
