# Agent team

I am using GitHub Copilot CLI in a Codespace to orchestrate this custom agent team as we build Mona's Project Pulse dashboard.

| Agent | Target model | Responsibility | Definition |
| --- | --- | --- | --- |
| Orchestrator | Claude Opus 5.5 (copilot) | Coordinates the team without implementing code: requests a plan, assigns file scopes, sequences dependent work, parallelizes independent tasks, and verifies the integrated dashboard. | [`.github/agents/orchestrator.agent.md`](../.github/agents/orchestrator.agent.md) |
| Planner | Claude Opus 5.5 (copilot) | Researches the repository, dependencies, and edge cases; produces an implementation plan with file assignments, task dependencies, and validation expectations. Does not write code. | [`.github/agents/planner.agent.md`](../.github/agents/planner.agent.md) |
| Coder | GPT-5.5 (copilot) | Implements dashboard code and logic within assigned files, handles errors explicitly, and validates behavior. Creates runnable-app support such as `.vscode/launch.json` when assigned. | [`.github/agents/coder.agent.md`](../.github/agents/coder.agent.md) |
| Designer | Gemini 3.7 Flash (copilot) | Creates accessible, responsive UI/UX and styling with clear information hierarchy, project cards, status badges, priorities, and polished visual treatment. | [`.github/agents/designer.agent.md`](../.github/agents/designer.agent.md) |

The Orchestrator starts with the Planner's plan, then delegates implementation and design to the Coder and Designer. Tasks run in parallel only when their file scopes do not overlap and they have no data dependencies; otherwise, they run sequentially. All agents leave staging, committing, and pushing to the learner through Copilot CLI prompts.
