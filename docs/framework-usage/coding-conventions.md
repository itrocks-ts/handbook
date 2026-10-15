# Coding conventions

Apply these rules to application and framework source, tests and development files.
For framework packages, also apply [package versioning](../framework-changes/README.md#package-versioning)
from the first file change.

## Layout and blocks

- Limit lines to 120 columns; count each indentation tab as two columns. Only indivisible content may exceed it.
- Indent with tabs wherever permitted, including HTML and SCSS; use spaces for alignment or tab-forbidding formats
  such as YAML.
- Omit semicolons; use single quotes and template literals for interpolation or multiline text.
- Space postfix operators: `index ++`, `index --`.
- Align `from`, `=`, `:` and values in adjacent related lines where the limit allows.
- Put `{` on the next line for classes, interfaces, functions, methods and constructors.
- Keep `{` on the control line for conditions, loops, `switch`, `try`, `catch` and `finally`.
- Put `else`, `catch` and `finally` on a new line after the preceding `}`.
- Braces may be omitted for a single-line control body; multiline bodies require them.
- Leave a blank line after a non-empty class opening brace and before its closing brace.

## Signatures

Choose the first layout below that fits 120 columns. Apply the same parameter and return-type breaks to methods,
constructors, overloads and arrow functions. When only the return type causes overflow, move it before splitting
parameters. After splitting at parentheses, keep parameters together if they fit; otherwise use one per line.
Omit the trailing comma and keep `): ReturnType` together.

```ts
function calculate(input: Input, options: Options): Result
{
}

function calculate(input: Input, options: Options)
	: Promise<Result>
{
}

function calculate(
	input: Input, options: Options
): Promise<Result>
{
}

function calculate(
	input: Input,
	options: Options
): Promise<Result>
{
}
```

## Ordering

Sort homogeneous sequences alphabetically by stable name wherever order has no semantic significance.
This includes configuration, documentation, object/array entries, declarations, members, imports, exports,
parameters and test cases. Separate coherent kinds where useful, then sort within each group.
Preserve required initialisation, side effects, fallback, precedence, lifecycle, overload, protocol and runtime order;
comment non-obvious constraints.

Group module declarations as: types/interfaces, constants, `let`, functions, classes.

For side-effect-free imports, locality precedes alphabetical order:

1. Bare specifiers, including packages and Node.js built-ins.
2. Parent-relative paths, farthest first (`../../../`, `../../`, `../`).
3. Subdirectory paths, deepest first.
4. Same-directory paths (`./` without a subdirectory).

Within the same locality and depth, sort by specifier; repeated specifiers sort by imported symbol.

## Modules and declarations

- Start TypeScript modules with a blank line unless imports come first; imports have no preceding blank line.
- Keep imports first, one symbol per declaration, with aligned `from`.
- Omit `.js` and `.ts` from specifiers when resolution permits; browser imports require explicit `.js`
  as described in [browser components](../framework-changes/architecture/browser-components.md).
- Prefer named exports; use default exports only for external API requirements.
- Use `const` unless reassignment is required; never `var`.
- Use object property/method shorthand and concise arrows for a single returned expression.
