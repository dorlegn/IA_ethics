# Unit 2: Reweighting and Resampling Techniques

---

## 1. Conceptual Foundation and Relevance

### Guiding Questions
1. How can we systematically adjust the influence of training instances to mitigate bias without modifying feature values or model architectures?  
2. When are reweighting and resampling approaches more appropriate than other fairness interventions, and how do we implement them while preserving statistical validity?

### Conceptual Context
Reweighting and resampling are **foundational data-level interventions**.  
- They adjust **instance influence** instead of changing feature values or model architectures.  
- Valuable because they **preserve original distributions** while balancing representation in training.  
- Example: Loan approval datasets underrepresent minority approvals due to historical redlining. Reweighting/resampling counteracts this by giving more weight or additional representation to minority approvals.  

These methods are:  
- **Versatile and simple**, often implemented as preprocessing steps.  
- Compatible with most ML workflows.  
- Effective at improving fairness while maintaining predictive performance (Kamiran & Calders, 2012).  

This unit builds on **Unit 1 (auditing)** by translating bias patterns into reweighting/resampling strategies, and prepares for **Unit 3 (transformations)**.  

---

## 2. Key Concepts

### Instance Influence in Model Training
- Instance influence = how strongly each training example affects model learning.  
- Standard training: all instances equal → majority groups dominate.  
- Reweighting/resampling: adjust influence so underrepresented groups shape the model fairly.  
- Example: Qualified minority applicants get higher weights to counteract historical underrepresentation.  

---

### Reweighting Approaches for Fairness
- Assign **different weights** to training examples without altering dataset size.  
- Methods:  
  - Inverse representation weighting.  
  - Attribute–outcome weighting (Kamiran & Calders, 2012).  
  - Conditional independence weights (Calders & Verwer, 2010).  
- Example: Loan dataset → higher weights for minority approvals and majority rejections that contradict biased patterns.  

---

### Resampling Strategies for Balanced Learning
- Modify dataset composition by including/duplicating samples.  
- Especially useful when frameworks don’t support instance weights.  
- Approaches:  
  - **Uniform resampling** across groups.  
  - **Preferential resampling** of bias-reducing cases.  
  - **Synthetic methods** (SMOTE, Chawla et al. 2002).  
- Example: Oversample underrepresented demographic groups in medical data to prevent neglect in diagnosis models.  

---

### Statistical Considerations and Validity
- Risks of naive application:  
  - Higher variance (effective sample size shrinks).  
  - Estimation bias (distorted probabilities).  
  - Overfitting (extreme weights or oversampling).  
- Solutions:  
  - Weighted cross-validation.  
  - Regularization.  
  - Calibration monitoring (Zadrozny et al., 2003).  

---

### Domain Modeling Perspective
- **Data Preparation** → Resampling modifies dataset composition.  
- **Training Process** → Reweighting modifies optimization objective.  
- **Evaluation** → Weighted validation ensures fairness without loss of validity.  
- **Deployment** → Monitor for weight drift.  

---

### Conceptual Clarifications (Analogies)
- **Reweighting** = weighted voting → minority voices get more weight so all groups influence outcomes.  
- **Resampling** = curated reading list → intentionally include underrepresented authors for balance.  
- **Statistical validity** = jury selection adjustment → account for uneven representation with larger error margins.  

---

### Intersectionality Consideration
- Must account for **multiple protected attributes simultaneously**.  
- Example: Addressing gender and race separately may worsen disparities for women of color.  
- Strategies:  
  - Stratified/intersectional sampling.  
  - Intersection-aware weighting schemes (Ghosh et al., 2021).  
  - Metrics at intersection level.  

---

## 3. Practical Considerations

### Implementation Framework
- **Weighting strategies**: inverse group size, attribute–outcome balancing, conditional independence.  
- **Implementation**:  
  - If model supports weights → feed directly.  
  - If not → resample according to weights.  
- **Statistical safeguards**:  
  - Cross-validation for weighted data.  
  - Regularization.  
  - Calibration monitoring.  

### Implementation Challenges
- **Fairness vs. performance**: aggressive reweighting may reduce accuracy. → Use progressive weighting + hybrid methods.  
- **Multiple attributes**: too many intersections can cause sparse data. → Use hierarchical weighting, smoothing, dimensionality reduction.  

### Evaluation Approach
- **Fairness impact**: compare fairness metrics before/after, across intersections.  
- **Performance impact**: track accuracy, F1, AUC, calibration.  
- **Stability**: robustness to data splits, parameter sensitivity, new data.  

---

## 4. Case Study: Medical Diagnosis Algorithm

- **Scenario**: Cardiovascular risk prediction. Lower sensitivity for women due to historical underdiagnosis.  
- **Problem**: Labels biased, especially for women of color and older women.  
- **Solution**:  
  - **Outcome-aware reweighting**: boost weight for diagnosed women cases, downweight biased outcomes.  
  - **Intersectional resampling**: stratify by gender × age × race.  
  - **Safeguards**: weighted CV, regularization, calibration monitoring.  
- **Outcomes**:  
  - Sensitivity gap ↓ 68%.  
  - Improved fairness across intersections.  
  - Maintained clinical validity.  

---

## 5. FAQs

**Q1: When to use reweighting vs resampling?**  
- Reweighting → precise, continuous control; requires model support.  
- Resampling → more compatible; simpler; produces explicit balanced dataset.  
- In practice: try both, compare results.  

**Q2: How to design weighting schemes?**  
- Define fairness goal first (DP, EO, etc.).  
- Start with inverse frequency or attribute–outcome weighting.  
- Avoid extreme weights.  
- Use progressive weighting and validation.  
- Document trade-offs.  

---

## 6. Project Component Development

In Unit 5, build the **Reweighting & Resampling Selector**:  
- **Technique matrix**: pros/cons, assumptions, contexts.  
- **Decision trees**: map bias patterns → methods.  
- **Configuration guides**: formulas, code snippets.  
- **Integration**: connects to Unit 1 auditing and Unit 3 transformations.  

---

## 7. Summary and Next Steps

**Key takeaways**:  
- Instance influence is a key lever for fairness.  
- Different reweighting schemes target different bias patterns.  
- Resampling complements reweighting when model/infra constraints exist.  
- Statistical validity must be preserved.  

**Application**:  
- Start with auditing (Unit 1).  
- Apply moderate reweighting/resampling.  
- Evaluate trade-offs (fairness vs performance).  
- Iterate progressively.  

**Looking ahead**: Unit 3 → **Feature Transformation** methods to break unfair correlations at feature level.  

---

## References
- Calders, T., & Verwer, S. (2010). *Three naive Bayes approaches for discrimination-free classification.* DMKD, 21(2), 277–292.  
- Chawla, N. V., Bowyer, K. W., Hall, L. O., & Kegelmeyer, W. P. (2002). *SMOTE: Synthetic minority over-sampling technique.* JAIR, 16, 321–357.  
- Feldman, M., Friedler, S. A., Moeller, J., Scheidegger, C., & Venkatasubramanian, S. (2015). *Certifying and removing disparate impact.* KDD ’15.  
- Ghosh, A., Chhabra, A., Ling, S. Y., Narayanan, P., & Koyejo, S. (2021). *An intersectional framework for fair and accurate AI.* arXiv:2105.01280.  
- Iosifidis, V., & Ntoutsi, E. (2018). *Dealing with bias via data augmentation in supervised learning scenarios.* IoT Stream.  
- Kamiran, F., & Calders, T. (2012). *Data preprocessing techniques for classification without discrimination.* KAIS, 33(1), 1–33.  
- Zadrozny, B., Langford, J., & Abe, N. (2003). *Cost-sensitive learning by cost-proportionate example weighting.* ICDM ’03.  
