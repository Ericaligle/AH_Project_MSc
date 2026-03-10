| Variável        | Descrição (Tradução)                                              | number of values | % of missing values | unique values | Tipo       | Classificação | dtype   |
|-----------------|-------------------------------------------------------------------|------------------|---------------------|---------------|------------|---------------|---------|
| Order           | Número da observação.                                             | 2930             | 0.00%               | 2930          | Numérica   | Discreta      | int64   |
| PID             | Número de identificação da parcela (vinculado ao site da cidade). | 2930             | 0.00%               | 2930          | Categórica | Nominal       | int64   |
| MS SubClass     | Identifica o tipo de habitação envolvida na venda.                | 2930             | 0.00%               | 16            | Categórica | Nominal       | int64   |
| MS Zoning       | Identifica a classificação de zoneamento geral da venda.          | 2930             | 0.00%               | 7             | Categórica | Nominal       | str     |
| Lot Frontage    | Pés lineares de rua conectados à propriedade.                     | 2440             | 16.72%              | 128           | Numérica   | Contínua      | float64 |
| Lot Area        | Tamanho do lote em pés quadrados.                                 | 2930             | 0.00%               | 1960          | Numérica   | Contínua      | int64   |
| Street          | Tipo de acesso rodoviário à propriedade.                          | 2930             | 0.00%               | 2             | Categórica | Nominal       | str     |
| Alley           | Tipo de acesso por beco à propriedade.                            | 198              | 93.24%              | 2             | Categórica | Nominal       | str     |
| Lot Shape       | Formato geral da propriedade.                                     | 2930             | 0.00%               | 4             | Categórica | Ordinal       | str     |
| Land Contour    | Nivelamento da propriedade.                                       | 2930             | 0.00%               | 4             | Categórica | Nominal       | str     |
| Utilities       | Tipo de utilitários disponíveis (água, luz, etc.).                | 2930             | 0.00%               | 3             | Categórica | Ordinal       | str     |
| Lot Config      | Configuração do lote.                                             | 2930             | 0.00%               | 5             | Categórica | Nominal       | str     |
| Land Slope      | Inclinação da propriedade.                                        | 2930             | 0.00%               | 3             | Categórica | Ordinal       | str     |
| Neighborhood    | Localização física dentro dos limites da cidade de Ames.          | 2930             | 0.00%               | 28            | Categórica | Nominal       | str     |
| Condition 1     | Proximidade de várias condições (vias, ferrovias, etc.).          | 2930             | 0.00%               | 9             | Categórica | Nominal       | str     |
| Condition 2     | Proximidade de várias condições (se houver mais de uma).          | 2930             | 0.00%               | 8             | Categórica | Nominal       | str     |
| Bldg Type       | Tipo de habitação.                                                | 2930             | 0.00%               | 5             | Categórica | Nominal       | str     |
| House Style     | Estilo da habitação.                                              | 2930             | 0.00%               | 8             | Categórica | Nominal       | str     |
| Overall Qual    | Avalia o material e acabamento geral da casa.                     | 2930             | 0.00%               | 10            | Categórica | Ordinal       | int64   |
| Overall Cond    | Avalia a condição geral da casa.                                  | 2930             | 0.00%               | 9             | Categórica | Ordinal       | int64   |
| Year Built      | Data original da construção.                                      | 2930             | 0.00%               | 118           | Numérica   | Discreta      | int64   |
| Year Remod/Add  | Data da reforma (igual à construção se não houver reforma).       | 2930             | 0.00%               | 61            | Numérica   | Discreta      | int64   |
| Roof Style      | Tipo de telhado.                                                  | 2930             | 0.00%               | 6             | Categórica | Nominal       | str     |
| Roof Matl       | Material do telhado.                                              | 2930             | 0.00%               | 8             | Categórica | Nominal       | str     |
| Exterior 1      | Cobertura externa da casa.                                        | 2930             | 0.00%               | 16            | Categórica | Nominal       | str     |
| Exterior 2      | Segunda cobertura externa (se houver).                            | 2930             | 0.00%               | 17            | Categórica | Nominal       | str     |
| Mas Vnr Type    | Tipo de revestimento de alvenaria.                                | 1155             | 60.58%              | 4             | Categórica | Nominal       | str     |
| Mas Vnr Area    | Área do revestimento de alvenaria em pés quadrados.               | 2907             | 0.78%               | 445           | Numérica   | Contínua      | float64 |
| Exter Qual      | Avalia a qualidade do material no exterior.                       | 2930             | 0.00%               | 4             | Categórica | Ordinal       | str     |
| Exter Cond      | Avalia a condição atual do material no exterior.                  | 2930             | 0.00%               | 5             | Categórica | Ordinal       | str     |
| Foundation      | Tipo de fundação.                                                 | 2930             | 0.00%               | 6             | Categórica | Nominal       | str     |
| Bsmt Qual       | Avalia a altura do porão.                                         | 2850             | 2.73%               | 5             | Categórica | Ordinal       | str     |
| Bsmt Cond       | Avalia a condição geral do porão.                                 | 2850             | 2.73%               | 5             | Categórica | Ordinal       | str     |
| Bsmt Exposure   | Refere-se a paredes no nível do jardim ou saída direta.           | 2847             | 2.83%               | 4             | Categórica | Ordinal       | str     |
| BsmtFin Type 1  | Classificação da área acabada do porão.                           | 2850             | 2.73%               | 6             | Categórica | Ordinal       | str     |
| BsmtFin SF 1    | Área acabada do tipo 1 em pés quadrados.                          | 2929             | 0.03%               | 995           | Numérica   | Contínua      | float64 |
| BsmtFin Type 2  | Classificação da segunda área acabada (se houver).                | 2849             | 2.76%               | 6             | Categórica | Ordinal       | str     |
| BsmtFin SF 2    | Área acabada do tipo 2 em pés quadrados.                          | 2929             | 0.03%               | 274           | Numérica   | Contínua      | float64 |
| Bsmt Unf SF     | Área inacabada do porão em pés quadrados.                         | 2929             | 0.03%               | 1137          | Numérica   | Contínua      | float64 |
| Total Bsmt SF   | Área total do porão em pés quadrados.                             | 2929             | 0.03%               | 1058          | Numérica   | Contínua      | float64 |
| Heating         | Tipo de aquecimento.                                              | 2930             | 0.00%               | 6             | Categórica | Nominal       | str     |
| HeatingQC       | Qualidade e condição do aquecimento.                              | 2930             | 0.00%               | 5             | Categórica | Ordinal       | str     |
| Central Air     | Possui ar condicionado central.                                   | 2930             | 0.00%               | 2             | Categórica | Nominal       | str     |
| Electrical      | Sistema elétrico.                                                 | 2929             | 0.03%               | 5             | Categórica | Ordinal       | str     |
| 1st Flr SF      | Área do primeiro andar em pés quadrados.                          | 2930             | 0.00%               | 1083          | Numérica   | Contínua      | int64   |
| 2nd Flr SF      | Área do segundo andar em pés quadrados.                           | 2930             | 0.00%               | 635           | Numérica   | Contínua      | int64   |
| Low Qual Fin SF | Área acabada de baixa qualidade (todos os andares).               | 2930             | 0.00%               | 36            | Numérica   | Contínua      | int64   |
| Gr Liv Area     | Área de estar acima do solo (ground) em pés quadrados.            | 2930             | 0.00%               | 1292          | Numérica   | Contínua      | int64   |
| Bsmt Full Bath  | Banheiros completos no porão.                                     | 2928             | 0.07%               | 4             | Numérica   | Discreta      | float64 |
| Bsmt Half Bath  | Lavabos (meio banheiro) no porão.                                 | 2928             | 0.07%               | 3             | Numérica   | Discreta      | float64 |
| Full Bath       | Banheiros completos acima do solo.                                | 2930             | 0.00%               | 5             | Numérica   | Discreta      | int64   |
| Half Bath       | Lavabos acima do solo.                                            | 2930             | 0.00%               | 3             | Numérica   | Discreta      | int64   |
| Bedroom         | Quartos acima do solo (não inclui porão).                         | 2930             | 0.00%               | 8             | Numérica   | Discreta      | int64   |
| Kitchen         | Cozinhas acima do solo.                                           | 2930             | 0.00%               | 4             | Numérica   | Discreta      | int64   |
| KitchenQual     | Qualidade da cozinha.                                             | 2930             | 0.00%               | 5             | Categórica | Ordinal       | str     |
| TotRmsAbvGrd    | Total de cômodos acima do solo (não inclui banheiros).            | 2930             | 0.00%               | 14            | Numérica   | Discreta      | int64   |
| Functional      | Funcionalidade da casa.                                           | 2930             | 0.00%               | 8             | Categórica | Ordinal       | str     |
| Fireplaces      | Número de lareiras.                                               | 2930             | 0.00%               | 5             | Numérica   | Discreta      | int64   |
| FireplaceQu     | Qualidade da lareira.                                             | 1508             | 48.53%              | 5             | Categórica | Ordinal       | str     |
| Garage Type     | Localização da garagem.                                           | 2773             | 5.36%               | 6             | Categórica | Nominal       | str     |
| Garage Yr Blt   | Ano de construção da garagem.                                     | 2771             | 5.43%               | 103           | Numérica   | Discreta      | float64 |
| Garage Finish   | Acabamento interno da garagem.                                    | 2771             | 5.43%               | 3             | Categórica | Ordinal       | str     |
| Garage Cars     | Capacidade de carros na garagem.                                  | 2929             | 0.03%               | 6             | Numérica   | Discreta      | float64 |
| Garage Area     | Tamanho da garagem em pés quadrados.                              | 2929             | 0.03%               | 603           | Numérica   | Contínua      | float64 |
| Garage Qual     | Qualidade da garagem.                                             | 2771             | 5.43%               | 5             | Categórica | Ordinal       | str     |
| Garage Cond     | Condição da garagem.                                              | 2771             | 5.43%               | 5             | Categórica | Ordinal       | str     |
| Paved Drive     | Se a calçada da garagem é pavimentada.                            | 2930             | 0.00%               | 3             | Categórica | Ordinal       | str     |
| Wood Deck SF    | Área de deck de madeira em pés quadrados.                         | 2930             | 0.00%               | 380           | Numérica   | Contínua      | int64   |
| Open Porch SF   | Área de varanda aberta em pés quadrados.                          | 2930             | 0.00%               | 252           | Numérica   | Contínua      | int64   |
| Enclosed Porch  | Área de varanda fechada em pés quadrados.                         | 2930             | 0.00%               | 183           | Numérica   | Contínua      | int64   |
| 3-Ssn Porch     | Área de varanda de três estações em pés quadrados.                | 2930             | 0.00%               | 31            | Numérica   | Contínua      | int64   |
| Screen Porch    | Área de varanda com tela em pés quadrados.                        | 2930             | 0.00%               | 121           | Numérica   | Contínua      | int64   |
| Pool Area       | Área da piscina em pés quadrados.                                 | 2930             | 0.00%               | 14            | Numérica   | Contínua      | int64   |
| Pool QC         | Qualidade da piscina.                                             | 13               | 99.56%              | 4             | Categórica | Ordinal       | str     |
| Fence           | Qualidade da cerca.                                               | 572              | 80.48%              | 4             | Categórica | Ordinal       | str     |
| Misc Feature    | Recursos extras (elevador, galpão, etc.).                         | 106              | 96.38%              | 5             | Categórica | Nominal       | str     |
| Misc Val        | Valor em dólares do recurso extra.                                | 2930             | 0.00%               | 38            | Numérica   | Contínua      | int64   |
| Mo Sold         | Mês da venda.                                                     | 2930             | 0.00%               | 12            | Numérica   | Discreta      | int64   |
| Yr Sold         | Ano da venda.                                                     | 2930             | 0.00%               | 5             | Numérica   | Discreta      | int64   |
| Sale Type       | Tipo de venda (escritura, novo, etc.).                            | 2930             | 0.00%               | 10            | Categórica | Nominal       | str     |
| Sale Condition  | Condição da venda (normal, anormal, etc.).                        | 2930             | 0.00%               | 6             | Categórica | Nominal       | str     |
| SalePrice       | Preço de venda (Alvo da predição).                                | 2930             | 0.00%               | 1032          | Numérica   | Contínua      | int64   |