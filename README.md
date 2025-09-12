![Capa do projeto](images/capa_cyclistic.png)

# 🚴‍♂️ Cyclistic Bike-Share | Estudo de Comportamento de Usuários


## 📌 Visão Geral

Este projeto é baseado em um estudo de caso realista no qual atuo como **analista de dados júnior** da equipe de marketing da **Cyclistic**, um programa de compartilhamento de bicicletas com sede em Chicago. Desde seu lançamento em 2016, a Cyclistic cresceu para uma frota de mais de **5.800 bicicletas** distribuídas em **mais de 600 estações**, oferecendo inclusive modelos adaptados, como triciclos de mão e bicicletas de carga, promovendo acessibilidade e inclusão.

A empresa oferece diferentes planos de uso: passe único, passe diário e assinatura anual. Atualmente, os **usuários casuais** (que usam passes pontuais) e os **membros anuais** apresentam comportamentos distintos, e entender essas diferenças é essencial para o próximo passo estratégico da empresa.

A diretora de marketing, **Lily Moreno**, acredita que o sucesso futuro da Cyclistic depende de **converter ciclistas casuais em membros anuais**, já que os membros geram maior receita recorrente. Para isso, é necessário identificar padrões de uso entre os diferentes perfis e fornecer à equipe executiva **recomendações embasadas em dados e visualizações profissionais**.

O objetivo deste projeto é analisar os dados históricos de viagens da Cyclistic para gerar **insights práticos que apoiem decisões estratégicas de marketing**, usando as etapas do processo analítico: *Perguntar, Preparar, Processar, Analisar, Compartilhar e Agir*.


## ⚙️ Abordagem / Etapas

### 1. Perguntar

Três perguntas fundamentais orientarão o desenvolvimento do novo programa de marketing da Cyclistic:

> 1. *Como os membros anuais e os ciclistas casuais utilizam as bicicletas da Cyclistic de forma diferente?*
> 2. *Por que os ciclistas casuais considerariam adquirir uma assinatura anual da Cyclistic?*
> 3. *Como a Cyclistic pode usar mídias digitais para incentivar ciclistas casuais a se tornarem membros anuais?*

Essas perguntas são o ponto de partida da análise e irão guiar todo o processo investigativo nas etapas seguintes.

#### Hipóteses iniciais

Antes de iniciar a análise, elaborei algumas hipóteses que refletem possíveis padrões de comportamento entre usuários casuais e membros.

> 1. *Usuários casuais utilizam mais as bicicletas aos finais de semana, especialmente sexta, sábado e domingo; enquanto membros usam de forma mais distribuída ao longo da semana*.
> 2. *O uso das bicicletas é maior durante as estações mais quentes, como o verão (junho a setembro) e o outono (setembro a novembro)*.
> 3. *Usuários casuais tendem a utilizar as bicicletas próximas a áreas de lazer, como parques, enquanto membros utilizam para deslocamentos urbanos mais distribuídos pela cidade*.
> 4. *Feriados aumentam o uso das bicicletas por usuários casuais, indicando um comportamento mais voltado ao lazer e ao turismo*.


### 2. Preparar

Nesta etapa, defini os recursos e ferramentas necessários para conduzir a análise, além de identificar a origem e a licença dos dados utilizados.

Os dados históricos de viagens foram obtidos por meio do portal oficial da Divvy, disponível em:  
🔗 <a href="https://divvy-tripdata.s3.amazonaws.com/index.html" target="_blank">divvy-tripdata</a>

O uso dos dados é permitido conforme os termos da licença disponibilizada pela Divvy:  
🔗 <a href="https://divvybikes.com/data-license-agreement" target="_blank">Data License Agreement</a>


**Ferramentas:** <br>
- Limpeza e manipulação de dados — Python (Pandas)  
- Visualização de dados — Matplotlib, Seaborn  
- Ambiente de desenvolvimento — Jupyter Notebook


### 3. Processar

Para esta análise, utilizei as bases de dados referentes ao ano de 2024. Dividi o processamento nas seguintes etapas:

1) [Combinação de Dados (Data Combination)](notebooks/01-Data-Combination.ipynb)
2) [Exploração de Dados (Data Exploration)](notebooks/02-Data-Exploration.ipynb)
3) [Limpeza de Dados (Data Cleaning)](notebooks/03-Data-Cleaning.ipynb)
4) [Análise de Dados (Data Analysis)](notebooks/04-Data-Analysis.ipynb)

#### Combinação de Dados
As tabelas de janeiro de 2024 a dezembro de 2024 foram empilhadas em uma única tabela, totalizando 5.860.568 linhas.

#### Exploração de Dados

Nesta etapa, o foco foi entender melhor como os dados estão distribuídos e identificar possíveis padrões. Foram analisados os valores únicos, presença de nulos, outliers e a distribuição geral das variáveis.

| **Nº** | **Coluna**         | **Descrição**                                 |
|--------|--------------------|-----------------------------------------------|
| 1      | ride_id            | Identificador único de cada viagem            |
| 2      | rideable_type      | Tipo de bicicleta utilizada na viagem         |
| 3      | started_at         | Data e hora de início da viagem               |
| 4      | ended_at           | Data e hora de término da viagem              |
| 5      | start_station_name | Nome da estação onde a viagem foi iniciada    |
| 6      | start_station_id   | Identificador da estação de início da viagem  |
| 7      | end_station_name   | Nome da estação onde a viagem foi finalizada  |
| 8      | end_station_id     | Identificador da estação de término da viagem |
| 9      | start_lat          | Latitude do ponto de partida da viagem        |
| 10     | start_lng          | Longitude do ponto de partida da viagem       |
| 11     | end_lat            | Latitude do ponto de chegada da viagem        |
| 12     | end_lng            | Longitude do ponto de chegada da viagem       |
| 13     | member_casual      | Categoria do usuário                          |

Essa análise inicial ajudou a ter uma visão mais clara da base e direcionar os próximos passos do projeto.

#### Limpeza de Dados

Nesta etapa, fiz alguns ajustes importantes para preparar os dados para a análise:

- Removi registros duplicados na coluna `ride_id`
- Excluí linhas com valores nulos
- Converti as colunas `started_at` e `ended_at` para o formato `datetime` e arredondei os valores para segundos (`HH:MM:SS`)
- Eliminei linhas onde o horário de início era maior ou igual ao horário de término
- Criei a coluna `ride_length` com a duração da viagem (término - início)
- Criei a coluna `day_of_week` para identificar o dia da semana da viagem (1 = domingo, 7 = sábado)
- Criei a coluna `month` para identificar o mês da viagem
- Criei a coluna `is_holiday` para verificar se o dia da viagem era feriado ou não
- Criei a coluna `seasons` para identificar a estação do ano correspondente a cada mês

Após esses passos, a base final ficou com **4.207.936 linhas**, ou seja, **removi 1.652.632 linhas** com dados inválidos ou incompletos para análise.


### 4. Analisar

#### Análise de Dados

Nesta etapa, o objetivo é **testar as hipóteses** e verificar, por meio de análises estatísticas e gráficas, se os padrões de comportamento entre usuários casuais e membros anuais realmente se confirmam nos dados.

#### Teste de Hipóteses

Para cada hipótese, foram aplicadas análises exploratórias e testes estatísticos a fim de verificar se há **evidências significativas** que sustentem ou refutem os padrões esperados.  

> 1. *Usuários casuais utilizam mais as bicicletas aos finais de semana, especialmente sexta, sábado e domingo; enquanto membros usam de forma mais distribuída ao longo da semana*.✅

![Gráfico](images/hipotese_1.png)

- Usuários casuais apresentam maior consumo entre quinta-feira e domingo, com menor utilização de segunda a quarta-feira. Já os membros mantêm um padrão mais equilibrado ao longo da semana, mas com redução nas sextas e sábados.

> 2. *O uso das bicicletas é maior durante as estações mais quentes, como o verão (junho a setembro) e o outono (setembro a novembro)*.✅

![Gráfico](images/hipotese_2.png)

- Tanto usuários casuais quanto membros utilizam mais as bicicletas nas estações mais quentes, apresentando uma queda significativa no inverno.

> 3. *Usuários casuais tendem a utilizar as bicicletas próximas a áreas de lazer, como parques, enquanto membros utilizam para deslocamentos urbanos mais distribuídos pela cidade*.✅

<p align="center">
  <img src="images/estacoes_de_inicio.png" width="50%">
  <img src="images/lazer_e_turismo.png" width="47%">
</p>

- Os usuários casuais concentram suas viagens em pontos turísticos e áreas de lazer, como parques e regiões centrais da cidade. Ao mesmo tempo, é possível observar que as viagens também estão distribuídas por outras regiões de Chicago, indicando que o uso não se limita apenas aos locais de maior interesse turístico.

> 4. *Feriados aumentam o uso das bicicletas por usuários casuais, indicando um comportamento mais voltado ao lazer e ao turismo*.✅

![Capa do projeto](images/hipotese_4.png)

- A análise descritiva mostrou que, em 11 dos 19 feriados de 2024, os usuários casuais apresentaram **mais viagens** do que nos mesmos dias da semana sem feriado, enquanto em 8 feriados houve **menos viagens**. Esses resultados indicam que, de forma geral, os feriados tendem a estimular o uso das bicicletas por usuários casuais.


### 5. Compartilhar

O dashboard a seguir foi desenvolvido no Power BI para oferecer uma visão geral do comportamento de **usuários casuais e membros**. A visualização fornece **insights estratégicos** que apoiam a **tomada de decisão do time de marketing da Cyclistic**.

![Dashboard](images/dashboard.png)

- **Participação por grupo:** Membros representam 63,8% das viagens (2.686.491), enquanto casuais somam 36,2% (1.521.445). A média mensal é de 223.874 viagens para membros e 126.787 para casuais.

- **Sazonalidade:** O pico de uso ocorre no verão (junho a setembro), com destaque para julho e agosto. No inverno há queda acentuada, principalmente entre casuais, que realizam menos de 30 mil viagens em dezembro, enquanto membros mantêm maior constância.

- **Padrão semanal:** Membros usam mais em dias úteis, com pico na terça-feira (446.873 viagens). Casuais se destacam em sextas e sábados, reforçando o perfil de lazer.

- **Tipo de bicicleta:** Ambos os grupos preferem as bicicletas clássicas, mas a proporção de uso de patinete elétrico é maior entre usuários casuais.

- **Estações de início:** A estação Streeter Dr & Grand Ave lidera com 62.274 viagens, mais que o dobro da 10ª colocada, refletindo concentração em áreas turísticas/centrais.

- **Duração média das viagens:** Casuais permanecem mais tempo (24,05 min) que membros (12,47 min), reforçando o uso recreativo.


### 6. Agir

Com base nos insights obtidos na etapa de análise e na visualização do dashboard, foram definidas recomendações estratégicas que visam aumentar o engajamento, fidelizar usuários e otimizar o uso do sistema de compartilhamento de bicicletas da Cyclistic.

#### Recomendações

1 - Criar programas de pontos ou recompensas para incentivar o uso recorrente por membros, especialmente fora de horários e dias de pico. Além disso, comunicar benefícios exclusivos, como acesso antecipado a novos modais ou eventos especiais.

2 - Desenvolver campanhas promocionais voltadas para usuários casuais durante o verão e a primavera, quando há maior volume de viagens. Oferecer descontos ou benefícios extras para quem migrar para um plano após atingir um número mínimo de viagens em fins de semana ou períodos de alta demanda.

3 - Direcionar campanhas específicas para casuais que utilizam mais bicicletas e patinetes elétricos, destacando vantagens exclusivas de membros, como tarifas reduzidas ou reservas prioritárias. Utilizar canais digitais personalizados (e-mail, push notification) e redes sociais para gerar engajamento e conversão.

4 - Promover eventos presenciais próximos às estações mais movimentadas, com promotores oferecendo trials de planos de membro, brindes e QR codes para cadastro rápido, estimulando a adesão imediata.


## 💡 Conclusão

Em resumo, este estudo de caso oferece uma visão clara sobre os diferentes perfis e comportamentos dos usuários da Cyclistic. Ao compreender essas particularidades, a empresa pode desenvolver estratégias mais eficazes e direcionadas, fortalecendo seu programa de bicicletas compartilhadas e ampliando o engajamento dos ciclistas casuais em potenciais membros.
