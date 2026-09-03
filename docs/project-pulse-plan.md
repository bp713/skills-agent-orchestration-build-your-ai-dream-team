# Project Pulse implementation plan

## Goal and deliverables

Build a lightweight, polished static Project Pulse dashboard for contributors. The dashboard must make active projects, owners, current status, recent activity, priority or risk, and a short contributor-friendly summary easy to scan. It must open the dashboard UI directly rather than a server directory listing.

Deliverables:

- `app/index.html`: accessible dashboard markup and client-side rendering of project cards.
- `app/styles.css`: the visual system, responsive layout, status and priority treatments, and polished card styling.
- `app/project-data.json`: the source data with a top-level `projects` array.
- `.vscode/launch.json`: a strict JSON launch configuration named `Run Project Pulse Dashboard`.

## Team responsibilities

### Orchestrator

- Owns the overall workflow, keeps the implementation aligned with this plan and the Project Pulse brief, and assigns work to the other agents.
- Resolves disagreements between visual requirements and implementation constraints.
- Tracks dependencies, coordinates handoffs, and confirms that all deliverables and acceptance criteria are covered.
- Leads the final review and reports validation results and any limitations.

### Planner

- Converts the brief into the phases, file ownership, dependencies, acceptance criteria, and validation gates documented here.
- Confirms the required data contract and launch behavior before implementation begins.
- Identifies which work can proceed in parallel and which handoffs must be sequential.
- Updates the plan only when the Orchestrator approves a scope or dependency change.

### Designer

- Defines the information hierarchy for the Project Pulse title, dashboard summary, project cards, status badges, recent activity, priority or risk, and contributor summary.
- Specifies a polished, readable visual direction with clear spacing, contrast, card states, and responsive behavior for narrow and wide viewports.
- Provides accessible interaction and presentation guidance, including semantic structure, keyboard-visible focus, meaningful labels, color-independent status and priority cues, and readable text sizing.
- Reviews the implemented UI against the design intent and flags usability or accessibility issues for the Coder to address.

### Coder

- Implements the approved dashboard in `app/index.html`, `app/styles.css`, and `app/project-data.json` without introducing an unnecessary framework.
- Loads `project-data.json`, renders visible cards using the `project-card` class, and shows each project's `name`, `owner`, `status`, `recentActivity`, and `priority` values.
- Implements responsive and accessible markup and styling, including `.dashboard`, `.project-card`, `border-radius`, and `box-shadow` as appropriate to the design.
- Creates `.vscode/launch.json` as strict JSON with no comments, serving from `app/` with `python3 -m http.server 5500` and opening `http://localhost:%s/index.html`.
- Fixes defects found during the Designer review and validation gates, while keeping changes within the assigned files.

## File assignments and dependencies

| File | Owner | Assignment | Depends on |
| --- | --- | --- | --- |
| `app/project-data.json` | Coder, with Planner contract review | Define representative project records under the top-level `projects` key. Every record includes `name`, `owner`, `status`, `recentActivity`, and `priority`; include a short contributor-friendly summary field if the UI needs one. | Planner's data contract; Designer's display requirements |
| `app/index.html` | Coder, with Designer review | Provide semantic page structure, reference `styles.css` and `project-data.json`, and render multiple visible `project-card` elements with the required project fields. | Data field names; Designer's information hierarchy |
| `app/styles.css` | Coder, guided by Designer | Define the dashboard layout and visual system, including `.dashboard` and `.project-card`, responsive rules, status and priority differentiation, `border-radius`, and `box-shadow`. | Designer's visual and accessibility guidance; HTML class and structure |
| `.vscode/launch.json` | Coder, reviewed by Orchestrator | Define strict JSON for `Run Project Pulse Dashboard`, serve from `app/`, run `python3 -m http.server 5500`, and open `index.html` through `http://localhost:%s/index.html`. | Fixed app location and launch contract in the brief |

The HTML depends on the JSON field contract and CSS selectors. The CSS and data can be drafted independently once the Designer has supplied the shared structure and field requirements. Launch configuration work is independent of the page styling, but launch validation must wait until the app path and entry point are fixed.

## Phased implementation

### Phase 1: Align and specify

1. Orchestrator confirms the Project Pulse brief, required files, launch behavior, and acceptance criteria.
2. Planner confirms the data schema, page requirements, file ownership, dependencies, and validation commands.
3. Designer defines the information hierarchy, card content, visual language, responsive rules, and accessibility expectations.

**Gate:** Orchestrator approves the plan and the Designer's structural guidance before implementation begins.

### Phase 2: Parallel foundation work

After Phase 1, the Coder may work in parallel on these independent foundations:

- Draft `app/project-data.json` with representative records that satisfy the agreed schema.
- Draft the semantic skeleton and data-loading/rendering logic in `app/index.html` against the agreed field names.
- Draft `.vscode/launch.json` with the fixed server command, `app/` working directory, launch name, and `index.html` URL.

The Coder may also draft initial `app/styles.css` rules in parallel with the data and launch work, but the final selectors and layout must follow the Designer's structure. Parallel work must not change the shared data contract or launch contract without Orchestrator approval.

### Phase 3: Integrate and polish sequentially

1. Coder integrates the JSON data contract with the HTML renderer.
2. Coder applies the Designer-approved CSS to the final HTML structure and verifies that every required field is visible and readable.
3. Designer reviews the integrated dashboard at desktop and mobile widths for hierarchy, spacing, contrast, focus states, and color-independent meaning.
4. Coder addresses Designer findings and performs a local browser smoke test.
5. Orchestrator checks that all four assigned files are present and that no required behavior was lost during revisions.

These steps are sequential because CSS review depends on the final markup, browser behavior depends on the integrated data and page, and final coordination depends on the reviewed implementation.

### Phase 4: Validate and hand off

1. Validate both JSON files with a JSON parser: `app/project-data.json` and `.vscode/launch.json`.
2. Start the `Run Project Pulse Dashboard` launch configuration and confirm the browser opens `/index.html` from the `app/` directory and displays Project Pulse cards rather than a directory listing.
3. Perform responsive and accessibility checks at narrow and wide viewport sizes.
4. Run `scripts/validate-exercise.sh` if it is available and record its result.
5. Orchestrator documents the completed work, participating agents, validation evidence, and any known limitations for the final handoff.

## Parallel versus sequential decisions

### Work that can run in parallel

- Planner can document acceptance criteria while Designer develops the visual and accessibility direction.
- Once the contracts are approved, Coder can draft project data, initial HTML, initial CSS, and launch configuration as separate work items in parallel.
- JSON syntax validation for `app/project-data.json` and `.vscode/launch.json` can run in parallel after both files exist.

### Work that must be sequential

- The Orchestrator must approve the requirements and Planner's contracts before implementation starts.
- HTML rendering and CSS integration must follow agreement on data field names and the Designer's structure.
- Designer's integrated review must follow the first combined HTML, CSS, and data implementation.
- Browser/launch validation must follow creation of all app files and `.vscode/launch.json`.
- Final handoff and repository validation must follow the implementation review and focused checks.

## Acceptance criteria

- The four deliverables exist at exactly `app/index.html`, `app/styles.css`, `app/project-data.json`, and `.vscode/launch.json`.
- `app/index.html` has the exact title `Project Pulse`, references `styles.css` and `project-data.json`, and renders multiple visible project cards with class `project-card`.
- Each visible card shows the project name, owner, status, recent activity, and priority or risk information, with a short contributor-friendly summary available in the UI.
- `app/project-data.json` is valid JSON with a top-level `projects` array; every project has `name`, `owner`, `status`, `recentActivity`, and `priority`.
- `app/styles.css` includes `.dashboard` and `.project-card`, creates clear visual hierarchy, and includes polished card styling with `border-radius` and `box-shadow`.
- The page is responsive, readable, keyboard navigable, semantically structured, and does not rely on color alone to communicate status or priority.
- `.vscode/launch.json` is strict JSON with no comments, contains `Run Project Pulse Dashboard`, serves from `app/` using `python3 -m http.server 5500`, and opens `http://localhost:%s/index.html`.
- Launching the configuration shows the Project Pulse dashboard from `index.html`, not a directory listing.
- The repository validator passes, or any unavailable check is explicitly recorded as an environment limitation.

## Validation expectations

- **JSON validation:** Run `python3 -m json.tool app/project-data.json` and `python3 -m json.tool .vscode/launch.json`. Also inspect the parsed data to confirm the top-level `projects` array and required fields for every record.
- **Browser and launch validation:** Use Run and Debug with `Run Project Pulse Dashboard`; confirm the server uses `app/`, the browser URL ends in `/index.html`, the title and project cards are visible, data loads without console errors, and stopping the preview leaves no required process running.
- **Responsive checks:** Inspect at a narrow mobile viewport and a wide desktop viewport. Confirm cards reflow without horizontal scrolling, text remains inside its containers, spacing stays readable, and no controls or content overlap.
- **Accessibility checks:** Use semantic headings and landmarks, descriptive labels, keyboard navigation with visible focus, sufficient text/background contrast, meaningful status and priority text or icons in addition to color, and sensible reading order. Check the page with browser accessibility tools when available.
- **Repository validator:** Run `bash scripts/validate-exercise.sh` when the script and its prerequisites are present. Treat a nonzero result as a release blocker unless it reports a pre-existing or unavailable environment dependency; record the exact limitation rather than silently skipping it.
- **Orchestrator evidence:** Record the commands or tools used, their pass/fail results, browser observations, and any remaining limitations in the final handoff.
