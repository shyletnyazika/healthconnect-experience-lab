# Week 7 Project Summary — Data Science Track

**AnalystLab Africa | Experience Lab Internship Programme | HealthConnect Clinic Project**
**Track:** Data Science | **Author:** Shylet Nyazika

---

**1. What you planned to test:** Whether the Week 6 candidate model is overfitting, whether its predicted probabilities are well-calibrated, whether two Data-Analytics-suggested interaction features improve it, and whether the Week 6 accuracy/AUC gain over the baseline is meaningful or within normal variation.

**2. What you actually tested:** Reproduced the candidate model exactly; checked the train/test performance gap; computed calibration (Brier score and reliability curve); built and tested two separate interaction features (from Victorea and Fatimah on Data Analytics); re-ran error analysis across all three model versions; ran permutation importance and SHAP as explainability checks.

**3. The most important testing results:** The candidate model shows only mild overfitting (accuracy gap 0.0014, AUC gap 0.0293) and reasonably usable calibration (Brier score 0.2246), though it's overconfident at the low end and underconfident at the high end of predicted probability. The Week 6 improvement over the baseline (62.4%→64.8% accuracy, 0.677→0.687 AUC) is confirmed as real and consistent across every metric, not noise — though still modest given the model's inherent uncertainty ceiling.

**4. Issues or weaknesses identified:** The model is overconfident on its lowest-risk predictions and underconfident on its highest-risk predictions (calibration test); the Specialist Consultation error rate (39–43% depending on model version) did not improve with tuning and resisted two separate tested interaction features.

**5. Improvements/refinements made:** Tested two interaction features suggested by Data Analytics — Victorea's `long_lead_time × has_previous_no_show` and Fatimah's `specialist_consultation × high_lead_time`. Neither was kept: the first slightly decreased performance (64.8%→64.6% accuracy), and the second produced zero measurable change and zero feature importance. The Week 6 candidate model stands unmodified as the model going into Week 8.

**6. Retesting results:** Neither tested interaction feature improved the model — Victorea's slightly decreased performance, and Fatimah's produced no change at all. Both were rejected on evidence; the candidate model was reconfirmed as stable and unchanged.

**7. Which track(s) you collaborated with:** Data Analytics (Fatimah Oreoluwa Ahmed, primary this week; building on Victorea Ikhazuangbe's Week 6 contribution).

**8. What was tested collaboratively:** Whether Fatimah's validated appointment-type × booking-lead-time pattern (and, from Week 6, Victorea's lead-time × prior-no-show pattern) translate into model-level performance improvements.

**9. What changed as a result:** Both suggested interaction features were tested and rejected with clear evidence, giving Data Analytics a concrete answer instead of an assumption, and confirming that Gradient Boosting doesn't need hand-engineered interactions the way a linear model would. Fatimah is now reviewing her segment findings for anything more specific about the Specialist Consultation segment to support further testing before Week 8.

**10. Key findings/validation outcomes:** The candidate model shows only mild overfitting (accuracy gap 0.0014, AUC gap 0.0293 between train and test) and reasonably usable calibration (Brier score 0.2246), though it runs overconfident on its lowest-risk predictions and underconfident on its highest-risk ones. Both teammate-suggested interaction features were tested and rejected on evidence rather than assumption, and the Week 6 improvement over the baseline is confirmed as real and consistent across every metric — genuine, if still modest. The one validation outcome that remains open is the Specialist Consultation error rate, which resisted every fix tried this week.

**11. Major challenges encountered:** Interpreting the calibration curve's mixed overconfident/underconfident pattern required care rather than a single summary number; and reporting two negative refinement results honestly (rather than searching for a way to frame them as wins) took more discipline than reporting a straightforward improvement would have.

**12. Important decisions made:** To reject both tested interaction features based on evidence rather than adopting either on the strength of a teammate's suggestion alone; to document the Specialist Consultation gap as an open, unresolved limitation for Week 8 rather than forcing an untested fix; to treat the negative test results as legitimate, reportable findings rather than something to downplay.

**13. Remaining limitations:** Calibration is uneven across the probability range (most reliable in the middle, least at the extremes) and hasn't been corrected this week; the Specialist Consultation error-rate gap remains unresolved after two tested fixes; the ~36% "coin-flip" uncertainty zone identified in Week 6 persists.

**14. Remaining issues or dependencies:** Awaiting any further segment-level findings from Fatimah that might suggest a different angle on the Specialist Consultation pattern before Week 8.

**15. Your contribution to the overall HealthConnect project:** A rigorously tested, calibration-checked candidate model, validated as genuinely (if modestly) better than the Week 5 baseline, with two candidate refinements tested and honestly rejected rather than assumed to help — reducing the risk of ML Engineering integrating untested features, and giving Data Analytics concrete, evidence-based feedback on how their findings translate (and don't) at the model level.

**16. What must be completed before Week 8:** Decide how to present the unresolved Specialist Consultation gap in the final Week 8 presentation — as a documented, honestly-assessed limitation rather than a solved problem; incorporate anything further from Fatimah's segment review if it arrives in time.
