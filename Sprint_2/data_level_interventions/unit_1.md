# Unit 1: Comprehensive Data Auditing

---

## 1. Conceptual Foundation and Relevance

### Guiding Questions
1. How do we systematically uncover and quantify bias patterns in training data before they propagate to machine learning models?  
2. What analytical frameworks enable us to distinguish between different types of data biases, and how can these insights guide appropriate pre-processing interventions?

### Conceptual Context
Before applying fairness interventions, we need to understand **how bias manifests in training data**. Comprehensive data auditing is the diagnostic foundation for fairness work—without it, interventions risk targeting symptoms rather than causes, or introducing new unfairness through misguided corrections.  

Data auditing goes beyond conventional quality checks, focusing on representation disparities, problematic correlations, label quality issues, and other bias patterns.  

This Unit builds on causal insights from Part 1 and translates them into **specific auditing methods** that guide which pre-processing interventions are appropriate. The methodologies here directly inform the **Pre-processing Strategy Selector** in Unit 5.

---

## 2. Key Concepts

### Multidimensional Representation Analysis
- Examines whether demographic groups are adequately represented.  
- Goes beyond univariate analysis to include **intersectional representation**.  
- Example: Adequate representation of women (48%) and people of color (30%) may still hide underrepresentation of women of color (9% vs expected 14.4%).  
- Inspired by *Gender Shades* (Buolamwini & Gebru, 2018).  

**Key steps:**  
- Compare dataset demographics to benchmarks (e.g., census).  
- Detect representation gaps across attributes and intersections.  
- Check representation across **outcome categories**.  
- Analyze shifts over time.  

---

### Correlation and Association Pattern Detection
- Focuses on how **protected attributes correlate with other features or outcomes**.  
- Important because correlations create pathways for proxy discrimination, even if attributes are excluded.  
- Example: In risk assessment data, "prior police contacts" correlate with race due to over-policing, enabling indirect discrimination.  

**Auditing involves:**  
- Checking correlations between protected attributes and labels.  
- Identifying proxies through higher-order associations.  
- Using advanced methods (mutual info, permutation importance, conditional independence).  

---

### Label Quality and Annotation Bias
- Labels can embed historical discrimination or annotator bias.  
- Example: Identical resumes rated lower with stereotypically female or non-white names (Bertrand & Mullainathan, 2004).  
- Annotation subjectivity can lead to systematic disparities.  

**Assessment includes:**  
- Analyzing label definitions and historical bias.  
- Checking inter-annotator agreement by group.  
- Validating against external benchmarks.  
- Counterfactual label tests (would outcome change if protected attribute changed?).  

---

### Fairness Metric Baseline Calculation
- Quantifies **initial fairness gaps** in raw training data.  
- Establishes benchmarks for intervention effectiveness.  
- Different metrics correspond to fairness definitions:  
  - Statistical parity (independence of outcome & attribute)  
  - Equal opportunity (equal TPR)  
  - Equalized odds (TPR + FPR parity)  

**Steps:**  
- Compute multiple fairness metrics.  
- Calculate confidence intervals.  
- Include intersections.  
- Prioritize most severe violations.  

---

### Domain Modeling Perspective
Comprehensive auditing maps onto ML components:  
- **Data collection**: how gathered, sampling biases?  
- **Feature distribution**: how features vary across groups.  
- **Label quality**: biases in labeling processes.  
- **Representation**: sufficient coverage of groups & intersections.  
- **Proxies**: features acting as stand-ins for protected attributes.  

---

### Conceptual Clarifications (Analogies)
- **Auditing = medical exam**: goes beyond temperature to scans, bloodwork → accurate diagnosis before treatment.  
- **Representation analysis = voter demographics**: underrepresentation can distort outcomes.  
- **Correlation detection = forensic accounting**: look for subtle patterns suggesting hidden unfairness.  

---

### Intersectionality Consideration
- Bias can manifest uniquely at intersections (Crenshaw, 1989).  
- Example: Gender Shades (Buolamwini & Gebru, 2018): <1% error for light-skinned men vs ~35% for dark-skinned women.  
- Requires explicit intersectional auditing for representation, correlations, labels, and fairness metrics.  

---

## 3. Practical Considerations

### Implementation Framework
1. **Initial profiling**: document data sources, collection, selection biases, protected attributes, proxies.  
2. **Representation analysis**: demographics vs benchmarks, intersections, outcomes, temporal trends.  
3. **Correlation detection**: correlation matrices, mutual info, conditional independence, visualization.  
4. **Label quality**: analyze historical bias, inter-annotator differences, validate externally.  
5. **Baseline metrics**: compute fairness metrics, statistical significance, prioritize by severity.  

### Implementation Challenges
- Missing protected attributes → use privacy-preserving methods, proxies, sensitivity analysis, or supplementary surveys.  
- Balancing thoroughness with practicality → staged approaches, prioritize high-risk areas, automate auditing workflows.  

### Evaluation Approach
- **Comprehensiveness:** check coverage of attributes, bias types, temporal aspects.  
- **Actionability:** ensure findings connect to interventions, metrics set clear priorities, and results are understandable to mixed audiences.  

---

## 4. Case Study: Employment Algorithm Bias Audit

**Scenario:**  
- Tech company auditing hiring algorithm dataset (50,000 resumes).  
- Stakeholders: HR, data scientists, compliance.  

**Findings:**  
- **Representation gaps**: women of color severely underrepresented (4% vs 18% benchmark).  
- **Correlations**:  
  - Gender ↔ programming languages (CS pipeline bias).  
  - Race ↔ prestigious universities.  
  - Resume language correlated with gender.  
- **Labels**:  
  - Male applicants 37% more likely to be hired than equally qualified women.  
  - Candidates from elite universities 45% more likely to be hired.  
- **Metrics**:  
  - 18pp demographic parity gap (gender).  
  - 12pp EO gap (race).  
  - 28pp gap for women of color vs white men.  

**Lessons:**  
- Intersectional gaps hidden in univariate checks.  
- Subtle linguistic proxies for gender.  
- Multiple mechanisms → multiple interventions needed.  

---

## 5. FAQs

**Q1: How to audit without protected attributes?**  
- Use aggregate/anonymized data, privacy-preserving computation, proxies with caveats, sensitivity analysis, or voluntary surveys.  

**Q2: How to prioritize under limited resources?**  
- Use risk-based approach (e.g., gender in hiring, race in lending).  
- Quick scans of fairness metrics.  
- Focus on **outcome disparities first**.  
- Prioritize historically marginalized intersections.  
- Automate & iterate progressively.  

---

## 6. Project Component Development

In Unit 5, you will build the **data auditing component** of the Pre-processing Strategy Selector. Deliverables:  

- **Representation analysis template**  
- **Correlation pattern framework**  
- **Label quality assessment**  
- **Baseline fairness metric calculators**  

Integration:  
- Provides diagnostic inputs for intervention selection.  
- Establishes evaluation metrics for interventions.  
- Enables communication of findings via documentation & visualization.  

---

## 7. Summary and Next Steps

**Key takeaways:**  
- Representation analysis must be intersectional.  
- Correlation analysis identifies proxy discrimination.  
- Label auditing addresses historical + annotator bias.  
- Baseline metrics quantify fairness gaps and set benchmarks.  

**Application:**  
- Document data sources, collection biases.  
- Start with demographics → add intersectional, correlation, label, and metric analysis.  
- Use multiple visualizations.  
- Connect findings directly to intervention strategies.  

**Looking ahead:**  
Next unit: **Reweighting and resampling techniques** to address representation disparities.  

---

## References
- Angwin, J., Larson, J., Mattu, S., & Kirchner, L. (2016). *Machine bias.* ProPublica.  
- Barocas, S., Hardt, M., & Narayanan, A. (2019). *Fairness and machine learning: Limitations and opportunities.* https://fairmlbook.org/  
- Bertrand, M., & Mullainathan, S. (2004). *Are Emily and Greg more employable than Lakisha and Jamal?* American Economic Review, 94(4), 991-1013.  
- Buolamwini, J., & Gebru, T. (2018). *Gender shades.* FAT* 2018.  
- Crenshaw, K. (1989). *Demarginalizing the intersection of race and sex.* Univ. of Chicago Legal Forum.  
- Gebru, T., et al. (2021). *Datasheets for datasets.* CACM, 64(12), 86-92.  
- Jacobs, A. Z., & Wallach, H. (2021). *Measurement and fairness.* FAT* 2021.  
