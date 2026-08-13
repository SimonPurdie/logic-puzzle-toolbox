# Diversity and Evaluation

This reference concerns collections of generated puzzles rather than correctness of a single instance. Its central distinction is between **literal/combinatorial variety** and **structural or experiential variety**.

A generator may be capable of producing millions of distinct outputs while repeatedly instantiating a small number of recognizable puzzle recipes.

## Several spaces of similarity

"Are these puzzles different?" is incomplete until the comparison space is specified.

Possible views include:

- **surface diversity**: names, values, wording, presentation, clue ordering;
- **clue-vocabulary diversity**: which clue templates or relation families appear;
- **clue-role diversity**: whether clues serve different logical functions in the solve;
- **constraint-structure diversity**: topology of variable/clue incidence graphs or constraint hypergraphs;
- **solution-structure diversity**: whether completed solutions themselves occupy different structural families;
- **deductive diversity**: proof traces, deduction motifs, branching, convergence, refutation, bottlenecks, and reuse of intermediate facts;
- **difficulty-profile diversity**: where effort occurs and what kind of effort it is;
- **generative-mechanism diversity**: whether instances arise through different construction mechanisms or merely different parameters of one mechanism.

High diversity under one descriptor does not imply high diversity under another.

## Expressive range

Procedural-content-generation research uses **expressive range** to characterize where a generator's outputs actually fall under selected metrics.

This is useful for puzzle generators because a huge theoretical output space can still map densely into a small region of a meaningful behavioural space. It also exposes an important caveat: expressive-range conclusions depend on the chosen descriptors. A generator can appear diverse under clue count and clue-type frequency while remaining narrow under solve topology or structural motifs.

The descriptor itself is therefore part of the analysis.

## Behavioural descriptions

Novelty-search and Quality-Diversity work distinguish literal genotype/encoding differences from differences in a chosen behaviour description.

Puzzle-oriented behavioural descriptions might include:

- clue-type or clue-role histograms;
- motifs in the clue-variable incidence graph;
- canonicalized constraint skeletons;
- number, depth, and arity of deductions in an explanation trace;
- proportion of final assignments versus derived intermediate relations;
- distribution of clue usefulness over the solve;
- amount of parallel reasoning and later convergence;
- cleanup-tail length;
- branching or ambiguity profiles;
- refutation depth;
- properties of the completed solution;
- construction ancestry or generator pathway.

These are examples of lenses, not a proposed universal feature vector.

## Hidden sameness and canonicalization

A useful diagnostic thought experiment is to remove literal labels and canonicalize the remaining structure.

For a logic-grid puzzle this might mean a labelled constraint graph or hypergraph. For another puzzle family it might mean a normalized geometric pattern, a canonical solution graph, or a deduction trace with entity names erased.

If a corpus of thousands of nominally different puzzles collapses to a small number of canonical skeletons, that provides a concrete account of "sameyness" that clue counts alone would not show.

Graph isomorphism, graph kernels, motif counts, edit distances, trace distances, and learned embeddings are all possible technical families behind this idea. None is automatically the right similarity metric for a puzzle family.

## Objective-induced concentration

A generator can converge on a narrow stylistic basin because that basin satisfies its measurable objectives reliably.

This creates a distinction between:

- explicit style constraints, intentionally encoded; and
- **accidental style induced by the objective**, tie-breaking, pruning, representation, or construction process.

The latter is easy to miss because every individual generated puzzle may satisfy all specified requirements.

## Novelty search and Quality-Diversity as conceptual neighbours

**Novelty search** asks what changes when search is rewarded for behavioural difference rather than progress toward a single objective.

**Quality-Diversity (QD)** methods search for repertoires of high-performing solutions spread across a behaviour space rather than only one optimum. **MAP-Elites** is a prominent example: user-chosen behavioural dimensions define niches, with strong candidates retained across those niches.

These ideas matter even when a puzzle generator never uses an evolutionary algorithm. They introduce useful questions:

- what behaviour space describes meaningful difference for this puzzle family?
- is one high-performing structural niche crowding out others?
- do quality criteria and diversity criteria describe different properties?
- are several different generator mechanisms needed to reach different niches?

## Corpus evaluation can reveal what instance evaluation cannot

Single-puzzle checks answer questions such as uniqueness or a particular solve trace. Corpus-level analysis can reveal:

- concentration around a few structural templates;
- clue types that occur frequently but play nearly identical roles;
- rare regions of the generator's design space;
- deterministic parameters that map disproportionately to one structure;
- diversity that exists only at the level of names or presentation;
- difficulty bands dominated by one deduction pattern;
- a strong generator "signature" visible after surface labels are removed.

Comparing distributions between generator versions can therefore be more revealing than comparing a handful of selected examples.

## Diversity is not automatically quality

A maximally diverse corpus can contain many poor puzzles. Conversely, a deliberately coherent puzzle series may value a recognizable style.

The useful separation is between:

- **quality of an individual puzzle**;
- **coverage or diversity of a corpus**;
- **controllability**, meaning whether desired regions can be reached intentionally.

Treating these as separate properties reduces the temptation to make one scalar score stand in for all of them.

## Further reading and resources

- Oliver Withington and Laurissa Tokarchuk, **The Right Variety: Improving Expressive Range Analysis with Metric Selection Methods**. Highlights that expressive-range conclusions depend strongly on metric choice. https://arxiv.org/abs/2304.02366
- Jean-Baptiste Mouret and Jeff Clune, **Illuminating search spaces by mapping elites**. Introduces MAP-Elites and behaviour-dimension repertoires. https://arxiv.org/abs/1504.04909
- Daniele Gravina et al., **Procedural Content Generation through Quality Diversity**. Survey and framing of QD for PCG. https://arxiv.org/abs/1907.04053
- Joel Lehman and Kenneth O. Stanley, **Abandoning objectives: Evolution through the search for novelty alone**. Behavioural novelty as an alternative search signal. https://doi.org/10.1162/EVCO_a_00025
- Fiona Shyne, Kaylah Facey, and Seth Cooper, **Procedurally Puzzling: On Algorithmic Difficulty and Player Experience in QD-Generated Logic Grid Puzzles**. A direct logic-grid example using constrained MAP-Elites. https://doi.org/10.1609/aiide.v20i1.31873
