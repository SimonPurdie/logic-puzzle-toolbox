# Generation and Design Space

This reference concerns the space a puzzle generator explores: how instances can come into existence, what the available clue language makes expressible, and how search or optimization can accidentally narrow the resulting style.

It is a catalogue of alternative formulations rather than a preferred workflow.

## Generator architectures as different views of the same problem

Common generator families include, among others:

- **solution-first / reductive generation**: a completed solution exists first, with information subsequently selected, hidden, or removed;
- **clue-first / constraint-first construction**: constraints accumulate while satisfiability, uniqueness, or other properties remain under consideration;
- **constructive generation**: the puzzle and its solution co-evolve or are built together rather than beginning from a fully specified target;
- **ambiguity-first generation**: alternative solutions or underdetermined states become explicit objects, with later constraints separating them;
- **deduction-first generation**: an intended reasoning structure or proof trace is part of the object being synthesized;
- **mutation or transformation**: existing valid instances are changed while preserving selected properties;
- **search or optimization over puzzle encodings**: local search, evolutionary search, MaxSAT/MIP/CP optimization, or other optimizers act over candidate instances;
- **repertoire-oriented generation**: the object of interest is a collection covering different regions of a design space rather than one optimum.

These views expose different variables and failure modes. A large parameter space inside one construction mechanism can still produce a narrow family of logical structures.

## The clue language is part of the generator

The available clue forms define more than presentation. They constrain which distinctions can be expressed and which kinds of intermediate reasoning can occur.

Several kinds of apparent variety can therefore differ:

- **lexical variety**: different wording for essentially the same relation;
- **syntactic variety**: several clue templates with similar logical effect;
- **relational variety**: genuinely different relationships among puzzle entities;
- **deductive-role variety**: clues that participate differently in a solve, such as setup, propagation, synthesis, bottleneck, confirmation, or cleanup.

A generator with dozens of clue templates may still have a narrow logical vocabulary if those templates repeatedly occupy the same role.

Candidate clue languages also delimit optimization claims. A clue set that is minimal or optimal within one candidate language need not be minimal under a richer language containing different relations or compound clues.

## Quality proxies and design specifications

Generator specifications often contain properties intended to encourage a player experience without directly describing that experience.

Examples include:

- every clue is eventually reachable;
- no more than one clue is revealed after an action;
- reveal state is deterministic or path-independent;
- a clue remains sufficient to make progress near the end;
- a minimum number of deduction steps occurs between reveals;
- a target number of clue templates appears;
- an exact solver reports a target difficulty.

These can all be useful constraints. They describe reachability, pacing, determinism, variety, or computational structure. Their satisfaction does not imply that clues interact, that intermediate discoveries are reusable, or that the player performs interesting inference.

A common response to shallow generated puzzles is to enlarge the surface vocabulary—for example by adding comparisons, counts, spatial relations, or compound clues. That can enlarge the design space, but it does not by itself enlarge the **deductive-role vocabulary**. More elaborate clue forms can still repeatedly serve as direct answer delivery, local propagation, or cleanup.

Conversely, very simple clue forms can support substantial reasoning when their consequences overlap and remain partially unresolved.

## Objective-induced style

Optimization pressure can create a recognizable style without representing it explicitly.

For example, an objective combining uniqueness, low clue count, target solver difficulty, and generation speed may have a region of the search space where a particular construction pattern satisfies all four reliably. Search can repeatedly return to that region even when many other valid puzzle structures exist.

This is one explanation for generators that produce large numbers of distinct instances with a small number of recurring "recipes".

The same concern applies to hand-designed heuristics. A deterministic tie-breaker, clue ordering, pruning rule, or canonical construction can become a strong stylistic prior even when it appears to be only an implementation detail.

## Counterexamples, hitting sets, and unavoidable sets

For a fixed target solution, clue selection has a useful connection to counterexamples.

Let `U` be a universe of candidate clues that are all true of target solution `T`. For an alternative solution `M`, the clues that distinguish `T` from `M` form a set:

```text
D(M) = { c in U : c is false in M }
```

Any selected clue set that excludes `M` intersects `D(M)`. Excluding every alternative solution therefore has the shape of a hitting-set problem over these distinguishing sets.

This perspective connects puzzle generation to:

- minimum or weighted hitting sets;
- MaxSAT;
- counterexample-guided refinement;
- minimal unsatisfiable subsets when clues are represented as assumptions;
- "unavoidable set" and "trade" terminology used in some established puzzle families.

This is not equivalent to saying clue selection ought to be implemented as a hitting-set solver. The value of the connection is that it exposes a well-developed family of algorithms and diagnostic concepts that may otherwise remain invisible.

## MUS, MCS, and clue sufficiency

Suppose puzzle rules plus all candidate clue assumptions determine target `T`, and an additional constraint requires the semantic solution to differ from `T`. The resulting formula is unsatisfiable.

Under that formulation:

- a **minimal unsatisfiable subset (MUS)** of clue assumptions can correspond to a subset-minimal sufficient clue set;
- an **optimal/smallest MUS** can correspond to a cheapest or smallest sufficient set under the chosen candidate language;
- **minimal correction sets (MCSes)** and hitting sets provide dual views of the same structure.

This connection is especially useful when clue costs encode something other than count, such as presentation complexity or a deliberately chosen aesthetic property.

## Mechanism diversity and parameter diversity

A generator can vary many parameters while retaining one generative ancestry. Another generator can produce a smaller literal output space through several qualitatively different construction mechanisms.

These are different notions of diversity. Related Quality-Diversity research sometimes uses heterogeneous search operators or "emitters," offering a useful analogy for generators whose construction processes themselves may need examination.

## Determinism does not remove distributional questions

A deterministic generator still induces a distribution or traversal over its reachable puzzle space through its inputs, seeds, enumeration order, tie-breaking, or external parameters. Repetition can arise from the mapping between those inputs and structural output, not only from pseudorandomness.

Consequently, deterministic generation can still exhibit concentration, blind spots, repeated motifs, and objective-induced mode collapse.

## Further reading and resources

- Barbara De Kegel and Mads Haahr, **Procedural Puzzle Generation: A Survey** (IEEE Transactions on Games, 2020). Broad survey of puzzle-generation methods and characteristics. https://doi.org/10.1109/TG.2019.2917792
- PySAT `Hitman`, a cardinality-/subset-minimal hitting-set enumerator. https://pysathq.github.io/docs/html/api/examples/hitman.html
- PySAT `OptUx`, an optimal MUS enumerator using implicit hitting-set machinery. https://pysathq.github.io/docs/html/api/examples/optux.html
- Jean-Baptiste Mouret and Jeff Clune, **Illuminating search spaces by mapping elites**. https://arxiv.org/abs/1504.04909
- Daniele Gravina et al., **Procedural Content Generation through Quality Diversity**. https://arxiv.org/abs/1907.04053
