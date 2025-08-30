# Executive Brief — Emakunde News-Bias Detector (NBD)

**What it is:**  
A system that analyzed Basque and Spanish digital media (2010–2024) to detect **bias in representation** — who appears, how often, and with what visibility.

---

## Why it mattered
- Women, especially **intersectional groups** (Afro-descendant, older women, LGBTQ+), were under-represented.  
- Mentions with **Basque names** were recognized less accurately.  
- Women’s quotes were less likely to appear in **headlines**, reducing visibility.  

These gaps risked reinforcing stereotypes and **violating equality mandates** in the Basque Equality Act (2022).

---

## Work completed
1. **Audit** — Historical patterns documented and risk-scored.  
2. **Fairness definitions** —  
   - **Demographic Parity (DP):** equal share of representation.  
   - **Equal Opportunity (EO):** equal chance of being recognized.  
3. **Repairs applied at 3 levels:**  
   - **Pre-processing:** balanced datasets, added Basque surnames, weighted Basque texts.  
   - **In-processing:** fairness constraints inside model training.  
   - **Post-processing:** threshold adjustments and calibration for gender × language.  
4. **Governance:** fairness dashboard + recalibration plan every 6 months.

---

## Results (at a glance)
- **Equal Opportunity gap:** 0.11 → **0.01**  
- **Basque vs Spanish recall gap:** −3.5 pp → **−0.3 pp**  
- **Headline disparity for women’s quotes:** reduced by **71%**  
- **System accuracy:** only −3% relative decrease, still robust  

---

## What’s next
- Expand 2024–2025 data for **Afro-descendant women**.  
- Clarify legal risks on **LGBTQ+ media framing**.  
- Maintain **regular recalibrations** and update knowledge bases.  

---

### Key takeaway
The Emakunde NBD showed that **fairer media monitoring** is possible:  
✅ Representation gaps reduced  
✅ Accuracy preserved  
✅ Compliance with equality laws strengthened  

> This case demonstrates that **responsible AI** can support gender equality policies in practice.
