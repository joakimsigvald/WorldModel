# Loop-Chemistry Model with Smooth Rates (Three Reversible Reactions)

This document defines a **crisp, self-contained loop-chemistry model** with three reversible reactions,
a smooth direction bias using **ln/exp**, and a **true lattice equilibrium** defined by *no net change*
in the amounts of 3-, 4-, and 5-loops (while conserving the total number of couples).

The model is written in terms of **probabilities / proportions** (p₃, p₄, p₅).  
For simulations with a finite population (e.g. 1000 couples), you convert between **counts** and **proportions** as specified below.

---

## 1) State Variables

We consider loop types by the number of couples in the loop:

- 3-loop, 4-loop, 5-loop

Let:

- n₃, n₄, n₅ = counts of 3-, 4-, 5-loops
- N = total number of loops:  
  **N = n₃ + n₄ + n₅**
- p₃, p₄, p₅ = proportions (probabilities) of each loop type:
  **pᵢ = nᵢ / N**, so **p₃ + p₄ + p₅ = 1**

### Couples are conserved

Let C be the total number of couples (constant):

**3 n₃ + 4 n₄ + 5 n₅ = C**

All reactions below conserve couples, so C remains constant.

> For a simulation: choose C (e.g. C = 1000), pick initial (n₃,n₄,n₅) satisfying the constraint,
> compute pᵢ = nᵢ / (n₃+n₄+n₅) whenever needed.

---

## 2) Reaction Set (Three Reversible Reactions)

We define three reversible reactions:

1. **R₁:**  [3,3,3]  ⇄  [4,5]
2. **R₂:**  [4,4]    ⇄  [3,5]
3. **R₃:**  [5,5]    ⇄  [3,3,4]

Each reaction is a *local repartitioning* of couples and conserves the total number of couples involved:
- R₁: 3+3+3 = 9 couples; 4+5 = 9
- R₂: 4+4 = 8; 3+5 = 8
- R₃: 5+5 = 10; 3+3+4 = 10

---

## 3) Encounter (Mixing) Factors Using Proportions

We define a **base encounter factor** B(R) for each reactant multiset R using proportions pᵢ.
This is a mean-field “mass-action” approximation.

- For a mixed pair [i,j] with i≠j:
  **B([i,j]) = 2 pᵢ pⱼ**
- For a same pair [i,i]:
  **B([i,i]) = pᵢ²**
- For a same triple [i,i,i]:
  **B([i,i,i]) = pᵢ³**
- For a multiset [3,3,4]:
  **B([3,3,4]) = 3 p₃² p₄**  
  (three permutations: 334, 343, 433)

Thus:

- B([3,3,3]) = p₃³
- B([4,5])   = 2 p₄ p₅
- B([4,4])   = p₄²
- B([3,5])   = 2 p₃ p₅
- B([5,5])   = p₅²
- B([3,3,4]) = 3 p₃² p₄

> In a simulation with counts: compute pᵢ from nᵢ, then compute B(·).

---

## 4) Local Cost of a Multiset (Sync + Redundancy)

We assign each multiset X a scalar cost E(X):

**E(X) = S_tot(X) + D(X)**

### 4.1 Redundancy term D(X)

For any multiset X:

**D(X) = |X| − (number of distinct loop types in X)**

Examples:
- D([3,3,3]) = 2
- D([4,5])   = 0
- D([4,4])   = 1
- D([3,5])   = 0
- D([5,5])   = 1
- D([3,3,4]) = 1

### 4.2 Sync/short-loop term S_tot(X)

Define per-loop sync/shortness score:

- S(3) = 1
- S(4) = 2
- S(5) = 4

(i.e. S(N) = 2^(N−3))

For any multiset X:

**S_tot(X) = Σ S(n) over n in X**

Examples:
- S_tot([3,3,3]) = 3
- S_tot([4,5])   = 6
- S_tot([4,4])   = 4
- S_tot([3,5])   = 5
- S_tot([5,5])   = 8
- S_tot([3,3,4]) = 4

### 4.3 Costs E(X) for the needed multisets

- E([3,3,3]) = 3 + 2 = 5
- E([4,5])   = 6 + 0 = 6
- E([4,4])   = 4 + 1 = 5
- E([3,5])   = 5 + 0 = 5
- E([5,5])   = 8 + 1 = 9
- E([3,3,4]) = 4 + 1 = 5

So the energy differences are:
- R₁: E([4,5]) − E([3,3,3]) = 1
- R₂: E([3,5]) − E([4,4])   = 0
- R₃: E([3,3,4]) − E([5,5]) = −4

---

## 5) Smooth Forward/Backward Rates (ln/exp form)

Introduce a single “softness/temperature” parameter:

- T > 0 (often start with T = 1)

For a reversible reaction R ⇄ P:

**k(R→P) = B(R) · exp( −(E(P) − E(R)) / (2T) )**  
**k(P→R) = B(P) · exp( −(E(R) − E(P)) / (2T) )**

This guarantees:
- both directions always have positive rate
- downhill moves are favored smoothly
- uphill moves remain possible (suppressed, not forbidden)

### 5.1 Explicit rates for the three reactions

Let ΔE₁ = E([4,5]) − E([3,3,3]) = 1  
Let ΔE₂ = E([3,5]) − E([4,4])   = 0  
Let ΔE₃ = E([3,3,4]) − E([5,5]) = −4

Then:

**R₁:** [3,3,3] ⇄ [4,5]
- k₁⁺ = k([3,3,3]→[4,5]) = p₃³ · exp( −ΔE₁/(2T) )
- k₁⁻ = k([4,5]→[3,3,3]) = 2p₄p₅ · exp( +ΔE₁/(2T) )

**R₂:** [4,4] ⇄ [3,5]
- k₂⁺ = k([4,4]→[3,5]) = p₄² · exp( −ΔE₂/(2T) ) = p₄²
- k₂⁻ = k([3,5]→[4,4]) = 2p₃p₅ · exp( +ΔE₂/(2T) ) = 2p₃p₅

**R₃:** [5,5] ⇄ [3,3,4]
- k₃⁺ = k([5,5]→[3,3,4]) = p₅² · exp( −ΔE₃/(2T) ) = p₅² · exp( +2/T )
- k₃⁻ = k([3,3,4]→[5,5]) = 3p₃²p₄ · exp( +ΔE₃/(2T) ) = 3p₃²p₄ · exp( −2/T )

---

## 6) Net Flux for Each Reaction

Define net flux (signed):

- J₁ = k₁⁺ − k₁⁻
- J₂ = k₂⁺ − k₂⁻
- J₃ = k₃⁺ − k₃⁻

Positive J means net flow in the “forward” direction as written.

---

## 7) True Lattice Equilibrium (Species Balance)

Let the loop counts evolve by stoichiometry:

- R₁ forward: [3,3,3]→[4,5] changes (n₃,n₄,n₅) by **(−3,+1,+1)**
- R₂ forward: [4,4]→[3,5]   changes (n₃,n₄,n₅) by **(+1,−2,+1)**
- R₃ forward: [5,5]→[3,3,4] changes (n₃,n₄,n₅) by **(+2,+1,−2)**

Therefore:

dn₃/dt = −3J₁ + 1J₂ + 2J₃  
dn₄/dt =  +J₁ − 2J₂ +  J₃  
dn₅/dt =  +J₁ +  J₂ − 2J₃

### Equilibrium definition

The **true lattice equilibrium** is:

dn₃/dt = dn₄/dt = dn₅/dt = 0

This is equivalent to the single condition:

**J₁ = J₂ = J₃**

(meaning the net fluxes match so that production/consumption cancels for each loop type.)

---

## 8) Solving for the Equilibrium Proportions (p₃,p₄,p₅)

At equilibrium:

1) J₁(p₃,p₄,p₅) = J₂(p₃,p₄,p₅)  
2) J₂(p₃,p₄,p₅) = J₃(p₃,p₄,p₅)  
3) p₃ + p₄ + p₅ = 1  
with constraints pᵢ ≥ 0

This yields (generally) a unique interior solution for a given T.

### Practical note: proportions vs counts

- The flux equations are written purely in terms of pᵢ, so they are **scale-free**.
- For a finite simulation with a fixed couple budget C, you evolve integer counts nᵢ,
  but compute pᵢ = nᵢ/(n₃+n₄+n₅) whenever you evaluate B(·), kᵢ, Jᵢ.

---

## 9) Signed Direction Score (Optional Diagnostic)

For each reversible pair R ⇄ P, define a signed direction score:

Δ(R⇄P) = ln( k(P→R) / k(R→P) )

Then:
- Δ > 0 means net bias toward P→R
- Δ < 0 means net bias toward R→P
- Δ = 0 means detailed balance for that reaction pair (not required for lattice equilibrium)

---

## 10) What You Need to Choose for Simulation

- Choose T (start with T = 1)
- Choose initial counts (n₃,n₄,n₅) satisfying 3n₃+4n₄+5n₅=C
- Iterate updates using the rates above (stochastic or deterministic)

This completes the model definition.
