# 🚗 Previsão de Preço de Carros Usados com Árvore de Regressão

Este projeto tem como objetivo prever o **preço de veículos usados** a partir de um conjunto de dados públicos. Utilizamos um modelo supervisionado de **regressão com árvore de decisão**, precedido por um processo robusto de **limpeza, tratamento e preparação dos dados**.

---
🔗 Link para o dataset no Kaggle
Você pode acessar o dataset "Used Cars Dataset" através do seguinte link:

👉 Used Cars Dataset - Kaggle
https://www.kaggle.com/datasets/austinreese/craigslist-carstrucks-data

## 📌 Objetivos do Projeto

- Explorar e tratar dados de veículos usados.
- Reduzir distorções causadas por outliers.
- Tratar valores ausentes de forma apropriada.
- Validar estatisticamente variáveis relevantes.
- Treinar um modelo preditivo de regressão com boa capacidade explicativa.
- Realizar uma previsão simples com variáveis numéricas.

---

## 🧹 Etapas de Limpeza e Tratamento de Dados

A qualidade dos dados foi tratada com muito cuidado, considerando as boas práticas de ciência de dados:

### 1️⃣ Tratamento de Outliers
- **Preço (`price`)**: Valores acima de R$500.000 foram considerados outliers e substituídos pela média dos valores dentro do limite.
- **Quilometragem (`odometer`)**: Veículos com mais de 200.000 km foram ajustados para a média dos registros considerados normais.

### 2️⃣ Tratamento de Valores Ausentes
- **Colunas numéricas** como `year` e `odometer`: preenchidas com a média.
- **Colunas categóricas**: preenchidas com `'unknown'`, evitando perda de informação.
- **Linhas com `lat`, `long` e `description` ausentes**: removidas por serem essenciais.

### 3️⃣ Redução de Ruído e Complexidade
- Remoção de colunas irrelevantes ou com excesso de valores nulos (`VIN`, `url`, `posting_date`, etc.).
- Agrupamento de categorias raras nas colunas `model` e `region` como `'other'`.

### 4️⃣ Verificação de Duplicatas
- Eliminação de registros duplicados.
### 5️⃣ 📊 Análise de Assimetria (Skew) e Transformação Logarítmica da Variável price
Realizamos a análise da assimetria (skewness) das variáveis numéricas para identificar distribuições distorcidas que podem impactar negativamente a performance dos modelos preditivos. A variável price apresentou skew superior a 0.75, indicando forte assimetria positiva.
Para corrigir essa distorção, aplicamos a transformação logarítmica na variável price, o que aproximou sua distribuição de uma forma mais simétrica. Essa transformação é fundamental para melhorar a estabilidade e a eficiência do modelo, facilitando o aprendizado e a generalização.

**O processo incluiu:

- Cálculo do skew das variáveis numéricas

- Identificação das variáveis com skew > 0.75

- Aplicação da transformação logarítmica na variável price

- Visualização comparativa da distribuição antes e depois da transformação

Esse passo é essencial para assegurar a qualidade dos dados e otimizar a modelagem preditiva.
---

## 📊 Análise Estatística

- **Teste Qui-Quadrado**: aplicado para avaliar a associação entre variáveis categóricas e o preço (`price`). Todas as variáveis mostraram relação significativa (p < 0.05).
- **Correlação**: as variáveis `year` (+0.28) e `odometer` (–0.43) apresentaram maior correlação com o preço.

---

## 🤖 Modelagem com Árvore de Decisão

- **Modelo:** `DecisionTreeRegressor`
- **Variáveis utilizadas:** `year`, `odometer`, além das colunas categóricas codificadas via One-Hot Encoding.
- **Divisão:** 70% treino, 30% teste
- **Métricas:**
  - MSE (Erro Quadrático Médio)
  - RMSE (Raiz do Erro Quadrático Médio)
  - MAE (Erro Absoluto Médio)
  - **R² (Coeficiente de Determinação):** `0.70`  
    ✅ Modelo com boa capacidade explicativa, apto para prever tendências de preço com base nas variáveis escolhidas.

---

## 💡 Previsão Simples com Variáveis Numéricas

Como exemplo adicional, foi treinado um modelo somente com `year` e `odometer`, capaz de estimar rapidamente o preço de um carro com base nesses dois atributos.

Exemplo:
```python
modelo.predict([[2015, 60000]])  # Previsão: ~R$XX.XXX,XX
```

---

## 🗂 Estrutura do Projeto

```
used-cars-price-prediction-decision-tree/
├── dados/
│   └── vehicles.csv
├── codigo/
│   └── projeto_preco_carros_usados.ipynb
├── README.md
└── .gitignore
```

---

## 🧠 Conclusão

Este projeto demonstrou a importância de um pipeline de **preparação de dados robusto** para o desenvolvimento de modelos preditivos eficazes. A abordagem envolveu:

- **Tratamento rigoroso de outliers** e valores ausentes;
- **Codificação cuidadosa de variáveis categóricas**, com controle da cardinalidade;
- **Validação estatística** por meio de testes de associação (Qui-Quadrado) e análise de correlação;
- E a aplicação de um modelo de **Árvore de Regressão**, escolhido por sua interpretabilidade e capacidade de capturar relações não lineares.

O modelo final apresentou um **coeficiente de determinação (R²) de 0.70**, o que indica um desempenho satisfatório para um problema real com dados heterogêneos e de origem aberta. Ainda que haja espaço para aprimoramentos com modelos mais complexos ou ajustes finos, a base construída é sólida e confiável.

Este projeto evidencia como a **ciência de dados aplicada** pode ser utilizada para estimar preços com boa precisão, contribuindo para análises de mercado, definição de estratégias comerciais e suporte à tomada de decisão no setor automotivo.
