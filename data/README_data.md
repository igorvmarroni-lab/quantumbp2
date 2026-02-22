# Data Access Instructions

All data used in this study are publicly available. No private or restricted datasets were used.

---

## 1. NHANES (2011–2020)

**Source:** CDC National Health and Nutrition Examination Survey  
**URL:** https://www.cdc.gov/nchs/nhanes/  
**N:** 8,965 participants  
**Used for:** Depression prevalence estimation with complex survey weighting

### Download
```bash
# Example: download PHQ-9 questionnaire data for 2017-2018 cycle
wget https://wwwn.cdc.gov/Nchs/Nhanes/2017-2018/DPQ_J.XPT -O data/nhanes/DPQ_J.XPT
```
Repeat for cycles: 2011–12, 2013–14, 2015–16, 2017–18, 2019–20.

### Key variables
| Variable | Description | Source |
|----------|-------------|--------|
| DPQ020–DPQ090 | PHQ-9 items | DPQ questionnaire |
| MDQ_* | Mood Disorder Questionnaire | (see codebook) |
| SEQN | Unique respondent ID | All files |

---

## 2. MEPS (2008–2019)

**Source:** Agency for Healthcare Research and Quality  
**URL:** https://meps.ahrq.gov/  
**N:** 84,653 person-years  
**Used for:** Longitudinal healthcare utilization, diagnoses, treatment identification

### Download
```bash
# Example: MEPS Panel 13 Full Year Consolidated File
wget https://meps.ahrq.gov/data_files/pufs/h163dta.zip -O data/meps/h163dta.zip
```

### Key variables
| Variable | Description |
|----------|-------------|
| ICD10CDX | ICD-10 diagnosis codes (F31.81, F31.89 for BD-II) |
| RXCLS | Drug therapeutic class codes |
| EVNTIDX | Event identifier (for linking) |
| PERWT* | Person-level weights |

---

## 3. State Policy Database

Mental health parity law implementation dates across 50 U.S. states (2008–2019).  
Used for Stepped-Wedge DiD instrument (Arm 3).

---

## Variable Definitions

See [`codebook.md`](codebook.md) for all derived variable definitions used in analysis.

### BD-II Conversion Algorithm
```
≥2 outpatient ICD-10 F31.81/F31.89 diagnoses
  (> 30 days apart, < 365 days apart)
AND mood stabilizer OR atypical antipsychotic prescription within ±60 days
```
**Validation:** Sensitivity 85%, Specificity 93%

### Major Depressive Episode
```
PHQ-9 ≥ 10 with MDQ-negative
OR PHQ-9 ≥ 15
OR PHQ-9 ≥ 10 with antidepressant prescription within 30 days
```

### Multicomponent Behavioral Intervention
```
≥6 psychotherapy sessions (CPT 90832 / 90834 / 90837)
with depression diagnosis within 90 days
```
