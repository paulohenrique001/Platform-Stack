# PostgreSQL Stack

Stack opcional para desenvolvimento local com PostgreSQL.

Ela fica desabilitada por padrão porque está fora do `docker-compose.yml` principal.

## Serviços

| Serviço | Uso | URL/porta |
| --- | --- | --- |
| PostgreSQL | Banco relacional local | `localhost:5432` |

## Como ativar

Pelo Dockge, use o scan de stacks e suba a stack `postgresql`.

Via terminal:

```bash
cd stacks/postgresql
cp .env.example .env
docker compose --env-file .env up -d
```

No Windows PowerShell:

```powershell
Set-Location stacks/postgresql
Copy-Item .env.example .env
docker compose --env-file .env up -d
```

## Acesso

Use estes dados em clientes locais:

```text
Host: localhost
Porta local: 5432
Usuario: app
Senha: postgres
Database: app
```

Para usar o CLI dentro do container:

```bash
docker compose --env-file .env exec postgresql psql -U app -d app
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
