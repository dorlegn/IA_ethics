# Unit 3: Prediction Transformation Methods

## 1. Conceptual Foundation and Relevance

### Guiding Questions
- **Q1:** How can we transform model outputs to satisfy fairness constraints while minimizing information loss from the original predictions?  
- **Q2:** What techniques enable us to implement complex fairness criteria through direct output modifications when we cannot retrain the model or lack access to its internal workings?  

### Conceptual Context
Prediction transformation methods extend basic threshold adjustments and calibration into **more flexible post-processing interventions**.  

They matter because:
- They work even for **black-box models**, legacy systems, or third-party tools where retraining is impossible.  
- They **preserve useful predictive information** while enforcing fairness requirements.  
- They decouple model training from fairness enforcement (Dwork et al., 2018).  

This Unit builds on:
- **Threshold optimization (Unit 1):** adjusts binary decision boundaries.  
- **Calibration (Unit 2):** ensures probability consistency across groups.  
- **Prediction transformations (Unit 3):** generalize both, enabling complex fairness interventions.  

---

## 2. Key Concepts

### Learned Transformation Functions
- Discover mappings from original predictions → fair outputs.  
- Approaches:
  - **Optimization-based**: minimize distortion subject to fairness constraints.  
  - **Transfer learning**: small fair models adjust outputs of larger models.  
  - **Adversarial methods**: transform outputs so protected attributes cannot be inferred.  
- Example: Canetti et al. (2019) show learned functions achieve stronger fairness-utility trade-offs than fixed threshold adjustments.  

---

### Distribution Alignment Techniques
- Align output distributions across demographic groups.  
- Useful when labels are missing or partial (unsupervised/semi-supervised).  
- Approaches:  
  - **Quantile mapping** (Feldman et al., 2015).  
  - **Optimal transport** (minimum-cost distribution alignment).  
  - **Distribution matching** (reduce statistical distance between groups).  
- Goal: prediction patterns are consistent across groups, preserving rank within each group.  

---

### Fair Score Transformations
- Directly modify prediction scores while preserving within-group order.  
- Crucial for ranking, recommendation, and risk scoring.  
- Approaches:  
  - **Monotonic transformations** (adjust scores without breaking order).  
  - **Constrained re-ranking** (adjust positions to satisfy fairness).  
  - **Score normalization** (align score scales across groups).  
- Example: Wei et al. (2020) show effective fairness improvements in ranking contexts.  

---

### Domain Modeling Perspective
Prediction transformations integrate into ML systems as:  
- **Output Layer Modification**: transformation before decision.  
- **Group-Specific Processing**: tailored adjustments using protected attributes.  
- **Decision Pipeline Integration**: sits between model and application.  
- **Evaluation Framework**: track fairness vs. utility.  
- **Model Independence**: works without model retraining.  

---

### Conceptual Clarifications (Analogies)
- **Learned transformations** ≈ currency exchange → convert scores to equivalent “value” across groups.  
- **Distribution alignment** ≈ standardized test score normalization across schools.  
- **Fair score transformations** ≈ handicapping in golf → adjusted scores for a fairer competition.  

---

### Intersectionality Consideration
- Simple transformations may miss **intersectional unfairness** (e.g., young Black women).  
- Approaches needed:  
  - Multi-attribute transformation functions.  
  - Hierarchical methods for small samples.  
  - Adaptive techniques detecting intersectional bias.  
  - Evaluation across demographic combinations.  
- Foulds et al. (2020) stress explicit modeling of intersections.  

---

## 3. Practical Considerations

### Implementation Framework
1. **Transformation Design**  
   - Classification: keep scores in [0,1].  
   - Regression: preserve scale.  
   - Ranking: preserve within-group ordering.  
2. **Learning Process**  
   - Use validation data with protected attributes.  
   - Optimize fairness ↔ utility balance.  
   - Regularize to avoid instability.  
3. **Deployment Integration**  
   - Implement as lightweight service or post-processing layer.  
   - Ensure compatibility with downstream systems.  
   - Document transformation behavior for transparency.  

---

### Challenges
- **Complexity vs. Interpretability** – complex mappings are harder to explain.  
- **Data requirements** – need sufficient validation samples per group.  
- **Intersectional sparsity** – small groups require smoothing/regularization.  

---

### Evaluation Approach
- **Fairness-Utility Analysis**: measure fairness gains vs. prediction distortion.  
- **Robustness Testing**: check subgroup stability and resilience to drift.  
- **Comparative Evaluation**: show benefit over simpler threshold/calibration methods.  

---

## 4. Case Study: Lending Algorithm Fairness

### Scenario Context
- A bank uses a **risk score model (0–100)** for loan approvals and interest rates.  
- Problem: marginalized groups receive systematically lower scores → reduced access to credit.  
- Constraint: cannot retrain model (compliance + cost).  

### Problem Analysis
- **Distribution discrepancies**: thresholds insufficient.  
- **Need to preserve score meaning**: rank matters to loan officers.  
- **Intersectional effects**: young women from marginalized racial groups most disadvantaged.  

### Solution Implementation
- **Transformation design**: monotonic, group-specific transformations preserving order.  
- **Learning**: optimization objective balancing fairness, accuracy, rank consistency.  
- **Intersectionality**: hierarchical approach – specific mappings for larger subgroups, regularized mappings for smaller ones.  
- **Deployment**: service layer applying transformations in real time, with uncertainty estimates near thresholds.  

### Outcomes
- Score disparities ↓ **65%**.  
- Predictive accuracy preserved at **92%** of original.  
- Intersectional disparities improved across subgroups.  
- Loan officers: interpretability intact, seamless workflow integration.  

---

## 5. Frequently Asked Questions (FAQ)

**Q1. How do I design fair transformations that preserve prediction meaning?**  
A: Choose functions that respect the prediction type (bounded probabilities, monotonic rankings). Use simple, explainable mappings where possible (linear shifts, scaling). Only increase complexity when necessary, validating each step.  

**Q2. When should I use transformations vs. retraining?**  
A: Use transformations when retraining is impossible, expensive, or requires long validation cycles. Use retraining when you have full access and the bias is deeply embedded in data representation. Many organizations apply transformations as **short-term fixes** while working on longer-term retraining solutions.  

---

## 6. Project Component Development

In Unit 5, you will build the **Prediction Transformation Section** of the Post-processing Calibration Guide:  
- **Selection Framework** – when to use learned transformations, distribution alignment, or fair score adjustments.  
- **Implementation Templates** – practical patterns for classification, regression, ranking.  
- **Evaluation Methodology** – fairness-utility analysis, robustness checks, visualization.  

---

## 7. Summary and Next Steps

### Key Takeaways
- Prediction transformations = **fairness without retraining**.  
- Methods: learned functions, distribution alignment, fair score adjustments.  
- They balance fairness gains with information preservation.  
- Crucial for black-box or legacy model contexts.  

### Next
**Unit 4 → Rejection Option Classification**: how to handle uncertain predictions where automated fairness interventions may be insufficient.  

---

## References
- Canetti, R., et al. (2019). *From soft classifiers to hard decisions: How fair can we be?* FAT*.  
- Dwork, C., et al. (2018). *Decoupled classifiers for group-fair and efficient machine learning.* FAT*.  
- Feldman, M., et al. (2015). *Certifying and removing disparate impact.* KDD.  
- Foulds, J. R., et al. (2020). *An intersectional definition of fairness.* ICDE.  
- Wei, K., et al. (2020). *FairSight: Visual analytics for fairness in decision making.* IEEE TVCG.  
