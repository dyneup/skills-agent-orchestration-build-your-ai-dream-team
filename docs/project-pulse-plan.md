# Project Pulse dashboard implementation plan

## Summary

Build a small, dependency-free static dashboard that presents the projects described in the Project Pulse brief. Contributors should be able to scan project names, owners, status, recent activity, and priority, with a short summary per project, clear status and priority treatments, and a responsive, accessible layout.

The repository currently contains the dashboard brief and agent definitions, but not the `app/` implementation or a VS Code launch configuration. Keep the work within the four requested implementation files and this plan; do not introduce a framework or package manifest unless an implementation blocker is found and agreed.

## Responsibilities and file assignments

| Role | Assigned files | Responsibilities |
| --- | --- | --- |
| **Planner** | `docs/project-pulse-plan.md` | Confirm requirements, sequence work, document file ownership, dependencies, parallel work, and validation. Resolve or flag open implementation choices before conflicting work begins. |
| **Designer** | `app/styles.css`; design guidance for `app/index.html` | Define information hierarchy, card layout, typography, spacing, responsive behavior, status and priority visual treatments, focus states, and contrast. Provide deterministic hooks such as `.dashboard` and `.project-card`; coordinate the required markup hooks with the Coder. |
| **Coder** | `app/index.html`, `app/project-data.json`, `.vscode/launch.json` | Create semantic, accessible dashboard markup; define and populate the JSON data contract; load and render project data; configure a deterministic VS Code launch flow that serves the `app/` directory and opens `index.html`. Integrate the Designer's agreed hooks and report validation results. |

## Ordered implementation steps

1. **Confirm the shared contract.** Planner confirms the brief's required fields and data-loading approach. Agree on stable markup/CSS hooks between Designer and Coder before integration.
2. **Create the project data.** Coder adds a top-level `projects` array to `app/project-data.json`. Every sample project has `name`, `owner`, `status`, `recentActivity`, and `priority`, plus a concise contributor-friendly summary. Use a small, representative set of projects and consistent status/priority values.
3. **Design and style the dashboard.** Designer creates `app/styles.css` for a polished, readable card-based dashboard, including responsive layout, visible status badges, priority/risk cues, hover/focus states, and reduced-motion-aware transitions if motion is used.
4. **Build the page and data rendering.** Coder creates `app/index.html` with semantic landmarks, a clear Project Pulse heading, and an accessible loading/error state. Fetch the JSON and render each project's required fields without relying on `file://` access. Keep displayed text safe as text content rather than interpreting project data as markup.
5. **Add the run configuration.** Coder creates `.vscode/launch.json` as strict JSON. It must serve with `app/` as the working/root directory and open `index.html` at a deterministic local URL, not expose a directory listing. Prefer tooling already available in the Codespace; document any required VS Code extension or runtime dependency in the handoff if one is necessary.
6. **Integrate and validate.** Designer and Coder verify their class/markup/data contract together. Coder runs the checks below and resolves any integration issues; Orchestrator reviews the final handoff and launch path.

## Dependencies and sequencing

- The Planner's shared data/rendering and CSS-hook contract is a prerequisite for parallel implementation.
- The JSON schema is a prerequisite for the page's renderer; Coder should define it before or alongside the HTML, and keep both changes synchronized.
- Designer's CSS can be developed in parallel with Coder's JSON and initial HTML once the class hooks and content structure are agreed. Final visual verification depends on both sides being integrated.
- The launch configuration can be authored in parallel with the page and data files once the serving approach and target URL are agreed. Its end-to-end verification depends on the app files being present.
- Final validation and handoff are sequential after all four implementation files are integrated.
- No application dependencies are present in the current repository. Prefer native HTML/CSS/JavaScript and the existing Codespace/VS Code capabilities; do not add a build system or package dependencies for this static app without a demonstrated need.

## Edge cases and implementation notes

- `fetch()` for `project-data.json` requires an HTTP server; opening `index.html` directly as a local file is not a valid data-loading test.
- Handle an empty or malformed project list and a failed data request with an understandable on-page message rather than a blank dashboard.
- Ensure long project names, owner names, and activity text wrap without breaking the card layout.
- Use semantic status and priority labels in addition to color so meaning remains available to color-blind users and assistive technology.
- Provide visible keyboard focus, sufficient text/background contrast, and a usable narrow-screen layout.
- Keep the JSON valid and consistent: required fields should be present and status/priority values should be used consistently in rendering and styling.
- Ensure the browser opens `/index.html` from the served `app/` root rather than showing the server's directory index.

## Validation expectations

1. Parse `app/project-data.json` and `.vscode/launch.json` with a JSON parser; confirm the data has a top-level array named `projects` and every project has all five required fields plus a short summary.
2. Inspect `app/index.html` for semantic structure, stylesheet and data paths, loading/error states, and matching Designer-provided CSS hooks.
3. Start the app using **Run Project Pulse Dashboard**. Confirm the launch flow serves from `app/`, opens `index.html`, and does not show a directory listing.
4. In a browser, confirm each JSON project renders with its name, owner, status, recent activity, priority, and summary; check the failed-fetch and empty-data states.
5. Check keyboard navigation and visible focus, status/priority readability without color alone, text contrast, and responsive layouts at narrow and wide viewport sizes.
6. Check browser developer tools for failed requests, JavaScript errors, and missing assets. Record the commands/manual checks and outcomes in the implementation handoff.

## Open implementation choice

The repository does not currently define a static-server dependency or a browser-debug launch convention. Before writing `.vscode/launch.json`, the Coder should choose a serving approach supported by the Codespace and confirm its launch configuration can start the server from `app/` and open the exact `/index.html` URL. Keep this choice dependency-free where practical and state any prerequisite clearly.
