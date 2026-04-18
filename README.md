# Platform Stack

Template de plataforma local para desenvolvimento com Docker Compose.

A stack principal sobe Dockge, Dozzle e Uptime Kuma para gerenciamento leve de stacks Compose, logs locais e monitoramento simples.

As stacks opcionais ficam em `stacks/` e não sobem junto com a plataforma base. O desenvolvedor ativa somente quando precisar de algum banco ou ferramenta local.

## Requisitos

- Docker
- Docker Compose

## Serviços principais

| Serviço | Uso | URL |
| --- | --- | --- |
| Dockge | Gerenciar stacks Compose com console interativo habilitado | `http://localhost:5001` |
| Dozzle | Logs dos containers | `http://localhost:8080` |
| Uptime Kuma | Monitoramento local | `http://localhost:3001` |

## Stacks opcionais

| Stack | Serviços | Padrão | Acesso |
| --- | --- | --- | --- |
| `stacks/redis` | Redis + Redis Insight | Desabilitada | Redis `localhost:6379`, Redis Insight `http://localhost:5540` |
| `stacks/neo4j` | Neo4j com Browser embutido | Desabilitada | Browser `http://localhost:7474`, Bolt `localhost:7687` |
| `stacks/mariadb` | MariaDB + phpMyAdmin | Desabilitada | MariaDB `localhost:3306`, phpMyAdmin `http://localhost:8081` |
| `stacks/mongodb` | MongoDB com `mongosh` no container | Desabilitada | MongoDB `localhost:27017` |
| `stacks/dynamodb` | DynamoDB Local + AWS CLI | Desabilitada | DynamoDB `http://localhost:8000` |
| `stacks/postgresql` | PostgreSQL + pgAdmin | Desabilitada | PostgreSQL `localhost:5432`, pgAdmin `http://localhost:5050` |
| `stacks/elasticsearch` | Elasticsearch + Kibana | Desabilitada | Elasticsearch `http://localhost:9200`, Kibana `http://localhost:5601` |

## Como subir a plataforma

Copie o arquivo de exemplo.

Windows PowerShell:

```powershell
Copy-Item .env.example .env
```

Ubuntu:

```bash
cp .env.example .env
```

Suba a stack principal:

```bash
docker compose --env-file .env up -d
```

Acesse:

```text
http://localhost:5001
```

## Ativando uma stack opcional

Pelo Dockge, use o scan de stacks e suba apenas a stack necessária.

Via terminal, entre na pasta da stack:

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

Troque `redis` pelo nome da stack desejada. Antes de usar em um projeto compartilhado, ajuste senhas e portas no `.env` local da stack.

Para o Dockge conseguir pausar, reiniciar, excluir e atualizar uma stack, o `STACK_NAME` da stack opcional deve ser igual ao nome da pasta. Exemplo: em `stacks/redis/.env`, mantenha `STACK_NAME=redis`. Usar `STACK_NAME=dockge-redis` dentro de `stacks/redis` faz o Docker Compose criar outro projeto e o Dockge pode exibir a mensagem "Esta stack não é gerenciada pelo Dockge".

Os containers, volumes e redes usam o prefixo `dockge-` ou `dockge_`, mas o nome do projeto Compose das stacks opcionais acompanha a pasta.

## Primeiro acesso ao Dockge

No primeiro acesso, o Dockge solicita a criação do usuário administrador pela interface.

Essas informações ficam persistidas no volume definido em `DOCKGE_DATA_VOLUME_NAME`. Para recriar o setup inicial, remova os volumes da stack com cuidado:

```bash
docker compose --env-file .env down -v
```

## Comandos úteis

Os comandos Docker Compose são iguais no Windows PowerShell e no Ubuntu:

```bash
docker compose --env-file .env ps
docker compose --env-file .env logs -f
docker compose --env-file .env down
docker compose --env-file .env down -v
```

## Usando em outros projetos

Este template não usa proxy reverso. Para acessar aplicações de outros projetos, exponha portas diretamente no Compose do próprio projeto.

```yaml
services:
  app:
    image: nginx:alpine
    ports:
      - "8088:80"
```

Depois acesse:

```text
http://localhost:8088
```

Se quiser gerenciar essa stack pelo Dockge, coloque o arquivo em `stacks/<nome-da-stack>/compose.yaml` e use o scan de stacks na interface.

## Estrutura

- `docker-compose.yml`: stack principal
- `.env.example`: variáveis públicas do template
- `stacks/`: stacks opcionais gerenciadas pelo Dockge
- `docs/`: documentação complementar
- `examples/`: exemplos de integração

## Notas

- Este projeto é para desenvolvimento local, não produção.
- Não publique `.env` ou chaves privadas.
- O arquivo `.env` é local e pode ter nomes personalizados de stack, containers e volumes; use `.env.example` como referência pública do template.
- Dockge e Dozzle usam o Docker socket para gerenciar stacks e ler logs locais.
- O console interativo do Dockge fica habilitado por padrão via `DOCKGE_ENABLE_CONSOLE=true`.
- Se as stacks do Dockge usarem bind mounts, prefira caminhos absolutos válidos para o Docker no `DOCKGE_STACKS_PATH`.
- Se alguma stack opcional já foi iniciada com nome antigo `platform-*`, derrube-a pelo terminal antes de recriar com o novo `.env`; containers antigos não passam a ser gerenciados automaticamente pelo Dockge.
- Bancos, filas, caches e aplicações devem ficar em stacks opcionais ou em outros repositórios, conforme a necessidade do projeto.
- Algumas imagens usam `latest` para manter o template simples em ambiente local; para maior reprodutibilidade, fixe tags conhecidas antes de usar como base estável.
