# Projeto Aplicado IV:  previsão diária de aluguéis de bicicletas em Londres

**Autor:** Kayo Oliveira Nukui, RA 10356420.

Este projeto investiga a previsão do total de aluguéis de bicicletas no dia seguinte com o conjunto [London Bike Sharing](https://www.kaggle.com/datasets/hmavrodiev/london-bike-sharing-dataset). A versão disponível reúne as etapas acadêmicas 1 e 2: proposta, descrição da base, referencial teórico, pipeline proposto e cronograma. A análise exploratória aprofundada e a avaliação dos modelos pertencem às próximas etapas.

## Arquivos principais

- [Notebook da etapa 1](notebooks/01_cd_projeto_aplicado_IV_doc_etapa1.ipynb) e [notebook da etapa 2](notebooks/02_cd_projeto_aplicado_IV_doc_etapa2.ipynb). Cada versão acumula o conteúdo pertinente das etapas anteriores.
- [Documentos acadêmicos](entregas/): versões em PDF elaboradas no modelo institucional.
- [Origem e estrutura dos dados](docs/DADOS_ORIGEM.md).
- [Dependências Python](requirements.txt).

## Dados e reprodução

O arquivo original `data/raw/london_merged.csv` está incluído para permitir a reexecução dos notebooks. Crie um ambiente Python, instale `requirements.txt` e execute o notebook da etapa 2 do início ao fim no VS Code ou Jupyter.

O arquivo original contém 17.414 registros horários entre 04/01/2015 e 03/01/2017, distribuídos por 730 datas observadas em um intervalo de 731 dias. Não há registros em 02/09/2016. A inspeção inicial do notebook confere estrutura, tipos e valores ausentes por coluna. A análise da cobertura temporal e as decisões de tratamento ficam para a etapa de implementação parcial.

As decisões sobre tratamento das lacunas e avaliação temporal dos modelos pertencem às próximas etapas. Os resultados deverão ser publicados somente após execução e revisão metodológica.

## Fonte e atribuição

Dados disponibilizados no [London Bike Sharing Dataset](https://www.kaggle.com/datasets/hmavrodiev/london-bike-sharing-dataset). Powered by TfL Open Data. Contains OS data © Crown copyright and database rights 2016 and Geomni UK Map data © and database rights [2019]. O uso e a redistribuição devem observar as condições descritas na página da fonte.
