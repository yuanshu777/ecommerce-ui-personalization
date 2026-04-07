# Analysis Design and Rationale

## 1. Metric Selection
Direct purchase data is unavailable in the dataset. Therefore, high-intent product interactions (`selectSize`, `miniCart`) are used as conversion proxies based on standard e-commerce user behavior patterns.

---

## 2. Control and Treatment Definition
The default UI (`visit_group = 'default'`) is treated as the control group. All non-default UI variants are treated as the treatment group in the initial analysis to maximize statistical power.

---

## 3. Statistical Testing
Two-proportion z-tests are used to assess whether observed differences in conversion rates are statistically significant. This aligns with standard A/B testing evaluation practices.

---

## 4. Modeling Strategy
Logistic regression serves as a baseline interpretable model. XGBoost is used to capture non-linear interactions and assess robustness of findings across modeling approaches.

Models are used to support decision-making rather than to automate predictions.

---

## 5. Sensitivity Analyses
Multiple sensitivity analyses are conducted to test robustness:
- Alternative conversion definitions
- Exclusion of low-quality sessions
- Temporal segmentation

---

## 6. Limitations
The data is observational and subject to selection bias. Results should be validated through randomized experiments before full rollout.

---

## 7. Product Implications
Findings inform UI personalization strategy and guide future experimentation design.
