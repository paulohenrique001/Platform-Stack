# MongoDB Stack

Stack opcional para desenvolvimento local com MongoDB. O `mongosh` é usado dentro do próprio container.

Ela fica desabilitada por padrão porque está fora do `docker-compose.yml` principal.

## Serviços

| Serviço | Uso | URL/porta |
| --- | --- | --- |
| MongoDB | Banco de documentos local | `localhost:27017` |

## Como ativar

Pelo Dockge, use o scan de stacks e suba a stack `mongodb`.

Via terminal:

```bash
cd stacks/mongodb
cp .env.example .env
docker compose --env-file .env up -d
```

No Windows PowerShell:

```powershell
Set-Location stacks/mongodb
Copy-Item .env.example .env
docker compose --env-file .env up -d
```

## Acesso

String local:

```text
mongodb://root:change_me_mongodb_password@localhost:27017/app?authSource=admin
```

Para usar o `mongosh` dentro do próprio MongoDB:

```bash
docker compose --env-file .env exec mongodb mongosh -u root -p change_me_mongodb_password --authenticationDatabase admin
```

Antes de usar em um projeto compartilhado, ajuste a senha no `.env` local.

## Como desativar

```bash
docker compose --env-file .env down
```

Para remover os dados persistidos:

```bash
docker compose --env-file .env down -v
```
