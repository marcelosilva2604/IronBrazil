# Template — Lancet Digital Health (Original Research)

Extraído de 5 artigos originais publicados no Lancet Digital Health (2025-2026).

---

## Título (22-28 palavras)

```
[Método ML] + [desfecho clínico] + [população/contexto] : a [descritivo do estudo]
```

Exemplos do journal:
- "The use of advanced machine learning to predict outcomes after atezolizumab plus bevacizumab for advanced hepatocellular carcinoma: a retrospective cohort study"
- "AI-enabled forecasting of prehospital transfusion needs in patients with trauma: a multinational, registry-based, retrospective, machine learning development and validation study"

**Nosso título sugerido:**
> "Causal machine learning to identify heterogeneous effects of iron supplementation on haematological, growth, and infectious morbidity outcomes in Brazilian infants: a nationally representative, cross-sectional, development and validation study"

---

## Summary (300-400 palavras)

Seções em bold:

**Background** (2-3 frases)
- Problema clínico + gap
- "We aimed to..."

**Methods** (3-5 frases)
- Desenho, população, dados
- Métodos ML
- Validação

**Findings** (5-10 frases — mais longa)
- Todos os resultados quantitativos: AUC (95% CI), OR, beta, p-values
- Densa em números

**Interpretation** (2-3 frases)
- Significado clínico
- Hedging: "could", "might", "supports the potential"

**Funding** (1 frase)

---

## Research in Context (obrigatório)

Painel estruturado logo após a Introduction:

**Evidence before this study**
- Busca PubMed OBRIGATÓRIA: databases, termos entre aspas, data range, N estudos encontrados
- Resumo do que a literatura mostra
- 150-200 palavras

**Added value of this study**
- "To our knowledge, this is the first..."
- O que este estudo adiciona
- 80-120 palavras

**Implications of all the available evidence**
- O que clínicos/policymakers devem extrair
- 80-120 palavras

---

## Introduction (600-900 palavras, 4-7 parágrafos)

1. **Burden**: problema clínico e carga global (com estatísticas)
2. **Current standard**: o que existe e suas limitações
3. **ML/AI potential**: como ML pode resolver, com 2-3 referências
4. **Knowledge gap**: o que NÃO foi feito
5. **Aim**: "We aimed to..." (último parágrafo)

**Tom**: autoritativo mas comedido. Sem hipérbole.
- "Despite the clear clinical benefit..."
- "However, these approaches are limited..."
- "To our knowledge, no studies to date have..."

---

## Methods (1500-2500 palavras)

### Subseções obrigatórias:

1. **Study design and participants**
   - Tipo de estudo, fonte de dados
   - Critérios de inclusão/exclusão
   - Aprovação ética (comitê, número CAAE)
   - Menção à Declaração de Helsinki
   - Aderência a guidelines: TRIPOD+AI, STROBE

2. **Data collection and procedures**
   - Variáveis, definições, codificação
   - Cutoffs usados (com referências)

3. **Machine learning model development**
   - TODOS os algoritmos testados (não só o vencedor)
   - Feature selection (métodos nomeados)
   - Hyperparameter tuning (grid search, CV)
   - Train/test split (ratio explícito)

4. **Interpretability analysis**
   - SHAP, permutation importance, ou outro
   - Surrogate R² se aplicável

5. **Statistical analysis**
   - Testes usados
   - Software com VERSÕES: "Python 3.12, scikit-learn 1.x, econml 0.14.6"
   - Significância: p < 0.05
   - Bootstrap iterations (n=1000)

6. **Role of the funding source**
   - SEMPRE presente
   - "The funders had no role in study design, data collection, analysis, interpretation, or writing."

---

## Results (1500-2500 palavras)

1. **Cohort description** + flow diagram (Figure 1)
   - N screened → N excluded (razões) → N included

2. **Baseline characteristics** (Table 1)
   - Training vs test, com p-valores

3. **Model performance** (Table 2)
   - AUC (95% CI) para TODOS os modelos testados
   - Comparação com benchmarks clínicos (DeLong test)

4. **Feature importance / SHAP**
   - Top features ranqueadas
   - SHAP summary plot (Figure)

5. **Risk stratification**
   - Grupos por quintil de CATE ou k-means
   - Kaplan-Meier se aplicável

6. **Subgroup / sensitivity analyses**
   - Por idade, sexo, geografia, temporal
   - Bootstrap CI para cada subgrupo

**Tom**: factual, denso em dados. Sem interpretação. Cada claim com número + CI.

---

## Discussion (1500-2000 palavras)

1. **Opening**: "In this study, we developed and validated..." ou "To our knowledge, this is the first..."
2. **Comparison with literature**: 2-3 parágrafos vs estudos prévios
3. **Mechanistic interpretation**: por que as features fazem sentido biológico/clínico
4. **Clinical applicability**: como a ferramenta pode ser deployada
5. **Strengths**: 1 parágrafo
6. **Limitations**: 5-8 itens explícitos. SEMPRE incluir:
   - Desenho retrospectivo/cross-sectional
   - Missing data
   - Limitação geográfica
   - Falta de validação prospectiva
   - Gaps demográficos (raça/etnia)
   - Aplicabilidade em LMIC
7. **Conclusion**: 3-5 frases. Restates finding + future direction. "These findings support...", "Further prospective validation is needed..."

---

## Figuras e Tabelas (5-6 no total)

| # | Conteúdo | Tipo |
|---|---|---|
| Fig 1 | Study flow / pipeline overview | Fluxograma |
| Fig 2 | Model comparison (ROC ou similar) | Performance |
| Fig 3 | SHAP / feature importance | Interpretabilidade |
| Fig 4 | Scatter trade-off ou decisão clínica | Aplicação |
| Table 1 | Baseline characteristics (train vs test) | Descritiva |
| Table 2 | Model performance metrics | Comparação |

Supplementary appendix extenso (20-30 páginas): tabelas adicionais, figuras, detalhes metodológicos.

---

## Referências

- 30-40 referências
- Vancouver format (numeradas)

---

## Seções Obrigatórias Adicionais

- **Contributors**: papel de cada autor por iniciais
- **Declaration of interests**: disclosures individuais
- **Data sharing**: statement de disponibilidade
- **Acknowledgments**: financiamento

---

## Convenções de Linguagem

| Regra | Exemplo |
|---|---|
| Inglês britânico | standardised, modelling, behaviour, tumour, centre |
| Hedging | "could", "might", "supports the potential" |
| Sem superlativos | nunca "breakthrough", "revolutionary" |
| "To our knowledge" | para claims de novidade |
| Foco no paciente | resultados em termos de impacto clínico, não métrica técnica |
| TRIPOD+AI | citar como guideline |
| Software versões | sempre especificar |
| CIs | "0.85 (95% CI 0.79-0.91)" |

---

## Checklist Pré-Submissão

- [ ] Título com 22-28 palavras + study design descriptor
- [ ] Summary com Background/Methods/Findings/Interpretation/Funding
- [ ] Research in Context com busca PubMed explícita
- [ ] Introduction termina com "We aimed to..."
- [ ] Methods cita TRIPOD+AI e ética
- [ ] Múltiplos algoritmos testados e reportados
- [ ] Holdout validation + bootstrap CI
- [ ] SHAP/interpretabilidade presente
- [ ] Equidade/demografia discutida
- [ ] Role of funding source no Methods
- [ ] 5-8 limitações explícitas no Discussion
- [ ] Inglês britânico throughout
- [ ] 30-40 referências Vancouver
- [ ] 5-6 figuras/tabelas
- [ ] Ferramenta/deploy mencionado
- [ ] DECIDE-AI citado se ferramenta clínica
- [ ] Supplementary appendix preparado
