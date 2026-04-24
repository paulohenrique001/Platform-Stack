# MariaDB Stack

Stack opcional para desenvolvimento local com MariaDB.

Ela fica desabilitada por padrão porque está fora do `docker-compose.yml` principal. O desenvolvedor ativa somente quando precisar de banco relacional no ambiente local.

## Serviços

| Serviço | Uso | URL/porta |
| --- | --- | --- |
| MariaDB | Banco relacional local | `localhost:3306` |

## Como ativar

Pelo Dockge, use o scan de stacks e suba a stack `mariadb`.

Via terminal:

```bash
cd stacks/mariadb
cp .env.example .env
docker compose --env-file .env up -d
```

No Windows PowerShell:

```powershell
Set-Location stacks/mariadb
Copy-Item .env.example .env
docker compose --env-file .env up -d
```

## Acesso

Use estes dados em clientes locais:

```text
Host: localhost
Porta local: 3306
Usuario: app
Senha: app
Database: app
```

Para usar o CLI dentro do container:

```bash
docker compose --env-file .env exec mariadb mariadb -uapp -papp app
```

Também é possível conectar como `root` usando `root`.

Antes de usar em um projeto compartilhado, ajuste as senhas no `.env` local.

## Como desativar

```bash
docker compose --env-file .env down
```

Para remover os dados persistidos:

```bash
docker compose --env-file .env down -v
```
