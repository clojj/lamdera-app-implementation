# Review and Debug Playbook

Use this reference for structured Lamdera review/debug analysis.

## Review Flow

1. Classify issue type: state, message, boundary, migration, or effect.
2. Reconstruct minimal reproducible path.
3. Trace message -> update branch -> resulting state.
4. Verify boundary ownership assumptions.
5. Propose smallest safe change first.

## Debug Heuristics by Symptom

1. UI shows impossible state:
- Check model type design for missing explicit states.
- Check update branches for incomplete handling.

2. Action appears ignored:
- Check message wiring from view.
- Check guard conditions in update path.

3. Data mismatch between frontend and backend:
- Check shared ownership assumptions and mapping logic.
- Check stale semantics after type changes.

4. Deployment check failures:
- Treat `lamdera check` output as blocking.
- Address migration/config/auth issues before deploy.

## Review Output Pattern

1. Decision: likely root cause and chosen next action.
2. Why: evidence from message/state/boundary trace.
3. Risks: side effects, migration sensitivity, regressions.
4. Next checks: build/test commands and expected outcomes.
