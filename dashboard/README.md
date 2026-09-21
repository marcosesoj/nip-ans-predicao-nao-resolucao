# Painel em Power BI

_Esta pasta ainda não contém o arquivo do painel. Adicione aqui o `.pbix` e complete as
seções abaixo._

## Arquivo

| | |
|---|---|
| Arquivo | `painel_nip.pbix` |
| Versão do Power BI Desktop | _[preencher]_ |
| Fonte de dados | `df_final_com_previsoes_2026.csv`, gerado pelo notebook 02 |

> **Atenção ao tamanho.** O GitHub rejeita arquivos acima de 100 MB e alerta acima de 50 MB.
> Se o `.pbix` exceder esse limite, as opções são: remover os dados incorporados e apontar
> o painel para o CSV, usar Git LFS, ou publicar o arquivo em um repositório de dados
> (como o Zenodo, que ainda fornece um DOI citável) e linkar aqui.

## Como abrir

1. Baixe o `.pbix` e abra no Power BI Desktop.
2. Se as consultas apontarem para um caminho local, atualize a origem em
   **Transformar dados → Configurações da fonte de dados**.

## Páginas do painel

_[preencher: nome de cada página e o que ela responde]_

## Medidas principais

_[preencher: medidas DAX relevantes e sua definição]_

## Uso pretendido

O painel destina-se à priorização de demandas críticas e ao acompanhamento de indicadores
pelas operadoras. A probabilidade estimada de não resolução deve ser lida como um critério
de **ordenação** — o modelo discrimina razoavelmente (AUC-ROC de 0,651), mas sua acurácia
de classificação binária é modesta, de modo que a leitura caso a caso não substitui a
análise humana.
