---
name: logic-puzzle-toolbox
description: Reference toolbox for explicitly invoked work on deterministic logic-puzzle generators, solvers, clue systems, human-facing deduction quality, diversity, evaluation, and correctness. Provides design judgment, alternative conceptual lenses, less-obvious techniques, and research pointers without prescribing a generator architecture or solver implementation.
disable-model-invocation: true
metadata:
  version: "0.1.0"
  invocation: "explicit-only"
---

# Logic Puzzle Toolbox

This skill is a toolbox for reasoning about logic-puzzle software rather than an instruction manual. It is deliberately **opinionated about puzzle qualities** while remaining **pluralistic about implementation and generation mechanisms**.

The central distinction is between technical success and puzzle quality. A puzzle can be valid, deterministic, unique, difficult for a machine, and superficially varied while still being repetitive or tedious for a person. Conversely, simple clue forms can participate in rich reasoning when their consequences interact.

Useful design judgments in this skill include:

- uniqueness and deterministic solvability are important properties, but a low bar for player-facing quality;
- effort caused by bookkeeping, scanning, or repeated obvious propagation is qualitatively different from effort caused by inference;
- interesting progress often creates reusable intermediate knowledge rather than only filling final assignments;
- many surface-level clue types can still amount to a narrow logical vocabulary;
- a generator can have an enormous combinatorial output space while occupying a narrow structural or experiential range;
- optimizing measurable properties can create an accidental house style even when no style was explicitly requested.

None of these imply that direct clues, repetition, narrow solve paths, or cleanup phases are inherently undesirable. They can provide setup, pacing, reinforcement, accessibility, or release. The concern is what role they play in the whole solve.

## References by task domain

### Generator construction and design space

[`references/generation-and-design-space.md`](references/generation-and-design-space.md)

Relevant to work involving generator architecture, instance construction, clue selection, clue-language design, optimization objectives, generators that converge on a small family of constructions, or questions about what kinds of puzzles a generator can reach.

Contains alternative generation formulations and connections to search, synthesis, hitting sets, MUS/MCS, counterexamples, and multiple generative mechanisms. The emphasis is on enlarging the agent's conceptual option space rather than choosing an architecture.

### Puzzle design and player-facing deduction

[`references/player-experience-and-deduction.md`](references/player-experience-and-deduction.md)

Relevant to work involving clue design, intended solution experience, human-facing difficulty, puzzles that are valid but dull or clerical, evaluation of a particular clue set, or questions about what makes one solve more satisfying than another.

Contains a compact qualitative heuristic, controlled contrasts, and concepts such as clue interaction, derived intermediate structure, logical payoff, recontextualization, deduction topology, refutation, and bookkeeping load.

### Diversity and corpus evaluation

[`references/diversity-and-evaluation.md`](references/diversity-and-evaluation.md)

Relevant to work involving repetitive or "samey" generated output, comparison of generator versions, selection from a large generated corpus, structural similarity, expressive range, or diversity metrics.

Contains several ways of describing similarity and difference across puzzles, including surface, structural, deductive, solution, and generative-mechanism perspectives, plus connections to expressive-range analysis, novelty search, and quality-diversity research.

### Technical toolbox and correctness

[`references/technical-toolbox-and-correctness.md`](references/technical-toolbox-and-correctness.md)

Relevant to work involving uniqueness, equivalence, solver representation, unusual constraints, independent verification, or technical machinery that may support generation and evaluation.

Contains the less-obvious parts of SAT/SMT/CP tooling: semantic versus auxiliary variables, projected uniqueness, assumptions and cores, MUS/MCS and hitting-set duality, global constraints, symmetry, and verification strategies. Standard introductions to backtracking, CSP, SAT, SMT, or MRV are intentionally omitted.

## Cross-cutting concerns

Some problems naturally span references. A generator whose outputs are repetitive may involve both its reachable design space and corpus-level expressive range. Puzzles that are diverse but tedious may involve both clue/generator design and player-facing deductive character. Apparent uniqueness failures may involve either solver representation or validation semantics.

The reference boundaries are therefore lenses, not mutually exclusive categories.
