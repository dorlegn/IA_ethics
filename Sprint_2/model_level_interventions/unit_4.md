# Unit 4: Multi-Objective Optimization  

---

## 1. Conceptual Foundation and Relevance  

### Guiding Questions  
- **Q1.** How can we systematically navigate the inherent tensions between fairness criteria and traditional performance metrics in ML?  
- **Q2.** What methodologies enable principled trade-off decisions rather than ad hoc compromises when multiple, potentially conflicting objectives must be balanced?  

### Conceptual Context  
Fairness objectives often conflict with performance metrics (accuracy, AUC, recall) and with each other.  

- **Constraints (Unit 1)**: treat fairness as hard requirements.  
- **Regularization (Unit 3)**: treats fairness as soft penalties.  
- **Multi-objective optimization**: explicitly models fairness and performance as competing objectives.  

This approach allows exploration of the **Pareto frontier** of solutions → balanced trade-offs, principled decision-making, stakeholder alignment.  

**Agarwal et al. (2019):** trade-offs in fair ML reflect **societal values**, not just technical artifacts.  

---

## 2. Key Concepts  

### The Fairness–Performance Trade-off  
- Fairness constraints restrict predictive capacity.  
- **Corbett-Davies et al. (2017):** enforcing demographic parity or equal opportunity reduces accuracy when base rates differ.  
- Example: loan approval → ignoring predictive income features (correlated with race) may reduce default prediction accuracy.  

---

### Pareto Optimality in Fairness  
- **Pareto optimal** = no objective can improve without worsening another.  
- **Pareto frontier** = set of optimal trade-offs.  
- **Martinez et al. (2020):** fairness definitions produce distinct frontiers.  
- Example: credit scoring → points along frontier:  
  - max accuracy, low fairness  
  - high fairness, low accuracy  
  - compromises in between  

---

### Scalarization Methods  
- **Linear scalarization**:  
  \[
  L = (1 - \lambda) \cdot L_\text{performance} + \lambda \cdot L_\text{fairness}
  \]  

- **ε-constraint method**: optimize one objective, bound others.  

- **Zafar et al. (2019):** varying λ explores the frontier.  
- Relation to Unit 3: regularization = scalarization with fixed λ.  

---

### Preference Articulation and Solution Selection  
- **A priori** → set preferences before optimization.  
- **A posteriori** → generate solutions, then stakeholders select.  
- **Interactive** → iterative refinement with stakeholder feedback.  

**Kleinberg et al. (2018):** choices reflect value judgments, not just technical trade-offs.  

---

### Domain Modeling Perspective  
Multi-objective fairness links to ML pipeline:  
- **Objective formulation** → performance + fairness objectives.  
- **Solution space exploration** → Pareto frontier generation.  
- **Visualization** → 2D plots, radar charts, parallel coordinates.  
- **Preference modeling** → stakeholder priorities.  
- **Operating point selection** → explicit value-based choices.  

---

### Intersectionality Consideration  
- Single-attribute fairness may miss subgroup harms.  
- **Buolamwini & Gebru (2018):** Gender Shades → disparities at intersections.  
- **Foulds et al. (2020):** intersectional fairness objectives across subgroups.  

Implementation:  
- Add objectives for subgroup disparities.  
- Use visualization tools for higher-dimensional trade-offs.  
- Efficient optimization needed for scalability (e.g., NSGA-III).  

---

## 3. Practical Considerations  

### Implementation Framework  
1. **Define objectives**: accuracy, demographic parity, equal opportunity, etc.  
2. **Pareto exploration**:  
   - Weighted-sum scalarization (vary λ).  
   - ε-constraint method.  
   - Verify Pareto optimality.  
3. **Evaluate & visualize**:  
   - 2D or 3D plots of fairness–performance trade-offs.  
   - Annotate thresholds (regulatory, business).  
4. **Preference articulation**:  
   - A priori, a posteriori, or interactive.  
   - Document rationales for accountability.  

---

### Implementation Challenges  
- **Computational cost**: many models needed → use warm-start, evolutionary algorithms.  
- **High-dimensional spaces**: many fairness criteria → use dimensionality reduction, hierarchical objectives, progressive exploration.  

---

### Evaluation Approach  
- **Pareto verification**: dominance analysis, local perturbations.  
- **Hypervolume**: measure coverage of frontier.  
- **Stakeholder evaluation**: check trade-off clarity, satisfaction, decision-making effort.  

---

## 4. Case Study: Lending Algorithm with Multiple Fairness Criteria  

### Scenario  
- Bank risk scoring model for loan approval.  
- Objectives: accuracy, demographic parity, equal opportunity.  
- Stakeholders: risk team, compliance, borrowers, business leaders.  

### Problem Analysis  
- Strict demographic parity → −15% accuracy.  
- DP vs EO sometimes conflict.  
- Intersectional disparities (e.g., young minority women).  
- Competing stakeholder priorities.  

### Solution Implementation  
- **Objectives**: accuracy (AUC), DP gap, EO gap.  
- **Pareto generation**: scalarization with varied weights.  
- **Visualization**: interactive 3D plots + 2D projections.  
- **Selection**: a posteriori → stakeholders chose model with 95% accuracy, DP below regulatory threshold, EO gap <5%.  
- **Intersectionality**: extended objectives to subgroup disparities.  

### Outcomes  
- Achieved balanced compromise → better than constraints or single fairness metric.  
- Transparent trade-offs improved stakeholder trust.  
- Challenges: computation + communicating high-dimensional results.  

**Lessons**:  
- Explicit modeling > ad hoc parameter tuning.  
- Visualization critical for communication.  
- Engagement with stakeholders transforms fairness from technical issue to collaborative decision.  

---

## 5. Frequently Asked Questions  

**Q1. Multi-objective vs Regularization?**  
- **Regularization**: simpler, implicit trade-offs via λ.  
- **Multi-objective**: explicit exploration of Pareto frontier, stakeholder engagement, multiple fairness criteria.  
- Use multi-objective when stakes are high, or multiple criteria must be balanced transparently.  

**Q2. Many objectives (intersectionality)?**  
- Reduce dimensionality by grouping metrics.  
- Use hierarchical/ progressive optimization.  
- Apply NSGA-III or reference-point algorithms.  
- Develop specialized visualizations (heatmaps, interactive dashboards).  

---

## 6. Project Component Development  

**Deliverable for Unit 5**:  
- **Formulation guide** for objectives.  
- **Pareto generation framework** (scalarization, constraints, evolutionary).  
- **Visualization & selection tools** for trade-offs.  

Integration:  
- Builds on Units 1–3 → constraints, adversarial, regularization.  
- Provides unifying framework for explicit fairness-performance trade-offs.  

---

## 7. Summary and Next Steps  

**Key Takeaways**  
- Trade-offs between fairness and performance are **inherent**.  
- **Pareto optimality** → principled compromise set.  
- **Scalarization** → practical exploration of frontier.  
- **Preference articulation** → stakeholders choose acceptable balances.  
- **Intersectionality** → requires multi-dimensional fairness objectives.  

**Looking Ahead**  
Unit 5 → integrate **constraints, adversarial, regularization, multi-objective** into a single **In-Processing Fairness Toolkit**.  

---

## References  

- Agarwal, A., Beygelzimer, A., Dudík, M., Langford, J., & Wallach, H. (2019). *A reductions approach to fair classification.* ICML.  
- Buolamwini, J., & Gebru, T. (2018). *Gender shades: Intersectional accuracy disparities in commercial gender classification.* FAT*.  
- Corbett-Davies, S., Pierson, E., Feller, A., Goel, S., & Huq, A. (2017). *Algorithmic decision making and the cost of fairness.* KDD.  
- Foulds, J. R., Islam, R., Keya, K. N., & Pan, S. (2020). *An intersectional definition of fairness.* ICDE.  
- Kleinberg, J., Ludwig, J., Mullainathan, S., & Rambachan, A. (2018). *Algorithmic fairness.* AEA Papers & Proc.  
- Martinez, N., Bertran, M., & Sapiro, G. (2020). *Minimax Pareto fairness.* ICML.  
- Valdivia, A., Sánchez-Monedero, J., & Casillas, J. (2021). *How fair can we go in machine learning?* Knowledge-Based Systems.  
- Zafar, M. B., Valera, I., Gomez-Rodriguez, M., & Gummadi, K. P. (2019). *Fairness constraints: A flexible approach for fair classification.* JMLR.  
