### Theory

A context-free grammar (CFG) specifies how strings in a language are generated from a start symbol using production rules.

#### Notation
- G = (V, Σ, P, S)
  - V: nonterminals (variables), e.g., S, A, B
  - Σ: terminals (alphabet), e.g., a, b, 0, 1
  - P: productions A → α where A ∈ V and α ∈ (V ∪ Σ)*
  - S: start symbol
- ⇒ one-step derivation, ⇒* zero-or-more steps

#### Why normal forms?
- They make algorithms (parsing, proofs, equivalence checks) simpler and systematic.
- Most common: Chomsky Normal Form (CNF) and Greibach Normal Form (GNF).


#### Simplifying CFGs (remove redundancy)

Before converting, simplify the grammar while preserving its language L(G). Two CFGs are equivalent if they generate the same language.

Redundancies to remove
- Useless symbols (non-generating or unreachable)
- ε-productions (null productions: A → ε)
- Unit productions (A → B)

Safe cleanup pipeline
1) Remove ε-productions (except possibly for the start symbol; use a fresh S0 if ε ∈ L(G)).
2) Remove unit productions.
3) Remove useless symbols (first non-generating, then unreachable).
4) Optionally repeat step 3 after transformations to catch any newly useless symbols.

##### 1) Useless productions
Two kinds of useless symbols:
- Non-generating: a nonterminal that cannot derive a terminal-only string (no w ∈ Σ* with A ⇒* w).
- Unreachable: a symbol never appearing in any sentential form derived from S.

Algorithm (two passes)
- Generating pass: mark terminals as generating; repeatedly mark A generating if A → α and every symbol in α is a terminal or already generating. Delete rules that reference non-generating nonterminals.
- Reachability pass: from S, mark all symbols reachable via productions. Delete rules whose LHS is unreachable; remove occurrences of unreachable symbols on RHS.

##### 2) ε-productions (null productions)
Goal: eliminate A → ε (except possibly for the start symbol, if ε ∈ L(G)).

Procedure
- Compute nullable nonterminals: A is nullable if A ⇒* ε.
- For each production X → α, add variants where any nonempty subset of nullable symbols in α is deleted (avoid duplicates).
- Remove all explicit ε-productions.
- If ε must remain in the language, introduce a fresh start symbol S0 not on any RHS and add S0 → S | ε; use S0 as the new start. Do not introduce ε on the RHS of non-start symbols.

##### 3) Unit productions
Unit productions have the form A → B with A, B ∈ V.

Removal via unit-closure
- For each A, compute U(A) = { B | A ⇒* B using only unit productions }.
- For each B ∈ U(A), copy all non-unit rules of B to A.
- Delete all unit productions.


#### Chomsky Normal Form (CNF)

##### Definition
A CFG is in CNF if every production is one of:
- A → BC where A, B, C ∈ V
- A → a where a ∈ Σ
- Optionally S0 → ε if ε ∈ L(G), where S0 is a fresh start symbol that does not appear on any RHS

##### Conversion to CNF
1) Simplify: remove ε-productions, unit productions, then useless symbols (repeat useless removal if needed).
2) Replace terminals inside long RHS: if a terminal appears together with other symbols, introduce a proxy nonterminal (e.g., A_a → a) and substitute the terminal with its proxy.
3) Binarize long RHS: factor any rule with length ≥ 3 into binary rules, e.g.,
   - A → B C D  ⇒  introduce X → C D, then A → B X; repeat until all RHS lengths ≤ 2.

##### Notes
- Using a fresh start symbol S0 avoids conflicts when ε is in the language and prevents the start symbol from appearing on RHS.


#### Greibach Normal Form (GNF)

##### Definition
A CFG is in GNF if every production is:
- A → a α where a ∈ Σ and α ∈ V* (α may be ε, so A → a is allowed)
- Optionally S0 → ε if ε ∈ L(G), with S0 a fresh start symbol not on any RHS

##### High-level conversion to GNF
- Preprocess: eliminate ε-productions (except possibly S0 → ε), unit productions, and useless symbols.
- Remove left recursion:
  - Order nonterminals A1, A2, …, An.
  - For i = 1..n:
    - For each rule Ai → Aj γ with j < i, expand Aj by its alternatives so Ai-rules no longer start with earlier nonterminals.
    - Eliminate immediate left recursion on Ai. If Ai → Ai α1 | … | Ai αm | β1 | … | βk (β’s do not start with Ai), then:
      - Ai → β1 R | … | βk R
      - R  → α1 R | … | αm R | ε
- After these steps, ensure each rule begins with a terminal; iterate substitutions if necessary.

##### Remarks
- Converting to CNF first isn’t required for GNF, but full simplification and left‑recursion removal are essential.
- GNF ensures each derivation step consumes exactly one input symbol, aiding top‑down parsing.


#### Common pitfalls (and how the converter handles them)
- Start symbol and ε: If ε ∈ L(G), introduce S0 with S0 → S | ε and keep S0 off all RHS.
- “Useless” means both non-generating and unreachable; handle both with the two-pass method and repeat after other eliminations if needed.
- Don’t leave unit chains; compute unit-closure and copy only non-unit rules.
- CNF prohibits terminals mixed with nonterminals on RHS; use terminal proxies.
- Remove left recursion before enforcing GNF’s “terminal-first” requirement.

