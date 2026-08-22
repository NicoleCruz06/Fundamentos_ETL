# Pipeline ETL: Tratamento e Limpeza de Dados Hospitalares

> **Projeto Prático** | *Desenvolvimento para Ciência de Dados I — UniCEUB*

## Contexto do Negócio
Atuando como **Analista de Dados Júnior** em uma instituição de saúde, recebi o relatório bruto de atendimentos hospitalares `Atendimentos_Hospitalares_ETL.xlsx`. O objetivo deste projeto é construir um pipeline de **ETL (Extract, Transform, Load)** em Python para tratar o dataset, eliminando ruídos, inconsistências e erros de cadastramento para disponibilizar uma base limpa e confiável para análises clínicas, operacionais e financeiras.

---

## ⚠️ Inconsistências Identificadas na Base Bruta
O arquivo original continha diversos problemas de qualidade de dados que impediam análises diretas:
- ❌ **Linhas em branco:** Registros totalmente nulos no histórico de atendimentos.
- ❌ **Inconsistência de texto:** Nomes de especialidades médicas e cidades dos pacientes com problemas de caixa alta/baixa e espaços extras (ex: `" cardiologia "`, `"CARDIOLOGIA"`).
- ❌ **Valores monetários formatados como texto:** Custo do procedimento/atendimento contendo o símbolo `R$` e formatação brasileira de milhar/decimal.
- ❌ **Datas inválidas:** Entradas impossíveis nas datas de atendimento/internação (ex: `"32/13/2026"`).
- ❌ **Registros duplicados:** Atendimentos idênticos gravados em duplicidade no sistema.
- ❌ **Valores e quantidades negativas:** Incoerência nos registros de dias de internação ou quantidade de exames/procedimentos.

---

## Etapas do Tratamento de Dados (ETL)

O desenvolvimento foi estruturado em **7 etapas de saneamento de dados** utilizando **Python** e **Pandas**:

### 1. Carregamento dos Dados
- Leitura da planilha Excel `Atendimentos_Hospitalares_ETL.xlsx` utilizando a biblioteca `pandas`.

### 2. Remoção de Linhas Vazias
- Eliminação de registros onde **todas as colunas** estavam nulas (`df.dropna(how="all")`).

### 3. Padronização de Especialidades / Cidades
- Remoção de espaços extras no início e fim do texto (`.str.strip()`).
- Padronização no formato *Title Case* (primeira letra maiúscula) (`.str.lower().str.title()`) para garantir o agrupamento correto de setores, especialidades e localidades.

### 4. Limpeza e Conversão do Custo do Procedimento
- Remoção do símbolo `R$` e ajuste de pontuação para o padrão numérico do Python (`.` para casas decimais).
- Conversão da coluna para tipo numérico (`pd.to_numeric`), transformando entradas inválidas em `NaN` (`errors="coerce"`).

### 5. Correção de Datas Inválidas
- Conversão da coluna de data de atendimento/internação para o tipo `datetime`.
- Tratamento de datas impossíveis transformando-as em `NaT` (Not a Time).

### 6. Remoção de Duplicatas
- Identificação e exclusão de linhas totalmente duplicadas (`df.drop_duplicates()`).

### 7. Tratamento de Quantidades e Dias Negativos
- Aplicação de regra de negócio para zerar valores negativos de dias de internação ou exames (`df.loc[df["dias_internacao"] < 0, "dias_internacao"] = 0`).

---

## Tecnologias Utilizadas
- **Linguagem:** Python 3.x
- **Manipulação de Dados:** Pandas, NumPy
- **Formato dos Dados:** Excel (`.xlsx`)

---

## Como Executar o Projeto

1. **Clone o repositório:**
   ```bash
   git clone [https://github.com/NicoleCruz06/SEU-REPOSITORIO.git](https://github.com/NicoleCruz06/SEU-REPOSITORIO.git)