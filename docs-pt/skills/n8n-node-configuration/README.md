# Configuraçêo de Nodes n8n

Orientaçêo para configuraçêo de nodes com consciência de operaçêo.

---

## Propósito

Esta skill ajuda a configurar nodes n8n corretamente, entendendo dependências de propriedades, campos obrigatórios e padrões específicos de cada node.

---

## Quando Usar

- Configurando operações específicas de nodes
- Entendendo dependências de propriedades
- Determinando campos obrigatórios
- Aprendendo padrões específicos de nodes

---

## Conceitos Chave

### Configuraçêo Consciente de Operaçêo

Operações diferentes precisam de campos diferentes. Exemplo com node Slack:

```javascript
// Para operation='post' (enviar mensagem)
{ resource: "message", operation: "post", channel: "#general", text: "Hello!" }

// Para operation='update' (editar mensagem) - campos diferentes!
{ resource: "message", operation: "update", messageId: "123", text: "Updated!" }
```

### Dependências de Propriedades

Campos mostram/escondem baseado em outros valores:

```
resource: "message"
└─ operation: "post"
   └─ channel (obrigatório)
   └─ text (obrigatório)
   └─ blocks (opcional)
```

### Descoberta Progressiva

1. **Comece com essenciais**: `get_node_essentials` - visêo rápida
2. **Depois detalhes completos**: `get_node_info` - documentaçêo completa

---

## Padrões Comuns de Configuraçêo

### HTTP Request

```javascript
{
  method: "GET" | "POST" | "PUT" | "DELETE",
  url: "https://api.example.com/endpoint",
  authentication: "none" | "genericCredential" | "predefinedCredential",
  sendHeaders: true,
  headerParameters: {
    parameters: [
      { name: "Authorization", value: "Bearer {{$credentials.token}}" }
    ]
  },
  sendBody: true,
  bodyParameters: {
    parameters: [
      { name: "key", value: "value" }
    ]
  }
}
```

### Slack

```javascript
// Enviar mensagem
{
  resource: "message",
  operation: "post",
  channel: "#channel-name",  // ou ID do canal
  text: "Mensagem aqui",
  // Opcional: blocks para formataçêo rica
  blocksUi: {
    blockValues: [
      {
        type: "section",
        text: {
          type: "mrkdwn",
          text: "*Título*\nConteúdo"
        }
      }
    ]
  }
}
```

### Postgres/MySQL

```javascript
// Select
{
  operation: "select",
  table: "users",
  returnAll: false,
  limit: 100,
  where: {
    values: [
      { column: "status", value: "active" }
    ]
  }
}

// Insert
{
  operation: "insert",
  table: "users",
  columns: "name, email, created_at",
  // Dados vêm do input
}
```

### Google Sheets

```javascript
// Append (adicionar linha)
{
  operation: "append",
  documentId: { mode: "id", value: "spreadsheet-id" },
  sheetName: "Sheet1",
  columns: {
    mappingMode: "autoMapInputData"
  }
}
```

### OpenAI Chat

```javascript
{
  resource: "chat",
  operation: "message",
  model: "gpt-4",
  prompt: {
    messages: {
      values: [
        { role: "system", content: "Você é um assistente útil." },
        { role: "user", content: "={{$json.question}}" }
      ]
    }
  },
  options: {
    temperature: 0.7,
    maxTokens: 1000
  }
}
```

---

## Fluxo de Configuraçêo Recomendado

```
1. Pesquisar Node
   └─ search_nodes("slack") → encontrar nome do node

2. Obter Essenciais
   └─ get_node_essentials("nodes-base.slack") → visêo rápida

3. Escolher Operaçêo
   └─ Identificar resource + operation necessários

4. Obter Detalhes
   └─ get_node_info("nodes-base.slack") → campos específicos da operaçêo

5. Configurar
   └─ Preencher campos obrigatórios primeiro
   └─ Adicionar campos opcionais conforme necessário

6. Validar
   └─ validate_node_operation() → verificar configuraçêo
```

---

## Autenticaçêo

### Tipos de Credenciais

| Tipo | Uso |
|------|-----|
| OAuth2 | Google, Slack, HubSpot, etc. |
| API Key | OpenAI, Stripe, muitos serviços |
| HTTP Basic | Autenticaçêo básica |
| HTTP Header | Token em header customizado |

### Configuraçêo

Credenciais sêo configuradas:
1. **Na UI do n8n**: Settings → Credentials → Create
2. **Referenciadas no workflow**: Seçêo "Credentials" do node

**Nunca hardcode credenciais nos parâmetros!**

---

## Campos Comuns

### Campos de Opções

```javascript
options: {
  // Campos opcionais específicos da operaçêo
  timeout: 5000,
  retry: true,
  // etc.
}
```

### Campos de Paginaçêo

```javascript
{
  returnAll: true,  // Buscar todos os registros
  // OU
  returnAll: false,
  limit: 100        // Limitar resultados
}
```

### Campos de Filtro

```javascript
where: {
  values: [
    { column: "field", operator: "equals", value: "test" }
  ]
}
```

---

## Dicas de Troubleshooting

### Node nêo aceita minha configuraçêo

1. Verifique se `resource` e `operation` estêo corretos
2. Verifique campos obrigatórios com `get_node_info`
3. Valide com `validate_node_operation`

### Credenciais nêo funcionando

1. Teste as credenciais separadamente
2. Verifique escopos OAuth necessários
3. Regenere tokens se expirados

### Dados nêo aparecendo no próximo node

1. Verifique a saída do node anterior
2. Use expressões corretas: `{{$json.field}}`
3. Verifique se o node retorna dados

---

## Integraçêo com Outras Skills

- **n8n MCP Tools Expert** - Encontrar nodes e operações
- **n8n Workflow Patterns** - Onde o node se encaixa no fluxo
- **n8n Expression Syntax** - Expressões nos campos
- **n8n Validation Expert** - Validar configuraçêo
