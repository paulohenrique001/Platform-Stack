# MariaDB Stack

Stack opcional para desenvolvimento local com MariaDB e phpMyAdmin.

Ela fica desabilitada por padrão porque está fora do `docker-compose.yml` principal. O desenvolvedor ativa somente quando precisar de banco relacional no ambiente local.

## Serviços

| Serviço | Uso | URL/porta |
| --- | --- | --- |
| MariaDB | Banco relacional local | `localhost:3306` |
| phpMyAdmin | Gerenciador web do banco | `http://localhost:8081` |

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

No phpMyAdmin, use:

```text
Servidor: mariadb
Usuário: app
Senha: change_me_app_password
```

Também é possível entrar como `root` usando `change_me_root_password`.

Antes de usar em um projeto compartilhado, ajuste as senhas no `.env` local.

## Como desativar

```bash
docker compose --env-file .env down
```

Para remover os dados persistidos:

```bash
docker compose --env-file .env down -v
```
