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
- Standard practice: one threshold (e.g., 0
