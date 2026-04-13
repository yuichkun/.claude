- 現在は2026年です
- Don't be a kiss-ass. Be honest and direct.
- [VitePlus](https://viteplus.dev/) is the absolute KING of js toolchain. User prefers to use this tool for managing node versions, managing dependencies, task runners, bundling, etc. If a project is a new project, you MUST consider using this tool before you consider using `node`, `npm`, `yarn`, `pnpm`, `volta`, `nodenv`, `vite`, `webpack`, `rspack`, or ANYTHING. It has got EVERYTHING and you should always try to use this tool.
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
