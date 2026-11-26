# Guia de Análise de Stack de Negócios

Integrações SaaS comuns, seu suporte no n8n e recomendações arquiteturais.

---

## Categorias de Stack

### Plataformas de E-Commerce

| Plataforma | Node n8n | Tipo de Auth | Suporte Webhook | Padrêo Recomendado |
|------------|----------|--------------|-----------------|---------------------|
| **Shopify** | `nodes-base.shopify` | OAuth | Sim | Processamento Webhook |
| **WooCommerce** | `nodes-base.wooCommerce` | OAuth | Sim | Processamento Webhook |
| **BigCommerce** | `nodes-base.bigCommerce` | OAuth | Sim | Processamento Webhook |
| **Magento** | HTTP Request | API Key | Sim | Integraçêo API HTTP |
| **Stripe** | `nodes-base.stripe` | API Key | Sim | Processamento Webhook |
| **Square** | HTTP Request | OAuth | Sim | Integraçêo API HTTP |

**Automações Comuns de E-commerce:**
1. Pedido → Notificaçêo de fulfillment
2. Novo cliente → Sync com CRM
3. Carrinho abandonado → Disparo de sequência de email
4. Atualizaçêo de estoque → Sync multi-canal
5. Reembolso → Ticket de suporte + contabilidade

**Exemplo de Stack: Shopify + Klaviyo + Slack**
```
Veredicto: n8n Puro
Justificativa:
- Todos têm nodes nativos
- Padrões de webhook padrêo
- Baixo volume de dados por evento
- OAuth gerenciado automaticamente
```

---

### Sistemas de CRM

| Plataforma | Node n8n | Tipo de Auth | Sync Real-time | Padrêo Recomendado |
|------------|----------|--------------|----------------|---------------------|
| **HubSpot** | `nodes-base.hubspot` | OAuth | Webhooks | Processamento Webhook |
| **Salesforce** | `nodes-base.salesforce` | OAuth | Streaming API | Integraçêo API HTTP |
| **Zoho CRM** | `nodes-base.zohoCrm` | OAuth | Webhooks | Processamento Webhook |
| **Pipedrive** | `nodes-base.pipedrive` | API Key | Webhooks | Processamento Webhook |
| **Copper** | HTTP Request | API Key | Webhooks | Integraçêo API HTTP |
| **Close** | HTTP Request | API Key | Webhooks | Integraçêo API HTTP |

**Automações Comuns de CRM:**
1. Formulário de lead → CRM + Notificaçêo de vendas
2. Mudança de estágio de deal → Criaçêo de tarefa
3. Atualizaçêo de contato → Sync com lista de email
4. Reuniêo agendada → Calendário + email de preparaçêo
5. Deal ganho → Disparo de workflow de onboarding

**Exemplo de Stack: HubSpot + Typeform + Notion**
```
Veredicto: n8n Puro
Justificativa:
- OAuth do HubSpot gerenciado nativamente
- Integraçêo webhook do Typeform
- API do Notion para atualizações de banco
- Workflow visual para equipe de vendas
```

---

### Automaçêo de Marketing

| Plataforma | Node n8n | Tipo de Auth | Operações em Lote | Padrêo Recomendado |
|------------|----------|--------------|-------------------|---------------------|
| **Mailchimp** | `nodes-base.mailchimp` | OAuth | Sim | Tarefas Agendadas |
| **Klaviyo** | `nodes-base.klaviyo` | API Key | Sim | Processamento Webhook |
| **ActiveCampaign** | `nodes-base.activeCampaign` | API Key | Sim | Integraçêo API HTTP |
| **Brevo (Sendinblue)** | `nodes-base.sendInBlue` | API Key | Sim | Tarefas Agendadas |
| **ConvertKit** | `nodes-base.convertKit` | API Key | Limitado | Integraçêo API HTTP |
| **Customer.io** | HTTP Request | API Key | Sim | Integraçêo API HTTP |

**Automações Comuns de Marketing:**
1. Novo cadastro → Sequência de boas-vindas
2. Compra → Campanha pós-compra
3. Score de engajamento → Segmentaçêo de lista
4. Participaçêo em evento → Sequência de follow-up
5. Carrinho abandonado → Email de recuperaçêo

**Exemplo de Stack: Klaviyo + Shopify + Google Sheets**
```
Veredicto: n8n Puro
Justificativa:
- Auth por API key do Klaviyo (simples)
- Webhooks do Shopify para triggers
- Google Sheets para relatórios (OAuth gerenciado)
- Sem processamento complexo necessário
```

---

### Produtividade & Colaboraçêo

| Plataforma | Node n8n | Tipo de Auth | Real-time | Padrêo Recomendado |
|------------|----------|--------------|-----------|---------------------|
| **Notion** | `nodes-base.notion` | OAuth | Polling | Operações de Banco |
| **Airtable** | `nodes-base.airtable` | API Key | Webhooks (pago) | Operações de Banco |
| **Google Sheets** | `nodes-base.googleSheets` | OAuth | Polling | Operações de Banco |
| **Coda** | `nodes-base.coda` | API Key | Webhooks | Operações de Banco |
| **Monday.com** | `nodes-base.mondayCom` | API Key | Webhooks | Processamento Webhook |
| **ClickUp** | `nodes-base.clickUp` | OAuth | Webhooks | Processamento Webhook |
| **Asana** | `nodes-base.asana` | OAuth | Webhooks | Processamento Webhook |

**Automações Comuns de Produtividade:**
1. Tarefa completada → Atualizaçêo de status + notificaçêo
2. Atualizaçêo de banco → Sync cross-platform
3. Envio de formulário → Criaçêo de tarefa
4. Marco de projeto → Geraçêo de relatório
5. Atribuiçêo de equipe → Calendário + notificaçêo

**Exemplo de Stack: Notion + Slack + Calendar**
```
Veredicto: n8n Puro
Justificativa:
- OAuth do Notion para acesso seguro
- Slack para notificações
- Google Calendar para agendamento
- Padrões de sync de banco de dados padrêo
```

---

### Plataformas de Comunicaçêo

| Plataforma | Node n8n | Tipo de Auth | Tratam. Mensagens | Padrêo Recomendado |
|------------|----------|--------------|-------------------|---------------------|
| **Slack** | `nodes-base.slack` | OAuth | Slash commands, Events | Processamento Webhook |
| **Discord** | `nodes-base.discord` | OAuth | Webhooks, bots | Processamento Webhook |
| **Microsoft Teams** | `nodes-base.microsoftTeams` | OAuth | Webhooks | Processamento Webhook |
| **Telegram** | `nodes-base.telegram` | API Token | Webhooks | Processamento Webhook |
| **WhatsApp Business** | HTTP Request | API Key | Webhooks | Integraçêo API HTTP |
| **Twilio** | `nodes-base.twilio` | API Key | Webhooks | Processamento Webhook |

**Automações Comuns de Comunicaçêo:**
1. Slash command → Busca de dados + resposta
2. Mensagem em canal → Criaçêo de tarefa
3. Alerta → Notificaçêo multi-canal
4. Envio de formulário → Notificaçêo no chat
5. Relatório agendado → Post no canal

---

### Suporte & Atendimento

| Plataforma | Node n8n | Tipo de Auth | Gerenc. Tickets | Padrêo Recomendado |
|------------|----------|--------------|-----------------|---------------------|
| **Zendesk** | `nodes-base.zendesk` | OAuth | Completo | Processamento Webhook |
| **Intercom** | `nodes-base.intercom` | OAuth | Completo | Processamento Webhook |
| **Freshdesk** | `nodes-base.freshdesk` | API Key | Completo | Processamento Webhook |
| **Help Scout** | HTTP Request | API Key | Completo | Integraçêo API HTTP |
| **Crisp** | HTTP Request | API Key | Completo | Integraçêo API HTTP |

**Automações Comuns de Suporte:**
1. Novo ticket → Roteamento por prioridade
2. Escalaçêo de ticket → Notificaçêo ao gerente
3. Violaçêo de SLA → Alerta + auto-escalaçêo
4. Feedback de cliente → Tracking de NPS
5. Ticket resolvido → Pesquisa de follow-up

---

### IA & Analytics

| Plataforma | Node n8n | Tipo de Auth | Rate Limits | Padrêo Recomendado |
|------------|----------|--------------|-------------|---------------------|
| **OpenAI** | `nodes-langchain.openAi` | API Key | Sim | Workflow Agente IA |
| **Anthropic** | `nodes-langchain.anthropic` | API Key | Sim | Workflow Agente IA |
| **Google AI** | `nodes-langchain.googleAi` | API Key | Sim | Workflow Agente IA |
| **Pinecone** | HTTP Request | API Key | Sim | Workflow Agente IA |
| **Google Analytics** | `nodes-base.googleAnalytics` | OAuth | Sim | Tarefas Agendadas |
| **Mixpanel** | HTTP Request | API Key | Sim | Integraçêo API HTTP |

**Automações Comuns com IA:**
1. Consulta de cliente → Classificaçêo IA + roteamento
2. Conteúdo recebido → Sumarizaçêo IA
3. Formulário de lead → Pontuaçêo de qualificaçêo IA
4. Ticket de suporte → Rascunho de resposta IA
5. Upload de documento → Extraçêo IA + armazenamento

**Exemplo de Stack: OpenAI + HubSpot + Slack**
```
Veredicto: Híbrido
Justificativa:
- HubSpot/Slack via n8n (OAuth)
- Processamento de IA em node Code ou serviço externo
- Prompts complexos podem precisar de Python para gerenciamento
- Tracking de custos importante
```

---

## Framework de Decisêo Multi-Stack

### Template de Análise

Quando usuário descrever seu stack, colete:

```markdown
## Inventário de Stack

### Sistemas Primários (Core do Negócio)
1. [Sistema] - [Papel] - [Volume de Dados]
2. ...

### Sistemas Secundários (Funções de Suporte)
1. [Sistema] - [Papel] - [Frequência]
2. ...

### Pontos de Integraçêo Necessários
1. [Sistema A] → [Sistema B]: [Trigger] → [Açêo]
2. ...

### Características de Dados
- Registros por dia: [estimativa]
- Pico de carga: [quando]
- Sensibilidade de dados: [PII/financeiro/padrêo]

### Capacidades da Equipe
- Nível técnico: [nêo-técnico/misto/equipe dev]
- Dono da manutençêo: [cargo]
```

### Pontuaçêo de Complexidade

| Fator | Baixa (1) | Média (2) | Alta (3) |
|-------|-----------|-----------|----------|
| Número de sistemas | 2-3 | 4-5 | 6+ |
| Integrações OAuth | 0-1 | 2-3 | 4+ |
| Volume de dados (diário) | < 1000 | 1000-10000 | > 10000 |
| Requisitos real-time | Nenhum | Alguns | Crítico |
| Envolvimento IA/ML | Nenhum | Classificaçêo | Generativo |
| Nível técnico da equipe de manutençêo | Equipe dev | Mista | Nêo-técnico |

**Interpretaçêo da Pontuaçêo:**
- 6-9: n8n puro recomendado
- 10-14: Híbrido provavelmente necessário
- 15-18: Componente Python significativo necessário

---

## Combinações de Stack Comuns

### Stack de Startup SaaS
**Stripe + HubSpot + Slack + Notion + Intercom**

```
Veredicto: n8n Puro
Complexidade: Média
Automações Principais:
1. Pagamento → Atualizaçêo CRM + Notificaçêo Slack
2. Novo cliente → Workflow de onboarding
3. Ticket de suporte → Roteamento por prioridade
4. Sinal de churn → Workflow de retençêo

Padrêo: Múltiplos workflows disparados por webhook
```

### Operações de E-commerce
**Shopify + Klaviyo + ShipStation + QuickBooks**

```
Veredicto: n8n Puro (possivelmente híbrido para inventário)
Complexidade: Média-Alta
Automações Principais:
1. Pedido → Fulfillment + notificaçêo ao cliente
2. Envio → Atualizaçêo de tracking
3. Devoluçêo → Processamento de reembolso
4. Diário → Sync de vendas para contabilidade

Padrêo: Processamento webhook + sync agendado
Aviso: Alto volume pode precisar de processamento em lote
```

### Negócio de Serviços com IA
**Typeform + OpenAI + Airtable + Calendly + Zoom**

```
Veredicto: Híbrido
Complexidade: Alta
Automações Principais:
1. Formulário → Análise IA → Score de qualificaçêo
2. Lead qualificado → Agendamento automático de reuniêo
3. Reuniêo → Resumo IA → Atualizaçêo CRM
4. Follow-up → Outreach personalizado

Padrêo: Workflow de agente IA com checkpoints humanos
Aviso: Custos de IA, necessário estratégia de cache
```

### Pipeline de Dados Enterprise
**Salesforce + Snowflake + Tableau + Slack**

```
Veredicto: Python-primário com triggers n8n
Complexidade: Alta
Automações Principais:
1. Agendado → Extraçêo de dados
2. Transformar → Carregar para warehouse
3. Anomalia detectada → Alerta
4. Diário → Distribuiçêo de relatório

Padrêo: Tarefas agendadas + processamento em lote
Aviso: Volume requer streaming Python
```

---

## Pegadinhas de Integraçêo por Plataforma

### Shopify
- Payload de webhook é aninhado
- Rate limit: 2 chamadas/segundo (burst), 40/minuto (sustentado)
- Considere: Sync de inventário pode ser alto volume

### HubSpot
- Lookups de associaçêo requerem múltiplas chamadas
- Rate limit: 100 chamadas/10 segundos
- Considere: Histórico de propriedades pode inflar payloads

### Salesforce
- Queries SOQL têm limites
- Use Bulk API para operações grandes
- Considere: Streaming API para real-time

### Google Sheets
- 300 requests/minuto
- Sem webhooks (precisa de polling)
- Considere: Use Airtable para necessidades real-time

### Slack
- Modo socket vs webhooks
- Rate limits variam por endpoint
- Considere: Thread replies para contexto

### OpenAI/Claude
- Custos de tokens acumulam rápido
- Rate limits por tier
- Considere: Caching, seleçêo de modelo

---

## Skills Relacionadas

- **n8n-node-configuration** - Configurar nodes de plataformas específicas
- **n8n-workflow-patterns** - Padrões de implementaçêo
- **n8n-mcp-tools-expert** - Encontrar nodes específicos de plataformas
