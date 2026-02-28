# Commands and Gates

Use this reference after classifying request intent (`generate`, `architecture`, `review-debug`, or `mixed`).

## Required commands

1. `lamdera init`
Creates a new Lamdera project scaffold in an empty directory.

2. `lamdera live`
Runs local full-stack Lamdera development with live reload.

3. `lamdera check`
Runs pre-deploy checks, including Evergreen migration/config/type safety checks.

4. `lamdera deploy`
Deploys the app once checks and auth prerequisites are met.

5. `lamdera reset`
Resets Lamdera/Elm-related caches when tooling or cache state is inconsistent.

6. `lamdera login`
Authenticates the CLI session for account-linked actions.

7. `lamdera make`
Compiles Elm code for local verification when app-remote context is unavailable.

## Optional diagnostics

1. `lamdera backend --help`
2. `lamdera backend --import=... --eval=...`
3. `npx elm-review --report=json` / `elm-review --report=json` (optional)

## Optional setup commands

1. `npx elm-review init --template jfmengels/elm-review-config/application` / `elm-review init --template jfmengels/elm-review-config/application`
Use only when user opts in to add `elm-review` to a project that does not yet have `review/`.

## Verification gate

After providing code or concrete implementation advice:
1. If `lamdera` CLI is available and app context exists (git repo + `lamdera` remote), run `lamdera check` as mandatory baseline verification.
2. If `lamdera` CLI is available but app context is missing, run local compile verification with `lamdera make <entry-elm-file> --output=/dev/null` and report that `lamdera check` was blocked by missing `lamdera` remote.
3. Run relevant build/compile checks and report result.
4. If code changed and compile verification succeeded, run optional `elm-review` only when `review/` already exists or user explicitly opts in.
5. If `review/` is missing and user opts in, initialize once with `npx elm-review init --template jfmengels/elm-review-config/application` for local installs, or `elm-review init --template jfmengels/elm-review-config/application` for global installs.
6. When eligible (and initialized when needed), run optional `npx elm-review --report=json` for local installs, or `elm-review --report=json` for global installs.
7. Report `elm-review` findings as markdown links with `path:line:column` from each error's `region.start`.
8. Then select additional verification commands from project-local scripts/config.
9. If `lamdera` CLI is not available and no project-defined verification command exists, report that verification is not runnable with current project metadata.
10. If tests are present, run relevant tests and report result.
11. If verification cannot run, state what was skipped and why.
12. Do not claim completion without command-backed evidence.

Use this entry file selection rule for local compile fallback:
1. Prefer `src/Frontend.elm` when present.
2. Otherwise use the project's actual entry module path as `<entry-elm-file>`.
3. If entry file cannot be determined, report verification as partially blocked and state why.

## Deployment gates

1. Account prerequisite:
User must have a Lamdera account (sign up if needed).

2. App context prerequisite:
Repository must be a git repo with a configured `lamdera` remote.

3. Auth prerequisite:
User must be logged in with `lamdera login` from the linked repository context.

4. Check prerequisite:
`lamdera check` must pass before `lamdera deploy`.
5. If mentioning git-push deployment, treat it as informational fallback only and only after confirming `lamdera check` succeeded.

## Command posture

1. Keep Lamdera as primary workflow commands, but allow optional `elm-review` commands.
2. Do not recommend `elm ...` commands in this skill.
3. LLVM toolchain commands are out of scope.
