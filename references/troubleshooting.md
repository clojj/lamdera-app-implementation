# Troubleshooting

Use this after classifying as `review-debug` (or `mixed` including debug).

## Init prompt in non-interactive runs

1. `lamdera init` prompts for confirmation.
2. In non-interactive agent execution, run `printf 'Y\n' | lamdera init`.
3. If initialization still fails, verify the directory is intended for new project scaffolding.

## Login/auth failures

1. Ensure repository app context exists (git repo + `lamdera` remote).
2. Run `lamdera login` from that linked repository context.
3. Re-run `lamdera check`.
4. Continue only after auth succeeds.

## Cache/compiler mismatch

1. Run `lamdera reset`.
2. Restart with `lamdera live`.
3. Re-run `lamdera check` before deployment only when app context exists (git repo + `lamdera` remote).
4. If app context is missing, run local compile verification with `lamdera make <entry-elm-file> --output=/dev/null` and treat deploy as blocked until app context is configured.

## Migration/config errors

1. Treat `lamdera check` failures as blocking.
2. Complete required migration/config fixes.
3. Re-run `lamdera check` until clean.
4. Then run `lamdera deploy`.

## Verification reporting

1. After suggesting a fix, run `lamdera check` if `lamdera` CLI and app context are available.
2. If app context is missing, run `lamdera make <entry-elm-file> --output=/dev/null` and report that `lamdera check` was blocked by missing `lamdera` remote.
3. Run relevant build/compile checks.
4. If code changed and compile verification succeeded, run optional `elm-review` only when `review/` already exists or user explicitly opts in.
5. If `review/` is missing and user opts in, initialize once with `npx elm-review init --template jfmengels/elm-review-config/application` for local installs, or `elm-review init --template jfmengels/elm-review-config/application` for global installs.
6. When eligible (and initialized when needed), run `npx elm-review --report=json` for local installs, or `elm-review --report=json` for global installs.
7. Report `elm-review` findings as markdown links with `path:line:column` using each error's `region.start`.
8. Then select additional verification commands from project-local scripts/config.
9. If `lamdera` CLI is unavailable and no project-defined verification command exists, report verification as not runnable instead of guessing commands.
10. If tests are present, run relevant tests for affected areas.
11. Report exact command outcomes, or state clearly what could not be run and why.

Use this entry file selection rule for local compile fallback:
1. Prefer `src/Frontend.elm` when present.
2. Otherwise use the project's actual entry module path as `<entry-elm-file>`.
3. If entry file cannot be determined, report verification as partially blocked and state why.

## Unknown app / missing remote

1. If Lamdera reports unknown app, check git remotes.
2. Configure a `lamdera` remote for the repository according to dashboard instructions.
3. Re-run `lamdera login`, then `lamdera check`.

## elm-review setup/execution

1. If `elm-review` command is missing, prefer local install with `npm install --save-dev elm-review` and run via `npx elm-review`; global install via `npm install -g elm-review` is allowed.
2. If `review/` does not exist and user opts in, initialize with `npx elm-review init --template jfmengels/elm-review-config/application` for local installs, or `elm-review init --template jfmengels/elm-review-config/application` for global installs.
3. If compile checks fail, skip `elm-review` and report it as blocked by compile failure.
