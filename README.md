# processo-seletivo-triggo
Processo Seletivo Triggo - Análise de Dados do E-commerce Olist

Visão Geral do Projeto

Este documento descreve o projeto de análise de dados realizado sobre um conjunto de dados de e-commerce da Olist. O objetivo principal é explorar os dados para extrair insights valiosos, responder a questões de negócio específicas, criar visualizações informativas e desenvolver um modelo preditivo simples. O projeto abrange desde a preparação e limpeza dos dados até a aplicação de técnicas de modelagem e análise de satisfação do cliente, utilizando o script Python Processo_Seletivo_Triggo_.py. Este README detalha como configurar o ambiente, executar o script e compreende as principais análises e os resultados que podem ser obtidos através da sua execução.

Pré-requisitos

Para executar o script e replicar as análises, é necessário ter um ambiente Python configurado. As principais bibliotecas utilizadas no script incluem:
pandas: Para manipulação e análise de dados tabulares.
numpy: Para operações numéricas eficientes.
matplotlib: Para a criação de gráficos estáticos.
seaborn: Para a criação de visualizações estatísticas mais elaboradas.
plotly: Para a criação de gráficos interativos.
sqlite3: Para a criação e manipulação de um banco de dados SQL em memória, facilitando consultas complexas.
scikit-learn (sklearn): Para tarefas de machine learning, como a criação do modelo preditivo (inferido pela natureza da tarefa de predição de atraso).

Configuração do Ambiente

Siga os passos abaixo para configurar o ambiente necessário para a execução do projeto.

1. Obtenção dos Dados
   
O script Processo_Seletivo_Triggo_.py espera que os arquivos CSV do dataset da Olist estejam disponíveis em um diretório específico. Conforme observado no script, os caminhos para os arquivos são definidos como, por exemplo, path_customers = 'upload/olist_customers_dataset.csv'. Certifique-se de que os seguintes arquivos CSV estejam presentes no diretório upload/ (ou ajuste os caminhos no script conforme a localização dos seus arquivos):
olist_customers_dataset.csv
olist_geolocation_dataset.csv
olist_order_items_dataset.csv
olist_order_payments_dataset.csv
olist_order_reviews_dataset.csv
olist_orders_dataset.csv
olist_products_dataset.csv
olist_sellers_dataset.csv
product_category_name_translation.csv

Estes arquivos compõem o conjunto de dados da Olist e são essenciais para todas as análises subsequentes.

3. Instalação de Dependências
Após configurar o Python, instale as bibliotecas necessárias. Você pode instalá-las utilizando o gerenciador de pacotes pip. Abra um terminal ou prompt de comando e execute:
bash
pip install pandas numpy matplotlib seaborn plotly scikit-learn

É possível que outras bibliotecas específicas sejam importadas dentro de funções ou blocos de código não totalmente visíveis na análise inicial do script; caso ocorram erros de importação, instale as bibliotecas faltantes conforme necessário.
Como Executar o Script

Com os dados no local correto e as dependências instaladas, o script Processo_Seletivo_Triggo_.py pode ser executado. Navegue até o diretório onde o script está salvo e execute o seguinte comando no seu terminal:

bash
python Processo_Seletivo_Triggo_.py

A execução do script processará os dados, realizará as análises e, conforme a implementação, poderá gerar saídas como gráficos (exibidos em janelas separadas ou salvos em arquivos, dependendo da configuração do matplotlib/seaborn/plotly no ambiente de execução) e impressões de resultados no console. O script utiliza um banco de dados SQLite em memória para armazenar e consultar os dados após o carregamento e tratamento inicial.
Principais Análises e Resultados Conforme o Script

O script Processo_Seletivo_Triggo_.py foi projetado para responder a diversas questões de negócio e realizar análises aprofundadas sobre os dados da Olist. Abaixo, detalhamos como o script aborda cada uma das principais investigações solicitadas:

1. Volume de Pedidos e Sazonalidade
   
Para entender o volume de transações ao longo do tempo e identificar possíveis padrões de sazonalidade, o script executa uma consulta SQL (query_pedidos_mes). Esta consulta agrega o número total de pedidos (COUNT(DISTINCT order_id)) por ano e mês, extraídos da coluna order_purchase_timestamp da tabela orders. Pedidos com status 'canceled' ou 'unavailable' são excluídos da contagem para focar em transações efetivas. O resultado é então utilizado para gerar um gráfico de linhas, onde o eixo X representa o tempo (Ano-Mês) e o eixo Y o total de pedidos. Esta visualização permite observar tendências de crescimento, quedas e picos de vendas, como os que podem ocorrer em datas comemorativas ou eventos promocionais como a Black Friday, ajudando a compreender a dinâmica temporal das vendas da plataforma.

3. Distribuição do Tempo de Entrega
   
A análise do tempo de entrega é crucial para avaliar a eficiência logística. O script calcula o tempo de entrega em dias para cada pedido entregue através da consulta SQL query_tempo_entrega. Este cálculo é feito subtraindo a data de compra (order_purchase_timestamp) da data em que o pedido foi efetivamente entregue ao cliente (order_delivered_customer_date), utilizando a função JULIANDAY do SQLite para converter as datas em números de dias. A análise foca apenas em pedidos com status 'delivered' e que possuem as datas necessárias preenchidas. Com os tempos de entrega calculados, o script gera um histograma para visualizar a distribuição desses valores. Este gráfico mostra a frequência de pedidos entregues em diferentes faixas de tempo (por exemplo, quantos pedidos levaram de 0-5 dias, 6-10 dias, etc.). Adicionalmente, são calculadas estatísticas descritivas como a média e a mediana do tempo de entrega, fornecendo uma compreensão quantitativa do desempenho logístico e identificando a concentração dos prazos de entrega.

4. Relação entre Frete e Localização (Estado)
   
O custo do frete é um fator importante na decisão de compra online. O script investiga como o valor médio do frete varia entre os diferentes estados brasileiros dos clientes. Para isso, utiliza a consulta SQL query_frete_estado, que calcula a média do valor do frete (AVG(oi.freight_value)) agrupada por estado do cliente (c.customer_state). As informações são obtidas juntando as tabelas order_items (que contém o valor do frete), orders (para conectar ao cliente) e customers (que contém o estado do cliente). O resultado é apresentado em um gráfico de barras, onde cada barra representa um estado e sua altura indica o valor médio do frete. Esta análise permite identificar estados com fretes mais caros ou mais baratos, o que geralmente está correlacionado com a distância dos centros de distribuição e a infraestrutura logística de cada região. Embora o script não calcule explicitamente a distância geográfica para correlacionar com o frete, a análise por estado oferece um proxy valioso para essa relação.

5. Categorias de Produtos por Faturamento
   
Identificar as categorias de produtos que mais geram receita é fundamental para estratégias de estoque e marketing. O script realiza essa análise através da consulta SQL query_faturamento_categoria. Esta consulta calcula o faturamento total (SUM(oi.price)) para cada categoria de produto. As categorias são obtidas da tabela products e, quando disponível, traduzidas para o inglês utilizando a tabela category_translation para padronização. A consulta junta as tabelas order_items (preço do item), products (categoria) e orders (para filtrar pedidos não cancelados ou indisponíveis). Os resultados são ordenados de forma decrescente pelo faturamento, e o script tipicamente visualiza as top 15 categorias em um gráfico de barras. Isso destaca claramente quais segmentos de produtos são os mais lucrativos para a Olist.

6. Valor Médio de Pedido por Estado
   
Compreender o comportamento de compra dos clientes em diferentes regiões pode revelar oportunidades de mercado. O script analisa o valor médio de pedido por estado brasileiro através da consulta query_valor_medio_pedido_estado. Esta consulta calcula a média do valor total pago por pedido (AVG(pay.payment_value)) agrupado pelo estado do cliente (c.customer_state). Os dados são extraídos das tabelas order_payments (valor do pagamento), orders (para ligar ao cliente) e customers (estado do cliente). Um gráfico de barras é gerado para comparar o valor médio dos pedidos entre os estados, permitindo identificar regiões onde os clientes tendem a gastar mais por compra.

7. Análise de Retenção de Clientes
   
A capacidade de reter clientes é um indicador chave da saúde de um e-commerce. O script visa calcular a taxa de clientes recorrentes, definindo um cliente recorrente como aquele que realizou mais de um pedido no período analisado. Embora a consulta SQL específica para esta análise não tenha sido detalhada na visualização inicial do código, a estrutura do projeto indica que esta análise é um dos objetivos. Tipicamente, isso envolveria contar o número de pedidos por customer_id e, em seguida, identificar quantos clientes têm uma contagem de pedidos superior a um. A taxa de retenção seria a proporção desses clientes recorrentes em relação ao total de clientes únicos. Os insights extraídos podem incluir a eficácia de programas de fidelidade, a satisfação geral do cliente ao longo do tempo e a identificação de características de clientes que tendem a comprar novamente.

8. Predição de Atraso na Entrega
   
Atrasos na entrega podem impactar negativamente a satisfação do cliente. O script se propõe a construir um modelo de machine learning simples para prever a probabilidade de um pedido ser entregue com atraso. O processo envolve várias etapas:
Definição de Atraso: Um pedido é considerado atrasado se a data de entrega ao cliente (order_delivered_customer_date) for posterior à data estimada de entrega (order_estimated_delivery_date). Uma nova coluna binária (atrasado/não atrasado) seria criada.
Criação de Features (Variáveis): Seriam selecionadas ou criadas variáveis relevantes para a predição, como o tempo estimado de entrega, distância (se calculável a partir da geolocalização), tipo de produto, informações do vendedor, época do ano, etc.
Divisão dos Dados: O conjunto de dados seria dividido em um conjunto de treino (para treinar o modelo) e um conjunto de teste (para avaliar sua performance em dados não vistos).
Implementação do Modelo: Um algoritmo de classificação, como Regressão Logística ou Random Forest (conforme sugerido pelo usuário), seria treinado com os dados de treino.
Avaliação do Modelo: A performance do modelo seria avaliada no conjunto de teste usando métricas como acurácia, precisão, recall, F1-score e análise da matriz de confusão. Os resultados ajudariam a entender a capacidade do modelo em prever atrasos e quais fatores são mais preditivos.

9. Segmentação de Clientes
   
Para personalizar estratégias de marketing e otimizar a experiência do cliente, o script planeja realizar uma segmentação de clientes. Isso geralmente é feito utilizando técnicas de clustering, como K-Means. O objetivo é agrupar clientes com características e comportamentos de compra semelhantes. As features para o clustering poderiam incluir frequência de compra, valor total gasto (ticket médio), categorias de produtos preferidas, tempo desde a última compra (recência), entre outras (análise RFM - Recency, Frequency, Monetary). Uma vez que os clusters (segmentos) são formados, o script analisaria o perfil de cada grupo (por exemplo, "clientes de alto valor", "compradores ocasionais", "clientes sensíveis a promoções"). Com base nesses perfis, poderiam ser sugeridas estratégias de marketing específicas para cada segmento, como ofertas personalizadas, campanhas de reengajamento ou programas de fidelidade direcionados.

10. Análise de Satisfação do Cliente
    
A satisfação do cliente é vital para o sucesso a longo prazo. O script explora a relação entre a nota de avaliação fornecida pelos clientes (presente no dataset olist_order_reviews_dataset.csv, coluna review_score) e diversos outros fatores. Estes fatores podem incluir a categoria do produto, o tempo de entrega, o valor do pedido, a qualidade do atendimento (se inferível de comentários), entre outros. A análise buscaria identificar quais desses aspectos têm maior impacto (positivo ou negativo) na avaliação final do cliente. Isso pode ser feito através de correlações, comparações de médias de satisfação entre diferentes grupos (por exemplo, clientes com entrega rápida vs. lenta) ou até mesmo modelos mais complexos para determinar a importância de cada fator. Os insights obtidos são cruciais para direcionar esforços de melhoria nos pontos que mais afetam a percepção do cliente.

Conclusão

O script Processo_Seletivo_Triggo_.py oferece uma estrutura robusta para a análise compreensiva dos dados da Olist. Ao seguir as instruções de configuração e execução, é possível replicar as análises detalhadas neste README e extrair insights valiosos sobre o desempenho do e-commerce, comportamento do cliente e áreas de oportunidade para o negócio. As visualizações e modelos gerados servem como ferramentas poderosas para a tomada de decisão baseada em dados.
