---
name: rust
description: >-
  Use when writing, editing, reviewing, testing, or debugging Rust code
---

# Rust 🦀

## Documentation

When exact standard library behavior matters, consult source under
`~/.rustup/toolchains/stable-aarch64-apple-darwin/lib/rustlib/src/rust/library`.

When exact third-party crate behavior matters, inspect crate source under
`~/.cargo/registry` and `~/.cargo/git`.

For Rust Reference and Rustonomicon use [`Docs`](../docs/SKILL.md) skill.


## Codestyle

### Code Structure

Keep execution order visible in source order. Compute a value immediately before the step
that consumes it, unless earlier evaluation is required for correctness.

Separate distinct logical steps with a blank line: lookup, validation, construction,
mutation and return. Keep tightly related statements together.

After a `let ... else` block, add a blank line before the value is used.

Put a blank line between multiline `match` arms.
Short adjacent arms may remain compact when they form one obvious group.

### Intermediate Values

Construct a nontrivial value in a named local before inserting it, wrapping it in `Some`,
or passing it to another call.

When a multiline lookup returns an `Option`, finish the lookup first,
then unwrap it with `let ... else`.

Name a multiline expression before using it in control flow.

Name resolved defaults and derived flags before branching on them.
Do not repeat a long field-access or fallback expression in a condition.

### Patterns and References

Use reference destructuring in closures when it removes dereference noise
without obscuring the item type.

When matching a borrowed enum, use reference patterns when fields are `Copy`.
Bind the values directly instead of dereferencing them later.

### Imports

Import a type when the code constructs it, names it repeatedly, or uses it in a function signature.
Avoid fully qualified paths around struct literals.

Keep `proptest` strategies and helper types explicitly qualified,
such as `proptest::sample::Index` and `proptest::collection::vec`.
Do not import them individually merely to shorten generator code.

### Tests

Visually separate setup, execution, result extraction and assertions.

Build nontrivial fixture values in named locals before storing them.
Keep the state transition being tested easy to identify.

### Restraint

Do not introduce a local or blank line for every expression.
Apply these rules when an expression spans several lines, combines lookup with control flow,
constructs a nontrivial value, or marks a distinct execution step.


## Formatting

Follow style of existing code and `rustfmt.toml`.
Format Rust code with `cargo +nightly fmt`.


## Validation

Run tests with `cargo nextest run`.
