# SYSTEMATIC-REVIEW SCREENING — Stroke Risk Prediction (Statistical Models → Traditional ML → Agentic AI)

REVISED criteria (2026-06-24).

Screen each record against five PICOS gates. A study must **PASS ALL FIVE** gates
to be **INCLUDED**; failing **ANY** single gate means **EXCLUDE**.

---

## Gate 1 — POPULATION (loosened)
The ONLY population exclusions are:
- (a) pediatric-only cohorts, and
- (b) animal studies.

Everything else PASSES population. The following are NOT population-based
exclusions: stroke survivors, recurrent-stroke cohorts, mixed cohorts with prior
stroke, lack of a stroke-free baseline, "not first-ever". DO NOT exclude on
population for any of those.

## Gate 2 — INTERVENTION / INDEX SYSTEM
INCLUDE any model for stroke RISK PREDICTION. Both AI/ML systems AND conventional
statistical models are eligible — machine learning, deep learning, agentic AI,
plain Cox regression, logistic regression, and C-statistic / regression-augmented
clinical risk scores (e.g. CHA2DS2-VASc) all PASS Gate 2.

EXCLUDE systems used ONLY for: acute stroke detection, triage, segmentation,
treatment/therapy selection, rehabilitation, or POST-STROKE PROGNOSIS. Post-stroke
prognosis and acute-treatment models FAIL Gate 2.

## Gate 3 — COMPARATOR
Cannot exclude on its own. Mark Pass unless a comparator issue independently
violates another gate.

## Gate 4 — OUTCOME
INCLUDE ISCHEMIC stroke as a primary or clearly extractable outcome — first-ever,
incident, or recurrent (the "first-ever" requirement does NOT apply).

EXCLUDE: hemorrhagic-only; composite CVD with no extractable stroke; a NON-stroke
outcome (AF, heart failure, diabetes, DVT, cognitive impairment, CKD/AKI,
other-cause mortality); acute stroke DIAGNOSIS/classification of an
already-occurred stroke; POST-STROKE functional outcome / disability / mRS /
recovery / complication. If the only stroke signal is an INPUT predictor (not the
outcome), Gate 4 FAILS.

## Gate 5 — STUDY
INCLUDE original peer-reviewed research, a preprint with methodology, or a
conference paper with validation; English; 2015 or later.

EXCLUDE reviews, editorials, viewpoints, protocols, commentaries (→ Background),
or studies with no validation / unclear methodology.

---

## DECISION
INCLUDE / EXCLUDE / UNCLEAR.
- With full-text PDF: resolve to a binary INCLUDE or EXCLUDE.
- Without PDF (title/abstract only): UNCLEAR is permitted when a gate cannot be
  judged from the available text.
- The first failing gate determines EXCLUDE; cite it in the reason.

## OUTPUT FORMAT
Write results to a JSON file: a JSON array with one object per screened record,
each containing exactly these fields:

```json
[
  {
    "PMID": "string — PubMed ID, or null if unavailable",
    "Filename": "string — source PDF/record filename",
    "Model name": "string — screening model/agent used",
    "Decision": "INCLUDE | EXCLUDE | UNCLEAR",
    "Reason": "string — concise rationale tied to the deciding gate(s)",
    "Section": "Include | Exclude | Background | Unclear",
    "PICOS Pass or Fail and Reason": {
      "Population": "Pass | Fail — reason",
      "Intervention": "Pass | Fail — reason",
      "Comparator": "Pass | Fail — reason",
      "Outcome": "Pass | Fail — reason",
      "Study": "Pass | Fail — reason"
    },
    "Runtime": "string — processing time for this record (e.g. \"3.2s\")"
  }
]
```
