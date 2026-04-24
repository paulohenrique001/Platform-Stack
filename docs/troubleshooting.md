# Troubleshooting

## Porta local não abre

Confirme se o serviço está rodando.

Windows PowerShell e Ubuntu:

```bash
docker compose --env-file .env ps
```

Confira se a porta está livre ou altere o valor correspondente no `.env`.

## Portas padrão

Stack principal:

- Dockge: `DOCKGE_PORT=5001`
- Dozzle: `DOZZLE_PORT=8080`
- Uptime Kuma: `UPTIME_KUMA_PORT=3001`

Stacks opcionais:

- Redis: `REDIS_PORT=6379`, `REDIS_INSIGHT_PORT=5540`
- Neo4j: `NEO4J_HTTP_PORT=7474`, `NEO4J_BOLT_PORT=7687`
- MariaDB: `MARIADB_PORT=3306`
- MongoDB: `MONGODB_PORT=27017`
- DynamoDB Local: `DYNAMODB_PORT=8000`
- PostgreSQL: `POSTGRESQL_PORT=5432`
- Elasticsearch: `ELASTICSEARCH_HTTP_PORT=9200`, `ELASTICSEARCH_TRANSPORT_PORT=9300`, `KIBANA_PORT=5601`

Essas variáveis ficam no `.env` local de cada stack opcional.

## Dockge não encontra stacks

As stacks precisam estar dentro de `stacks/<nome-da-stack>/docker-compose.yml`.

Depois use a opção de scan do Dockge para atualizar a lista.

As stacks em `stacks/` vêm prontas no template, mas ficam desabilitadas até o desenvolvedor subir pelo Dockge ou executar `docker compose --env-file .env up -d` dentro da pasta correspondente.

O nome do projeto Compose das stacks opcionais fica fixo no próprio `docker-compose.yml`, igual ao nome da pasta. Se uma stack aparecer fora do Dockge, confirme se ela foi iniciada dentro da pasta correta ou pela interface do Dockge.

Se uma stack usa bind mounts, configure `DOCKGE_STACKS_PATH` com um caminho absoluto acessível pelo Docker. Isso evita que o Docker crie volumes em outro lugar quando o Compose for executado pelo Dockge.

## Stack aparece como não gerenciada pelo Dockge

Se a mensagem for "Esta stack não é gerenciada pelo Dockge", confira:

- O arquivo está em `stacks/<nome-da-stack>/docker-compose.yml`.
- A stack foi iniciada dentro da própria pasta ou pelo Dockge.
- Não existe um projeto antigo com nome `platform-*` ainda rodando.

Se ela já foi iniciada com um nome de projeto antigo como `platform-*`, derrube a stack antiga pelo terminal usando o nome do projeto antigo, depois recrie com o compose atual. Containers antigos não passam a ser gerenciados automaticamente pelo Dockge.

## Elasticsearch não inicia

No Linux ou WSL, Elasticsearch pode exigir aumento de `vm.max_map_count`.

Linux:

```bash
sudo sysctl -w vm.max_map_count=262144
```

WSL, em uma janela administrativa do PowerShell:

```powershell
wsl -d docker-desktop sysctl -w vm.max_map_count=262144
```

Também confira a memória disponível no Docker Desktop. A stack usa `ES_JAVA_OPTS=-Xms512m -Xmx512m` por padrão, mas Elasticsearch e Kibana podem precisar de mais memória dependendo do uso.

## Aviso de permissão no Docker do Windows

Se aparecer um aviso parecido com este:

```text
Error loading config file: open C:\Users\<usuario>\.docker\config.json: Acesso negado
```

Isso indica um problema de permissão na configuração local do Docker CLI, não um erro do Compose deste projeto.

Opções de correção:

- Ajustar a permissão do arquivo `C:\Users\<usuario>\.docker\config.json` para o seu usuário.
- Recriar a configuração do Docker Desktop fazendo login novamente.
- Remover ou renomear o arquivo `config.json` se ele estiver corrompido e deixar o Docker Desktop recriá-lo.
