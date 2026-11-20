# Notebooks

- **`03_cd_projeto_aplicado_IV_doc_etapa3.ipynb` (ponto de entrada do fluxo completo):** executa ponta a ponta a ingestão e auditoria dos dados brutos, a agregação diária causal (`37.697` em `02/09/2016`), a EDA (gráficos, decomposição `s=7`, ACF/PACF, ADF e KPSS), a partição cronológica (`640` treino / `91` teste), a modelagem *walk-forward* (*Seasonal Naive*, Holt-Winters Aditivo e SARIMA) e a tabela de métricas.
- `01_cd_projeto_aplicado_IV_doc_etapa1.ipynb`: versão histórica da Etapa 1 (proposta e inspeção inicial da base).
- `02_cd_projeto_aplicado_IV_doc_etapa2.ipynb`: versão histórica da Etapa 2 (referencial, pipeline e auditoria preliminar).

Para reproduzir o fluxo completo localmente, utilize **Python 3.12**, instale as dependências de `../requirements.txt`, confirme a presença de `london_merged.csv` em `../data/raw/` e execute todas as células de `03_cd_projeto_aplicado_IV_doc_etapa3.ipynb` em ordem.
