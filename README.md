# 📊 Dashboard Analítico de Vendas — Power BI

Projeto de Business Intelligence desenvolvido em **Power BI** a partir de uma base simulada de vendas, com foco em transformação de dados, modelagem dimensional, criação de indicadores e análise de negócio.

## 🎯 Objetivo

Construir um dashboard analítico capaz de apoiar a análise do desempenho comercial por:

- Produtos
- Clientes
- Vendedores
- Estados e regiões
- Canais de venda
- Status das vendas

O projeto foi desenvolvido como um **MVP de Business Intelligence** para fins de estudo e portfólio.

---

## 🛠️ Tecnologias utilizadas

- Power BI
- Power Query
- DAX
- Excel
- Modelagem Dimensional
- Star Schema

---

## 🔄 Processo de desenvolvimento

### 1. Ingestão

A base original foi disponibilizada em Excel contendo dados de:

- Vendas
- Produtos
- Categorias
- Fornecedores
- Clientes
- Vendedores
- Estados
- Regiões

### 2. ETL com Power Query

Foi criada uma camada de staging para preservar os dados de origem.

Principais tratamentos realizados:

- Tipagem de dados
- Padronização de campos
- Mesclagem de consultas
- Criação das dimensões
- Criação da tabela fato
- Tratamento das chaves de relacionamento

### 3. Modelagem de Dados

O modelo foi estruturado utilizando **Star Schema**.

Tabelas principais:

- `FATO_VENDAS`
- `Dim_Cliente`
- `Dim_Vendedores`
- `Dim_Produtos`
- `Dim_Estado`

Os relacionamentos foram configurados no padrão:

**1 : N — Dimensão → Fato**

---

## 📐 Principais medidas DAX

Foram desenvolvidos indicadores como:

- Receita Total
- Ticket Médio
- Quantidade Vendida
- Vendas Concluídas
- Total de Vendas
- Vendas Canceladas
- Taxa de Cancelamento
- Receita Cancelada
- Meta Mensal
- Meta do Período
- Percentual de Atingimento
- Ranking de Vendedores

---

## 📊 Estrutura do Dashboard

O relatório foi dividido em cinco visões:

### 01 — Visão Executiva

- Receita Total
- Ticket Médio
- Quantidade Vendida
- Vendas Concluídas
- Evolução mensal da receita
- Top 5 produtos por receita
- Participação da receita por categoria

### 02 — Vendas Geográficas

- Receita por região
- Receita por estado
- Distribuição geográfica das vendas
- Estado com maior receita

### 03 — Vendedores

- Ranking de vendedores
- Receita por vendedor
- Meta do período
- Percentual de atingimento
- Análise individual de desempenho

### 04 — Clientes

- Receita por segmento
- Pessoa Física x Pessoa Jurídica
- Top 10 clientes por receita

### 05 — Status e Canais

- Total de vendas
- Vendas canceladas
- Taxa de cancelamento
- Distribuição por status
- Receita por canal de venda e região

---

## 🔎 Principais insights

A análise identificou:

- **R$ 384,4 mil** em receita proveniente de vendas concluídas.
- **R$ 5,1 mil** de ticket médio.
- Das 120 vendas registradas, **62,5% foram concluídas**.
- **17,5% das vendas foram canceladas**.
- **20% permaneceram pendentes**.
- Vendas canceladas e pendentes representam aproximadamente **R$ 336 mil em valor potencial não realizado**.
- Os cinco produtos com maior receita concentram aproximadamente **89,5% do faturamento**.
- Maio apresentou o maior resultado mensal, representando aproximadamente **26,7% da receita concluída do período**.
- O atingimento consolidado da meta acumulada de 9 meses foi de aproximadamente **9,93%**.

---

## 💡 Regra de negócio importante

A meta dos vendedores é originalmente mensal.

Para realizar uma comparação coerente com a receita acumulada do período, foi criada a seguinte lógica:

**Meta do período = Meta mensal × quantidade de meses analisados**

No projeto:

**9 meses de análise**

Assim:

**Percentual de atingimento = Receita acumulada ÷ Meta acumulada do período**

---

## 📌 Observação

Este projeto utiliza uma **base de dados simulada**, exclusivamente para fins de estudo, desenvolvimento técnico e portfólio.

---

## 👨‍💻 Autor

**Fernando Dias**

Data Analytics | Business Intelligence | Power BI | Python | SQL | Databricks
