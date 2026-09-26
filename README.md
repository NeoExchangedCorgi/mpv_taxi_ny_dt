# MVP: Pipeline de Dados na Nuvem – NYC Taxi (Databricks)

Pipeline de dados completo utilizando a **Arquitetura Medalhão** (Bronze → Silver → Gold) sobre o dataset público `samples.nyctaxi.trips` no Databricks Free Edition.

---

## 1. Contexto de Negócios e Perguntas (Etapa 2 e 4.1)

### Problema / Contexto
O objetivo deste trabalho é construir um pipeline de dados na nuvem para analisar o padrão de uso e precificação das corridas de táxi em Nova York.  
A partir dos dados disponíveis no dataset `samples.nyctaxi.trips`, buscamos identificar os principais fatores que influenciam o valor da corrida, os horários e locais de maior demanda, e possíveis problemas de qualidade nos dados.  

Os insights gerados podem apoiar decisões de otimização de frota, precificação dinâmica ou planejamento urbano.

### Fonte dos Dados
- **Dataset:** `samples.nyctaxi.trips` (Databricks Public Datasets)
- **Licença:** Uso livre para fins educacionais e de aprendizado
- **Conteúdo:** Registros de corridas de táxi amarelo (Yellow Cab) de Nova York, contendo data/hora de embarque e desembarque, distância, valor da corrida e CEPs de origem/destino.
- **Volume:** 21.932 registros | 6 colunas originais

### Perguntas de Negócio
1. Qual é a distribuição do valor da corrida e da distância? Existem outliers significativos?
2. Existe correlação clara entre distância percorrida e valor da corrida? Qual a força dessa relação?
3. Quais são os horários do dia e dias da semana com maior volume de corridas e maior valor médio?
4. Quais são os CEPs de origem e destino mais frequentes? Existem rotas especialmente rentáveis?
5. Qual a duração média das corridas e como ela se relaciona com o valor cobrado?

---

## 2. Carga dos Dados (Etapa 4.2)

Os dados já estavam disponíveis no catálogo `samples` do Databricks.  
Foi realizada a carga para a camada Bronze adicionando metadados de rastreabilidade (`ingestion_timestamp` e `source_table`).

**Evidências:**

![Estrutura da tabela fonte](# MVP: Pipeline de Dados na Nuvem – NYC Taxi (Databricks)

Pipeline de dados completo utilizando a **Arquitetura Medalhão** (Bronze → Silver → Gold) sobre o dataset público `samples.nyctaxi.trips` no Databricks Free Edition.

---

## 1. Contexto de Negócios e Perguntas (Etapa 2 e 4.1)

### Problema / Contexto
O objetivo deste trabalho é construir um pipeline de dados na nuvem para analisar o padrão de uso e precificação das corridas de táxi em Nova York.  
A partir dos dados disponíveis no dataset `samples.nyctaxi.trips`, buscamos identificar os principais fatores que influenciam o valor da corrida, os horários e locais de maior demanda, e possíveis problemas de qualidade nos dados.  

Os insights gerados podem apoiar decisões de otimização de frota, precificação dinâmica ou planejamento urbano.

### Fonte dos Dados
- **Dataset:** `samples.nyctaxi.trips` (Databricks Public Datasets)
- **Licença:** Uso livre para fins educacionais e de aprendizado
- **Conteúdo:** Registros de corridas de táxi amarelo (Yellow Cab) de Nova York, contendo data/hora de embarque e desembarque, distância, valor da corrida e CEPs de origem/destino.
- **Volume:** 21.932 registros | 6 colunas originais

### Perguntas de Negócio
1. Qual é a distribuição do valor da corrida e da distância? Existem outliers significativos?
2. Existe correlação clara entre distância percorrida e valor da corrida? Qual a força dessa relação?
3. Quais são os horários do dia e dias da semana com maior volume de corridas e maior valor médio?
4. Quais são os CEPs de origem e destino mais frequentes? Existem rotas especialmente rentáveis?
5. Qual a duração média das corridas e como ela se relaciona com o valor cobrado?

---

## 2. Carga dos Dados (Etapa 4.2)

Os dados já estavam disponíveis no catálogo `samples` do Databricks.  
Foi realizada a carga para a camada Bronze adicionando metadados de rastreabilidade (`ingestion_timestamp` e `source_table`).

**Evidências:**

![Estrutura da tabela fonte](ds_nt_taxi/o1_explorando_o_ds_estrutura_da_tabela.png)

![Contagem da tabela fonte](images/02_fonte_count.png)

![Criação e verificação da Bronze](images/03_bronze_describe.png)

![Amostra da Bronze com metadados](images/04_bronze_sample.png)

![Contagem da tabela fonte](images/02_fonte_count.png)

![Criação e verificação da Bronze](images/03_bronze_describe.png)

![Amostra da Bronze com metadados](images/04_bronze_sample.png)

---






































































# mpv_taxi_ny_dt
Estudo de banco de **dados** de taxis em Nova Iorque

[Link do dataset](https://docs.databricks.com/aws/en/discover/databricks-datasets#nyctaxi)


## Contexto de Negócios e Perguntas (Etapa 2 e 4.1)

### Problema / Contexto
O objetivo deste trabalho é construir um pipeline de dados na nuvem (usando a arquitetura Medalhão) para analisar o padrão de uso e precificação das corridas de táxi em Nova York.

A partir dos dados de corridas disponíveis no dataset `samples.nyctaxi.trips`, identifico os principais fatores que influenciam o valor da corrida, os horários e locais de maior demanda, e possíveis inconsistências de qualidade nos dados.

Os insights gerados podem apoiar decisões de otimização de frota, precificação dinâmica ou planejamento urbano.

### Fonte dos Dados
- Dataset: `samples.nyctaxi.trips` (Databricks Public Datasets); tabela com registros de corridas de táxi de Nova York contendo data/hora de embarque e desembarque, distância, valor da corrida e CEPs de origem e destino.

### Perguntas de Negócio
1. Qual é a distribuição do valor da corrida e da distância? Existem outliers, pontos fora da curva, significativos?
2. Existe correlação clara entre distância percorrida e valor da corrida? Qual a força dessa relação?
3. Quais são os horários do dia e dias da semana com maior volume de corridas e maior valor médio?
4. Qual a duração média das corridas e como ela se relaciona com o valor cobrado?
5. Quais são os CEPs de origem e destino mais frequentes? Existem rotas especialmente rentáveis?

### Legenda: Variáveis e Tabelas do Pipeline

Esta seção descreve o significado completo de cada coluna e tabela utilizada no notebook, do dado bruto às agregações finais.

#### Tabela de origem: `samples.nyctaxi.trips`
Dataset público de corridas de táxi amarelo (Yellow Cab) da cidade de Nova York, disponibilizado pela Databricks.

| Coluna | Tipo | Significado |
| --- | --- | --- |
| `tpep_pickup_datetime` | timestamp | Momento exato em que o passageiro entrou no táxi (início da corrida). *TPEP* significa *Taxi and Limousine Commission Passenger Enhancement Program*, o sistema de registradores eletrônicos instalados nos veículos. |
| `tpep_dropoff_datetime` | timestamp | Momento exato em que o passageiro saiu do táxi (fim da corrida). |
| `trip_distance` | double | Distância percorrida durante a corrida, medida em milhas, registrada pelo taxímetro do veículo. |
| `fare_amount` | double | Valor da tarifa cobrada do passageiro pelo taxímetro, em dólares americanos. Não inclui gorjetas, pedágios ou adicionais — apenas a tarifa base calculada por distância e tempo. |
| `pickup_zip` | int | Código postal (ZIP code) da zona onde o passageiro foi embarcado. Corresponde a áreas de Manhattan e arredores. |
| `dropoff_zip` | int | Código postal da zona onde o passageiro foi desembarcado. |

#### Camada Bronze: `workspace.bronze.nyctaxi_trips`
Cópia bruta dos dados de origem, projetada com metadados de rastreabilidade. Nenhuma transformação de valor é aplicada; o objetivo é preservar o dado exatamente como chegou.

| Coluna | Tipo | Significado |
| --- | --- | --- |
| `tpep_pickup_datetime` | timestamp | Momento exato do início da corrida. |
| `tpep_dropoff_datetime` | timestamp | Momento exato do fim da corrida. |
| `trip_distance` | double | Distância percorrida em milhas. |
| `fare_amount` | double | Tarifa base em dólares. |
| `pickup_zip` | int | CEP do embarque. |
| `dropoff_zip` | int | CEP do desembarque. |
| `ingestion_timestamp` | timestamp | Carimbo de data/hora gerado automaticamente no momento em que o dado foi copiado para a Bronze. Permite saber quando cada carga ocorreu, essencial para auditoria e reprodução. |
| `source_table` | string | Nome completo da tabela de origem (`samples.nyctaxi.trips`). Permite rastrear de onde cada registro veio, útil quando múltiplas fontes alimentam a Bronze. |

#### Camada Silver: `workspace.silver.nyctaxi_trips`
Dado limpo, filtrado e enriquecido. Registros com distância inválida (≤ 0), tarifa inválida (≤ 0) ou com dropoff anterior ao pickup são removidos. Novas colunas derivadas são calculadas para suportar as análises de negócio.

| Coluna | Tipo | Significado |
| --- | --- | --- |
| `tpep_pickup_datetime` | timestamp | Momento exato do início da corrida — agora garantidamente válido. |
| `tpep_dropoff_datetime` | timestamp | Momento exato do fim da corrida — agora garantidamente posterior ao pickup. |
| `trip_distance` | double | Distância em milhas — agora garantidamente maior que zero. |
| `fare_amount` | double | Tarifa em dólares — agora garantidamente maior que zero. |
| `pickup_zip` | int | CEP do embarque, preservado da Bronze. |
| `dropoff_zip` | int | CEP do desembarque, preservado da Bronze. |
| `duration_minutes` | decimal(24,2) | **Derivada:** duração total da corrida em minutos, calculada como a diferença entre `tpep_dropoff_datetime` e `tpep_pickup_datetime` convertida para minutos e arredondada a duas casas decimais. |
| `pickup_hour` | int | **Derivada:** hora do dia (0 a 23) extraída de `tpep_pickup_datetime`. Permite agrupar corridas por faixa horária e identificar picos de demanda. |
| `pickup_dayofweek` | int | **Derivada:** dia da semana (1 = Domingo, 7 = Sábado) extraído de `tpep_pickup_datetime`. Permite comparar volume e receita entre dias da semana. |
| `ingestion_timestamp` | timestamp | Metadado de rastreabilidade, preservado da Bronze. |
| `source_table` | string | Metadado de origem, preservado da Bronze. |

#### Camada Gold: tabelas agregadas
As tabelas Gold contêm dados prontos para análise e visualização, pré-agregados em diferentes granularidades.

##### `workspace.gold.trips_by_hour`
Agrupa todas as corridas por hora do dia (0 a 23). Cada linha resume o comportamento da frota em uma determinada hora.

| Coluna | Tipo | Significado |
| --- | --- | --- |
| `pickup_hour` | int | Hora do dia (0 a 23) em que as corridas foram iniciadas. |
| `total_trips` | long | Número total de corridas iniciadas naquela hora. |
| `avg_fare` | double | Tarifa média (em dólares) das corridas daquela hora. |
| `avg_distance` | double | Distância média (em milhas) das corridas daquela hora. |
| `avg_duration` | decimal(25,2) | Duração média (em minutos) das corridas daquela hora. |
| `total_revenue` | double | Receita total (em dólares) somada de todas as corridas daquela hora. |

##### `workspace.gold.trips_by_dayofweek`
Agrupa todas as corridas por dia da semana (1 a 7). Inclui o nome do dia em português para facilitar a leitura.

| Coluna | Tipo | Significado |
| --- | --- | --- |
| `pickup_dayofweek` | int | Número do dia da semana (1 = Domingo, 7 = Sábado). |
| `day_name` | string | Nome do dia da semana (já em português), derivado por uma expressão `CASE`. |
| `total_trips` | long | Número total de corridas iniciadas naquele dia da semana. |
| `avg_fare` | double | Tarifa média (em dólares) das corridas daquele dia. |
| `avg_distance` | double | Distância média (em milhas) das corridas daquele dia. |
| `total_revenue` | double | Receita total (em dólares) somada de todas as corridas daquele dia. |

##### `workspace.gold.top_routes`
Agrupa as corridas por par de CEP (origem → destino) e mantém apenas as 50 rotas mais frequentes.

| Coluna | Tipo | Significado |
| --- | --- | --- |
| `pickup_zip` | int | CEP onde o passageiro foi embarcado. |
| `dropoff_zip` | int | CEP onde o passageiro foi desembarcado. |
| `total_trips` | long | Número total de corridas que percorreram essa rota (par de CEPs). |
| `avg_fare` | double | Tarifa média (em dólares) dessa rota. |
| `avg_distance` | double | Distância média (em milhas) dessa rota. |
| `total_revenue` | double | Receita total (em dólares) acumulada nessa rota. |

## Fluxo de dependências


`samples.nyctaxi.trips` (origem) >>

`workspace.bronze.nyctaxi_trips` (cópia bruta + metadados) >>

`workspace.silver.nyctaxi_trips` (limpeza + colunas derivadas) >>

. `workspace.gold.trips_by_hour`

. `workspace.gold.trips_by_dayofweek`

. `workspace.gold.top_routes`

Cada camada consome exclusivamente a camada imediatamente anterior, seguindo o princípio do Medalhão: a Bronze nunca é alterada após a carga; a Silver filra e enriquece a Bronze; a Gold agrega a Silver.
