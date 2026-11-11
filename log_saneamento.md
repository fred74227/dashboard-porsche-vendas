# Log de Saneamento — Porsche.xlsx

**Data de geração:** 11/11/2026  
**Fonte:** `Porsche.xlsx` (aba `Sanitized`, 100 registros × 21 colunas) + `Invalidos_saneados.xlsx` (24 datas corrigidas, enviado pelo usuário)

## 1. Metodologia

A auditoria validou cada par de colunas bruta × sanitizada com parsers independentes (datas, preços, quilometragem, anos, textos). As colunas sanitizadas da planilha foram adotadas como base. Nenhum valor foi alterado sem registro e nenhuma fonte externa foi usada para os dados de vendas.

## 2. Suposições declaradas

| Suposição | Valor adotado | Confiança |
|---|---|---|
| Taxa de câmbio para conversão US$ → R$ (decisão do usuário) | R$ 5,5840 por US$ 1,00 (dólar PTAX de 10/11/2026, Banco Central) | Alto |
| Correção das 24 datas `INVALID` | Valores fornecidos pelo usuário em `Invalidos_saneados.xlsx`, incorporados integralmente, sem exclusão de registros | Alto |
| Critério do insight “carro popular por cidade” (decisão do usuário) | Maior volume de unidades vendidas; desempate por receita total | Alto |

## 3. Resultado da auditoria (bruta × sanitizada)

**Zero divergências reais de valor.** Todos os pares de colunas reconciliaram após parsing correto dos formatos mistos (ex.: “USD 112.750” = 112750; “$121k” = 121000; “KM 18,900” = 11.744 milhas; “twenty twenty four” = 2024).

| Campo | Registros com padronização (bruta ≠ sanitizada) | Regra aplicada |
|---|---|---|
| `sale_date` → `SaleDateSanitized` | 100 (24 inválidas + 76 formatos mistos) | Conversão para ISO `YYYY-MM-DD`; 24 inválidas corrigidas pelo usuário |
| `sale_price` → `SalesPriceSanitized` | 100 | Remoção de símbolos/moeda, normalização de separadores, sufixo “k” × 1000, valores por extenso |
| `vehicle_mileage` → `VehicleMileageSanitized` | 97 | Extração numérica; km × 0,621371; “zero/new” → 0; valores por extenso |
| `payment_method` → `PayMethodSanitized` | 87 | Normalização para 1 dos 9 métodos do catálogo |
| `delivery_status` → `DeliveryStatusSanitized` | 91 | Normalização de caixa, erros (“DELIVERD”) e ruído (“delivered!!!”) |
| `state` → `StateSanitized` | 68 | Sigla de 2 letras maiúscula |
| `model_year` → `ModelYearSanitized` | 24 | Ano por extenso e padrão “20-23” → ano; faixa validada 2020–2026 (100% dentro) |
| `city` → `CitySanitized` | 30 | Padronização de caixa (ex.: “boston” → “Boston”) |
| `porsche_model` → `PorscheModelSanitized` | 0 | Já padronizada (40 modelos distintos) |
| `sale_id` | 0 | Único, sem duplicados |
| `sale_price` (faixa) | 0 | 100% dentro da faixa US$ 58.900–US$ 286.500 |

## 4. Correção das 24 datas inválidas (destino dos registros)

Conforme decisão do usuário, **nenhum registro foi excluído**: os 24 registros com data `INVALID` tiveram a data corrigida a partir do arquivo `Invalidos_saneados.xlsx` e permanecem na base (100 registros no total).

| sale_id | Data bruta (inválida) | Data corrigida |
|---|---|---|
| 6 | 2024-02-30 | 28/02/2024 |
| 9 | April 31st, 2024 | 30/07/2024 |
| 13 | 2024/15/07 | 15/07/2024 |
| 17 | 2024-10-40 | 04/10/2024 |
| 22 | 01/32/2025 | 23/01/2025 |
| 24 | February 29th, 2025 | 28/02/2025 |
| 28 | 2025/04/31 | 30/04/2025 |
| 31 | 06/31/2025 | 30/06/2025 |
| 36 | 2025-09-31 | 30/09/2025 |
| 43 | 2025/18/11 | 18/11/2025 |
| 44 | November 31st, 2025 | 30/11/2025 |
| 47 | 2025-12-40 | 04/12/2025 |
| 52 | February 30th, 2026 | 28/02/2026 |
| 57 | 03/32/2026 | 30/03/2026 |
| 59 | April 31st, 2026 | 31/08/2026 |
| 67 | 2026-06-31 | 30/06/2026 |
| 70 | 2026-07-35 | 31/07/2026 |
| 81 | 11/31/2026 | 30/11/2026 |
| 84 | 2026-12-38 | 03/12/2026 |
| 89 | February 30th, 2027 | 28/02/2027 |
| 93 | 2027/15/04 | 15/04/2027 |
| 94 | April 31st, 2027 | 30/04/2027 |
| 97 | 2027-06-40 | 04/06/2027 |
| 102 | August 32nd, 2027 | 31/08/2027 |

Observação de interpretação: correções como “2024-02-30 → 28/02/2024” seguem a regra de ajuste ao último dia válido; outras (ex.: “April 31st, 2024 → 30/07/2024”) refletem a data definida pelo usuário no arquivo enviado e foram incorporadas como fornecidas.

## 5. Conversão monetária

Todos os preços foram convertidos de dólar para real com a taxa declarada de R$ 5.5840/US$ (PTAX 10/11/2026). Receita total: US$ 12.827.800,50 → R$ 71.630.437,99. A coluna `preco_usd` foi preservada na base saneada.

## 6. Desvio de ferramenta declarado

O prompt previa a construção da dashboard exclusivamente com o plugin Canva. Nesta sessão, as ferramentas de geração do Canva não estavam disponíveis para uso; para não comprometer a entrega, a dashboard HTML foi construída diretamente, seguindo integralmente a identidade visual Porsche e os demais requisitos (filtros combináveis, KPIs, 3 perguntas de negócio, PT-BR).

## 7. Indicadores finais da base saneada

- Unidades vendidas: **100**
- Receita total: **R$ 71.630.437,99**
- Ticket médio: **R$ 716.304,38**
- Cidades atendidas: **79**
- Modelos comercializados: **40**
- Período das vendas: **28/02/2024 a 01/10/2027**
