# DynamoDB Local Stack

Stack opcional para desenvolvimento local com DynamoDB Local e AWS CLI.

Ela fica desabilitada por padrão porque está fora do `docker-compose.yml` principal.

## Serviços

| Serviço | Uso | URL/porta |
| --- | --- | --- |
| DynamoDB Local | Banco DynamoDB local | `http://localhost:8000` |
| AWS CLI | Toolbox para comandos DynamoDB | `docker compose exec aws-cli ...` |

## Como ativar

Pelo Dockge, use o scan de stacks e suba a stack `dynamodb`.

Via terminal:

```bash
cd stacks/dynamodb
cp .env.example .env
docker compose --env-file .env up -d
```

No Windows PowerShell:

```powershell
Set-Location stacks/dynamodb
Copy-Item .env.example .env
docker compose --env-file .env up -d
```

## Acesso

Endpoint local:

```text
http://localhost:8000
```

Listar tabelas pelo AWS CLI da stack:

```bash
docker compose --env-file .env exec aws-cli aws dynamodb list-tables --endpoint-url http://dynamodb-local:8000
```

As credenciais no `.env.example` são dummy e servem apenas para o DynamoDB Local.

## Como desativar

```bash
docker compose --env-file .env down
```

Para remover os dados persistidos:

```bash
docker compose --env-file .env down -v
```
