ï»¿# n8n Powerhouse

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="48" />
  <p><strong>Arckhé AI</strong></p>
</div>


**Transforme o Claude em um especialista em automaêÂ§êÂ£o n8n.** Construa, valide e implante workflows prontos para produêÂ§êÂ£o atravêÂ©s de conversas.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![n8n](https://img.shields.io/badge/n8n-Automation-orange)](https://n8n.io)
[![Claude Code](https://img.shields.io/badge/Claude-Code-blue)](https://claude.ai/claude-code)

> ê°Å¸â¡Â¬ê°Å¸â¡Â§ [English version](README-EN.md)

---

## O Problema

Construir workflows no n8n normalmente requer:
- Aprender as configuraêÂ§êÂµes e peculiaridades dos nodes do n8n
- Entender quais nodes existem e como configurêÂ¡-los
- Conhecer os padrêÂµes corretos para webhooks, APIs e bancos de dados
- Debugar erros de sintaxe em expressêÂµes
- Descobrir por que seu workflow nêÂ£o estêÂ¡ validando

**E se o Claude simplesmente soubesse tudo isso?**

---

## A SoluêÂ§êÂ£o

O n8n Powerhouse êÂ© um **framework de skills** que dêÂ¡ ao Claude expertise profunda em automaêÂ§êÂ£o n8n. Ele combina:

1. **8 skills especializadas** - Conhecimento profundo sobre padrêÂµes, sintaxe e boas prêÂ¡ticas do n8n
2. **IntegraêÂ§êÂ£o n8n MCP** - ConexêÂ£o direta com sua instêÂ¢ncia n8n para criar/editar/validar workflows
3. **OrientaêÂ§êÂ£o para produêÂ§êÂ£o** - Conhecimento embutido sobre idempotêÂªncia, tratamento de erros e questêÂµes operacionais

---

## Antes e Depois

### Antes (sem o n8n Powerhouse)

```
VocêÂª: Construa um workflow que sincronize pedidos do Shopify com meu CRM

Claude: Posso ajudêÂ¡-lo a desenhar um workflow. VocêÂª precisaria de:
1. Um node trigger do Shopify
2. Alguma transformaêÂ§êÂ£o
3. Um node de CRM

VocêÂª precisarêÂ¡ configurar isso no n8n...
[Conselho genêÂ©rico, sem implementaêÂ§êÂ£o real]
```

### Depois (com o n8n Powerhouse)

```
VocêÂª: Construa um workflow que sincronize pedidos do Shopify com meu CRM

Claude: Vou construir isso para vocêÂª. Deixe-me:
1. Analisar seu stack ê¢â â Recomendando n8n puro (ambos têÂªm nodes OAuth)
2. Aplicar padrêÂ£o de processamento de webhook com idempotêÂªncia
3. Criar o workflow na sua instêÂ¢ncia n8n...

ê¢Åâ¦ Workflow criado: "Shopify Order ê¢â â Zoho CRM + Slack"
   ID: BbRLnEFYH9f4T6Jr
   URL: https://sua-instancia.app.n8n.cloud/workflow/BbRLnEFYH9f4T6Jr

PrêÂ³ximos passos:
1. Adicione suas credenciais do Shopify e Zoho
2. Ative o workflow
```

**O Claude realmente constrêÂ³i e implanta o workflow.**

---

## O Que SêÂ£o Skills do Claude Code?

[Claude Code](https://claude.ai/claude-code) êÂ© a ferramenta CLI da Anthropic para trabalhar com Claude no seu terminal. **Skills** sêÂ£o coleêÂ§êÂµes de arquivos markdown que dêÂ£o ao Claude conhecimento especializado.

Quando vocêÂª coloca skills em `.claude/skills/`, o Claude as lêÂª e ganha essa expertise. O n8n Powerhouse fornece 8 skills (~25.000 palavras de conhecimento sobre n8n) cobrindo:

- DecisêÂµes de arquitetura
- PadrêÂµes de workflow
- ConfiguraêÂ§êÂ£o de nodes
- Sintaxe de cêÂ³digo
- Debug de expressêÂµes
- ValidaêÂ§êÂ£o

---

## O Que êÂ© o n8n MCP?

[MCP (Model Context Protocol)](https://modelcontextprotocol.io/) permite que o Claude use ferramentas externas. O [n8n MCP](https://www.npmjs.com/package/n8n-mcp) dêÂ¡ ao Claude ferramentas para:

- **Pesquisar** nodes e templates
- **Criar** workflows na sua instêÂ¢ncia n8n
- **Atualizar** workflows existentes
- **Validar** configuraêÂ§êÂµes
- **Disparar** workflows via webhook
- **Listar** execuêÂ§êÂµes e debugar

Juntos, skills + MCP = Claude pode **conhecer** n8n E **fazer** n8n.

---

## InêÂ­cio RêÂ¡pido

### 1. Instalar o n8n MCP

```bash
claude mcp add n8n-mcp-api \
  -e MCP_MODE=stdio \
  -e LOG_LEVEL=error \
  -e DISABLE_CONSOLE_OUTPUT=true \
  -e N8N_API_URL=https://SUA-INSTANCIA.app.n8n.cloud \
  -e N8N_API_KEY=sua-chave-api-aqui \
  -- npx -y n8n-mcp
```

**Obtenha sua chave API:** Dashboard do n8n ê¢â â Settings ê¢â â API ê¢â â Create API Key

### 2. Clonar Este RepositêÂ³rio

```bash
git clone https://github.com/linnoff88-dev/n8n-ps.git
cd n8n-ps
```

### 3. Iniciar o Claude Code

```bash
claude
```

Pronto. O Claude agora tem expertise completa em n8n.

---

## Exemplos do Mundo Real

### Exemplo 1: AutomaêÂ§êÂ£o de E-commerce

```
VocêÂª: Eu tenho uma loja Shopify e uso Zoho CRM. Quando alguêÂ©m faz um pedido,
      quero sincronizar o cliente no Zoho e notificar minha equipe no Slack.

Claude: Vou analisar seu stack e construir isso...

[Claude usa n8n-workflow-architect para analisar]
ê¢â â Shopify: OAuth, node trigger nativo ê¢Åâ
ê¢â â Zoho CRM: OAuth, node nativo ê¢Åâ
ê¢â â Slack: OAuth, node nativo ê¢Åâ
ê¢â â RecomendaêÂ§êÂ£o: n8n puro (todos os serviêÂ§os suportados)
ê¢â â PadrêÂ£o: Processamento de Webhook com idempotêÂªncia

[Claude usa n8n MCP para criar workflow]
ê¢â â Criado: Shopify Order ê¢â â Zoho CRM + Slack
ê¢â â Inclui: PrevenêÂ§êÂ£o de duplicatas (verificar email antes de criar)
ê¢â â Inclui: Tratamento de erros
ê¢â â Inclui: NotificaêÂ§êÂ£o Slack com detalhes do pedido

Aqui estêÂ¡ seu workflow: [link]
```

### Exemplo 2: SeleêÂ§êÂ£o de Ferramenta

```
VocêÂª: Devo usar n8n ou Python para processar 50.000 registros de clientes diariamente?

Claude: [Usa n8n-workflow-architect/tool-selection-matrix.md]

Para 50.000 registros, recomendo uma **abordagem hêÂ­brida**:

Use n8n para:
- Disparo (schedule trigger)
- AutenticaêÂ§êÂ£o (se APIs precisarem de OAuth)
- NotificaêÂ§êÂµes (alertas no Slack)

Use Python para:
- O processamento real de dados (>5.000 registros êÂ© o limite)
- Streaming eficiente de memêÂ³ria
- TransformaêÂ§êÂµes complexas

Arquitetura:
ê¢âÅê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢âÂ     ê¢âÅê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢âÂ     ê¢âÅê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢âÂ
ê¢ââ n8n         ê¢ââ     ê¢ââ Python      ê¢ââ     ê¢ââ n8n         ê¢ââ
ê¢ââ (Schedule)  ê¢ââ ê¢ââ¬ê¢ââ¬ê¢âÂº ê¢ââ (Process)   ê¢ââ ê¢ââ¬ê¢ââ¬ê¢âÂº ê¢ââ (Notify)    ê¢ââ
ê¢ââê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢âË     ê¢ââê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢âË     ê¢ââê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢âË

Por que nêÂ£o n8n puro?
- n8n roda em Node.js com limites de memêÂ³ria
- 50k registros provavelmente travaria ou daria timeout
- Python pode fazer streaming/chunks eficientemente
```

### Exemplo 3: Debugando ExpressêÂµes

```
VocêÂª: Minha expressêÂ£o nêÂ£o estêÂ¡ funcionando: {{ $json.email }}
      O webhook envia {"body": {"email": "test@example.com"}}

Claude: [Usa n8n-expression-syntax/COMMON_MISTAKES.md]

Encontrei o problema! Dados do webhook estêÂ£o aninhados em `body`.

ê¢ÂÅ Errado: {{ $json.email }}
ê¢Åâ¦ Correto: {{ $json.body.email }}

O node de webhook encapsula o payload:
{
  "headers": {...},
  "body": {           ê¢â Â Seus dados estêÂ£o aqui
    "email": "test@example.com"
  }
}
```

### Exemplo 4: ProntidêÂ£o para ProduêÂ§êÂ£o

```
VocêÂª: Estou prestes a implantar meu workflow de webhook do Stripe. O que devo verificar?

Claude: [Usa n8n-workflow-architect/production-readiness.md]

Checklist prêÂ©-implantaêÂ§êÂ£o para webhooks de pagamento:

ê¢âÂ¡ SeguranêÂ§a
  - Verificar assinaturas de webhook do Stripe (node Code)
  - Rejeitar assinaturas invêÂ¡lidas imediatamente

ê¢âÂ¡ IdempotêÂªncia
  - Armazenar IDs de eventos processados
  - Verificar antes de processar: SELECT 1 FROM processed_events WHERE event_id = $1
  - Pular se jêÂ¡ processado

ê¢âÂ¡ Tratamento de Erros
  - Workflow de Error Trigger ê¢â â Slack #alerts
  - Registrar todas as falhas com contexto

ê¢âÂ¡ Tempo de Resposta
  - Usar responseMode: "onReceived" (confirmar para o Stripe imediatamente)
  - Processar de forma assêÂ­ncrona (Stripe tenta novamente em respostas lentas)

ê¢âÂ¡ Testes
  - Usar modo de teste do Stripe
  - Verificar com Stripe CLI: stripe trigger payment_intent.succeeded

Quer que eu adicione esses padrêÂµes ao seu workflow?
```

---

## Arquitetura

```
ê¢âÅê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢âÂ
ê¢ââ                         REQUISIêâ¡êÆO DO USUêÂRIO                            ê¢ââ
ê¢ââ         "Preciso automatizar X com Shopify, HubSpot e IA"               ê¢ââ
ê¢ââê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢âË
                                    ê¢ââ
                                    ê¢âÂ¼
ê¢âÅê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢âÂ
ê¢ââ                      CAMADA DE PLANEJAMENTO                              ê¢ââ
ê¢ââ  ê¢âÅê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢âÂ  ê¢ââ
ê¢ââ  ê¢ââ                    n8n-workflow-architect                          ê¢ââ  ê¢ââ
ê¢ââ  ê¢ââ  ê¢â¬Â¢ Analisar stack de negêÂ³cios (Shopify, Zoho, HubSpot, etc.)      ê¢ââ  ê¢ââ
ê¢ââ  ê¢ââ  ê¢â¬Â¢ Decidir: n8n vs Python vs HêÂ­brido                               ê¢ââ  ê¢ââ
ê¢ââ  ê¢ââ  ê¢â¬Â¢ Avaliar requisitos de prontidêÂ£o para produêÂ§êÂ£o                   ê¢ââ  ê¢ââ
ê¢ââ  ê¢ââê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢âË  ê¢ââ
ê¢ââê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢âË
                                    ê¢ââ
                    ê¢âÅê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢âÂ¼ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢âÂ
                    ê¢âÂ¼               ê¢âÂ¼               ê¢âÂ¼
ê¢âÅê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢âÂ
ê¢ââ                    CAMADA DE IMPLEMENTAêâ¡êÆO                               ê¢ââ
ê¢ââ  ê¢âÅê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢âÂ ê¢âÅê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢âÂ ê¢âÅê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢âÂ  ê¢ââ
ê¢ââ  ê¢ââ n8n-workflow-       ê¢ââ ê¢ââ n8n-node-           ê¢ââ ê¢ââ n8n-mcp-tools-    ê¢ââ  ê¢ââ
ê¢ââ  ê¢ââ patterns            ê¢ââ ê¢ââ configuration       ê¢ââ ê¢ââ expert            ê¢ââ  ê¢ââ
ê¢ââ  ê¢ââ                     ê¢ââ ê¢ââ                     ê¢ââ ê¢ââ                   ê¢ââ  ê¢ââ
ê¢ââ  ê¢ââ ê¢â¬Â¢ Processam. webhookê¢ââ ê¢ââ ê¢â¬Â¢ Config. de nodes  ê¢ââ ê¢ââ ê¢â¬Â¢ SeleêÂ§êÂ£o de tool ê¢ââ  ê¢ââ
ê¢ââ  ê¢ââ ê¢â¬Â¢ IntegraêÂ§êÂ£o API    ê¢ââ ê¢ââ ê¢â¬Â¢ Depend. de props  ê¢ââ ê¢ââ ê¢â¬Â¢ Ajuda parêÂ¢metrosê¢ââ  ê¢ââ
ê¢ââ  ê¢ââ ê¢â¬Â¢ Ops de banco      ê¢ââ ê¢ââ ê¢â¬Â¢ Config. de auth   ê¢ââ ê¢ââ ê¢â¬Â¢ PadrêÂµes MCP     ê¢ââ  ê¢ââ
ê¢ââ  ê¢ââ ê¢â¬Â¢ Workflows IA      ê¢ââ ê¢ââ ê¢â¬Â¢ Config. operaêÂ§êÂ£o  ê¢ââ ê¢ââ                   ê¢ââ  ê¢ââ
ê¢ââ  ê¢ââ ê¢â¬Â¢ Tarefas agendadas ê¢ââ ê¢ââ                     ê¢ââ ê¢ââ                   ê¢ââ  ê¢ââ
ê¢ââ  ê¢ââê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢âË ê¢ââê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢âË ê¢ââê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢âË  ê¢ââ
ê¢ââê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢âË
                                    ê¢ââ
                    ê¢âÅê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢âÂ¼ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢âÂ
                    ê¢âÂ¼               ê¢âÂ¼               ê¢âÂ¼
ê¢âÅê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢âÂ
ê¢ââ                      CAMADA DE CêâDIGO E SINTAXE                          ê¢ââ
ê¢ââ  ê¢âÅê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢âÂ ê¢âÅê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢âÂ ê¢âÅê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢âÂ  ê¢ââ
ê¢ââ  ê¢ââ n8n-code-           ê¢ââ ê¢ââ n8n-code-           ê¢ââ ê¢ââ n8n-expression-   ê¢ââ  ê¢ââ
ê¢ââ  ê¢ââ javascript          ê¢ââ ê¢ââ python              ê¢ââ ê¢ââ syntax            ê¢ââ  ê¢ââ
ê¢ââ  ê¢ââ                     ê¢ââ ê¢ââ                     ê¢ââ ê¢ââ                   ê¢ââ  ê¢ââ
ê¢ââ  ê¢ââ ê¢â¬Â¢ $input/$json      ê¢ââ ê¢ââ ê¢â¬Â¢ _input/_json      ê¢ââ ê¢ââ ê¢â¬Â¢ sintaxe {{ }}   ê¢ââ  ê¢ââ
ê¢ââ  ê¢ââ ê¢â¬Â¢ uso de $helpers   ê¢ââ ê¢ââ ê¢â¬Â¢ Biblioteca padrêÂ£o ê¢ââ ê¢ââ ê¢â¬Â¢ acesso $json    ê¢ââ  ê¢ââ
ê¢ââ  ê¢ââ ê¢â¬Â¢ manejo DateTime   ê¢ââ ê¢ââ ê¢â¬Â¢ Limites Python    ê¢ââ ê¢ââ ê¢â¬Â¢ refs $node      ê¢ââ  ê¢ââ
ê¢ââ  ê¢ââê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢âË ê¢ââê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢âË ê¢ââê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢âË  ê¢ââ
ê¢ââê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢âË
                                    ê¢ââ
                                    ê¢âÂ¼
ê¢âÅê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢âÂ
ê¢ââ                      CAMADA DE VALIDAêâ¡êÆO                                 ê¢ââ
ê¢ââ  ê¢âÅê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢âÂ  ê¢ââ
ê¢ââ  ê¢ââ                    n8n-validation-expert                           ê¢ââ  ê¢ââ
ê¢ââ  ê¢ââ  ê¢â¬Â¢ Interpretar erros de validaêÂ§êÂ£o ê¢â¬Â¢ Corrigir problemas comuns      ê¢ââ  ê¢ââ
ê¢ââ  ê¢ââ  ê¢â¬Â¢ Perfis de validaêÂ§êÂ£o ê¢â¬Â¢ Checklist prêÂ©-implantaêÂ§êÂ£o                 ê¢ââ  ê¢ââ
ê¢ââ  ê¢ââê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢âË  ê¢ââ
ê¢ââê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢âË
                                    ê¢ââ
                                    ê¢âÂ¼
ê¢âÅê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢âÂ
ê¢ââ                         FERRAMENTAS n8n MCP                              ê¢ââ
ê¢ââ                                                                          ê¢ââ
ê¢ââ  Descoberta            Gerenc. Workflow        ValidaêÂ§êÂ£o                 ê¢ââ
ê¢ââ  ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬     ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬     ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬       ê¢ââ
ê¢ââ  ê¢â¬Â¢ search_nodes        ê¢â¬Â¢ n8n_create_workflow  ê¢â¬Â¢ validate_workflow        ê¢ââ
ê¢ââ  ê¢â¬Â¢ get_node_info       ê¢â¬Â¢ n8n_update_workflow  ê¢â¬Â¢ validate_node_operation  ê¢ââ
ê¢ââ  ê¢â¬Â¢ list_nodes          ê¢â¬Â¢ n8n_get_workflow     ê¢â¬Â¢ validate_expressions     ê¢ââ
ê¢ââ  ê¢â¬Â¢ list_ai_tools       ê¢â¬Â¢ n8n_list_workflows   ê¢â¬Â¢ validate_connections     ê¢ââ
ê¢ââê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢ââ¬ê¢âË
```

---

## As 8 Skills

| Skill | PropêÂ³sito | DecisêÂ£o Chave |
|-------|-----------|---------------|
| **n8n-workflow-architect** | Planejamento estratêÂ©gico | "Devo usar n8n ou Python?" |
| **n8n-workflow-patterns** | PadrêÂµes de implementaêÂ§êÂ£o | "Qual êÂ© o padrêÂ£o certo para webhooks?" |
| **n8n-node-configuration** | ConfiguraêÂ§êÂ£o de nodes | "Quais campos esse node precisa?" |
| **n8n-mcp-tools-expert** | OrientaêÂ§êÂ£o MCP | "Qual ferramenta MCP devo usar?" |
| **n8n-code-javascript** | Nodes Code em JS | "Como acesso $json no Code?" |
| **n8n-code-python** | Nodes Code em Python | "Quais mêÂ³dulos Python estêÂ£o disponêÂ­veis?" |
| **n8n-expression-syntax** | Debug de expressêÂµes | "Por que minha expressêÂ£o nêÂ£o funciona?" |
| **n8n-validation-expert** | CorreêÂ§êÂ£o de erros | "O que esse erro de validaêÂ§êÂ£o significa?" |

### Detalhes das Skills

<details>
<summary><strong>n8n-workflow-architect</strong> - Planejamento estratêÂ©gico</summary>

**Quando o Claude usa isso:**
- Iniciando um novo projeto de automaêÂ§êÂ£o
- Decidindo entre n8n, Python ou hêÂ­brido
- Avaliando prontidêÂ£o para produêÂ§êÂ£o

**Arquivos principais:**
- `SKILL.md` - Framework de decisêÂ£o
- `tool-selection-matrix.md` - CritêÂ©rios n8n vs Python (OAuth, volume, complexidade)
- `business-stack-analysis.md` - Guias de compatibilidade SaaS
- `production-readiness.md` - Checklist prêÂ©-lanêÂ§amento

**CritêÂ©rios de decisêÂ£o:**
| Use n8n quando | Use Python quando |
|----------------|-------------------|
| OAuth necessêÂ¡rio | >5.000 registros |
| Mantenedores nêÂ£o-têÂ©cnicos | >20MB arquivos |
| Esperas de vêÂ¡rios dias | Algoritmos complexos |
| IntegraêÂ§êÂµes padrêÂ£o | IA de ponta |

</details>

<details>
<summary><strong>n8n-workflow-patterns</strong> - PadrêÂµes de implementaêÂ§êÂ£o</summary>

**Os 5 padrêÂµes principais:**

1. **Processamento de Webhook** - Receber HTTP ê¢â â Processar ê¢â â Responder
   - Webhooks do Stripe, envios de formulêÂ¡rio, integraêÂ§êÂµes de chat

2. **IntegraêÂ§êÂ£o de API HTTP** - Buscar APIs ê¢â â Transformar ê¢â â Armazenar
   - SincronizaêÂ§êÂ£o de dados, agregaêÂ§êÂ£o de API, enriquecimento

3. **OperaêÂ§êÂµes de Banco de Dados** - Ler/Escrever/Sincronizar bancos
   - ETL, migraêÂ§êÂµes, backups

4. **Workflow de Agente IA** - IA com ferramentas e memêÂ³ria
   - Chatbots, geraêÂ§êÂ£o de conteêÂºdo, anêÂ¡lise

5. **Tarefas Agendadas** - AutomaêÂ§êÂ£o recorrente
   - RelatêÂ³rios diêÂ¡rios, limpeza, monitoramento

</details>

<details>
<summary><strong>n8n-node-configuration</strong> - ConfiguraêÂ§êÂ£o de nodes</summary>

**Conceitos principais:**
- **Consciente de operaêÂ§êÂ£o:** OperaêÂ§êÂµes diferentes precisam de campos diferentes
- **DependêÂªncias de propriedade:** Campos mostram/escondem baseado em outros valores
- **Descoberta progressiva:** Comece com essenciais, adicione complexidade

**Exemplo:** Node do Slack
```javascript
// Para operation='post' (enviar mensagem)
{ resource: "message", operation: "post", channel: "#general", text: "Hello!" }

// Para operation='update' (editar mensagem) - campos diferentes!
{ resource: "message", operation: "update", messageId: "123", text: "Updated!" }
```

</details>

<details>
<summary><strong>n8n-code-javascript</strong> - Nodes Code em JS</summary>

**Sintaxe principal:**
```javascript
// Acessar dados de entrada
const items = $input.all();
const firstItem = $json;

// Referenciar outros nodes
const prevData = $node["Previous Node"].json;

// RequisiêÂ§êÂµes HTTP (embutido)
const response = await $helpers.httpRequest({
  method: 'GET',
  url: 'https://api.example.com/data'
});

// DateTime (Luxon)
const now = DateTime.now();
const formatted = now.toFormat('yyyy-MM-dd');
```

</details>

<details>
<summary><strong>n8n-expression-syntax</strong> - Debug de expressêÂµes</summary>

**Erros comuns:**

| Errado | Correto | Por quêÂª |
|--------|---------|---------|
| `{{ $json.email }}` | `{{ $json.body.email }}` | Dados do webhook estêÂ£o em `.body` |
| `{{ json.field }}` | `{{ $json.field }}` | Faltando prefixo `$` |
| `$json.field` | `{{ $json.field }}` | Faltando `{{ }}` |

**PadrêÂµes êÂºteis:**
```javascript
// Condicional
{{ $json.status === 'active' ? 'Sim' : 'NêÂ£o' }}

// Valor padrêÂ£o
{{ $json.name || 'Desconhecido' }}

// Referenciar outros nodes
{{ $node["Extract Data"].json.email }}
```

</details>

---

## Estrutura de Arquivos

```
n8n-ps/
ê¢âÅê¢ââ¬ê¢ââ¬ README.md                          # Este arquivo (portuguêÂªs)
ê¢âÅê¢ââ¬ê¢ââ¬ README-EN.md                       # VersêÂ£o em inglêÂªs
ê¢âÅê¢ââ¬ê¢ââ¬ INSTALL.md                         # Guia de instalaêÂ§êÂ£o (portuguêÂªs)
ê¢âÅê¢ââ¬ê¢ââ¬ INSTALL-EN.md                      # Guia de instalaêÂ§êÂ£o (inglêÂªs)
ê¢âÅê¢ââ¬ê¢ââ¬ docs-pt/                           # DocumentaêÂ§êÂ£o detalhada em portuguêÂªs
ê¢âÅê¢ââ¬ê¢ââ¬ examples/
ê¢ââ   ê¢ââê¢ââ¬ê¢ââ¬ README.md                      # Prompts de exemplo
ê¢ââê¢ââ¬ê¢ââ¬ .claude/
    ê¢âÅê¢ââ¬ê¢ââ¬ CLAUDE.md                      # ConfiguraêÂ§êÂ£o principal
    ê¢ââê¢ââ¬ê¢ââ¬ skills/
        ê¢âÅê¢ââ¬ê¢ââ¬ n8n-workflow-architect/    # 4 arquivos - Planejamento
        ê¢âÅê¢ââ¬ê¢ââ¬ n8n-workflow-patterns/     # 6 arquivos - PadrêÂµes
        ê¢âÅê¢ââ¬ê¢ââ¬ n8n-node-configuration/    # 4 arquivos - Config. de nodes
        ê¢âÅê¢ââ¬ê¢ââ¬ n8n-mcp-tools-expert/      # 5 arquivos - OrientaêÂ§êÂ£o MCP
        ê¢âÅê¢ââ¬ê¢ââ¬ n8n-code-javascript/       # 6 arquivos - CêÂ³digo JS
        ê¢âÅê¢ââ¬ê¢ââ¬ n8n-code-python/           # 6 arquivos - CêÂ³digo Python
        ê¢âÅê¢ââ¬ê¢ââ¬ n8n-expression-syntax/     # 4 arquivos - ExpressêÂµes
        ê¢ââê¢ââ¬ê¢ââ¬ n8n-validation-expert/     # 4 arquivos - ValidaêÂ§êÂ£o
```

**Total:** 46 arquivos, ~25.000 palavras de expertise n8n

---

## Perguntas Frequentes

### Preciso do n8n Cloud ou posso usar self-hosted?

Ambos funcionam. Apenas mude `N8N_API_URL` para a URL da sua instêÂ¢ncia.

### Isso funciona com a EdiêÂ§êÂ£o Community do n8n?

Sim! VocêÂª precisa ter acesso êÂ  API habilitado. Nas variêÂ¡veis de ambiente do seu n8n:
```
N8N_PUBLIC_API_ENABLED=true
```

### O Claude pode ativar workflows?

NêÂ£o. A API do n8n nêÂ£o suporta ativaêÂ§êÂ£o. O Claude vai criar o workflow e dizer para vocêÂª ativêÂ¡-lo na UI.

### E se o Claude cometer um erro?

Workflows sêÂ£o criados inativos. Sempre revise antes de ativar. O Claude tambêÂ©m valida antes de criar.

### Como isso êÂ© diferente dos recursos de IA do n8n?

O n8n tem IA embutida para gerar workflows. O n8n Powerhouse dêÂ¡ ao Claude **expertise profunda** mais **acesso direto êÂ  API**. O Claude pode:
- Tomar decisêÂµes de arquitetura (n8n vs Python)
- Aplicar padrêÂµes de produêÂ§êÂ£o (idempotêÂªncia, tratamento de erros)
- Debugar problemas complexos
- Criar workflows que seguem boas prêÂ¡ticas

### Posso adicionar minhas prêÂ³prias skills?

Sim! Adicione arquivos `.md` em `.claude/skills/nome-da-sua-skill/` e atualize `.claude/CLAUDE.md`.

---

## ReferêÂªncia das Ferramentas MCP

<details>
<summary><strong>Ferramentas de Descoberta</strong></summary>

```bash
search_nodes          # Encontrar nodes por palavra-chave
get_node_essentials   # VisêÂ£o rêÂ¡pida do node (comece aqui)
get_node_info         # DocumentaêÂ§êÂ£o completa
list_nodes            # Listar por categoria/pacote
list_ai_tools         # Nodes com capacidade de IA
```

</details>

<details>
<summary><strong>Gerenciamento de Workflow</strong></summary>

```bash
n8n_create_workflow          # Criar novo workflow
n8n_get_workflow             # Obter por ID
n8n_update_partial_workflow  # AtualizaêÂ§êÂµes incrementais (add/remove nodes)
n8n_update_full_workflow     # SubstituiêÂ§êÂ£o completa
n8n_list_workflows           # Listar todos workflows
n8n_delete_workflow          # Deletar workflow
```

</details>

<details>
<summary><strong>Ferramentas de ValidaêÂ§êÂ£o</strong></summary>

```bash
validate_workflow             # ValidaêÂ§êÂ£o completa do workflow
validate_node_operation       # ValidaêÂ§êÂ£o de node êÂºnico
validate_workflow_connections # Verificar apenas conexêÂµes
validate_workflow_expressions # Verificar apenas expressêÂµes
n8n_validate_workflow         # Validar por ID do workflow
```

</details>

<details>
<summary><strong>Ferramentas de Template</strong></summary>

```bash
search_templates       # Pesquisar por palavra-chave
list_node_templates    # Encontrar templates usando nodes especêÂ­ficos
get_template           # Obter JSON completo do workflow
get_templates_for_task # Templates curados por tipo de tarefa
```

</details>

<details>
<summary><strong>Ferramentas de ExecuêÂ§êÂ£o</strong></summary>

```bash
n8n_trigger_webhook_workflow  # Disparar via webhook
n8n_list_executions           # HistêÂ³rico de execuêÂ§êÂµes
n8n_get_execution             # Detalhes da execuêÂ§êÂ£o
n8n_health_check              # Verificar conectividade do n8n
```

</details>

---

## ProntidêÂ£o para ProduêÂ§êÂ£o

As skills incluem orientaêÂ§êÂ£o de produêÂ§êÂ£o para:

| êÂrea | Cobertura |
|------|-----------|
| **Observabilidade** | Workflows de erro, log de execuêÂ§êÂ£o, health checks |
| **IdempotêÂªncia** | Tratamento de duplicatas, verificar-antes-criar, chaves de idempotêÂªncia |
| **GestêÂ£o de Custos** | Custos de API de IA, cache, seleêÂ§êÂ£o de modelo |
| **Controle Operacional** | Kill switches, filas de aprovaêÂ§êÂ£o, trilhas de auditoria |
| **SeguranêÂ§a** | Assinaturas de webhook, tratamento de credenciais, validaêÂ§êÂ£o de entrada |

Veja [production-readiness.md](.claude/skills/n8n-workflow-architect/production-readiness.md) para o checklist completo.

---

## Contribuindo

1. FaêÂ§a fork deste repositêÂ³rio
2. Adicione/edite arquivos em `.claude/skills/`
3. Atualize descriêÂ§êÂµes de skills em `.claude/CLAUDE.md`
4. Envie um PR

### Estrutura de Skill

Cada skill precisa de:
- `SKILL.md` - Arquivo principal (carregado quando a skill êÂ© invocada)
- `README.md` - VisêÂ£o geral legêÂ­vel por humanos
- Arquivos `.md` adicionais para têÂ³picos detalhados

---

## Links

- [DocumentaêÂ§êÂ£o do n8n](https://docs.n8n.io/)
- [n8n MCP no npm](https://www.npmjs.com/package/n8n-mcp)
- [Claude Code](https://claude.ai/claude-code)
- [DocumentaêÂ§êÂ£o de Skills do Claude Code](https://docs.anthropic.com/en/docs/claude-code/skills)
- [Model Context Protocol](https://modelcontextprotocol.io/)

---

## LicenêÂ§a

LicenêÂ§a MIT - Use livremente para seus projetos de automaêÂ§êÂ£o.

---

<p align="center">
  <strong>ConstruêÂ­do com Claude Code + n8n MCP</strong><br>
  <em>Transforme conversas em automaêÂ§êÂ£o pronta para produêÂ§êÂ£o</em>
</p>

---

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="32" />
  <p><strong>Arckhé AI</strong></p>
</div>