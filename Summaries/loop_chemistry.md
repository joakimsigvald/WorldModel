## Loop Chemistry Postulates

We model the underlying medium not as a perfectly frozen crystal of 3- and 4-loops, but as a **dynamic loop soup**: loops continuously form, dissolve, and repack into new loops through local bond reconfiguration. Loops are not independent “particles,” but higher-level compounds built from the same underlying couples (pairs). All reactions therefore correspond to local repartitionings of already-existing structure.

The allowed reactions are constrained by locality, conservation of constituents, and by the structural pressures that govern stability in the mixed loop lattice.

### Postulate 1 — Local couple-conserving repackaging

Most reactions are local **repartitionings** of a small neighborhood of couples into new loops, approximately conserving the total number of couples involved. Examples:

* `[3,3,3] ↔ [4,5]` conserves 9 couples  
* `[3,5] ↔ [4,4]` conserves 8 couples  

This is the smallest class of reactions compatible with strict locality: the medium reshuffles what is already present rather than creating or destroying structure non-locally.

### Postulate 2 — Large loops fracture

Loops longer than five are structurally fragile. As loop size increases, the number of vertical bonds and synchronization constraints grows, creating more potential failure points. Consequently, any loop with more than five couples rapidly fractures into two smaller loops:

```
[n] → [floor(n/2), ceil(n/2)]   for n > 5
```

This rule closes the chemistry on the set {3,4,5}, which therefore contains the only long-lived loop species.

### Postulate 3 — The two reversible core reactions

Within {3,4,5}, the minimal non-trivial couple-conserving repartitions are:

```
[3,3,3] ↔ [4,5]
[3,5]   ↔ [4,4]
```

These reactions are special because they are the smallest transformations that simultaneously:

1. create or eliminate a 5-loop (which acts as a mediator species), and  
2. allow the soup to move between rigid (3-rich) and flexible (4-rich) regimes  
   without introducing loops of length ≥ 6.

All other reactions in the loop soup can be understood as compositions or cascades of these two transformations together with the fracture rule for long loops.

### Postulate 4 — 5-loops cannot form a stable phase

A region that becomes too rich in 5-loops is unstable and tends to collapse back into the stable basis set {3,4}. The simplest couple-conserving “anti-trap” channel is:

```
[5,5] → [3,3,4]
```

This prevents a pathological dead-corner state consisting entirely of 5-loops and reflects the role of 5-loops as intermediate structures rather than a stable lattice phase.

## What drives these reactions

### Driver A — Strain minimization

Energy in the model is stored as **phase strain** and **connector strain**. Local updates tend to dissolve redundant bonds and reorganize structures to reduce this strain. This explains both the fracture of long loops and the dominant direction of many reactions: configurations with fewer synchronization constraints and better connector balance are preferred.

### Driver B — Escape from uniform phases (variance preference)

The mixed 3/4 medium has a natural stability near a balanced connector regime. Regions that become too uniform are dynamically poor:

* 3-rich regions are overly rigid and restrict reconfiguration.  
* 4-rich regions are overly flexible and tend toward connector surplus and instability.

To escape such traps, the loop soup admits rare **variance-injecting reactions**. The key example is:

```
[3,3,3] → [4,5]
```

This reaction cannot be justified by a preference for shorter loops alone. Its role is to break overly rigid local phases by introducing flexibility (a 4-loop) and a mediator (a 5-loop), enabling further reconfiguration.

## Correlation note — beyond mean-field behavior

Because the loop soup locally prefers **diversity of loop identity**, neighboring loops are not distributed independently. Similar loops are under-represented as neighbors, while dissimilar loops are over-represented.

As a result, reaction rates should not be assumed to scale purely as products of global frequencies (for example p(3)^3 or p(3)p(5)), but require **correlation or activity coefficients** that account for adjacency bias.

This deviation from mean-field behavior is a natural consequence of the same variance-seeking tendency that prevents the formation of rigid or overly flexible phases.
