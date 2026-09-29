# Dados

O arquivo `raw/london_merged.csv` é a cópia sem alterações do [London Bike Sharing Dataset](https://www.kaggle.com/datasets/hmavrodiev/london-bike-sharing-dataset) usada nos notebooks 01 e 02. O checksum SHA-256 desta cópia é `db881c26314329377f81265480856f2fe4fb049fc1e79bd5f548813c99c4c446`.

O notebook da etapa 2 lê o arquivo bruto e agrega diretamente os registros horários por data. Há uma data sem observações e alguns dias com cobertura parcial; consulte [qualidade temporal](../docs/TRATAMENTO_BASE_DADOS.md) antes de interpretar totais diários.
