# Regressão com Árvores de Decisão e Florestas Aleatórias  

## Contexto  
Este projeto foi desenvolvido com fins **educacionais**, para explorar o uso de **modelos baseados em árvores de decisão** aplicados a um problema de regressão.  

O objetivo é prever o **custo de entrega de esculturas** com base em variáveis relacionadas a dimensões, peso, reputação do artista, tipo de transporte, localização e outros atributos.  

---

## Data Understanding e Preprocessing  

- Base de dados com **4462 registros e 19 colunas**.  
- Nenhum valor nulo ou duplicado.  
- Variáveis incluem:  
  - `peso`, `altura`, `largura`, `material`  
  - `preco_escultura`, `preco_base_envio`  
  - `internacional`, `envio_expresso`, `fragil`, `transporte`  
  - `data_agendada`, `data_entrega`  
  - Target: **`custo`**  

### Preprocessing  
- Conversão de variáveis categóricas em **dummies (One Hot Encoding)**.  
- Extração de **features temporais** a partir de datas (`dia`, `mês`, `ano`).  
- Criação da variável `diferenca_dias_entrega` (tempo entre agendamento e entrega).  

---

## Feature Engineering  

1. **Binning**  
   - Criação de faixas para variáveis contínuas:  
     - `faixa_peso`: Pequeno, Médio, Grande.  
     - `faixas_reputacao`: Baixa, Média, Alta.  

2. **Date Features**  
   - Extração de componentes de datas para capturar sazonalidade.  

3. **Dummy Encoding**  
   - Transformação de variáveis categóricas como transporte, material, envio expresso.  

4. **Domain Knowledge**  
   - Reputação do artista e fragilidade da escultura foram mantidas como variáveis relevantes por intuição de negócio.  

---

## Modelagem  

### Decision Tree Regressor  
- **Modelo inicial:**  
  - `R² treino = 100%` (overfitting claro).  
  - `R² teste = 67.7%`  
  - RMSE teste ≈ 1507.  

- **Após tuning (GridSearchCV):**  
  - Melhor profundidade: 10  
  - `R² teste = 75.1%`  
  - RMSE teste ≈ 1324.  
  - Importância de features:  
    - `preco_escultura`, `reputacao_artista`, `peso` e `preco_base_envio` foram as mais relevantes.  

### Random Forest Regressor  
- Modelo de ensemble que combina várias árvores.  
- **Resultado inicial:**  
  - `R² treino = 97.7%`  
  - `R² teste = 82.2%`  
  - RMSE teste ≈ 1117.  

- **Após tuning:**  
  - Melhor configuração: `max_leaf_nodes=550`, `min_samples_leaf=2`.  
  - `R² treino = 96.4%`  
  - `R² teste = 81.4%`  
  - RMSE teste ≈ 1142.  

### Cross Validation  
- Média RMSE treino: ~506  
- Média RMSE teste: ~1094  
- Resultados estáveis → bom poder de generalização.  

---

## Resultados  

- Árvores de decisão simples **tendem a overfitting** → resolver com poda e tuning.  
- Random Forest apresentou **melhor equilíbrio** entre bias e variância.  
- Features relacionadas ao **preço da escultura**, **reputação do artista** e **peso** foram as mais influentes.  
- O modelo final consegue prever custos com **erro médio absoluto ~466**.  

---

## Próximos Passos  

- Testar outros ensembles (Gradient Boosting, XGBoost, LightGBM).  
- Realizar **Feature Scaling** para verificar impacto em métodos ensemble.  
- Implementar técnicas de **Feature Selection** (remover atributos de baixa importância).  
- Avaliar **SHAP values** para interpretabilidade do modelo.  
- Testar tuning mais agressivo para melhorar RMSE.  

---

## Tecnologias  

- **Python 3.11**  
- `pandas`, `numpy` – Data manipulation  
- `matplotlib`, `seaborn` – Data visualization  
- `scikit-learn` – Machine Learning (Decision Tree, Random Forest, GridSearchCV, Cross Validation)  

---

Projeto desenvolvido como prática de **Machine Learning com regressão baseada em árvores**, abordando:  
- **Exploração de dados (EDA)**  
- **Feature Engineering**  
- **Decision Trees**  
- **Random Forest**  
- **Model Evaluation e Tuning**  
