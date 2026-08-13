# Player Experience and Deduction

This reference concerns what solving asks a person to do. Its broad preference is for **discovery over administration**: satisfying progress often creates relationships that can be combined or reinterpreted later, while tedious progress often grows a ledger of assignments and exclusions.

Direct clues, routine propagation, repetition, and cleanup are not inherently poor design; they can provide setup, pacing, reinforcement, accessibility, or release.

## Five-question clue-set heuristic

These are diagnostic questions, not a scoring rubric.

### 1. Where does the player's effort come from?

Is effort coming from combining information and finding non-local consequences, or mainly from scanning, remembering state, and propagating elementary exclusions? More work does not necessarily mean more reasoning.

### 2. Do clues need each other?

Could most clues be converted into an assignment or exclusion and then mentally discarded? Clues and derived facts that remain partially useful and later combine with information from elsewhere create a different solving experience from serial data entry.

### 3. Does solving create reusable intermediate knowledge?

Beyond final assignments, does the solve produce restricted sets, pairings, equivalences, orderings, conditionals, grouped possibilities, or other small "lemmas" that become premises later? A long chain of assignments can be shallower than a shorter solve that creates and reuses structure.

### 4. Does the reasoning develop and pay off?

Do separate threads converge, old information acquire new significance, or a bottleneck deduction unlock previously dormant information? A dependency chain such as `A -> B -> C -> D -> E` can still be mechanically repetitive.

### 5. What remains when surface details are removed?

If names, theme, wording, and literal values are replaced by abstract symbols, is there still a distinctive logical shape? This can expose recurring recipes hidden by presentation variety.

## Reveal progression is not logical progression

Progressive disclosure can create pacing without creating deduction. A reveal system may be deterministic, path-independent, and free of unreachable clues while the solve still behaves like:

```text
fact -> enter fact -> unlock next fact -> enter fact -> unlock next fact
```

Reveal conditions describe when information appears; they do not describe why the next player action is inferable. Requiring several forced actions between reveals measures spacing, not necessarily deductive richness.

## Clue syntax, information strength, and deductive role

Three properties are easy to conflate:

- **clue complexity**: how complicated the statement is;
- **information strength**: how much of the solution space it removes;
- **deductive role**: what reasoning it enables in combination with the rest of the puzzle.

They can vary independently. A count, comparison, adjacency, or compound clue can still function mainly as answer delivery; a simple equality or exclusion can be useful setup for a later synthesis. Generating clues from a known hidden solution is therefore not itself a source of triviality.

A useful distinction is whether a clue mostly exposes a final relationship or leaves a partially resolved constraint that can interact with other information. The latter can create intermediate reasoning material instead of only transmitting stated facts.

## Solve shape and logical payoff

Human-oriented explanation traces can have very different shapes: broad independent propagation, long shallow chains, converging threads, bottlenecks, or facts that are reused after a delay. Clue count and solver runtime describe these poorly.

**Recontextualization** is one useful pattern: something established earlier becomes important for a reason that was unavailable when it was first derived. This creates logical payoff without requiring exotic clue types or a particularly long solve.

## Refutation and counterfactual reasoning

Some puzzles support deductions of the form "if X, then these consequences lead to contradiction, therefore not X." Refutation depth and the amount of reasoning needed to expose a contradiction provide another lens on human difficulty that ordinary propagation counts can miss. Their presence is not a requirement for quality.

## Difficulty is not one quantity

Useful but non-equivalent views include:

- machine effort such as runtime, conflicts, branches, or propagation rounds;
- human-style inference cost and explanation structure;
- bookkeeping, memory, or visual-search burden;
- empirical player completion time, error rate, or subjective rating.

A change that makes a solver work harder can increase human difficulty, human tedium, both, or neither.

## Further reading and resources

- Bart Bogaerts, Emilio Gamba, and Tias Guns, **A framework for step-wise explaining how to solve constraint satisfaction problems**. Logic-grid puzzles are used as a case study; explanations can involve combinations of constraints. https://arxiv.org/abs/2006.06343
- Radek Pelánek, **Difficulty Rating of Sudoku Puzzles by a Computational Model**. Separates solving-technique difficulty from dependency and availability structure. https://ocs.aaai.org/ocs/index.php/FLAIRS/FLAIRS11/paper/view/2517
- Fiona Shyne, Kaylah Facey, and Seth Cooper, **Procedurally Puzzling: On Algorithmic Difficulty and Player Experience in QD-Generated Logic Grid Puzzles**. Examines the relationship between an algorithmic difficulty proxy and player experience. https://doi.org/10.1609/aiide.v20i1.31873
