# Unit 1: Fairness Objectives and Constraints  

---

## 1. Conceptual Foundation and Relevance  

### Guiding Questions  
- **Q1.** How can abstract fairness definitions be translated into concrete optimization objectives and constraints that algorithms can directly optimize during training?  
- **Q2.** What are the mathematical and computational implications of incorporating fairness constraints into model optimization, and how do these affect model performance?  

### Conceptual Context  
Fairness cannot be an afterthought. While **pre-processing** adjusts the training data and **post-processing** modifies outputs, **in-processing** directly embeds fairness in the model’s optimization.  

This is done by reformulating standard optimization problems (e.g., minimize classification error) to also include **fairness constraints** or **multi-objective formulations**. The result is a model that is fair **by design**.  

- **Dwork et al. (2012)** emphasized that pre-processing alone cannot guarantee fairness if the model’s decision boundary remains biased.  
- In-processing provides **mathematical guarantees** by constraining the decision boundary itself.  

This unit sets the foundation for the *In-Processing Fairness Toolkit (Unit 5)*, equipping you to:  
1. Translate fairness definitions into mathematical constraints.  
2. Implement constrained optimization methods.  
3. Understand trade-offs between fairness and performance.  

---

## 2. Key Concepts  

### Translating Fairness Definitions to Mathematical Constraints  
- **Demographic parity** → equality of mean predictions across groups:  
  \[
  |E[h(X) | Z = 0] - E[h(X) | Z = 1]| \leq \epsilon
  \]  

- **Equalized odds** → conditional equality constraints across groups given ground truth.  

**Zafar et al. (2017)** showed how convex relaxations can bring fairness constraints into logistic regression.  

---

### Constrained Optimization Approaches  
Baseline optimization:  
\[
\min_\theta L(\theta)
\]  

Fairness-constrained optimization:  
\[
\min_\theta L(\theta) \quad \text{subject to } C_i(\theta) \leq \epsilon_i
\]  

**Agarwal et al. (2018)** introduced reduction methods to turn constrained problems into unconstrained ones, enabling fairness across many model classes.  

---

### Lagrangian Methods and Duality  
Fairness-constrained loss with multipliers:  
\[
\mathcal{L}(\theta, \lambda) = L(\theta) + \sum_i \lambda_i C_i(\theta)
\]  

- Multipliers control the **trade-off** between performance and fairness.  
- **Cotter et al. (2019)** extended Lagrangian approaches to handle multiple, non-differentiable fairness constraints.  

---

### Feasibility and Trade-offs  
- **Feasible region** = set of model parameters that satisfy fairness constraints.  
- If constraints are too strict, feasible region shrinks (or is empty).  
- Trade-offs must be understood: stricter fairness → possible performance drops.  

**Menon & Williamson (2018)** quantified costs of fairness in classification.  

---

### Domain Modeling Perspective  
Fairness constraints affect multiple components:  
- **Objective function** → fairness as extra terms.  
- **Constraint definition** → boundaries for fairness compliance.  
- **Optimization algorithm** → must handle constrained problems.  
- **Evaluation** → fairness + accuracy both assessed.  
- **Model selection** → trade-offs determine deployment choice.  

---

### Intersectionality Consideration  
Standard constraints may protect gender and race separately, but fail at intersections (e.g., women of minority ethnicity).  

- **Kearns et al. (2018)**: subgroup fairness.  
- **Foulds et al. (2020)**: efficient intersectional fairness across many subgroups.  

Approaches:  
- Multi-attribute constraints.  
- Hierarchical constraint structures.  
- Statistical aggregation to handle combinatorial explosion.  

---

## 3. Practical Considerations  

### Implementation Framework  
1. **Constraint Formulation**  
   - Equality or inequality constraints.  
   - Proxy constraints if exact ones are intractable.  

2. **Optimization Integration**  
   - Choose algorithm (projected gradient, Lagrangian, ADMM).  
   - Monitor constraint satisfaction.  

3. **Feasibility Analysis**  
   - Check if fairness constraints can be satisfied.  
   - Adjust tolerance ε for balance.  

---

### Implementation Challenges  
- **Optimization difficulty**: non-convex landscapes, convergence issues.  
- **Trade-offs**: strict fairness can hurt predictive accuracy.  
- **Resource cost**: constrained optimization is computationally heavier.  

---

### Evaluation Approach  
- **Constraint satisfaction verification**: check violations on train/test.  
- **Performance impact assessment**: compare constrained vs unconstrained.  
- **Subgroup analysis**: ensure fairness persists across intersections.  

---

## 4. Case Study: Loan Approval System  

**Scenario Context**  
- Model: predict default risk for loans.  
- Issue: minority applicants had 15% lower approval despite equivalent creditworthiness.  

**Problem Analysis**  
- Fairness definition: **Demographic Parity**.  
- Translation: constrain mean predictions across racial groups.  
- Implementation:  
  - Strict constraint infeasible.  
  - Relaxed inequality (ε = 0.05) workable.  

**Optimization Approach**  
- Logistic regression with Lagrangian formulation.  
- Intersectional fairness extended to young minority applicants.  

**Results**  
- Disparity reduced: 15% → 4.8%.  
- Accuracy drop limited to 3%.  
- Intersectional protections improved subgroup outcomes.  

**Lessons Learned**  
- Relaxed constraints often more practical.  
- Multiple ε values should be tested (Pareto analysis).  
- Intersectional fairness must be explicitly encoded.  

---

## 5. Frequently Asked Questions  

**Q1. Equality vs Inequality vs Lagrangian constraints?**  
- Equality = strongest guarantees, often infeasible.  
- Inequality = flexible, realistic.  
- Lagrangian = best for exploring trade-offs.  

**Q2. Multiple protected attributes?**  
- Avoid constraint explosion.  
- Use subgroup fairness (Kearns et al.) or statistical aggregation (Foulds et al.).  

---

## 6. Project Component Development  

**Deliverable in Unit 5**:  
- **Fairness Constraint Catalog** → math formulations per fairness definition.  
- **Implementation Patterns** → Lagrangian, projection, ADMM examples.  
- **Trade-off Analysis Tools** → Pareto front visualizations, feasibility checks.  

Integration:  
- Builds on causal audits (Part 1).  
- Complements pre-processing (Part 2).  
- Foundations for adversarial (Unit 2) and regularization (Unit 3).  

---

## 7. Summary and Next Steps  

**Key Takeaways**  
- Fairness definitions can be translated into precise mathematical constraints.  
- Constrained optimization integrates fairness directly into training.  
- Lagrangian methods provide flexible trade-offs.  
- Feasibility analysis is critical for practical adoption.  
- Intersectionality requires advanced formulations.  

**Application Guidance**  
- Start with inequality constraints with tolerance ε.  
- Monitor feasibility and constraint violations.  
- Explore multiple models with varying ε.  
- Communicate trade-offs clearly with stakeholders.  

**Looking Ahead**  
Next unit → **Adversarial debiasing**: fairness through competing objectives rather than explicit constraints.  

---

## References  

- Agarwal, A., Beygelzimer, A., Dudík, M., Langford, J., & Wallach, H. (2018). *A reductions approach to fair classification.* ICML.  
- Cotter, A., Jiang, H., Gupta, M. R., Wang, S., Narayan, T., You, S., & Sridharan, K. (2019). *Optimization with non-differentiable constraints with applications to fairness.* JMLR.  
- Dwork, C., Hardt, M., Pitassi, T., Reingold, O., & Zemel, R. (2012). *Fairness through awareness.* ITCS.  
- Foulds, J. R., Islam, R., Keya, K. N., & Pan, S. (2020). *An intersectional definition of fairness.* ICDE.  
- Kearns, M., Neel, S., Roth, A., & Wu, Z. S. (2018). *Preventing fairness gerrymandering: Auditing and learning for subgroup fairness.* ICML.  
- Menon, A. K., & Williamson, R. C. (2018). *The cost of fairness in binary classification.* FAT*.  
- Zafar, M. B., Valera, I., Gomez Rodriguez, M., & Gummadi, K. P. (2017). *Fairness constraints: Mechanisms for fair classification.* AISTATS.  
