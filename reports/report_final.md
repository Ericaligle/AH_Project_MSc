# Relatório final Ames Housing: Predição de Preços Residenciais  
**Dataset:** Ames Housing (Iowa) | **Amostras:** 2.930 | **Escopo:** Regressão e Classificação  

---

## 1. Análise de Dados Faltantes (Missing Analysis)

A estratégia de tratamento foi pautada na diferenciação entre ausência de informação e ausência de característica física.

### Tratamento de Dados Estruturais
Variáveis como `Garage Yr Blt`, `Garage Finish`, `Bsmt Qual` e `Fireplace Qu` apresentavam um alto volume de missings.  
A análise cruzada revelou que esses valores nulos coincidiam com `Garage Area = 0` ou `Total Bsmt SF = 0`.  

Portanto, os dados não estavam "faltando", mas indicavam que a casa não possuía garagem, porão ou lareira.

**Ação:**  
- Imputação de `0` para variáveis numéricas  
- Imputação de `'None'` para variáveis categóricas  

### Correções de Erros de Preenchimento (MCAR)

- **Índice 1356:** possuía garagem física, mas o ano de construção estava nulo.  
  → Utilizado `Year Built` como proxy  

- **Índice 2236:** indicava garagem no tipo, mas área zero.  
  → Corrigido para `None` e `0`  

### Variáveis Críticas
A variável `Electrical` possuía apenas um valor faltante, preenchido com a moda.

---

## 2. Análise Univariada e Seleção de Atributos

Nesta etapa, avaliou-se a variância e o poder preditivo individual de cada variável.

### Filtro de Baixa Variância
A variável `Heating` foi descartada, pois 98,46% das observações pertenciam à categoria `GasA`, não oferecendo sinal estatístico relevante.

### Agrupamento de Categorias Raras
Para evitar overfitting e explosão de dimensões no One-Hot Encoding:

- `Foundation` (Stone, Wood, Slab)
- `Exterior 1st` (BrkComm, AsphShn)

Essas categorias foram agrupadas como `'Outros'`.

### Tratamento de Outliers
Casas com `Gr Liv Area > 4000 sq ft` apresentaram comportamento de preço atípico.  
Esses pontos foram monitorados para evitar distorções em modelos lineares.

---

## 3. Correlações e Multicolinearidade

A análise de correlação de Pearson (numéricas) e de contingência (categóricas) guiou a engenharia de atributos.

### Colinearidade Crítica
Foi observada alta correlação entre:

- `1st Flr SF`
- `Total Bsmt SF` (0.80+)

**Ação:** priorização de variáveis agregadas de área para mitigar multicolinearidade.

### Associações Espúrias
A variável `Pool QC` foi descartada em sua forma original, pois apenas 13 casas possuíam piscina, gerando correlações artificiais.


### Consistência de Qualidade
Foi observada correlação de 0.55 entre:

- `Exter Qual`
- `Kitchen Qual`

Indicando que o padrão de acabamento tende a ser consistente em toda a residência.

---

## 4. Pré-processamento e Engenharia de Atributos

O Notebook 4 estabeleceu o pipeline de preparação dos dados para os modelos.

### Transformações
- Aplicação de logaritmo na área do lote (`log(Lot Area)`) para normalizar a distribuição  
- Redução de assimetria e melhor adequação aos modelos lineares  

### Codificação
- Variáveis qualitativas (`Exter`, `Bsmt`, `Kitchen`) transformadas em escalas ordinais (1 a 5)  
- Variáveis nominais com categorias raras agrupadas em `'Outros'`  

### Correlação
A análise do Notebook 3 revelou alta colinearidade entre áreas dos pavimentos e do porão.

**Ação:**  
- Seleção de atributos para evitar redundância  
- Priorização de variáveis agregadas  

---

## 5. Modelos de Regressão (L1 a L6)

Foram desenvolvidos seis modelos de regressão linear (*Ordinary Least Squares*) com complexidade crescente.

### L1 (Simples)
- Variável principal: `Gr Liv Area`  
- Foco na área habitável acima do solo  

### L2
- Adição da idade da propriedade  
- Captura do efeito de depreciação  

### L3 & L4
- Inclusão de variáveis de infraestrutura:  
  - Número de banheiros  
  - Número de lareiras  

### L5
- Inclusão de `Overall Qual`  
- Identificado como o preditor mais forte  

### L6 (Final)
- Inclusão de:
  - `log(Lot Area)`  
  - Estado de conservação  

### Justificativa do Modelo Final
O modelo L6 apresentou o melhor equilíbrio entre simplicidade e desempenho.

**Insights:**
- Qualidade e área total explicam a maior parte da variância  
- Número de banheiros adiciona valor marginal independente  

---

## 6. Modelos de Classificação (G1 a G6)

A tarefa de classificação utilizou Regressão Logística para prever faixas de preço.

### G1 & G2
- Variáveis básicas:
  - Área  
  - Presença de garagem  

### G3 & G4
- Inclusão de:
  - Qualidade  
  - Idade  

→ Melhor distinção entre casas de padrão **Baixo** e **Médio**

### G5
- Inclusão de:
  - Número de banheiros  
  - Tipo de porão  

### G6 (Final)
- Modelo mais robusto  
- Inclusão de:
  - `log(Lot Area)`  
  - Interações de qualidade  

### Resultado
O modelo G6 demonstrou que:

- `Kitchen Qual` perde significância estatística quando `Overall Qual` está presente  
- O padrão de acabamento é consistente em toda a residência  

---

## 7. Resultados Finais e Generalização

Os modelos finais (L6 e G6) foram validados em um conjunto de teste independente (Notebook 5).

### Resultados da Regressão (L6)

- **RMSE:** Indicou alta precisão nas previsões  
- **MAE:** Confirmou robustez contra outliers  

### Resultados da Classificação (G6)

- **Acurácia:** Alta taxa de acerto nas três faixas de preço  
- **F1-Score:** Bom equilíbrio entre precisão e recall  
- **ROC AUC:** Próximo de 1.0, indicando excelente capacidade de discriminação  

---

## 8. Conclusões

### Drivers de Preço
- `Overall Qual` e `Gr Liv Area` são os principais determinantes do valor imobiliário  

### Engenharia de Dados
- A transformação logarítmica de `Lot Area` é essencial para capturar seu impacto real  

### Simplificação do Modelo
- Variáveis específicas como `Kitchen Qual` podem ser removidas  
- `Overall Qual` já captura o padrão geral de acabamento  

Possibilita modelos mais simples e eficientes, além de otimizar futuras coletas de dados