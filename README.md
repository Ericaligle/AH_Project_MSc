# Ames Housing Project: Pipeline de Análise Preditiva
Estruturação de Workflow e Modelagem de Dados Imobiliários

## Visão Geral e Objetivos
Este repositório implementa um pipeline end-to-end de Ciência de Dados aplicado ao mercado imobiliário de Ames (Iowa). Mais do que buscar a performance isolada de um algoritmo, este projeto prioriza o desenvolvimento de uma arquitetura de software robusta e reprodutível, garantindo a integridade de cada etapa analítica, do dado bruto ao insight final.

A abordagem aqui é baseada na governança dos dados: transformar informações complexas em um fluxo modularizado e bem documentado, capaz de sustentar investigações profundas sobre os determinantes de valor das propriedades residenciais e fornecer uma base sólida para modelos de regressão avançada.

### Objetivos Estratégicos:
**Modularização de Processos**: Implementar um scaffolding (arquitetura de pastas) que separe responsabilidades e proteja a integridade dos dados originais.

**Qualidade Analítica**: Aplicar métodos rigorosos de limpeza e tratamento de variáveis, tratando cada atributo sob a ótica de domínio de mercado.

**Documentação Técnica**: Assegurar que o experimento seja 100% replicável através de um ambiente virtual isolado e gestão transparente de dependências.

## Estrutura do Projeto (Scaffolding)
A organização do diretório foi planejada para separar as etapas de processamento e proteger a integridade dos dados originais:

`data/raw/` : Armazena o dataset original e imutável.

`data/processed/`: Repositório para os dados limpos e prontos para modelagem.

`notebooks/`: Onde reside o AH_project.ipynb para experimentação e análise exploratória (EDA).
 
`src/`: Pasta para scripts Python e funções auxiliares que mantêm os notebooks limpos.

`reports/figures/`: Exportação de gráficos e visualizações geradas para o relatório final.

`requirements.txt`: Registro de todas as bibliotecas necessárias para o projeto.

```
Ames_Housing_Project/
├── .venv/             # Ambiente virtual isolado (Python)
├── data/
│   ├── raw/           # Datasets originais e imutáveis
│   └── processed/     # Dados limpos e transformados para modelagem
├── notebooks/         # Laboratório de experimentação e EDA
│   └── AH_project.ipynb
├── reports/
│   └── figures/       # Gráficos e visualizações exportadas
├── src/               # Scripts Python e funções auxiliares
├── .gitignore         # Filtro de arquivos para versionamento
├── README.md          # Documentação principal do projeto
└── requirements.txt   # Lista de dependências do projeto
```


## Configuração do Ambiente e Reprodutibilidade
Para garantir que o projeto execute corretamente em qualquer máquina, siga os passos abaixo. Estas instruções assumem que você já possui o Python 3.x instalado.

### **1. Clonar o Repositório**
Primeiro, baixe o projeto para a sua máquina local:

```
git clone https://github.com/Ericaligle/AH_Project_MSc.git
cd Ames_Housing_Project
``` 
### **2. Configurar o Ambiente Virtual**

Recomenda-se o uso de um ambiente isolado para evitar conflitos de versões entre bibliotecas:

```
Windows:

python -m venv .venv
.venv\Scripts\activate
``` 

```
macOS/Linux:

python -m venv .venv
source .venv/bin/activate
```
(Ao ativar, você deverá ver o prefixo (.venv) no seu terminal).


### **3. Instalar Dependências**

Com o ambiente ativo, instale todas as bibliotecas necessárias listadas no arquivo requirements.txt:

```
pip install -r requirements.txt
```

## Fonte e Estrutura dos Dados (Data Source & Structure)
A base de dados utilizada neste projeto é o Ames Housing Dataset, um conjunto de dados amplamente reconhecido na comunidade de Ciência de Dados por sua riqueza de detalhes e complexidade estatística.

### **Origem e Contexto**

Os dados foram originalmente compilados por Dean De Cock para fins educacionais e são frequentemente acessados via repositórios públicos (como o Kaggle ou o UCI Machine Learning Repository). O dataset descreve transações imobiliárias residenciais ocorridas em Ames, Iowa, entre os anos de 2006 e 2010.

### **Estrutura e Formato**

* **Formato do Arquivo**: Os dados brutos estão armazenados em formato `.csv` (Comma-Separated Values) dentro da pasta data/raw/.

* **Dimensões**: O conjunto de dados original contém 2.930 observações (imóveis) distribuídas em 82 variáveis (atributos).

* **Tipagem dos Dados**: A base apresenta uma estrutura multimodal, composta por:

     * 43 Variáveis Categóricas (Nominais e Ordinais): Descrevem aspectos qualitativos como o tipo da vizinhança, qualidade do acabamento e tipo de acesso (pavimentado ou não).

    * 39 Variáveis Numéricas (Discretas e Contínuas): Incluem medidas de área (ft²), contagem de cômodos, anos de construção e o valor final de venda (`SalePrice`).

### **Descrição das Variáveis Chave**

As variáveis fornecem um detalhamento granular da propriedade, abrangendo:

* **Características do Terreno**: Área do lote (`Lot Area`), configuração do lote e topografia.

* **Qualidade e Condição**: Índices de avaliação da estrutura geral e estado de conservação (`Overall Qual` e `Overall Cond`).

* **Dimensões Internas**: Metragem dos andares, porão e áreas de garagem.

* **Localização**: Zoneamento urbano e identificação de bairros específicos.


## Inspeção Inicial dos Dados (Initial Data Inspection)

Esta etapa documenta o primeiro contato com o dataset, onde realizamos um diagnóstico de saúde dos dados para orientar as estratégias de limpeza e modelagem.

### **1. Classificação e Tipagem (Data Type Classification)**
Uma análise preliminar via df.info() revelou a heterogeneidade do dataset. A conversão correta dos tipos é fundamental para evitar erros em cálculos estatísticos:

* **Numéricos**: Identificamos variáveis contínuas (ex: Lot `Frontage`) e discretas (ex: `Fireplaces`).

* **Categóricos**: Diferenciamos variáveis nominais (ex: *Neighborhood*) de ordinais (ex: `Exter Qual`), que possuem uma hierarquia lógica (Excellent > Good > Average).

### **2. Estatísticas Resumo (Summary Statistics)**

**Variáveis Numéricas**

Para os atributos quantitativos, focamos na dispersão e tendência central. Notamos uma grande variabilidade em medidas de área, sugerindo um mercado imobiliário heterogêneo.

| Variável    | Média     | Desvio Padrão | Mín    | Máx   |
|-------------|-----------|---------------|--------|-------|
| SalePrice   | 180,796.1 | 79,886.7      | 12,789 | 755   |
| Gr Liv Area | 1,499.7   | 505.5         | 334    | 5,642 |

A tabela completa pode ser visualizada em: `reports\data_dictionary_numeric.md`

**Variáveis Categóricas**

Para os atributos qualitativos, analisamos a frequência e a dominância de certas categorias. Isso nos ajuda a entender o "perfil padrão" das casas em Ames.

| Variável     | Categ. Únicas | Top (Moda) | Freq. da Moda | % de Dominância |
|--------------|---------------|------------|---------------|-----------------|
| Neighborhood | 28            | NAmes      | 443           | 15.1%           |
| House Style  | 8             | 1Story     | 1481          | 50.5%           |
| MS Zoning    | 7             | RL         | 2273          | 77.5%           |
| Foundation   | 6             | PConc      | 1310          | 44.7%           |

A tabela completa pode ser visualizada em: `reports\data_dictionary_categorical.md`

### **3. Análise de Dados Faltantes (Missing Value Analysis)**

A inspeção revelou que o dataset de Ames possui um volume significativo de valores ausentes (NaN), mas com naturezas distintas:

* **Ausência Informativa**: Variáveis como `Pool QC`, `Misc Feature` e `Alley` apresentam mais de 90% de valores nulos. Na maioria dos casos, isso indica a inexistência do atributo no imóvel, e não um erro de coleta.

* **Lacunas de Dados**: Variáveis como `Lot Frontage` (~16% missing) sugerem a necessidade de técnicas de imputação (como o uso da mediana da vizinhança).


---

## 9. Padrões e Irregularidades (Notable Patterns)

Durante a análise exploratória (EDA) e estatística, foram observados comportamentos que exigiram intervenções estratégicas no pipeline de dados.

### Assimetria (Skewness) e Normalização
A variável alvo `SalePrice` e a variável preditora `Lot Area` apresentaram distribuições assimétricas à direita.

**Ação:**
- Aplicação de transformações logarítmicas:
  - `log(SalePrice)`
  - `log(Lot Area)`

**Resultado:**
- Distribuições mais próximas da normalidade  
- Redução do impacto de valores extremos  
- Estabilização da variância dos resíduos  
- Coeficientes de regressão mais confiáveis  

---

### Outliers Críticos
Foram identificados imóveis com área extremamente elevada:

- `Gr Liv Area > 4000 ft²`  
- Preços desproporcionais  

**Ação:**
- Isolamento ou tratamento desses pontos  

**Justificativa:**
- Evitar distorções na linha de tendência  
- Representam transações atípicas no mercado de Ames  

---

### Multicolinearidade de Áreas
A análise de correlação revelou redundâncias severas entre atributos de área.

**Exemplo:**
- `1st Flr SF`
- `Total Bsmt SF` (correlação > 0.80)

**Ação:**
- Priorização de variáveis agregadas de área habitável  

**Objetivo:**
- Reduzir inflação de variância (VIF alto)  
- Melhorar estabilidade dos coeficientes  

---

### Determinantes de Qualidade
A variável `Overall Qual` foi identificada como o preditor mais forte do dataset.

**Observação:**
- `Kitchen Qual` apresentou alta colinearidade com `Overall Qual`  

**Insight:**
- O padrão de acabamento tende a ser uniforme na residência  

**Impacto:**
- Possibilidade de simplificação do modelo  
- Redução de redundância sem perda significativa de acurácia  

---

### Variância Insuficiente
A variável `Heating` apresentou concentração extrema:

- ~99% na categoria `GasA`

**Ação:**
- Remoção do modelo  

**Justificativa:**
- Baixo poder discriminativo  
- Ausência de sinal estatístico relevante  

---

### Associações Espúrias (Pool QC)
A variável `Pool QC` apresentou baixa representatividade:

- Apenas 13 imóveis com piscina  

**Problema:**
- Geração de correlações artificiais  

**Ação:**
- Conversão para variável binária: `has_pool`  

**Resultado:**
- Redução de ruído  
- Representação mais robusta da característica 

📊 Resumo Executivo (Executive Summary)

- **Principal Insight:**  
  A variável `Overall Qual` (Qualidade Geral) é o principal driver de valor. Imóveis com acabamento superior superam propriedades maiores com acabamento médio.

- **Regressão (Modelo L6):**  
  - RMSE: **43,882.48**  
  - MAE: **28,628.46**  
  → Modelo capaz de estimar preços com boa precisão, considerando a variabilidade do mercado.

- **Classificação (Modelo G5):**  
  - Acurácia: **69.55%**  
  - F1-Score: **0.6929**  
  - ROC AUC: **0.8465**  
  → Boa capacidade de segmentação entre imóveis de baixo, médio e alto padrão.

- **Diferencial Técnico:**  
  Uso de transformações logarítmicas e controle de multicolinearidade, garantindo modelos **interpretáveis e estatisticamente robustos**.

---

## 🧱 Estrutura do Pipeline

O projeto é modularizado em etapas para garantir reprodutibilidade e clareza analítica:

1. **Auditoria de Dados** (`1.Missing_analisys.ipynb`)  
   - Tratamento de 2.930 observações  
   - Imputação lógica para ausência estrutural (garagem, porão, etc.)  
   - Correções pontuais com uso de proxy  

2. **Filtragem de Sinal** (`2.Univariate_analisys.ipynb`)  
   - Remoção de variáveis com baixa variância (ex: `Heating`)  
   - Identificação e controle de outliers (`Gr Liv Area > 4000`)  

3. **Engenharia de Atributos** (`3.Correlation_analisys.ipynb`)  
   - Identificação de multicolinearidade  
   - Conversão de variáveis ordinais (escala 1–5)  

4. **Processamento** (`4.Processing.ipynb`)  
   - Pipeline com `StandardScaler`, `OneHotEncoder`  
   - Transformações logarítmicas (`log(SalePrice)`, `log(Lot Area)`)  

5. **Modelagem e Validação** (`5.Modeling.ipynb`)  
   - Treinamento de modelos  
   - Avaliação em conjunto de teste independente  

---

## 🤖 Modelagem Preditiva

### 📈 Regressão (Estimativa de Preço)

Modelos desenvolvidos: **L1 a L6**

- **L1–L2:** Baselines (área e idade)  
- **L3–L5:** Inclusão de infraestrutura (banheiros, lareiras)  
- **L6 (Final):**
  - `Overall Qual`
  - `Gr Liv Area`
  - `log(Lot Area)`
  - Estado de conservação  

→ Melhor equilíbrio entre simplicidade, interpretabilidade e desempenho.

---

### 🏷️ Classificação (Segmentação de Mercado)

Modelos desenvolvidos: **G1 a G5**

- **G1–G2:** Variáveis básicas (área, garagem)  
- **G3–G4:** Inclusão de qualidade e idade  
- **G5 (Final):**
  - Variáveis estruturais + qualidade + área do lote  
  - Melhor desempenho no conjunto de teste  

→ Modelo robusto para segmentação de mercado imobiliário.

---

## 📊 Resultados e Métricas

Performance avaliada em conjunto de teste (dados não vistos):

| Tarefa         | Modelo | Métrica   | Resultado |
|---------------|--------|----------|----------|
| Regressão     | L6     | RMSE     | 43,882.48 |
| Regressão     | L6     | MAE      | 28,628.46 |
| Classificação | G5     | Acurácia | 0.6955 |
| Classificação | G5     | F1-Score | 0.6929 |
| Classificação | G5     | ROC AUC  | 0.8465 |

---

## 📈 Interpretação dos Resultados

### Regressão (L6)
- Erro médio de aproximadamente **$28 mil**
- Sensível a imóveis de alto valor (outliers)
- Boa captura da tendência geral de preços  

### Classificação (G5)
- Acurácia próxima de **70%**, adequada para segmentação  
- F1-score equilibrado entre precisão e recall  
- ROC AUC indica **boa separação entre classes**  

---

## 🔍 Padrões e Irregularidades (Notable Patterns)

### Assimetria (Skewness)
- Aplicação de:
  - `log(SalePrice)`
  - `log(Lot Area)`  

→ Redução de outliers e melhor ajuste aos modelos lineares  

---

### Multicolinearidade
- Correlação > 0.80 entre:
  - `1st Flr SF`
  - `Total Bsmt SF`  

→ Uso de variáveis agregadas para evitar inflação de variância  

---

### Redundância de Qualidade
- `Kitchen Qual` torna-se redundante com `Overall Qual`  

→ Permite simplificação do modelo sem perda relevante  

---

## 💡 Insights de Negócio

- **Qualidade > Tamanho:**  
  Melhorar acabamento gera mais valor do que aumentar área  

- **Segmentação de Mercado:**  
  Área do lote ajuda a distinguir imóveis de alto padrão  

- **Eficiência Operacional:**  
  Poucas variáveis explicam grande parte do preço  
  → Redução de custo em futuras coletas  

---

## ⚠️ Limitações e Próximos Passos

### Limitações
- Modelo específico para Ames (Iowa)  
- Não considera fatores macroeconômicos  

### Roadmap
- Testar modelos não-lineares (Random Forest, XGBoost)  
- Implementar API para previsão de preços  
- Melhorar validação com cross-validation  

---

## 🛠️ Tecnologias e Stack

- **Linguagem:** Python 3.x  
- **Análise:** Pandas, NumPy, Scipy  
- **Modelagem:** Statsmodels, Scikit-learn  
- **Visualização:** Matplotlib, Seaborn  