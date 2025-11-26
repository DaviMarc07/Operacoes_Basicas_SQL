# Consultas SQL Intermediárias (Agregação e KPIs) com SQLite e Pandas

1. Visão Geral do Projeto
Este projeto é a continuação do módulo de integração de dados, focado na prática de Consultas SQL de nível intermediário. O objetivo é ir além da seleção básica de dados e utilizar o SQL para realizar agregações, agrupamentos e calcular Key Performance Indicators (KPIs) essenciais do negócio, como o preço médio por produto e o volume de compras por cliente.

A base de dados de Vendas (tb_vendas) é utilizada, mantendo o ambiente de banco de dados SQLite temporário (em memória) conectado ao Python/Pandas.

2. Configuração do Ambiente e Função de Consulta
A seção inicial do código estabelece o link entre Python e o banco de dados.

Ferramentas: sqlite3 (para o banco de dados) e pandas (para manipulação e leitura do CSV).

Conexão: É estabelecida uma conexão sqlite3.connect(':memory:'), criando um banco de dados temporário e altamente rápido.

Transferência de Dados: O dataframe de vendas é carregado para o SQLite com df_vendas.to_sql('tb_vendas', conn, ...).

Função run_query: Uma função de conveniência é definida para simplificar a execução de qualquer consulta SQL e converter o resultado diretamente em um DataFrame Pandas, o que facilita a visualização e a análise posterior no Python.

3. Detalhe das Consultas SQL
O foco principal do módulo está na sintaxe e na lógica das seguintes consultas SQL:

3.1. Consulta de Filtro Simples (Obrigatoriedade)
Objetivo: Filtrar o dataset para visualizar apenas as vendas de um produto específico (Exemplo: 'CAMISETA').

Cláusula Principal: WHERE PRODUTO = 'CAMISETA'

Importância: É a base de qualquer análise, permitindo isolar subconjuntos de dados relevantes para a investigação.

3.2. Consulta de Agregação por Produto (Média e Ordenação)
Objetivo: Calcular o preço médio unitário de venda para cada produto e ordenar o resultado.

Processos de Limpeza/Cálculo:

Limpeza no SQL (REPLACE e CAST): O código repete a etapa crucial de limpeza no SQL: REPLACE(VALOR_UNID, ',', '.') e CAST(... AS REAL). Isso é necessário para garantir que o SQL interprete a coluna como um número real antes de calcular a média.

Agregação (AVG): A função AVG() é usada para calcular a média do preço unitário.

Agrupamento (GROUP BY): O comando GROUP BY PRODUTO é fundamental. Ele garante que a média seja calculada de forma independente para cada item único na coluna PRODUTO, resultando no preço médio por categoria.

Ordenação (ORDER BY): O resultado é ordenado por ORDER BY MEDIA_PRECO_UNIDADE DESC para destacar os produtos de maior valor na primeira visualização.

3.3. Consulta de KPIs de Clientes (Soma e Contagem)
Objetivo: Obter Key Performance Indicators (KPIs) do comportamento de compra de cada cliente, medindo o volume total de unidades compradas e o número de transações.

Agrupamento (GROUP BY): O comando GROUP BY ID_CLIENTE garante que todos os cálculos de agregação sejam realizados no nível de cada cliente individual.

Soma (SUM): Usado para calcular o volume total de itens comprados pelo cliente (SUM(UNIDADES)).

Contagem (COUNT): Usado para calcular o número total de compras (transações) feitas pelo cliente (COUNT(ID_COMPRA)).

Importância: Estas métricas são a base para análises de valor do cliente (LTV - Lifetime Value) e segmentação (RFM).

4. Conclusão sobre SQL e Análise de Dados
O módulo reforça que o SQL é a ferramenta ideal para a fase de "Data Wrangling" e extração de insights básicos de grandes volumes de dados que já estão estruturados em um banco.

A capacidade de usar GROUP BY com funções de agregação (SUM, AVG, COUNT) permite que um analista de dados gere resumos e KPIs diretamente do banco, de forma rápida e eficiente, antes de transferir os resultados finais para o Python para a modelagem preditiva ou visualização avançada.

