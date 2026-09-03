# Project Pulse agent team

## Agents

### Orchestrator
- **Model:** Claude Opus 4.7 (copilot)
- **Responsibility:** Coordinates the team, delegates work, resolves conflicts, and keeps delivery aligned with Project Pulse goals.
- **Agent file:** `.github/agents/orchestrator.agent.md`

### Planner
- **Model:** Claude Opus 4.7 (copilot)
- **Responsibility:** Defines requirements, breaks work into tasks, and creates an implementation plan.
- **Agent file:** `.github/agents/planner.agent.md`

### Coder
- **Model:** GPT-5.5 (copilot)
- **Responsibility:** Implements the planned features, integrations, tests, and fixes.
- **Agent file:** `.github/agents/coder.agent.md`

### Designer
- **Model:** Gemini 3.1 Pro (copilot)
- **Responsibility:** Designs the user experience, visual system, information architecture, and accessibility approach.
- **Agent file:** `.github/agents/designer.agent.md`

## How the team works together

1. The Orchestrator clarifies the goal, assigns work, and coordinates dependencies.
2. The Planner turns the Project Pulse objective into requirements, user stories, milestones, and acceptance criteria.
3. The Designer proposes the dashboard experience, layout, interaction patterns, and accessibility guidance.
4. The Coder implements the approved plan and design, adding tests and reporting blockers.
5. The Orchestrator reviews progress, integrates the outputs, and requests revisions when needed.
6. The team validates the completed dashboard against the acceptance criteria before release.
