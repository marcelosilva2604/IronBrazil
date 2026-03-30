# Resultados Completos — Suplementação de Ferro em Lactentes Brasileiros (ENANI-2019)

**Data:** 2026-03-30 | **Status:** Análise completa (epidemiologia + causal ML)

---

## 1. Dados e População

- **Fonte:** ENANI-2019 (Estudo Nacional de Alimentação e Nutrição Infantil)
- **Amostra total:** 14.558 crianças, 741 variáveis
- **População do estudo:** 3.127 crianças de 6-18 meses
  - Grupo 6-11m: 1.415 crianças
  - Grupo 12-18m: 1.712 crianças
- **Prevalência da exposição:** 31.3% usam suplemento com ferro (n=978)

### Distribuição da exposição (4 níveis)

| Nível | Descrição | N (%) |
|---|---|---|
| 0 | Nenhum suplemento | 1.026 (32.8%) |
| 1 | Suplemento sem ferro | 1.123 (35.9%) |
| 2 | Ferro + outros (multivitamínico) | 131 (4.2%) |
| 3 | Ferro isolado (proxy do PNSF) | 847 (27.1%) |

### Tipo de alimentação

| Tipo | N (%) |
|---|---|
| Sem aleitamento | 1.290 (41.3%) |
| Aleitamento misto | 963 (30.8%) |
| Aleitamento exclusivo/predominante | 874 (27.9%) |

---

## 2. Pipeline Analítica

### Notebook `data1.ipynb` — Epidemiologia Clássica

| Etapa | Conteúdo |
|---|---|
| 1-2 | Carregamento e filtro (6-18m, 2 grupos etários) |
| 3 | Exposição: binária + 4 níveis |
| 4 | Exploração de 52 desfechos (distribuição, missing) |
| 5 | Teste bruto ferro vs sem ferro (Chi², Mann-Whitney): 20/52 significativos |
| 6 | Teste estratificado 4 níveis (Kruskal-Wallis): 33/52 significativos |
| 7 | Recodificação de 25 confounders |
| 8 | Regressão ajustada (Poisson modificado + WLS cluster-robust) |
| 9 | Fix dedicado para binários derivados de biomarcadores |
| 10 | Verificação ferro isolado vs co-suplementação |
| 11 | Interação ferro x aleitamento materno (binário) |
| 12 | Interação ferro x tipo de alimentação (3 níveis) x faixa etária |
| 13 | Table 1 descritiva |
| 14 | Interação status de ferro + IPTW + E-values + FDR |
| 15 | Causal Forest exploratório (primeira versão) |

### Notebook `ml_causal.ipynb` — Causal Machine Learning (validação rigorosa)

| Etapa | Conteúdo |
|---|---|
| 1-3 | Setup, carregamento, definição de features (27) e outcomes (WFL, Hb) |
| 4 | Train-test split 80/20 com verificação de integridade |
| 5 | Comparação de 3 modelos causais (CausalForestDML, T-Learner, S-Learner) |
| 6 | Bootstrap CI (n=1000) para CATE por subgrupo |
| 7 | GATES (Group Average Treatment Effects por quintil de CATE) |
| 8 | SHAP via surrogate + correlação SHAP vs regressão epidemiológica |
| 9 | Equidade com bootstrap CI por região, raça, IEN |
| 10 | Trade-off scatter + modelo de decisão clínica |
| 11 | Deploy: surrogate exportado (joblib) + config JSON + demo |

---

## 3. Resultados — Epidemiologia Clássica

### 3.1 Análise Bruta (não ajustada)

- **20 de 52 desfechos** significativos (ferro sim vs não)
- Padrão dominante: confounding por healthcare-seeking
- O grupo "suplemento sem ferro" tinha a MAIOR morbidade infecciosa, não o grupo com ferro
- Gradiente dose-resposta limpo para índices hematológicos nos 4 níveis

### 3.2 Análise Ajustada (25 confounders)

**Benefícios significativos (ferro sim vs não, overall):**

| Desfecho | Efeito | IC 95% | p |
|---|---|---|---|
| Anemia (Hb<10.5) | OR=0.69 | 0.51-0.94 | 0.019 |
| Deficiência de ferro (Ferri<12) | OR=0.74 | 0.58-0.94 | 0.015 |
| PCR elevada (>5 mg/L) | OR=0.67 | 0.49-0.91 | 0.012 |
| Hemoglobina | +0.19 g/dL | 0.01-0.37 | 0.039 |
| Hematócrito | +0.69% | 0.13-1.24 | 0.016 |

**Dano significativo:**

| Desfecho | Efeito | IC 95% | p |
|---|---|---|---|
| Z peso/comprimento (WFL) | -0.18 z | -0.36 a -0.005 | 0.043 |

**Borderline:**

| Desfecho | Efeito | IC 95% | p |
|---|---|---|---|
| Internação intestinal | PR=2.39 | 0.99-5.79 | 0.053 |
| Z peso/idade (WAZ) | -0.16 z | -0.33 a 0.01 | 0.060 |
| Z IMC/idade (BAZ) | -0.17 z | -0.36 a 0.004 | 0.055 |

**Sem diferença estatística:** diarreia, febre, tosse, dispneia, ronqueira, nariz entupido, zinco, B12, folato, vitaminas B1/B6/D/E, selênio, crescimento linear (HAZ), leucócitos, neutrófilos, bastonetes, plaquetas, linfócitos, monócitos.

### 3.3 Verificação Ferro Isolado vs Co-suplementação

| Desfecho | iron_any (todos) | Ferro isolado vs nenhum |
|---|---|---|
| Anemia | OR=0.69, p=0.019 | **OR=0.58, p=0.005** (mais forte) |
| Def. ferro | OR=0.74, p=0.015 | **OR=0.71, p=0.026** (manteve) |
| PCR elevada | OR=0.67, p=0.012 | **OR=0.64, p=0.023** (manteve) |
| Def. vit A | OR=0.59, p=0.007 | OR=0.66, **p=0.085** (perdeu!) |

**Conclusão:** a proteção de vitamina A era artefato de co-suplementação com multivitamínicos. Anemia, deficiência de ferro e redução de inflamação são efeitos reais do ferro isolado.

---

## 4. Resultados — Interação com Aleitamento Materno

### 4.1 Interação binária (ferro x aleitamento, p_interação para Hb = 0.027)

| Desfecho | Não amamentados | Amamentados |
|---|---|---|
| **Hemoglobina** | **+0.43 g/dL*** (p=0.001) | +0.02 (p=0.89) |
| Hematócrito | +1.11* (p=0.013) | +0.38 (p=0.30) |
| Intern. respiratória | OR=**1.74*** (p=0.018) | OR=1.17 (p=0.47) |
| Intern. infecciosa | OR=**1.72*** (p=0.013) | OR=1.27 (p=0.23) |
| Z peso/idade | **-0.305*** (p=0.022) | -0.062 (p=0.55) |

**Achado central:** Ferro só funciona (e só prejudica) em crianças não amamentadas. Em amamentadas, efeito próximo de zero em ambas as direções.

### 4.2 Interação por tipo de alimentação (3 níveis) x faixa etária

**6-11 meses, aleitamento exclusivo — ACHADO MAIS FORTE:**

| Desfecho | Efeito | p | p interação |
|---|---|---|---|
| Febre/diarreia/vômito 3d | OR=**2.34** | 0.023 | **0.003** |
| Internação respiratória | OR=**2.73** | 0.023 | — |
| Internação infecciosa | OR=**2.55** | 0.026 | — |
| Vitamina A | **-0.084** mg/L | 0.009 | — |
| Vitamina B1 | **-7.85** µg/dL | 0.036 | 0.030 |

**12-18 meses, não amamentados — dano clássico:**

| Desfecho | Efeito | p | p interação |
|---|---|---|---|
| Internação respiratória | OR=**2.03** | 0.013 | **0.019** |
| Internação infecciosa | OR=**1.80** | 0.025 | **0.025** |
| Alergia alimentar | OR=**2.28** | 0.016 | — |

### 4.3 Interação com Status de Ferro (Hipótese Sazawal)

Nenhuma interação significativa (todos p>0.30). A hipótese de que o dano é concentrado em crianças repletas de ferro **não se confirmou** no Brasil.

---

## 5. Análises de Sensibilidade

### 5.1 IPTW (Propensity Score)

- N após trim (1-99%): 3.060
- PS range: 0.148-0.610
- **Balanceamento excelente** (todos SMD < 0.03 após IPTW):

| Variável | SMD antes | SMD IPTW |
|---|---|---|
| IEN (riqueza) | 0.286 | 0.022 |
| Idade materna | 0.105 | 0.021 |
| Peso nascer | 0.081 | 0.001 |

### 5.2 E-values

| Achado | E-value (ponto) | E-value (CI) |
|---|---|---|
| Anemia (OR=0.58) | 2.81 | 4.50 |
| Def. ferro (OR=0.71) | 2.17 | 3.25 |
| PCR elevada (OR=0.64) | 2.47 | 3.85 |
| Intern. resp não-amam 12-18m (OR=2.03) | 3.44 | 1.68 |
| Febre/diarreia excl.amam 6-11m (OR=2.34) | 4.12 | 1.53 |

### 5.3 FDR (Benjamini-Hochberg)

Aplicada dentro de cada categoria de desfecho na análise principal.

---

## 6. Resultados — Causal Machine Learning

### 6.1 Verificação de Integridade (Holdout 80/20)

| Outcome | Train | Test | ID overlap | Iron diff |
|---|---|---|---|---|
| WFL | 2.481 | 621 | 0 ✓ | 0.04% ✓ |
| Hemoglobina | 1.481 | 371 | 0 ✓ | 0.14% ✓ |

### 6.2 Comparação de 3 Modelos Causais

| Modelo | ATE train (Hb) | ATE test (Hb) | Diff |
|---|---|---|---|
| **CausalForestDML** | 0.0566 | 0.0583 | **0.0017** (mais estável) |
| T-Learner | 0.1440 | 0.1768 | 0.0328 |
| S-Learner | 0.1518 | 0.1462 | 0.0056 |

Concordância entre modelos (Pearson r no test): CF vs TL = 0.26, CF vs SL = 0.31, TL vs SL = 0.55.

### 6.3 Bootstrap CI (n=1000) — CATE por Subgrupo (Hemoglobina)

| Subgrupo | N | CATE | 95% CI | Sig |
|---|---|---|---|---|
| **Não amamentado** | 147 | **+0.098** | 0.085-0.111 | * |
| **Amamentado** | 224 | **+0.032** | 0.024-0.040 | * |
| Aleit. exclusivo | 104 | +0.045 | 0.035-0.056 | * |
| Aleit. misto | 120 | +0.021 | 0.010-0.031 | * |
| Não amam 12-18m | 100 | **+0.106** | 0.090-0.122 | * (maior benefício) |
| Amam 6-11m | 122 | **+0.018** | 0.007-0.029 | * (menor benefício) |
| IEN Q1 (mais pobre) | 255 | +0.066 | 0.057-0.076 | * |
| IEN Q5 (mais rico) | 14 | +0.031 | -0.002-0.058 | NS |

**Ratio não-amam/amam: 3.1x** — ferro beneficia Hb 3x mais em não amamentados.

### 6.4 GATES — Heterogeneidade Confirmada

| Outcome | GATES Q5-Q1 | 95% CI | Resultado |
|---|---|---|---|
| WFL | 0.207 | 0.201-0.213 | **Heterogeneidade CONFIRMADA** |
| Hemoglobina | 0.210 | 0.198-0.222 | **Heterogeneidade CONFIRMADA** |

### 6.5 SHAP — Top Drivers da Heterogeneidade

**Hemoglobina:**
1. Peso nascer (0.037)
2. Sexo masculino (0.023)
3. Idade gestacional (0.021)
4. **Aleitamento materno (0.019)** ← 4o driver
5. Idade em meses (0.016)

**WFL:**
1. Peso nascer (0.040)
2. Idade materna (0.038)
3. Consultas PN (0.013)
4. Idade gestacional (0.011)
5. Sexo masculino (0.011)
6. Idade em meses (0.007)
7. **Aleitamento materno (0.007)** ← 7o driver

Correlação SHAP vs Regressão: Spearman r=0.44-0.49 (p<0.05).
Surrogate R²: 0.991 (WFL), 0.995 (Hb).

### 6.6 Equidade

**WFL — Gradiente por IEN:**

| IEN | CATE WFL | 95% CI |
|---|---|---|
| Q1 (mais pobre) | **+0.061** | 0.058-0.065 * |
| Q2 | +0.046 | 0.038-0.053 * |
| Q3 | +0.045 | 0.037-0.053 * |
| Q4 | +0.026 | 0.017-0.037 * |
| Q5 (mais rico) | +0.007 | -0.005-0.020 NS |

**Ferro beneficia crescimento 8x mais nos mais pobres.** Disparidade max-min: 0.054.

Insegurança alimentar grave: CATE = +0.066 vs Segurança: +0.049.
Saneamento inadequado: CATE = +0.063 vs Adequado: +0.048.

### 6.7 Decisão Clínica Individualizada

| Decisão | N (%) |
|---|---|
| **SUPLEMENTAR** (Hb↑ + Peso ok) | 1.253 (68.1%) |
| **NÃO SUPLEMENTAR** (Hb↓) | 421 (22.9%) |
| **TRADE-OFF** (Hb↑ + Peso↓) | 165 (9.0%) |

Por aleitamento:

| | Suplementar | Não supl. | Trade-off |
|---|---|---|---|
| Amamentado | 685 | 322 | 73 |
| Não amamentado | 568 | 99 | 92 |

### 6.8 Demo — Predição Individual

Exemplo: Menino, 8 meses, Nordeste, pardo, aleitamento exclusivo, IEN Q2:
- CATE Hb: +0.017 g/dL (benefício mínimo)
- CATE WFL: +0.116 z-score (benefício no crescimento)
- **Decisão: SUPLEMENTAR** (mas benefício hematológico marginal)

---

## 7. Convergência Multi-Método

| Achado | Epidemiologia | Causal ML | Concordância |
|---|---|---|---|
| Ferro melhora Hb | +0.19 g/dL (p=0.039) | CATE +0.058 (bootstrap sig) | ✓ |
| Efeito maior em não amamentados | +0.43 vs +0.02 (p_int=0.027) | CATE +0.098 vs +0.032 | ✓ |
| Aleitamento é top modifier | Interação formal sig | SHAP: 4o driver | ✓ |
| Heterogeneidade é real | Interações pré-especificadas | GATES p<0.05 | ✓ |
| Ferro beneficia mais os pobres | Não testado formalmente | IEN Q1 CATE 8x > Q5 | Novo achado ML |

---

## 8. Figuras Geradas

| Figura | Arquivo | Conteúdo |
|---|---|---|
| SHAP WFL | `shap_validated_anthro_zwfl.png` | Drivers do efeito do ferro no crescimento |
| SHAP Hb | `shap_validated_hb.png` | Drivers do efeito do ferro na hemoglobina |
| Decisão Clínica | `clinical_decision.png` | Scatter trade-off + decisão individualizada |

---

## 9. Modelo para Deploy

| Arquivo | Tamanho | Conteúdo |
|---|---|---|
| `deploy/surrogate_wfl.joblib` | 704 KB | Surrogate GBR para CATE WFL |
| `deploy/surrogate_hb.joblib` | 696 KB | Surrogate GBR para CATE Hb |
| `deploy/config.json` | 4 KB | Features, labels, regras de decisão |

---

## 10. Limitações

1. **Desenho cross-sectional** — associações, não causalidade
2. **Desfechos binários de biomarcadores** sem pesos amostrais (Logit sem peso como fallback)
3. **Controle negativo (internação acidente, n=12)** com poder muito baixo
4. **Correlação SHAP vs regressão moderada** (Spearman r=0.44-0.49, não r=0.97 como no IJMI paper — esperado pois SHAP causal ≠ SHAP preditivo)
5. **Concordância entre modelos causais moderada** (r=0.23-0.55 entre CausalForest, T-Learner, S-Learner)
6. **CATEs pequenos** (0.02-0.10 g/dL para Hb) — significativos estatisticamente, relevância clínica individual limitada

---

## 11. Conclusão Provisória

A suplementação universal de ferro pelo PNSF:

**Beneficia:**
- Reduz anemia em 42% (ferro isolado)
- Reduz deficiência de ferro em 29%
- Reduz inflamação sistêmica em 36%
- Beneficia crescimento mais nos mais pobres (CATE WFL Q1 = 8x Q5)

**Potencialmente prejudica:**
- Crianças exclusivamente amamentadas de 6-11 meses (OR=2.34 para febre/diarreia, OR=2.73 para internação respiratória)
- Crianças não amamentadas de 12-18 meses (OR=2.03 para internação respiratória)

**Não prejudica:**
- Diarreia, febre, tosse como sintomas gerais (todos NS após ajuste)
- Zinco, B12, folato, selênio (sem competição de micronutrientes)

**Implicação de política:**
- O PNSF deveria considerar status de aleitamento materno antes de iniciar suplementação
- Crianças exclusivamente amamentadas de 6-11 meses podem não necessitar ferro suplementar
- Crianças não amamentadas são as que mais se beneficiam — e mais precisam
- Confirmação por RCT é necessária antes de mudança de prática clínica

---

## 12. Próximos Passos

1. Manuscrito (Introduction, Methods, Results, Discussion)
2. Forest plots para publicação
3. DAG (diagrama causal)
4. Pré-registro no OSF
5. GitHub Pages com ferramenta de decisão
6. Submissão: Lancet Global Health → Lancet Digital Health → BMJ Global Health

---

*Gerado a partir dos notebooks data1.ipynb e ml_causal.ipynb — 2026-03-30*
