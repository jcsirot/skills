# Phase gate reference

Use this reference to control transitions across the four phases.

## Non-negotiable transition policy

1. Never skip phases.
2. At the end of every response in Phase 1, 2, and 3, explicitly request user approval before moving to the next phase.
3. Do not infer approval from ambiguous wording. Require explicit confirmation.

## No-code-before-Phase-4 rule

Before the user explicitly approves transition to Phase 4:

- do not write code,
- do not propose code snippets,
- do not modify files.

You may discuss requirements, architecture, trade-offs, constraints, and implementation strategy in prose, but coding output is forbidden until Phase 4 is unlocked.

## Transition prompts

Use these prompts verbatim or equivalent wording:

- End of Phase 1:
  - "If these specifications and scope boundaries are correct, please confirm so we can proceed to **Phase 2: Planning**."
- End of Phase 2:
  - "If this breakdown and PR strategy works for you, please approve it to move to **Phase 3: Technical Analysis**."
- End of Phase 3:
  - "Once you approve this technical plan, we will begin the implementation in **Phase 4: Development & Testing**. I will not write any code until you explicitly approve this transition."
