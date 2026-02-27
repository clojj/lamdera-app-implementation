# Elm for Lamdera Core Guidance

Use this reference when a Lamdera task needs deeper Elm language guidance for generation, architecture, or review/debug.

## Mental Model

1. Model real domain states explicitly with custom types.
2. Keep messages as clear user/system intents, not implementation details.
3. Keep `update` as the single source of truth for transitions.
4. Treat `view` as a pure projection of model state.

## Generation Heuristics

1. Start from domain states, then derive messages.
2. Prefer narrow message payloads over broad context blobs.
3. Keep each update branch focused on one transition concern.
4. Use small helper functions for repetitive transition logic.

## Lamdera-Oriented Architecture Heuristics

1. Decide ownership first: frontend-only, backend-only, or shared.
2. Share types only when both sides truly need the same semantics.
3. Avoid leaking backend concerns into frontend model types.
4. Call out migration-sensitive type changes before implementation.

## Beginner Anti-Patterns

1. Using booleans where a custom type is clearer.
2. Overloading one message type for unrelated actions.
3. Hiding side-effect intent in ambiguous update branches.
4. Growing shared types without boundary ownership rules.

## Review/Debug Checks

1. Does each symptom map to a clear message path?
2. Are transitions complete for all state variants?
3. Are impossible states prevented by the type design?
4. Is any boundary mismatch causing stale assumptions?
