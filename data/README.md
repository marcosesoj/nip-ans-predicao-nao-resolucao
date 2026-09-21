# Dados

Nenhum arquivo de dados é versionado neste repositório. Todas as bases são públicas e
estão disponíveis no portal de dados abertos da ANS: <https://dadosabertos.ans.gov.br>

Os arquivos brutos somam mais do que o GitHub aceita por arquivo (100 MB) e, sendo
públicos e permanentes na fonte, não há ganho em duplicá-los aqui.

## Bases utilizadas

| Base | Conteúdo | Pasta esperada |
|---|---|---|
| NIP | Notificações de Intermediação Preliminar, 2021 a abril de 2026 | `raw/NIPS/` |
| CADOP | Cadastro de operadoras ativas | `raw/CADOP/CADOP.csv` |
| IGR | Índice Geral de Reclamações por operadora e mês | `raw/BENEF. IGR/IGR.csv` |
| IBGE | Dimensão de municípios e capitais (via pacote `geobr`) | gerada pelo notebook 01 |

## Estrutura esperada

Os notebooks foram executados no Google Colab, apontando para uma pasta no Google Drive.
Ao reproduzir, replique esta estrutura e ajuste a constante de caminho no início de cada
notebook — `RAIZ` no notebook 01 e `PASTA` no notebook 02.

```
<raiz dos dados>/
├── NIPS/                      arquivos anuais da NIP (CSV, separador ';')
├── CADOP/CADOP.csv
├── BENEF. IGR/IGR.csv
├── 2026_BASE_COMPLETA/
│   └── base_analitica_tcc.csv        gerado pelo notebook 01
└── 2026_CLASSIFICACAO/
    └── df_final_com_previsoes_2026.csv   gerado pelo notebook 02
```

## Recorte aplicado

O notebook 01 filtra para operadoras **ativas**, de **médio porte** (carteira entre 50 mil
e 100 mil beneficiários) e de modalidade **médico-hospitalar**, resultando em 183.796
registros.
