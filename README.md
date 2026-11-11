# Dashboard de Vendas Porsche

Dashboard interativa de vendas da Porsche construída a partir de uma base bruta de 100 registros, com pipeline completo de saneamento de dados, log rastreável de correções e painel executivo em HTML com identidade visual inspirada no site da Porsche Brasil.

**Acesse a dashboard:** https://fred74227.github.io/dashboard-porsche-vendas/

## Sobre o projeto

A planilha de origem (`Porsche.xlsx`, aba `Sanitized`) continha pares de colunas brutas e sanitizadas, com problemas típicos de dados reais: datas inválidas (24 registros), formatos mistos de preço e quilometragem, textos com inconsistência de caixa e erros de digitação em status de entrega.

O projeto executa três etapas:

1. **Auditoria:** validação de cada par de colunas bruta × sanitizada com parsers independentes (datas, preços, quilometragem, anos, textos). Resultado: zero divergências reais de valor.
2. **Saneamento:** padronização e correção dos 24 registros com data inválida, sem exclusão de registros, com 100% das correções documentadas no log.
3. **Visualização:** painel HTML interativo, 100% em Português Brasil, com filtros combináveis, KPIs e respostas visuais a 3 perguntas de negócio.

## Indicadores da base saneada

| Indicador | Valor |
|---|---|
| Unidades vendidas | 100 |
| Receita total | R$ 71.630.437,99 (US$ 12.827.800,50 na origem) |
| Ticket médio | R$ 716.304,38 |
| Cidades atendidas | 79 |
| Modelos comercializados | 40 |
| Período das vendas | 28/02/2024 a 01/10/2027 |

Conversão cambial declarada como suposição: R$ 5,5840/US$ (dólar PTAX de 10/11/2026, Banco Central).

## Perguntas de negócio respondidas

- **PQ1 · Principais modelos vendidos por cidade:** ranking de modelos por volume de unidades, reativo ao filtro de cidade e aos demais filtros.
- **PQ2 · Modelos vendidos por período:** evolução mensal das unidades vendidas, reativa ao filtro de período, com modelo líder de cada mês.
- **PQ3 · Carro popular por cidade:** modelo mais vendido em cada cidade (critério: maior volume de unidades; desempate por receita total), com volume e receita de apoio.

## Filtros da dashboard

Os 5 filtros funcionam de forma combinada e atualizam todos os KPIs e gráficos:

- Modelo da Porsche
- Ano modelo
- Cidade
- Método de pagamento
- Período da venda (de/até)

## Estrutura do repositório

```
dashboard-porsche-vendas/
├── index.html            # Dashboard interativa (arquivo único, sem dependências)
├── porsche_saneada.xlsx  # Base final após saneamento (100 registros)
├── log_saneamento.md     # Log rastreável: correções, suposições e confiança
└── README.md
```

## Como executar localmente

Não há dependências nem instalação: basta abrir o `index.html` em qualquer navegador moderno.

## Stack

- HTML, CSS e JavaScript puros (sem frameworks, sem build)
- Python (pandas, openpyxl) para auditoria e saneamento
- Excel (.xlsx) como formato de entrega da base tratada

## Autor

Frederico Silvestre Leôncio
Analista em transição para Dados e Inteligência Artificial
[LinkedIn](https://linkedin.com/in/frederico-leoncio-0a1633294)
