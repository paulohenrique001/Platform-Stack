# Elasticsearch Stack

Stack opcional para desenvolvimento local com Elasticsearch single-node e Kibana.

Ela fica desabilitada por padrão porque está fora do `docker-compose.yml` principal.

## Serviços

| Serviço | Uso | URL/porta |
| --- | --- | --- |
| Elasticsearch | API HTTP e engine de busca | `http://localhost:9200` |
| Elasticsearch transport | Porta de transporte | `localhost:9300` |
| Kibana | Interface web | `http://localhost:5601` |

## Como ativar

Pelo Dockge, use o scan de stacks e suba a stack `elasticsearch`.

Via terminal:

```bash
cd stacks/elasticsearch
cp .env.example .env
docker compose --env-file .env up -d
```

No Windows PowerShell:

```powershell
Set-Location stacks/elasticsearch
Copy-Item .env.example .env
docker compose --env-file .env up -d
```

## Acesso

Elasticsearch roda sem autenticação para desenvolvimento local:

```text
Elasticsearch: http://localhost:9200
Kibana: http://localhost:5601
```

O heap padrão fica em `-Xms512m -Xmx512m`. Ajuste `ES_JAVA_OPTS` no `.env` local se precisar de mais memória.

## Como desativar

```bash
docker compose --env-file .env down
```

Para remover os dados persistidos:

```bash
docker compose --env-file .env down -v
```
