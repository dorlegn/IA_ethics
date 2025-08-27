# Unit 3: Distribution Transformation Approaches

---

## 1. Conceptual Foundation and Relevance

### Guiding Questions
1. How can we transform feature distributions to mitigate bias while preserving the predictive utility of our data?  
2. What are the mathematical foundations and practical implementations of distribution transformation techniques that enable fair prediction without requiring changes to modeling algorithms?

### Conceptual Context
- Reweighting and resampling (Unit 2) adjust **instance influence** but leave features unchanged.  
- Many biases come from **problematic correlations** between protected attributes and other features (proxies).  
- Distribution transformation modifies the **feature space** itself.  
- Example: Zip code may act as a proxy for race in lending. Simply removing it discards useful info, but transformation can preserve predictive signal while removing proxy effects.  

**Key idea**: Transform features to reduce correlation with protected attributes while keeping predictive power.  

- Feldman et al. (2015): “Disparate Impact Removal” → map group distributions to a common reference while preserving rank order.  
- Zemel et al. (2013): Learn **fair representations** that obscure protected attributes but preserve prediction-relevant info.  

This unit complements auditing (Unit 1) and reweighting (Unit 2), adding a powerful tool for proxy discrimination.  

---

## 2. Key Concepts

### Disparate Impact Removal
- Adjust distributions so features cannot predict protected attributes.  
- Preserves rank-order and predictive utility.  
- Example: Transform “distance to financial center” to have the same distribution across racial groups.  
- Feldman et al. (2015) → “repair” feature distributions to break proxy discrimination.  

---

### Optimal Transport for Fair Representations
- Frame transformation as an **optimization problem**:  
  - Minimize information loss (“transport cost”).  
  - Achieve independence from protected attributes.  
- Handles **multidimensional features**.  
- Example: Resume screening → transform communication style/education distributions across genders with minimal distortion.  
- Jiang et al. (2020): FARE uses optimal transport for fairness.  

---

### Learning Fair Representations
- Create **new feature spaces** that obscure protected attributes but preserve prediction relevance.  
- Extends beyond modifying features → learns a new representation.  
- Zemel et al. (2013): LFR balances fairness, fidelity, accuracy.  
- Madras et al. (2018): LAFTR uses adversarial learning for fair, transferable representations.  
- Particularly valuable for **text, images, or high-dimensional tabular data**.  

---

### Domain Modeling Perspective
- **Feature Engineering** → transforms attributes into new fair representations.  
- **Pipeline Integration** → must apply same transformations at training + inference.  
- **Evaluation** → check both fairness and predictive utility.  
- **Deployment** → transformations must remain stable over time.  

---

### Conceptual Clarifications (Analogies)
- **Disparate impact removal** = color correction in photography → balance representation without losing meaning.  
- **Optimal transport** = logistics optimization → move “goods” (info) efficiently to fair distribution.  
- **Fair representations** = gender-neutral translation → preserve meaning but remove biased signals.  

---

### Intersectionality Consideration
- Transformations must handle **multiple attributes together**, not separately.  
- Foulds et al. (2020): single-attribute fairness can worsen disparities at intersections.  
- Example: Ensure features cannot predict “Black woman,” not just race or gender independently.  

---

## 3. Practical Considerations

### Implementation Framework
1. **Feature Correlation Analysis**  
   - Identify features correlated with protected attributes.  
   - Quantify correlation strength and predictive value.  

2. **Technique Selection**  
   - Simple correlations → univariate distribution alignment.  
   - Complex, multidimensional → optimal transport.  
   - High-dimensional/text → fair representation learning.  

3. **Implementation**  
   - Build pipelines consistent for training/inference.  
   - Parameterize transformations during training, apply without protected attributes at inference.  

4. **Evaluation**  
   - Assess fairness (independence).  
   - Assess utility (accuracy, rank-order).  
   - Compare techniques, refine trade-offs.  

---

### Implementation Challenges
- **Fairness vs. utility trade-offs**: stronger transformations may harm predictive power.  
- **Computational cost**: optimal transport can be expensive for large, high-dimensional data.  
- **Robustness**: transformations must hold across time and new data.  

---

### Evaluation Approach
- **Independence**: measure predictability of protected attributes after transformation.  
- **Utility preservation**: check predictive performance and rank order.  
- **Robustness**: test stability across datasets, outliers, and time.  

---

## 4. Case Study: Job Recommendation Algorithm

**Scenario**: Algorithm recommended higher-paying tech jobs to men more than women with similar qualifications.  

- **Bias source**: gender-correlated features (language style, engagement metrics, education).  
- **Intersectionality**: women with non-traditional paths most disadvantaged.  

**Solution**:  
- Feature correlation analysis → identified 12 strongly gender-correlated features.  
- Mixed methods:  
  - Disparate impact removal for simple features.  
  - Optimal transport for multidimensional clusters.  
  - LAFTR for text features.  
- Evaluation:  
  - Gender predictability from features ↓ 87%.  
  - Job recommendation disparity ↓ from 37% → 6%.  
  - Utility preserved at 94% of original relevance.  

---

## 5. FAQs

**Q1: How to transform when protected attributes aren’t available at deployment?**  
- Use protected attributes **only during training** to learn transformations.  
- Apply learned transforms at inference without needing protected attributes.  

**Q2: How to handle multiple protected attributes?**  
- Use **intersectional transformations** (independence from combined attributes).  
- Or hierarchical/multi-objective optimization to balance trade-offs.  

---

## 6. Project Component Development
- **Decision tree**: when to apply distribution transformation.  
- **Technique catalog**: from univariate repairs → optimal transport → representation learning.  
- **Implementation guides**: code patterns, computational tips, pipeline integration.  

Integration: complements auditing (Unit 1) + reweighting (Unit 2); provides options when bias stems from proxies.  

---

## 7. Summary and Next Steps

**Key takeaways**:  
- Transformations fix **proxy discrimination** by modifying feature distributions.  
- **Disparate impact removal** → univariate fixes.  
- **Optimal transport** → multidimensional, minimal information loss.  
- **Fair representations** → new feature spaces optimized for fairness.  
- Must explicitly handle **intersectionality**.  

**Application**:  
- Start with correlation analysis.  
- Choose technique by complexity.  
- Evaluate trade-offs (fairness vs. predictive accuracy).  
- Document all transformations.  

**Looking ahead**: Unit 4 → **Fairness-Aware Data Generation** (synthetic data creation).  

---

## References
- Feldman, M. et al. (2015). *Certifying and removing disparate impact.* KDD ’15.  
- Foulds, J. R. et al. (2020). *An intersectional definition of fairness.* ICDE ’20.  
- Jiang, R. et al. (2020). *Wasserstein fair classification.* UAI ’20.  
- Madras, D. et al. (2018). *Learning adversarially fair and transferable representations.* ICML ’18.  
- Zemel, R. et al. (2013). *Learning fair representations.* ICML ’13.  
- Lum, K., & Johndrow, J. E. (2016). *A statistical framework for fair predictive algorithms.* arXiv:1610.08077.  
- Creager, E. et al. (2019). *Flexibly fair representation learning by disentanglement.* ICML ’19.  
