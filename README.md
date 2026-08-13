# Logic Puzzle Toolbox

This repository contains a small Agent Skill for coding agents working on deterministic logic-puzzle generators and solvers.

The installable skill lives at [`skills/logic-puzzle-toolbox/`](skills/logic-puzzle-toolbox/). This README is deliberately **outside** that skill directory. It documents the design intent and maintenance philosophy for humans; it is not part of the normal agent-facing context and is intentionally not referenced from `SKILL.md`.

## Why this skill exists

A capable coding model already knows a great deal about backtracking, constraint programming, SAT/SMT, search, testing, and ordinary software design. Repeating that material consumes context without changing many decisions.

The gap this skill is meant to address is different: agents can build generators that are technically successful while failing to notice that the resulting puzzles are weak.

Typical failures include:

- puzzles are unique and deterministically solvable but mostly clerical;
- clues look varied syntactically but repeatedly play the same logical role;
- long solves contain many forced steps but little synthesis or payoff;
- progressive reveal systems have sophisticated gating while merely spoon-feeding answers;
- large corpora contain thousands of literal variants of a small number of structural recipes;
- solver difficulty, clue count, reachability, or similar proxies are treated as if they established player-facing quality;
- the generator and its audit text agree with each other while both disagree with the encoded puzzle semantics.

A useful shorthand for the project is:

> Make the agent harder to fool by a generator that is technically successful but produces weak puzzles.

## Design stance

The skill is intended to be **opinionated about qualities and pluralistic about mechanisms**.

It can make strong distinctions such as:

- bookkeeping difficulty is not the same as inference difficulty;
- clue complexity, information strength, and deductive role are separate properties;
- reveal progression is not necessarily logical progression;
- combinatorial variety is not necessarily structural or experiential variety;
- a human-style solve trace is a model whose conclusions depend on its inference vocabulary;
- model uniqueness is not necessarily semantic/player-visible uniqueness.

It should not imply that one generator architecture, solver paradigm, clue language, search algorithm, or optimization method is the correct implementation.

Alternative formulations such as counterexample-guided clue selection, MUS/MCS reasoning, hitting sets, deduction-first generation, novelty search, or Quality-Diversity are included as conceptual doors rather than prescribed workflows.

## What belongs in the skill

The strongest candidates are ideas that satisfy at least one of these tests:

1. A competent coding agent is unlikely to think to inspect the property without prompting.
2. The idea changes how an agent judges apparently successful output.
3. The idea exposes a useful formulation, tool, research vocabulary, or failure mode that would otherwise remain invisible.
4. The idea helps distinguish properties that models commonly conflate.

Material is a weaker candidate when it is standard implementation knowledge, follows trivially from something already present, or merely adds completeness.

Context is treated as a budget. A paragraph earns its place by making better decisions more likely, not by making the reference more encyclopedic.

## Progressive-disclosure structure

The skill is divided by the **object under examination**, because this is a decision an agent can usually make before it knows which conceptual lens will solve the problem:

- **Generator** — what structures can be produced, and what biases that reachable space?
- **Puzzle** — what kind of reasoning does one instance ask a player to perform?
- **Corpus** — how does a generator behave across many outputs?
- **Solver semantics** — what does the formal representation actually mean and prove?

The root `SKILL.md` contains the minimum shared judgments plus routing. Detailed material lives in four one-hop references. Most tasks should need one reference; a second is useful when moving from characterizing a symptom to investigating its cause.

The current references are:

- [`generation-and-design-space.md`](skills/logic-puzzle-toolbox/references/generation-and-design-space.md)
- [`player-experience-and-deduction.md`](skills/logic-puzzle-toolbox/references/player-experience-and-deduction.md)
- [`diversity-and-evaluation.md`](skills/logic-puzzle-toolbox/references/diversity-and-evaluation.md)
- [`solver-semantics-and-verification.md`](skills/logic-puzzle-toolbox/references/solver-semantics-and-verification.md)

A fifth reference is not inherently bad, but splitting material only helps when an agent can reliably decide *before reading it* which file is relevant. Conceptual neatness alone is not enough reason to create another branch in the routing tree.

## Attention is a constraint

Long diagnostic checklists tend to diffuse a model's attention. The player-facing reference therefore uses a deliberately short five-question heuristic rather than an exhaustive puzzle-quality rubric.

The desired pattern is:

```text
small, salient heuristic
        ↓
identify the suspicious property
        ↓
load deeper vocabulary only for that property
```

This is also why similar concepts are sometimes repeated once across references but aggressively deduplicated within a reference. A small amount of cross-file redundancy can make each progressive-disclosure branch self-sufficient; repeated paragraphs within the same loaded context usually do not earn their cost.

## Examples should isolate the quality being taught

Examples can easily teach the wrong lesson. A comparison between a weak and strong puzzle is not useful if the supposedly stronger puzzle also introduces richer clue semantics, extra state, or a different domain mechanic. The model may attribute the improvement to the wrong variable.

Where examples are added, the preference is for **controlled contrasts**: hold unrelated puzzle features as constant as practical and vary the qualitative property being illustrated.

The project also avoids canonizing a particular admired puzzle as the model of "good" design. Named exemplars encourage imitation of surface characteristics. The aim is to extract transferable qualities instead.

## Failure modes we especially care about

### Serial fact transmission

A clue is consumed, converted into an assignment, and mentally discarded; the next clue repeats the process. The puzzle may have many clues and a long reveal sequence without much interaction.

Useful nearby concepts include clue lifetime, reusable intermediate knowledge, convergence, recontextualization, and deduction topology.

### Proxy satisfaction

A specification successfully guarantees properties such as clue reachability, deterministic reveal order, minimum steps, uniqueness, or target solver difficulty. The implementation then treats those successes as evidence that the intended player experience exists.

The recurring question is: **what property was the proxy meant to encourage, and is that property actually present?**

### Surface-only variety

Names, values, themes, clue templates, or random seeds change while the underlying constraint skeleton, clue roles, solve trace, or construction ancestry remains nearly identical.

Useful nearby concepts include expressive range, behavioural descriptors, canonicalization, novelty, Quality-Diversity, and objective-induced concentration.

### Solver semantics leaking into puzzle semantics

Auxiliary variables, symmetry breaking, or internal representations accidentally define what counts as a distinct solution. The verifier answers a precise formal question that is not the question the player-facing puzzle intended to ask.

Useful nearby concepts include semantic projection, equivalence classes, second-solution queries, assumptions, unsat cores, MUS/MCS, and independent verification.

## Language and tone constraints

The agent-facing skill avoids prescribing implementations. It prefers formulations such as "one useful distinction," "another view," or "this connects to" over commands like "use algorithm X."

This does not require neutrality about puzzle quality. The skill can state that uniqueness is a weak proxy for enjoyment, that a chain of direct assignments can be shallow, or that a corpus is structurally narrow despite large literal output.

The intended balance is:

> strong judgment about what is happening; weak commitment about how software must be built.

Jargon is welcome when it gives the agent a precise search term or connects the problem to established work, but important local meaning should not depend on the reader already knowing the term. Acronyms such as MUS/MCS are expanded where they matter; terms such as behavioural descriptor or recontextualization are given a short local explanation.

## Research references

Research earns inclusion when it contributes a concrete lens rather than merely demonstrating relevance to logic puzzles. Examples currently used include work on:

- human-style logic-grid solving and clue lifetime;
- stepwise CSP explanations;
- human-oriented difficulty modelling;
- expressive-range analysis;
- novelty search and Quality-Diversity;
- hitting sets, MUS/MCS, and solver assumptions.

References are kept close to the section where their concepts matter. The skill is not intended to become a literature survey.

## Maintaining the skill

Real generator failures are the most useful source of revisions. When an agent produces or endorses a bad puzzle, the interesting question is often not "what instruction did it fail to follow?" but "what distinction did it fail to notice?"

A good iteration cycle is therefore:

```text
observe a real failure
→ identify the missing judgment or conceptual lens
→ ask whether that lens generalizes beyond the example
→ add the smallest amount of agent-facing context that makes the distinction salient
→ later remove or merge it if other material makes it redundant
```

The README can retain more of the rationale behind those decisions. The installable skill should stay smaller and more operational.

## Packaging

The skill is explicit-invocation only. The installable directory contains `SKILL.md`, `agents/openai.yaml`, and the four references. Repository-level documentation stays outside that directory so it does not compete with task-relevant skill context.

For clients that install a skill from a GitHub path, use the `skills/logic-puzzle-toolbox` directory rather than the repository root.
