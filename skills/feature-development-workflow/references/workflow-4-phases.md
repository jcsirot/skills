# 4-phase workflow (large_feature mode)

Use this reference only when the orchestrator classified the request as `large_feature`.

## Critical rule

Do not skip phases. At the end of each phase, explicitly request user approval before moving to the next one.

## PHASE 1: Product owner (requirements gathering)

Objective: fully understand business requirements and define scope boundaries before touching code.

### Guidelines
1. Analyze the initial feature request.
2. Ask targeted questions to uncover edge cases, UX details, and hidden complexity.
3. Define explicit boundaries: what is in scope and out of scope.

### Deliverable
- Concise requirements summary + acceptance criteria.
- Transition prompt:
  - "If these specifications and scope boundaries are correct, please confirm so we can proceed to **Phase 2: Planning**."

## PHASE 2: Planning (decomposition and PR strategy)

Objective: break the feature into manageable increments and define delivery slicing.

### Guidelines
1. Decompose into incremental user stories.
2. Propose PR sequence and branch names using `references/git-governance.md`.
3. Apply the golden rule `1 Feature = 1 PR` unless safe review requires splitting.

### Deliverable
- Structured user stories, PR sequence, branch names, and expected commit style.
- Transition prompt:
  - "If this breakdown and PR strategy works for you, please approve it to move to **Phase 3: Technical Analysis**."

## PHASE 3: Technical analysis

Objective: produce a robust technical blueprint.

### Guidelines
1. Outline implementation plan (files/components impacted, data/API changes, architecture impacts).
2. Surface risks, performance concerns, compatibility concerns, and debt trade-offs.
3. Ask the user to arbitrate important technical choices when multiple viable options exist.

### Deliverable
- Approved technical plan.
- Transition prompt:
  - "Once you approve this technical plan, we will begin the implementation in **Phase 4: Development & Testing**. I will not write any code until you explicitly approve this transition."

## PHASE 4: Development and testing

Objective: implement production-ready code with tests.

### Guidelines
1. Execute the approved plan incrementally.
2. Ensure every produced change has corresponding automated tests.
3. Follow project coding standards and naming conventions.
4. Keep commits scoped and aligned with Conventional Commits.
5. Apply branch safety and PR policy from `references/git-governance.md`.

### Deliverable
- Complete implementation with passing tests.
