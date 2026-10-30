# Agent team for Mona's Project Pulse dashboard

I will use a four-agent custom team, coordinated through GitHub Copilot CLI in a Codespace, to plan, design, implement, and integrate Mona's Project Pulse dashboard.

- Planner — Target model: Claude Opus 5.5 (copilot). Responsibility: researches the repository, reviews docs and dependencies, identifies risks and edge cases, and produces a concrete implementation plan for the dashboard work. Definition: `.github/agents/planner.agent.md`.
- Designer — Target model: Gemini 3.7 Flash (copilot). Responsibility: focuses on UX, information hierarchy, accessibility, responsive layout, and visual polish for the dashboard experience. Definition: `.github/agents/designer.agent.md`.
- Coder — Target model: GPT-5.5 (copilot). Responsibility: writes and validates the actual application logic and feature code, staying within the scope assigned by the orchestrator. Definition: `.github/agents/coder.agent.md`.
- Orchestrator — Target model: Claude Opus 5.5 (copilot). Responsibility: breaks the work into phases, delegates to the specialized agents, coordinates dependencies, and ensures the final result fits together cleanly. Definition: `.github/agents/orchestrator.agent.md`.

This team is defined under the repository's agent folder and is run through GitHub Copilot CLI in the Codespace so the work can be staged, delegated, and reviewed as a coordinated engineering workflow.
