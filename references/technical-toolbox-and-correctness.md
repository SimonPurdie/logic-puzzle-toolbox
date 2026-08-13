# Technical Toolbox and Correctness

This reference intentionally does not explain standard backtracking, CSP modelling, MRV, SAT, SMT, or ordinary unit testing. A capable coding agent can usually reconstruct those techniques.

The emphasis is on concepts, solver facilities, and resources that are easier to overlook and that connect directly to puzzle generation or validation.

## Semantic solutions versus solver models

Solver encodings often contain variables that are not part of the puzzle answer:

- Tseitin or reification variables;
- channeling variables;
- reachability or flow variables;
- symmetry-breaking auxiliaries;
- bookkeeping variables introduced by an encoding.

Two complete solver models can disagree on these variables while representing the same human-visible solution.

This creates a distinction between **model uniqueness** and **projected/semantic uniqueness**. A second-solution constraint usually concerns the variables that define the displayed puzzle solution rather than every internal solver variable.

The same distinction matters for model enumeration and model counting.

## Equivalence and symmetry

Some puzzle domains contain interchangeable labels, rotations, reflections, colours, groups, or other automorphisms.

Three ideas can easily be conflated:

- **solver symmetry**, which may be broken to reduce search;
- **puzzle equivalence**, under which two outputs may intentionally count as the same solution or same generated puzzle;
- **aesthetic symmetry**, a visual or stylistic property of the clues.

A uniqueness test that silently inherits solver symmetry-breaking constraints may answer a different question from the intended player-facing notion of uniqueness.

## Uniqueness as a second-solution or UNSAT question

Given a known semantic target `T`, uniqueness can be represented by asking whether the rules and clues admit any semantic solution different from `T`:

```text
base rules
AND selected clues
AND semantic_solution != T
```

Unsatisfiability establishes uniqueness relative to that semantic projection.

This formulation is useful because it connects uniqueness checking to incremental solving, assumptions, unsatisfiable cores, MUS extraction, and clue-selection formulations.

## Assumption literals and incremental solving

SAT and SMT solvers commonly support temporary assumptions over a persistent base problem. Candidate clues can be represented by assumption literals, allowing many related puzzle variants to be checked without rebuilding the whole solver state.

Assumption-based APIs can also expose unsatisfiable cores: subsets of assumptions sufficient for contradiction. Those cores are not automatically minimal, but they connect naturally to clue sufficiency and explanation problems.

## MUS, MCS, hitting sets, and MaxSAT

Several related concepts are worth recognizing:

- **MUS** — minimal unsatisfiable subset;
- **SMUS / optimal MUS** — smallest or minimum-cost MUS under a chosen cost model;
- **MCS** — minimal correction subset whose removal restores satisfiability;
- **hitting set** — a set intersecting every member of a family of sets;
- **MaxSAT** — optimization over satisfied/violated soft clauses under hard constraints.

MUS/MCS and hitting-set dualities appear in clue minimization, counterexample exclusion, human-readable explanation generation, and weighted clue selection. PySAT exposes unusually convenient implementations of several of these algorithms.

## Global constraints as an idea catalogue

Constraint-programming systems contain named high-level constraints for structures that puzzle implementations often encode manually.

Examples include:

- `all_different` and cardinality constraints;
- `table` / extensional constraints;
- `regular` / automaton constraints;
- circuits and paths;
- connectivity;
- flows;
- spanning trees;
- value precedence and sequencing relations.

Even when the implementation ultimately uses SAT, SMT, ILP, or bespoke search, global-constraint catalogues can serve as dictionaries of known modelling structures and propagation ideas.

Redundant implied constraints can also be useful computationally when they strengthen propagation. Logical redundancy and implementation uselessness are not equivalent.

## Alternative formalisms can expose different structure

Puzzle encodings may fit several paradigms:

- finite-domain constraint programming;
- SAT / MaxSAT;
- SMT;
- Answer Set Programming;
- ILP/MIP;
- exact cover;
- graph algorithms;
- automata;
- bespoke propagators and search.

The main value of recognizing alternatives is not that one formalism is generally superior, but that each can expose different primitives, optimization machinery, symmetry handling, counting, or explanation facilities.

## Independent verification and dual encodings

A generator and its verifier can share the same modelling bug if they reuse the same encoding and assumptions.

Stronger forms of validation can include:

- an independently implemented verifier;
- a second solver paradigm or alternative encoding;
- differential testing between implementations;
- exhaustive enumeration on reduced instances;
- property-based or metamorphic tests;
- regression corpora containing known edge cases;
- explicit checks that generated clues are true of the claimed solution and that no inequivalent semantic solution survives.

Generated audit text can need checking too. Statements such as "this clue entails X" or a walkthrough of a reveal plan can disagree with the encoded instance, so diagnostic claims can be checked against the same formal semantics used for validation.

For deterministic generators, reproducibility is itself testable: identical inputs should map to identical outputs, while corpus tests can separately examine whether that deterministic mapping has undesirable concentration.

## Useful resources

- **MiniZinc global constraint library** — a broad catalogue of modelling structures, useful even as an idea dictionary outside MiniZinc. https://docs.minizinc.dev/en/stable/lib-globals.html
- **Global Constraint Catalog** — extensive catalogue of named global constraints and structural patterns. https://sofdem.github.io/gccat/
- **PySAT** — Python SAT toolkit with assumptions plus examples for `Hitman`, `MUSX`, `OptUx`, `RC2`, MCS enumeration, and model enumeration. https://pysathq.github.io/docs/html/
- **PySAT Hitman** — minimum/minimal hitting-set enumeration. https://pysathq.github.io/docs/html/api/examples/hitman.html
- **PySAT OptUx** — optimal MUS enumeration via implicit hitting sets. https://pysathq.github.io/docs/html/api/examples/optux.html
- **Z3 Guide** — SMT solver documentation including assumptions, cores, models, and optimization facilities. https://microsoft.github.io/z3guide/
- **Conjure** — high-level constraint modelling and automated refinement, useful as a source of alternative representations. https://conjure.readthedocs.io/
- **XCSP3** — constraint-programming format, benchmarks, and model ecosystem. https://xcsp.org/
- Bart Bogaerts, Emilio Gamba, and Tias Guns, **A framework for step-wise explaining how to solve constraint satisfaction problems**. https://arxiv.org/abs/2006.06343
