
# 🚀 Processo Seletivo Triggo - Análise de Dados do E-commerce Olist

Este projeto tem como objetivo realizar uma análise completa do dataset da Olist, um marketplace brasileiro, como parte do processo seletivo da Triggo. A proposta envolve desde a análise exploratória de dados (EDA), passando por modelagem preditiva, até a segmentação de clientes e análise de satisfação.

---

## 📁 Estrutura do Projeto

- `Processo_Seletivo_Triggo_.py`: script principal com toda a lógica de tratamento, análise e modelagem.
- `upload/`: pasta onde devem estar localizados os arquivos `.csv` da Olist.
- `output/`: local sugerido para salvar gráficos, relatórios e modelos treinados.

---

## 🧰 Tecnologias e Bibliotecas Utilizadas

- Python 3.8+
- Pandas, NumPy – manipulação de dados
- SQLite3 – consultas SQL em memória
- Matplotlib, Seaborn, Plotly – visualizações
- Scikit-learn – pré-processamento, modelagem e avaliação

---

## 🛠️ Instalação e Execução

### 1. Clonar o repositório

```bash
git clone https://github.com/seuusuario/processo-seletivo-triggo.git
cd processo-seletivo-triggo
```

### 2. Instalar dependências

```bash
pip install -r requirements.txt
```

> Se não houver um `requirements.txt`, instale manualmente:

```bash
pip install pandas numpy matplotlib seaborn plotly scikit-learn
```

### 3. Colocar os arquivos `.csv` da Olist na pasta `upload/`:

- `olist_customers_dataset.csv`
- `olist_geolocation_dataset.csv`
- `olist_order_items_dataset.csv`
- `olist_order_payments_dataset.csv`
- `olist_order_reviews_dataset.csv`
- `olist_orders_dataset.csv`
- `olist_products_dataset.csv`
- `olist_sellers_dataset.csv`
- `product_category_name_translation.csv`

### 4. Executar o script

```bash
python Processo_Seletivo_Triggo_.py
```

---

## 📊 Etapas da Análise e Principais Resultados

### 📈 1. Volume de Pedidos e Sazonalidade

- **Tendência crescente de pedidos ao longo dos meses**.
- **Picos em novembro/dezembro**, sugerindo sazonalidade (ex: Black Friday).
- Permite insights para **planejamento de estoque e campanhas sazonais**.

### ⏱️ 2. Tempo de Entrega

- **Mediana de entrega**: ~10 dias.
- Pedidos com **entrega no prazo** recebem em média **nota 4.30**.
- **Pedidos atrasados** recebem média de **2.62**, mostrando **impacto direto na satisfação**.

### 🚚 3. Relação entre Frete e Localização

- Correlação positiva fraca (r ~ 0.39) entre **distância** e **valor do frete**.
- Estados do **Norte e Nordeste** possuem valores de frete mais altos.
- Fretes variam também por políticas dos vendedores e promoções (ex: frete grátis).

### 🛒 4. Categorias Mais Lucrativas

Top 5 categorias por faturamento (produto + frete):

1. `health_beauty`
2. `watches_gifts`
3. `bed_bath_table`
4. `sports_leisure`
5. `computers_accessories`

> Direciona decisões sobre **investimento em marketing e parcerias estratégicas**.

### 💳 5. Valor Médio de Pedido por Estado

- Estados como **SP, RJ, MG** têm os **maiores tickets médios**.
- Insights para **ofertas regionalizadas e segmentação de campanhas publicitárias**.

### ♻️ 6. Retenção de Clientes

- **0% de clientes recorrentes** no dataset analisado.
- Indica **oportunidade crítica** de implementar:
  - Programas de fidelidade
  - Campanhas de reengajamento
  - Abandono de carrinho e remarketing

---

## 🤖 7. Predição de Atraso de Entrega

### Definição:

- Atraso = data de entrega real > data de entrega estimada

### Pipeline:

- Engenharia de features: tempo de aprovação, volume, peso, frete, estados etc.
- Divisão treino/teste (80/20)
- Modelo: **Regressão Logística**
- Acurácia: **72.34%**
- Precisão para atraso: **17.83%**

### Considerações:

- **Desbalanceamento** (apenas 8.11% dos pedidos atrasados).
- Recomendado testar **Random Forest**, **SMOTE** ou **XGBoost** para melhorar recall.

---

## 👤 8. Segmentação de Clientes (Clustering)

### Técnica Utilizada:

- K-Means com análise RFM (Recência, Frequência, Monetário)
- **4 clusters identificados** com base no método do cotovelo

### Cluster Insights:

| Cluster | Descrição | % de Clientes |
|---------|-----------|---------------|
| 0 | Alto gasto, baixa frequência | 2.8% |
| 1 | Baixo gasto, esporádico | 34.4% |
| 2 | Similar ao 1, menor recência | 46.6% |
| 3 | Alta frequência, ticket baixo | 2.6% |

### Estratégias:

- Cluster 0: programa VIP, recomendações personalizadas
- Cluster 1/2: cupons e campanhas de reativação
- Cluster 3: fidelização com cashback e planos de assinatura

---

## 🌟 9. Análise de Satisfação do Cliente

### Métricas:

- `review_score` médio para entregas no prazo: **4.30**
- Para entregas atrasadas: **2.62**
- Correlação negativa com tempo de entrega: **r = -0.327**

### Categorias com Melhor Avaliação:

- `fashion_sport`
- `books_general_interest`
- `la_cuisine`

### Categorias com Piores Avaliações:

- `security_and_services`
- `office_furniture`
- `pc_gamer`

> Reforça a importância da **logística ágil** e **comunicação transparente com o cliente**.

---

## ✅ Conclusão

Este projeto forneceu uma análise aprofundada sobre comportamento de compra, performance logística, fatores que afetam a satisfação e insights para segmentação de clientes. Além disso, foi implementado um modelo preditivo funcional para antecipar atrasos de entrega.

