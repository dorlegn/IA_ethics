# Unit 4: Fairness-Aware Data Generation

---

## 1. Conceptual Foundation and Relevance

### Guiding Questions
1. How can generative approaches create balanced datasets that preserve desired properties while mitigating bias patterns identified in original data?  
2. What are the trade-offs between modifying existing data through reweighting or transformation versus generating entirely new synthetic data for fairness purposes?  

### Conceptual Context
- Traditional pre-processing (reweighting, transformation) may be insufficient.  
- Generative methods create **entirely new fairness-aware data**, useful when:  
  - Severe representation imbalances exist.  
  - Minority groups are underrepresented.  
  - Privacy prevents modifying original data.  

Generative methods can:  
- Fill representation gaps.  
- Reduce problematic correlations.  
- Create counterfactual examples.  

**Key idea**: generation can produce samples **beyond what exists**, enabling fairness that modification cannot.  

---

## 2. Key Concepts

### Synthetic Data Generation for Fairness
- Creates **new samples** that satisfy fairness constraints.  
- Overcomes limitations of reweighting/transformation (cannot create unseen examples).  
- Xu et al. (2019) – **FairGAN** → generates realistic, bias-reduced data.  

*Example*: Loan applications with synthetic applicants breaking historical correlations (income × gender × geography).  

---

### Conditional Generation for Group Fairness
- Conditions generation on **protected attributes** to balance group representation.  
- Ensures **statistical parity by design**.  
- Choi et al. (2020): conditional tabular GANs create datasets with specified demographic compositions.  

*Example*: Employment dataset → balanced synthetic candidates across gender and race with equal qualification distributions.  

---

### Counterfactual Data Augmentation
- Creates **“what if” variants**: change protected attributes, hold other variables constant.  
- Implements **counterfactual fairness**.  
- Kusner et al. (2017): counterfactual augmentation helps models ignore discriminatory pathways.  

*Example*: Resume screening → generate same resume with name/gender swapped, qualifications unchanged.  

---

### Domain Modeling Perspective
- **Requirements analysis** → define fairness objectives.  
- **Generation design** → choose model + constraints.  
- **Fairness constraint implementation** → conditionals, adversarial terms, filtering.  
- **Integration** → combine synthetic + original data, define weights.  
- **Quality assurance** → validate both fairness and predictive utility.  

---

### Conceptual Clarifications (Analogies)
- **Synthetic data generation** = creating a custom recipe from scratch.  
- **Conditional generation** = programmed manufacturing with exact specifications.  
- **Counterfactual augmentation** = parallel universes of the same person, differing only in protected attributes.  

---

### Intersectionality Consideration
- Must handle **multiple protected attributes at once**.  
- Risks of naive approaches: women of color underrepresented even if women + minorities balanced.  
- Ghosh et al. (2021): intersectional fairness requires:  
  - Multi-attribute conditioning.  
  - Subgroup quality checks.  
  - Constraints to avoid stereotypes.  
  - Intersectional fairness metrics.  

---

## 3. Practical Considerations

### Implementation Framework
1. **Requirements Analysis**  
   - Identify gaps, correlations, constraints.  
   - Define fairness + utility goals.  

2. **Approach Selection**  
   - GANs for images.  
   - VAEs for tabular.  
   - Statistical approaches for simpler data.  

3. **Constraint Implementation**  
   - Conditioned models.  
   - Adversarial fairness constraints.  
   - Counterfactual rules.  

4. **Integration**  
   - Mix synthetic + real data.  
   - Apply weighting/transition strategies.  
   - Document processes clearly.  

---

### Implementation Challenges
- **Fairness vs. realism** trade-offs.  
- **Artifacts** → risk of unrealistic data.  
- **High resource needs** → computational + domain expert validation.  

---

### Evaluation Approach
- **Fairness**: representation, reduced correlations, consistent predictions across counterfactuals.  
- **Utility**: predictive accuracy, preserved relationships, similarity to real data.  
- **Robustness**: performance on new data, time stability, subgroup checks.  

---

## 4. Case Study: Healthcare Risk Prediction

**Scenario**: Predict hospital readmission.  
- Underrepresented groups: elderly rural minority patients.  
- Privacy prevented more sampling.  

**Problem**:  
- Severe underrepresentation.  
- Complex feature relations (medical + social).  
- Need to separate legitimate biological vs biased care differences.  

**Solution**:  
- Used **Conditional VAE** with fairness constraints.  
- Hybrid dataset = real + synthetic patients.  
- Controlled demographic balance, preserved medical logic.  

**Outcomes**:  
- Prediction disparities ↓ 43%.  
- Identified new risk factors for minorities.  
- Addressed privacy while maintaining utility.  

---

## 5. FAQs

**Q1: When to generate vs. modify?**  
- Use generation when:  
  - <20–30 samples for a group.  
  - Severe underrepresentation (<5%).  
  - Complex correlations embedded across many features.  
  - Privacy/legal constraints block modification.  

**Q2: How to validate synthetic data?**  
- Combine:  
  - **Metrics** (fairness + utility).  
  - **Expert review** for plausibility.  
  - **Counterfactual consistency** checks.  
  - **Progressive integration** monitoring.  

---

## 6. Project Component Development
- **Decision tree** → when to use generation.  
- **Constraint guide** → templates for conditional/adversarial/counterfactual rules.  
- **Integration strategy** → ratios, weighting, validation guidelines.  

---

## 7. Summary and Next Steps

**Key takeaways**:  
- Generation goes beyond modification, creating **new fair data**.  
- **Conditional generation** → guarantees group fairness.  
- **Counterfactual generation** → directly operationalizes causal fairness.  
- Must rigorously validate fairness **and** utility.  

**Application guidance**:  
- Start with generation when gaps are severe, correlations complex, or privacy prevents modification.  
- Choose models based on data type.  
- Validate both fairness and predictive performance.  
- Document process thoroughly.  

**Looking ahead**: Unit 5 → build the **Pre-processing Strategy Selector** combining auditing, reweighting, transformation, and generation.  

---

## References
- Choi, E. et al. (2017). *Generating multi-label discrete patient records using GANs.* MLHC.  
- Ghosh, A. et al. (2021). *Intersectional fairness in generative models.* arXiv:2103.13775.  
- Iosifidis, V., & Ntoutsi, E. (2018). *Dealing with bias via data augmentation.* Workshop on AI For Societal Good.  
- Kusner, M. J. et al. (2017). *Counterfactual fairness.* NeurIPS.  
- Sattigeri, P. et al. (2019). *Fairness GAN.* IBM JRD.  
- Xu, D. et al. (2019). *FairGAN.* IEEE Big Data.  
- Zhang, B. et al. (2018). *Mitigating unwanted biases with adversarial learning.* AIES.  
