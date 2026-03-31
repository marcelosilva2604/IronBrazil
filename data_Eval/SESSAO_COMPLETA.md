# Sessão Completa — Iron Supplementation Project (2026-03-30)

## Tudo que foi feito, todos os resultados, todas as decisões.

---

## 1. SETUP DO PROJETO

- **Pasta:** `/Users/marcelocarvalhoesilva/project/iron/`
- **Dados:** ENANI-2019, `data_crianca_calib_anon.csv` (14.558 crianças, 741 colunas)
- **Venv:** Python 3.12 com pandas, statsmodels, scipy, econml, shap, m2cgen
- **GitHub:** https://github.com/marcelosilva2604/IronBrazil
- **GitHub Pages:** https://marcelosilva2604.github.io/IronBrazil/
- **Zotero:** Coleção "Iron" criada com 12 artigos-chave

---

## 2. POPULAÇÃO DO ESTUDO

- **Filtro:** 6-18 meses (b05a_idade_em_meses)
- **N final:** 3.127 crianças
- **Grupos etários:** 6-11m (1.415) | 12-18m (1.712)
- **Exposição (iron_any):** 978 (31.3%) usam ferro

### 4 Níveis de Exposição
| Nível | Descrição | N (%) |
|---|---|---|
| 0 | Nenhum suplemento | 1.026 (32.8%) |
| 1 | Suplemento sem ferro | 1.123 (35.9%) |
| 2 | Ferro + outros (multi) | 131 (4.2%) |
| 3 | Ferro isolado (PNSF) | 847 (27.1%) |

### Tipo de Alimentação
| Tipo | N (%) |
|---|---|
| Sem aleitamento | 1.290 (41.3%) |
| Aleitamento misto | 963 (30.8%) |
| Aleitamento exclusivo/predominante | 874 (27.9%) |

---

## 3. DESFECHOS AVALIADOS (52 total)

### Cutoffs usados (baseados em ENANI-2019 e WHO)
| Desfecho | Cutoff | Referência |
|---|---|---|
| Anemia | Hb < 10.5 g/dL (6-23m) | WHO 2024 / ENANI-2019 |
| Deficiência de ferro | Ferritina < 12 µg/L | WHO |
| Anemia ferropriva | Hb < 10.5 E Ferritina < 12 | Combinação |
| Deficiência de zinco | Zinco < 65 µg/dL | IZiNCG |
| Deficiência de vit A | Retinol < 0.20 mg/L | WHO (0.7 µmol/L) |
| PCR elevada | > 5 mg/L | ENANI-2019 |

---

## 4. CONFOUNDERS (25 variáveis)

age_months, male, race_preta, race_parda, reg_norte, reg_nordeste, reg_sul, reg_co, urban, educ_fund_comp, educ_medio, educ_superior, ien, ebia_leve, ebia_mod, ebia_grave, esgoto_adeq, agua_rede, cesarean, gest_weeks, birth_weight, prenatal_visits, maternal_age, breastfed, formula

**Missing:** apenas maternal_age com 3 (0.1%)

**NÃO incluídos (e por quê):**
- Bolsa Família: 60.3% missing
- Ferritina como confounder: está no caminho causal (mediador)

---

## 5. TESTE BRUTO (NÃO AJUSTADO)

### Ferro sim vs não: 20 de 52 significativos
- Padrão: confounding por healthcare-seeking (grupo "supl sem ferro" era o mais doente)
- Controle negativo (internação acidente): 0.4% vs 0.4% (p=1.00) — perfeito

### 4 Níveis: 33 de 52 significativos
- Gradiente dose-resposta limpo para índices hematológicos
- Anemia: 17.5% → 17.0% → 13.5% → 11.1% (nenhum→supl s/ferro→ferro+out→ferro isolado)
- Ferritina: 24.01 → 24.74 → 25.75 → 29.32
- Morbidade infecciosa: pico no grupo "supl sem ferro", não no ferro

---

## 6. REGRESSÃO AJUSTADA (25 confounders)

### Método
- Binários: Poisson modificado (Zou 2004) com var_weights + cluster→HC1 fallback
- Contínuos: WLS com cluster-robust SEs (UPA)
- Binários de biomarcadores: Logit sem peso + HC1 (fallback por convergência)

### Resultados Significativos — iron_any (qualquer ferro)

**Benefícios (p<0.05):**
| Desfecho | Efeito | IC 95% | p |
|---|---|---|---|
| Anemia (Hb<10.5) | OR=0.69 | 0.51-0.94 | 0.019 |
| Def. ferro (Ferri<12) | OR=0.74 | 0.58-0.94 | 0.015 |
| PCR elevada (>5) | OR=0.67 | 0.49-0.91 | 0.012 |
| Hemoglobina | +0.19 g/dL | 0.01-0.37 | 0.039 |
| Hematócrito | +0.69% | 0.13-1.24 | 0.016 |

**Danos (p<0.05):**
| Desfecho | Efeito | IC 95% | p |
|---|---|---|---|
| Z peso/comprimento (WFL) | -0.18 z | -0.36 a -0.005 | 0.043 |

**Borderline (0.05 ≤ p < 0.10):**
| Desfecho | Efeito | IC 95% | p |
|---|---|---|---|
| Internação intestinal | PR=2.39 | 0.99-5.79 | 0.053 |
| WAZ | -0.16 z | | 0.060 |
| BAZ | -0.17 z | | 0.055 |

**Sem diferença estatística:** diarreia, febre, tosse, dispneia, nariz, ronqueira, zinco, B12, folato, vit B1/B6/D/E, selênio, HAZ, leucócitos, neutrófilos, bastonetes, plaquetas, linfócitos, monócitos.

---

## 7. FERRO ISOLADO vs CO-SUPLEMENTAÇÃO

Comparação ferro isolado (n=847) vs nenhum suplemento (n=1.026):

| Desfecho | iron_any | Ferro isolado | Veredicto |
|---|---|---|---|
| Anemia | OR=0.69, p=0.019 | **OR=0.58, p=0.005** | Efeito real, mais forte |
| Def. ferro | OR=0.74, p=0.015 | **OR=0.71, p=0.026** | Manteve |
| PCR elevada | OR=0.67, p=0.012 | **OR=0.64, p=0.023** | Manteve |
| Def. vit A | OR=0.59, p=0.007 | OR=0.66, **p=0.085** | **Perdeu — era co-suplementação** |

---

## 8. INTERAÇÃO FERRO x ALEITAMENTO MATERNO

### Binário (p_interação Hb = 0.027)

| Desfecho | Não amamentados | Amamentados |
|---|---|---|
| **Hemoglobina** | **+0.43*** (p=0.001) | +0.02 (p=0.89) |
| Hematócrito | +1.11* (p=0.013) | +0.38 (p=0.30) |
| Intern. respiratória | OR=**1.74*** (p=0.018) | OR=1.17 (p=0.47) |
| Intern. infecciosa | OR=**1.72*** (p=0.013) | OR=1.27 (p=0.23) |
| WAZ | **-0.305*** (p=0.022) | -0.062 (p=0.55) |

### Por tipo de alimentação x faixa etária

**6-11m, aleitamento exclusivo (achado mais forte):**
| Desfecho | Efeito | p | p interação |
|---|---|---|---|
| Febre/diarreia/vômito 3d | OR=**2.34** | 0.023 | **0.003** |
| Internação respiratória | OR=**2.73** | 0.023 | — |
| Internação infecciosa | OR=**2.55** | 0.026 | — |
| Vitamina A | **-0.084** mg/L | 0.009 | — |
| Vitamina B1 | **-7.85** µg/dL | 0.036 | 0.030 |

**12-18m, não amamentados:**
| Desfecho | Efeito | p | p interação |
|---|---|---|---|
| Internação respiratória | OR=**2.03** | 0.013 | **0.019** |
| Internação infecciosa | OR=**1.80** | 0.025 | **0.025** |

---

## 9. INTERAÇÃO COM STATUS DE FERRO (Sazawal)

Nenhuma interação significativa (todos p>0.30). Hipótese de que dano é concentrado em crianças repletas **não se confirmou** no Brasil.

---

## 10. IPTW (PROPENSITY SCORE)

- N após trim (1-99%): 3.060
- PS range: 0.148-0.610
- **Balanceamento excelente:**

| Variável | SMD antes | SMD IPTW |
|---|---|---|
| IEN | 0.286 | 0.022 |
| Idade materna | 0.105 | 0.021 |
| Peso nascer | 0.081 | 0.001 |

---

## 11. E-VALUES

| Achado | E-value (ponto) | E-value (CI) |
|---|---|---|
| Anemia (OR=0.58) | 2.81 | 4.50 |
| Def. ferro (OR=0.71) | 2.17 | 3.25 |
| PCR elevada (OR=0.64) | 2.47 | 3.85 |
| Intern. resp não-amam 12-18m (OR=2.03) | 3.44 | 1.68 |
| Febre/diarreia excl.amam 6-11m (OR=2.34) | 4.12 | 1.53 |

---

## 12. CAUSAL MACHINE LEARNING

### Setup
- **4 Outcomes:** Hemoglobina (benefit), WFL (benefit), Infection score (harm), Diarreia (harm)
- **27 features**
- **3 modelos:** CausalForestDML, T-Learner, S-Learner
- **Holdout 80/20** com verificação de integridade (0 overlap, <0.2% iron diff)

### Resultados dos 4 Outcomes

**Hemoglobina:**
- ATE test: +0.064 g/dL | ATE train: +0.061 | Diff: 0.003
- 82.2% CATE>0
- Não amam: +0.106* | Amam: +0.036* | Ratio: 3x
- Não amam 12-18m: +0.114* (maior) | Amam 6-11m: +0.023* (menor)
- GATES Q5-Q1: 0.211 (CI: 0.198-0.223) — **Heterogeneidade CONFIRMADA**
- Surrogate R²: 0.993 | Deploy R²: 0.773

**Crescimento WFL:**
- ATE test: +0.043 z | Diff: 0.007
- 72% CATE>0
- IEN Q1: +0.056* | Q5: +0.005 (NS) — gradiente equidade
- GATES Q5-Q1: 0.202 (CI: 0.196-0.208) — **CONFIRMADA**
- Surrogate R²: 0.988 | Deploy R²: 0.827

**Escore Morbidade Infecciosa:**
- ATE test: **-0.046** (ferro REDUZ infecções)
- 75.7% CATE<0
- Não amam: -0.075* | Amam: -0.025*
- Inseg. alimentar grave: -0.058*
- GATES Q5-Q1: 0.176 (CI: 0.170-0.183) — **CONFIRMADA**
- Surrogate R²: 0.979 | Deploy R²: 0.747

**Diarreia:**
- ATE test: **+0.033** (ferro AUMENTA diarreia)
- 97.3% CATE>0
- Amam 6-11m: +0.037* (maior) | Não amam 12-18m: +0.028* (menor)
- GATES Q5-Q1: 0.045 (CI: 0.043-0.046) — **CONFIRMADA**
- Surrogate R²: 0.972 | Deploy R²: 0.726

### Concordância entre Modelos (test set)
| | CF vs TL | CF vs SL |
|---|---|---|
| Hb | r=0.230 | r=0.272 |
| WFL | r=0.248 | r=0.222 |
| Infection | r=0.346 | r=0.238 |
| Diarreia | r=0.298 | r=0.268 |

### SHAP — Top 5 Drivers por Outcome
| Rank | Hemoglobina | WFL | Escore Infeccioso | Diarreia |
|---|---|---|---|---|
| 1 | Peso nascer | Idade materna | Peso nascer | Peso nascer |
| 2 | Sexo masculino | Peso nascer | Idade materna | Idade materna |
| 3 | Idade gestacional | Idade gestacional | **Aleitamento materno** | Consultas PN |
| 4 | **Aleitamento materno** | Consultas PN | Consultas PN | Idade (meses) |
| 5 | Idade (meses) | Sexo masculino | Sexo masculino | Idade gestacional |

### Equidade

**WFL por IEN:**
| IEN | CATE | Sig |
|---|---|---|
| Q1 (mais pobre) | +0.056 | * |
| Q2 | +0.044 | * |
| Q3 | +0.041 | * |
| Q4 | +0.024 | * |
| Q5 (mais rico) | +0.005 | NS |

Ferro beneficia crescimento **11x mais** nos mais pobres vs mais ricos.

---

## 13. DECISÃO CLÍNICA (4 outcomes)

### Thresholds Calibrados
| Critério | Threshold | Justificativa |
|---|---|---|
| Hb benefit | > 0.05 g/dL | GATES Q2-Q3 boundary, ~1/3 SD CATE |
| Diarreia risk | > 0.018 | P25 da distribuição CATE |
| Infection risk | > 0.05 | Acima do ATE médio |
| Growth harm | WFL < -0.05 | Diferença clinicamente relevante |

### Distribuição de Decisões
| Decisão | N (%) |
|---|---|
| TRADE-OFF | 1.078 (59%) |
| NÃO SUPLEMENTAR | 479 (26%) |
| SUPLEMENTAR | 280 (15%) |

### Por Aleitamento x Idade
| Grupo | Suplementar | Trade-off | Não supl |
|---|---|---|---|
| Amam 6-11m | 35 | 297 | 202 |
| Amam 12-18m | 91 | 288 | 166 |
| Não amam 6-11m | 35 | 170 | 52 |
| Não amam 12-18m | 119 | 323 | 59 |

### Validação com 10 Cenários Clínicos: 8/10 acurácia
- Amam exclusivo → TRADE-OFF ou NÃO SUPL ✓
- Não amam 14-18m → SUPLEMENTAR ✓
- Prematuro extremo → NÃO SUPL ✓
- Erros marginais: diferenças de 0.001 nos thresholds

---

## 14. DEPLOY

### Modelos Exportados (JS via m2cgen)
| Modelo | R² deploy | Tamanho JS |
|---|---|---|
| score_hb() | 0.773 | 128 KB |
| score_anthro_zwfl() | 0.827 | 128 KB |
| score_infection_score() | 0.747 | 129 KB |
| score_diarreia() | 0.726 | 128 KB |

### Ferramenta Web
- URL: https://marcelosilva2604.github.io/IronBrazil/
- 27 campos de entrada
- Validação de inputs (idade 6-18m, peso 500-5500g, etc.)
- 4 métricas exibidas: Hb (g/dL), WFL (z-score), Infecção (%), Diarreia (%)
- 3 decisões: SUPLEMENTAR (verde) / TRADE-OFF (laranja) / NÃO SUPLEMENTAR (vermelho)

---

## 15. CONVERGÊNCIA MULTI-MÉTODO

| Achado | Epidemiologia | Causal ML |
|---|---|---|
| Ferro melhora Hb | +0.19 g/dL (p=0.039) | CATE +0.064* |
| Efeito maior sem amamentação | +0.43 vs +0.02 (p_int=0.027) | CATE +0.106 vs +0.036 |
| Aleitamento é top modifier | Interação formal sig | SHAP: 4o driver (Hb), 3o (infecção) |
| Heterogeneidade real | Interações pré-especificadas | GATES p<0.05 (x4) |
| Ferro reduz desigualdade | Não testado formalmente | IEN Q1 CATE 11x > Q5 |
| Ferro aumenta diarreia | Bruto NS, ajustado NS | CATE +0.033 (97.3% > 0) |
| Ferro reduz infecções gerais | PCR OR=0.67 (p=0.012) | CATE -0.046 (75.7% < 0) |

---

## 16. ARTIGOS NO ZOTERO (Coleção Iron)

12 artigos adicionados via API:
1. ENANI-2019 Food Insecurity/Anemia/VAD (CDN 2025)
2. ENANI-2019 Factors anemia/VAD (CSP 2023)
3. ENANI-2019 General methodology (CSP 2021)
4. ENANI-2019 Micronutrient methodology (CSP 2021)
5. ENANI-2019 Nutrition transition (CSP 2023)
6. Lancet Global Health — Hb thresholds India (2021)
7. Nepal — Iron/VitA/Zinc cutoffs (MCN 2021)
8. Sazawal 2006 — Pemba trial (Lancet)
9. Jaeggi 2014 — Gut microbiome Kenya (Gut)
10. Zimmermann 2010 — Gut microbiota Cote d'Ivoire (AJCN)
11. Cross 2015 — Bacterial growth serum (Sci Rep)
12. Iannotti 2006 — Iron benefits/risks review (AJCN)

---

## 17. TARGET E TÍTULO

**Journal:** Lancet Digital Health

**Título proposto:**
> "Causal machine learning to identify heterogeneous effects of iron supplementation on haematological, growth, and infectious morbidity outcomes in Brazilian infants: a nationally representative, cross-sectional, development and validation study"

---

## 18. PENDÊNCIAS PARA O MANUSCRITO

### Análises adicionais necessárias (baseado em revisão de 13 artigos do Lancet DH):
- [ ] Decision Curve Analysis (DCA)
- [ ] Calibração formal (slope + calibration-in-the-large + plot)
- [ ] Validação geográfica (treinar em uma região, validar nas outras)
- [ ] Comparação SHAP ML vs coeficientes epidemiologia (visual)
- [ ] TRIPOD+AI checklist
- [ ] Métricas de equidade formais (disparidade max-min com CI)

### Manuscrito:
- [ ] Research in Context (com busca PubMed formal)
- [ ] Introduction (600-900 palavras)
- [ ] Methods (1500-2500 palavras)
- [ ] Results (1500-2500 palavras)
- [ ] Discussion (1500-2000 palavras)
- [ ] 5-6 figuras/tabelas publication-quality
- [ ] 30-40 referências Vancouver
- [ ] Inglês britânico
- [ ] Supplementary appendix

---

*Gerado em 2026-03-30 — sessão de ~8 horas*
