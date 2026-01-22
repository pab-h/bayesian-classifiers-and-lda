# Classificador Bayesiano e LDA com Dados Contínuos

Este repositório contém a implementação de diferentes **classificadores Bayesianos** e do **LDA (Linear Discriminant Analysis)** aplicados a um conjunto de dados sintético gerado a partir de transformações lineares de variáveis Gaussianas.

O trabalho foi desenvolvido como parte da disciplina **Tópicos Especiais em Telecomunicações I – Reconhecimento de Padrões**, do curso de **Engenharia de Computação**, Universidade Federal do Ceará – Campus Sobral.

## 🎯 Objetivo

Implementar, **sem o uso de bibliotecas prontas de classificação**, diferentes variantes do classificador Bayesiano e o método LDA, avaliando seus desempenhos por meio de **validação cruzada K-Fold (K = 10)**.

O objetivo principal é analisar como **suposições estatísticas progressivamente mais restritivas** impactam o desempenho dos classificadores.

## 🧪 Geração da Base de Dados

A base de dados é gerada sinteticamente seguindo os passos:

1. Definição das matrizes:
   - Matrizes `A` e `B` (2×2), derivadas dos dígitos do CPF.
2. Geração das amostras:
   - `X1`: matriz 2×1000 com amostras Gaussianas (classe A)
   - `X2`: matriz 2×2000 com amostras Gaussianas (classe B)
3. Transformações lineares:
   - `Y1 = A · X1`
   - `Y2 = B · X2`
4. Base final:
   - `Z1 = Y1`
   - `Z2 = Y2 + k · M`, onde `M` é uma matriz de uns e `k` é um deslocamento escalar.

O valor de `k` é escolhido de forma que a **melhor acurácia obtida seja superior a 96%**, conforme exigido no enunciado.

## 📊 Exploração dos Dados

O código gera automaticamente:

- Histograma dos atributos por classe
- Gráfico de dispersão 2D
- Matriz de correlação
- Verificação do balanceamento das classes
- Normalização dos atributos (z-score)

## 🤖 Modelos Implementados

Todos os classificadores foram implementados **do zero**, sem uso de funções prontas do `scikit-learn`.

### Classificadores Bayesianos

1. **Bayesiano Geral**
   - Atributos Gaussianos
   - Matrizes de covariância completas

2. **Naive Bayes**
   - Atributos Gaussianos
   - Atributos descorrelacionados

3. **Bayesiano com Variância Constante**
   - Atributos descorrelacionados
   - Variâncias iguais entre atributos

4. **Bayesiano com Variância Constante e Classes Equiprováveis**
   - Simplificação máxima do modelo Bayesiano

### LDA (Linear Discriminant Analysis)

- Projeção linear dos dados em uma dimensão
- Classificação baseada em limiar unidimensional

## 🔁 Validação e Avaliação

- **Holdout:**  
  - 70% treino  
  - 30% teste  
  - Amostragem estratificada  

- **Validação Cruzada:**  
  - K-Fold com K = 10  
  - Avaliação por acurácia média e desvio padrão  

## 📈 Resultados

O código apresenta automaticamente:

- Acurácia média dos 10 folds para cada modelo
- Desvio padrão da acurácia
- Acurácia final no conjunto de teste

### Observações Importantes

Os resultados mostram que:

- O **classificador Bayesiano Geral** apresentou o melhor desempenho.
- Modelos com suposições mais restritivas (Naive Bayes, variância constante, equiprobabilidade) tiveram queda progressiva de desempenho.
- O **LDA** apresentou o pior resultado, pois não conseguiu encontrar uma projeção linear que separasse adequadamente as classes.

Essa degradação de desempenho ocorre porque **as hipóteses impostas pelos modelos simplificados não são validadas pela base de dados**.