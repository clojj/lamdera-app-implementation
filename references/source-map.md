# Source Map

Use this policy to keep recommendations consistent and source-grounded.
This is the canonical source-governance file for this skill.

## Intent Routing

1. `generate`: Lamdera docs for workflow constraints, Elm guide for modeling heuristics.
2. `architecture`: Lamdera docs for platform constraints, Elm guide for type/module design.
3. `review-debug`: Lamdera docs first for operational behavior; Elm guide for model/message checks.
4. `mixed`: apply source routing in this order: architecture -> generate -> review-debug.

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

## Out of Scope in v1

1. `elm ...` command recommendations.
2. LLVM toolchain command recommendations (`clang`, `llc`, `opt`, etc.).
