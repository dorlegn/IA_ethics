# Unit 1: Threshold Optimization Techniques

## 1. Conceptual Foundation and Relevance

### Guiding Questions
- **Q1:** How can we adjust classification thresholds after model training to satisfy specific fairness definitions without requiring retraining or model modification?  
- **Q2:** What are the mathematical relationships between threshold selection and different fairness metrics, and how do we navigate the inherent trade-offs between them?  

### Conceptual Context
Threshold optimization is one of the most accessible and powerful fairness interventions.  
Instead of retraining or modifying models, it **works directly on model outputs**, making it ideal for:
- Black-box models  
- Legacy systems  
- Environments where retraining is impractical or costly  

**Key insight**: Using the same threshold for all groups often perpetuates disparities.  
Group-specific thresholds can satisfy fairness criteria such as **equal opportunity** or **equalized odds**, as shown in Hardt et al. (2016).  

This approach:
- Builds on **causal insights** (Part 1)  
- Complements **pre-processing** (Part 2) and **in-processing** (Part 3)  
- Prepares the ground for the **Post-processing Calibration Guide** in Unit 5  

---

## 2. Key Concepts

### Decision Boundaries and Thresholds
- Standard practice: one threshold (e.g., 0.5) for all.  
- Problem: groups often have different score distributions → unequal error rates.  
- Solution: group-specific thresholds to directly target fairness metrics.

### Mathematical Optimization for Fairness
- **Equal Opportunity:** thresholds equalize true positive rates across groups.  
- **Equalized Odds:** thresholds equalize both TPR and FPR.  
- **Demographic Parity:** thresholds equalize selection rates.  

These are formalized as **constraint optimization problems**, balancing fairness and performance.

### ROC Curves and Trade-offs
- ROC curves show TPR/FPR trade-offs.  
- Different groups → different ROC curves.  
- Fairness = navigating trade-offs between accuracy and fairness (no perfect solution).  

### Implementation With/Without Protected Attributes
- **With protected attributes:** direct group-specific thresholds.  
- **Without protected attributes:**  
  - Derived feature approaches (Dwork et al. 2018)  
  - Multiple-threshold schemes (Lipton et al. 2018)  

### Intersectionality
- Threshold optimization must address **intersections of multiple identities**, not just single attributes (Buolamwini & Gebru 2018).  
- Requires multi-dimensional thresholding and monitoring of smaller subgroups.

---

## 3. Practical Considerations

### Implementation Framework
1. **Fairness Criteria Selection** – choose fairness definition (DP, EO, EOds).  
2. **Threshold Calculation** – compute group-specific thresholds.  
3. **Trade-off Analysis** – measure fairness vs. accuracy frontier.  
4. **Deployment Strategy** – implement directly or via proxies depending on legality.  

### Implementation Challenges
- **Legal constraints**: use of protected attributes may be restricted.  
- **Stability**: thresholds may drift with data distributions.  
- **Monitoring**: requires recalibration over time.  

### Resource Requirements
- Validation data with protected attributes.  
- Statistical expertise.  
- Monitoring infrastructure.  

---

## 4. Case Study: Loan Application System

### Scenario Context
- Model: predicts loan default risk.  
- Threshold at 0.5 applied to all applicants.  
- Disparity: TPR = 85% (advantaged group), 70% (disadvantaged group).  

**Stakeholders**:  
- Risk managers (accuracy)  
- Compliance officers (regulatory fairness)  
- Business leaders (profitability)  

### Problem Analysis
- **Fairness Definition**: Equal Opportunity (qualified applicants should have equal approval rates).  
- **ROC Analysis**: single threshold produces unequal error rates.  
- **Trade-off**: equalizing TPR → 3% profit reduction but major fairness gain.  
- **Constraint**: cannot explicitly use race at decision time.  

### Solution Implementation
- **Thresholds**:  
  - Advantaged group: 0.65  
  - Disadvantaged group: 0.45  
  - TPR equalized ~80% across groups.  
- **Proxy-based approach**: derived permissible features to avoid using protected attributes directly.  
- **Monitoring**: periodic recalibration + intersectional fairness checks.  

### Outcomes
- Disparity reduced by 80% (15pp → 3pp gap).  
- Profit impact: −1.8% (less than expected).  
- Improved fairness for intersections (e.g., young disadvantaged applicants).  
- Challenges: proxy legality, threshold drift, stakeholder communication.  

---

## 5. Frequently Asked Questions (FAQ)

**Q1. Doesn’t using different thresholds violate equal treatment?**  
A: One rule for all looks equal but creates unfair outcomes when groups differ systematically. Group-specific thresholds correct for structural inequities, aiming for equal **impact**, not just equal **procedure**.

**Q2. How to implement without protected attributes?**  
A: Use **derived features**, **multi-threshold schemes**, or **adversarially fair score transformations**. These capture fairness benefits without explicit group membership.

---

## 6. Project Component Development

In Unit 5, you will develop a **Threshold Optimization Guide**, including:  
- Algorithms for calculating optimal thresholds.  
- Trade-off visualization templates.  
- Proxy-based and direct implementation approaches.  
- Monitoring and recalibration strategies.  

---

## 7. Summary and Next Steps

### Key Takeaways
- Threshold optimization = simple yet powerful post-processing tool.  
- It improves fairness **without retraining**, ideal for production systems.  
- Requires navigating trade-offs and documenting rationale.  
- Can be implemented with or without protected attributes.  

### Next
Unit 2 will explore **Calibration**, ensuring probability estimates have consistent meaning across groups, complementing threshold adjustments.  

---

## References
- Buolamwini, J., & Gebru, T. (2018). *Gender Shades.* FAT*.  
- Corbett-Davies, S. et al. (2017). *Algorithmic decision making and the cost of fairness.* KDD.  
- Dwork, C. et al. (2018). *Decoupled classifiers for group-fair ML.* FAT*.  
- Friedler, S. et al. (2019). *A comparative study of fairness interventions.* FAT*.  
- Hardt, M., Price, E., & Srebro, N. (2016). *Equality of Opportunity in Supervised Learning.* NeurIPS.  
- Kleinberg, J., Mullainathan, S., & Raghavan, M. (2016). *Inherent trade-offs in the fair determination of risk scores.* ITCS.  
- Lipton, Z. C. et al. (2018). *Detecting and correcting for label shift with black box predictors.* ICML.  
