# Literature Review: Quantum Sudoku

## Quantum Computing Approaches and Quantum Game Variants

### Overview

This literature review examines existing efforts to apply quantum computing to Sudoku puzzles, encompassing both (1) algorithmic approaches for solving standard Sudoku using quantum computers, and (2) genuine quantum variants of the game with modified rules that incorporate quantum mechanical principles. The research reveals a diverse landscape ranging from practical quantum computing applications to purely theoretical quantum game constructions.

---

## Part I: Solving Standard Sudoku with Quantum Computers

### 1. Grover's Algorithm Approaches

#### 1.1 Hybrid Classical-Quantum Algorithms

Multiple research groups have developed hybrid approaches combining classical preprocessing with quantum search algorithms, particularly Grover's algorithm, which provides O(√N) speedup for unstructured search problems.

**Pal et al. (2018) - Hybrid Algorithm with Helper Qubits**

Pal et al. created a combination algorithm where classical computing identifies clues and flags helper qubits that act as control qubits in the quantum circuit, with every square having n + 2 qubits where n is the minimum number to represent possible numbers and two extra are helper qubits.

**Behera et al. (2019) - Duality Computing Approach**

Behera and Panigrahi proposed an algorithm for 4×4 Sudoku puzzles using concepts of duality quantum computing, achieving logarithmic complexity O(log n) and providing exponential speedup compared to classical linear complexity O(n).

#### 1.2 Implementation Challenges and Limitations

**Qubit Requirements**

A significant practical limitation is that qubit requirements grow rapidly: 2×2 grids require 12 qubits, 4×4 grids require 64 qubits, and 9×9 grids would theoretically require 486 qubits. Implementations on 2×2 puzzles have shown inconsistent accuracy, occasionally producing zeros in every blank square.

**Success Rates and Practical Performance**

Researchers have focused on simplified 4×4 Sudoku (Shi Doku) as a starting point, with the goal of eventually designing algorithms capable of solving NxN Sudoku deterministically.

### 2. Quantum Annealing Approaches

#### 2.1 D-Wave Quantum Annealer Applications

**QUBO Formulation**

Sudoku constraints can be reformulated as Quadratic Unconstrained Binary Optimization (QUBO) problems using penalty terms that penalize wrong behavior, with squared distance functions ensuring each number appears exactly once per row and column.

**Empirical Performance Studies**

**Radcliffe (2020) - D-Wave 2000Q Experiments**

Radcliffe tested the D-Wave 2000Q quantum annealer on 50 Sudoku puzzles with 30 clues each, successfully solving 48 out of 50 attempts with average execution time of 0.2 seconds per problem on the device. However, when testing medium difficulty puzzles with 27 clues, success rates declined.

**Hatzky (2025) - Performance Comparison**

Recent work comparing quantum annealing with simulated annealing on 4×4 Sudoku showed quantum annealers need roughly constant time (20µs per sampling) while classical algorithm times vary, though the quantum annealer achieved only ~1% success probability compared to nearly 100% for simulated annealing.

### 3. Quantum Backtracking Approaches

#### 3.1 Qrisp Framework Implementation

The Qrisp quantum programming framework implements quantum backtracking for Sudoku, offering an alternative to Grover's algorithm that better exploits problem structure. This approach addresses the limitation that Grover's algorithm provides only quadratic speedup which barely mitigates the exponential growth of the state space.

**Accept and Reject Functions**

Quantum backtracking uses predicate functions (accept and reject) that must return QuantumBool values, not change tree state, delete all temporary QuantumVariables, and never simultaneously return True on the same node.

### 4. Comparative Analysis: Quantum vs Classical

#### 4.1 Complexity Analysis

**Theoretical Speedup**

While classical brute force Sudoku solving has O(9^n) complexity where n is empty cells and quantum computing can theoretically reduce this to O(√N), the practical reality shows classical algorithms with constraint propagation remain superior for standard 9×9 Sudoku.

**Why Classical Often Wins**

Sudoku has inherent structure that classical algorithms exploit through constraint propagation and backtracking, whereas quantum search algorithms like Grover's treat the problem as unstructured, negating their theoretical advantages.

---

## Part II: Quantum Variants of Sudoku with Modified Rules

### 5. SudoQ: The Mathematical Quantum Sudoku Variant

#### 5.1 Nechita and Pillet (2020) - Foundational Work

**Definition and Concept**

Nechita and Pillet introduced SudoQ as a quantum version where entries are (non-commutative) projections instead of integers, meaning entries are unit column vectors from a Hilbert space with the constraint that vectors in each row and column must form an orthonormal basis.

**Mathematical Framework**

A SudoQ square of size n² is an n²×n² matrix of vectors in C^(n²) where the n² vectors in each row, column, or n×n sub-square form an orthonormal basis of C^(n²).

#### 5.2 Extended Analysis - Cardinality Studies

**Genuinely Quantum Solutions**

Follow-up work expanded SudoQ by introducing the notion of cardinality equal to the number of distinct vectors appearing in the pattern, focusing on genuinely quantum solutions that have cardinality greater than N² and cannot be reduced to classical counterparts by unitary transformation.

**4×4 SudoQ Parametrization**

Complete parametrization of genuinely quantum solutions for 4×4 SudoQ established that admissible cardinalities are 4, 6, 8, and 16, with a solution achieving maximal cardinality of 16 being presented.

#### 5.3 Theoretical Connections

**Relation to Quantum Latin Squares**

SudoQ is closely related to quantum Latin squares and the mathematical framework of mutually unbiased bases, connecting the game to fundamental quantum information theory.

**Magic Unitaries and Quantum Permutation Groups**

The mathematical formulation involves magic unitaries (matrices where row and column sums equal identity) which appear in the representation theory of the quantum permutation group S+.

### 6. Playable Quantum Game Variants

#### 6.1 Conceptual Quantum Sudoku Games

**Human Memory and Superposition**

Some researchers have proposed using quantum Sudoku to model how superposition might be used by human memory while solving puzzles manually, bridging cognitive science with quantum mechanics.

#### 6.2 "Quantum Sudoku" Mobile Application

A mobile application called "Quantum Sudoku" offers a solving method based on finding "Entangled Pairs" - two empty cells with mutually exclusive properties, where players identify cells with exactly two possible hiding places for a number within a block. Note: Despite the name, this appears to be a classical solving technique inspired by quantum terminology rather than a genuine quantum mechanical implementation.

### 7. Related Quantum Game Research

#### 7.1 Quantum Games Ecosystem

Researchers developing quantum games have created quantum versions of various classical games including Tic-Tac-Toe, Bingo, and Go, where players have options for classical moves (causing measurement and collapse) and quantum moves (creating entanglement between game positions).

**Quantum Tic-Tac-Toe**

In quantum Tic-Tac-Toe, classical moves measure boxes resulting in collapse while quantum moves entangle two separate boxes, favoring the player if the control box collapses in their favor.

---

## Part III: Applications and Connections

### 8. Quantum Error Correction

#### 8.1 Sudoku Codes

Sudoku codes are non-linear error correcting codes used mainly for erasure channels, with Sinkhorn-like algorithms related to Bayesian belief propagation being applicable to quantum erasure channel decoding.

### 9. Constraint Satisfaction Problem Framework

#### 9.1 Graph Coloring Equivalence

Sudoku puzzles can be formulated as graph coloring problems with 81 nodes and 810 edges for a 9×9 grid, allowing quantum annealing approaches designed for graph coloring to be applied.

The graph coloring formulation is common in quantum computing education, with tutorials in both Qiskit and Q# using graph coloring examples before applying techniques to Sudoku.

---

## Part IV: Critical Assessment and Future Directions

### 10. Current State of Practical Quantum Sudoku Solving

#### 10.1 Hardware Limitations

**Qubit Requirements vs. Availability**

Current quantum computers provide ~100-1000 qubits with significant noise, while 9×9 Sudoku would require 486 qubits according to some implementations. This creates a substantial gap between theoretical algorithms and practical deployment.

**Success Probability Challenges**

Even for simplified 4×4 Sudoku, quantum annealers show only 1% success probability requiring multiple sampling runs, though constant-time execution makes this feasible if 1000 runs take only seconds.

#### 10.2 When Quantum Approaches Excel

The literature reveals that quantum advantages appear primarily in:

1. **Unstructured search spaces** where classical heuristics don't apply
2. **Verification rather than solving** - quantum approaches for checking validity may outperform solving
3. **Theoretical frameworks** demonstrating quantum computing principles

### 11. Pedagogical Value

#### 11.1 Educational Applications

Sudoku serves as an effective pedagogical example for teaching quantum computing principles, with 2×2 Sudoku being particularly suitable for introducing Grover's algorithm, oracle construction, and quantum gates to students.

Multiple educational implementations note that while it may be difficult to find a solution to a 9×9 Sudoku, given one it is easy to verify validity, making Sudoku well-suited for teaching quantum verification concepts.

### 12. Open Problems and Future Research

#### 12.1 Algorithmic Development

Researchers acknowledge they are "yet to design an algorithm which can solve NxN Sudoku deterministically" using quantum computing, indicating substantial open questions remain.

#### 12.2 Hybrid Approaches

The most promising direction appears to be hybrid classical-quantum algorithms that:
- Use classical preprocessing for constraint propagation
- Apply quantum search for remaining ambiguous cells
- Employ classical verification for final solutions

#### 12.3 Theoretical SudoQ Development

Open conjectures remain regarding the relationship between quantum and classical solutions of SudoQ puzzles, with only 4×4 grids fully characterized.

---

## Conclusions

### Key Findings

1. **Algorithmic Approaches**: Multiple quantum algorithms (Grover's search, quantum annealing, quantum backtracking) have been applied to Sudoku with varying success, though practical implementations remain limited to small grids (2×2, 4×4).

2. **Quantum Variants**: SudoQ represents a genuine quantum generalization using non-commutative projections and orthonormal bases, creating puzzles with solution spaces fundamentally different from classical Sudoku.

3. **Practical Reality**: For standard 9×9 Sudoku, classical algorithms with constraint propagation remain superior to current quantum approaches due to:
   - Limited qubit availability
   - Structure exploitation by classical methods
   - Quantum overhead and error rates

4. **Educational Value**: Both solving standard Sudoku quantumly and exploring quantum variants serve valuable pedagogical purposes for teaching quantum computing concepts.

5. **Future Potential**: As quantum hardware improves (more qubits, lower error rates), quantum approaches may become competitive, particularly for larger or more complex constraint satisfaction problems.

### Research Gaps

- **Deterministic quantum Sudoku solvers** for full 9×9 grids
- **Complete characterization** of SudoQ solutions beyond 4×4
- **Experimental validation** of theoretical quantum advantages
- **Playable quantum Sudoku games** implementing genuine quantum mechanical rules (beyond mathematical constructions)
- **Practical hybrid algorithms** optimally balancing classical and quantum components

### Significance

The quantum Sudoku literature demonstrates both the promise and limitations of quantum computing for constraint satisfaction problems, serving as a microcosm for understanding where quantum advantages emerge and where classical approaches remain supreme.

---

## References

### Quantum Algorithmic Approaches

1. Pal, A., et al. (2018). "Solving Sudoku Game Using Quantum Computation."

2. Behera, B. K., & Panigrahi, P. K. (2019). "Solving Sudoku game using a hybrid classical-quantum algorithm." EPL (Europhysics Letters), 128(3).

3. Forsythe, E. (2021). "Quantum Sudoku Solver." MIT 6.S089 — Intro to Quantum Computing.

4. Radcliffe, D. (2020). "Solving Sudoku puzzles on a quantum computer." LinkedIn article.

5. Hatzky, J. (2025). "Solving Sudoku with a Quantum Power-Up." Towards Data Science.

### Quantum Backtracking

6. Qrisp Documentation. "Solving Sudoku using Quantum Backtracking." https://qrisp.eu/

### Quantum Game Variants (SudoQ)

7. Nechita, I., & Pillet, J. (2020). "SudoQ — a quantum variant of the popular game." Quantum Information & Computation, 21(9-10), 781-799.

8. Rajchel-Mieldzioc, G., et al. (2021). "Genuinely quantum solutions of the game Sudoku and their cardinality." Physical Review A, 104(4), 042423.

### Educational and Tutorial Works

9. Theodo Blog (2022). "Quantum sudoku." https://blog.theodo.com/2022/10/quantum-sudoku/

10. Various authors. "Sudoku Solving Using Quantum Computer." International Journal of Scientific Research in Computer Science.

---

## Attribution Note

This literature review synthesizes research from multiple sources including academic papers, technical blog posts, educational materials, and software documentation. All specific claims are properly cited using the citation format. The review aims to provide an honest assessment of both achievements and limitations in quantum Sudoku research.

**Methodology**: Web search conducted January 2025 covering academic databases, preprint servers, technical blogs, and quantum computing educational resources.

**Scope**: Limited to English-language sources accessible through web search. May not capture all work in quantum Latin squares and related mathematical frameworks published in specialized journals.
