# Especialista em Validaçêo n8n

Interprete erros de validaçêo e guie a correçêo.

---

## Propósito

Esta skill ajuda a interpretar erros de validaçêo, entender avisos, corrigir problemas comuns e usar perfis de validaçêo apropriados antes de implantar workflows.

---

## Quando Usar

- Encontrando erros de validaçêo
- Antes de implantar workflows
- Entendendo avisos de validaçêo
- Corrigindo problemas de estrutura de operadores

---

## Perfis de Validaçêo

O n8n MCP oferece diferentes perfis de validaçêo:

| Perfil | Descriçêo | Uso |
|--------|-----------|-----|
| `minimal` | Apenas campos obrigatórios | Desenvolvimento rápido |
| `runtime` | O que o n8n realmente verifica | Pré-deploy |
| `ai-friendly` | Balanceado para uso com IA | Padrêo recomendado |
| `strict` | Tudo validado | Workflows críticos |

### Usando Perfis

```javascript
validate_workflow({
  workflow: {...},
  profile: "ai-friendly"
})
```

---

## Tipos de Erro Comuns

### 1. Campo Obrigatório Faltando

**Erro**:
```
Missing required field: channel
```

**Causa**: Node Slack sem canal especificado

**Soluçêo**:
```javascript
{
  resource: "message",
  operation: "post",
  channel: "#notifications",  // Adicionar campo
  text: "Mensagem"
}
```

### 2. Tipo de Dado Inválido

**Erro**:
```
Invalid type: expected string, got number
```

**Causa**: Passando número onde string é esperada

**Soluçêo**:
```javascript
// ERRADO
{ limit: "100" }

// CORRETO
{ limit: 100 }
```

### 3. Conexêo Inválida

**Erro**:
```
Invalid connection: Node "X" output cannot connect to Node "Y" input
```

**Causa**: Tentando conectar tipos incompatíveis

**Soluçêo**: Verifique tipos de porta (main vs ai_tool, etc.)

### 4. Node Nêo Encontrado

**Erro**:
```
Unknown node type: nodes-base.nonexistent
```

**Causa**: Tipo de node incorreto ou nêo existe

**Soluçêo**: Use `search_nodes` para encontrar nome correto

### 5. Credencial Nêo Configurada

**Erro**:
```
Credentials not configured for node: Slack
```

**Causa**: Node requer credenciais nêo especificadas

**Soluçêo**: Adicionar referência de credencial:
```javascript
{
  credentials: {
    slackApi: { id: "cred-id", name: "Slack Creds" }
  }
}
```

---

## Erros de Expressêo

### Sintaxe Inválida

**Erro**:
```
Invalid expression syntax: {{ $json.email }
```

**Causa**: Faltando `}}` de fechamento

**Soluçêo**:
```javascript
// ERRADO
{{ $json.email }

// CORRETO
{{ $json.email }}
```

### Variável Nêo Definida

**Erro**:
```
Cannot read property 'email' of undefined
```

**Causa**: Acessando propriedade de objeto que nêo existe

**Soluçêo**:
```javascript
// ERRADO
{{ $json.user.email }}

// CORRETO (com optional chaining)
{{ $json.user?.email }}
{{ $json.user?.email || 'N/A' }}
```

### Node Referenciado Nêo Existe

**Erro**:
```
Node "Webhook" not found
```

**Causa**: Referenciando node que nêo existe no workflow

**Soluçêo**: Verificar nome exato do node (case-sensitive)

---

## Falsos Positivos

Alguns erros de validaçêo podem ser falsos positivos:

### Credenciais

Validaçêo pode alertar sobre credenciais faltando, mas:
- Credenciais sêo gerenciadas na UI do n8n
- IDs de credencial podem nêo estar disponíveis via MCP
- **Açêo**: Ignorar se credenciais serêo configuradas na UI

### Campos Opcionais

Alguns campos sêo opcionais mas podem aparecer como "recomendados":
- **Açêo**: Avaliar se sêo realmente necessários para seu caso

### Expressões Dinâmicas

Expressões como `{{ $json.field }}` podem parecer inválidas:
- Validador nêo consegue avaliar em tempo de build
- **Açêo**: Ignorar se expressêo está correta

---

## Checklist de Validaçêo

### Antes de Criar Workflow

- [ ] Todos os nodes têm tipo correto (`nodes-base.xxx`)
- [ ] Campos obrigatórios preenchidos
- [ ] Expressões com sintaxe correta `{{ }}`
- [ ] Nomes de nodes únicos
- [ ] Posições definidas para cada node

### Depois de Criar Workflow

- [ ] Executar `validate_workflow`
- [ ] Resolver erros críticos
- [ ] Avaliar avisos (podem ser falsos positivos)
- [ ] Testar com dados de amostra

### Antes de Ativar

- [ ] Credenciais configuradas na UI do n8n
- [ ] Workflow testado manualmente
- [ ] Error handling configurado
- [ ] Monitoramento/alertas configurados

---

## Processo de Correçêo

### 1. Identificar o Erro

```javascript
const result = validate_workflow({workflow});
console.log(result.errors);
```

### 2. Localizar o Problema

- Qual node?
- Qual campo?
- Qual valor atual?

### 3. Aplicar Correçêo

```javascript
n8n_update_partial_workflow({
  workflowId: "abc",
  updateNodes: [
    {
      name: "Node Problemático",
      parameters: {
        // campo corrigido
      }
    }
  ]
})
```

### 4. Revalidar

```javascript
validate_workflow({workflow: updatedWorkflow})
```

---

## Ferramentas de Validaçêo

### validate_workflow

Valida workflow completo:
```javascript
validate_workflow({
  workflow: workflowObject,
  profile: "ai-friendly"
})
```

### validate_node_operation

Valida node específico:
```javascript
validate_node_operation({
  node: nodeObject
})
```

### validate_workflow_connections

Verifica apenas conexões:
```javascript
validate_workflow_connections({
  connections: connectionsObject
})
```

### validate_workflow_expressions

Verifica apenas expressões:
```javascript
validate_workflow_expressions({
  workflow: workflowObject
})
```

---

## Dicas de Troubleshooting

### Erro Persistente

1. Verifique documentaçêo do node com `get_node_info`
2. Compare com template funcional via `search_templates`
3. Simplifique configuraçêo ao mínimo necessário

### Muitos Erros

1. Comece pelo primeiro erro (pode causar os outros)
2. Valide nodes individualmente
3. Reconstrua workflow gradualmente

### Erro Nêo Faz Sentido

1. Pode ser falso positivo
2. Verifique se perfil de validaçêo está apropriado
3. Teste o workflow mesmo assim (n8n pode aceitar)

---

## Integraçêo com Outras Skills

- **n8n MCP Tools Expert** - Ferramentas de validaçêo
- **n8n Node Configuration** - Configuraçêo correta de nodes
- **n8n Expression Syntax** - Corrigir erros de expressêo
- **n8n Workflow Patterns** - Estruturas válidas de workflow
