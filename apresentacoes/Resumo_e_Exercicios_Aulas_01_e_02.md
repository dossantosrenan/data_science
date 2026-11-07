# Caderno de Estudos e Resolução de Exercícios — Aulas 01 e 02
**Curso:** Pós-Graduação em Data Science e Big Data na Indústria  
**Disciplina:** Data Science e Big Data  
**Professor:** Daniel Vieira  
**Instituição:** Centro Universitário SENAI - Campus Roberto Mange  

---

# PARTE 1 — AULA 01: RESUMO TEÓRICO & METODOLÓGICO

## 1.1 Contexto e Desafio da Indústria 4.0
O setor industrial contemporâneo opera sob forte pressão por redução de custos, eficiência energética e eliminação de desperdícios. Historicamente, a manutenção e a gestão da produção eram essencialmente **reativas (corretivas)**: a intervenção só acontecia após a ocorrência de quebras ou paralisações de linha, gerando custos elevados com componentes destruídos, horas ociosas e atrasos em entregas.

A Ciência de Dados e o Big Data surgem para transformar esse cenário através da pergunta norteadora:  
> **"É possível identificar sinais de falha antes de a máquina parar?"**

A resposta é sim, desde que os dados coletados ao longo do processo produtivo sejam tratados, minerados e convertidos em conhecimento acionável.

---

## 1.2 Onde uma Indústria Gera Dados?
Em uma fábrica automatizada, os dados provêm de múltiplos níveis da pirâmide de automação:
1. **Chão de Fábrica e Instrumentação (Níveis 0 e 1):**
   - Sensores de telemetria contínua: temperatura (°C), vibração mecânica (mm/s), pressão hidráulica/pneumática (bar), corrente elétrica (A), vazão e horímetro.
   - Dispositivos de borda (IoT) e microcontroladores dedicados.
2. **Controle e Supervisão (Níveis 2 e 3):**
   - Controladores Lógicos Programáveis (CLPs), Interfaces Homem-Máquina (IHMs) e sistemas SCADA.
   - Sistemas de Execução da Manufatura (MES), que apontam ordens de produção, tempos de ciclo, paradas e refugo.
3. **Gestão Corporativa (Nível 4):**
   - Sistemas ERP (gestão de estoques, compras, faturamento e custos).
   - Sistemas CMMS/GMAO (histórico de ordens de serviço de manutenção corretiva e preventiva).

---

## 1.3 O Processo KDD (Knowledge Discovery in Databases)
O KDD é o referencial metodológico consagrado para transformar dados brutos em conhecimento estratégico. No ambiente industrial, ele é estruturado em 5 fases sequenciais:

```
[Dados Brutos de Sensores]
         ↓
  1. Seleção (filtrar variáveis e equipamentos relevantes)
         ↓
  2. Pré-processamento (limpeza de ruídos, nulos e duplicatas)
         ↓
  3. Transformação (padronização de escalas e novas métricas)
         ↓
  4. Mineração de Dados (modelos preditivos e clusters)
         ↓
  5. Interpretação & Avaliação (validação técnica e implantação no chão de fábrica)
```

1. **Seleção dos Dados:** Escolha das variáveis que possuem correlação física ou operacional com o problema investigado (ex.: descartar telemetrias irrelevantes e focar nos sensores térmicos e vibratórios).
2. **Pré-processamento:** Tratamento de valores ausentes (`NaN`), eliminação de leituras espúrias geradas por oscilações elétricas na instrumentação e remoção de registros repetidos causados por falhas de rede.
3. **Transformação:** Conversão de unidades, normalização de grandezas com escalas muito diferentes (como horas em milhares versus vibração de 0 a 15) e engenharia de atributos (como taxas de defeito ou indicadores de consumo específico).
4. **Mineração de Dados (Data Mining):** Aplicação de técnicas matemáticas e estatísticas para descoberta de padrões ocultos, englobando aprendizado supervisionado (classificação e regressão) e aprendizado não supervisionado (agrupamentos/perfis).
5. **Interpretação e Avaliação:** Tradução dos resultados matemáticos em regras práticas para operadores e gerentes, validando se o conhecimento gerado atende às metas de disponibilidade e confiabilidade da planta.

---

## 1.4 O Ecossistema Python e a Biblioteca Pandas
Python é a linguagem padrão na ciência de dados industrial pela sua vasta biblioteca de pacotes abertos.
* **Pandas:** Biblioteca fundamental para ingestão, manipulação, limpeza e análise tabular de dados. Suporta formatos industriais comuns como CSV, Excel (`.xlsx`) e Parquet.
* **Estruturas Básicas:**
  - `Series`: Vetor unidimensional rotulado (equivale a uma coluna isolada).
  - `DataFrame`: Estrutura bidimensional tabular (linhas e colunas), análoga a uma planilha ou tabela de banco de dados SQL.
* **Principais Comandos Exploratórios:**
  - `.head()` e `.tail()`: Visualização das linhas iniciais e finais.
  - `.info()`: Diagnóstico de tipos de dados (`dtypes`) e contagem de valores não nulos.
  - `.describe()`: Quadro estatístico paramétrico (média, desvio-padrão, mínimos, quartis e máximos).
  - `.query()` e filtros booleanos: Seleção condicional de subconjuntos de dados.
  - `.groupby()`: Agrupamento por categorias para sumarização com funções como `.mean()`, `.sum()` e `.agg()`.
  - `.corr()`: Coeficiente de correlação linear de Pearson entre variáveis quantitativas.

---

# PARTE 2 — AULA 01: EXERCÍCIOS RESOLVIDOS PASSO A PASSO

## 2.1 Exercício 1 (Aula 01): Motores Industriais, Temperatura e Defeitos

### Contexto e Pergunta Norteadora
Foi disponibilizado um conjunto de dados monitorando 5 lotes de motores (`Motor A`, `Motor B` e `Motor C`).  
**Pergunta do exercício:** *"Será que o aumento de defeitos está relacionado ao aumento da temperatura?"*

### Código em Python
```python
import pandas as pd

# 1. Criação do DataFrame
dados = {
    "produto": ["Motor A", "Motor B", "Motor A", "Motor C", "Motor B"],
    "producao": [100, 120, 110, 90, 130],
    "defeitos": [5, 12, 6, 3, 15],
    "temperatura": [70, 82, 73, 68, 85]
}
df = pd.DataFrame(dados)

# 2. Seleção e Filtros
temp_alta = df[df["temperatura"] > 75]
criticos = df[(df["temperatura"] > 75) & (df["defeitos"] > 10)]

# 3. Estatísticas e Agrupamento
media_temp = df["temperatura"].mean()
media_prod = df["producao"].mean()
resumo_produto = df.groupby("produto").agg({
    "producao": "mean",
    "defeitos": "mean",
    "temperatura": "mean"
})

# 4. Nova coluna: Taxa percentual de defeitos
df["taxa_defeitos"] = (df["defeitos"] / df["producao"]) * 100

# 5. Matriz de Correlação
matriz_corr = df[["producao", "defeitos", "temperatura"]].corr()
```

### Resultados Obtidos
1. **Dados Gerais:**
   - Produção média geral: **110,0 peças**.
   - Temperatura média geral: **75,6 °C** (mínima de 68 °C no Motor C e máxima de 85 °C no Motor B).
2. **Comportamento por Produto:**
   - **Motor A:** Produção média = 105 peças | Defeitos médios = 5,5 | Temperatura média = 71,5 °C | Taxa de defeitos = 5,0% a 5,45%.
   - **Motor B:** Produção média = 125 peças | Defeitos médios = 13,5 | Temperatura média = 83,5 °C | Taxa de defeitos = 10,0% a 11,54%.
   - **Motor C:** Produção média = 90 peças | Defeitos médios = 3,0 | Temperatura média = 68,0 °C | Taxa de defeitos = 3,33%.
3. **Matriz de Correlação de Pearson:**
   - Produção x Defeitos: **+0,9669**
   - Produção x Temperatura: **+0,9693**
   - **Defeitos x Temperatura:** **+0,9951**

### Resposta à Pergunta Investigativa
**Sim, com comprovação matemática cabal.**  
O coeficiente de correlação linear de Pearson entre temperatura e defeitos é de **+0,9951**, indicando uma associação positiva quase perfeita. Na prática fabril, o superaquecimento dos motores durante a montagem ou usinagem atua como o principal sintoma e acelerador de desajustes mecânicos e quebra de tolerâncias dimensionais, elevando exponencialmente o número de peças refugadas.

---

## 2.2 Exercício 2 (Aula 01 / Exercício 1 da Aula 02): Análise de Produção e Eficiência Energética

### Enunciado
Você tem dados de produção e consumo de energia elétrica de 5 máquinas industriais (A, B, C, D e E):
* Máquina A: 1.250 peças, 420 kWh
* Máquina B: 1.380 peças, 465 kWh
* Máquina C: 1.190 peças, 390 kWh
* Máquina D: 1.450 peças, 510 kWh
* Máquina E: 1.320 peças, 405 kWh

### Código em Python
```python
import pandas as pd

df = pd.DataFrame({
    "maquina": ["A", "B", "C", "D", "E"],
    "producao": [1250, 1380, 1190, 1450, 1320],
    "energia": [420, 465, 390, 510, 405]
})

# a) Máquina que produziu mais
maq_mais_prod = df.loc[df["producao"].idxmax()]

# b) Máquina que menos consumiu energia
maq_menos_energ = df.loc[df["energia"].idxmin()]

# c) Produção média
media_prod = df["producao"].mean()

# d) Consumo médio
media_energ = df["energia"].mean()

# e) Ordenação por produção decrescente
df_ordenado = df.sort_values(by="producao", ascending=False)

# f) Cálculo da eficiência (produção / energia)
df["eficiencia"] = df["producao"] / df["energia"]

# g) Máquina mais eficiente
maq_mais_eficiente = df.loc[df["eficiencia"].idxmax()]
```

### Respostas Detalhadas
* **a) Qual máquina produziu mais?**  
  **Máquina D**, com **1.450 unidades produzidas**.
* **b) Qual máquina consome menos energia?**  
  **Máquina C**, com consumo de **390 kWh**.
* **c) Qual foi a produção média das máquinas?**  
  **1.318,00 peças** por máquina.
* **d) Qual foi o consumo médio de energia?**  
  **438,00 kWh** por máquina.
* **e) Ordene as máquinas da maior para a menor produção:**
  1. Máquina D: 1.450 peças (510 kWh)
  2. Máquina B: 1.380 peças (465 kWh)
  3. Máquina E: 1.320 peças (405 kWh)
  4. Máquina A: 1.250 peças (420 kWh)
  5. Máquina C: 1.190 peças (390 kWh)
* **f) Tabela de Eficiência Calculada ($\text{peças} / \text{kWh}$):**
  - Máquina A: $1.250 / 420 = \mathbf{2{,}9762}$ peças/kWh
  - Máquina B: $1.380 / 465 = \mathbf{2{,}9677}$ peças/kWh
  - Máquina C: $1.190 / 390 = \mathbf{3{,}0513}$ peças/kWh
  - Máquina D: $1.450 / 510 = \mathbf{2{,}8431}$ peças/kWh
  - Máquina E: $1.320 / 405 = \mathbf{3{,}2593}$ peças/kWh
* **g) Qual máquina apresentou a melhor relação entre produção e consumo de energia?**  
  **Máquina E**, com eficiência de **3,2593 peças por kWh**.

> **Insight para Engenharia de Produção:**  
> A Máquina D é a maior produtora em volume absoluto (1.450 peças), porém é **a menos eficiente energeticamente de toda a planta** (apenas 2,84 peças/kWh). A Máquina E consome quase 20% menos energia por unidade produzida. Em um plano de gestão energética (ISO 50001), a Máquina E deve ser priorizada para turnos contínuos.

---

# PARTE 3 — AULA 02: RESUMO TEÓRICO & METODOLÓGICO

## 3.1 Aprofundamento da Análise Exploratória de Dados (EDA)
Na Aula 02, o foco avançou da manipulação elementar para a **análise diagnóstica de bases industriais com múltiplos registros e séries temporais**. 

Uma EDA completa no ambiente produtivo exige responder a três perguntas preliminares:
1. **Quais variáveis são numéricas e quais são categóricas?**  
   - Numéricas contínuas (temperatura, horas de ciclo, quilometragem).
   - Numéricas discretas (contagens de peças, quantidade de viagens).
   - Categóricas nominais/ordinais (turnos de trabalho, identificadores de máquina, dias da semana).
2. **Há dados ausentes (`NaN`) ou repetidos (duplicatas)?**  
   - Duplicatas inflam artificialmente contagens e distorcem métricas de qualidade.
   - Nulos devem ser investigados antes de qualquer descarte ou imputação.
3. **Qual é o comportamento das distribuições?**  
   - Comparação entre média e mediana para diagnosticar assimetrias e presença de outliers operacionais.

---

## 3.2 Visualização Orientada a Objetos com Matplotlib e Seaborn
Para comunicar resultados técnicos com clareza, a disciplina introduziu a sintaxe estruturada:
```python
import matplotlib.pyplot as plt
import seaborn as sns

fig, ax = plt.subplots(figsize=(8, 5))
```
* `fig` (Figure): A tela / moldura que abriga toda a visualização.
* `ax` (Axes): O sistema de coordenadas onde os dados são plotados (gráficos de barras, linhas ou dispersão).
* `figsize=(8, 5)`: Define a largura (8 pol) e altura (5 pol) para visualização adequada em relatórios.
* **Heatmap (Mapa de Calor):** Recurso gráfico do Seaborn (`sns.heatmap(corr, annot=True, cmap='coolwarm')`) utilizado para avaliar visualmente coeficientes de correlação, permitindo detectar colinearidades em sensores industriais em segundos.

---

# PARTE 4 — AULA 02: EXERCÍCIOS RESOLVIDOS PASSO A PASSO

## 4.1 Exemplo 2 (Aula 02): Desempenho e Qualidade de Produção por Turno

### Contexto
Base `producao_por_turno.csv` com 100 registros cobrindo data, turno (Manhã, Tarde e Noite), produto, peças produzidas, peças defeituosas e peças aprovadas.

### Código em Python
```python
import pandas as pd

df_turno = pd.read_csv('producao_por_turno.csv')

# a) Total de peças produzidas
total_pecas = df_turno['pecas_produzidas'].sum()

# b) Turno com maior produção total
prod_turno = df_turno.groupby('turno')['pecas_produzidas'].sum()

# c) Quantidade média de peças por registro em cada turno
media_turno = df_turno.groupby('turno')['pecas_produzidas'].mean()

# d) Turno com maior percentual de peças defeituosas
resumo_qualidade = df_turno.groupby('turno')[['pecas_produzidas', 'pecas_defeituosas']].sum()
resumo_qualidade['pct_defeitos'] = (resumo_qualidade['pecas_defeituosas'] / resumo_qualidade['pecas_produzidas']) * 100

# e) Correlação entre peças produzidas e peças defeituosas
corr_prod_def = df_turno[['pecas_produzidas', 'pecas_defeituosas']].corr().loc['pecas_produzidas', 'pecas_defeituosas']
```

### Respostas Detalhadas
* **a) Qual é a quantidade total de peças produzidas durante o período analisado?**  
  **29.479 peças**.
* **b) Qual turno apresenta a maior produção total de peças?**  
  **Turno Manhã**, com **10.777 peças** (Tarde: 9.937 peças | Noite: 8.765 peças).
* **c) Qual é a quantidade média de peças produzidas por registro em cada turno?**  
  - **Manhã:** **316,97 peças/registro**
  - **Tarde:** **301,12 peças/registro**
  - **Noite:** **265,61 peças/registro**
* **d) Qual turno apresenta o maior percentual de peças defeituosas em relação à sua produção total?**  
  **Turno Manhã**, com **3,32% de refugo** (358 defeitos em 10.777 peças).  
  *(Noite teve 3,16% e Tarde teve 3,08%)*.
* **e) Existe correlação entre a quantidade de peças produzidas e a quantidade de peças defeituosas?**  
  **Sim.** O coeficiente de correlação de Pearson é **r = +0,3697**.  
  Existe uma **correlação positiva moderada**: quanto maior o ritmo ou o volume total produzido em um lote/turno, maior tende a ser a contagem absoluta de itens defeituosos gerados.

---

## 4.2 Exercício 2 (Aula 02): Transporte e Logística de Frotas

### Contexto
Base `dados_viagens.csv` contendo 100 registros diários de operações de transporte, com data, dia da semana, quantidade de viagens e quilometragem total percorrida.

### Código em Python
```python
import pandas as pd

df_viagens = pd.read_csv('dados_viagens.csv')

# a) Total de viagens no período
total_viagens = df_viagens['quantidade_viagens'].sum()

# b) Dia com a maior quantidade de viagens
dia_max = df_viagens.loc[df_viagens['quantidade_viagens'].idxmax()]

# c) Média diária de viagens
media_diaria = df_viagens['quantidade_viagens'].mean()

# d) Mês com maior quantidade total de viagens
df_viagens['mes'] = pd.to_datetime(df_viagens['data']).dt.to_period('M').astype(str)
viagens_mes = df_viagens.groupby('mes')['quantidade_viagens'].sum()

# e) Correlação entre quantidade de viagens e distância total
corr_viag_dist = df_viagens[['quantidade_viagens', 'distancia_total_km']].corr().loc['quantidade_viagens', 'distancia_total_km']
```

### Respostas Detalhadas
* **a) Quantas viagens foram realizadas durante todo o período analisado?**  
  **2.893 viagens**.
* **b) Qual dia apresentou a maior quantidade de viagens?**  
  O dia **26/02/2026 (Quinta-feira)**, com um pico de **48 viagens** (distância de 1.065,5 km).
* **c) Qual é a média diária de viagens realizadas?**  
  **28,93 viagens por dia** (com desvio-padrão de 9,11 viagens).
* **d) Em qual mês foi registrada a maior quantidade total de viagens?**  
  No mês de **Janeiro de 2026 (2026-01)**, com **901 viagens acumuladas**.  
  *(Fevereiro/2026 teve 816 viagens; Março/2026 teve 895 viagens; Abril/2026 teve 281 viagens parciais)*.
* **e) Existe correlação entre a quantidade de viagens realizadas e a distância total percorrida?**  
  **Sim, fortíssima.** O coeficiente de correlação linear é **r = +0,8694**.  
  Isso demonstra que a operação de transporte possui rotas relativamente homogêneas: o aumento de demanda em número de fretes reflete-se de maneira diretamente proporcional no desgaste da frota e no consumo de combustível.

---

## 4.3 Exercício 3 (Aula 02): Desempenho Comercial do Produto A

### Contexto
Base `dados_vendas.csv` com 100 registros mensais contendo mês, produto (`Produto A`), unidades vendidas, preço unitário praticado (R$) e faturamento total (R$).

### Código em Python
```python
import pandas as pd

df_vendas = pd.read_csv('dados_vendas.csv')

# a) Quantidade total de unidades vendidas
total_vendido = df_vendas['unidades_vendidas'].sum()

# b) Mês com maior faturamento
mes_recorde = df_vendas.loc[df_vendas['faturamento_rs'].idxmax()]

# c) Faturamento total obtido com Produto A
faturamento_total = df_vendas['faturamento_rs'].sum()

# d) Ano com maior quantidade de unidades vendidas
df_vendas['ano'] = df_vendas['mes'].str.split('-').str[0]
vendas_por_ano = df_vendas.groupby('ano')['unidades_vendidas'].sum()

# e) Relação entre preço unitário e unidades vendidas
corr_preco_vendas = df_vendas[['preco_unitario_rs', 'unidades_vendidas']].corr().loc['preco_unitario_rs', 'unidades_vendidas']
```

### Respostas Detalhadas
* **a) Qual foi a quantidade total de unidades vendidas durante o período analisado?**  
  **24.499 unidades vendidas**.
* **b) Qual mês apresentou o maior faturamento?**  
  O mês de **Novembro de 2025 (2025-11)**, registrando **R$ 22.516,32** de faturamento (com 366 unidades vendidas ao preço de R$ 61,52).
* **c) Qual foi o faturamento total obtido com a comercialização do Produto A?**  
  **R$ 1.281.779,17** acumulados ao longo dos 100 meses.
* **d) Qual ano apresentou a maior quantidade de unidades vendidas?**  
  O ano de **2025**, com **3.511 unidades vendidas**.  
  *(Histórico: 2018: 2.330 | 2019: 2.363 | 2020: 2.600 | 2021: 2.800 | 2022: 3.102 | 2023: 3.280 | 2024: 3.370 | 2025: 3.511 | 2026: 1.143 parcial)*.
* **e) Existe relação entre o preço unitário do produto e a quantidade de unidades vendidas?**  
  **Sim.** A correlação de Pearson é **r = +0,7713** (correlação positiva forte).  
  **Interpretação Econômica:**  
  Sob a ótica teórica convencional de demanda, preços mais altos tendem a reduzir o consumo. No entanto, nesta série temporal histórica, observamos a consolidação e amadurecimento de um produto industrial: a demanda cresceu continuamente ano a ano, mesmo com os reajustes inflacionários progressivos no preço unitário (que subiu gradualmente de R$ 39,90 em 2018 até R$ 62,67 em 2026).

---

# PARTE 5 — GUIA DE APRESENTAÇÃO PARA O PROFESSOR DANIEL VIEIRA

Ao apresentar este trabalho em aula ou gravar um vídeo explicativo para o professor Daniel Vieira, estruture sua fala em 4 momentos objetivos (cerca de 5 a 7 minutos):

1. **Abertura e Metodologia (1 min):**  
   Explique que as Aulas 01 e 02 forneceram o ferramental técnico de análise exploratória com Pandas orientado pelo processo KDD, conectando as fontes de dados de chão de fábrica (sensores, CLPs e MES) ao processo decisório.
2. **Defesa dos Exercícios da Aula 01 (2 min):**  
   - Mostre como a correlação de Pearson de +0,995 provou que a temperatura excessiva nos motores acelera a taxa de peças defeituosas.
   - Enfatize a análise energética das máquinas: mostre que a Máquina D foi quem mais produziu (1.450 peças), mas a Máquina E foi a campeã real de eficiência (3,26 peças/kWh).
3. **Defesa dos Exercícios da Aula 02 (2 min):**  
   - Na análise de turnos, destaque que o turno da Manhã teve a maior produção (10.777 peças), mas também a maior taxa de defeito (3,32%), com correlação moderada (0,37).
   - Na logística, aponte a alta correlação de +0,87 entre viagens e distância percorrida no mês de pico (Janeiro/2026 com 901 viagens).
   - No Produto A, comente sobre a receita acumulada de R$ 1,28 milhão e o ano recorde de 2025.
4. **Fechamento e Integração (1 min):**  
   Ressalte que todo esse aprendizado prático com Pandas e estatística descritiva serviu de alicerce para desenvolver as etapas posteriores da disciplina (machine learning supervisionado, K-Means e PySpark no projeto integrador da S&M Industry).

