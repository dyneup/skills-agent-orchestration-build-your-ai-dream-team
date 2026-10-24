# Agent team for Mona's Project Pulse dashboard

We will use a four-agent team defined under the repository's agent folder to orchestrate the build of Mona's Project Pulse dashboard. The work is coordinated through GitHub Copilot CLI in a Codespace, with each specialist handling a distinct part of the delivery flow.

## 1. Orchestrator
- Model: Claude Opus 5.5 (copilot)
- Responsibility: Breaks the project into phases, assigns work to the right specialist agents, manages dependencies, and verifies that the combined result hangs together.
- Definition: `.github/agents/orchestrator.agent.md`

## 2. Planner
- Model: Claude Opus 5.5 (copilot)
- Responsibility: Researches the repository and requirements, then produces the implementation plan, file ownership, sequencing, parallel work, edge cases, and validation expectations.
- Definition: `.github/agents/planner.agent.md`

## 3. Designer
- Model: Gemini 3.7 Flash (copilot)
- Responsibility: Focuses on UI/UX, accessibility, information hierarchy, interaction flow, and visual polish for the dashboard so it feels like a real Project Pulse frontend.
- Definition: `.github/agents/designer.agent.md`

## 4. Coder
- Model: GPT-5.5 (copilot)
- Responsibility: Implements the actual static app files, logic, and supporting configuration for the dashboard in the assigned code scope.
- Definition: `.github/agents/coder.agent.md`

## Team workflow

The Orchestrator coordinates the specialists, the Planner creates the execution roadmap, the Designer shapes the experience, and the Coder implements the dashboard. The repository also includes the dashboard brief in `.github/project-pulse-brief.md`, which sets the product requirements for the app.

> This project uses GitHub Copilot CLI in a Codespace to orchestrate the work instead of handling everything in one undifferentiated prompt.
