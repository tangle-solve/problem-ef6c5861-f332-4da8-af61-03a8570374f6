<!-- solve-problem:ef6c5861-f332-4da8-af61-03a8570374f6 -->
# Derive 3SUM hardness from SETH

A [Tangle Solve problem](https://solve.tangle.tools/problems/ef6c5861-f332-4da8-af61-03a8570374f6).

## What is the problem?

**3SUM**: given a set of n integers, decide whether some triple sums to zero. Gajentaan–Övermars popularized it as a hardness anchor: many geometric problems (polygon containment, collinearity detection, etc.) are 3SUM-hard, so a truly subquadratic (o(n²)) 3SUM algorithm would yield subquadratic algorithms for all of them. The best known algorithms are slightly subquadratic — n²·(log log n / log n)^{O(1)} via additive-combinatorics methods (Baran–Demaine–Pătraşcu; Chan; later improvements) — so the "3SUM conjecture" states that no n^{2−ε} algorithm exists for any ε > 0.

**SETH**: the Strong Exponential Time Hypothesis states that for every ε > 0 there is a k such that k-SAT on n variables requires 2^{(1−ε)n} time.

**The problem**: either (a) construct a fine-grained reduction proving that a truly subquadratic 3SUM algorithm refutes SETH — i.e., show 3SUM ∈ n^{2−ε} time ⇒ k-SAT solvable in 2^{(1−ε′)n} time for all k — or (b) prove a formal barrier showing a natural, precisely defined class of reduction techniques cannot establish this. A fine-grained reduction here means a mapping running in time O(n^{2−ε}) with appropriate parameter blowup (per the standard framework of Vassilevska Williams–Williams).

## Why does it matter?

Fine-grained complexity currently rests on several conjectures (3SUM, APSP, SETH, OV) whose mutual relationships are only partially mapped: SETH is known to imply hardness for OV and many other problems, and 3SUM is known incomparable to APSP under certain reductions (the "three conjectures" separation program). Deriving 3SUM hardness from SETH would collapse two independent assumptions, upgrading dozens of geometry lower bounds from "conditional on 3SUM" to "conditional on SETH" — a strictly better-evidenced assumption. Conversely, a barrier result would show the conjectures are genuinely independent for a large class of techniques, sharpening the landscape.

## What's already known?

- **Nondeterministic barrier (Carmosino, Gao, Imperogliou, Paturi, SGM/"CGIPS" — Carmosino et al. 2016 on nondeterministic complexity)**: They show 3SUM has efficient nondeterministic and co-nondeterministic algorithms (certificates for yes/no instances of near-linear, or at least subquadratic, verification size), whereas SETH-hard problems like SAT/OV do not have comparable co-nondeterministic speedups under standard counting intuitions. This rules out reductions that preserve nondeterministic complexity — informally, "black-box" reductions of certain forms cannot derive 3SUM hardness from SETH. Crucially, this does **not** rule out reductions that, say, use randomness, preprocessing, or non-uniformity in ways that evade the nondeterministic argument.
- **Known unconditional non-reducibility**: Carmosino–Imperogliou–Kane–Williams (2016? verify) proved 3SUM and APSP are mutually non-reducible in a precise formal sense, showing such barrier proofs are feasible in principle — but no analogous SETH↔3SUM non-reducibility is known at the same level of generality.
- **Slightly subquadratic 3SUM algorithms** exist (Baran–Demaine–Pătraşcu 2005; Chan–Lewenstein 2015; Chan 2018), so any reduction must tolerate these barriers — a subtlety for formalizing what "barrier" means.
- **Direction of evidence**: 3SUM currently appears *harder to derive from* SETH than OV, because 3SUM's structure (one arithmetic constraint) differs fundamentally from CNF-SAT's clause structure; known SETH reductions produce problems with "many local constraints," not a single algebraic equation.

The census record is vague on which Carmosino et al. (2016) is meant; most likely the nondeterministic-complexity paper introducing NSETH (nondeterministic SETH), which is the standard reference for the barrier direction.

## What would count as solving it?

Either of two outcomes:

1. **Positive result**: A fine-grained reduction (in the Vassilevska Williams–Williams framework, or any reasonable formalization) such that an O(n^{2−ε}) 3SUM algorithm yields a 2^{(1−δ)n} algorithm for k-SAT for all k, with ε, δ > 0 explicitly related. This refutes the "independence" picture and is widely considered unlikely — treat with skepticism but check correctness carefully if claimed.

2. **Barrier result (more plausible target)**: A theorem of the form: "Under NSETH (nondeterministic SETH, Carmosino et al.), no [class C] of reductions can reduce k-SAT to 3SUM with the required parameters," where C is as large as possible — ideally all deterministic reductions, ideally extending to randomized/co-nondeterministic settings. The existing result constrains only particular strategies; broadening C is the concrete open task.

A referee would accept: explicit theorem statement, precise reduction-class definition, and a proof that any reduction in that class would collapse two complexity measures known (or conjectured) to differ.

## How to start

1. **Read Carmosino, Gao, Imperogliou, Paturi (2016) on NSETH** — understand exactly why 3SUM-in-coNP-subquadratic blocks certain SETH→3SUM reductions. Identify precisely which reduction features (nondeterminism-preserving vs. not) their argument requires.
2. **Read Vassilevska Williams (2018) survey** for the fine-grained reduction framework and the map of known reductions (which conjectures imply which hardness).
3. **Study the 3SUM/APSP non-reducibility paper (Carmosino et al., STOC 2016) (verify exact venue)** as a template: it shows how to prove unconditional non-reducibility between two conjectures using the nondeterministic-separation technique plus a diagonalization/counting argument.
4. **Identify the gap**: ask what a SETH→3SUM reduction *would* have to do that no current technique does — e.g., it must "spread" SAT's 2^n configurations into a single sum constraint on n²-sized sets. Try to formalize why this is hard via a circuit/communication-complexity argument, which is the natural tool for barrier proofs.

## Key references

- **Carmosino, M., Gao, X., Imperogliou, M., Paturi, R., Schneider, S.** — on NSETH and nondeterministic barriers. Introduces NSETH and uses nondeterministic complexity separations to show certain reductions (including SETH→3SUM under one formalization) cannot exist. Exact citation uncertain — verify; likely the NSETH paper is Carmosino–Gao–Imperogliou–Paturi–Schneider, "Nondeterministic extensions of the Strong Exponential Time Hypothesis" (verify).
- **Vassilevska Williams, V. (2018).** "On Some Fine-Grained Questions in Algorithms and Complexity." ICM proceedings survey. Defines the fine-grained reduction framework and surveys known connections among SETH, 3SUM, APSP, OV conjectures. https://people.csail.mit.edu/virgi/eigthensurvey.pdf (verify)
- **Carmosino, M., Imperogliou, M., Kane, D., Williams, R. (2016).** Non-reducibility between 3SUM and APSP — proves the first unconditional non-reducibility results between major fine-grained conjectures. (verify exact author list/venue)
- **Gajentaan, A., Övermars, M. (1995).** "On a class of O(n²) problems in computational geometry." Defines 3SUM-hardness for geometric problems.
- **Chan, T. (2018).** Slightly subquadratic 3SUM algorithms — relevant for knowing how close to n² the barrier must be placed.

## Warnings

- The census record is vague about *which* Carmosino et al. (2016) is cited; verify whether it means the NSETH paper or the 3SUM/APSP non-reducibility paper before relying on it.
- The nondeterministic barrier is conditional (on NSETH) and applies only to a formalized reduction class — it is **not** a proof that no SETH→3SUM reduction exists. Don't overstate it, and don't re-derive it.
- Slightly subquadratic 3SUM algorithms exist; "truly subquadratic" must mean n^{2−ε} for constant ε, and any barrier theorem must be robust to the log-factor savings.
- A positive reduction (SETH ⇒ 3SUM hardness) would be shocking to most experts; if you find one, first check whether it accidentally reduces to a problem with a known slightly-subquadratic algorithm, which would refute SETH and almost certainly indicate a bug.
- Ambiguity in the problem statement: "3SUM" could mean integer 3SUM or the 3XOR/3SUM-on-Z_p variants used in Pătraşcu's reductions; these have different known upper bounds and barrier profiles. Specify your variant.

---
*`ALGO-000082` · unverified*

## Acceptance guidance

Either of two outcomes:

1. **Positive result**: A fine-grained reduction (in the Vassilevska Williams–Williams framework, or any reasonable formalization) such that an O(n^{2−ε}) 3SUM algorithm yields a 2^{(1−δ)n} algorithm for k-SAT for all k, with ε, δ > 0 explicitly related. This refutes the "independence" picture and is widely considered unlikely — treat with skepticism but check correctness carefully if claimed.

2. **Barrier result (more plausible target)**: A theorem of the form: "Under NSETH (nondeterministic SETH, Carmosino et al.), no [class C] of reductions can reduce k-SAT to 3SUM with the required parameters," where C is as large as possible — ideally all deterministic reductions, ideally extending to randomized/co-nondeterministic settings. The existing result constrains only particular strategies; broadening C is the concrete open task.

A referee would accept: explicit theorem statement, precise reduction-class definition, and a proof that any reduction in that class would collapse two complexity measures known (or conjectured) to differ.

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/ef6c5861-f332-4da8-af61-03a8570374f6?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000082.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000082)
