# Ames Housing Project: Pipeline de Análise Preditiva
Estruturação de Workflow e Modelagem de Dados Imobiliários

## 📖 Visão Geral e Objetivos
Este repositório implementa um pipeline end-to-end de Ciência de Dados aplicado ao mercado imobiliário de Ames (Iowa). Mais do que buscar a performance isolada de um algoritmo, este projeto prioriza o desenvolvimento de uma arquitetura de software robusta e reprodutível, garantindo a integridade de cada etapa analítica, do dado bruto ao insight final.

A abordagem aqui é baseada na governança dos dados: transformar informações complexas em um fluxo modularizado e bem documentado, capaz de sustentar investigações profundas sobre os determinantes de valor das propriedades residenciais e fornecer uma base sólida para modelos de regressão avançada.

### Objetivos Estratégicos:
**Modularização de Processos**: Implementar um scaffolding (arquitetura de pastas) que separe responsabilidades e proteja a integridade dos dados originais.

**Qualidade Analítica**: Aplicar métodos rigorosos de limpeza e tratamento de variáveis, tratando cada atributo sob a ótica de domínio de mercado.

**Documentação Técnica**: Assegurar que o experimento seja 100% replicável através de um ambiente virtual isolado e gestão transparente de dependências.

## 🏗️ Estrutura do Projeto (Scaffolding)
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


## 🛠️ Configuração do Ambiente e Reprodutibilidade
Para garantir que o projeto execute corretamente em qualquer máquina, siga os passos abaixo. Estas instruções assumem que você já possui o Python 3.x instalado.

**1. Clonar o Repositório**
Primeiro, baixe o projeto para a sua máquina local:

```
git clone https://github.com/Ericaligle/AH_Project_MSc.git
cd Ames_Housing_Project
``` 
**2. Configurar o Ambiente Virtual**

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


**3. Instalar Dependências**

Com o ambiente ativo, instale todas as bibliotecas necessárias listadas no arquivo requirements.txt:

```
pip install -r requirements.txt
```

## 📊 Fonte e Estrutura dos Dados (Data Source & Structure)
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

_Nota de Contexto: Esta riqueza de variáveis permite uma investigação profunda sobre a multicolinearidade (como a relação entre o ano de construção e a qualidade dos materiais) e o impacto de fatores externos no preço final dos imóveis._

## 🔍 Inspeção Inicial dos Dados (Initial Data Inspection)

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


### **4. Padrões e Irregularidades (Notable Patterns)**

Durante a análise exploratória (EDA), observamos comportamentos que exigem atenção especial:

**Assimetria (Skewness)**: A variável alvo `SalePrice` apresenta uma distribuição assimétrica à direita, o que pode exigir uma transformação logarítmica para normalização.

**Outliers**: Identificamos imóveis com metragens extremamente altas (`Gr Liv Area` > 4000 ft²) que não acompanham o crescimento proporcional do preço, agindo como pontos fora da curva.