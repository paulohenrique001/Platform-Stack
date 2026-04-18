# Networking

Este template usa portas locais diretas. Não há proxy reverso nem resolução automática por domínio.

## Portas padrão

Stack principal:

- Dockge: `5001`
- Dozzle: `8080`
- Uptime Kuma: `3001`

Stacks opcionais, usadas somente quando o desenvolvedor ativar a stack correspondente:

- Redis: `6379`
- Redis Insight: `5540`
- Neo4j Browser: `7474`
- Neo4j Bolt: `7687`
- MariaDB: `3306`
- phpMyAdmin: `8081`
- MongoDB: `27017`
- DynamoDB Local: `8000`
- PostgreSQL: `5432`
- pgAdmin: `5050`
- Elasticsearch HTTP: `9200`
- Elasticsearch transport: `9300`
- Kibana: `5601`

## Outros projetos

Exponha as portas no Compose do próprio projeto:

```yaml
services:
  app:
    image: nginx:alpine
    ports:
      - "8088:80"
```

Depois acesse `http://localhost:8088`.

## Redes Docker

A stack principal usa a rede `dockge_platform_network` para comunicação interna entre os serviços.

Cada stack opcional cria a própria rede:

- `dockge_redis_network`
- `dockge_neo4j_network`
- `dockge_database_network`
- `dockge_mongodb_network`
- `dockge_dynamodb_network`
- `dockge_postgresql_network`
- `dockge_elasticsearch_network`

Outros projetos podem usar as portas locais ou entrar na rede da stack correspondente quando precisarem conversar com o serviço por nome de container.
