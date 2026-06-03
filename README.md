# [x] Specs CLI

Specs CLI is an agentic CLI for AI-assisted specification-driven development. It applies the DSPI Verified Workflow—combining systematic governance with traceability for auditable, quality-gated feature delivery.

## DSPI Verified Workflow

Ship features deliberately with verified quality gates. DSPI Verified combines specification-driven development with ASPICE-aligned quality practices, enabling traceable, systematic feature delivery with explicit governance. Capture intent, specify neutral requirements, plan confidently, and implement with quality gates and artifact discipline that keep docs and code in sync.

With Specs CLI, each phase has a simple command. Outputs live in your repo, are reviewable, and remain versioned. The agent accelerates documentation and validation; you make the decisions.

- Discovery — Understand the system and define the feature. Extract global specs (`specs/business-logic.md`, `specs/data-model.md`, `specs/api-contract.md`, `specs/ui-design.md`, `specs/infrastructure.md`) and write a clear `STORY.md` describing intent, value, and boundaries.
- Specification — Convert the story into precise, technology‑agnostic specifications split by type: business logic, data model, API contract, and UI design. Resolve open questions early and link decisions back to the story.
- Planning — Translate specifications into an implementation plan: phases, tasks, testing strategy, risks, and integration notes. Every task maps to a spec, making scope and success measurable.
- Implementation — Execute the plan iteratively. Keep documentation and code synchronized; validate with automated checks and human review. When tests pass and specs are satisfied, the feature is complete.

Why teams use DSPI Verified:
- **Clarity**: Specifications are the single source of truth across discovery through implementation.
- **Control**: Humans approve all decisions; AI accelerates documentation and validation.
- **Consistency**: ASPICE-aligned templates and quality gates reduce ambiguity and prevent drift.
- **Traceability**: Every change is traceable from story → specification → design → code → test.
- **Governance**: Explicit quality gates, artifact discipline, and ASPICE process dimensions (REQ, DES, IMP, VER, CM, QA, SUP) ensure systematic, auditable delivery.
- **Verification**: Built-in testing strategy, design reviews, and requirement traceability validate feature completeness.

## Installation

| IDE | 1. Agent Installation | 2. Commands Installation (agentic) |
| --- | --- | --- |
| Roo Code | Click [⋯] → Modes → Import Mode → Select [dspi-verified-developer.yaml](roo-modes/dspi-verified-developer.yaml) | Switch to DSPI Verified Developer and type task: `install commands` |
| Cline | Copy [dspi-verified-developer.md](agents/dspi-verified-developer.md) into `your-project/.clinerules/` | Type task: `install DSPI Verified commands` |
| Windsurf | Copy [dspi-verified-developer.md](agents/dspi-verified-developer.md) into `your-project/.windsurf/rules/` | Type task: `install DSPI Verified commands` |
| Trae AI | Create new Agent with name: *DSPI Verified Developer* → Paste content of [dspi-verified-developer.md](agents/dspi-verified-developer.md) | Switch to DSPI Verified Developer and enter: `install commands` |
| Visual Studio Code | Copy [dspi-verified-developer.md](agents/dspi-verified-developer.md) to `your-project/.github/agents/dspi-verified-developer.agent.md` |  |
| Others | Copy [dspi-verified-developer.md](agents/dspi-verified-developer.md) into your project | Ask: `@dspi-verified-developer.md install commands` |

Now ask the Agent what to do next and it will guide you through the DSPI Verified Workflow.

Want to apply the workflow manually, here is how: [DSPI_VERIFIED_WORKFLOW.md](DSPI_VERIFIED_WORKFLOW.md)

## Customization

This is how you can customize Specs CLI for your specific needs:

1. **Fork the repository**:
    - Fork the Specs CLI repository to your GitHub account.
    - This allows you to make changes and share them with others.

2. **Adapt command management**:
    - Update the `Command Management` section in `agents/dspi-verified-developer.md` to reference your fork.
    - Update the same section in `roo-modes/dspi-verified-developer.yaml` (if you use Roo Code).
    - The URL should look like this in both Agents:
        ```
        https://raw.githubusercontent.com/[your-username]/specs-cli/main/commands/
        ```
    - Commands will now be downloaded from your fork when using your Agent.

3. **Customize specification templates**:
    - Templates are embedded into `sc_discover.md` and `sc_specify.md`.
    - Customize existing templates or add new templates as needed.
    - Changing command structure and logic is not recommended but of course possible.

4. **Create a stable version**:
    - Create a new version branch in your fork (e.g. `custom1`).
    - Push to the new branch (e.g. `custom1`).
    - Update the command URLs in `agents/dspi-verified-developer.md` and `roo-modes/dspi-verified-developer.yaml` (if applicable) to point to your new branch.
    - Example:
        ```
        https://raw.githubusercontent.com/[your-username]/specs-cli/custom1/commands/
        ```
    - Agents are now using the stable version of your fork during command installation.

## Acknowledgments

- **Mastering AI Agents**: Specs CLI templates and project structure were originally developed and documented in the book [Mastering AI Agents](https://mastering-ai-agents.com)
- **HumanLayer**: Specs CLI command structure was heavily influenced by the [HumanLayer](https://www.humanlayer.dev) Claude Code setup

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.