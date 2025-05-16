
# Processo Seletivo Triggo - Análise de Dados do E-commerce Olist

Este projeto tem como objetivo analisar os dados do e-commerce Olist, extraindo insights estratégicos e desenvolvendo um modelo de machine learning para prever atrasos nas entregas. A análise foi realizada com Python, utilizando bibliotecas como `pandas`, `matplotlib`, `seaborn`, `plotly`, `scikit-learn`, entre outras.

## 🔧 Como Executar o Projeto

### 1. Pré-requisitos

- Python 3.8 ou superior
- Instalar dependências com:

```bash
pip install pandas numpy matplotlib seaborn plotly scikit-learn
```

### 2. Dados

Coloque os seguintes arquivos `.csv` da Olist na pasta `upload/` ou ajuste os caminhos no script:

- `olist_customers_dataset.csv`
- `olist_geolocation_dataset.csv`
- `olist_order_items_dataset.csv`
- `olist_order_payments_dataset.csv`
- `olist_order_reviews_dataset.csv`
- `olist_orders_dataset.csv`
- `olist_products_dataset.csv`
- `olist_sellers_dataset.csv`
- `product_category_name_translation.csv`

### 3. Executar o Script

```bash
python Processo_Seletivo_Triggo_.py
```

O script realiza todas as etapas: carregamento, tratamento, análise e visualização.

## 📊 Principais Análises

### 1. Volume de Pedidos e Sazonalidade

- Foi identificada sazonalidade nas vendas, com picos significativos em novembro e dezembro, indicando influência de eventos promocionais como a Black Friday.

### 2. Tempo de Entrega

- A mediana de entrega foi de aproximadamente 10 dias.
- Pedidos atrasados apresentaram nota média de 2.62, enquanto os entregues no prazo obtiveram 4.30.

### 3. Frete por Localização

- Estados mais distantes dos centros de distribuição apresentaram fretes médios maiores (ex: regiões Norte e Nordeste).

### 4. Faturamento por Categoria

- Top 3 categorias em faturamento:
  1. `health_beauty`
  2. `watches_gifts`
  3. `bed_bath_table`

### 5. Valor Médio de Pedido por Estado

- Estados como SP e RJ concentraram maiores valores médios por pedido, sugerindo maior poder aquisitivo ou preferência por produtos mais caros.

### 6. Retenção de Clientes

- A taxa de clientes recorrentes foi 0%, apontando necessidade de ações de fidelização.

## 🤖 Predição de Atraso

- Modelo: **Regressão Logística**
- Acurácia: 72.34%
- Precisão para pedidos atrasados: 17.83%
- Pontos de melhoria: balanceamento de classes e testes com Random Forest.

## 👥 Segmentação de Clientes

Utilizando **K-Means**, foram identificados 4 grupos principais:

- **Cluster 0**: Alto ticket médio, baixa frequência.
- **Cluster 1/2**: Compradores de baixo valor e frequência.
- **Cluster 3**: Clientes fiéis com maior frequência.

### Estratégias de Marketing

- Cluster 0: programas premium.
- Cluster 1/2: campanhas de reengajamento.
- Cluster 3: fidelização e assinatura.

## 😊 Análise de Satisfação

- Atrasos e tempo de entrega impactam negativamente a nota do cliente.
- Categorias como `fashion_sport` e `books_general_interest` receberam as melhores avaliações.

## ✅ Conclusão

O projeto oferece uma análise completa do ecossistema da Olist, fornecendo bases sólidas para decisões estratégicas de logística, marketing e experiência do cliente.
