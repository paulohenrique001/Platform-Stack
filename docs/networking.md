# Networking

Este template usa portas locais diretas. Não há proxy reverso nem resolução automática por domínio.

## Portas padrão

- Dockge: `5001`
- Dozzle: `8080`
- Uptime Kuma: `3001`

## Outros projetos

Exponha as portas no Compose do próprio projeto:

```yaml
services:
  app:
    image: nginx:alpine
    ports:
      - "8088:80"
```

Depois acesse `http://localhost:8088`.

## Rede Docker

A stack ainda usa a rede `platform_network` para comunicação interna entre os serviços. Outros projetos só precisam entrar nessa rede se houver uma integração explícita com algum serviço da plataforma.
