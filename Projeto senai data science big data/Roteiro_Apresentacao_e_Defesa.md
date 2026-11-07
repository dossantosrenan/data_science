# Guia Definitivo de Apresentação: Manutenção Preditiva Industrial
**Projeto Integrador: Data Science e Big Data Aplicados à Indústria**  
**Instituição:** Centro Universitário SENAI – Campus Roberto Mange  
**Professor:** Me. Daniel Vieira | **Caso:** S&M Industry Tech  

---

## 1. Visão Geral e Storytelling do Projeto

O segredo de uma apresentação nota 10 no SENAI e em pós-graduações é **conectar a técnica ao chão de fábrica e ao negócio**. 

A sua narrativa central é uma jornada de transformação:
1. **O Drama da Fábrica (O Problema):** A S&M Industry possui 5 máquinas críticas ($M_{01}$ a $M_{05}$). Elas quebram de surpresa porque a manutenção é puramente **corretiva** (espera quebrar para consertar). Isso causa paradas de linha, multas contratuais e prejuízo financeiro.
2. **A Oportunidade dos Dados:** As máquinas já possuem sensores de telemetria coletando vibração, temperatura, pressão, corrente elétrica e horas de funcionamento. A diretoria pediu para você usar Ciência de Dados e Big Data para prever e evitar essas paradas.
3. **O Rigor Científico:** Você tratou a base com extremo cuidado metodológico (sem atalhos errados: não usou acurácia enganosa, não fez shuffle aleatório para não "olhar o futuro", não deletou outliers que eram as próprias quebras).
4. **Os Dois Braços de IA:**
   - **Supervisionado (Random Forest):** Classifica se há falha iminente, analisando o trade-off crítico entre falso alarme vs. quebra não detectada.
   - **Não Supervisionado (K-Means):** Cria um "Semáforo de Saúde" que já pode entrar em operação amanhã no chão de fábrica, alertando quando a máquina entra na zona de perigo ($>8.000$ h e vibração $>3{,}5$ mm/s).
5. **A Escalabilidade Industrial (Big Data com PySpark):** O Pandas resolve o protótipo com 5.000 linhas, mas uma fábrica 4.0 real tem centenas de máquinas gerando gigabytes por dia. Você demonstrou no Spark a arquitetura distribuída pronta para nuvem e streaming.
6. **Recomendações Práticas (Retorno ao Negócio):** Você não entrega só código; entrega um plano de ação em 3 horizontes (curto, médio e longo prazo) que a gerência pode executar imediatamente.

---

## 2. Roteiro de Fala Slide a Slide (Tempo Total: 7 a 9 minutos)

Este roteiro foi planejado para você falar com segurança, clareza e ritmo natural de um profissional apresentando uma solução para a diretoria ou banca.

---

### Slide 1: Capa e Abertura (0:00 - 0:45)
- **Título no Slide:** *Projeto Integrador Final | Data Science & Big Data - Manutenção Preditiva em Equipamentos Industriais*
- **O que você fala:**
  > *"Olá a todos, professor Daniel e colegas. Hoje apresento o meu Projeto Integrador da disciplina de Data Science e Big Data. O tema que desenvolvi é de aplicação direta no setor produtivo: **Manutenção Preditiva em Equipamentos Industriais**, aplicando Análise Exploratória, Modelagem Preditiva com Machine Learning e processamento distribuído com Apache Spark na empresa S&M Industry. O objetivo aqui foi responder como a Ciência de Dados pode tirar uma indústria do modo reativo e transformá-la em uma operação inteligente e preditiva."*

---

### Slide 2: Introdução & Cenário do Negócio (0:45 - 1:45)
- **O que destacar no slide:** O desafio da S&M Industry (5 máquinas críticas M01 a M05, custos de paradas) e a Pergunta Norteadora.
- **O que você fala:**
  > *"Para contextualizar o problema: a S&M Industry opera equipamentos automatizados em regime contínuo. O grande gargalo deles são as paradas não programadas. Hoje, a empresa atua na **manutenção corretiva**: a máquina quebra, a linha para, o operador chama a manutenção e o prejuízo se acumula com atrasos de entrega e componentes danificados.  
  Como os equipamentos já contam com sensores instalados, a diretoria encomendou este projeto com uma pergunta central:  
  **'Como utilizar Data Science, Machine Learning e Big Data para identificar padrões de falhas e apoiar decisões estratégicas de manutenção?'**  
  Para resolver isso, estruturei o trabalho em 5 etapas bem definidas: exploração com Pandas, mineração e limpeza rigorosa, modelagem supervisionada com validação temporal, clusterização com K-Means para segmentação de saúde e escalabilidade com PySpark."*

---

### Slide 3: Análise Exploratória Inicial - Etapa 1 (1:45 - 2:45)
- **O que destacar no slide:** Gráfico de falhas por máquina, 5.050 registros, e o **desbalanceamento crítico** (18% falha vs. 82% normal).
- **O que você fala:**
  > *"Entrando na Etapa 1, fiz a exploração inicial da telemetria bruta. Temos uma base com **5.050 registros** e 8 atributos, acompanhando 5 máquinas entre janeiro e fevereiro de 2026.  
  Temos leituras de temperatura, vibração mecânica, pressão hidráulica, corrente elétrica e horímetro de operação.  
  Aqui encontramos o primeiro alerta crítico do projeto: **o desbalanceamento de classes**. Temos 82% de registros em operação normal e apenas 18% de falhas.  
  Por que isso é tão importante? Porque define nossa postura metodológica: **a acurácia tradicional é uma métrica cega para este problema**. Se criarmos um modelo 'preguiçoso' que simplesmente disser 'nunca vai quebrar', ele teria 82% de acurácia acertando zero falhas!  
  Ao analisar as máquinas individualmente, a **M04** despontou com a maior taxa de quebras do lote, com quase 19%."*

---

### Slide 4: Qualidade & Mineração de Dados - Etapa 2 (2:45 - 3:55)
- **O que destacar no slide:** Tratamento de 50 duplicatas, 50 nulos por sensor no Pipeline, decisão sobre outliers (278 °C) e correlações (+0.38 horas, +0.30 vibração).
- **O que você fala:**
  > *"Na Etapa 2, passamos para a higienização e engenharia dos dados. Encontrei e removi **50 duplicatas exatas**, consolidando a base em 5.000 registros redondos.  
  Identifiquei também 50 valores ausentes por sensor — exatamente 1% da base. Mantive esses nulos na fase exploratória e apliquei a imputação pela mediana via *Pipeline* dentro da modelagem, garantindo que não houvesse vazamento de dados (*data leakage*).  
  Agora, chamo atenção para uma decisão técnica fundamental: **os outliers**. Encontramos picos de temperatura de até 278 °C e vibração de 15 mm/s. Um analista desavisado descartaria esses dados. Eu tomei a decisão consciente de **NÃO descartá-los**, porque em engenharia de manutenção, picos térmicos e vibratórios não são ruídos aleatórios: são o próprio sintoma físico da máquina prestes a quebrar!  
  Na correlação de Pearson, confirmamos isso numericamente: **Horas de Operação (+0,38)** e **Vibração (+0,30)** são as variáveis que têm maior associação direta com a falha. Máquinas com falha acumulam média de quase 8.900 horas contra 5.400 horas nas saudáveis. Já a pressão hidráulica teve correlação praticamente nula (-0,02)."*

---

### Slide 5: Modelagem Preditiva Supervisionada - Etapa 3 (3:55 - 5:10)
- **O que destacar no slide:** Por que validação temporal? Tabela comparativa na validação e vitória da Random Forest.
- **O que você fala:**
  > *"Chegando na modelagem supervisionada, adotei uma **estratégia de divisão temporal estrita**, em vez do tradicional embaralhamento aleatório (*train_test_split com shuffle*).  
  Por que? Em séries industriais, se você embaralha amostras no tempo, o modelo aprende com dados do futuro para prever o passado. Para garantir realismo de fábrica, separamos:  
  - 60% inicial (3.000 amostras) para Treino;  
  - 20% intermediário (1.000 amostras) para Validação;  
  - 20% final cronológico (1.000 amostras) mantido como Teste Cego intocado.  
  Testamos o Modelo Dummy (linha de base), Árvore de Decisão, Regressão Logística e Random Forest.  
  Como esperado, o Dummy teve F1 zero. A Árvore de Decisão sofreu com sobreajuste. A Regressão Logística teve bom comportamento, mas a **Random Forest foi a vencedora incontestável**: obteve o maior F1-score (0,352), mantendo 59,4% de precisão e o melhor recall (25%) na partição de validação."*

---

### Slide 6: Resultados no Teste Cego & Reflexão Crítica (5:10 - 6:20)
- **O que destacar no slide:** Matriz de Confusão no teste cego, trade-off de Falso Positivo vs. Falso Negativo e maturidade técnica.
- **O que você fala:**
  > *"Avaliamos então a Random Forest no conjunto de teste cego — dados que o modelo nunca tinha visto.  
  Ele atingiu 82,5% de acurácia geral, 58,4% de precisão e 23,9% de recall na classe de falhas.  
  Aqui trago a reflexão mais importante do projeto, que diferencia um cientista de dados de fábrica de um acadêmico teórico: **o impacto do erro no chão de fábrica**.  
  Olhem para a matriz de confusão:  
  Tivemos **32 Falsos Positivos**: o modelo alertou falha, o mecânico foi até a máquina e viu que ela estava bem. O custo disso é baixo: apenas o tempo de uma inspeção preventiva rápida.  
  Mas tivemos **143 Falsos Negativos**: a máquina quebrou de surpresa e o modelo não avisou! Isso causa parada não programada, quebra ferramentas e atrasa entregas.  
  Portanto, minha conclusão técnica sincera é: com 24% de recall, este modelo **NÃO deve operar de forma 100% autônoma desligando máquinas**. Ele deve funcionar como uma ferramenta consultiva de priorização de rondas para os técnicos."*

---

### Slide 7: Aprendizado Não Supervisionado - K-Means (6:20 - 7:25)
- **O que destacar no slide:** Gráfico de dispersão dos clusters (horas vs. vibração), StandardScaler e o Semáforo de Saúde (Cluster 0 vs. Cluster 1).
- **O que você fala:**
  > *"Na Etapa 4, aplicamos Machine Learning Não Supervisionado com **K-Means**. Retiramos a variável alvo de falha para deixar o algoritmo encontrar os grupos naturais de operação das máquinas.  
  Aplicamos o `StandardScaler` — passo indispensável, já que horas de operação estão na escala de milhares e vibração na escala de 0 a 15. Pelos métodos do Cotovelo e da Silhueta, encontramos **k=3 grupos** muito nítidos:  
  - **Cluster 0 (Máquinas Novas / Revisadas):** Quase metade da base, com média de 3.400 horas e vibração baixa (2,56 mm/s). A taxa de quebra é de apenas **4,5%**!  
  - **Cluster 1 (Desgaste / Operação Severa):** Máquinas com média de 8.780 horas e vibração de 3,57 mm/s. Aqui a taxa de falha salta para **32,0%** — um risco 7 vezes maior!  
  - **Cluster 2 (Anomalias Térmicas):** 25 ocorrências atípicas com temperatura média de 208 °C, indicando aquecimento severo.  
  Isso gera um valor prático imediato: a S&M Industry não precisa esperar o modelo supervisionado ficar perfeito. Ela pode implantar hoje um **Semáforo de Saúde**: se a telemetria da máquina migra para o perfil do Cluster 1, o sistema agenda uma revisão preventiva antes da quebra acontecer."*

---

### Slide 8: Big Data & Escalabilidade com Apache Spark (7:25 - 8:15)
- **O que destacar no slide:** PySpark, leitura estruturada, DataFrame API, tabela comparativa Pandas vs. Spark.
- **O que você fala:**
  > *"Na Etapa 5, demonstramos a escalabilidade do projeto utilizando o **Apache Spark via PySpark**.  
  Reproduzi todo o fluxo de ingestão, tipagem explícita com StructType, deduplicação com `dropDuplicates()` e agregações de falhas por equipamento via DataFrame API. Os números bateram exatamente com os do Pandas, comprovando a consistência dos cálculos.  
  E por que o Spark é vital aqui?  
  Hoje temos 5 máquinas e 5.000 linhas de dados históricos — qualquer notebook com Pandas processa isso em 2 segundos. Porém, no paradigma da Indústria 4.0, uma fábrica real opera com centenas de sensores transmitindo leituras segundo a segundo.  
  Em poucos meses, esse volume ultrapassa gigabytes e terabytes. O Pandas roda apenas na memória RAM de uma única máquina e geraria erro de *Out Of Memory*.  
  O Spark resolve isso com **processamento distribuído em cluster**, particionamento de dados e **Lazy Evaluation** (otimização por DAG), preparando a arquitetura da S&M Industry para crescer sem gargalos."*

---

### Slide 9: Plano de Ação e Recomendações Técnicas (8:15 - 9:00)
- **O que destacar no slide:** Tabela com Curto, Médio e Longo Prazo.
- **O que você fala:**
  > *"Para encerrar o relatório executivo da S&M Industry, traduzi essas descobertas em um plano de ação escalonado em 3 horizontes:  
  1. **No Curto Prazo (Imediato):** Auditar a instrumentação para entender a perda de dados dos 50 nulos, calibrar termopares que registraram picos acima de 270 °C e fazer uma revisão prioritária na máquina M04, que foi a mais vulnerável.  
  2. **No Médio Prazo (Operação & Modelagem):** Implementar a regra de gatilho do Cluster 1 no supervisório da fábrica e aprimorar o modelo Random Forest ajustando o limiar de decisão (*threshold*) de 0.5 para 0.25 e usando `class_weight='balanced'`, elevando o recall para cima de 70%.  
  3. **No Longo Prazo (Escala & IoT):** Integrar o PySpark com Apache Kafka para ingestão em tempo real (*streaming*) e evoluir da classificação binária para um modelo de **RUL (Remaining Useful Life)**, calculando exatamente quantas horas de vida restam antes da próxima quebra."*

---

### Slide 10: Síntese e Conclusão Final (9:00 - 9:30)
- **O que você fala:**
  > *"Concluindo: demonstramos de ponta a ponta a viabilidade de transformar a manutenção da S&M Industry de corretiva para preditiva. Comprovamos que Horas de Uso e Vibração são os maiores indicadores de falha, geramos um semáforo de saúde operacional com o K-Means e preparamos a fundação de Big Data com o PySpark.  
  Agradeço a atenção do professor Daniel Vieira e dos meus colegas, e fico à disposição para as perguntas da banca. Muito obrigado!"*

---

## 3. Banco de Defesa: As 7 Perguntas mais Prováveis da Banca

Esteja preparado para estas perguntas. Respondê-las com segurança garante nota máxima:

| # | Pergunta Provável do Professor | Resposta Matadora |
| :--- | :--- | :--- |
| **1** | *"Por que você não usou a Acurácia como métrica principal para escolher o modelo?"* | *"Porque nossa base tem classes desbalanceadas: 82% normal e 18% falha. Um modelo ingênuo que sempre previsse 'sem falha' atingiria 82% de acurácia acertando zero falhas. Por isso adotamos o **F1-Score**, que equilibra Precisão e Recall na classe minoritária de falhas."* |
| **2** | *"Por que você fez divisão temporal cronológica em vez de usar K-Fold Cross Validation aleatório?"* | *"Porque dados de telemetria industrial constituem uma **série temporal**. Se usássemos `shuffle=True` ou K-Fold tradicional, amostras do futuro seriam usadas para treinar dados do passado, gerando **data leakage temporal** (vazamento de dados). A divisão cronológica 60-20-20 simula exatamente o cenário real de produção."* |
| **3** | *"Você identificou temperaturas de 278 °C. Por que não tratou isso como outlier excluindo essas linhas?"* | *"Em análise de dados industriais, não se pode remover outliers de forma cega. Uma temperatura de 270 °C em um motor ou rolamento não é um erro de digitação: é o **sintoma termodinâmico de sobreaquecimento e travamento mecânico**. Excluir esses pontos seria deletar a própria evidência da falha que o modelo precisa aprender."* |
| **4** | *"Por que você escolheu a Random Forest e não a Árvore de Decisão simples ou Regressão Logística?"* | *"A Random Forest obteve o maior F1-score na validação (0,352 contra 0,208 da Árvore e 0,315 da Regressão). Por ser um método de ensemble (*bagging*), ela constrói múltiplas árvores com subamostras de dados e variáveis, reduzindo a variância e mitigando o sobreajuste severo que vimos na Árvore de Decisão simples."* |
| **5** | *"Por que o StandardScaler foi obrigatório antes do K-Means?"* | *"O K-Means calcula distâncias euclidianas. Nossos atributos possuem grandezas completamente discrepantes: `horas_operacao` varia na casa dos milhares (0 a 10.000 h), enquanto `vibracao_mm_s` varia entre 0 e 15. Se não padronizássemos com média 0 e desvio padrão 1, as horas dominariam 99% da distância euclidiana, anulando a influência da vibração e temperatura."* |
| **6** | *"O teste final teve um Recall de 23,94%. O que isso significa na prática e como resolveria?"* | *"Significa que de cada 100 falhas que realmente aconteceram, o modelo detectou apenas 24 e deixou passar 76 como falsos negativos. Para o chão de fábrica, deixar passar 76% das quebras é arriscado para uma automação total. Para resolver, propus no slide de recomendações: (1) reduzir o limiar de decisão de 0.5 para 0.25 (tornando o modelo mais sensível a alertas) e (2) treinar com `class_weight='balanced'` para penalizar rigorosamente os falsos negativos."* |
| **7** | *"Por que utilizar PySpark se a base de dados tem apenas 5.000 linhas e cabe facilmente no Excel ou Pandas?"* | *"O dataset atual foi um projeto-piloto com 5 máquinas para prova de conceito. Na vida real, a S&M Industry monitora dezenas ou centenas de equipamentos gerando telemetria em alta frequência (Hertz ou segundos). Em poucos dias teríamos milhões de linhas, causando erro de Out-Of-Memory no Pandas. O código em PySpark foi construído para provar que a solução está arquitetada para escalar horizontalmente para qualquer volume sem refazer o pipeline."* |

---

## 4. Dicas de Gravação do Vídeo / Apresentação em Aula

1. **Tempo de Fala:** Mantenha o vídeo entre **7 e 9 minutos**. Não se apresse nos slides 4, 6 e 7 (eles contêm os argumentos de maior peso técnico).
2. **Postura e Tom:** Fale como um consultor ou engenheiro de dados apresentando para a liderança. Use termos precisos: *"telemetria"*, *"desbalanceamento de classes"*, *"trade-off de falsos negativos"*, *"semáforo operacional"*, *"processamento distribuído"*.
3. **Ponteiro e Gestos no Vídeo:** Se for gravar a tela (com OBS Studio, PowerPoint Gravar Apresentação ou Teams/Zoom), use o cursor do mouse ou o apontador laser do PowerPoint para destacar os números-chave na tabela e nos gráficos.
4. **Slide 1 - Ajuste do Nome:** No slide 1 do PowerPoint original, verifique se o nome do aluno está como o seu ou de sua preferência antes de iniciar a gravação.
