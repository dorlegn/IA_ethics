# Part 1 · Unit 1 — From Correlation to Causation in Fairness  
*Conceptual Foundation and Relevance*

> **Why this matters:** Purely statistical (correlational) fairness checks can treat symptoms while leaving root causes of discrimination untouched. Causality gives us the language and tools to locate—and fix—the mechanisms that generate unfair outcomes.

---

## Guiding questions
1. **Why** do traditional statistical fairness metrics often miss genuine discrimination, and **how** does causality provide a stronger foundation?
2. **How** can causal reasoning separate legitimate predictive relationships from problematic pathways that perpetuate historical biases?

---

## Conceptual context
Correlation-based fairness (e.g., equalized odds, demographic parity) flags **associations** between protected attributes and outcomes. But equalizing associations can “break the thermometer”: it may hide the signal without curing the disease. A **causal** perspective asks *how* protected attributes influence outcomes—directly, via proxies, through historically shaped mediators, or due to selection effects—and then targets the **mechanisms** creating harm. As Pearl puts it, every serious attempt at fairness relies—implicitly or explicitly—on a **causal model**.

---

## Key concepts

### 1) Limits of correlation-based fairness
- Treats any association as suspect, without distinguishing:
  - **Legitimate** pathways (e.g., domain-relevant skill → outcome)
  - **Illegitimate** pathways (e.g., protected attr. → decision)
- Consequences:
  - Can **over-correct** (hurting utility) or **under-correct** (missing bias)
  - Cannot tell two worlds apart that look **statistically identical** but are **causally different**  
  *(e.g., same approval gaps; in A, gaps stem from access inequities; in B, from direct bias)*

**Why it matters:** Interventions should **remove unfair causes**, not merely flatten correlations.

---

### 2) Causal models of discrimination
Let **A** (protected attribute) → **Y** (decision/outcome), via:
- **Direct discrimination:** `A → Y`
- **Indirect discrimination:** `A → M → Y` where `M` (mediator) was shaped by historical inequity
- **Proxy discrimination:** Feature **X** is statistically tied to **A** (via hidden causes) and drives **Y**
- **Selection/measurement bias:** Data/labels skewed by past processes

**Implication:** Different structures → **different fixes** (feature surgery, constraint training, data repair, task reformulation).

---

### 3) Counterfactual reasoning for fairness
Ask the **what-if**: *“Would this person’s prediction be the same if we changed only their protected attribute, holding causally unrelated factors fixed?”*  
This yields **counterfactual fairness**: predictions should be **invariant** to protected-attribute flips along unfair paths.

**Use it to:**
- Diagnose individual-level unfairness
- Specify which causal paths are **allowed** vs **blocked**
- Evaluate if an intervention truly removes unfair influence

---

### 4) Choosing intervention points (causal view)
- **Pre-processing (data):** reweight/repair labels; debias proxies; correct selection bias  
- **In-processing (model):** fairness constraints; adversarial debiasing; path-specific regularization  
- **Post-processing (outputs):** group thresholds; calibration; reject option/recourse  
- **Task reformulation:** change what is predicted or how it’s operationalized, if the task embeds unfair pathways

**Principle:** **Target the mechanism** you’ve identified in the causal graph—not a generic metric.

---

### 5) Domain modeling perspective
| ML stage | Causal questions |
|---|---|
| Problem formulation | Does the task definition encode unfair paths? |
| Data collection | Any selection/collider biases? Missingness by group? |
| Feature engineering | Which features are legitimate vs proxy/tainted? |
| Model design | What constraints/architectures block unfair paths? |
| Evaluation | Do counterfactual and causal tests align with fairness goals? |

---

## Intersectionality lens
Causal analysis must allow **interactions** between protected attributes (e.g., gender×race). Model:
- **Path-specific effects** per intersectional subgroup  
- **Counterfactual tests** at intersections  
- **Interactions** in structural equations

**Why:** Single-attribute views can miss harms concentrated at **identity intersections**.

---

## Practical considerations

### A) Implementation framework
1. **Identify mechanisms**  
   Direct? Indirect via mediators? Proxies? Selection/measurement issues? Document evidence.
2. **Choose causal fairness criterion**  
   Group-level vs individual-level (counterfactual). Declare **fair vs unfair** paths.
3. **Sketch initial causal graph**  
   Protected attributes, mediators, outcomes, confounders. List assumptions & open questions.

### B) Common challenges (and moves)
- **Limited causal knowledge** → consider **multiple plausible graphs**, do **sensitivity analyses**, iterate, document assumptions.
- **Fairness–utility tension** → optimize to remove **unfair** paths while preserving **legitimate** ones; make trade-offs explicit.

### C) Evaluation
- **Validate assumptions:** check implied independencies; expert review; sensitivity analysis.  
- **Assess counterfactual fairness:** estimate flip-invariance; compare with statistical metrics; analyze by intersection.

---

## Case study — College admissions (CS program)
**Observed:** Higher recommendation rates for men vs women with similar observed records.  
**Causal inquiry revealed:**
- **Proxies:** heavy weight on activities with gendered access (e.g., competitive programming clubs)
- **Mediator effects:** stereotype-threat–affected test scores
- **Text bias:** recommendation letter language differences

**Interventions:**
- Reduce weight of gendered-proxy activities; adjust text features; re-focus on validated performance signals
- Counterfactual checks confirm **reduced unfair paths** while preserving valid predictors

**Outcome:** Maintained predictive utility, improved fairness, clearer stakeholder justification.

---

## FAQs

**Q1: Do I need perfect causal truth to act?**  
No. Use **plausible models + sensitivity**. If several plausible graphs point to the same fix, you have robust direction. Be transparent about assumptions.

**Q2: How does this change interventions vs. correlational methods?**  
You stop “equalizing the symptom” and **target the cause**: fix proxies, repair labels, or adapt the task—rather than bluntly forcing parity.

---

## Unit deliverable (for Part 1 · Unit 5 handoff)
Create a **Preliminary Causal Analysis Pack**:
1. **Mechanism ID questionnaire** (direct/indirect/proxy/selection)  
2. **Counterfactual question template** (what flips, what holds fixed, why)  
3. **Initial causal diagram** with annotated assumptions & candidate unfair paths

This feeds the formal modeling Units (2–4).

---

## Summary & next steps
- Correlation-based metrics alone can mislead; **causal models** distinguish **how** discrimination arises.  
- **Counterfactual fairness** operationalizes the ethical question at the individual level.  
- Interventions should be **path-targeted**—data, model, or output—guided by the causal graph.  
- Next: build formal causal graphs and structural equations, then estimate and test them.

---

## References
- Crenshaw, K. (1989). *Demarginalizing the intersection of race and sex*. Univ. of Chicago Legal Forum.  
- Hardt, M., Price, E., & Srebro, N. (2016). *Equality of opportunity in supervised learning*. NeurIPS.  
- Kilbertus, N., et al. (2017). *Avoiding discrimination through causal reasoning*. NeurIPS.  
- Kusner, M. J., Loftus, J., Russell, C., & Silva, R. (2017). *Counterfactual fairness*. NeurIPS.  
- Pearl, J. (2009). *Causality* (2nd ed.). Cambridge Univ. Press.  
- Pearl, J. (2019). *The seven tools of causal inference*. CACM.  
- Yang, K., Loftus, J. R., & Stoyanovich, J. (2020). *Causal intersectionality for fair ranking*. arXiv.  
- Zhang, J., & Bareinboim, E. (2018). *Fairness in decision-making – the causal explanation formula*. AAAI.

