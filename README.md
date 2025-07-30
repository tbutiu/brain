# Brain: A Multi-Agent Framework

This repository contains a multi-agent framework designed to analyze and report on a given "Goal". The framework operates in a staged workflow, with different agents collaborating to produce a final report.

This project also serves as an interesting case study in self-orchestration. The entire multi-agent workflow, including the different stages and agent handoffs, is coordinated by the Gemini model itself, interacting through the Gemini CLI. This demonstrates a novel approach to creating complex, autonomous behaviors from high-level directives. We encourage you to read the `GEMINI.md` file to see how a few simple prompt directives can be used to generate the sophisticated, multi-step process documented here.

## How to Run

To initiate a run, provide a prompt starting with the key phrase `GOAL:`.

**Example:**

```
GOAL: Analyze the impact of AI on the US stock market and provide a report.
```

### Providing Pre-Read Materials (Optional)

You can provide the agents with initial context by placing files in the top-level `info` directory.

1.  Add any relevant files (`.md`, `.txt`, `.pdf`, etc.) to the `/info` directory. This can be done at any time **before** starting a run.
2.  When you initiate a new `GOAL:`, the framework will automatically detect these files, present you with a list, and ask you to select which ones the agents should read for that specific run.
3.  The content of the selected files will be used as the starting context for the C-Suite agents. This allows for a library of reusable documents across different runs.

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

5.  **Stage 4: Synthesis & Reporting (Report-Writer Agents)**
    *   **Agents**: `JuniorReportWriter`, `SeniorReportWriter`.
    *   **Process**: The writers synthesize the entire `transcript.md` to construct the initial draft of the detailed `report.md`.
    *   **Output**: A draft `report.md` file ready for review.

6.  **Stage 5: C-Suite Review & Feedback (Iterative Loop)**
    *   **Agents**: `ChiefExecutiveOfficer`, `ChiefOperatingOfficer`, etc.
    *   **Process**: The C-Suite agents review the generated `report.md` against the strategic objectives defined in Stage 1.
        *   **If the report is approved:** The run is considered complete.
        *   **If the report requires revision:** The C-Suite provides specific feedback, asking for additional information, deeper analysis, or clarification. This feedback serves as a new set of high-level objectives.
    *   **Output**: Either final approval of the `report.md` or a list of feedback points and new requirements.

7.  **Iteration Loop**
    *   If the C-Suite provides feedback, the process loops back to **Stage 2: Tactical Breakdown**.
    *   The Project Management agents will take the C-Suite's feedback and create new `WorkItem`s to address them.
    *   The workflow then proceeds through **Stage 3 (Execution)** and **Stage 4 (Synthesis & Reporting)** again, generating a revised `report.md`.
    *   This iterative process continues until the C-Suite gives their final approval in **Stage 5**.

## Run Directory & Artifacts

Each run will have a unique directory inside the `runs` directory. The directory name will be prefixed with a timestamp in the format `YYYYMMDD_hhmmss_<short_goal>`, where `<short_goal>` is a brief, 10-20 character version of the goal that best describes it.

Within this directory, the following files will be generated:

*   **`transcript.md`**: A detailed log of all agent interactions. This includes not just the results of each `WorkItem`, but also the detailed internal monologue, discussions, and step-by-step reasoning of the agents as they perform their tasks.
*   **`report.md`**: The final, user-facing report. This is a comprehensive, boardroom-quality document that leads with a strong executive summary and includes detailed sections on methodology, macroeconomic analysis, sector deep dives, company profiles, risk analysis, and the final strategic recommendation.
