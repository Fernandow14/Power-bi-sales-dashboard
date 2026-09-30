# Medidas DAX do Projeto

Este arquivo reúne as principais medidas DAX utilizadas no Dashboard Analítico de Vendas desenvolvido em Power BI.

---

## Receita Total

Considera somente vendas com status **Concluída**.

```DAX
Receita_Total =
CALCULATE(
    SUM(FATO_VENDAS[Valor_Total]),
    FATO_VENDAS[Status] = "Concluída"
)
```

---

## Quantidade Vendida

Quantidade total de produtos provenientes de vendas concluídas.

```DAX
Quantidade_Vendida =
CALCULATE(
    SUM(FATO_VENDAS[Quantidade]),
    FATO_VENDAS[Status] = "Concluída"
)
```

---

## Vendas Concluídas

Quantidade de vendas finalizadas com sucesso.

```DAX
Vendas_Concluidas =
CALCULATE(
    COUNTROWS(FATO_VENDAS),
    FATO_VENDAS[Status] = "Concluída"
)
```

---

## Ticket Médio

Valor médio das vendas concluídas.

```DAX
Ticket_Medio =
DIVIDE(
    [Receita_Total],
    [Vendas_Concluidas],
    0
)
```

---

## Total de Vendas

Quantidade total de registros de vendas, independentemente do status.

```DAX
Total_Vendas =
COUNTROWS(FATO_VENDAS)
```

---

## Vendas Canceladas

Quantidade de vendas com status Cancelada.

```DAX
Vendas_Canceladas =
CALCULATE(
    COUNTROWS(FATO_VENDAS),
    FATO_VENDAS[Status] = "Cancelada"
)
```

---

## Taxa de Cancelamento

Percentual de vendas canceladas sobre o total de vendas.

```DAX
Taxa_Cancelamento =
DIVIDE(
    [Vendas_Canceladas],
    [Total_Vendas],
    0
)
```

---

## Receita Total Cancelada

Valor financeiro correspondente às vendas canceladas.

```DAX
Receita_Total_Cancelada =
CALCULATE(
    SUM(FATO_VENDAS[Valor_Total]),
    FATO_VENDAS[Status] = "Cancelada"
)
```

---

## Receita Total Pendente

Valor financeiro correspondente às vendas pendentes.

```DAX
Receita_Total_Pendente =
CALCULATE(
    SUM(FATO_VENDAS[Valor_Total]),
    FATO_VENDAS[Status] = "Pendente"
)
```

---

## Meta do Vendedor

Meta mensal cadastrada para cada vendedor.

```DAX
Meta_Vendedor =
SUM(
    Dim_Vendedores[Meta_Mensal]
)
```

---

## Total de Meses

Calcula a quantidade de meses existente no período analisado.

```DAX
Meses_Periodo =
VAR DataInicial =
    CALCULATE(
        MIN(FATO_VENDAS[Data_Venda]),
        REMOVEFILTERS(Dim_Vendedores)
    )

VAR DataFinal =
    CALCULATE(
        MAX(FATO_VENDAS[Data_Venda]),
        REMOVEFILTERS(Dim_Vendedores)
    )

RETURN
    DATEDIFF(
        DATE(
            YEAR(DataInicial),
            MONTH(DataInicial),
            1
        ),
        DATE(
            YEAR(DataFinal),
            MONTH(DataFinal),
            1
        ),
        MONTH
    ) + 1
```

---

## Meta do Período

A meta mensal é multiplicada pela quantidade de meses analisados.

```DAX
Meta_Periodo =
[Meta_Vendedor] * [Meses_Periodo]
```

No período atual:

- Meses analisados: 9
- Meta mensal total da equipe: R$ 430.000
- Meta acumulada do período: R$ 3.870.000

---

## Percentual do Período

Compara a receita acumulada com a meta acumulada do mesmo período.

```DAX
Percentual_Atingimento_Periodo =
DIVIDE(
    [Receita_Total],
    [Meta_Periodo],
    0
)
```

O resultado consolidado do projeto é aproximadamente:

**9,93%**

---

## Ranking de Vendedores

Classifica os vendedores pela Receita Total, do maior para o menor.

```DAX
Ranking_Vendedores =
IF(
    ISINSCOPE(Dim_Vendedores[Nome_Vendedor]),
    RANKX(
        ALLSELECTED(Dim_Vendedores[Nome_Vendedor]),
        [Receita_Total],
        ,
        DESC,
        DENSE
    )
)
```

---

## Total de Clientes

Quantidade distinta de clientes presentes nas vendas.

```DAX
Total_Clientes =
DISTINCTCOUNT(
    FATO_VENDAS[ID_Cliente]
)
```

---

# Medidas Geográficas

## Estado Líder em Receita

Identifica dinamicamente o estado que apresenta maior Receita Total dentro do contexto de filtros aplicado.

```DAX
Estado_Lider_Receita =
VAR TopEstado =
    TOPN(
        1,
        ADDCOLUMNS(
            ALLSELECTED(Dim_Estado[Estado]),
            "@Receita",
            [Receita_Total]
        ),
        [@Receita],
        DESC,
        Dim_Estado[Estado],
        ASC
    )

RETURN
    MAXX(
        TopEstado,
        Dim_Estado[Estado]
    )
```

---

## Receita do Estado Líder

Retorna a Receita Total correspondente ao estado com maior faturamento.

```DAX
Receita_Estado_Lider =
VAR TopEstado =
    TOPN(
        1,
        ADDCOLUMNS(
            ALLSELECTED(Dim_Estado[Estado]),
            "@Receita",
            [Receita_Total]
        ),
        [@Receita],
        DESC,
        Dim_Estado[Estado],
        ASC
    )

RETURN
    MAXX(
        TopEstado,
        [@Receita]
    )
```

---

# Regras de Negócio

Algumas regras importantes adotadas no projeto:

- Receita Total considera somente vendas com status **Concluída**.
- Quantidade Vendida considera somente vendas concluídas.
- Ticket Médio utiliza Receita Total dividida pelo número de vendas concluídas.
- Taxa de Cancelamento utiliza quantidade de vendas canceladas dividida pelo total de vendas.
- A meta original dos vendedores é mensal.
- A Meta do Período corresponde à meta mensal multiplicada pelos meses analisados.
- No conjunto atual, o período analisado corresponde a **9 meses**.
- O percentual consolidado de atingimento da meta do período é aproximadamente **9,93%**.
- O Ranking de Vendedores utiliza Receita Total e respeita os filtros aplicados no relatório.
