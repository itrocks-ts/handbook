# Persistence and schema

Domain classes do not own persistence identifiers. Opt in with `@Store()`; supply a name only to override convention
and use `@Store(false)` to opt out. At the storage boundary, instances are `Entity<T>` with an attached `id`.

Use abstract `DataSource` operations for count, read, search, save, delete and collections.
Select the configured engine with `createDataSource`; do not construct MySQL adapters in actions or models.
Pass typed query options rather than SQL.

Stored object collections use relation operations and identifiers. `@Component` marks owned data and `@Composite`
its back-reference. Ownership affects loading, saving, deletion and edit rendering; declare it explicitly.

## Schema layers

1. Reflection and metadata describe the model.
2. `reflect-to-schema` produces neutral `Database`, `Table`, `Column`, `Index` and `Type` objects.
3. Introspection (e.g. `mysql-to-schema`) produces the same neutral model from the database.
4. `schema-diff` compares models.
5. A dialect adapter (e.g. `schema-to-mysql`) renders SQL.

Naming, former names, length/range/precision, optionality, representative indexes and relation metadata belong in
reflection conversion. SQL syntax and dialect limits belong in the dialect adapter.
Value conversion uses `SQL`/`READ` and `SQL`/`SAVE` transformers; see [transformations](transformations-and-views.md).
Check new/existing entities, optional values, relations, collection diffs, conversion symmetry and migration
preservation
of former names and representative indexes.

References: `storage/src/data-source.ts`, `reflect-to-schema/src/to-column.ts`,
`schema-to-mysql/src/schema-to-mysql.ts`.
