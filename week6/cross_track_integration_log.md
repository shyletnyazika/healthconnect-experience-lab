# Cross-Track Integration Log — Week 6

**Data Science ↔ Data Analytics**

Evidence record for the Week 6 mandatory cross-track integration requirement (Section 9 of the assignment brief). This log documents an actual exchange and the resulting change to the Data Science deliverable — not just communication.

---

## Integration Point (planned before the exchange)
- **Track collaborated with:** Data Analytics (Fatimah Oreoluwa Ahmed and Victorea Ikhazuangbe)
- **Project dependency:** Data Analytics' validated segment-level findings could confirm or challenge the Data Science model's feature importances and explain a specific error pattern found in the model.
- **Integration objective:** Determine whether the Specialist Consultation appointment type's high *model error rate* (42.2%, found in Part 2 error analysis) reflects a genuine data pattern or a modelling gap, and identify any candidate features for Week 7.

## Exchange Record

| Date | What I asked for | What I received | What I provided |
|---|---|---|---|
| Week 6 | Validated segment findings on appointment type, previous no-shows, booking lead time, and reminder status | **From Fatimah Oreoluwa Ahmed:** No-show rate by appointment type (Diagnostic Test 49.75%, Follow-up 51.23%, General Consultation 46.64%, Specialist Consultation 47.44%); no-show rate by previous-no-show count (43.51% → 67.95% from 0 to 3 prior no-shows); no-show rate by booking lead time (29.01% at 0–9 days → 67.92% at 50–59 days); reminder gap (51.39% without vs 47.36% with, a 4.03pp gap) | My model's feature importance ranking and error-analysis breakdown (Part 5 of the Week 6 notebook) |
| Week 6 | General collaboration (no specific ask) | **From Victorea Ikhazuangbe:** Overall no-show rate 48.5%, rising to 60.5% for 30+ day lead times; a compounding effect where long lead time (30+ days) combined with a prior no-show reaches 67.9% no-show rate, vs 55.2% for long lead time alone | Acknowledged the interaction finding and flagged it as a Week 7 candidate feature (see Outcome below) |

## Outcome

**What changed as a result:**
1. **Corrected a misreading in my own error analysis.** I had been treating Specialist Consultation's highest *model error rate* (42.2%) as if it implied the segment was inherently the highest-risk group. Fatimah Oreoluwa Ahmed's validated findings show Specialist Consultation does **not** have the highest no-show rate (47.44%, vs 51.23% for Follow-up) — meaning the model's error there is a modelling gap, not a reflection of segment risk. This is now corrected in the notebook's Part 9 limitations (previously read as an open question; now explained).
2. **Independent confirmation of the model's top two features.** Fatimah Oreoluwa Ahmed's booking-lead-time trend (29% → 68% no-show rate) and previous-no-show trend (43.5% → 68%) closely track the tuned model's two strongest features (`booking_lead_days` at 57% importance, `historical_no_show_rate` at 12%) — this is now noted in Part 5's interpretation as external validation, not just an internal metric.
3. **New candidate feature added to Week 7 requirements.** Victorea Ikhazuangbe's finding that lead time and previous-no-show history compound (67.9% vs 55.2% no-show rate) suggests an explicit interaction feature (e.g. `long_lead_time × has_previous_no_show`) could capture signal the model currently treats as two independent features. Added as a new Week 7 testing/feature requirement, credited to Victorea Ikhazuangbe.

**Evidence attached/linked:** Slack thread with Fatimah Oreoluwa Ahmed and Victorea Ikhazuangbe (Week 6 coordination channel), screenshotted and archived in `/evidence/week6_data_analytics_exchange.png`. *[Replace with your actual saved screenshot/export path once filed.]*

---

