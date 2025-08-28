# Unit 2: Adversarial Debiasing Approaches  

---

## 1. Conceptual Foundation and Relevance  

### Guiding Questions  
- **Q1.** How can we leverage adversarial learning techniques to prevent models from encoding discriminatory patterns while preserving predictive performance?  
- **Q2.** What architectural and optimization principles enable effective implementation of adversarial debiasing across different model types and fairness definitions?  

### Conceptual Context  
Adversarial debiasing embeds fairness into model training through **competition between networks**:  
- A **predictor** learns the main task.  
- An **adversary** tries to infer protected attributes from the predictor’s outputs or representations.  

The predictor is penalized whenever the adversary succeeds. This creates a **minimax game** where the equilibrium is:  
- High predictive accuracy.  
- Low recoverability of protected attributes.  

Key benefits:  
- Works well with **complex models** (e.g., deep neural networks) where explicit constraints (Unit 1) are hard to apply.  
- Removes protected attribute information from **representations**, not just outputs.  
- Offers flexibility when data pre-processing or hard constraints are insufficient.  

---

## 2. Key Concepts  

### Adversarial Network Architecture for Fairness  
- Inspired by GANs.  
- Components:  
  - **Predictor** → learns target Y.  
  - **Adversary** → predicts protected attribute A from predictor outputs/representations.  
- Training objective:  
  \[
  \min_\theta \max_\phi L_\text{task}(\theta) - \lambda L_\text{adv}(\theta, \phi)
  \]  

**Zhang et al. (2018):** showed adversarial frameworks can enforce demographic parity, equalized odds, or equal opportunity.  
**Beutel et al. (2017):** highlighted how adversary placement (outputs vs. internal reps) changes fairness effects.  

---

### Fairness Through Adversarial Unlearning  
- Goal: create **“censored representations”** (Edwards & Storkey, 2016).  
- Predictor must encode information for Y but not for A.  
- Works across linear models, CNNs, RNNs, transformers → any differentiable architecture.  
- Key idea: fairness is achieved by **unlearning correlations** between A and Y.  

---

### Optimization Dynamics and Training Stability  
Adversarial training is elegant but **unstable**.  

Challenges:  
- Oscillation, mode collapse, non-convergence.  

Stabilization strategies:  
- **Balance predictor vs adversary capacity.**  
- **Gradient reversal layer (GRL):** multiplies gradients by −λ to pit predictor vs adversary.  
- **Progressive λ scheduling:** start small, increase gradually.  
- **Regularization:** spectral normalization, gradient penalties.  

**Madras et al. (2018):** showed stable training is key for achieving both fairness and predictive performance.  

---

### Domain Modeling Perspective  
Adversarial debiasing maps to:  
- **Model architecture** → predictor + adversary components.  
- **Loss function design** → combine primary and adversarial losses.  
- **Representation learning** → adversary pressure removes A-information.  
- **Optimization** → minimax dynamics need careful scheduling.  
- **Fairness evaluation** → must check leakage of protected attributes.  

---

### Intersectionality Consideration  
- Standard adversaries may miss intersectional patterns.  
- Solutions:  
  - Multi-task adversaries (predict multiple A’s).  
  - Adversaries trained on attribute combinations.  
  - Hierarchical adversarial structures.  
- **Subramanian et al. (2021):** showed intersection-aware adversaries improve fairness across overlapping subgroups.  

---

## 3. Practical Considerations  

### Implementation Framework  
1. **Architecture**  
   - Base predictor (task).  
   - Adversary with GRL connection.  
   - Placement: outputs, labels, or internal reps (depends on fairness definition).  

2. **Loss function**  
   - \(L = L_\text{primary} - \lambda L_\text{adversarial}\).  
   - Gradual λ schedule.  

3. **Training**  
   - Progressive λ increase.  
   - Alternating updates for predictor/adversary if needed.  
   - Early stopping based on fairness-performance combined metric.  

---

### Implementation Challenges  
- **Instability:** fix with gradient clipping, progressive λ, asymmetry in learning rates.  
- **Architecture balance:** adversary must be strong enough to detect A, but not overpower predictor.  

---

### Evaluation Approach  
- **Leakage testing:** train probes to predict A from outputs/representations.  
- **Fairness metrics:** DP, EO, intersectional parity.  
- **Pareto frontiers:** map trade-offs between fairness and accuracy.  

---

## 4. Case Study: Resume Screening System  

**Scenario Context**  
- Resume screening model with text embeddings.  
- Found bias: women scored lower despite equal qualifications.  
- Pre-processing failed, constraint methods infeasible.  

**Problem Analysis**  
- Gender correlated with: language patterns, employment gaps, education.  
- Intersectional bias: worse for women >40 and minority women.  

**Solution Implementation**  
- Added adversary predicting gender, age, ethnicity.  
- Connected adversary to both outputs and intermediate reps.  
- Loss: \(L = L_\text{primary} - \lambda L_\text{adv}\).  
- Progressive λ schedule (0.1 → 1.0).  

**Results**  
- Gender score gap reduced **87%** (vs 62% with pre-processing).  
- Preserved **92%** of predictive power.  
- Intersectional fairness improved (≥75% gap reduction).  

**Lessons**  
- **Architecture matters:** adversary placement is key.  
- **Progressive training:** stabilizes fairness-performance trade-off.  
- **Explicit intersectionality:** critical for real fairness.  

---

## 5. Frequently Asked Questions  

**Q1. When use adversarial vs. constraints?**  
- Use adversarial for **complex models** (neural nets, text, images).  
- Use constraints for **simple/convex models** with stronger guarantees.  

**Q2. How to stabilize training?**  
- Start with small λ and increase gradually.  
- Lower adversary learning rate (2–5× smaller).  
- Gradient clipping + spectral normalization.  
- Pretrain predictor before adversary.  

---

## 6. Project Component Development  

**Deliverable in Unit 5**:  
- **Architectural patterns** → templates for demographic parity, EO, representational fairness.  
- **Implementation guidance** → GRL, loss design, λ schedules.  
- **Selection criteria** → matrices comparing adversarial vs constraint/regularization.  

Integration:  
- Builds on Unit 1 (constraints).  
- Connects to Unit 3 (regularization).  
- Provides inputs for Unit 4 (multi-objective).  

---

## 7. Summary and Next Steps  

**Key Takeaways**  
- Adversarial debiasing = fairness through competition between predictor and adversary.  
- Protects internal representations → deeper fairness.  
- Requires careful optimization tuning.  
- Must explicitly account for intersectionality.  

**Looking Ahead**  
Next unit → **Regularization approaches**: fairness via penalty terms in loss, lighter than adversarial training but less expressive.  

---

## References  

- Beutel, A., Chen, J., Zhao, Z., & Chi, E. H. (2017). *Data decisions and theoretical implications when adversarially learning fair representations.* FAT/ML.  
- Crenshaw, K. (1989). *Demarginalizing the intersection of race and sex.* U. Chicago Legal Forum.  
- Edwards, H., & Storkey, A. (2016). *Censoring representations with an adversary.* ICLR.  
- Louppe, G., Kagan, M., & Cranmer, K. (2017). *Learning to pivot with adversarial networks.* NeurIPS.  
- Madras, D., Creager, E., Pitassi, T., & Zemel, R. (2018). *Learning adversarially fair and transferable representations.* ICML.  
- Subramanian, S., Chakraborty, S., & Slotta, J. (2021). *Fairness through adversarially learned debiasing.* AIES.  
- Zhang, B. H., Lemoine, B., & Mitchell, M. (2018). *Mitigating unwanted biases with adversarial learning.* AIES.  
