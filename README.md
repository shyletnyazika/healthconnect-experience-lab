# HealthConnect Experience Lab — Week 4 (Data Science Track)

**AnalystLab Africa — Experience Lab Internship Programme**

## Objective
Define the machine learning problem for predicting patient appointment no-shows at HealthConnect Clinic, and assess whether the provided appointment data can realistically support that goal. Week 4 is a foundation stage — no model is trained or deployed at this point.

## Business Context
HealthConnect Clinic experiences missed appointments (no-shows), which waste appointment slots and disrupt care. The central project question: *how can HealthConnect Clinic use data and AI to reduce missed appointments and improve the patient support experience?* This track's contribution is the Data Science / predictive modelling angle.

## Files in This Submission
| File | Description |
|---|---|
| `HealthConnect_Week4_Notebook.ipynb` | Data assessment, target definition, and initial modelling plan |
| `HealthConnect_Week4_ML_Problem_Definition.docx` | Full problem definition, data assessment, and modelling approach |
| `Week4_Project_Summary.docx` | Concise summary of Week 4 work and Week 5 focus |

## Proposed ML Task
Binary classification: predict `no_show_target` (1 = No-Show, 0 = Attended). Cancelled appointments (5.3% of data) are excluded from this first model, since a cancellation is a communicated decision rather than an unexplained absence.

## Key Findings
- 5,000 appointment records, 18 variables, no duplicates.
- Outcome split: No-Show 48.5%, Attended 46.3%, Cancelled 5.3%.
- `reminder_channel` missingness (27.3%) is structural — it corresponds exactly to appointments where no reminder was sent, not a data quality issue.
- No-show rate among non-cancelled appointments (~51.2%) is close to balanced, simplifying the initial classification approach.

## Key Risks Identified
- Possible data leakage via `waiting_time_minutes` (may only be known after the appointment).
- Repeated `patient_id` values across appointments — random train/test splitting risks patient-level leakage.

## Week 4 Status
This submission contains problem understanding, data assessment, and an initial modelling plan only. No model has been built, trained, or evaluated at this stage.

## Next Step (Week 5)
Reproducible data preparation, leakage confirmation, feature engineering (including a historical no-show rate feature), and baseline model development.

## About Me
Final-year Medical Analytics and Informatics student at the University of Zimbabwe, currently a Data Science Intern at AnalystLab Africa.

[Connect with me on LinkedIn](https://www.linkedin.com/in/shylet-nyazika-04585329b/)



## Week 5 — Data Preparation, Feature Engineering & Baseline Model

### Files
| File | Description |
|---|---|
| `HealthConnect_Week5_DataScience_Notebook.ipynb` | Data preparation, 4 exploratory visualizations, 3 engineered features, patient-grouped train/test split, baseline Logistic Regression model, full evaluation |
| `HealthConnect_Week5_Baseline_Modelling_Report.docx` | Full write-up of data prep, feature engineering, modelling approach, evaluation, and limitations |
| `Week5_Project_Summary.docx` | Concise summary of Week 5 work and Week 6 focus |

### Key Development
- **Resolved a Week 4 open question:** `waiting_time_minutes` was flagged as a possible data-leakage risk. Investigation confirmed it's populated regardless of appointment outcome (including for No-Shows), meaning it's a pre-appointment estimate, not a post-visit measurement — safe to use as a feature.
- **Patient-grouped train/test split:** confirmed zero patient overlap between training (3,771 rows) and test (966 rows) sets, preventing patient-level data leakage.
- **Baseline model:** Logistic Regression reached 62.4% accuracy and 0.677 ROC-AUC, meaningfully ahead of the 50% majority-class dummy baseline.
- **Strongest predictors:** `booking_lead_days` and `previous_no_shows` (both positive coefficients).
- **New issue flagged for Week 6:** `historical_no_show_rate` and `previous_appointments` show negative coefficients despite the closely related `previous_no_shows` being strongly positive — likely feature overlap/redundancy to resolve before finalizing the feature set.


### Next Step (Week 6)
Resolve the feature-overlap issue identified above, compare the Logistic Regression baseline against tree-based models (Random Forest, Gradient Boosting), and begin basic hyperparameter tuning.



## Week 6 — Model Improvement, Error Analysis & Validation

**Track:** Data Science
**Status:** Candidate model ready for ML Engineering integration

### What changed from Week 5
| | Week 5 | Week 6 |
|---|---|---|
| Model | Logistic Regression | Tuned Gradient Boosting |
| Accuracy | 62.4% | **64.8%** |
| ROC-AUC | 0.677 | **0.687** |
| Feature set | `historical_no_show_rate` + `previous_no_shows` (redundant) | `historical_no_show_rate` only, redundancy resolved with evidence (Part 3) |
| Model selection | No comparison performed | Random Forest + Gradient Boosting compared, then tuned via GridSearchCV |

### Files in this folder
| File | Description |
|---|---|
| `HealthConnect_Week6_DataScience_Notebook.ipynb` | Full notebook: baseline reproduction, error analysis, feature refinement, model comparison, tuning, business relevance, limitations |
| `Week6_Project_Summary.md` | Standalone project summary (submission requirement, separate from the notebook) |
| `week6_candidate_model.pkl` | Serialized candidate model artefact (tuned Gradient Boosting) + its feature column list, for ML Engineering to load directly |
| `requirements.txt` | Python dependencies to reproduce this notebook |
| `cross_track_integration_log.md` | Evidence of the Week 6 cross-track collaboration with Data Analytics |

### Reproducing this work
```bash
pip install -r requirements.txt
jupyter notebook HealthConnect_Week6_DataScience_Notebook.ipynb
```
Run top to bottom with `HealthConnect_Appointment_Data.csv` in the same folder. The Part 1 reproduction cell should print `Accuracy: 0.6242` and `ROC-AUC: 0.6767` before any Week 6 result is trusted — if it doesn't match, something differs in the environment.

### Loading the candidate model elsewhere (for ML Engineering)
```python
import joblib
bundle = joblib.load("week6_candidate_model.pkl")
model = bundle["model"]
feature_columns = bundle["feature_columns"]   # column order the model expects after get_dummies
# align a new dataframe to feature_columns with .reindex(columns=feature_columns, fill_value=0) before predicting
```

### Known limitations (see notebook Part 9 for full detail)
- Model calibration and SHAP-based explainability not yet assessed — Week 7.
- ~36% of predictions fall in a genuine 0.4–0.6 "uncertain" probability zone — a feature-set ceiling, not a tuning problem.
- Error rate varies by `appointment_type` (31.2%–42.2%) — not yet investigated at the feature level.

- <!-- Paste this section into your existing README.md, under your Week 6 section -->

## Week 7 — Model Testing, Refinement & End-to-End Validation

**Track:** Data Science
**Status:** Candidate model tested and confirmed unchanged going into Week 8

### What this week established
| Test | Result |
|---|---|
| Reproduction of Week 6 candidate | Exact match (Acc 0.6480, AUC 0.6872) |
| Overfitting check | Minimal — Acc gap 0.0014, AUC gap 0.0293 |
| Calibration | Brier score 0.2246 — reliable in the mid-range, drifts at the extremes |
| Interaction feature (Victorea, DA) | Tested, **rejected** — slightly decreased performance |
| Interaction feature (Fatimah, DA) | Tested, **rejected** — zero measurable effect |
| Is the Week 6 gain over baseline meaningful? | Yes — consistent across every metric, not noise |
| Specialist Consultation error gap | **Still open** — neither tested fix resolved it |

### Files in this folder
| File | Description |
|---|---|
| `HealthConnect_Week7_DataScience_Notebook.ipynb` | Full notebook: reproduction, overfitting check, calibration, two interaction-feature tests, explainability (permutation importance + SHAP), and cross-track testing evidence |
| `Week7_Project_Summary.md` | Standalone project summary (submission requirement, separate from the notebook) |
| `Week7_Testing_Validation_Record.md` | Structured test-by-test record (component, objective, expected/actual result, pass/fail, action taken) |
| `Week7_HC-POD_Cross-Track_Testing_Log.md` | Full documentation of the Data Analytics testing exchange (Fatimah Oreoluwa Ahmed) |
| `week7_candidate_model.pkl` | The model artefact — unchanged from Week 6, since both tested refinements were rejected |
| `requirements.txt` | Python dependencies (adds `shap` for explainability testing) |
| `evidence/` | Screenshots of the Data Analytics Slack exchange, calibration curve, and SHAP plot |

### Reproducing this work
```bash
pip install -r requirements.txt
jupyter notebook HealthConnect_Week7_DataScience_Notebook.ipynb
```
Run top to bottom with `HealthConnect_Appointment_Data.csv` in the same folder. Part 1's reproduction cell should print `Acc=0.6480, AUC=0.6872` before any other Week 7 result is trusted.

### Loading the model (unchanged from Week 6)
```python
import joblib
bundle = joblib.load("week7_candidate_model.pkl")
model = bundle["model"]
feature_columns = bundle["feature_columns"]
# bundle["week7_note"] explains why this is identical to the Week 6 artefact
```

### Known limitations carried into Week 8 (see notebook for full detail)
- Calibration is uneven — overconfident at low predicted probabilities, underconfident at high ones.
- The Specialist Consultation segment's elevated error rate (39–43%) remains unexplained after two tested interaction features.
- The ~36% "coin-flip" uncertainty zone identified in Week 6 persists — a feature-set ceiling, not a tuning problem.
