# PostgreSQL Stack

Stack opcional para desenvolvimento local com PostgreSQL e pgAdmin.

Ela fica desabilitada por padrão porque está fora do `docker-compose.yml` principal.

## Serviços

| Serviço | Uso | URL/porta |
| --- | --- | --- |
| PostgreSQL | Banco relacional local | `localhost:5432` |
| pgAdmin | Gerenciador web do banco | `http://localhost:5050` |

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

No pgAdmin, entre com:

```text
Email: admin@example.local
Senha: change_me_pgadmin_password
```

Ao registrar o servidor PostgreSQL no pgAdmin, use:

```text
Host: postgresql
Porta: 5432
Usuário: app
Senha: change_me_postgresql_password
Database: app
```

Antes de usar em um projeto compartilhado, ajuste as senhas no `.env` local.

## Como desativar

```bash
docker compose --env-file .env down
```

Para remover os dados persistidos:

```bash
docker compose --env-file .env down -v
```
