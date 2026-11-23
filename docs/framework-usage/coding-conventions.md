# Coding conventions

Apply these rules to all development: application code, framework packages, other modules, tests and development files.
For framework packages, also apply [package versioning](../framework-changes/README.md#package-versioning)
from the first file change.

## Design choices

Before implementing a feature or fix, consider several ways to express the requested behaviour. Keep this comparison
proportionate to the task; choose the KISS (Keep It Simple And Stupid) solution that meets the actual requirements:

- Prefer a direct model of the behaviour, using the relevant events and state, over indirect calculations or heuristics.
- Reuse existing behaviour and share the same algorithm between variants; make their actual differences explicit.
- Minimise abstraction layers, preferably adding none. Introduce one only for a concrete current need that makes the
  solution easier to understand or maintain.
- Choose code that a beginner developer can reread and maintain, and whose operation is easy to explain to a human.
  Prefer less code when correctness and readability are equivalent.
- Apply SOLID through clear responsibilities, existing extension points, substitutable contracts, focused interfaces
  and appropriate dependency boundaries. Each separation must serve the current behaviour and simplify maintenance.
- When a condition encloses the rest of a loop body, prefer an inverted `continue` guard to another indentation level.

When fixing a bug, reconsider the model before adding another condition or special case. For example, column drag
placement can remember the hovered column and react to changes of column and movement direction, instead of repeatedly
inferring placement from position thresholds.

## Layout and blocks

- Limit lines to 120 columns; count each indentation tab as two columns. Only indivisible content may exceed it.
- Indent with tabs wherever permitted, including HTML and SCSS; use spaces for alignment or tab-forbidding formats
  such as YAML.
- Omit semicolons; use single quotes and template literals for interpolation or multiline text.
- Space postfix operators: `index ++`, `index --`.
- Align `from`, `=`, `:`, `??` and values in adjacent related lines where the limit allows. Include mixed `const`/`let`
  declarations, assignments and constructor parameters in the same alignment group; keep a space before each operator.
- Declare one variable per statement. Separate preparation, object configuration and the final call or return with
  blank lines when they form distinct steps.
- Put `{` on the next line for classes, interfaces, functions, methods and constructors.
- Keep `{` on the control line for conditions, loops, `switch`, `try`, `catch` and `finally`.
- Put `else`, `catch` and `finally` on a new line after the preceding `}`.
- An `if` or `else` body may stay on the same line without braces only if the line fits within 120 columns and the
  body is a single control-flow exit, such as `break`, `continue` or a `return` of nothing, a variable or a literal.
  Otherwise, use braces and start the body on the next line. In an `if`/`else` pair, use braces for both or neither.
- For empty constructors, keep `{}` on the closing parameter line, including after a multiline parameter list.
- Leave a blank line after a non-empty class opening brace and before its closing brace.

## Wrapped expressions

The 120-column limit is a maximum, not a target. Break dense expressions earlier when their structure is clearer.

- For multiline control conditions, put `if (` on its own line, indent the condition once, and align `) {` with `if`.
  Put leading `&&` and `||` on continuation lines at the same condition indentation.
- Prefer a direct ternary return when choosing between two values. Keep only simple ternaries on one line; otherwise
  put `?` and `:` on separate lines, one level below the return or assignment. Parenthesise concatenation branches.
- For a ternary chain, align successive conditions and their results instead of increasing indentation for each case.
- In multiline array and object literals, put one entry per line, including spreads and shorthand properties.
  Break nested calls at argument boundaries and close each enclosing call at its corresponding indentation level.

```ts
if (
	!path || !path.startsWith('/') || path.startsWith('//')
	|| (new URL(path, origin).pathname !== path)
) {
	return ''
}

return (!prefix || path.startsWith(prefix + '/'))
	? path
	: (prefix + path)

result =
	isFunction(value) ? value(options)     :
	isType(value)     ? new value(options) :
	value
```

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
parameters and test cases. Preserve existing responsibility groups, placing new members in their matching group,
then sort within each group. Use short sentence-case section comments, preserving acronym capitals such as HTML and URL.
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
