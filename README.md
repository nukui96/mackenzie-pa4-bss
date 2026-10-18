# Projeto Aplicado IV — Previsão Diária de Demanda de Bicicletas em Londres

**Autor:** Kayo Oliveira Nukui  
**RA:** 10356420  
**Instituição:** Universidade Presbiteriana Mackenzie  
**Curso:** Superior de Tecnologia em Banco de Dados  
**Alinhamento:** ODS 11 — Cidades e Comunidades Sustentáveis (Meta 11.2)  

---

## Visão Geral do Projeto

Este repositório reúne o desenvolvimento cumulativo das **Etapas 1, 2 e 3** do Projeto Aplicado IV. O objetivo central é construir, validar e comparar modelos preditivos capazes de antecipar a demanda diária agregada de novos aluguéis de bicicletas compartilhadas em Londres para o dia subsequente ($t+1$, horizonte de 24 horas de antecedência), utilizando a base pública [London Bike Sharing Dataset](https://www.kaggle.com/datasets/hmavrodiev/london-bike-sharing-dataset).

A pergunta formal de pesquisa investiga:
> *Em que medida duas técnicas consolidadas de séries temporais (Suavização Exponencial Holt-Winters e modelo SARIMA) reduzem o erro de previsão em relação a uma referência sazonal ingênua (Seasonal Naive: repetir o mesmo dia da semana anterior), garantindo a ausência estrita de vazamento de informação temporal?*

---

## Pipeline da Solução em 6 Fases

O fluxo de dados foi projetado para assegurar causalidade estrita, rastreabilidade e reprodutibilidade:

```
[Fase 1: Ingestão & Auditoria]
      │ 17.414 registros horários brutos | 19.905.972 aluguéis reconciliados
      ▼
[Fase 2: Agregação & Preparação Causal]
      │ Grade civil de 731 dias | Imputação causal y(t-7) em 02/09/2016 restrita ao treino
      ▼
[Fase 3: EDA & Diagnósticos Estatísticos]
      │ ACF/PACF, decomposição semanal s=7, testes ADF (p < 0,0001 na 1ª dif) e KPSS
      ▼
[Fase 4: Particionamento Temporal Cronológico]
      │ Treino: 640 dias (04/01/2015 a 04/10/2016) | Teste: 91 dias (05/10/2016 a 03/01/2017)
      ▼
[Fase 5: Modelagem Preditiva]
      │ Seasonal Naive (s=7), Holt-Winters Aditivo (s=7) e SARIMA(1,1,1)x(1,1,1)₇
      ▼
[Fase 6: Avaliação de Desempenho out-of-sample]
        Projeção walk-forward avaliada exclusivamente sobre datas reais observadas
```

---

## Resultados Preditivos no Conjunto de Teste (91 dias)

A avaliação fora da amostra (*out-of-sample*) foi calculada sobre o período de teste (05/10/2016 a 03/01/2017) utilizando o Erro Absoluto Médio (MAE) e a Raiz do Erro Quadrático Médio (RMSE):

| Modelo Preditivo | MAE (Aluguéis) | RMSE (Aluguéis) | Redução MAE vs. Baseline (%) | Redução RMSE vs. Baseline (%) |
| :--- | :---: | :---: | :---: | :---: |
| **Linha de Base Sazonal (Seasonal Naive $s=7$)** | 4.533,8 | 6.744,8 | 0,00% | 0,00% |
| **Suavização Exponencial Holt-Winters (Aditivo $s=7$)** | 3.731,4 | 5.493,3 | +17,70% | +18,55% |
| **SARIMA(1,1,1)x(1,1,1)$_7$** | **3.237,6** | **5.057,3** | **+28,59%** | **+25,02%** |

### Diagnóstico Técnico dos Modelos:
- Ambos os modelos superaram substancialmente a linha de base sazonal ingênua.
- O modelo **SARIMA(1,1,1)x(1,1,1)$_7$** entregou o melhor desempenho global, reduzindo o erro absoluto médio em 28,59% (ganho de 1.296 aluguéis/dia de precisão).
- A **Suavização Exponencial de Holt-Winters** demonstrou alta eficiência operacional com redução de 17,70% no MAE aliada a uma formulação parcimoniosa e rápida convergência.
- Os erros residuais concentram-se em feriados bancários atípicos e dias de choque pluviométrico severo, cujo diagnóstico detalhado constitui o escopo da Etapa 4.

---

## Estrutura do Repositório

```
├── data/
│   ├── raw/
│   │   └── london_merged.csv       # Base bruta preservada (17.414 linhas)
│   └── README.md                   # Metadados e reconciliação dos dados
├── docs/
│   └── DADOS_ORIGEM.md             # Dicionário e fonte oficial TfL
├── entregas/
│   ├── [PA4] Previsao Diaria London Bike Sharing.docx  # Documento acadêmico institucional consolidado
│   └── README.md                   # Orientações sobre o entregável oficial
├── notebooks/
│   ├── 01_cd_projeto_aplicado_IV_doc_etapa1.ipynb      # Etapa 1: delimitação e governança
│   ├── 02_cd_projeto_aplicado_IV_doc_etapa2.ipynb      # Etapa 2: caracterização exploratória
│   ├── 03_cd_projeto_aplicado_IV_doc_etapa3.ipynb      # Etapa 3: modelagem e avaliação de métricas
│   └── README.md                                       # Guia de execução dos notebooks
└── requirements.txt                # Dependências fixadas do projeto
```

---

## Instruções para Reprodução Local

1. **Clone do repositório:**
   ```bash
   git clone https://github.com/kayonukui/mackenzie-pa4-bss.git
   cd mackenzie-pa4-bss
   ```

2. **Criação e ativação do ambiente virtual:**
   ```bash
   python -m venv .venv
   # Windows (PowerShell):
   .venv\Scripts\Activate.ps1
   # Linux/macOS:
   source .venv/bin/activate
   ```

3. **Instalação das dependências:**
   ```bash
   pip install -r requirements.txt
   ```

4. **Execução do notebook da Etapa 3:**
   Execute `notebooks/03_cd_projeto_aplicado_IV_doc_etapa3.ipynb` integralmente para reproduzir a agregação diária, os testes estatísticos e a tabela de métricas dos modelos.

---

## Fonte dos Dados e Atribuição

Dados originais disponibilizados por Hristo Mavrodiev via [Kaggle](https://www.kaggle.com/datasets/hmavrodiev/london-bike-sharing-dataset).  
Powered by Transport for London (TfL) Open Data. Contains OS data © Crown copyright and database rights 2016 and Geomni UK Map data © and database rights [2019].
