# dialog-timeout

A Claude Code mod that ends a turn left waiting on an open dialog and tells the agent the user is away. `README.md` explains the parts.

## Project state

- 2026-10-08: public and installable; the maintainer is the only known user. Retires at the first report from another user.
- 2026-10-08: holds no user data; it keeps only its own setting (minutes, on or off) in the plugin's local store. Retires if it ever stores or sends data off the user's machine.

## Rules

- Mod code: `$` is only passed to functions in the same file as the hooks (`claude plugin validate` refuses `$` across an import). Pure logic is exported from `hooks/register.ts` and tested in `tests/dialog-timeout.test.ts`.

<!-- >>> git-workflow (generated block; do not edit by hand) -->
## Git workflow

- `main` changes only through a PR, squash-merged.
<!-- <<< git-workflow -->
