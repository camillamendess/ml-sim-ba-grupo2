# Machine Learning - SIM BA

Trabalho prático da disciplina de Aprendizado de Máquina (UESB, 2026), Grupo 2.
Classificação de registros de óbito do Sistema de Informações sobre Mortalidade (SIM) de residentes na Bahia.

## Questão de pesquisa

Qual o ganho de desempenho na discriminação de óbitos por causas externas em relação aos demais óbitos registrados no SIM, entre residentes da Bahia de 2022 a 2025, ao acrescentar características demográficas e territoriais a um modelo baseado apenas em sexo e idade?

## Problema

- Tarefa: classificação binária supervisionada
- Alvo: 1 quando a causa básica (CAUSABAS) está no Capítulo XX da CID-10 (V01 a Y98), 0 nos demais casos
- Classe positiva: 13,04% dos óbitos

| Conjunto | Atributos |
|---|---|
| M1 | Sexo e idade |
| M2 | M1 + raça/cor, escolaridade (ESC2010) e situação conjugal |
| M3 | M2 + região de saúde de residência (28 regiões) |

## Métodos

- Algoritmos: Regressão Logística, Random Forest, KNN e MLP (scikit-learn), cada um com M1, M2 e M3
- Validação temporal: ajuste com treino em 2022 e 2023 e avaliação em 2024; modelo final treinado em 2022 a 2024; teste único em 2025
- Métricas: ROC-AUC e PR-AUC; o ganho é a diferença entre conjuntos
- Desbalanceamento: pesos por classe ou subamostragem, aplicados só no treino, dentro de um Pipeline da imbalanced-learn

## Dados

- Fonte: microdados da Declaração de Óbito por residência (DATASUS, arquivos `DOBA2022` a `DOBA2025.dbc`); 2022 a 2024 definitivos, 2025 preliminar
- Base do estudo: 412.692 óbitos não fetais de residentes na Bahia com 1 ano ou mais
- Regiões de saúde: base territorial do DATASUS
- Os dados brutos não são versionados. O notebook baixa os arquivos direto do servidor do DATASUS.
- O dataset final não contém campos que permitam identificar pessoas.

## Estrutura

```
notebooks/   verificação da base, etapas do projeto e notebook final
src/         preparação, pipeline e métricas comuns
data/        dataset final e dicionário de atributos
resultados/  métricas de cada modelo e conjunto
figuras/     gráficos
docs/        relatório, slides e diagrama de integração
```

## Como executar

1. Abra o notebook final em `notebooks/` no Google Colab
2. Execute as células em ordem; os arquivos .dbc são baixados e convertidos com `pyreaddbc`
3. Bibliotecas e versões estão em `requirements.txt`; sementes fixadas em `random_state = 42`

## Integrantes

Camilla Novaes Mendes, Gabriel Marcone Magalhães Santos, Giovana Fortunato Costa Gomes, Ítalo de Souza Leão e Lucas de Menezes Chaves.

Prof. Geraldo Pereira Rocha Filho
