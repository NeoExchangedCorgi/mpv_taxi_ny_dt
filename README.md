# mpv_taxi_ny_dt
Estudo de banco de **dados** de taxis em Nova Iorque

## Contexto de Negócios e Perguntas (Etapa 2 e 4.1)

### Problema / Contexto
O objetivo deste trabalho é construir um pipeline de dados na nuvem (usando a arquitetura Medalhão) para analisar o padrão de uso e precificação das corridas de táxi em Nova York.  
A partir dos dados de corridas disponíveis no dataset `samples.nyctaxi.trips`, buscamos identificar os principais fatores que influenciam o valor da corrida, os horários e locais de maior demanda, e possíveis inconsistências de qualidade nos dados.  
Os insights gerados podem apoiar decisões de otimização de frota, precificação dinâmica ou planejamento urbano.

### Fonte dos Dados
- Dataset: `samples.nyctaxi.trips` (Databricks Public Datasets); tabela com registros de corridas de táxi de Nova York contendo data/hora de embarque e desembarque, distância, valor da corrida e CEPs de origem e destino.

### Perguntas de Negócio
1. Qual é a distribuição do valor da corrida e da distância? Existem outliers, pontos fora da curva, significativos?
2. Existe correlação clara entre distância percorrida e valor da corrida? Qual a força dessa relação?
3. Quais são os horários do dia e dias da semana com maior volume de corridas e maior valor médio?
4. Qual a duração média das corridas e como ela se relaciona com o valor cobrado?
5. Quais são os CEPs de origem e destino mais frequentes? Existem rotas especialmente rentáveis?