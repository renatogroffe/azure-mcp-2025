# azure-mcp-2025
Testes com Azure MCP Server durante o mês de Junho-2026. Envolve o uso de containers (build + publish no Docker Hub, Docker Compose para testes com VS Code).

Imagem pública mais recente para testes:

```
renatogroffe/azure-mcp-2025-06:8
```

Será necessária a criação de um Service Principal, em que para efeito de testes associei permissões como **reader**:

```bash
az ad sp create-for-rbac --name testes-mcp-azure --role Reader --scopes /subscriptions/SUBSCRIPTION_ID
```

Que produzirá como retorno um JSON com as configurações da App Registration que representa o Service Principal:

```json
{
  "appId": "ID DA APP REGISTRATION",
  "displayName": "testes-mcp-azure",
  "password": "SECRET DA APP REGISTRATION",
  "tenant": "ID DO TENANT EM QUE SE ENCONTRA A SUBSCRIPTION"
}
```

Essas configurações deverão então ser informadas nas variáveis **x**, **y** e **z**, que se encontram no **arquivo .env** (pasta **scripts**).

Criando o server MCP via **docker run**:

```bash
docker run -d --env-file .env -p 5008:5008 renatogroffe/azure-mcp-2025-06:8 --transport sse
```
