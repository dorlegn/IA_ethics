# Part 2: Data-Level Interventions (Pre-Processing) — Intro Summary

## Context  
This part focuses on fixing unfairness **at the data stage**, before it propagates into models. Instead of treating datasets as fixed, you’ll learn to **reweight, transform, and augment data** so that training inputs better reflect fairness goals.  

- **Reweighting**: adjust sample importance to counter historical underrepresentation (e.g., give more weight to groups that were excluded in lending data).  
- **Transformations**: modify features to break unfair correlations (e.g., zip code as a race proxy in housing) while keeping predictive utility.  
- **Data augmentation**: generate synthetic samples for underrepresented groups, improving balance and robustness.  

These techniques span the whole ML pipeline—from identifying representation gaps in EDA to validating whether interventions improve fairness without losing predictive power.  

The **Pre-Processing Fairness Toolkit (Unit 5)** will help you apply these methods systematically, ensuring fairer training data from the start.  

---

## Learning Objectives  
By the end of this part, you will be able to:  

1. Detect and quantify data disparities across groups.  
2. Apply reweighting methods (frequency-based → distribution matching).  
3. Transform features to reduce proxy discrimination.  
4. Use fairness-aware augmentation to enrich underrepresented groups.  
5. Evaluate trade-offs between fairness gains and predictive accuracy.  
