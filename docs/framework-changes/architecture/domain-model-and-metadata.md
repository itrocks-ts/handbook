# Domain model and metadata

Use plain domain classes and focused decorators. Discover fields through `ReflectClass` and `ReflectProperty`,
not duplicated field lists.

- Declare rendered or persisted fields with explicit types and meaningful default initialisers.
- Keep zero-argument construction usable: `ReflectClass.propertyNames` instantiates the class.
- Use inheritance for an is-a relationship and `@Uses(...mixins)` for orthogonal reusable components.
- Keep storage identifiers out of domain classes; see [persistence](persistence-and-schema.md).

A metadata package owns a private `Symbol`, a PascalCase decorator using `@itrocks/decorator/class` or `/property`,
and a lower-camel accessor ending in `Of` that defines defaults and inheritance.
Decorators may register metadata or a target transformer; global dependency binding belongs in bootstrap.

Reflection requires a readable `.d.ts` beside the runtime module for property types and the corresponding TypeScript
source for defaults. Imported model types may resolve lazily to tolerate cycles. Values are cached on first access:
complete configurable binding before reading them. Read `collectionType` only for collection properties.

Verify inheritance, optionality, collection element types and defaults when changing reflection behaviour.
Keep presentation, conversion and database behaviour in their consumer layers.

References: `decorator/src/class.ts`, `reflect/src/class.ts`, `property-type/src/property-type.ts`, `uses/src/uses.ts`.
