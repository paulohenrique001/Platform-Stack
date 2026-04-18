# Troubleshooting

## Porta local não abre

Confirme se o serviço está rodando.

Windows PowerShell e Ubuntu:

```bash
docker compose --env-file .env ps
```

Confira se a porta está livre ou altere o valor correspondente no `.env`.

## Portas padrão

- Dockge: `DOCKGE_PORT=5001`
- Dozzle: `DOZZLE_PORT=8080`
- Uptime Kuma: `UPTIME_KUMA_PORT=3001`

## Dockge não encontra stacks

As stacks precisam estar dentro de `stacks/<nome-da-stack>/compose.yaml` ou `stacks/<nome-da-stack>/docker-compose.yml`.

Depois use a opção de scan do Dockge para atualizar a lista.

Se uma stack usa bind mounts, configure `DOCKGE_STACKS_PATH` com um caminho absoluto acessível pelo Docker. Isso evita que o Docker crie volumes em outro lugar quando o Compose for executado pelo Dockge.

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
