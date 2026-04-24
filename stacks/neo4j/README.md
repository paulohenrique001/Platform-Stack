# Neo4j Stack

Stack opcional para desenvolvimento local com Neo4j Community e o Browser embutido.

Ela fica desabilitada por padrão porque está fora do `docker-compose.yml` principal.

## Serviços

| Serviço | Uso | URL/porta |
| --- | --- | --- |
| Neo4j Browser | Interface web embutida | `http://localhost:7474` |
| Neo4j Bolt | Conexão para drivers | `localhost:7687` |

## Como ativar

Pelo Dockge, use o scan de stacks e suba a stack `neo4j`.

Via terminal:

```bash
cd stacks/neo4j
cp .env.example .env
docker compose --env-file .env up -d
```

No Windows PowerShell:

```powershell
Set-Location stacks/neo4j
Copy-Item .env.example .env
docker compose --env-file .env up -d
```

## Acesso

No Neo4j Browser, use:

```text
URL: http://localhost:7474
Usuário: neo4j
Senha: neo4jpass
Bolt: bolt://localhost:7687
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
