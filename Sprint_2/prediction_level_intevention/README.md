# Part 4: Prediction-Level Interventions (Post-Processing)

## Context
Post-processing interventions address fairness **after model training**, making them especially valuable for:
- Already deployed systems
- Legacy models that are costly or impossible to retrain
- Environments where retraining requires lengthy regulatory approval

Instead of modifying inputs or training, post-processing techniques **adjust model outputs** to satisfy fairness definitions.

Typical approaches include:
- **Threshold optimization** – Different decision thresholds per group to equalize outcomes (e.g., equal opportunity in loan approvals).  
- **Calibration** – Ensures predicted probabilities mean the same thing across groups.  
- **Score transformation** – Modifies raw scores to align with fairness definitions while preserving rank ordering.

These interventions connect directly to fairness criteria:
- Score transformation → **Demographic parity**  
- Threshold adjustment → **Equal opportunity**  
- Calibration → **Equalized odds**

## Why It Matters
Post-processing lets organizations **fix fairness issues without retraining**, which is crucial when:
- Models are already in production
- Retraining is too expensive
- Regulations slow down redeployment

It provides a **practical, low-friction pathway** to fairness improvements.

---

## Learning Objectives
By the end of this Part, you will be able to:

1. **Implement threshold optimization**  
   Find optimal group-specific thresholds to enforce fairness in classification.

2. **Design calibration techniques**  
   Equalize probability estimates so that predictions mean the same thing across groups.

3. **Apply score transformation methods**  
   Modify prediction scores to satisfy fairness constraints while preserving order.

4. **Evaluate trade-offs**  
   Compare the impact of post-processing techniques on fairness and predictive performance.

5. **Integrate into production**  
   Apply post-processing to deployed systems without disrupting workflows.

---

## Deliverables
For this Part, you will create the **Post-Processing Fairness Toolkit**, including:

- **Threshold Optimization Patterns** (Unit 1)  
- **Calibration Approaches** (Unit 2)  
- **Score Transformation Methods** (Unit 3)  
- **Evaluation Framework** for post-processing trade-offs (Unit 4)  
- **Case Study** applying post-processing to a real-world system (Unit 5)

This toolkit forms the **fourth component** of the **Fairness Intervention Playbook**.
