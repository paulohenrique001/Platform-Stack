# Redis Stack

Stack opcional para desenvolvimento local com Redis e Redis Insight.

Ela fica desabilitada por padrão porque está fora do `docker-compose.yml` principal.

## Serviços

| Serviço | Uso | URL/porta |
| --- | --- | --- |
| Redis | Cache e banco chave-valor local | `localhost:6379` |
| Redis Insight | Interface web para Redis | `http://localhost:5540` |

## Como ativar

Pelo Dockge, use o scan de stacks e suba a stack `redis`.

Via terminal:

```bash
cd stacks/redis
cp .env.example .env
docker compose --env-file .env up -d
```

No Windows PowerShell:

```powershell
Set-Location stacks/redis
Copy-Item .env.example .env
docker compose --env-file .env up -d
```

## Acesso

Use estes dados no Redis Insight ou em clientes locais:

```text
Host: redis
Porta interna: 6379
Porta local: 6379
Senha: change_me_redis_password
```

Para usar o CLI dentro do container:

```bash
docker compose --env-file .env exec redis redis-cli -a change_me_redis_password
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
