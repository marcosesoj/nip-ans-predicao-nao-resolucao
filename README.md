# Predição de não resolução de demandas NIP na saúde suplementar

Trabalho de Conclusão de Curso — MBA em Data Science & Analytics
USP/Esalq — 2026

**Autor:** José Marcos da Silva
**Orientador(a):** _[Gabrielle Maria Romeiro Lombardi]_

---

## Resumo

A Notificação de Intermediação Preliminar (NIP) é o principal instrumento de mediação
entre beneficiários e operadoras de planos de saúde no Brasil, mas grande parte das
demandas permanece sem desfecho avaliado. Este trabalho caracteriza essas demandas,
estima a probabilidade de não resolução daquelas ainda sem avaliação e disponibiliza o
resultado em painel interativo.

Foram utilizados dados abertos da Agência Nacional de Saúde Suplementar (ANS) de 2021 a
abril de 2026, complementados pelo cadastro de operadoras (CADOP) e pelo Índice Geral de
Reclamações (IGR). O recorte contemplou operadoras ativas, de médio porte e de modalidade
médico-hospitalar.

## Desenho do estudo

| | |
|---|---|
| Registros após filtragem | 183.796 |
| Demandas com avaliação registrada | 68.559 (37,3%) |
| Conjunto de treino | 62.931 demandas avaliadas entre 2021 e 2025 |
| Conjunto de teste | 5.628 demandas avaliadas em 2026 |
| Aplicação do modelo | 10.528 demandas de 2026 sem avaliação |
| Classe positiva | "não resolvido" (prevalência de 57,46% no teste) |

A partição é **temporal**, não aleatória: reproduz a condição real de uso do modelo, em que
o desfecho de demandas futuras é estimado a partir do histórico disponível.

## Resultados

| Métrica | Regressão Logística | Random Forest (padrão) | Random Forest (ajustada) |
|---|---|---|---|
| AUC-ROC | 0,640 | 0,595 | **0,651** |
| Acurácia | **0,620** | 0,577 | 0,607 |
| Sensibilidade | **0,667** | 0,608 | 0,631 |
| Especificidade | 0,556 | 0,535 | **0,575** |
| Precisão (VPP) | **0,670** | 0,639 | 0,667 |
| Escore F1 | **0,669** | 0,623 | 0,649 |
| Escore de Brier | 0,234 | 0,251 | **0,233** |

Referência do escore de Brier: 0,2444, dada pela prevalência da classe positiva. A Random
Forest ajustada e a Regressão Logística superam essa referência em 4,8% e 4,5%,
respectivamente; a Random Forest com parâmetros padrão não a supera.

A floresta ajustada lidera em AUC-ROC e escore de Brier — métricas independentes do limiar,
que avaliam ordenamento e calibração. A regressão logística lidera em acurácia,
sensibilidade e F1, medidas no limiar fixo de 0,5. Os ganhos sobre a previsão trivial são
modestos em todos os casos, sugerindo que as variáveis administrativas disponíveis
capturam parcela limitada dos fatores associados à não resolução.

## Estrutura

```
.
├── notebooks/
│   ├── 01_etl_eda.ipynb                     extração, limpeza, integração e análise exploratória
│   ├── 02_modelagem_classificacao.ipynb     ajuste, avaliação e aplicação, com busca em grade
│   └── 02b_modelagem_execucao_rapida.ipynb  idêntico, com os hiperparâmetros já fixados
├── data/
│   ├── raw/                             bases originais da ANS (não versionadas)
│   └── processed/                       base analítica gerada pelo notebook 01 (não versionada)
├── outputs/
│   ├── figuras/                         figuras exportadas
│   └── tabelas/                         tabelas exportadas em .xlsx
├── dashboard/                           painel em Power BI e sua documentação
└── docs/                                documentação complementar
```

## Reprodução

Os notebooks foram executados no Google Colab, com as bases hospedadas no Google Drive.
Para reproduzir:

1. Baixe as bases conforme [`data/README.md`](data/README.md).
2. Ajuste a constante de caminho no início de cada notebook (`RAIZ` no notebook 01,
   `PASTA` no notebook 02) para a pasta onde os dados foram colocados.
3. Execute `01_etl_eda.ipynb`, que gera a base analítica.
4. Execute `02_modelagem_classificacao.ipynb`, que ajusta os modelos, avalia no conjunto
   de 2026 e escora as demandas sem avaliação. A busca em grade avalia 108 combinações
   para a random forest e 8 para a regressão logística, o que leva cerca de duas horas —
   para reexecutar a análise sem refazer a seleção, use `02b_modelagem_execucao_rapida.ipynb`,
   que aplica diretamente os hiperparâmetros vencedores e produz os mesmos resultados.

A semente aleatória está fixada em 42 e a validação cruzada usa 5 folds estratificados,
aplicados apenas dentro do conjunto de treino.

Hiperparâmetros selecionados: random forest com 500 árvores, profundidade livre, mínimo de
10 observações por folha e critério Gini; regressão logística com `C = 0,1`.

No ajuste inferencial da regressão logística (statsmodels), duas colunas da matriz de
delineamento apresentavam dependência linear exata em relação às demais e foram removidas,
de modo a garantir a identificabilidade dos coeficientes. A remoção não altera o espaço
gerado pelas variáveis e, portanto, não afeta as estimativas de desempenho preditivo.

Fora do Colab, instale as dependências com:

```bash
pip install -r requirements.txt
```

## Fonte dos dados

Todos os dados são públicos e provêm do portal de dados abertos da ANS:
<https://dadosabertos.ans.gov.br>

## Licença

Código distribuído sob a licença MIT — veja [LICENSE](LICENSE).
Os dados da ANS seguem os termos de uso da própria agência.

## Como citar

> _[SOBRENOME, Nome]_. **Predição de não resolução de demandas NIP na saúde suplementar
> brasileira**. Trabalho de Conclusão de Curso (MBA em Data Science & Analytics) —
> USP/Esalq, Piracicaba, 2026. Disponível em:
> <https://github.com/marcosesoj/nip-ans-predicao-nao-resolucao>.
