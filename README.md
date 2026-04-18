# Platform Stack

Template de plataforma local para desenvolvimento com Docker Compose.

A stack sobe Dockge, Dozzle e Uptime Kuma para gerenciamento leve de stacks Compose, logs locais e monitoramento simples.

## Requisitos

- Docker
- Docker Compose

## Serviços

| Serviço | Uso | URL |
| --- | --- | --- |
| Dockge | Gerenciar stacks Compose com console interativo habilitado | `http://localhost:5001` |
| Dozzle | Logs dos containers | `http://localhost:8080` |
| Uptime Kuma | Monitoramento local | `http://localhost:3001` |

## Como subir

Copie o arquivo de exemplo.

Windows PowerShell:

```powershell
Copy-Item .env.example .env
```

Ubuntu:

```bash
cp .env.example .env
```

Suba a stack:

```bash
docker compose --env-file .env up -d
```

Acesse:

```text
http://localhost:5001
```

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
- `stacks/`: stacks gerenciadas pelo Dockge
- `docs/`: documentação complementar
- `examples/`: exemplos de integração

## Notas

- Este projeto é para desenvolvimento local, não produção.
- Não publique `.env` ou chaves privadas.
- O arquivo `.env` é local e pode ter nomes personalizados de stack, containers e volumes; use `.env.example` como referência pública do template.
- Dockge e Dozzle usam o Docker socket para gerenciar stacks e ler logs locais.
- O console interativo do Dockge fica habilitado por padrão via `DOCKGE_ENABLE_CONSOLE=true`.
- Se as stacks do Dockge usarem bind mounts, prefira caminhos absolutos válidos para o Docker no `DOCKGE_STACKS_PATH`.
- Bancos, filas, caches e aplicações devem ficar em outros repositórios.
- Algumas imagens usam `latest` para manter o template simples em ambiente local; para maior reprodutibilidade, fixe tags conhecidas antes de usar como base estável.
