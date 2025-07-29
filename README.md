# Brain: A Multi-Agent Framework

This repository contains a multi-agent framework designed to analyze and report on a given "Goal". The framework operates in a staged workflow, with different agents collaborating to produce a final report.

## Framework

The basic concept is a "Goal" that will be analyzed and reported on in a "run". Each "run" will have its own working directory in the `runs` subdirectory.

### Core Concepts

*   **Goal**: A statement or question that will need to be analyzed and reported on.
*   **WorkItem**: A task to be completed by an agent. It has a `description` and a `result`.
*   **Run**: Manages the state for a given `Goal`. It tracks all `WorkItem`s and other necessary state.
*   **Agent Persona**: A definition of an agent's capabilities, expertise, and personality, stored as a heading in the `agents.md` file.

### Staged Workflow

1.  **Initiation**:
    *   The user provides a `GOAL:` prompt.
    *   All Agent Personas from `agents.md` are loaded.
    *   A `Run` is initiated, and its unique directory is created.

2.  **Stage 1: Strategic Direction (C-Suite Agents)**
    *   **Agents**: `ChiefExecutiveOfficer`, `ChiefOperatingOfficer`, etc.
    *   **Process**: The C-Suite agents collaborate to analyze the `GOAL`, define the overall strategy, and establish success metrics. Their detailed discussion is logged.
    *   **Output**: A refined goal and a set of high-level strategic objectives.

3.  **Stage 2: Tactical Breakdown (Project Management Agents)**
    *   **Agents**: `SeniorProjectManager`, `JuniorProjectManager`.
    *   **Process**: The `SeniorProjectManager` breaks down the strategic objectives into major epics. The `JuniorProjectManager` then decomposes those epics into a granular, actionable list of `WorkItem`s with assigned agents.
    *   **Output**: A comprehensive list of `WorkItem`s.

4.  **Stage 3: Execution (Worker Agents)**
    *   **Agents**: Specialized workers (e.g., `Researcher`, `Analyst`).
    *   **Process**: Worker agents execute `WorkItem`s in sequence. All actions, including the agent's internal reasoning and the data gathered, are logged to `transcript.md`.
    *   **Output**: A list of completed `WorkItem`s with their detailed results.

5.  **Stage 4: Final Reporting (Report-Writer Agents)**
    *   **Agents**: `JuniorReportWriter`, `SeniorReportWriter`.
    *   **Process**: The writers synthesize the entire `transcript.md` to construct the final, detailed `report.md`.
    *   **Output**: The final `report.md` file.

## How to Run

To initiate a run, provide a prompt starting with the key phrase `GOAL:`.

**Example:**

```
GOAL: Analyze the impact of AI on the US stock market and provide a report.
```

## Run Directory & Artifacts

Each run will have a unique directory inside the `runs` directory. The directory name will be prefixed with a timestamp in the format `YYYYMMDD_hhmmss_<short_goal>`, where `<short_goal>` is a brief, 10-20 character version of the goal that best describes it.

Within this directory, the following files will be generated:

*   **`transcript.md`**: A detailed log of all agent interactions. This includes not just the results of each `WorkItem`, but also the detailed internal monologue, discussions, and step-by-step reasoning of the agents as they perform their tasks.
*   **`report.md`**: The final, user-facing report. This is a comprehensive, boardroom-quality document that leads with a strong executive summary and includes detailed sections on methodology, macroeconomic analysis, sector deep dives, company profiles, risk analysis, and the final strategic recommendation.