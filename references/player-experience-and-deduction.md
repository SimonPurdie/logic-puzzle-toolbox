# Player Experience and Deduction

This reference concerns what solving a puzzle asks a person to do. It is deliberately more opinionated than the technical references: logical validity, uniqueness, and computational difficulty do not by themselves make a satisfying puzzle.

A useful broad preference is for **discovery over administration**. Interesting puzzle states often contain newly derived relationships that can be remembered, combined, or reinterpreted later. Tedious states often contain mostly a growing ledger of individual assignments and exclusions.

This is a tendency rather than a rule. Direct clues, routine propagation, repetition, and cleanup can all contribute pacing, accessibility, reinforcement, or relief.

## Five-question clue-set heuristic

These questions are intended as a compact diagnostic rather than a scoring rubric.

### 1. Where does the player's effort come from?

The same amount of time can be spent on very different cognitive work. Some puzzles require combining facts or finding consequences that are not locally obvious; others require scanning many possibilities, maintaining a large state table, or repeatedly propagating elementary exclusions.

A useful distinction is therefore **inferential effort versus bookkeeping effort**, rather than simply easy versus hard.

### 2. Do clues need each other?

Could most clues be processed one at a time, converted into an assignment or exclusion, and then mentally discarded? Or do partially useful clues and derived facts remain relevant because they later combine with information from elsewhere?

A clue set can be highly interconnected in the formal constraint graph while still behaving like serial data entry for the player. Convergence of independent reasoning threads, multi-premise deductions, and facts that acquire significance later all belong to the broader idea of interaction.

### 3. Does solving create useful intermediate knowledge?

Progress need not consist only of final assignments such as `Alice = baker` or `Tuesday != blue`.

Potential intermediate discoveries include restricted sets, pairings, equivalence classes, ordering relations, conditional facts, grouped possibilities, structural invariants, or other small "lemmas." Their value is especially visible when they become premises for later deductions.

A long solve that only produces assignments can be shallower than a shorter solve that creates and reuses intermediate structure.

### 4. Does the reasoning develop and pay off?

A solve can repeat the same operation from beginning to end, or it can change character as earlier information is recontextualized.

Possible forms of development include separate threads converging, an earlier observation becoming newly useful, a bottleneck deduction unlocking dormant clues, a derived relationship receiving a later payoff, or a difficult inference being followed by a deliberate release into simpler cleanup.

The presence of a long dependency chain alone does not imply this kind of development; `A -> B -> C -> D -> E` can still be mechanically shallow.

### 5. What remains when surface details are stripped away?

Names, themes, wording, numbers, and clue templates can make two instances appear different while leaving the same logical skeleton underneath.

A useful mental experiment replaces surface content with abstract symbols and asks what the player is still discovering. This can reveal repeated anchor-chain-disambiguator patterns, identical clue roles, or near-identical deduction structures hidden by presentation variety.

## Reveal progression is not logical progression

Progressive disclosure can create pacing without creating deduction. A reveal system may be monotonic, deterministic, path-independent, and free of unreachable clues while still behaving as:

```text
fact -> enter fact -> unlock next fact -> enter fact -> unlock next fact
```

Those are meaningful properties of the reveal mechanism, but they do not describe **why** the next player action is inferable. A newly revealed clue can function mainly as answer delivery even when the condition that revealed it is elaborate.

Similarly, requiring several forced actions before the next reveal measures spacing, not necessarily deductive richness. Several routine propagations can still amount to clerical work.

## Answer-bearing clues and constraint-bearing clues

One useful qualitative distinction concerns whether a clue mostly exposes a final relationship or leaves a partially resolved constraint that can interact with other information.

This is not a distinction between simple and sophisticated clue syntax. Equality, inequality, counts, comparisons, adjacency, spatial relations, and compound statements can all be either cognitively direct or richly interactive depending on their role in the surrounding puzzle.

Generating a clue from a known hidden solution is not itself a source of triviality. Many successful generation methods begin from a completed solution. The relevant question is what inferential work remains for the player after the clue is presented.

## Fact transmission versus derived structure

Consider a conventional logic-grid domain with people, jobs, and drinks.

A clue fragment dominated by fact transmission might behave like:

```text
Alice is the baker.
The baker drinks tea.
Carol is the doctor.
The doctor drinks coffee.
Bob does not drink tea.
```

Much of the useful state is a collection of assignments reached by following one clue at a time:

```text
Alice -> baker -> tea
Carol -> doctor -> coffee
Bob != tea
```

Contrast that with an equally ordinary clue vocabulary whose consequences produce partial relationships before final answers. For example, knowing that the baker drinks tea and the doctor drinks coffee, together with a person's exclusions from both drinks, can establish that the person's job lies in the remaining pair of jobs. If another thread independently restricts a second person to an overlapping pair, all-different structure can turn those partial results into a stronger group-level fact. A later clue can then resolve that fact.

The qualitative distinction is not "direct clues versus relational clues." It is whether the solve mostly **transmits stated information** or **creates new reasoning material that later participates in further inference**.

## Interaction does not require exotic clue types

Simple equality, inequality, cardinality, and all-different constraints can support rich deductions when their consequences overlap. Conversely, a linguistically elaborate or mathematically strong clue can be cognitively trivial if it independently settles a large part of the grid.

This separates at least three properties that are easy to conflate:

- **clue complexity**: how complicated an individual statement is;
- **information strength**: how many possible solutions the statement excludes;
- **deductive character**: what reasoning becomes possible through the statement's interaction with the rest of the puzzle.

A clue can score high on one and low on another.

## Deduction topology

A human-oriented explanation or proof trace gives another view of puzzle character.

Some recurring shapes include:

```text
Broad independent propagation

      start
   / / | | \ \
  A B  C D  E F
```

```text
Long shallow chain

start -> A -> B -> C -> D -> E
```

```text
Convergence

A -> C --\
         +-> F
B -> D --/
```

```text
Separated threads with later payoff

A -> B -> C ----\
                +-> G -> H
D -> E -> F ----/
```

No topology is intrinsically superior. The point is that clue count and solver runtime do not describe these shapes well, while players can experience them very differently.

## Recontextualization and logical payoff

A particularly useful qualitative phenomenon occurs when a fact learned earlier becomes important for a reason that was not yet available when it was derived.

This can create the feeling that earlier work mattered and that the puzzle is developing rather than merely shrinking domains. It is related to, but not identical with, dependency depth: an old fact can be reused after a long interval or combined with a newly discovered structure.

## Refutation and counterfactual reasoning

Some puzzles permit progress of the form:

```text
if X were true
    -> consequences
    -> contradiction
therefore not X
```

Refutation depth, assumption-based reasoning, and the amount of simple reasoning needed to expose a contradiction provide another lens on human-facing difficulty. Their presence is not a requirement for quality; they simply describe a kind of deductive work that ordinary propagation metrics can miss.

## Difficulty is not one quantity

Several notions of difficulty can coexist:

- machine solver runtime, conflicts, branches, or propagation rounds;
- number or cost of human-style inference steps;
- depth and dependency structure of an explanation;
- refutation depth;
- information-theoretic reduction;
- bookkeeping or memory burden;
- visual search burden;
- empirical human completion time, error rate, or subjective rating.

These can correlate without being interchangeable. An objective that makes a solver work harder may increase human difficulty, human tedium, both, or neither depending on the representation and puzzle family.

## Further reading and resources

- Bart Bogaerts, Emilio Gamba, and Tias Guns, **A framework for step-wise explaining how to solve constraint satisfaction problems**. Logic-grid puzzles are used as a case study; explanations can involve combinations of constraints. https://arxiv.org/abs/2006.06343
- Emilio Gamba, Bart Bogaerts, and Tias Guns, **Efficiently Explaining CSPs with Unsatisfiable Subset Optimization**. Connects human-oriented explanation steps with optimal unsatisfiable subsets and hitting sets. https://arxiv.org/abs/2105.11763
- Radek Pelánek, **Difficulty Rating of Sudoku Puzzles by a Computational Model** (FLAIRS 2011). A useful example of separating individual solving techniques from dependency/availability structure in human-oriented difficulty modelling. https://ocs.aaai.org/ocs/index.php/FLAIRS/FLAIRS11/paper/view/2517
- Fiona Shyne, Kaylah Facey, and Seth Cooper, **Procedurally Puzzling: On Algorithmic Difficulty and Player Experience in QD-Generated Logic Grid Puzzles** (AIIDE 2024). Directly examines generated logic-grid puzzles and the relationship between an algorithmic difficulty proxy and player experience. https://doi.org/10.1609/aiide.v20i1.31873
