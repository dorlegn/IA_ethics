Got it! Here’s the improved **single markdown case study in English**, written in the past tense (what work was done, not “what we did”).

---

# Case Study — Emakunde **News-Bias Detector (NBD)**

*Integrated version of **Audit** + **Interventions**, with explanations for non-technical readers.*

---

## 0) Executive Summary

**What this is:** A system that analyzed Spanish and Basque digital news to detect and reduce representation bias (who appeared, how, and with what visibility).

**Main issue found:** Under-representation of women (especially intersectional groups), lower recognition of names with Basque morphology, and reduced visibility of women’s quotes in headlines.

**Work completed:**

1. Full audit (historical context, bias patterns, risk matrix, formal sign-off).
2. Clear fairness definitions established.
3. Technical interventions in **pre-processing**, **in-processing**, and **post-processing**.
4. Deployment of fairness metrics dashboard and governance plan.

**Measured impact:** Equal Opportunity gaps reduced to \~**0.01**, EU–ES recall gap narrowed to **−0.3 pp**, headline disparity for women’s quotes reduced by **\~71%**, with only **minor performance losses** (−1–2.3%).

> **For non-technical readers:** Imagine a “counter” that measures how often different groups appear in the news and how accurately the system recognizes them. There were imbalances; these were reduced without breaking the system’s usefulness.

---

## 1) Context and Scope

* **Sponsor:** Emakunde – Basque Institute for Women
* **Scope:** Digital media (2010–2024), Spanish and Basque language
* **Core ML task:** Detecting mentions of people and attributing quotes; measuring **share of voice (SOV)** and visibility by gender × ethnicity × language.
* **Regulation:** Basque Equality Act (2022) and Spanish Equality Law (LO 3/2007).

**Stakeholders & roles:**

* **Product Manager (PM):** Dorleta Urrutia Oñate (business priorities).
* **DS Lead:** Iñaki/Jon Garai (technical responsibility).
* **Domain SME:** Dr. Leire/Miren Urrutia/Etxezarreta (media & equality expertise).
* **Legal:** Itziar López (compliance and risks).

> **For non-technical readers:** The system was not deciding “who is right,” but rather **measuring and correcting imbalances** in representation.

---

## 2) Historical Audit

### 2.1 Artefacts produced

* `risk_ticket_emakunde.yaml` – scope, risks, timeline.
* `pattern_registry_emakunde.csv` – structured bias catalogue.
* `pattern_risk_matrix_emakunde.md` – severity × likelihood × relevance.
* SME interview notes in `/docs/support/`.

**Formal sign-off (15-07-2025):** PM, DS Lead, and SME approved.
Checklist covered: artefacts present, thresholds verified, intersectionality marked, open questions assigned.

> **For non-technical readers:** Before touching the model, the team **agreed on which biases existed, how severe they were, and what evidence supported them.**

### 2.2 Registry of patterns

* **PAT-001 (🔴 4.3):** Women underrepresented as sources in politics.
* **PAT-002 (🔴 4.0):** Stereotype framing (women as victims/domestic).
* **PAT-003 (🔴 4.4):** Afro-descendant women nearly invisible (intersectional).
* **PAT-004 (🟠 3.3):** Women 50+ severely underexposed on-screen.
* **PAT-005 (🟠 3.4):** LGBTQ+ coverage framed negatively (crime contexts).

**Outstanding gaps:** more 2024–2025 data for PAT-003; legal clarification for PAT-005.

### 2.3 Risk scoring recipe

Risk = 0.40·Severity + 0.30·Likelihood + 0.30·Relevance
Thresholds: 🔴 ≥4.0 · 🟠 3.0–3.9 · 🟡 2.0–2.9 · 🟢 <2.0

> **For non-technical readers:** The focus was placed first on issues that were **most harmful, most likely, and most relevant to the system.**

---

## 3) Fairness Definitions

* **Primary:** **Demographic Parity (DP)** — every group should have equal share of detected mentions.
* **Secondary:** **Equal Opportunity (EO)** — if someone truly should be detected, the system should succeed equally across groups.

**Rationale:** Top risks related to *visibility*. DP directly addressed presence/quotas; EO monitored recall gaps.

**Accepted trade-offs:**

* DP could increase false positives but improved recall for underrepresented groups.
* EO required reliable labels, feasible with Emakunde annotators.

> **For non-technical readers:** “Fair” here meant **two things**: (1) similar representation shares (DP), and (2) equal recognition performance (EO).

---

## 4) Bias Sources (“Eight doors”)

* **HB Historical:** past datasets inherit old newsroom slants.
* **RB Representation:** missing voices in datasets.
* **MB Measurement:** systematic errors (dialects, morphology).
* **AB Aggregation:** one global model ignoring section-specific context.
* **LB Learning:** optimizing clicks amplifies sensational content.
* **EB Evaluation:** test sets not representative.
* **FB Feedback:** outputs shape future data, reinforcing bias.
* **DB Deployment:** accessibility issues hiding alerts.

> **For non-technical readers:** Bias can creep in at many “doors” — not just the data, but also evaluation, editorial choices, or even the dashboard UI.

---

## 5) Causal Model and Critical Paths

**Key variables:**

* Protected: gender, ethnicity; Slice: language (EU/ES).
* Proxies/mediators: name morphology, topic/section, headline presence.
* Measurement: NER/Coref, knowledge base coverage.
* Outcomes: exposure (SOV), quote share.

**Problematic unfair paths (validated with counterfactuals):**

* Gender/Ethnicity → Name morphology → NER/Coref → KB → Exposure.
* Gender/Ethnicity → Language (EU/ES) → NER → Exposure.
* Gender/Ethnicity → Topic/Section → Exposure.
* Gender/Ethnicity → Headline presence → (Quotes, Exposure).

> **For non-technical readers:** Recognition was worse for Basque names, Basque-language articles, and quotes in body text vs headlines — systematically reducing women’s visibility.

---

## 6) Fairness Metrics

**Libraries:** `fairlearn`, `aequitas`.
**DP metrics:** positive rate difference, statistical parity ratio.
**EO metrics:** TPR difference, equal opportunity ratio.
**Intersectional analysis:** ON (gender × ethnicity, language as slice).

> **For non-technical readers:** Metrics checked both **representation** and **recall**, across all relevant groups.

---

## 7) Technical Interventions

### 7.1 Pre-Processing

* **Representation:** stratified resampling + \~4,000 counterfactual samples (gender/ethnicity swapped).
* **Proxy (names):** disparate impact removal + KB expansion with >1,200 Basque surnames.
* **Language (measurement):** weight factor 1.3 for Basque mentions + per-language calibration.
* **Editorial (headlines):** normalized weighting of headline vs body mentions.

**Results:**

* EU–ES TPR gap: **−3.5 pp → −0.8 pp**.
* Quote attribution disparity: **−62%**.
* Representation gap in politics/economy narrowed by **+7 pp**.
* Training cost +8%, inference latency unchanged.

---

### 7.2 In-Processing

* **Adversarial debiasing:** gradient reversal layer to suppress gender leakage.
* **Fairness regularization:** EO penalty at classification head (λ=0.3, Pareto frontier).

**Results:**

* Macro-F1: **0.86 → 0.84** (−2.3%).
* EO gap: **0.11 → 0.04** (−64%).
* EU–ES recall gap: **−3.5 pp → −1.0 pp** (−71%).
* Headline disparity: reduced by **55%**.
* Interpretability preserved (SHAP stable).

---

### 7.3 Post-Processing

* **Equalized Odds** + group-specific thresholds.
* **Platt scaling** per language; normalization of headline vs body quotes.

**Results:**

* Macro-F1: **0.84 → 0.83** (−1.2%).
* EO gap: **0.04 → 0.01**.
* EU–ES recall gap: **−1.0 pp → −0.3 pp**.
* Headline disparity: **−6.2 pp → −1.8 pp** (−71%).
* Small drop in precision for men (≈−1.5%).

---

## 8) Governance and Monitoring

* **Compliance:** versioned calibration thresholds, fairness dashboards, periodic SME review.
* **Dashboard:** DP and EO by gender × ethnicity × language, with drift alerts.
* **Intersectionality:** Bayesian pooling for rare groups, suppression of unstable cells, HITL routing.
* **Accessibility:** WCAG 2.1 AA audits on dashboard plugin.

> **For non-technical readers:** Fairness was not a one-time fix but a **continuous monitoring process** with governance and transparency.

---

## 9) Roadmap and Outstanding Work

* **New data (2024–2025) for PAT-003** (Afro-descendant women).
* **Legal clarification** on LGBTQ+ coverage framing (PAT-005).
* **Maintenance:** recalibration every 6 months; updates to KB of names; drift monitoring.

---

## 10) Key Results (at a glance)

* **EO gap (gender TPR):** 0.11 → **0.01**.
* **EU–ES recall gap:** −3.5 pp → **−0.3 pp**.
* **Headline disparity (women’s quotes):** reduced by **71%**.
* **Performance:** Macro-F1 from 0.86 → **0.83**, with interpretability intact.

---

## 11) Repo Structure

```
/emakunde_nbd/
  ├─ 01_historical/
  │   ├─ risk_ticket.yaml
  │   ├─ pattern_registry.csv
  │   ├─ pattern_risk_matrix.md
  │   └─ historical_signoff.md
  ├─ 02_definition/
  │   └─ definition_decision.yaml
  ├─ 03_bias_sources/
  │   ├─ bias_taxonomy_checklist.pdf
  │   └─ bias_priority_calculator.xlsx
  ├─ 04_metrics/
  │   ├─ metric_selector_tree.txt
  │   └─ metric_config.yaml
  ├─ interventions/
  │   ├─ preprocessing/
  │   ├─ inprocessing/
  │   └─ postprocessing/
  ├─ dashboards/
  └─ docs/support/
```

---

## 12) Glossary

* **DP (Demographic Parity):** equal proportion of positive outcomes per group.
* **EO (Equal Opportunity):** equal recall per group when they should be detected.
* **TPR/Recall:** share of actual positives correctly detected.
* **NER/Coref:** recognizing names and grouping mentions of the same person.
* **KB (Knowledge Base):** dictionary or catalogue used for recognition.
* **Platt scaling:** probability calibration method.
* **Equalized Odds:** post-processing adjustment to equalize true/false positive rates.

---

### TL;DR

* **Fairness defined** as equal representation (DP) + equal recall (EO).
* **Interventions applied** across pre-, in-, and post-processing.
* **Impact:** Large fairness gains, minimal performance loss.
* **Next:** expand intersectional data and maintain recalibrations.

---

Would you like me to also prepare a **shorter “non-technical summary” version** (like a 1-page executive brief with visuals), so you can share it with policy or NGO stakeholders?
