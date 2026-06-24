# SYSTEMATIC-REVIEW SCREENING — Stroke Prediction (Traditional ML → Agentic AI)

REVISED criteria (2026-06-24).

Pass ALL FIVE gates to **INCLUDE**; fail ANY one to **EXCLUDE**.

## Gate 1 — POPULATION (revised / loosened)
The ONLY population exclusions are (a) pediatric-only cohorts and (b) animal
studies. Everything else PASSES population. Specifically, the following are NO
LONGER population-based exclusions: stroke survivors, recurrent-stroke cohorts,
mixed cohorts with prior stroke, lack of a stroke-free baseline, "not
first-ever". DO NOT exclude on population for any of those.

## Gate 2 — INTERVENTION / INDEX SYSTEM
INCLUDE only a genuine AI/ML system for stroke RISK PREDICTION. Conventional
statistical models (plain Cox regression, logistic regression, C-statistic /
regression-augmented clinical scores like CHA2DS2-VASc) are NOT eligible and
FAIL Gate 2. EXCLUDE systems used ONLY for: acute stroke detection, triage,
segmentation, treatment/therapy selection, rehabilitation, or POST-STROKE
PROGNOSIS. Post-stroke prognosis and acute-treatment models FAIL Gate 2 even
though population is loosened.

## Gate 3 — COMPARATOR
Cannot exclude on its own.

## Gate 4 — OUTCOME
INCLUDE ISCHEMIC stroke as a primary or clearly extractable outcome (first-ever,
incident, or recurrent — the "first-ever" requirement no longer applies).
EXCLUDE: hemorrhagic-only; composite CVD with no
extractable stroke; a NON-stroke outcome (AF, heart failure, diabetes, DVT,
cognitive impairment, CKD/AKI, other-cause mortality); acute stroke
DIAGNOSIS/classification of already-occurred stroke; POST-STROKE functional
outcome/disability/mRS/recovery/complication. If the only stroke signal is an
input predictor (not the outcome), Gate 4 FAILS.

## Gate 5 — STUDY
INCLUDE original peer-reviewed research / preprint with methodology /
conference paper with validation; English; 2015+. EXCLUDE
reviews/editorials/viewpoints/protocols/commentaries (→ Background), or no
validation/unclear.

## DECISION
INCLUDE / EXCLUDE / UNCLEAR (with PDF, resolve to binary; without PDF, UNCLEAR
allowed).

## OUTPUT FORMAT
Write results to a JSON file. The file is a JSON array; emit one object per
screened record with exactly these fields:

```json
[
  {
    "PMID": "string — PubMed ID, or null if unavailable",
    "Filename": "string — source PDF/record filename",
    "Model name": "string — screening model/agent used",
    "Decision": "INCLUDE | EXCLUDE | UNCLEAR",
    "Reason": "string — concise rationale for the decision",
    "Section": "string — Include | Exclude | Background | Unclear",
    "PICOS Pass or Fail and Reason": {
      "Population": "Pass | Fail — reason",
      "Intervention": "Pass | Fail — reason",
      "Comparator": "Pass | Fail — reason",
      "Outcome": "Pass | Fail — reason",
      "Study": "Pass | Fail — reason"
    },
    "Runtime": "string — processing time (e.g. seconds) for this record"
  }
]
```
