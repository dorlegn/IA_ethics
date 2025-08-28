# Unit 2: Calibration Across Groups

## 1. Conceptual Foundation and Relevance

### Guiding Questions
- **Q1:** How do we ensure predicted probabilities convey consistent meaning across demographic groups?  
- **Q2:** How can we address calibration disparities without sacrificing other fairness properties?  

### Conceptual Context
Calibration ensures that predicted probabilities align with actual outcomes **consistently across demographic groups**.  
A 70% risk prediction should mean the same thing for everyone, regardless of group membership.  

Why it matters:
- Miscalibration creates **hidden unfairness** even in accurate models (Pleiss et al. 2017).  
- Critical in **lending, healthcare, criminal justice, hiring**, where probability estimates directly influence life-changing decisions.  
- Calibration is distinct from error-rate parity: it focuses on **probability reliability**, not just classification outcomes.  

This Unit builds on **threshold optimization (Unit 1)**:
- Thresholds adjust **decision boundaries**.  
- Calibration corrects **probability scores themselves**.  
- Together, they form the foundation for the **Post-processing Calibration Guide (Unit 5)**.  

---

## 2. Key Concepts

### Calibration as a Fairness Criterion
- Definition: For probability *p%*, exactly *p%* of cases should be positive.  
- Miscalibration across groups = same score means different risks → unfair outcomes.  
- Kleinberg et al. (2016): calibration conflicts with equal error rates when base rates differ → impossible to satisfy all fairness criteria simultaneously.  

### Group-Specific Calibration Techniques
- **Platt Scaling (logistic regression transform)** – simple, effective for moderate miscalibration.  
- **Isotonic Regression (non-parametric)** – flexible, preserves ranking, good for non-linear issues.  
- **Beta Calibration** – models probabilities with bounded beta distribution.  
- **Temperature Scaling** – common in neural networks, adjusts logits with one parameter.  

These can be applied **per demographic group** to align probabilities consistently.

### Calibration Evaluation Metrics
- **ECE (Expected Calibration Error)** – average gap between predicted and actual.  
- **MCE (Maximum Calibration Error)** – worst-case group disparity.  
- **Reliability Diagrams** – visualize predicted vs. observed outcomes.  
- **Group-Specific Metrics** – must be computed separately per demographic group.  

### Calibration-Fairness Trade-off
- Cannot have: perfect calibration + balanced error rates + equal base rate handling (impossibility theorem).  
- Requires **prioritization**: calibration is often more critical in risk-assessment contexts (Corbett-Davies & Goel, 2018).  
- Trade-offs must be **documented and explained to stakeholders**.  

### Domain Modeling Perspective
- **Probability Calibration Layer** – transforms outputs.  
- **Group-Specific Functions** – separate mappings per group.  
- **Calibration Dataset** – holdout set for fitting curves.  
- **Monitoring Module** – track calibration drift.  
- **Governance Manager** – navigate calibration vs. fairness trade-offs.  

---

## 3. Practical Considerations

### Implementation Framework
1. **Assessment**  
   - Compute ECE/MCE per group.  
   - Draw reliability diagrams.  
   - Document disparities.  

2. **Method Selection**  
   - Platt scaling → parametric, simple miscalibration.  
   - Isotonic regression → flexible, non-linear.  
   - Temp scaling → deep learning models.  
   - Histogram/binning → complex score distributions.  

3. **Process**  
   - Split into train / calibration / test sets.  
   - Fit transformations separately per group.  
   - Apply calibrated scores in predictions.  

4. **Validation**  
   - Compare pre- vs. post-calibration metrics.  
   - Check for impacts on other fairness criteria.  
   - Preserve ranking consistency when needed.  

### Challenges
- **Small sample sizes** – harder calibration for minority groups → use Bayesian/smoothing.  
- **Deployment complexity** – multiple calibration curves require lookup systems.  
- **Drift** – recalibration needed as distributions change.  

### Resource Requirements
- Sufficient validation data with group labels.  
- Infrastructure for group-specific mappings.  
- Monitoring pipeline for recalibration.  

---

## 4. Case Study: Recidivism Risk Assessment

### Scenario Context
- A justice system uses ML to predict **recidivism risk**.  
- Risk scores influence parole and sentencing decisions.  
- Initial analysis → equal accuracy across groups, **but reliability diagrams show miscalibration**:  
  - Black defendants: risk underestimated (−5–10%).  
  - Hispanic defendants: risk overestimated (+7–12%).  

Stakeholders: judges, defendants, compliance officers, communities.  
Problem: same score → different meaning → **hidden unfairness**.  

### Problem Analysis
- **Fairness definition**: Calibration takes priority (probability interpretation matters most).  
- **ROC analysis**: Threshold adjustments insufficient (from Unit 1).  
- **Trade-offs**: Calibration improved interpretation consistency but slightly worsened demographic parity.  
- **Intersectionality**: Worst disparities for young Hispanic men and older Black women.  

### Solution Implementation
- **Method**: Isotonic regression per group (handles non-linear miscalibration).  
- **Process**:  
  - Split data into calibration-train/test sets.  
  - Fitted group-specific curves.  
  - Built lookup system + fallback strategies for small groups.  
- **Intersectionality**: Hierarchical borrowing for small intersectional groups.  
- **Trade-off navigation**: Stakeholders agreed calibration > equal detention rates.  

### Outcomes
- **ECE reduced** from 0.08 → 0.03 across groups.  
- Scores now represent **consistent actual risk**.  
- Improved decision consistency for judges.  
- **Challenges**:  
  - Small groups remained harder to calibrate.  
  - Needed regular recalibration.  
  - Communication to non-technical stakeholders required visual + intuitive explanations.  

---

## 5. Frequently Asked Questions (FAQ)

**Q1. Calibration vs. Error Rate Fairness**  
A: Prioritize calibration when score *interpretation* drives decisions (e.g., medical risk, credit scoring). Prioritize error rates when binary decisions are final (e.g., hiring with fixed cutoff). Document trade-offs—perfect balance is mathematically impossible (Kleinberg et al., 2016).  

**Q2. Calibration Without Protected Attributes**  
A: Options include:  
- Use **proxy variables** (geography, etc.) where legal.  
- **Multiaccuracy methods** (Kim et al., 2019) detect subgroup miscalibration without labels.  
- **Distributionally robust optimization** during training.  
- **Ensemble calibration transformations**.  

These yield partial but meaningful improvements.  

---

## 6. Project Component Development

In Unit 5, you will build the **Calibration Methodology Guide** with:  
- Group-specific calibration assessment framework.  
- Decision guide for selecting methods (Platt, isotonic, temp scaling).  
- Reusable implementation templates.  
- Evaluation and monitoring strategies.  

---

## 7. Summary and Next Steps

### Key Takeaways
- Calibration = **probabilities mean the same across groups**.  
- Techniques: Platt, isotonic, beta, temperature scaling.  
- Metrics: ECE, MCE, reliability diagrams.  
- Trade-offs: cannot satisfy all fairness criteria simultaneously.  
- Calibration is crucial where **probability interpretation drives decisions**.  

### Next
Unit 3 → **Prediction Transformation Methods**: general post-processing modifications that go beyond calibration, enabling fairness via direct score transformations.  

---

## References
- Corbett-Davies, S., & Goel, S. (2018). *The measure and mismeasure of fairness.* arXiv:1808.00023.  
- Guo, C., Pleiss, G., Sun, Y., & Weinberger, K. Q. (2017). *On calibration of modern neural networks.* ICML.  
- Kim, M. P., Ghorbani, A., & Zou, J. (2019). *Multiaccuracy: Black-box post-processing for fairness in classification.* AIES.  
- Kleinberg, J., Mullainathan, S., & Raghavan, M. (2016). *Inherent trade-offs in the fair determination of risk scores.* ITCS.  
- Kull, M., Silva Filho, T. M., & Flach, P. (2017). *Beta calibration.* AISTATS.  
- Kumar, A., Liang, P. S., & Ma, T. (2019). *Verified uncertainty calibration.* NeurIPS.  
- Naeini, M. P., Cooper, G. F., & Hauskrecht, M. (2015). *Bayesian binning into quantiles.* AAAI.  
- Platt, J. (1999). *Probabilistic outputs for support vector machines.* Large Margin Classifiers.  
- Pleiss, G., Raghavan, M., Wu, F., Kleinberg, J., & Weinberger, K. Q. (2017). *On fairness and calibration.* NeurIPS.  
- Zadrozny, B., & Elkan, C. (2002). *Transforming classifier scores into accurate probability estimates.* KDD.  
