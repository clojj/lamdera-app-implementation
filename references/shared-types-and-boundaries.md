# Shared Types and Boundaries

Use this reference for Lamdera architecture decisions involving frontend/backend/shared ownership.

## Ownership Rules

1. Frontend-only types:
- UI state, local interaction flow, view formatting concerns.

2. Backend-only types:
- Persistence-centric structures, server workflows, internal operational state.

3. Shared types:
- Stable domain semantics needed on both sides.
- Keep shared types small and explicit.

## Decision Checklist

1. Does the frontend need this exact semantic meaning?
2. Does the backend need to persist or compute over the same shape?
3. Can the shared type remain stable under expected feature changes?
4. Would duplication with explicit mapping reduce coupling?

## Boundary Anti-Patterns

1. Sharing UI-specific types with backend.
2. Sharing backend-internal workflow types with frontend.
3. Expanding one shared "god type" for unrelated concerns.
4. Treating shared as the default instead of explicit choice.

## Beginner Guidance

1. Default to frontend-only or backend-only first.
2. Promote to shared only when both sides require the same semantics.
3. Add mapping functions when ownership differs.
4. Re-evaluate sharing decisions when type changes start cascading.
