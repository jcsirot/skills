# 4-phase workflow (large_feature mode)

Use this reference after the user has confirmed `large_feature` through `SKILL.md`.

## Critical rule

Complete each phase and obtain explicit approval before entering the next one. On resumption or escalation, reuse completed, still-valid approved deliverables; do not replay them. Missing approvals must be obtained rather than inferred.

Phases 1-3 permit read-only exploration, not implementation edits. Approval of a phase does not authorize Git writes or external publication; apply `references/git-governance.md` separately.

## PHASE 1: Product owner (requirements gathering)

Objective: understand business requirements and define scope boundaries before modifying code.

### Guidelines
1. Analyze the request and references collected through `SKILL.md`. If source collection has not happened, perform it first; otherwise do not ask again. Retain document links and ticket identifiers, and record inaccessible sources without claiming to have read them.
2. Ask targeted questions to uncover edge cases, UX details, and hidden complexity.
3. Define explicit boundaries: what is in scope and out of scope. Separate confirmed requirements, assumptions, and open questions.
4. Define observable acceptance criteria. Surface material contradictions between the request and references for user resolution; sources do not replace approval or authorize ticket updates.

### Deliverable
- Concise requirements summary, source references and limitations, in/out of scope, observable acceptance criteria, and remaining assumptions or questions.
- Transition prompt:
  - "If these specifications and scope boundaries are correct, please confirm so we can proceed to **Phase 2: Planning**."

## PHASE 2: Planning (decomposition and PR strategy)

Objective: break the feature into manageable increments and define delivery slicing.

### Guidelines
1. Ground the decomposition in the initial read-only reconnaissance: affected components, existing solutions, dependencies, and available tests.
2. Decompose into incremental user stories with dependency order, expected outcome, and validation for each increment.
3. Propose a provisional PR sequence and branch names using `references/git-governance.md`. Do not create branches merely because their names were approved in a plan.
4. Apply the golden rule `1 Feature = 1 PR` unless safe review requires splitting. Identify assumptions that technical analysis must confirm.

### Deliverable
- Structured user stories, dependencies and validation per increment, provisional PR sequence and branch names, expected commit style, and technical assumptions.
- Transition prompt:
  - "If this breakdown and PR strategy works for you, please approve it to move to **Phase 3: Technical Analysis**."

## PHASE 3: Technical analysis

Objective: produce a robust technical blueprint.

### Guidelines
1. Inspect the relevant code and outline the implementation plan: actual files/components, existing mechanisms to reuse, data/API changes, and architecture impacts.
2. Map acceptance criteria to planned verification. Surface risks, performance and compatibility concerns, migration and rollback needs where applicable, and debt trade-offs.
3. Ask the user to arbitrate important technical choices when multiple viable options exist.
4. Confirm or revise the provisional PR strategy. If findings materially alter approved scope or decomposition, present the affected decisions for reapproval before implementation; do not silently change the plan or restart unaffected phases.

### Deliverable
- Technical plan ready for approval, with acceptance-to-verification mapping and confirmed or revised delivery strategy.
- Transition prompt:
  - "Once you approve this technical plan, we will begin the implementation in **Phase 4: Development & Testing**. I will not write any code until you explicitly approve this transition."

## PHASE 4: Development and testing

Objective: implement production-ready code with tests.

### Guidelines
1. Execute the approved plan incrementally after Git safety checks.
2. Provide evidence appropriate to each acceptance criterion. Add or update automated tests for behavior changes where appropriate; use justified manual or documentation checks when automation is unsuitable. Reuse existing validation tooling rather than inventing a test framework for a documentation-only change.
3. Follow project coding standards and naming conventions.
4. Run the smallest relevant checks, expanding coverage when results or risk warrant it. Record passing, failing, and unexecuted checks separately; report unavailable dependencies or infrastructure and distinguish pre-existing failures from regressions.
5. Keep any authorized commits scoped and aligned with Conventional Commits. Apply branch safety and publication permissions from `references/git-governance.md`.

### Deliverable
- Implementation summary, acceptance-criterion evidence, validation results, and unresolved limitations or blockers.
- Declare completion only when mandatory acceptance criteria are verified. If verification is blocked, say what is implemented and what remains unverified.
- There is no implicit fifth phase or publication step: finishing implementation does not itself authorize commits, pushes, PR creation, or ticket updates.
