<!-- solve-problem:6920190e-ec80-46bc-829c-958b77e0ee21 -->
# The 4/3 subtour-LP integrality-gap conjecture

A [Tangle Solve problem](https://solve.tangle.tools/problems/6920190e-ec80-46bc-829c-958b77e0ee21).

## What is the problem?

The (symmetric, metric) traveling salesman problem: given a complete graph on \(n\) vertices with edge costs \(c_{ij}\) satisfying the triangle inequality, find a minimum-cost Hamiltonian tour. The subtour-elimination LP (also called the Held–Karp or Held–Karp–Subtour relaxation) is:

\[
\min \sum_e c_e x_e \quad \text{s.t.} \quad x(\delta(v)) = 2 \;\forall v,\quad x(\delta(S)) \ge 2 \;\forall \emptyset \neq S \neq V,\quad x_e \ge 0.
\]

The integrality gap is \(\sup_{\text{instances } I} \frac{\mathrm{OPT}(I)}{\mathrm{LP}(I)}\), where OPT is the optimal tour cost and LP the optimal fractional value. The conjecture: **the integrality gap of this LP is exactly \(4/3\)**. The lower bound \(4/3\) is witnessed by classic examples (e.g., two cliques of size \(n/2\) joined by two edges, or the "bad" instances of Held–Karp and later constructions), so the open part is proving the upper bound: every metric instance admits a tour of cost at most \((4/3)\cdot \mathrm{LP}\).

Ambiguities to note: "metric" here means costs are symmetric and satisfy the triangle inequality (asymmetric TSP is a different, separate gap problem); whether "tour" may revisit vertices is immaterial under the triangle inequality.

## Why does it matter?

This LP is the central relaxation for the TSP and its variants (survivable network design, prize-collecting, path versions); resolving the gap would settle the exact approximability strength of the most-studied relaxation in combinatorial optimization. The famous 1.5-approximation of Wolsey (via Christofides' algorithm, analyzed against the LP) is conjectured improvable to 4/3, which would be the best possible matching the known lower bound. Progress on this problem has repeatedly generated tools (LP rounding, thin-tree methods, matroid techniques) that transferred to broader network design.

## What's already known?

- The gap is at least 4/3 (classical examples; see Benoit & Boyd, and "Subtour LP gaps" literature).
- Christofides/Wolsey gives an upper bound of 1.5 (i.e., 3/2) for all metric instances — unchanged for decades as the best general metric guarantee.
- Best gap bounds are known for special graph classes: graphic TSP (approx. 7/5, Momke–Annamdury/Sebő–Vygen line of work), graphical metric and bounded-degree cases, and for LP solutions with special structure.
- A structural line of attack analyzes the gap as a function of the support of the optimal LP solution: the gap is 4/3 for low-support solutions. Early work handled solutions whose support is "narrow"; Villa, Vercesi, Barta, and Mastrolilli (2026) extends this to LP optima with at most \(n+8\) nonzero components (verify exact statement/constant). This suggests inducting on components of the support, but the general case requires components of unbounded complexity.
- Rounding-based attacks (thin trees, maximum-entropy sampling à la Asadpour et al. for the asymmetric case) have not closed the symmetric 4/3 gap; the thin-tree conjecture itself was shown insufficient as stated (verify).

## What would count as solving it?

- **Primary goal:** a proof that for every metric instance, \(\mathrm{OPT} \le \frac{4}{3}\mathrm{LP}\) — equivalently a polynomial-time 4/3-approximation matching the LP bound. A referee would accept either an explicit rounding/analysis of a tour construction or a direct argument bounding OPT/LP.
- **Partial results that count:** (a) extending the 4/3 bound to LP solutions with \(n+k\) nonzero components for growing \(k\) or all \(k\); (b) improving the general upper bound below 3/2 by any \(\epsilon > 0\); (c) resolving structured subclasses (graphic TSP at 4/3, bounded-degree, etc.). Note (b) alone — beating 3/2 for general metrics — would be a landmark independent of the exact 4/3 constant.

## How to start

1. Read Williamson–Shmoys, *The Design of Approximation Algorithms*, Chapter 2 (TSP, subtour LP, Christofides/Wolsey analysis) to internalize the standard framework.
2. Study the structural-support line: understand why the gap is 4/3 when the support has few components, and what breaks as the number of components grows. The Villa et al. (2026) paper is the frontier; work backward through its references (e.g., prior "n+O(1) components" or narrow-support results — verify citations).
3. Second angle: the "best-of-many" Christofides framework — decompose the LP into a convex combination of spanning trees, round the best one; identify which structural property of trees would suffice.
4. Main obstacle: no general technique controls the cost of the matching augmentation relative to the LP simultaneously for all instances; known bad instances show slack must be extracted globally, not edge-locally.

## Key references

- D. P. Williamson and D. B. Shmoys, *The Design of Approximation Algorithms*, Cambridge University Press, 2011. Chapter 2 contains the subtour LP, Wolsey's Christofides-vs-LP analysis, and the standard 4/3 examples. https://www.designofapproxalgs.com/
- M. Held and R. M. Karp, "The traveling-salesman problem and minimum spanning trees," *Operations Research* 18 (1970), 1138–1162 (and Part II, *Mathematical Programming* 1 (1971), 6–25). Introduces the Held–Karp relaxation and its Lagrangian/1-tree view, the foundation of the LP under study.
- Villa, Vercesi, Barta, and Mastrolilli, *The Integrality Gap of the Subtour LP Is 4/3 if the LP Solution Has at Most n+8 Non-Zero Components*, 2026. Proves the conjecture for instances whose optimal LP solution has support of at most \(n+8\) edges, extending the structural-support approach. (No stable link recorded — verify.)
- A. Benoit and S. Boyd, "Finding the exact integrality gap for small traveling salesman problems," *Mathematics of Operations Research* 33 (2008), 921–931. Empirically/analytically establishes the gap on small and structured instances, certifying 4/3 in those cases. (verify)

## Warnings

- Verify the Villa et al. (2026) result independently; it is the only recent citation in the record and its exact hypotheses matter (what "non-zero components" means — edges? connected components of support?).
- Don't conflate the symmetric metric gap with the asymmetric TSP gap (Asadpour et al. \(O(\log n/\log\log n)\)) or with the graph-TSP approximability literature, which is closely related but not identical to the LP-gap question.
- The 4/3 lower bound is folklore-solid, but tight-gap claims on small instances use exhaustive computation and don't constitute proof.
- Common dead end: trying to fix Christofides by local edge-exchange arguments; known instances defeat all such fixes since parity correction is not where the 1/6 slack lives.
- Ambiguity: the original statement doesn't specify symmetric vs. asymmetric; the standard reading (Held–Karp, degree-2 constraints) is symmetric metric, adopted above.

---
*`ALGO-000236` · unverified*

## Acceptance guidance

- **Primary goal:** a proof that for every metric instance, \(\mathrm{OPT} \le \frac{4}{3}\mathrm{LP}\) — equivalently a polynomial-time 4/3-approximation matching the LP bound. A referee would accept either an explicit rounding/analysis of a tour construction or a direct argument bounding OPT/LP.
- **Partial results that count:** (a) extending the 4/3 bound to LP solutions with \(n+k\) nonzero components for growing \(k\) or all \(k\); (b) improving the general upper bound below 3/2 by any \(\epsilon > 0\); (c) resolving structured subclasses (graphic TSP at 4/3, bounded-degree, etc.). Note (b) alone — beating 3/2 for general metrics — would be a landmark independent of the exact 4/3 constant.

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/6920190e-ec80-46bc-829c-958b77e0ee21?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000236.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000236)
