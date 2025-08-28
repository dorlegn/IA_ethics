# Part 3: Model-Level Interventions (In-Processing)

---

## Context  
In-processing interventions embed fairness directly into model training, addressing biases that persist despite data-level fixes.  
Rather than treating fairness as an afterthought, these techniques **reshape how models learn** by integrating fairness into optimization itself.  

- **Constraint-based methods** enforce fairness during training, guiding models toward decision boundaries that satisfy fairness criteria.  
- **Adversarial approaches** train predictors against discriminators that try to recover protected attributes, forcing the model to “unlearn” discriminatory signals.  
- **Regularization techniques** introduce fairness penalties as soft terms in the loss function, creating more flexible trade-offs.  
- **Multi-objective optimization** explicitly models fairness and performance as competing goals, allowing systematic exploration of the Pareto frontier.  

These interventions make fairness **intrinsic to the training process**—from loss formulation to hyperparameter selection and evaluation.  

---

## Learning Objectives  
By the end of this Part, you will be able to:  

- **Formulate fairness constraints** within optimization objectives to directly enforce criteria such as demographic parity or equalized odds.  
- **Design adversarial debiasing architectures** that prevent models from encoding protected attribute information while retaining predictive utility.  
- **Apply fairness regularizers** that penalize discriminatory outcomes, balancing fairness and accuracy via parameter tuning.  
- **Implement multi-objective optimization strategies** to systematically navigate fairness-performance trade-offs.  
- **Adapt interventions across architectures**, from linear classifiers to deep neural networks, ensuring fairness remains feasible regardless of model type.  

---

## Units Overview  

### **Unit 1: Fairness Objectives and Constraints**  
- Translates fairness definitions into **mathematical constraints** (e.g., demographic parity, equalized odds).  
- Uses **constrained optimization** and **Lagrangian methods** to enforce fairness during training.  
- Addresses feasibility and trade-offs, showing when constraints are achievable.  
- Introduces **intersectional fairness constraints** to protect subgroups beyond single attributes.  

---

### **Unit 2: Adversarial Debiasing Approaches**  
- Builds **adversarial networks** where a predictor competes against an adversary trying to infer protected attributes.  
- Implements **gradient reversal layers**, progressive training schedules, and stability mechanisms.  
- Ensures fairness via **adversarial unlearning**, filtering out discriminatory information in representations.  
- Extends to **intersectional adversaries** that protect overlapping demographic groups.  

---

### **Unit 3: Regularization for Fairness**  
- Introduces **fairness as penalty terms** in loss functions rather than strict constraints.  
- Enables smoother trade-offs with **regularization parameters (λ)** controlling fairness-performance balance.  
- Supports **group-specific and intersectional regularization** to address subgroup disparities.  
- Provides a flexible, stable alternative when constraints are too rigid or adversarial methods too complex.  

---

### **Unit 4: Multi-Objective Optimization**  
- Explicitly models fairness and performance as **separate objectives**.  
- Generates **Pareto frontiers** of trade-offs, highlighting optimal compromise solutions.  
- Implements **scalarization and ε-constraint methods** to explore trade-off spaces.  
- Uses **preference articulation frameworks** (a priori, a posteriori, interactive) for stakeholder-driven decision-making.  
- Extends to **intersectional fairness objectives**, scaling to multi-dimensional trade-offs.  

---

## Integration in the Toolkit  
This Part provides the **third component of the Fairness Intervention Playbook**:  
The **In-Processing Fairness Toolkit**, which:  

- Embeds fairness directly into training via constraints, adversaries, regularization, or multi-objective optimization.  
- Offers flexible techniques for diverse models and fairness goals.  
- Equips practitioners to select principled strategies for balancing fairness and performance.  

---

## Summary  
In-processing methods make fairness **a core optimization criterion** instead of a post-hoc adjustment.  
Together, Units 1–4 demonstrate how fairness can be:  

- **Constrained** (hard requirements)  
- **Unlearned** (adversarial protection)  
- **Penalized** (regularization)  
- **Balanced** (multi-objective trade-offs)  

This comprehensive approach ensures fairness is **intrinsic to model design** and responsive to real-world trade-offs.  

---

## Next Steps  
In **Part 4**, we will integrate **pre-processing, in-processing, and post-processing** into a unified **Fairness Intervention Playbook**, showing how to combine techniques across levels for robust, end-to-end fairness strategies.  
