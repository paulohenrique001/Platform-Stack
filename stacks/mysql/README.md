# MySQL Stack

Stack opcional para desenvolvimento local com MySQL 8.0.42.

Ela fica desabilitada por padrao porque esta fora do `docker-compose.yml` principal. O desenvolvedor ativa somente quando precisar de MySQL no ambiente local.

## Servicos

| Servico | Uso | URL/porta |
| --- | --- | --- |
| MySQL | Banco relacional local | `localhost:3306` |

## Como ativar

Pelo Dockge, use o scan de stacks e suba a stack `mysql`.

Via terminal:

```bash
cd stacks/mysql
cp .env.example .env
docker compose --env-file .env up -d
```

No Windows PowerShell:

```powershell
Set-Location stacks/mysql
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
docker compose --env-file .env exec mysql mysql -uapp -papp app
```

Tambem e possivel conectar como `root` usando `root`.

Antes de usar em um projeto compartilhado, ajuste as senhas no `.env` local.

## Como desativar

```bash
docker compose --env-file .env down
```

Para remover os dados persistidos:

```bash
docker compose --env-file .env down -v
```
