## **2.8. Loop Chemistry**

The qualitative tendencies described above can be captured in a deliberately simplified **loop-chemistry model**. The aim of this model is not to describe the full microscopic dynamics of loops, but to test whether a small set of natural assumptions is sufficient to produce a stable equilibrium among a few loop types.

The model treats loops as a population of interacting species that locally **repartition existing structure** through reversible reactions, biased only by structural strain. No external targets or ideal values are imposed.

---

### **2.8.1. Loop species and conservation**

We consider only three loop species:

- **3-loops** (three couples),
- **4-loops** (four couples),
- **5-loops** (five couples).

Loops larger than five couples are assumed to be structurally fragile and to fragment rapidly into smaller loops. They therefore do not appear as long-lived species in the model.

All reactions conserve the total number of couples. Loop chemistry is a **repackaging of existing structure**, not the creation or destruction of constituents.

Let:
- \( n_3, n_4, n_5 \) be the counts of 3-, 4-, and 5-loops,
- \( N = n_3 + n_4 + n_5 \) be the total number of loops,
- \( p_i = n_i / N \) be the corresponding proportions.

The conserved quantity is:
\[
3n_3 + 4n_4 + 5n_5 = C
\]
where \( C \) is the total number of couples.

---

### **2.8.2. Allowed reversible reactions**

We allow three reversible local reactions, chosen as the smallest non-trivial repartitionings that conserve couples:

\[
[3,3,3] \;\leftrightarrow\; [4,5]
\]

\[
[4,4] \;\leftrightarrow\; [3,5]
\]

\[
[5,5] \;\leftrightarrow\; [3,3,4]
\]

Each reaction rearranges a small neighborhood of loops while preserving the total number of couples involved. Five-loops appear only as intermediates and are never produced as a stable isolated phase.

---

### **2.8.3. Encounter factors**

As a mean-field approximation, the availability of a given multiset of loops is assumed to scale with the product of their proportions:

- \([i,i]\) occurs with weight \( p_i^2 \),
- \([i,j]\) with weight \( 2p_ip_j \) for \( i \neq j \),
- \([i,i,i]\) with weight \( p_i^3 \),
- \([3,3,4]\) with weight \( 3p_3^2p_4 \).

These **encounter factors** encode only combinatorics and mixing, not preference.

---

### **2.8.4. Structural cost (strain)**

Each multiset of loops is assigned a scalar **cost** representing combined phase strain and redundancy. The cost is defined as:
\[
E(X) = S_{\text{tot}}(X) + D(X)
\]

where:

- the redundancy term is
\[
D(X) = |X| - (\text{number of distinct loop types in } X),
\]

- the synchronization term is
\[
S_{\text{tot}}(X) = \sum_{n \in X} S(n),
\]
with per-loop values
\[
S(3)=1,\quad S(4)=2,\quad S(5)=4.
\]

This assigns increasing strain to longer loops, reflecting their greater synchronization burden.

For the multisets appearing in the reactions, the resulting costs are:

| Multiset | Cost |
|--------|------|
| [3,3,3] | 5 |
| [4,5] | 6 |
| [4,4] | 5 |
| [3,5] | 5 |
| [5,5] | 9 |
| [3,3,4] | 5 |

---

### **2.8.5. Reaction rates**

Reactions are biased smoothly toward lower total cost but remain fully reversible. For a reaction
\[
R \;\leftrightarrow\; P
\]
the forward and backward rates are defined as:
\[
k(R \rightarrow P) = B(R)\,\exp\!\left(-\frac{E(P)-E(R)}{2}\right)
\]
\[
k(P \rightarrow R) = B(P)\,\exp\!\left(-\frac{E(R)-E(P)}{2}\right)
\]
where \( B(\cdot) \) is the encounter factor.

This form ensures that:
- lower-strain configurations are favored,
- higher-strain transitions remain possible,
- directionality emerges from relative strain rather than hard rules.

---

### **2.8.6. Equilibrium condition**

For each reaction, define the net flux
\[
J = k_{\text{forward}} - k_{\text{backward}}.
\]

The loop counts evolve according to reaction stoichiometry. Equilibrium is defined as the absence of net production or consumption of any loop type:
\[
\frac{dn_3}{dt} = \frac{dn_4}{dt} = \frac{dn_5}{dt} = 0.
\]

In this model, that condition is equivalent to:
\[
J_1 = J_2 = J_3.
\]

Together with \( p_3 + p_4 + p_5 = 1 \), this system has a unique interior solution.

---

### **2.8.7. Numerical equilibrium and connector count**

Solving the equilibrium equations yields approximately:
\[
p_3 \approx 0.57,\quad
p_4 \approx 0.34,\quad
p_5 \approx 0.09.
\]

Interpreting loop sizes as exposing:
- 6 connectors for 3-loops,
- 8 connectors for 4-loops,
- 10 connectors for 5-loops,

the resulting average connector count is:
\[
\langle c \rangle = 6p_3 + 8p_4 + 10p_5 \approx 7.04.
\]

This value is not imposed by construction. It emerges solely from the reaction set, conservation of couples, and smooth bias toward reduced strain. Given the simplicity of the model, the number should be regarded as approximate rather than exact.
