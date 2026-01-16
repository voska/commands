$ARGUMENTS

## Phase 1: Research
Before designing anything, research current best practices:
- Web search for canonical 2026 patterns for the technologies involved
- Read relevant existing code to understand current patterns
- Check git history for context on past decisions

## Phase 2: Think Deeply
Question every assumption:
- Is this the right problem to solve?
- What's the simplest solution that could work?
- Can this be solved by **deleting code** rather than adding it?
- What code can be removed to make this simpler?

## Phase 3: Design
Architect the solution:
- Prefer established patterns over clever inventions
- Keep it KISS - the best solution is often the simplest
- Keep it DRY - but don't over-abstract prematurely
- Every function name should be obvious, every abstraction natural

## Phase 4: Plan
Present your approach before implementing:
- Outline the solution and reasoning
- Identify files to modify
- Note any risks or edge cases
- Get approval, then execute

The goal: code so clean and elegant it would impress even Linus Torvalds.
