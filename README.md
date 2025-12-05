# 🍷 Mineração de Dados Aplicada à Enologia: Qualidade e Segurança Alimentar

> Um projeto de Data Science para prever a qualidade do vinho tinto e detectar anomalias químicas utilizando Machine Learning.

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue)](https://www.python.org/)
[![Scikit-Learn](https://img.shields.io/badge/Library-Scikit--Learn-orange)](https://scikit-learn.org/)
[![Pandas](https://img.shields.io/badge/Library-Pandas-green)](https://pandas.pydata.org/)
[![Status](https://img.shields.io/badge/Status-Concluído-brightgreen)]()

---

## 📋 Sobre o Projeto

A indústria vitivinícola enfrenta desafios constantes para garantir a consistência e a segurança de seus produtos. A avaliação tradicional, feita por sommeliers, é subjetiva e não escalável.

Este projeto utiliza **Mineração de Dados** para analisar propriedades físico-químicas de vinhos tintos (Vinho Verde português). O objetivo é duplo:
1.  **Classificação Objetiva:** Determinar a qualidade do vinho (Ruim/Bom) baseando-se apenas em dados químicos.
2.  **Segurança Alimentar:** Demonstrar como algoritmos podem atuar como "barreiras sanitárias digitais", detectando desequilíbrios (como excesso de Acidez Volátil) que indicam deterioração ou risco de contaminação (contexto: *metanol* e adulterações).

---

## 🗂️ Dataset

Os dados foram obtidos do **UCI Machine Learning Repository** e referem-se ao estudo de *Cortez et al. (2009)*.

* **Arquivo:** `winequality-red.csv`
* **Amostras:** 1.599 vinhos tintos.
* **Variáveis (Features):**
    * `fixed acidity`, `volatile acidity`, `citric acid`, `residual sugar`, `chlorides`, `free sulfur dioxide`, `total sulfur dioxide`, `density`, `pH`, `sulphates`, `alcohol`.
* **Variável Alvo (Target):**
    * `quality` (nota sensorial entre 0 e 10).

---

## 🚀 Metodologia e Tecnologias

O projeto foi desenvolvido em **Python** (Jupyter Notebook), seguindo o pipeline padrão de KDD (Knowledge Discovery in Databases):

### 1. Pré-processamento
* **Padronização (`StandardScaler`):** Essencial para equalizar as escalas das variáveis químicas (ex: *Dióxido de Enxofre* vs *Cloretos*), garantindo o funcionamento correto de algoritmos baseados em distância.

### 2. Redução de Dimensionalidade
* **PCA (Análise de Componentes Principais):** Utilizado para reduzir as 11 variáveis originais para 2 componentes principais, permitindo a visualização espacial dos grupos químicos.

### 3. Agrupamento (Não Supervisionado)
* **K-Means:** Aplicado com **K=2** para forçar uma segmentação binária clara entre vinhos de "Perfil Superior" e "Perfil de Risco".
* **Validação:** O número de clusters foi definido utilizando o **Método do Cotovelo (Elbow Method)** e a **Análise de Silhueta**.

### 4. Regras de Associação (Supervisionado)
* **Decision Tree (Árvore de Decisão):** Utilizada para extrair as regras "White-box" que explicam os clusters formados. Isso traduz a matemática em regras de negócio compreensíveis.

---

## 📊 Principais Resultados

O algoritmo identificou dois perfis químicos distintos com base nas regras abaixo:

### 🏆 Regra de Ouro (Perfil Premium)
* **Condição:** `Álcool ≥ 10.5%` E `Acidez Volátil < 0.65`
* **Interpretação:** Vinhos equilibrados, produzidos com uvas maduras e processo fermentativo limpo.

### ⚠️ Regra de Risco (Perfil de Entrada/Defeito)
* **Condição:** `Álcool < 10.5%` OU `Acidez Volátil ≥ 0.70`
* **Interpretação:** Vinhos aguados ou com indícios de deterioração acética (vinagre). Alta acidez volátil é um marcador crítico para controle de qualidade e segurança.

> **Insight:** O modelo provou que a química não mente. O teor alcoólico é o maior preditor de qualidade percebida, enquanto a acidez volátil é o maior detrator.

---

## 🛠️ Como Executar

1.  **Clone o repositório:**
    ```bash
    git clone [https://github.com/seu-usuario/nome-do-repo.git](https://github.com/seu-usuario/nome-do-repo.git)
    ```
2.  **Instale as dependências:**
    ```bash
    pip install pandas matplotlib seaborn scikit-learn
    ```
3.  **Execute o Notebook:**
    Abra o arquivo `MD_vinho.ipynb` (ou `mineração_vinho.ipynb`) em seu ambiente Jupyter ou Google Colab.

---

## 📈 Visualizações

O notebook gera os seguintes gráficos para análise:
1.  **Mapa de Correlação (Heatmap):** Para identificar relações entre variáveis.
2.  **Método do Cotovelo & Silhueta:** Para justificar a escolha do K.
3.  **PCA Scatter Plot:** Visualização 2D da separação dos vinhos.
4.  **Árvore de Decisão:** Representação gráfica das regras de classificação.

---

## 📚 Referências

1.  *Cortez, P., Cerdeira, A., Almeida, F., Matos, T., & Reis, J. (2009). Modeling wine preferences by data mining from physicochemical properties. Decision Support Systems, 47(4), 547-553.*
2.  *BBC News Brasil. Notícias sobre segurança alimentar e riscos de bebidas adulteradas (Metanol).*
3.  *UCI Machine Learning Repository: Wine Quality Data Set.*

---

**Autor:** Matheus Henrique e Nicolas Ferreira
