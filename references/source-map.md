# Source Map

Use this policy to keep recommendations consistent and source-grounded.
This is the canonical source-governance file for this skill.

## Intent Routing

1. `generate`: Lamdera docs for workflow constraints, Elm guide for modeling heuristics.
2. `architecture`: Lamdera docs for platform constraints, Elm guide for type/module design.
3. `review-debug`: Lamdera docs first for operational behavior; Elm guide for model/message checks.
4. `mixed`: apply source routing in this order: architecture -> generate -> review-debug.
5. When optional `elm-review` setup or findings reporting is requested, route to `elm-review` docs for configuration concepts and `node-elm-review` docs for CLI command/report behavior.

## Lamdera Docs Usage

Use Lamdera docs as source of truth for:
1. CLI commands and command behavior.
2. Local development and deploy workflow.
3. Platform-specific checks and constraints.

## Elm Guide Usage

Use Elm guide for:
1. Language-level modeling patterns.
2. Frontend architecture and design heuristics.
3. Beginner-friendly Elm conceptual framing.

Do not use Elm guide as command/workflow source for this skill.

## Elm Package Catalog Usage

Use `https://package.elm-lang.org/` for package discovery and API lookup only for Lamdera frontend code.
Do not use package-catalog guidance for backend operational tooling, deployment gates, or command workflow decisions.

## elm-review Docs Usage

Use `https://github.com/jfmengels/elm-review` for:
1. Configuration model (`review/` directory and `ReviewConfig` concepts).
2. Recommended starter templates and rule ecosystem context.

Use `https://github.com/jfmengels/node-elm-review` for:
1. CLI installation/command forms (`npx` vs global binary).
2. JSON/NDJSON report formats and region fields for linkable findings.

## Out of Scope in v1

1. `elm ...` command recommendations.
2. LLVM toolchain command recommendations (`clang`, `llc`, `opt`, etc.).
