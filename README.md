# Data Science e Big Data na Indústria

Repositório de estudos da disciplina de **Data Science e Big Data na Indústria**, com materiais das aulas, notebooks, exercícios, bases de dados e projeto aplicado de manutenção industrial.

Este README organiza os principais conceitos e práticas encontrados nos materiais das aulas de Python e nas cinco aulas da disciplina. Para acompanhar cada exemplo completo, consulte também os PDFs e notebooks vinculados abaixo.

## Sumário

- [Objetivos de aprendizagem](#objetivos-de-aprendizagem)
- [Visão geral do conteúdo](#visão-geral-do-conteúdo)
- [Python para Data Science](#python-para-data-science)
- [Aula 1 — Ciência de Dados, KDD e Pandas](#aula-1--ciência-de-dados-kdd-e-pandas)
- [Aula 2 — Análise exploratória e visualização](#aula-2--análise-exploratória-e-visualização)
- [Aula 3 — Machine Learning supervisionado](#aula-3--machine-learning-supervisionado)
- [Aula 4 — Classificação e agrupamento](#aula-4--classificação-e-agrupamento)
- [Aula 5 — Big Data e Apache Spark](#aula-5--big-data-e-apache-spark)
- [Projeto aplicado — Manutenção industrial](#projeto-aplicado--manutenção-industrial)
- [Materiais e bases de dados](#materiais-e-bases-de-dados)
- [Como estudar e executar os notebooks](#como-estudar-e-executar-os-notebooks)
- [Glossário](#glossário)

## Objetivos de aprendizagem

Ao percorrer os materiais, o estudante pratica como:

- entender problemas e fontes de dados em ambientes industriais;
- transformar uma pergunta de negócio em uma análise de dados;
- importar, inspecionar, limpar, transformar e resumir dados com Python e Pandas;
- explorar variáveis, estatísticas, relações e padrões com gráficos;
- treinar e avaliar modelos de classificação;
- descobrir grupos de observações com aprendizado não supervisionado;
- reconhecer quando o volume de dados pede processamento distribuído;
- comunicar resultados e limitações para apoiar decisões.

## Visão geral do conteúdo

| Etapa | Assunto principal | Ferramentas e técnicas |
|---|---|---|
| Preparação | Python e ambiente de desenvolvimento | VS Code, `pip`, `venv`, Git e GitHub |
| 1 | Ciência de Dados e descoberta de conhecimento | Fontes industriais, mineração de dados e KDD |
| 2 | Exploração e comunicação dos dados | Pandas, estatística descritiva, Matplotlib e Seaborn |
| 3 | Previsão de categorias | Aprendizado supervisionado, árvore de decisão e Random Forest |
| 4 | Descoberta de perfis | K-Means, padronização, inércia e análise de clusters |
| 5 | Escala de processamento | Big Data, Data Lake, Data Warehouse, Apache Spark e PySpark |
| Projeto | Análise de falhas de máquinas | Exploração, preparação, classificação, agrupamento e processamento distribuído |

## Python para Data Science

O material introdutório apresenta Python como linguagem de propósito geral e ferramenta para análise de dados. A preparação do ambiente inclui:

- fundamentos da linguagem: sintaxe, variáveis e tipos, operadores, condicionais e laços de repetição;
- uso de números, strings, listas, tuplas, dicionários, datas e horários, funções e arquivos;
- instalar Python e usar o VS Code com a extensão Python;
- instalar bibliotecas com o `pip`;
- criar um ambiente virtual com `venv` para isolar dependências de cada projeto;
- registrar e reinstalar dependências com `requirements.txt`;
- organizar arquivos de código e dados e versionar o trabalho com Git e GitHub.

Nos exemplos, Pandas é usado para criar DataFrames, resumir dados de sensores e vendas e preparar gráficos com Matplotlib. Os exercícios incluem análise de temperaturas ao longo do tempo, comparação de faturamento entre setores e visualização da evolução de preços de ações.

**Material:** [Aula 01 — Python para Data Science](<python_aula06/Aula 01 - Python para Data Science.pdf>) · [Exemplos e exercícios Python](python_aula06/)

## Aula 1 — Ciência de Dados, KDD e Pandas

### Ciência de Dados na indústria

Indústrias podem gerar dados em sensores e máquinas, linhas de produção, sistemas de controle, registros de manutenção, consumo de energia e operações logísticas. A análise combina dados, programação, estatística e conhecimento do processo para responder perguntas práticas, como identificar indícios de falha antes que uma máquina pare.

**Mineração de dados** é a busca de padrões úteis nos dados. Ela pode envolver exploração, análise estatística e modelos; os padrões encontrados precisam ser interpretados no contexto do problema antes de orientar uma decisão.

### Processo KDD

O KDD (*Knowledge Discovery in Databases*) organiza a descoberta de conhecimento em cinco etapas:

1. **Seleção:** escolher os dados relacionados à pergunta.
2. **Pré-processamento:** verificar e tratar ausências, duplicidades e inconsistências.
3. **Transformação:** preparar os dados no formato adequado para análise.
4. **Mineração:** aplicar técnicas estatísticas ou de aprendizado de máquina para encontrar padrões.
5. **Interpretação e avaliação:** verificar se os resultados são válidos, úteis e coerentes com o problema.

O processo é iterativo: a interpretação pode mostrar que é necessário revisar os dados escolhidos ou a preparação.

### Pandas e primeiros exercícios

Pandas oferece estruturas tabulares e operações para importar e analisar dados. Os notebooks trabalham com:

- `Series` para dados unidimensionais e `DataFrame` para tabelas;
- leitura de dados e inspeção inicial com `head()`, `tail()`, `info()` e `describe()`;
- seleção de colunas e filtragem de linhas;
- médias, valores mínimos e máximos e ordenação;
- agrupamentos e agregações com `groupby()`;
- criação de novas colunas e cálculo de correlações.

Os primeiros problemas investigam a relação entre temperatura e defeitos de motores e comparam produção e consumo de energia entre máquinas. A correlação ajuda a descrever uma associação entre variáveis, mas, por si só, não prova causalidade.

**Materiais:** [PDF da Aula 1](<PDF_AULAS/Aula 01 - Data Science e Big Data na Indústria.pdf>) · [Notebook de introdução](<Códigos Aulas/Aula_01_DataScience_e_Big_Data.ipynb>) · [Exercícios resolvidos das Aulas 1 e 2](<Códigos Aulas/Exercicios_Resolvidos_Aulas_01_e_02.ipynb>)

## Aula 2 — Análise exploratória e visualização

A **análise exploratória de dados (EDA)** ajuda a entender a estrutura dos dados antes de modelar: observar dimensões e tipos, calcular estatísticas, comparar grupos, identificar valores suspeitos e investigar relações entre variáveis.

Os exercícios e notebooks estendem o uso de Pandas para:

- comparar produção, peças aprovadas e defeituosas por turno;
- resumir viagens e distâncias percorridas;
- analisar unidades vendidas, preço e faturamento por mês;
- agrupar dados e calcular indicadores para responder perguntas operacionais.

### Gráficos

Matplotlib e Seaborn apoiam a comunicação dos resultados:

- gráficos de linha para dados ordenados no tempo;
- gráficos de barras para comparar categorias;
- gráficos de dispersão para observar relações entre variáveis;
- mapas de calor para visualizar correlações entre várias colunas.

Os exemplos com Matplotlib apresentam a separação entre a figura (`Figure`) e a área de desenho (`Axes`), facilitando a configuração de título, eixos, legenda e conteúdo visual.

**Materiais:** [PDF da Aula 2](<PDF_AULAS/Aula 02 - Data Science e Big Data na Indústria.pdf>) · [Notebook — análise de produção por turno](<Códigos Aulas/Aula02DSBD_Exemplo1.ipynb>) · [Notebook — exemplos adicionais](<Códigos Aulas/Aula02DSBD_Exemplo02.ipynb>) · [Resumo e exercícios das Aulas 1 e 2](<apresentacoes/Resumo_e_Exercicios_Aulas_01_e_02.md>)

## Aula 3 — Machine Learning supervisionado

**Machine Learning** permite ajustar modelos a partir de exemplos para produzir previsões. No aprendizado **supervisionado**, os dados de treino incluem a resposta correta (rótulo). Entre as tarefas mais comuns:

- **Classificação:** prever uma categoria, como consumo alto ou baixo, ou presença ou ausência de falha.
- **Regressão:** prever um valor numérico, como consumo ou quantidade produzida.

A aula apresenta árvores de decisão e Random Forest em exemplos de operação e consumo energético. O fluxo de modelagem inclui separar atributos e rótulo, dividir os dados em treino e teste, ajustar o modelo e avaliar suas previsões em dados que não foram usados no treino.

### Preparação e avaliação

Os exercícios exploram o tratamento de dados ausentes, a distribuição das variáveis e a preparação de colunas numéricas e categóricas. Pipelines ajudam a encadear o pré-processamento e o modelo; imputação e codificação categórica podem ser aplicadas conforme o tipo de atributo.

As métricas respondem a perguntas diferentes:

- **Acurácia:** proporção total de previsões corretas.
- **Precisão:** entre as previsões positivas, quantas estavam corretas?
- **Recall (sensibilidade):** entre os positivos reais, quantos foram encontrados?
- **Matriz de confusão:** mostra acertos e tipos de erro por classe.

Em dados desbalanceados, a acurácia isolada pode ocultar falhas na classe minoritária. O custo de falsos positivos e falsos negativos deve ser considerado antes de usar um modelo em uma decisão operacional.

**Materiais:** [PDF da Aula 3](<PDF_AULAS/Aula 03 - Data Science e Big Data na Indústria.pdf>) · [Notebook — árvore de decisão e Random Forest](<Códigos Aulas/Aula_03_DSBD.ipynb>) · [Primeiros exemplos de Machine Learning](<Códigos Aulas/Exemplo1.ipynb>) · [Exemplo de preparação e classificação](<Códigos Aulas/Exemplo2.ipynb>)

## Aula 4 — Classificação e agrupamento

A aula dá continuidade à classificação de máquinas pelo consumo de energia, incluindo inspeção de dados ausentes, análise das distribuições, preparação das variáveis, comparação de modelos e interpretação das métricas. Os materiais também introduzem o aprendizado **não supervisionado**: os dados não trazem rótulos conhecidos para ensinar a resposta.

### K-Means

O **K-Means** agrupa observações por similaridade com base nos atributos selecionados:

1. escolhe-se a quantidade `K` de grupos;
2. o algoritmo ajusta centros (centroides) e associa observações ao centro mais próximo;
3. as associações e os centros são atualizados até a convergência;
4. os grupos são examinados e interpretados no contexto do problema.

Como a distância é afetada pela escala das variáveis, a padronização pode ser importante antes do agrupamento. A **inércia** ou WCSS (*Within-Cluster Sum of Squares*) mede as distâncias quadráticas dentro dos grupos. O método do cotovelo compara a inércia para diferentes valores de `K`; a escolha final também precisa fazer sentido para a aplicação.

Os exercícios usam perfis de produção e consumo de energia, viagens e variáveis de sensores de máquinas, como vibração e corrente elétrica. Um cluster é um agrupamento matemático, não uma explicação automática: cabe analisar suas características para atribuir significado operacional.

**Materiais:** [PDF da Aula 4](<PDF_AULAS/Aula 04 - Data Science e Big Data na Indústria.pdf>) · [Notebook de preparação e K-Means](<Códigos Aulas/Aula04prepDSBD.ipynb>) · [Notebook com exemplos adicionais](<Códigos Aulas/A03DSBD_Parte1.ipynb>)

## Aula 5 — Big Data e Apache Spark

**Big Data** trata da organização e do processamento de grandes volumes de dados, frequentemente provenientes de fontes diversas. A aula apresenta os **5 Vs**:

- **Volume:** quantidade de dados;
- **Velocidade:** rapidez com que são gerados e precisam ser processados;
- **Variedade:** diversidade de formatos e fontes;
- **Veracidade:** qualidade, confiabilidade e contexto dos dados;
- **Valor:** utilidade que a análise pode gerar.

Os dados também podem ser:

- **estruturados**, com esquema tabular definido;
- **semiestruturados**, com alguma organização, mas estrutura flexível;
- **não estruturados**, sem organização tabular predefinida, como imagens e documentos.

### Armazenamento e processamento distribuído

Um **Data Lake** pode armazenar grandes volumes de dados em diferentes formatos, inclusive dados ainda não transformados. Um **Data Warehouse** organiza dados integrados e preparados para consultas analíticas e relatórios. A escolha depende do uso, da governança e das necessidades do projeto.

O **Apache Spark**, acessado em Python pela API **PySpark**, distribui dados e cálculos entre partições e nós de um cluster. Os exemplos apresentam leitura de CSV em DataFrames Spark, definição e consulta de dados, filtragem, agrupamento e agregações com a API de DataFrames e SQL. Quando os dados já podem ser trabalhados em uma máquina, Pandas é conveniente; Spark é apresentado para cenários que exigem escala distribuída. A conversão para Pandas nos exemplos é usada para visualizar resultados menores com Matplotlib, não como estratégia para trazer uma base inteira muito grande para a memória local.

**Material:** [PDF da Aula 5](<PDF_AULAS/Aula 05 - Data Science e Big Data na Indústria.pdf>)

## Projeto aplicado — Manutenção industrial

O projeto reúne as etapas da disciplina em um problema de manutenção da empresa fictícia S&M Industry: analisar registros de cinco máquinas para identificar padrões associados a falhas e apoiar decisões.

O notebook do projeto percorre:

1. **Compreensão e exploração:** inspeção dos registros, colunas, tipos, estatísticas e proporção de falhas.
2. **Preparação e mineração:** investigação de duplicidades, ausências, valores extremos, distribuições e relações entre sensores.
3. **Aprendizado supervisionado:** treinamento e comparação de modelos de classificação para prever falhas.
4. **Aprendizado não supervisionado:** uso de K-Means para encontrar perfis operacionais sem fornecer o rótulo ao algoritmo.
5. **Big Data e tomada de decisão:** leitura e agregação dos dados com PySpark e discussão da diferença entre processamento local e distribuído.

Um cuidado importante do estudo é o **desbalanceamento das classes**. Por isso, acurácia sozinha não é suficiente para avaliar um detector de falhas; recall, precisão, F1 e os custos dos erros também importam. Os resultados do notebook mostram limitações do modelo testado, então suas previsões devem ser tratadas como apoio à análise, não como substituição automática da avaliação técnica.

**Arquivos do projeto:** [Notebook de análise](<Projeto senai data science big data/Projeto_Data_Science_Manutencao_Industrial.ipynb>) · [Dados de manutenção](<Projeto senai data science big data/dados_manutencao.csv>) · [Apresentação](<Projeto senai data science big data/Apresentacao_Projeto_Manutencao_Industrial.pptx>) · [Roteiro de apresentação e defesa](<Projeto senai data science big data/Roteiro_Apresentacao_e_Defesa.md>) · [Simulador de apresentação](<Projeto senai data science big data/Simulador_e_Treino_Apresentacao.html>)

## Materiais e bases de dados

### Aulas e exercícios

| Material | Conteúdo |
|---|---|
| [Apresentações em PDF — Aulas 1 a 5](PDF_AULAS/) | Slides da disciplina de Data Science e Big Data |
| [Cadernos de estudos e exercícios](<Códigos Aulas/>) | Notebooks e bases para as atividades |
| [Resumo e exercícios resolvidos das Aulas 1 e 2](<apresentacoes/Resumo_e_Exercicios_Aulas_01_e_02.md>) | Revisão conceitual e atividades com Pandas |
| [Apresentação de revisão das Aulas 1 e 2](<apresentacoes/Apresentacao_Resumo_Aulas_01_e_02.pptx>) | Slides de revisão |
| [Python para Data Science](python_aula06/) | PDF, exemplos em Python e dependências da aula |

### Bases incluídas

| Arquivo | Uso nos materiais |
|---|---|
| [consumo_energetico_alunos.csv](<Códigos Aulas/consumo_energetico_alunos.csv>) | Exercícios de análise de consumo energético |
| [dados_manutencao.csv](<Projeto senai data science big data/dados_manutencao.csv>) | Projeto de manutenção industrial e análise de falhas |
| [producao_por_turno.csv](<dados/producao_por_turno.csv>) | Produção e qualidade por turno |
| [dados_viagens.csv](<dados/dados_viagens.csv>) | Exercícios de transporte e agrupamento de viagens |
| [dados_vendas.csv](<dados/dados_vendas.csv>) | Análise de vendas e faturamento |

Há cópias de algumas bases na pasta de exercícios de aula para uso junto aos respectivos notebooks.

### Leituras complementares

Os artigos e materiais de referência enviados junto com o repositório estão em [Artigos](Artigos/) e [PDFs do projeto](<Projeto senai data science big data/>). A pasta [apresentacoes](apresentacoes/) também contém materiais de revisão em PDF e PowerPoint.

## Como estudar e executar os notebooks

1. Comece pelo PDF introdutório de Python e configure Python, VS Code e um ambiente virtual.
2. Siga a sequência das Aulas 1 a 5, alternando os slides, os notebooks e as bases de cada atividade.
3. Abra os arquivos `.ipynb` no VS Code com a extensão Jupyter ou em um ambiente compatível, como Google Colab.
4. Execute as células em ordem e confira as saídas; alguns exemplos dependem dos arquivos CSV deste repositório.
5. Para instalar as bibliotecas listadas na aula introdutória, a partir da raiz do repositório:

   ```powershell
   python -m venv .venv
   .\.venv\Scripts\Activate.ps1
   python -m pip install -r python_aula06/requirements.txt
   ```

6. Os exemplos com PySpark requerem PySpark e Java; o material da aula demonstra a execução no Google Colab.

O ambiente virtual `.venv` é local e não faz parte dos arquivos do repositório.

## Glossário

| Termo | Significado |
|---|---|
| **Atributo / feature** | Coluna de entrada usada para descrever uma observação ou alimentar um modelo. |
| **Rótulo / target** | Resposta conhecida que um modelo supervisionado aprende a prever. |
| **DataFrame** | Estrutura tabular do Pandas ou Spark, com linhas e colunas. |
| **EDA** | Análise exploratória feita para entender dados, distribuições e relações. |
| **KDD** | Processo de seleção, preparação, transformação, mineração e avaliação de conhecimento em dados. |
| **Classificação** | Previsão de uma categoria. |
| **Regressão** | Previsão de um valor numérico. |
| **Cluster** | Grupo de observações semelhantes segundo os atributos e o método usados. |
| **K-Means** | Algoritmo que agrupa observações em `K` grupos usando centroides. |
| **Pipeline** | Encadeamento reprodutível de etapas de preparação e modelagem. |
| **PySpark** | Interface Python para processamento com Apache Spark. |
| **Falso negativo** | Falha real que o modelo classificou como normal; pode ser crítico em manutenção. |
| **Falso positivo** | Caso normal que o modelo classificou como falha; pode gerar inspeções desnecessárias. |
