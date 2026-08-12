# Pipeline ETL: Tratamento e Limpeza de Dados de E-commerce

> **Projeto Prático** | *Desenvolvimento para Ciência de Dados I — UniCEUB*

## Contexto do Negócio
Atuando como **Analista de Dados Júnior** em uma empresa de e-commerce, recebi o relatório bruto de vendas `Vendas_Teste_ETL.xlsx`. O objetivo deste projeto é construir um pipeline de **ETL (Extract, Transform, Load)** em Python para tratar o dataset, eliminando ruídos, inconsistências e erros de formatação para disponibilizar uma base limpa e confiável para relatórios institucionais.

---

## ⚠ Inconsistências Identificadas na Base Bruta
O arquivo original continha diversos problemas de qualidade de dados que impediam análises diretas[cite: 1]:
- ❌ **Linhas em branco:** Registros sem nenhuma informação[cite: 1].
- ❌ **Inconsistência de texto:** Nomes de cidades com problemas de caixa alta/baixa e espaços extras (ex: `" brasilia "`, `"BRASÍLIA"`)[cite: 1].
- ❌ **Valores monetários formatados como texto:** Presença do símbolo `R$` e formatação brasileira de milhar/decimal[cite: 1].
- ❌ **Datas inválidas:** Entradas impossíveis (ex: `"32/13/2026"`)[cite: 1].
- ❌ **Registros duplicados:** Pedidos idênticos repetidos no sistema[cite: 1].
- ❌ **Valores e quantidades negativas:** Incoerência nos registros de unidades vendidas[cite: 1].

---

## Etapas do Tratamento de Dados (ETL)

O desenvolvimento foi estruturado em **7 etapas de saneamento de dados** utilizando **Python** e **Pandas**[cite: 1]:

### 1. Carregamento dos Dados
- Leitura da planilha Excel `Vendas_Teste_ETL.xlsx` utilizando a biblioteca `pandas`[cite: 1].

### 2. Remoção de Linhas Vazias
- Eliminação de registros onde **todas as colunas** estavam nulas (`df.dropna(how="all")`)[cite: 1].

### 3. Padronização de Cidades
- Remoção de espaços antes e depois do texto (`.str.strip()`)[cite: 1].
- Padronização no formato *Title Case* (primeira letra maiúscula) (`.str.lower().str.title()`) para garantir o agrupamento correto[cite: 1].

### 4. Limpeza e Conversão do Valor Unitário
- Remoção do símbolo `R$` e ajuste de pontuação para o padrão numérico do Python (`.` para casas decimais)[cite: 1].
- Conversão da coluna para tipo numérico (`pd.to_numeric`), transformando entradas inválidas em `NaN` (`errors="coerce"`)[cite: 1].

### 5. Correção de Datas Inválidas
- Conversão da coluna `data_venda` para o tipo `datetime`[cite: 1].
- Tratamento de datas impossíveis transformando-as em `NaT` (Not a Time)[cite: 1].

### 6. Remoção de Duplicatas
- Identificação e exclusão de linhas totalmente duplicadas (`df.drop_duplicates()`)[cite: 1].

### 7. Tratamento de Quantidades Negativas
- Aplicação de regra de negócio para zerar valores de quantidade negativos (`df.loc[df["quantidade"] < 0, "quantidade"] = 0`)[cite: 1].

---

## Tecnologias Utilizadas
- **Linguagem:** Python 3.x
- **Manipulação de Dados:** Pandas, NumPy[cite: 1]
- **Formato dos Dados:** Excel (`.xlsx`)[cite: 1]

---

## Como Executar o Projeto

1. **Clone o repositório:**
   ```bash
   git clone [https://github.com/NicoleCruz06/SEU-REPOSITORIO.git](https://github.com/NicoleCruz06/SEU-REPOSITORIO.git)