# Multi-Agent Framework

The basic concept will be a "Goal" that will be analyzed and reported on in a "run". Each "run" will have its own working directory in runs subdirectory.

## Core Concepts

*   **Goal**: A statement or question that will need to be analyzed and reported on.
*   **WorkItem**: A task to be completed by an agent. It has a `description` and a `result`.
*   **Run**: Manages the state for a given `Goal`. It tracks all `WorkItem`s and other necessary state.
*   **Agent Persona**: A definition of an agent's capabilities, expertise, and personality, stored as a heading in the `agents.md` file.

## Run Directory & Artifacts

Each run will have a unique directory inside the `runs` directory. The directory name will be prefixed with a timestamp in the format `YYYYMMDD_hhmmss_<short_goal>`, where `<short_goal>` is a brief, 10-20 character version of the goal that best describes it.

Within this directory, the following files will be generated:

*   `transcript.md`: A detailed log of all agent interactions, including every `WorkItem` description and result.
*   `report.md`: The final, user-facing report generated after all work is complete.

## Staged Workflow

1.  **Initiation**:
    *   The user provides a `GOAL:` prompt.
    *   All Agent Personas from `agents.md` are loaded.
    *   A `Run` is initiated, and its unique directory is created.

2.  **Stage 1: Strategic Direction (C-Suite Agents)**
    *   **Agents**: `ChiefExecutiveOfficer`, `ChiefOperatingOfficer`, etc.
    *   **Process**: The C-Suite agents collaborate to analyze the `GOAL`, define the overall strategy, and establish success metrics.
    *   **Output**: A refined goal and a set of high-level strategic objectives.

3.  **Stage 2: Tactical Breakdown (Project Management Agents)**
    *   **Agents**: `SeniorProjectManager`, `JuniorProjectManager`.
    *   **Process**: The `SeniorProjectManager` breaks down the strategic objectives into large tasks. The `JuniorProjectManager` then decomposes those tasks into granular, actionable `WorkItem`s.
    *   **Output**: A comprehensive list of `WorkItem`s.

4.  **Stage 3: Execution (Worker Agents)**
    *   **Agents**: Specialized workers (e.g., `Researcher`, `Coder`, `Writer`).
    *   **Process**: Worker agents execute `WorkItem`s in a loop. They can complete tasks, use tools, or generate new sub-tasks. All actions are logged to `transcript.md`.
    *   **Output**: A list of completed `WorkItem`s with their results.

5.  **Stage 4: Final Reporting (Reporter Agent)**
    *   **Agent**: `Reporter`.
    *   **Process**: Synthesizes the `transcript.md` and all `WorkItem` results into a final, coherent report.
    *   **Output**: The `report.md` file.

## Execution Trigger

To initiate a run, the user will provide a prompt starting with the key phrase `GOAL:`.