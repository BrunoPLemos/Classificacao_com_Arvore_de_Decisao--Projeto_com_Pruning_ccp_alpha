Este projeto utiliza uma Árvore de Decisão para classificar observações com base em um subconjunto de variáveis de sensores (dados derivados de experimentos humanos com sensores de movimento). O foco está na otimização do modelo por meio de pruning (poda) usando o hiperparâmetro ccp_alpha, que controla a complexidade da árvore e ajuda a evitar overfitting.

Bibliotecas Utilizadas
pandas
numpy
matplotlib
scikit-learn

1. Importação e Leitura dos Dados
Leitura dos arquivos de treino e teste (X, y, subject).

Nomes das colunas atribuídos com base em features.txt.

Inclusão da coluna id_indiv com identificadores dos sujeitos do experimento.

Definição de um índice hierárquico ([index, id_indiv]).

2. Seleção de Variáveis
Utilização apenas das 3 primeiras variáveis (colunas) de X_train e X_test para facilitar a visualização e o desempenho computacional na construção da árvore.

3. Criação da Árvore de Decisão com Poda
Um modelo DecisionTreeClassifier é treinado para gerar o caminho de complexidade de custo usando:

python
Copiar
Editar
path = clf.cost_complexity_pruning_path(X_train, y_train)
Os valores de ccp_alpha retornados são usados para criar várias árvores com diferentes níveis de complexidade.

4. Treinamento com Diferentes ccp_alpha
Criação de múltiplos modelos com diferentes valores de ccp_alpha.

Seleção de apenas 1 a cada 5 valores para reduzir o número de árvores avaliadas (clfs_fracionado).

5. Avaliação dos Modelos
Para cada árvore criada, calcula-se a acurácia nos dados de treino e teste.

Os resultados são armazenados em listas e visualizados com gráficos.

6. Visualização dos Resultados
Dois gráficos são gerados:

Acurácia vs. ccp_alpha (versão simplificada) — para valores fracionados.

Acurácia x Alpha (completo) — com a função steps-post para melhor visualização da variação da acurácia.

7. Seleção da Melhor Árvore
A árvore com melhor desempenho nos dados de teste é selecionada.

Sua acurácia é reportada.

python
Copiar
Editar
melhor_arvore = clfs_fracionado[ind_melhor_arvore]
melhor_arvore.score(x_test, y_test)

8. Matriz de Confusão
O modelo final é avaliado com uma matriz de confusão, que exibe o desempenho por classe.

Exibe acertos e erros por categoria com ConfusionMatrixDisplay.

Resultados
A análise mostra como o hiperparâmetro ccp_alpha influencia o desempenho do modelo.

A árvore ótima é selecionada com base na acurácia dos dados de teste.

A matriz de confusão fornece uma visão detalhada da performance por classe.
