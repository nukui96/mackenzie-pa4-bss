# Registro de Origem dos Dados

## 1. Identificação da Fonte e Licença
- **Dataset**: London Bike Sharing Dataset
- **Publicador original no Kaggle**: Hristo Mavrodiev (`hmavrodiev`)
- **URL da Fonte**: https://www.kaggle.com/datasets/hmavrodiev/london-bike-sharing-dataset
- **Atribuição da fonte**: "Powered by TfL Open Data" e "Contains OS data © Crown copyright and database rights 2016 and Geomni UK Map data © and database rights [2019]". A página do Kaggle informa dados de bicicletas da TfL, meteorologia de freemeteo.com e feriados do governo britânico.
- **Licença e redistribuição**: conferir as condições vigentes na página do conjunto de dados e na fonte original antes de redistribuir o CSV.
- **Arquivo publicado sem alterações**: `data/raw/london_merged.csv`.

## 2. Metadados Estruturais do Arquivo
- **Nome do Arquivo Bruto**: `london_merged.csv`
- **Tamanho do Arquivo**: 1.034.821 bytes (~1,03 MB)
- **Contagem Total de Linhas**: 17.414 registros horários
- **Contagem Total de Colunas**: 10
- **Total Acumulado da Demanda Bruta (`cnt`)**: 19.905.972 aluguéis de bicicletas.

## 3. Dicionário de Variáveis
| Coluna | Tipo Detectado | Domínio / Unidade | Descrição | Nulos |
|---|---|---|---|---|
| `timestamp` | `object` / `datetime64[ns]` | `2015-01-04 00:00:00` a `2017-01-03 23:00:00` | Marcação temporal agregada por hora | 0 |
| `cnt` | `int64` | [0, 7860] | Contagem de aluguéis registrada no período de 1 hora (alvo horário) | 0 |
| `t1` | `float64` | [-1.5, 34.0] ºC | Temperatura real do ar em graus Celsius | 0 |
| `t2` | `float64` | [-6.0, 34.0] ºC | Sensação térmica ("feels like") em graus Celsius | 0 |
| `hum` | `float64` | [20.5, 100.0] % | Umidade relativa do ar | 0 |
| `wind_speed` | `float64` | [0.0, 56.5] km/h | Velocidade do vento | 0 |
| `weather_code` | `float64` no CSV | [1, 26] | Código meteorológico numérico; os valores presentes são inteiros representados com decimal | 0 |
| `is_holiday` | `float64` no CSV | {0, 1} | Indicador de feriado (1: sim, 0: não) | 0 |
| `is_weekend` | `float64` no CSV | {0, 1} | Indicador de fim de semana (1: sim, 0: não) | 0 |
| `season` | `float64` no CSV | {0, 1, 2, 3} | Código de estação meteorológica (0: primavera, 1: verão, 2: outono, 3: inverno) | 0 |

## 4. Limitações Conhecidas do Dataset
1. **Nível de Agregação Espacial**: A série é agregada para toda a cidade de Londres. Não há desagregação por estação, ponto de retirada ou rota, o que impossibilita a modelagem de rebalanceamento local de frota por estação.
2. **Horizonte Temporal Fixo**: Cobertura restrita entre 4 de janeiro de 2015 e 3 de janeiro de 2017 (2 anos completos).
3. **Não-disponibilidade de Clima Futuro Perfeito**: Embora o CSV contenha variáveis climáticas observadas, elas não podem ser utilizadas na modelagem causal de $t+1$ sem incorrer em vazamento de informação (lookahead bias), pois no momento da previsão ($t$) o operador só tem acesso a previsões meteorológicas imperfeitas.
