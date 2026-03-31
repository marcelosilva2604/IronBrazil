# ML Completo — Todos os Resultados

Gerado automaticamente | ml_completo.ipynb | 2026-03-30 18:24

---

## 1. Causal Forest (4 Outcomes)

### Hemoglobina (g/dL) (benefit)

- N train: 1481 | N test: 371
- ATE train: 0.0609 | ATE test: 0.0636 | Diff: 0.0027
- CATE>0 test: 82.2% | CATE<0: 17.8%

#### Bootstrap CI

| Subgrupo | N | CATE | 95% CI | Sig |
|---|---|---|---|---|
| ATE Global | 371 | 0.0636 | 0.0560 to 0.0709 | * |
| Nao amamentado | 147 | 0.1060 | 0.0937 to 0.1188 | * |
| Amamentado | 224 | 0.0357 | 0.0281 to 0.0433 | * |
| Aleit. exclusivo | 104 | 0.0454 | 0.0357 to 0.0552 | * |
| Idade 6-11m | 169 | 0.0409 | 0.0298 to 0.0513 | * |
| Idade 12-18m | 202 | 0.0825 | 0.0710 to 0.0935 | * |
| Nao amam 6-11m | 47 | 0.0884 | 0.0681 to 0.1088 | * |
| Nao amam 12-18m | 100 | 0.1142 | 0.0973 to 0.1293 | * |
| Amam 6-11m | 122 | 0.0226 | 0.0135 to 0.0324 | * |
| Amam 12-18m | 102 | 0.0514 | 0.0402 to 0.0624 | * |
| IEN Q1 | 255 | 0.0718 | 0.0624 to 0.0814 | * |
| IEN Q5 | 14 | 0.0360 | 0.0000 to 0.0660 | * |

#### GATES: Q5-Q1 = 0.2106 (CI: 0.1983 to 0.2231) — CONFIRMADA

#### Equidade IEN
| IEN | N | CATE | 95% CI | Sig |
|---|---|---|---|---|
| Q1 | 1267 | 0.0699 | 0.0653 to 0.0744 | * |
| Q2 | 231 | 0.0463 | 0.0371 to 0.0555 | * |
| Q3 | 174 | 0.0422 | 0.0301 to 0.0534 | * |
| Q4 | 105 | 0.0310 | 0.0170 to 0.0443 | * |
| Q5 | 75 | 0.0519 | 0.0343 to 0.0694 | * |

---

### Crescimento WFL (z-score) (benefit)

- N train: 2481 | N test: 621
- ATE train: 0.0499 | ATE test: 0.0431 | Diff: 0.0068
- CATE>0 test: 72.0% | CATE<0: 28.0%

#### Bootstrap CI

| Subgrupo | N | CATE | 95% CI | Sig |
|---|---|---|---|---|
| ATE Global | 621 | 0.0431 | 0.0376 to 0.0487 | * |
| Nao amamentado | 261 | 0.0345 | 0.0260 to 0.0417 | * |
| Amamentado | 360 | 0.0494 | 0.0417 to 0.0571 | * |
| Aleit. exclusivo | 169 | 0.0457 | 0.0348 to 0.0566 | * |
| Idade 6-11m | 266 | 0.0484 | 0.0399 to 0.0576 | * |
| Idade 12-18m | 355 | 0.0392 | 0.0315 to 0.0464 | * |
| Nao amam 6-11m | 85 | 0.0402 | 0.0253 to 0.0536 | * |
| Nao amam 12-18m | 176 | 0.0318 | 0.0218 to 0.0411 | * |
| Amam 6-11m | 181 | 0.0523 | 0.0422 to 0.0639 | * |
| Amam 12-18m | 179 | 0.0465 | 0.0360 to 0.0573 | * |
| IEN Q1 | 416 | 0.0499 | 0.0421 to 0.0571 | * |
| IEN Q5 | 29 | 0.0063 | -0.0150 to 0.0290 |  |

#### GATES: Q5-Q1 = 0.2019 (CI: 0.1961 to 0.2076) — CONFIRMADA

#### Equidade IEN
| IEN | N | CATE | 95% CI | Sig |
|---|---|---|---|---|
| Q1 | 2073 | 0.0559 | 0.0529 to 0.0588 | * |
| Q2 | 405 | 0.0437 | 0.0367 to 0.0507 | * |
| Q3 | 292 | 0.0410 | 0.0339 to 0.0483 | * |
| Q4 | 190 | 0.0238 | 0.0142 to 0.0330 | * |
| Q5 | 142 | 0.0050 | -0.0071 to 0.0170 |  |

---

### Escore morbidade infecciosa (harm)

- N train: 2499 | N test: 625
- ATE train: -0.0494 | ATE test: -0.0456 | Diff: 0.0038
- CATE>0 test: 24.3% | CATE<0: 75.7%

#### Bootstrap CI

| Subgrupo | N | CATE | 95% CI | Sig |
|---|---|---|---|---|
| ATE Global | 625 | -0.0456 | -0.0508 to -0.0409 | * |
| Nao amamentado | 259 | -0.0745 | -0.0818 to -0.0673 | * |
| Amamentado | 366 | -0.0251 | -0.0311 to -0.0195 | * |
| Aleit. exclusivo | 180 | -0.0288 | -0.0373 to -0.0204 | * |
| Idade 6-11m | 274 | -0.0394 | -0.0476 to -0.0309 | * |
| Idade 12-18m | 351 | -0.0504 | -0.0565 to -0.0446 | * |
| Nao amam 6-11m | 92 | -0.0734 | -0.0881 to -0.0578 | * |
| Nao amam 12-18m | 167 | -0.0752 | -0.0836 to -0.0676 | * |
| Amam 6-11m | 182 | -0.0222 | -0.0313 to -0.0129 | * |
| Amam 12-18m | 184 | -0.0279 | -0.0353 to -0.0208 | * |
| IEN Q1 | 416 | -0.0447 | -0.0509 to -0.0386 | * |
| IEN Q5 | 29 | -0.0389 | -0.0642 to -0.0140 | * |

#### GATES: Q5-Q1 = 0.1763 (CI: 0.1695 to 0.1830) — CONFIRMADA

#### Equidade IEN
| IEN | N | CATE | 95% CI | Sig |
|---|---|---|---|---|
| Q1 | 2089 | -0.0498 | -0.0524 to -0.0473 | * |
| Q2 | 408 | -0.0471 | -0.0527 to -0.0408 | * |
| Q3 | 293 | -0.0433 | -0.0496 to -0.0369 | * |
| Q4 | 192 | -0.0488 | -0.0568 to -0.0409 | * |
| Q5 | 142 | -0.0465 | -0.0572 to -0.0355 | * |

---

### Diarreia 15 dias (harm)

- N train: 2492 | N test: 624
- ATE train: 0.0327 | ATE test: 0.0327 | Diff: 0.0001
- CATE>0 test: 97.3% | CATE<0: 2.7%

#### Bootstrap CI

| Subgrupo | N | CATE | 95% CI | Sig |
|---|---|---|---|---|
| ATE Global | 624 | 0.0327 | 0.0314 to 0.0339 | * |
| Nao amamentado | 267 | 0.0302 | 0.0283 to 0.0321 | * |
| Amamentado | 357 | 0.0346 | 0.0330 to 0.0363 | * |
| Aleit. exclusivo | 164 | 0.0342 | 0.0321 to 0.0363 | * |
| Idade 6-11m | 294 | 0.0354 | 0.0335 to 0.0373 | * |
| Idade 12-18m | 330 | 0.0304 | 0.0289 to 0.0320 | * |
| Nao amam 6-11m | 111 | 0.0329 | 0.0299 to 0.0359 | * |
| Nao amam 12-18m | 156 | 0.0284 | 0.0259 to 0.0309 | * |
| Amam 6-11m | 183 | 0.0369 | 0.0344 to 0.0395 | * |
| Amam 12-18m | 174 | 0.0322 | 0.0302 to 0.0341 | * |
| IEN Q1 | 406 | 0.0326 | 0.0312 to 0.0340 | * |
| IEN Q5 | 28 | 0.0345 | 0.0266 to 0.0420 | * |

#### GATES: Q5-Q1 = 0.0447 (CI: 0.0429 to 0.0466) — CONFIRMADA

#### Equidade IEN
| IEN | N | CATE | 95% CI | Sig |
|---|---|---|---|---|
| Q1 | 2085 | 0.0322 | 0.0315 to 0.0329 | * |
| Q2 | 407 | 0.0308 | 0.0291 to 0.0325 | * |
| Q3 | 292 | 0.0365 | 0.0343 to 0.0388 | * |
| Q4 | 192 | 0.0352 | 0.0322 to 0.0379 | * |
| Q5 | 140 | 0.0344 | 0.0313 to 0.0376 | * |

---

## 2. Decisão Clínica

Thresholds: Hb > 0.05 | Diarreia > 0.018 | Infecção > 0.05 | WFL < -0.05

| Decisão | N | % |
|---|---|---|
(rode célula c9)

## 3. Deploy

| Modelo | R² | JS |
|---|---|---|
| score_hb() | 0.7731 | 128 KB |
| score_anthro_zwfl() | 0.8267 | 128 KB |
| score_infection_score() | 0.7472 | 129 KB |
| score_diarreia() | 0.7264 | 128 KB |

URL: https://marcelosilva2604.github.io/IronBrazil/

## 4. Decision Curve Analysis

Figuras salvas: `dca_hb.png`, `dca_infection_score.png`
O modelo é superior a "suplementar todos" para thresholds acima de ~0.10

## 5. Calibração

| Outcome | Calibration Slope | Intercept | R² |
|---|---|---|---|
| Hemoglobina (g/dL) | -0.535 | 0.2240 | 0.016 |
| Crescimento WFL (z-score) | -0.235 | -0.1253 | 0.002 |
| Escore morbidade infecciosa | -3.698 | -0.0875 | 0.347 |
| Diarreia 15 dias | 2.840 | -0.1437 | 0.403 |

Figuras salvas: `calibration_*.png`

## 6. Validação Geográfica (Cross-Region)

Treino em uma região, validação nas outras. Modelos CausalForestDML treinados com n_estimators=200, min_samples_leaf=30.

| Treino | Validação | ATE treino | ATE valid | Diff | Estável |
|---|---|---|---|---|---|
| Sudeste (Hb) | Resto | +0.0582 | +0.0614 | 0.0032 | ✓ |
| Nordeste (Hb) | Resto | +0.0647 | +0.0598 | 0.0049 | ✓ |
| SE+Sul (Hb) | N+NE+CO | +0.0571 | +0.0639 | 0.0068 | ✓ |
| Sudeste (Infecção) | Resto | -0.0478 | -0.0501 | 0.0023 | ✓ |
| Nordeste (Infecção) | Resto | -0.0512 | -0.0469 | 0.0043 | ✓ |

Todos os ATEs estáveis entre regiões (diff < 0.01). O modelo generaliza geograficamente.

## 7. SHAP vs Regressão Epidemiológica

Comparação entre SHAP importance (Causal Forest surrogate) e |coeficientes| da regressão epidemiológica ajustada.

**Hemoglobina:**
- Pearson: r=0.488 (p=0.010)
- Spearman: r=0.438 (p=0.022)
- Figura: `shap_vs_regression.png`

Concordância moderada e significativa. SHAP captura efeitos não-lineares que a regressão linear não detecta, explicando a divergência parcial.

### SHAP Surrogate R² por Outcome

| Outcome | Surrogate R² |
|---|---|
| Hemoglobina | 0.9934 |
| Crescimento WFL | 0.9875 |
| Escore infeccioso | 0.9785 |
| Diarreia | 0.9724 |

### SHAP Top 5 por Outcome

| Rank | Hemoglobina | WFL | Escore Infeccioso | Diarreia |
|---|---|---|---|---|
| 1 | Peso nascer (0.035) | Idade materna (0.039) | Peso nascer (0.032) | Peso nascer (0.010) |
| 2 | Sexo masculino (0.025) | Peso nascer (0.037) | Idade materna (0.019) | Idade materna (0.005) |
| 3 | Aleitamento materno (0.023) | Idade gestacional (0.012) | Aleitamento materno (0.018) | Consultas PN (0.004) |
| 4 | Idade gestacional (0.022) | Consultas PN (0.012) | Consultas PN (0.016) | Idade meses (0.004) |
| 5 | Idade meses (0.016) | Sexo masculino (0.009) | Sexo masculino (0.010) | Idade gestacional (0.002) |

**Aleitamento materno** aparece como top 3 driver em Hemoglobina e Escore Infeccioso — confirmando independentemente o achado epidemiológico da interação.

## 8. Equidade Formal

### Equidade Completa por Outcome (todos os subgrupos)

**Hemoglobina:**

| Grupo | N | CATE | 95% CI | Sig |
|---|---|---|---|---|
| IEN Q1 | 1267 | 0.0699 | 0.0657 to 0.0741 | * |
| IEN Q2 | 231 | 0.0463 | 0.0368 to 0.0552 | * |
| IEN Q3 | 174 | 0.0422 | 0.0309 to 0.0536 | * |
| IEN Q4 | 105 | 0.0310 | 0.0179 to 0.0445 | * |
| IEN Q5 | 75 | 0.0519 | 0.0341 to 0.0718 | * |
| Cor preta | 102 | 0.0675 | 0.0504 to 0.0843 | * |
| Cor branca/outra | 1750 | 0.0611 | 0.0575 to 0.0649 | * |
| Inseg. grave | 100 | 0.0751 | 0.0589 to 0.0906 | * |
| Segurança alim. | 873 | 0.0698 | 0.0648 to 0.0755 | * |
| Saneam. adequado | 1175 | 0.0634 | 0.0590 to 0.0680 | * |
| Saneam. inadequado | 677 | 0.0579 | 0.0528 to 0.0641 | * |

**Crescimento WFL:**

| Grupo | N | CATE | 95% CI | Sig |
|---|---|---|---|---|
| IEN Q1 | 2073 | 0.0559 | 0.0529 to 0.0589 | * |
| IEN Q2 | 405 | 0.0437 | 0.0367 to 0.0499 | * |
| IEN Q3 | 292 | 0.0410 | 0.0336 to 0.0482 | * |
| IEN Q4 | 190 | 0.0238 | 0.0136 to 0.0328 | * |
| IEN Q5 | 142 | 0.0050 | -0.0079 to 0.0169 | |
| Cor preta | 171 | 0.0546 | 0.0429 to 0.0663 | * |
| Cor branca/outra | 2931 | 0.0482 | 0.0454 to 0.0508 | * |
| Inseg. grave | 139 | 0.0612 | 0.0502 to 0.0717 | * |
| Segurança alim. | 1625 | 0.0443 | 0.0407 to 0.0477 | * |
| Saneam. adequado | 2094 | 0.0437 | 0.0404 to 0.0470 | * |
| Saneam. inadequado | 1008 | 0.0588 | 0.0543 to 0.0632 | * |

**Escore Morbidade Infecciosa:**

| Grupo | N | CATE | 95% CI | Sig |
|---|---|---|---|---|
| IEN Q1 | 2089 | -0.0498 | -0.0527 to -0.0472 | * |
| IEN Q2 | 408 | -0.0471 | -0.0531 to -0.0416 | * |
| IEN Q3 | 293 | -0.0433 | -0.0496 to -0.0371 | * |
| IEN Q4 | 192 | -0.0488 | -0.0573 to -0.0405 | * |
| IEN Q5 | 142 | -0.0465 | -0.0573 to -0.0355 | * |
| Cor preta | 173 | -0.0457 | -0.0550 to -0.0363 | * |
| Cor branca/outra | 2951 | -0.0488 | -0.0511 to -0.0467 | * |
| Inseg. grave | 141 | -0.0577 | -0.0681 to -0.0469 | * |
| Segurança alim. | 1635 | -0.0493 | -0.0525 to -0.0462 | * |
| Saneam. adequado | 2111 | -0.0503 | -0.0529 to -0.0478 | * |
| Saneam. inadequado | 1013 | -0.0452 | -0.0490 to -0.0412 | * |

**Diarreia:**

| Grupo | N | CATE | 95% CI | Sig |
|---|---|---|---|---|
| IEN Q1 | 2085 | 0.0322 | 0.0315 to 0.0329 | * |
| IEN Q2 | 407 | 0.0308 | 0.0292 to 0.0323 | * |
| IEN Q3 | 292 | 0.0365 | 0.0343 to 0.0386 | * |
| IEN Q4 | 192 | 0.0352 | 0.0327 to 0.0377 | * |
| IEN Q5 | 140 | 0.0344 | 0.0312 to 0.0377 | * |
| Cor preta | 173 | 0.0329 | 0.0302 to 0.0356 | * |
| Cor branca/outra | 2943 | 0.0327 | 0.0321 to 0.0332 | * |
| Inseg. grave | 141 | 0.0315 | 0.0290 to 0.0343 | * |
| Segurança alim. | 1632 | 0.0323 | 0.0314 to 0.0331 | * |
| Saneam. adequado | 2105 | 0.0316 | 0.0309 to 0.0324 | * |
| Saneam. inadequado | 1011 | 0.0349 | 0.0338 to 0.0358 | * |

### Disparidades Formais (resumo)

| Outcome | Disparidade IEN | Ratio | Sig | Disparidade Racial |
|---|---|---|---|---|
| Hemoglobina | Q1-Q4 = 0.039 | 2.3x | * | 0.006 (NS) |
| Crescimento WFL | Q1-Q5 = 0.051 | 11.1x | * | 0.006 (NS) |
| Escore infeccioso | Q3-Q1 = 0.007 | 0.9x | NS | 0.003 (NS) |
| Diarreia | Q3-Q2 = 0.006 | 1.2x | * | 0.000 (NS) |

**Conclusão de equidade:** Ferro beneficia mais os mais pobres (gradiente IEN significativo para Hb e WFL). Sem disparidade racial relevante (< 0.007 em todos os outcomes). Ferro é uma intervenção **equity-positive**.

**Hemoglobina (g/dL):** IEN Q1-Q4 = 0.0389 (CI: 0.0250 to 0.0521) * | Ratio: 2.3x
  Preta: CATE=0.0675 (CI: 0.0507 to 0.0835) N=102
  Branca/outra: CATE=0.0611 (CI: 0.0573 to 0.0650) N=1750

**Crescimento WFL (z-score):** IEN Q1-Q5 = 0.0508 (CI: 0.0368 to 0.0628) * | Ratio: 11.1x
  Preta: CATE=0.0546 (CI: 0.0433 to 0.0656) N=171
  Branca/outra: CATE=0.0482 (CI: 0.0456 to 0.0510) N=2931

**Escore morbidade infecciosa:** IEN Q3-Q1 = 0.0065 (CI: -0.0006 to 0.0135)  | Ratio: 0.9x
  Preta: CATE=-0.0457 (CI: -0.0541 to -0.0363) N=173
  Branca/outra: CATE=-0.0488 (CI: -0.0511 to -0.0466) N=2951

**Diarreia 15 dias:** IEN Q3-Q2 = 0.0057 (CI: 0.0029 to 0.0085) * | Ratio: 1.2x
  Preta: CATE=0.0329 (CI: 0.0305 to 0.0354) N=173
  Branca/outra: CATE=0.0327 (CI: 0.0321 to 0.0333) N=2943


## 9. Figuras Geradas

- `calibration_anthro_zwfl.png` (137 KB)
- `calibration_diarreia.png` (151 KB)
- `calibration_hb.png` (156 KB)
- `calibration_infection_score.png` (141 KB)
- `clinical_decision.png` (2559 KB)
- `dca_hb.png` (133 KB)
- `dca_infection_score.png` (132 KB)
- `shap_anthro_zwfl.png` (408 KB)
- `shap_diarreia.png` (434 KB)
- `shap_hb.png` (377 KB)
- `shap_infection_score.png` (412 KB)
- `shap_vs_regression.png` (278 KB)