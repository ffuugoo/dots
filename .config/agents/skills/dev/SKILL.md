---
name: dev
description: >-
  Use when writing, revising, or reviewing code, documentation and comments.
  Focuses on semantic accuracy, project vocabulary, and explaining non-obvious behavior.
---

# Code Structure

Organize source files from general entry points and public interfaces toward specific
implementation details.

In executable code, put the main entry point first, followed by the functions it calls,
in usage order where practical. In libraries and modules, put public types, functions
and methods before private items. Within those groups, prefer usage order over
alphabetical or arbitrary ordering when it makes the control flow easier to follow.

Treat a private helper used by exactly one function, method or type as part of that
item. It may appear directly after its sole user instead of in the general private
section. This exception applies to private functions and methods, and to data-only
private types that have no implementation block.

A private support type with its own implementation block is a separate component.
Place it after the main type it supports, following the normal ordering for its
definition and implementation rather than interleaving it with the main item.

Declare and initialize local variables as close as practical to their first use.
Do not collect declarations at the beginning of a scope. Move a declaration earlier
only when evaluation order, lifetime, shared use or another concrete constraint requires it.

# Documentation

Write for a reader who has the repository and code, but not the conversation that led to it.

## Explain the Reason

Explain why behavior exists and what would go wrong without it.
Do not merely narrate the code.

Preserve the causal chain behind non-obvious behavior.
Name what can happen, how state can differ, what happens next,
and why the documented action restores correct behavior.

When the same synchronization or validation appears in two places,
explain what can happen between them and why each invocation is needed.

For internal operations and signals, explain their purpose and lifecycle.
Saying only that they are never persisted or committed does not explain why they exist.

Make comparisons complete.
Say what a lightweight representation stores instead of the omitted state.

Leave out facts that do not explain the behavior at that location,
even when those facts are true.

## Match the Code

Open module documentation with the module's purpose and central abstraction.
Assume readers know the surrounding domain basics; explain local invariants
and unusual behavior.

Scale detail to how surprising the behavior is.
Synchronization, recovery, retries, partial writes, and duplicated work need
more explanation than ordinary control flow.

Describe behavior at the abstraction level visible in the file.
Do not refer to a deeply nested implementation step when a direct description
of the visible operation is clearer.

Use established project terms exactly.
Do not infer a narrower or more specific name from implementation details.

Prefer concrete component names and roles over relative labels such as
"real", "existing", "legacy", or "shadow", unless the label is an established term.

Match grammatical number to the code path.
Use singular when each invocation involves one handler or operation,
and plural only for multiple actors or the subsystem as a whole.

## Check the Meaning

Verify documentation against execution order and failure behavior,
especially around retries, recovery, persistence, and partial application.

Check whether another layer already guarantees the behavior before claiming
that the documented code must do it.

Avoid absolute claims unless the implementation guarantees them.

Preserve every necessary premise when condensing an explanation.

When reviewing wording, separate semantic problems from grammar and style.
Report meaning errors explicitly instead of silently treating them as prose cleanup.
