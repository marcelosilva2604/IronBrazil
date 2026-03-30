# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Development Setup

```bash
# Activate existing virtual environment
source .venv/bin/activate

# Or create from scratch (requires Python 3.12)
python3.12 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

## Running Scripts

Scripts are numbered and run sequentially. Each depends on output from the previous phase:
```bash
python 01_data_prep.py
python 02_table1.py
python 03_primary_analysis.py
python 04_interactions.py
python 05_sensitivity.py
python 06_figures.py
```

Scripts do not exist yet — they will be created as the analysis progresses.

---

# Iron Supplementation Project — ENANI-2019

## What This Project Is

Cross-sectional analysis evaluating whether Brazil's universal iron supplementation programme (PNSF) is associated with infectious morbidity, systemic inflammation, and micronutrient competition in infants — and whether breastfeeding (via lactoferrin) protects against potential harms.

**Target journal:** Lancet Global Health (1st submission) > BMJ Global Health / AJCN (fallback)

## Why This Matters

All evidence of iron supplementation harm in children comes from Africa (Sazawal 2006/Lancet — Pemba trial stopped early due to 12% increase in hospitalizations/deaths; Jaeggi 2014/Gut — iron increases gut pathogens and inflammation in Kenyan infants; Zimmermann 2010/AJCN — iron fortification produces pathogenic gut microbiota in Ivorian children). No study has evaluated this in Latin America. Brazil's PNSF provides universal prophylactic iron (1mg/kg/day) to ALL children 6-24 months regardless of iron status — the same universal approach that caused harm in Pemba. This is NOT targeted supplementation; confounding by indication is minimal.

## Dataset

- **Source:** ENANI-2019 (Estudo Nacional de Alimentacao e Nutricao Infantil) — nationally representative survey
- **File:** `data_crianca_calib_anon.csv` (14,557 children, 741 columns)
- **Dictionaries:** `features_enani.txt` (text) and `4-Dicionario-ENANI-2019 (1).xlsx` (Excel)
- **Encoding:** Categorical variables are in Portuguese text ("Sim"/"Nao"), NOT numeric
- **Survey design:** 52 strata (`estrato_sel_anon`), 1,087 PSUs (`id_upa_anon`), calibrated weights (`peso_crianca_calib` + biomarker-specific weights)
- **All biomarker variables and weights are already in the main CSV.** No merge needed with biomarker files.

## Study Population

Two age groups, analyzed separately AND combined:
- **Group 1 (6-11 months):** ~2,100 children. Iron just introduced (PNSF starts at 6m). High breastfeeding rates. Temporal coherence is strongest: "iron in last 6 months" covers essentially their entire post-complementary feeding life.
- **Group 2 (12-17 months):** ~2,200 children. Iron used longer (up to 12 months exposure). Lower breastfeeding. Natural contrast for lactoferrin hypothesis.
- **18-23 months:** Excluded from main analysis (temporal window too loose, breastfeeding rare). Include as sensitivity analysis only.

Filter: `b05a_idade_em_meses` — string format "X meses", extract numeric with `str.extract(r'(\d+)')`.

## Exposure

**Primary:** `vd_supl1_com_ferro` = "Sim" (any iron supplement in past 6 months, ~30% prevalence)

**Three-level dose-response:**
- Level 0: No supplement at all
- Level 1: Supplement WITHOUT iron
- Level 2: Supplement WITH iron
If gradient exists (0 < 1 < 2 for harm), strengthens causal inference.

**Secondary exposures:** `vd_supl1_somente_ferro` (iron only), `vd_supl1_ferro_sus` (iron from SUS/public health = PNSF proxy), `vd_supl1_exclusivamente_ferro` (exclusively iron).

## Outcomes

### Primary (3 only — pre-specified, avoid fishing)
1. `h13_diarreia` — diarrhea in last 15 days (binary, ~23% prevalence)
2. `vd_pcr_final` — C-reactive protein mg/L (continuous, log-transform; also binary >5 mg/L)
3. `vd_hb_final` — hemoglobin g/dL (continuous, expected benefit)

### Secondary — Infectious Morbidity (binary, "Sim"=1)
- `h14_tosse` (cough 15d), `h15_respiracao` (difficulty breathing), `h16_canseira` (fatigue/dyspnea), `h17_nariz` (congestion), `h18_ronqueira` (wheezing), `h19_febre` (fever 15d)
- `h211_internado_respiratoria` (respiratory hospitalization since birth, ~6%)
- `h212_internado_intestinais` (intestinal hospitalization, ~1.4% — LOW power, report cautiously)
- `u01_febre_diarreia` (fever/diarrhea/vomiting 3 days before blood collection — recode any "Sim*" to 1)
- Composites: `any_infection_symptom` (diarrhea OR fever OR cough+dyspnea), `any_hospitalization_infect` (respiratory OR intestinal)

### Secondary — Inflammation Biomarkers (continuous)
- `vd_leuco_final` (WBC), `vd_bast_final` (band cells = left shift), `vd_seg_final` (neutrophils), `vd_pla_final` (platelets)

### Secondary — Hematological Benefits (continuous)
- `vd_ferri_final` (ferritin, log-transform), `vd_ht_final` (hematocrit), `vd_vcm_final` (MCV), `vd_hcm_final` (MCH), `vd_rdw_final` (RDW)

### Secondary — Micronutrient Competition (continuous)
- `vd_zn_final` (zinc — iron competes via DMT1), `vd_vita_final` (vitamin A), `vd_vit25_final` (vitamin D), `vd_vb12_final` (B12), `vd_afoli_final` (folate)

### Secondary — Growth (continuous)
- `vd_zhaz` (height-for-age z), `vd_zwaz` (weight-for-age z), `vd_zimc` (BMI-for-age z)

### Negative Control
- `h213_internado_acidente` (hospitalization for accident, ~0.4%). Should NOT associate with iron. If it does, signals residual confounding — FLAG THIS.

## Effect Modifiers (Interactions)

1. **Breastfeeding** (`e01_leite_peito`) — PRIMARY interaction. Lactoferrin hypothesis: breastfed infants have apo-lactoferrin that sequesters iron from pathogens while delivering it to the infant via LfR receptors. Expect: iron harms attenuated in breastfed children.
2. **Iron status** — `vd_ferri_final < 12` ng/mL (deficient) vs >= 12 (replete). Sazawal hypothesis: harm mainly in iron-replete children.
3. **Region** — North/Northeast vs South/Southeast/Central-West (exploratory)
4. **Food insecurity** — `vd_ebia_categ` any insecurity vs secure (exploratory)

## Confounders (Adjustment Set)

`age_months` + `b02_sexo` + `d01_cor` (3 levels) + `a00_regiao` (5 levels) + `a11_situacao` + `j10_serie` (4 levels) + `vd_ien_quintos` (1-5) + `vd_ebia_categ` (4 levels) + `p10_esgoto` (adequate/inadequate) + `p11_agua` (rede geral/other) + `h01_semanas_gravidez` + `h02_peso` + `h04_parto` (normal/cesarean) + `k05_prenatal_consultas` (impute median if missing) + `bb04_idade_da_mae` + `e01_leite_peito` + `e10_formula_infantil`

**DO NOT include as confounder:**
- `q031_programa_bolsa_familia` — 60% missing, use only in sensitivity
- `vd_ferri_final` — it's on the causal pathway (mediator), not a confounder

## Survey Weights by Outcome

| Outcome | Weight variable |
|---------|----------------|
| Clinical symptoms, hospitalizations, growth z-scores | `peso_crianca_calib` |
| Hb, Ht, MCV, MCH, RDW, WBC, bands, neutrophils, platelets | `peso_crianca_y_2` |
| Ferritin | `peso_crianca_y_3` |
| CRP | `peso_crianca_y_4` |
| Zinc | `peso_crianca_y_5` |
| Vitamin A | `peso_crianca_y_6` |
| Vitamin D | `peso_crianca_y_7` |
| Vitamin B12 | `peso_crianca_y_9a` |
| Folate | `peso_crianca_y_9b` |

## Statistical Methods

**Binary outcomes:** `statsmodels.GLM(family=Binomial(), freq_weights=weight).fit(cov_type='cluster', cov_kwds={'groups': id_upa_anon})`. Report OR, 95% CI, p-value.

**Continuous outcomes:** `statsmodels.WLS(weights=weight).fit(cov_type='cluster', cov_kwds={'groups': id_upa_anon})`. Report beta, 95% CI, p-value. Log-transform CRP and ferritin; back-transform as % change.

**Three models per outcome:** (1) unadjusted, (2) demographics only, (3) fully adjusted.

**Run everything 3 times:** overall 6-17m, group 6-11m, group 12-17m.

**Sensitivity analyses:**
- IPTW (propensity score): P(iron=1|confounders), multiply IPTW by survey weight, trim 1st/99th percentile
- Alternative exposures: iron_only, iron_sus
- Exclude CRP >5 mg/L from ferritin analyses
- E-values for significant findings
- Benjamini-Hochberg FDR within each outcome category
- Include 18-23m as extended sample
- Negative control validation

## Pipeline

| Phase | Script | Output |
|-------|--------|--------|
| 1 | `01_data_prep.py` | Clean analytic dataset |
| 2 | `02_table1.py` | Table 1 (descriptive by iron status) |
| 3 | `03_primary_analysis.py` | Table 2 + Figure 1 (forest plot) |
| 4 | `04_interactions.py` | Table 3 + Figure 2 (breastfeeding stratified) |
| 5 | `05_sensitivity.py` | Supp Tables S2-S4, Supp Figures S1-S2 |
| 6 | `06_figures.py` | All final publication-quality figures |

## Critical Decision Points

1. **After data prep:** Confirm N ~ 4,300 for 6-17m
2. **After Table 1:** Check covariate balance — if severely imbalanced, IPTW becomes essential
3. **After primary analysis:** If negative control (accident hospitalization) associates with iron → residual confounding is present, STOP and reassess conclusions
4. **After interactions:** If breastfeeding interaction is significant → headline finding. If not → reframe narrative
5. **After IPTW:** If IPTW and regression disagree substantially → report both and discuss

## Coding Rules

- Always use survey weights (correct weight for each outcome — see table above)
- Always cluster SEs at PSU level (`id_upa_anon`)
- Recode Portuguese text to numeric before modeling ("Sim"=1, "Nao"=0, etc.)
- Log-transform CRP and ferritin before linear regression
- DO NOT adjust for ferritin in main models (it's a mediator)
- Use complete-case analysis as default; multiple imputation as sensitivity
- All scripts should be reproducible with `random_state=42` where applicable
