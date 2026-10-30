# Mona’s Project Pulse Dashboard — Implementation Plan

## Summary

Build a small, static Project Pulse dashboard that helps contributors scan project names, owners, status, recent activity, priority or risk, and short summaries. Follow the repository brief: use HTML, CSS, and JSON, with a top-level `projects` array and a VS Code launch configuration named **Run Project Pulse Dashboard**.

The repository does not show an existing app implementation or frontend framework to extend. Prefer the specified files and avoid adding dependencies or files unless the Orchestrator confirms they are needed. The dashboard should load its JSON over HTTP; opening `index.html` directly from the filesystem may prevent that fetch.

## Ordered implementation steps

### 1. Confirm the shared UI and data contract

- **Designer:** Set the information hierarchy, card layout, status and priority treatments, responsive behavior, and accessibility expectations. Specify the CSS hooks and the content order the markup should use.
- **Coder:** Confirm the `projects` schema and agree with Designer on the DOM/class hooks before implementation.
- **Files:** No implementation files; this is a brief handoff.
- **Dependency:** Complete before parallel implementation to avoid mismatched class names, fields, or UI expectations.

### 2. Implement the dashboard files

- **Designer — `app/styles.css`:** Create the polished, responsive dashboard styling. Include `.dashboard` and `.project-card` hooks, clear status badges and priority treatment, readable spacing and contrast, rounded cards, and shadows. Consider reduced-motion preferences if adding animation.
- **Coder — `app/project-data.json`:** Create valid JSON with a top-level `projects` array. Each project must include `name`, `owner`, `status`, `recentActivity`, and `priority`. The brief also requests a contributor-friendly summary but does not list it among required fields; resolve whether to include a `summary` property before treating it as required. Use clearly illustrative sample data rather than implying unprovided real project facts.
- **Coder — `app/index.html`:** Create the page with the exact title **Project Pulse**, link `styles.css`, and load `project-data.json`. Render visible `.project-card` elements showing the required project fields. Since no separate JavaScript file is in scope, keep any rendering script in this file unless the Orchestrator approves another file. Provide a clear loading, empty, and fetch-error state.
- **Coder — `.vscode/launch.json`:** Add strict JSON for **Run Project Pulse Dashboard**. Per the repository instructions, use `python3 -m http.server 5500`, set `cwd` to `${workspaceFolder}/app`, and open `http://localhost:%s/index.html` through `serverReadyAction`. Ensure the resulting URL targets `index.html`, not the directory root.
- **Dependencies:** Step 1’s agreed data and UI contract is required. After that, Designer’s stylesheet and Coder’s JSON/HTML/config work can proceed in parallel, provided each agent owns only the files assigned above. The HTML should use the agreed CSS hooks and data fields.

### 3. Integrate and validate

- **Coder:** Check that markup, CSS selectors, and JSON fields agree; fix integration issues within the assigned files.
- **Orchestrator:** Run the automated checks and preview the dashboard using the launch configuration.
- **Files:** Any fixes remain limited to `app/index.html`, `app/styles.css`, `app/project-data.json`, and `.vscode/launch.json`.
- **Dependency:** This step follows implementation; browser validation requires all three app files to be integrated.

## Responsibilities and file ownership

| Owner | Assignment |
|---|---|
| **Designer** | UX and visual direction; implement `app/styles.css` if assigned. Avoid editing Coder-owned files. Report design tradeoffs and accessibility/responsive checks. |
| **Coder** | Implement `app/index.html`, `app/project-data.json`, and `.vscode/launch.json`; integrate the agreed design hooks; validate structure, JSON, and launch behavior. Do not edit `app/styles.css` unless explicitly reassigned. |
| **Orchestrator** | Coordinate the shared contract and handoffs, prevent overlapping edits, run integration checks, and report remaining risks. |

## Dependencies and parallel work

- **Must run sequentially:** Agree on the schema and UI hooks before implementation; integrate and preview after implementation.
- **Can run in parallel after agreement:** Designer can build `app/styles.css` while Coder builds `app/project-data.json`, `app/index.html`, and `.vscode/launch.json`. Keep file ownership separate.
- **Integration dependency:** HTML rendering depends on the agreed JSON contract and CSS hooks. The launch configuration can be authored alongside the app files, but runtime validation depends on all files being present.

## Edge cases and risks

- Handle JSON fetch failure, malformed or empty project data, and an empty `projects` array without leaving a blank dashboard.
- Render project-provided text safely; avoid inserting untrusted values as raw HTML.
- Do not convey status or priority by color alone. Preserve readable contrast, semantic structure, and usable behavior at narrow viewport widths.
- Port `5500` may already be occupied. Report the conflict rather than silently changing the required port.
- The specified VS Code launch behavior depends on a compatible debugger extension being available. The devcontainer lists Copilot and GitHub Actions extensions, but does not explicitly list the Python extension/debugger. Verify the launch configuration in the Codespace; do not assume that dependency is installed.
- Python’s `http.server` is appropriate for this exercise’s local static preview, not production hosting.

## Validation expectations

1. Confirm all four assigned files exist and remain within scope.
2. Run `python3 -m json.tool app/project-data.json` and `python3 -m json.tool .vscode/launch.json`.
3. Check that the HTML has the exact title, references both `styles.css` and `project-data.json`, and renders cards with status, `recentActivity`, and priority.
4. Check for `.dashboard`, `.project-card`, `border-radius`, and `box-shadow` in the stylesheet.
5. Check every project has `name`, `owner`, `status`, `recentActivity`, and `priority`.
6. Select **Run Project Pulse Dashboard** in VS Code. Verify it serves from `app/`, opens `/index.html`, and displays populated cards rather than a directory listing. Check a narrow viewport and the visible loading/error/empty states where practical; stop the server afterward.
7. The existing Step 3 workflow checks file presence, keyphrases, and JSON parsing. Those checks do **not** prove successful browser rendering or launch behavior, so the manual preview remains necessary.

## Open questions

- Should each project include a `summary` field? The brief requests contributor-friendly summaries, but its explicit required schema omits that field.
- Is the Python debugger extension available in the target Codespace for the requested launch configuration? Verify before relying on VS Code’s Run and Debug behavior.
- Should the plan specify a minimum number of sample projects or exact status/priority values? The repository materials inspected do not define either.

## Research references

- Repository requirements: `.github/project-pulse-brief.md`, `.github/steps/2-step.md`, and `.github/steps/3-step.md`.
- Agent roles: `.github/agents/designer.agent.md`, `.github/agents/coder.agent.md`, and `.github/agents/planner.agent.md`.
- Automated checks: `.github/workflows/3-step.yml`.
- VS Code launch configurations and `serverReadyAction`: [VS Code debugging configuration](https://code.visualstudio.com/docs/debugtest/debugging-configuration).
- Python preview server: [Python `http.server` documentation](https://docs.python.org/3/library/http.server.html).
- Python debugger availability: [VS Code Python debugging](https://code.visualstudio.com/docs/python/debugging).
