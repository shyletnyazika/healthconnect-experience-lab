# Week 6 Project Summary — Data Science Track

**AnalystLab Africa | Experience Lab Internship Programme | HealthConnect Clinic Project**
**Track:** Data Science | **Author:** Shylet Nyazika

---

**1. Planned for Week 6:** Analyse the Week 5 baseline's weaknesses through formal error analysis, resolve the flagged feature-redundancy question, develop and tune an improved model, and validate whether the result is fit for HealthConnect's use case.

**2. Actually completed:** Reproduced the Week 5 split and baseline exactly for a fair comparison; ran a structured error analysis on false positives/negatives and by appointment segment; resolved the `historical_no_show_rate` vs `previous_no_shows` redundancy with a direct isolation test; built and compared Random Forest and Gradient Boosting against the baseline; tuned Gradient Boosting via grid search; assessed the resulting model's suitability for real HealthConnect use; and completed cross-track integration with two Data Analytics contributors.

**3. What improved from Week 5:** Accuracy rose from 62.4% to 64.8% and ROC-AUC from 0.677 to 0.687 with the tuned Gradient Boosting candidate; the redundant feature flagged but unresolved in Week 5 is now resolved with evidence; the model is now compared against non-linear alternatives and has been through a hyperparameter search, both explicitly listed as Week 5 limitations.

**4. What was integrated:** Data Analytics' validated segment findings (no-show rate by appointment type, previous no-shows, booking lead time, and reminder status) were cross-checked against this track's model — corrected a misreading of the Specialist Consultation error pattern and independently confirmed the model's two strongest features.

**5. Track(s) collaborated with:** Data Analytics (two contributors).

**6. What was exchanged:** Received validated no-show rate breakdowns by segment and a lead-time/previous-no-show interaction finding; provided this track's feature importance ranking and error-analysis breakdown in return.

**7. What changed as a result:** Corrected the interpretation of Specialist Consultation's high model error rate — it is a modelling gap, not evidence the segment is inherently highest-risk, since Data Analytics' validated no-show rate for that segment (47.44%) is not the highest (Follow-up is, at 51.23%). Also added a new candidate interaction feature (`long_lead_time × has_previous_no_show`) to the Week 7 requirements, based on Data Analytics' compounding-effect finding.

**8. Key findings:** The model's main limitation is not the algorithm but the feature set — `booking_lead_days` dominates predictive power (57% of tuned-model importance), and 35.8% of appointments carry genuine, irreducible uncertainty given current data. Errors are also unevenly distributed across appointment types (31.2%–42.2%) — now understood, via cross-track input, to reflect an interaction effect rather than segment-level risk.

**9. Major challenges:** Tree-based models did not deliver as large a lift as expected from a change in model family alone, reinforcing that the ceiling here is largely feature-driven rather than algorithm-driven.

**10. Important decisions and why:** Dropped `previous_no_shows` in favour of `historical_no_show_rate` based on direct evidence rather than intuition; selected Tuned Gradient Boosting as the Week 6 candidate model over Random Forest based on across-the-board metric performance; corrected the Specialist Consultation interpretation based on Data Analytics' validated findings rather than assuming the model's error pattern reflected true segment risk.

**11. Remaining issues:** Model calibration and explainability (SHAP) still not formally assessed; the new interaction feature idea from Data Analytics not yet built or tested; single-clinic, single-snapshot dataset limits generalisability claims.

**12. Contribution to the overall HealthConnect project:** A validated, evidence-improved candidate model (`week6_candidate_model.pkl`) ready for ML Engineering to integrate into the pipeline, plus a documented feature-refinement decision, a corrected error-pattern interpretation, and a new candidate feature — all informed by direct cross-track validation with Data Analytics.

**13. Proposed focus for Week 7:**
1. Validate model calibration (reliability diagram / Brier score).
2. Run SHAP explainability on the tuned Gradient Boosting model.
3. Build and test the `long_lead_time × has_previous_no_show` interaction feature (from Data Analytics collaboration).
4. Stress-test the model on the 35.8% "coin-flip zone" segment.
5. Confirm the ML Engineering pipeline reproduces these exact metrics end-to-end.
6. Re-run the appointment_type segment analysis on the tuned model specifically, now that the Specialist Consultation pattern is understood as an interaction effect.
