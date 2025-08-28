# Part 3: Model-Level Interventions (In-Processing)

## Context
In-processing interventions embed fairness **directly into model training**, tackling bias that persists even after data-level fixes.  
Instead of adjusting inputs (pre-processing) or outputs (post-processing), this stage reshapes **how models learn**.  

Practitioners often treat fairness as an afterthought. Here, fairness becomes a **core optimization goal**, integrated into the loss function, constraints, and architecture itself.

- **Constraint-based methods** add fairness requirements into the optimization process.  
  *Example:* a hiring model trained with constraints to keep acceptance rates across groups balanced, while still leveraging valid predictors.  

- **Adversarial approaches** pit two networks against each other: a predictor learns the main task, while an adversary tries to infer protected attributes. The predictor is penalized when the adversary succeeds, forcing it to learn representations that are **useful but blind to sensitive features**.  

- **Regularization and multi-objective optimization** extend this further: loss functions can include fairness penalties, or optimization can explicitly search the trade-off frontier between fairness and accuracy.  

The **In-Processing Fairness Toolkit** (Unit 5) is the third component of the Playbook. It equips you with the methods to ensure fairness is intrinsic to your models—shaping how they train, not just how they behave after deployment.

---

## Learning Objectives
By the end of this Part, you will be able to:

- **Implement fairness constraints** in optimization objectives, so models satisfy fairness definitions natively rather than via post-hoc fixes.  
- **Design adversarial debiasing architectures** that remove protected information from learned representations while preserving predictive power.  
- **Apply fairness regularization terms** that steer training away from discriminatory solutions without imposing hard constraints.  
- **Develop multi-objective optimization strategies** to balance fairness and accuracy along the Pareto frontier.  
- **Adapt in-processing techniques across architectures**, from linear models to deep networks, ensuring fairness is achievable regardless of modeling choice.  
