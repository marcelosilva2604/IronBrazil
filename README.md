# Iron Supplementation Benefits and Harms in Brazilian Infants (ENANI-2019)

Cross-sectional analysis evaluating the benefit-harm balance of Brazil's universal iron supplementation programme (PNSF) in infants aged 6-17 months, using nationally representative data from ENANI-2019 (N~4,300).

## Research Question

Is universal prophylactic iron supplementation associated with infectious morbidity, systemic inflammation, and micronutrient competition in Brazilian infants — and does breastfeeding (lactoferrin) modify this effect?

## Study Design

- **Data:** ENANI-2019 (Estudo Nacional de Alimentacao e Nutricao Infantil)
- **Population:** 2 age groups: 6-11 months and 12-17 months
- **Exposure:** Iron supplement use in past 6 months (`vd_supl1_com_ferro`)
- **Primary outcomes:** Diarrhea (15 days), CRP, Hemoglobin
- **Effect modifier:** Breastfeeding status (lactoferrin hypothesis)
- **Statistical approach:** Survey-weighted GLM with cluster-robust SEs, IPTW, negative control

## Data Files

| File | Description |
|------|-------------|
| `data_crianca_calib_anon.csv` | ENANI-2019 microdata (14,557 children, 741 variables) |
| `features_enani.txt` | Variable dictionary (text format) |
| `4-Dicionario-ENANI-2019 (1).xlsx` | Official variable dictionary (Excel) |

**Note:** Data files are anonymized and calibrated with survey weights. Do not redistribute.

## Setup

```bash
# Activate virtual environment
source .venv/bin/activate

# Or from scratch
python3.12 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

## Key Libraries

- `pandas` / `numpy` — data manipulation
- `statsmodels` — survey-weighted GLM, WLS, multiple testing (BH-FDR)
- `scipy` — statistical tests
- `tableone` — Table 1 generation
- `causalinference` — propensity score / IPTW
- `matplotlib` / `seaborn` — figures (forest plots, Love plots)

## Analysis Pipeline

| Phase | Script | Output |
|-------|--------|--------|
| 1. Data prep | `01_data_prep.py` | Clean analytic dataset |
| 2. Descriptive | `02_table1.py` | Table 1 |
| 3. Primary | `03_primary_analysis.py` | Table 2 + Figure 1 (forest plot) |
| 4. Interactions | `04_interactions.py` | Table 3 + Figure 2 |
| 5. Sensitivity | `05_sensitivity.py` | Supp Tables S2-S4 |
| 6. Figures | `06_figures.py` | All final figures |

## Target Journal

Lancet Global Health (1st submission) > BMJ Global Health / AJCN (fallback)

## References

- Sazawal et al. (2006) Lancet 367:133-43 — Pemba trial (iron harm in malaria-endemic setting)
- Jaeggi et al. (2014) Gut 64:731-42 — Iron fortification and gut microbiome in Kenyan infants
- Zimmermann et al. (2010) AJCN 92:1406-15 — Iron fortification and gut microbiota in Cote d'Ivoire
- Cross et al. (2015) Sci Rep 5:16670 — Oral iron elevates bacterial growth in serum
