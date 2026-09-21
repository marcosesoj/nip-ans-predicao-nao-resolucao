# Painel em Power BI

## Arquivo

| | |
|---|---|
| Arquivo | `Demandas Demandas ANS.pbix` |
| Versão do Power BI Desktop | _Versão: 2.157.1354.0 64-bit (agosto de 2026) |
| Fonte de dados | `df_final_com_previsoes_2026.csv`, gerado pelo notebook 02 |


## Como abrir

1. Baixe o `.pbix` e abra no Power BI Desktop.
2. Se as consultas apontarem para um caminho local, atualize a origem em
   **Transformar dados → Configurações da fonte de dados**.


## Uso pretendido

O painel destina-se à priorização de demandas críticas e ao acompanhamento de indicadores
pelas operadoras. A probabilidade estimada de não resolução deve ser lida como um critério
de **ordenação** — o modelo discrimina razoavelmente (AUC-ROC de 0,651), mas sua acurácia
de classificação binária é modesta, de modo que a leitura caso a caso não substitui a
análise humana.
