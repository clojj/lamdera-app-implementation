# Evolution and Migration Safety

Use this reference when changes may affect deployed data or cross-version compatibility.

## Risk Signals

1. Changing custom type variants used in persisted or shared data.
2. Renaming or removing fields used across frontend/backend boundaries.
3. Reinterpreting field semantics without explicit migration logic.
4. Bundling many type changes in one release.

## Safe Change Sequence

1. Identify impacted types and call out migration sensitivity before coding.
2. Prefer additive, backward-compatible shape changes first.
3. Isolate semantic changes into small, reviewable steps.
4. Run `lamdera check` early and after each migration-sensitive change.
5. Do not proceed to deploy until `lamdera check` is clean.

## Beginner Defaults

1. Prefer introducing new fields/variants over mutating old semantics in place.
2. Avoid "big-bang" refactors of shared/persisted types.
3. Keep migration intent explicit in task notes and review output.

## Review Questions

1. What previously valid data shapes now fail?
2. Are transitions defined for all old and new variants?
3. Can this change be split into safer increments?
4. Is `lamdera check` output treated as blocking?
