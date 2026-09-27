# Week 8 Project Closure Summary — Data Science Track

**AnalystLab Africa | Experience Lab Internship Programme | HealthConnect Clinic Project**
**Track:** Data Science | **Author:** Shylet Nyazika

---

**Final component:** Tuned Gradient Boosting Classifier for predicting patient appointment no-shows — Accuracy 64.8%, ROC-AUC 0.687, Brier score 0.2246. Trained, tuned, tested, calibrated, and confirmed explainable three independent ways.

**The journey, week by week:**
- **Week 5:** Established a Logistic Regression baseline (62.4% accuracy, ROC-AUC 0.677) with a patient-grouped train/test split, engineered features including `historical_no_show_rate`, `is_new_patient`, and `high_lead_time`.
- **Week 6:** Ran a formal error analysis; resolved a feature-redundancy issue flagged in Week 5 with direct evidence (`historical_no_show_rate` kept, `previous_no_shows` dropped); compared Logistic Regression, Random Forest, and Gradient Boosting; tuned the winner to reach 64.8% accuracy, ROC-AUC 0.687.
- **Week 7:** Tested the candidate model for overfitting (minimal — accuracy gap 0.0014, AUC gap 0.0293) and calibration (Brier score 0.2246, uneven at the extremes); tested two Data-Analytics-suggested interaction features and rejected both on evidence; confirmed explainability via permutation importance and SHAP, both agreeing with the model's built-in feature importances.
- **Week 8:** Consolidated all of the above into final model documentation, wrote a non-technical summary for stakeholders, and handed off the final model artefact and its requirements to ML Engineering for pipeline integration.

**Cross-track collaboration across the project:**
- **Data Analytics** (Fatimah Oreoluwa Ahmed and Victorea Ikhazuangbe) — a complete, closed-loop collaboration across Weeks 6–7: validated segment-level findings shaped feature selection and error-pattern interpretation, and two of their suggested interaction features were rigorously tested and honestly reported back as not improving the model. This stands as the final HC-POD integration for this submission.
- **ML Engineering** — a handoff message with the final model artefact and its technical requirements was sent this week. No reply was received before the submission deadline; this is documented honestly as an outstanding item rather than left unaddressed.

**Key modelling decisions, with reasoning:**
1. Dropped `previous_no_shows` in favour of `historical_no_show_rate` — tested both together and separately; combining them hurt performance.
2. Selected Gradient Boosting over Logistic Regression and Random Forest based on direct comparison, not assumption.
3. Rejected two teammate-suggested interaction features after testing — Gradient Boosting already captures these interactions internally through its tree structure, so explicit engineering added nothing measurable.

**What the model can be used for:** A triage/prioritisation signal — ranking patients by no-show risk to help clinic staff prioritise reminder calls and follow-up outreach.

**What it cannot be used for:** Automated, consequential decisions (e.g. auto-rebooking a slot) without human review — the error rate and the ~36% genuine-uncertainty zone make that unsuitable.

**Honestly documented limitations:**
- Calibration is uneven — overconfident at low predicted probabilities, underconfident at high ones.
- The Specialist Consultation appointment type has a persistently higher error rate (39–43%) that neither tested refinement explained or resolved.
- The dataset is a single-clinic, single-time-period snapshot — generalisability beyond it is untested.

**Biggest lesson from the project:** Rigorous testing sometimes means reporting that a promising idea didn't work. Two interaction features were tested this internship, and both were rejected — honestly, with evidence, and reported back to the teammates who suggested them. That discipline is as much a part of good data science as finding an improvement, and it's the part of this project I'm proudest of demonstrating.

**What I'd do differently with more time:** Bring in an additional data source (e.g. clinic staffing levels, local weather, or a longer historical window) — the current feature set appears to have a real predictive ceiling that further modelling alone can't push past, and Week 7's testing gave good evidence for exactly where that ceiling sits.
