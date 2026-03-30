# Resultados Parciais — Suplementação de Ferro em Lactentes Brasileiros (ENANI-2019)

**Data:** 2026-03-30 | **Status:** Análise exploratória concluída, pendente interação com aleitamento materno

---

## 1. Dados e População

- **Fonte:** ENANI-2019 (Estudo Nacional de Alimentação e Nutrição Infantil)
- **Amostra total:** 14.558 crianças, 741 variáveis
- **População do estudo:** 3.127 crianças de 6-18 meses
  - Grupo 6-11m: 1.415 crianças
  - Grupo 12-18m: 1.712 crianças
- **Prevalência da exposição:** 31.3% usam suplemento com ferro

## 2. Exposição

| Nível | Descrição | N (%) |
|---|---|---|
| 0 | Nenhum suplemento | 1.026 (32.8%) |
| 1 | Suplemento sem ferro | 1.123 (35.9%) |
| 2 | Ferro + outros (multivitamínico) | 131 (4.2%) |
| 3 | Ferro isolado (proxy do PNSF) | 847 (27.1%) |

## 3. Desfechos Avaliados

- 16 binários clínicos (sintomas 15 dias, internações, alergias)
- 6 binários derivados de biomarcadores (anemia, def. ferro, def. zinco, def. vit A, PCR elevada, anemia ferropriva)
- 29 contínuos (hemograma completo, micronutrientes, z-scores de crescimento)
- 1 controle negativo (internação por acidente)
- **Total: 52 desfechos**

## 4. Métodos Estatísticos

- **Teste bruto:** Chi² (binários), Mann-Whitney (contínuos)
- **Teste estratificado:** Chi², Kruskal-Wallis (4 níveis de exposição)
- **Regressão ajustada:** Poisson modificado (Zou 2004) com SEs robustos para binários; WLS com SEs cluster-robustos para contínuos
- **Confounders (25):** idade, sexo, cor/raça, região, urbano/rural, escolaridade materna, IEN, EBIA, saneamento, água, tipo de parto, idade gestacional, peso ao nascer, consultas pré-natal, idade materna, aleitamento materno, fórmula infantil
- **Verificação de co-suplementação:** comparação ferro isolado vs nenhum suplemento

## 5. Resultados

### 5.1 Análise Bruta (não ajustada)
- **20 de 52 desfechos significativos** (ferro sim vs não)
- Padrão dominante: confounding por healthcare-seeking (crianças que recebem suplementos frequentam mais o sistema de saúde)
- Gradiente dose-resposta limpo para índices hematológicos no teste de 4 níveis

### 5.2 Análise Ajustada — iron_any (qualquer ferro, n=3.127)

**Associações com benefício (p<0.05):**

| Desfecho | Efeito | IC 95% | p |
|---|---|---|---|
| Anemia (Hb<10.5) | OR=0.69 | 0.51-0.94 | 0.019 |
| Deficiência de ferro (Ferri<12) | OR=0.74 | 0.58-0.94 | 0.015 |
| Deficiência de vit A (<0.20 mg/L) | OR=0.59 | 0.40-0.86 | 0.007 |
| PCR elevada (>5 mg/L) | OR=0.67 | 0.49-0.91 | 0.012 |
| Hemoglobina | +0.19 g/dL | 0.01-0.37 | 0.039 |
| Hematócrito | +0.69% | 0.13-1.24 | 0.016 |

**Associações com dano (p<0.05):**

| Desfecho | Efeito | IC 95% | p |
|---|---|---|---|
| Z peso/comprimento (WFL) | -0.18 z | -0.36 a -0.005 | 0.043 |

**Borderline (0.05 ≤ p < 0.10):**

| Desfecho | Efeito | IC 95% | p |
|---|---|---|---|
| Internação intestinal | PR=2.39 | 0.99-5.79 | 0.053 |
| Anemia ferropriva | OR=0.69 | 0.45-1.05 | 0.082 |
| Z peso/idade (WAZ) | -0.16 z | -0.33 a 0.01 | 0.060 |
| Z IMC/idade (BAZ) | -0.17 z | -0.36 a 0.004 | 0.055 |

**Sem diferença estatística:** diarreia, febre, tosse, dispneia, nariz entupido, ronqueira, zinco, B12, folato, vitaminas B1/B6/D/E, selênio, crescimento linear (HAZ), leucócitos, neutrófilos, bastonetes, plaquetas, linfócitos, monócitos.

### 5.3 Verificação: Ferro Isolado (PNSF) vs Nenhum Suplemento

Comparação restrita a ferro isolado (n=847) vs nenhum suplemento (n=1.026) para separar efeito do ferro de co-suplementação:

| Desfecho | iron_any (todos) | Ferro isolado | Veredicto |
|---|---|---|---|
| Anemia | OR=0.69, p=0.019 | **OR=0.58, p=0.005** | Efeito real, mais forte |
| Def. ferro | OR=0.74, p=0.015 | **OR=0.71, p=0.026** | Efeito real |
| PCR elevada | OR=0.67, p=0.012 | **OR=0.64, p=0.023** | Efeito real |
| Def. vit A | OR=0.59, p=0.007 | OR=0.66, **p=0.085** | **Era co-suplementação** |

## 6. Interpretação Provisória

### Benefícios reais do ferro (confirmados com ferro isolado):
- Reduz prevalência de anemia em 42%
- Reduz deficiência de ferro em 29%
- Associado a menor inflamação sistêmica (36% menos PCR elevada)

### Possíveis danos:
- Associado a menor z-score peso/comprimento (-0.18, p=0.043), consistente com Iannotti et al. 2006 (AJCN)
- Tendência a maior internação por infecção intestinal (PR=2.39, p=0.053), consistente com Sazawal et al. 2006 (Lancet)

### Sem diferença estatística para morbidade infecciosa:
- Diarreia, febre, tosse, dispneia — todos sem associação após ajuste
- Contrasta com achados em settings endêmicos de malária na África

### Achado metodológico:
- Proteção aparente de vitamina A era artefato de co-suplementação com multivitamínicos, não efeito do ferro

## 7. Limitações até o momento

1. Desenho cross-sectional — associações, não causalidade
2. Desfechos binários de biomarcadores rodaram sem pesos amostrais (limitação técnica do statsmodels)
3. Controle negativo (internação por acidente, n=12) com poder muito baixo
4. Não testada ainda interação com aleitamento materno
5. Não estratificado por faixa etária (6-11m vs 12-18m)
6. Sem análise de sensibilidade (IPTW, E-values)

## 8. Próximos Passos

1. **Interação ferro x aleitamento materno** — hipótese da lactoferrina
2. **Estratificação por grupo etário** (6-11m vs 12-18m)
3. **Propensity score (IPTW)** como sensibilidade
4. **Table 1** descritiva
5. **Forest plot** e figuras para publicação
6. **Manuscrito**

---

*Gerado automaticamente a partir do notebook data1.ipynb*
