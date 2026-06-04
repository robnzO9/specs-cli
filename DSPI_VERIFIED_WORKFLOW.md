# DSPI Verified Workflow

**Discovery → Specification → Planning → Implementation**

Combines **DSPI** with **ASPICE-aligned** quality practices for traceability, artifact discipline, and governance.

> **Note**: This workflow is *inspired by* and *aligned with* Automotive SPICE (ASPICE) process dimensions, but is **not a full ASPICE-compliant process**. It does not define capability levels, process attributes (PA 1.1–3.2), or assessment-ready evidence as required by the ASPICE PAM. The ASPICE dimension labels (REQ, DES, IMP, VER, CM, QA, SUP) are used as an organizing vocabulary. For formal ASPICE supplier assessment, additional process governance is required.

---

## ASPICE Dimensions

| Dimension | Focus | Key Artifacts |
|-----------|-------|---------------|
| **REQ** | Requirements capture, analysis, validation | `specs/[feature]/STORY.md`, `*-nfr.md`, `*-api-contract.md` |
| **DES** | System design, detailed design, design review | `architecture/`, `*-design.md` |
| **IMP** | Code, review, integration, build | `src/`, `CODE_REVIEW_FINDINGS.md` |
| **VER** | Unit, integration, system, acceptance, NFR tests | `tests/`, `TEST_EXECUTION_REPORT.md` |
| **CM** | Version control, baselines, traceability | `.git/`, `REQUIREMENTS_TRACEABILITY.md` |
| **QA** | Quality gates, metrics, standards | `quality-metrics.md`, review findings |
| **SUP** | Documentation, risk management | `docs/`, `risk-register.md` |

---

## Folder Structure

```
project-root/
├── specs/
│   ├── api-contract.md               ← Global API spec
│   ├── data-model.md                 ← Global data model
│   ├── business-logic.md             ← Global business logic
│   ├── infrastructure.md             ← Global infrastructure
│   ├── ui-design.md                  ← Global UI patterns
│   │
│   └── [NN-feature]/
│       ├── STORY.md                  ← REQ: Feature requirements
│       ├── [NN-feature]-api-contract.md ← REQ: APIs (or "Not Applicable")
│       ├── [NN-feature]-data-model.md   ← REQ: Data structures (or reference)
│       ├── [NN-feature]-ui-design.md    ← REQ: UI design (or "Not Applicable")
│       ├── [NN-feature]-business-logic.md ← REQ: Workflows and rules
│       ├── [NN-feature]-nfr.md          ← REQ: Non-functional requirements
│       ├── [NN-feature]-plan.md         ← IMP: Implementation plan
│       ├── [NN-feature]-traceability.md ← CM:  Req → Code → Test mapping
│       └── [NN-feature]-testing-strategy.md ← VER: IF novel test approach
│
├── architecture/
│   ├── infrastructure.md             ← DES: System infrastructure
│   ├── nfr-baseline.md              ← DES: Baseline metrics
│   ├── risk-register.md             ← SUP: Risks and mitigation
│   ├── quality-metrics.md           ← QA:  Quality targets
│   │
│   └── [NN-feature]/                ← IF: Architecture changes needed
│       ├── system-design.md          ← DES: Component overview
│       ├── detailed-design.md        ← DES: Interfaces, class diagrams
│       └── design-review-findings.md ← QA:  Formal review results
│
├── src/                              ← IMP: Implementation
├── tests/                            ← VER: All tests (REQUIRED)
├── docs/                             ← SUP: Documentation
└── REQUIREMENTS_TRACEABILITY.md      ← CM:  Master req→code→test matrix
```

---

## Feature Specification Documents

Every feature creates the **same 9 spec documents**. Adjust **depth**, not **presence**.

| Document | ASPICE | Content Guidance |
|----------|--------|-----------------|
| **STORY.md** | REQ | User story, acceptance criteria, scope, business value |
| **[NN-feature]-api-contract.md** | REQ | Endpoints & payloads if APIs exist; otherwise `"Not Applicable: [reason]"` |
| **[NN-feature]-data-model.md** | REQ, DES | New entities/relationships; or brief reference to global if unchanged |
| **[NN-feature]-ui-design.md** | REQ, DES | Layouts, flows, interactions if UI exists; otherwise `"Not Applicable: [reason]"` |
| **[NN-feature]-business-logic.md** | REQ | Algorithms, workflows, rules; or `"Inherits from [reference]"` if unchanged |
| **[NN-feature]-nfr.md** | REQ | Performance/security/reliability targets; or `"See global nfr-baseline.md"` |
| **[NN-feature]-plan.md** | IMP, CM | Phases, tasks, deliverables, quality gates |
| **[NN-feature]-traceability.md** | CM | Every requirement ID → design → code → test |
| **[NN-feature]-testing-strategy.md** | VER | Optional: If novel test approach required |

> **Principle**: Don't skip documents — use "Not Applicable" or reference existing docs. This keeps governance consistent and auditable across all feature types.

---

## Phase 1: Discovery (D)
**ASPICE-Aligned Focus**: REQ + DES extraction, QA + SUP baseline

### 1.1 Codebase Discovery (existing projects only)

**Run**: `/sc_discover`

Generates global specs in `specs/`:
- `api-contract.md`, `business-logic.md`, `data-model.md`, `infrastructure.md`, `ui-design.md`

Also create manually in `architecture/`:
- `infrastructure.md`, `nfr-baseline.md`, `risk-register.md`, `quality-metrics.md`

Review and adapt all generated files to match the actual project state.

### 1.2 Feature Discovery

Write `specs/[feature-name]/STORY.md` manually:

```markdown
# [Feature Name]

## User Story
As a [user], I want [capability], so that [business value]

## Acceptance Criteria
- [ ] Criterion 1
- [ ] Criterion 2

## Feature Description
[Context, scope, boundaries, constraints]
```

> **Tip**: For the first feature of a new project, include Vision Statement, General Architecture, Technology Stack, and Feature Boundaries to establish the project baseline.

**Quality Gate**:
```
☐ Global specs extracted and reviewed
☐ Architecture documented (infrastructure.md, nfr-baseline.md, risk-register.md, quality-metrics.md)
☐ STORY.md written per feature with acceptance criteria
```

---

## Phase 2: Specification (S)
**ASPICE-Aligned Focus**: REQ specification + DES design + VER test planning

**Run**: `/sc_specify with @STORY.md`

Creates feature-specific specs from STORY.md. Review and complete **all 9 feature spec documents**.

Also create if applicable:
- `architecture/[NN-feature]/system-design.md` — if significant architecture changes
- `architecture/[NN-feature]/detailed-design.md` — if complex component design needed
- `[NN-feature]/[NN-feature]-testing-strategy.md` — if test approach differs from standard

**Quality Gate**:
```
☐ All 9 feature spec documents created (with "Not Applicable" or references where appropriate)
☐ File naming consistent: all files follow [NN-feature] pattern matching directory name
☐ Traceability plan defined: every requirement mapped to at least one test
☐ Architecture design documented (if architecture changes)
☐ Testing approach planned (>80% code coverage target)
☐ Stakeholder review completed
```

---

## Phase 3: Planning (P)
**ASPICE-Aligned Focus**: IMP planning + CM baselines

**Run**: `/sc_plan with @specs/[NN-feature]/STORY.md`

Creates `specs/[NN-feature]/[NN-feature]-plan.md` with phases, tasks, deliverables, and quality gates traced to requirements.

**Quality Gate**:
```
☐ All phases and tasks defined with deliverables
☐ Tasks traced to requirements
☐ Testing tasks included per phase
☐ Quality gates defined per milestone
☐ Plan approved by technical lead
```

---

## Phase 4: Implementation (I)
**ASPICE-Aligned Focus**: IMP + VER + CM

**Run**: `/sc_implement with @specs/[NN-feature]/[NN-feature]-plan.md`

### Code & Review (IMP)
- Implement feature following design documents
- Reference requirement IDs in commits: `Impl REQ-001: description`
- Document code review findings in `CODE_REVIEW_FINDINGS.md` if formal review conducted

### Verification & Validation (VER)
- `tests/unit/[NN-feature]/` — unit tests (>80% coverage)
- `tests/integration/[NN-feature]/` — component interaction tests
- `tests/system/[NN-feature]/` — end-to-end requirement validation
- `tests/acceptance/[NN-feature]/` — user scenarios from STORY.md
- `TEST_EXECUTION_REPORT.md` — results summary
- `NONFUNCTIONAL_TEST_RESULTS.md` — if NFRs were defined

### Traceability & Sign-off (CM + REQ)

Update `REQUIREMENTS_TRACEABILITY.md`:
```
REQ-001: [Requirement description]
  Specified:    specs/[NN-feature]/STORY.md
  Designed:     architecture/[NN-feature]/system-design.md
  Implemented:  src/[NN-feature]/module.py
  Tested:       tests/unit/[NN-feature]/test_module.py::TestClass::test_case
  Status:       ✓ Implemented  ✓ Verified  ✓ Validated
```

**Quality Gate**:
```
☐ Code review completed (if team policy requires)
☐ Unit test coverage >80%
☐ All integration, system, and acceptance tests passed
☐ NFR targets met (if NFRs defined)
☐ EVERY requirement in STORY.md traced in REQUIREMENTS_TRACEABILITY.md
☐ EVERY requirement traced to at least one test
☐ All defects resolved or accepted with justification
☐ Stakeholder sign-off obtained (if required by policy)
```

---

## Quality Gates Summary

| Phase | Gate Condition |
|-------|---------------|
| **D → S** | Global specs + architecture + STORY.md complete |
| **S → P** | All 9 feature specs + traceability plan + design (if needed) complete |
| **P → I** | Implementation plan approved with traceable tasks |
| **I → Done** | All tests passing + traceability matrix complete + sign-off |

**No phase proceeds without passing its quality gates.**

---

## ASPICE-Aligned Quality Checklist

> These items reflect ASPICE-*inspired* practices. They are not a substitute for a formal ASPICE capability assessment.

- ☐ **REQ**: STORY.md with acceptance criteria + all 9 spec documents
- ☐ **DES**: Design documentation (if architecture changes)
- ☐ **IMP**: Code commits with requirement IDs
- ☐ **VER**: Tests covering >80% of code; all test types executed
- ☐ **CM**: `REQUIREMENTS_TRACEABILITY.md` — every requirement linked to code and test
- ☐ **QA**: Quality gates passed at each phase transition
- ☐ **SUP**: Feature plan and documentation up to date

