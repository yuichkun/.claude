- 現在は2026年です
- Don't be a kiss-ass. Be honest and direct.
- **VitePlus hard rules (user has repeated this many times — internalize it; do not make them repeat again).** Applies to every repo where `vite-plus` appears in `package.json` or `vp` is in scripts. Detection: `grep -l vite-plus package.json` or look for `vp ` in scripts. Authoritative reference: `node_modules/vite-plus/AGENTS.md` in the project, and `https://viteplus.dev`.
  - **Never invoke `npm` / `pnpm` / `yarn` / `npx` directly.** Not in shell, not in issue bodies, not in README, not in CI config, not in test-plan commands.
  - **Command cheat sheet — use these exact forms:**
    - Install all deps: `vp install` (alias `vp i`) — run after cloning or pulling.
    - Add a package: `vp add <pkg>` (dev dep: `vp add -D <pkg>`).
    - Remove: `vp remove <pkg>` (aliases `vp rm`, `vp un`, `vp uninstall`).
    - Update: `vp update` (alias `vp up`). Check outdated: `vp outdated`. List: `vp list` / `vp ls`. Why installed: `vp why`. Info: `vp info`.
    - Dev server: `vp dev`. Build: `vp build`. Preview: `vp preview`. Library pack: `vp pack`.
    - Tests: `vp test`. Lint: `vp lint` (oxlint; `vp lint --type-aware` works out of the box — do NOT install `oxlint-tsgolint`). Format: `vp fmt`. **Combined format+lint+typecheck: `vp check` (and `vp check --fix` auto-corrects).** There is no separate `vp typecheck` — `vp check` includes tsgo typecheck.
    - Run a `package.json` script: `vp run <script>`. **Critical gotcha:** `vp dev` / `vp build` / `vp test` / `vp lint` / `vp fmt` / `vp check` always invoke the Vite+ built-in tool, NOT a same-named script in `package.json`. If the user's `package.json` defines its own `dev` that chains multiple processes (e.g. `concurrently ...`), you MUST call it as `vp run dev` — calling `vp dev` will silently ignore that script and only start Vite's dev server.
    - One-off tool from registry: `vp dlx <pkg>` (replaces `npx` / `pnpm dlx`).
    - One-off local binary: `vp exec <binary>` (replaces `./node_modules/.bin/...`).
    - Node version management: `vp env`. Self-upgrade Vite+: `vp upgrade`. Migrate existing project: `vp migrate`. Staged-file lint (pre-commit): `vp staged`. Task cache: `vp cache`.
    - There is **no** `vp vitest`, `vp oxlint`, `vp tsc`, `vp typecheck` — these are not commands. Use the mapped command above.
  - **Imports, not installs:** do not install `vitest`, `oxlint`, `oxfmt`, `tsdown`, or `vite` directly — they are wrapped by Vite+. Import from the `vite-plus` package instead: `import { defineConfig } from 'vite-plus'`, `import { expect, test, vi } from 'vite-plus/test'`. If you see existing code importing from `vitest`/`vite` in a Vite+ project, that is a bug worth flagging.
  - **CI in GitHub Actions:** use `voidzero-dev/setup-vp@v1` (replaces setup-node + cache + install). Run `vp check` + `vp test`.
  - **Validation loop after any change:** `vp check` (zero errors) and `vp test` (all pass). That is the equivalent of "typecheck + lint + format + test" for any other stack.
  - **If you do not know the Vite+ equivalent of a task, STOP and read `node_modules/vite-plus/AGENTS.md` or fetch https://viteplus.dev before writing.** Falling back to `npm` because you are unsure is never acceptable.
- always use context7 (plugin) to check the latest docs of libraries
- always use `pushd` instead of `cd`
- ## Code Comment Guidelines

  Never use temporal or chronological expressions in comments or documentation. Code
  should describe its current state, not reference past implementations or changes.

  **Expressions to avoid:**
  - "now", "currently", "previously", "before", "after", "used to"
  - "changed from X to Y", "updated to", "modified to", "recently"
  - "new", "old", "legacy", "originally", "initially"
  - Any phrases implying time-based transitions

  **Bad examples:**
  ```python
  # Now using top 3 salaries instead of all
  # Previously calculated average of all salaries
  # Updated to use new algorithm
  # This replaces the old implementation

  Good examples:
  # Calculates average of top 3 salaries
  # Uses highest salary values for calculation
  # Top 3 selection algorithm
  # Filters zero values from salary list

  Git handles change history. Comments should only explain what the code does, not how it
   evolved.
- never run `dev` commands such as `npm run dev` as it will be forever stuck. Let the user run the command
