# Unit 2: Building Causal Models for Bias Detection

## 1. Conceptual Foundation and Relevance
- **Guiding Q1:** How to translate domain knowledge into formal causal models that represent bias mechanisms?  
- **Guiding Q2:** How to identify and validate critical causal pathways from protected attributes to outcomes?  
- **Context:**  
  - Causal models reveal *root causes* of bias, not just symptoms.  
  - They provide explicit representations of how protected attributes influence outcomes.  
  - Foundation for targeted interventions, counterfactual fairness, and robust bias detection.  

---

## 2. Key Concepts
### Causal Graph Construction
- **Directed Acyclic Graphs (DAGs):** Nodes = variables; edges = causal relationships.  
- Capture:  
  - Direct discrimination (protected attribute → outcome)  
  - Indirect discrimination (via mediators)  
  - Proxy discrimination (via shared ancestors/proxies).  

### Identifying Causal Variables and Relationships
- Systematic approach to selecting variables:  
  - **Protected attributes**, **outcomes**, **mediators**, **confounders**.  
- Sources: domain expertise, data analysis, literature.  

### Structural Equation Models (SEMs)
- Add quantitative structure to graphs.  
- Specify functional relationships + error terms.  
- Enable counterfactual analysis.  

### Validating Causal Models
- Test implied independencies.  
- Compare predictions with data.  
- Sensitivity analysis + domain expert review.  

### Domain Modeling Perspective
- **Data collection:** detect missing confounders.  
- **Feature engineering:** identify legitimate vs. proxy predictors.  
- **Model design:** constrain/disallow unfair paths.  
- **Evaluation & interventions:** causal models guide fairness metrics and corrective actions.  

---

## 3. Practical Considerations
### Implementation Framework
1. **Variable Identification** (PA, outcomes, mediators, confounders).  
2. **Causal Relationship Mapping** (domain knowledge, experts, literature, temporal order).  
3. **Formal Model Development** (DAG + SEMs, document assumptions).  
4. **Validation** (independencies, sensitivity, predictions vs. reality, expert review).  

### Challenges
- Limited domain knowledge → iterative, multi-expert, multiple candidate models.  
- Unobserved confounders → sensitivity analysis, proxy variables, transparency.  

---

## 4. Case Study: Loan Approval Algorithm
- **Problem:** Disparities in approval rates across racial groups.  
- **Findings:**  
  - 60% disparity via proxy (zip code).  
  - 25% via indirect (credit history, income).  
  - 15% via selection bias in training data.  
- **Solutions:**  
  - Remove proxy effect (zip code).  
  - Adjust for historical disparities in credit access.  
  - Rebalance training data.  
- **Lessons:** Different bias mechanisms need different interventions; causal models enable nuanced solutions.  

---

## 5. FAQs
- **Causal vs. Statistical models:** Causal models explain *why*, not just correlations; support counterfactual reasoning.  
- **Limited data:** Use domain expertise, qualitative inputs, causal discovery cautiously, candidate models, sensitivity analysis.  

---

## 6. Project Component Development (toward Unit 5)
- Deliverables:  
  - Variable identification templates.  
  - Causal graph construction methodology.  
  - SEM specification templates.  
  - Model validation protocols.  
- Integration: forms the structural base for Units 3–5 (counterfactual fairness & practical inference).  

---

## 7. Summary & Next Steps
- **Key Takeaways:**  
  - DAGs = explicit bias pathways.  
  - Systematic variable identification = foundation.  
  - SEMs = mathematical precision.  
  - Validation = prevent wrong interventions.  
- **Next Unit:** Counterfactual fairness (using these causal models).  

---

## References
- Pearl (2009) – *Causality*.  
- Kusner et al. (2017) – *Counterfactual Fairness*.  
- Loftus et al. (2018) – *Causal Reasoning for Algorithmic Fairness*.  
- Kilbertus et al. (2020) – *Sensitivity of Counterfactual Fairness*.  
- Plečko & Bareinboim (2022) – *Causal Fairness Analysis*.  
- Yang et al. (2020) – *Causal Intersectionality for Fair Ranking*.  
- Zhang & Bareinboim (2018) – *Causal Explanation Formula*.  
- Crenshaw (1989) – *Intersectionality*.  
