# Matriz de Seleçêo de Ferramenta

Critérios detalhados de decisêo para escolher entre n8n, Python ou abordagens híbridas.

---

## A Pergunta Fundamental

Antes de escrever uma única linha de código ou arrastar um único node:

> **Qual ferramenta é apropriada para este problema específico, e quem vai mantê-lo?**

---

## Matriz de Decisêo

### Complexidade de Autenticaçêo

| Cenário | Ferramenta Recomendada | Justificativa |
|---------|------------------------|---------------|
| API key simples | Qualquer uma | Trivial de qualquer forma |
| OAuth 2.0 (Google, Slack, HubSpot) | **n8n** | Ciclo de vida de tokens gerenciado, tratamento de refresh |
| Implementaçêo OAuth customizada | Python | Controle total necessário |
| OAuth multi-tenant | Híbrido | n8n por tenant, Python para gerenciamento |

**A Verificaçêo de Realidade do OAuth:**
- URLs de redirect
- Códigos de autorizaçêo
- Access tokens
- Refresh tokens
- Expiraçêo de tokens
- Armazenamento seguro
- Tratamento de rotaçêo

O n8n lida com TUDO isso. Implementações Python frequentemente armazenam tokens em texto puro.

---

### Avaliaçêo de Manutenibilidade

| Equipe de Manutençêo | Ferramenta Recomendada | Por quê |
|---------------------|------------------------|---------|
| Usuários de negócio nêo-técnicos | **n8n** | Visual = auto-documentado |
| Misto técnico/nêo-técnico | **Híbrido** | n8n para UI, Python para lógica |
| Equipe dev dedicada | Qualquer uma | Escolha baseado em outros fatores |
| Dev solo, handoff futuro desconhecido | **n8n** | Menor barreira para sucessor |
| Rotaçêo de terceirizados/offshore | **n8n** | Reduz tempo de ramp-up |

**O Teste do Ônibus:**
> "Se eu for atropelado por um ônibus, alguém consegue entender isso em um dia?"

---

### Duraçêo do Processo

| Duraçêo do Processo | Ferramenta Recomendada | Implementaçêo |
|--------------------|------------------------|---------------|
| Segundos a minutos | Qualquer uma | Execuçêo padrêo |
| Horas | **n8n** | Node Wait |
| Dias a semanas | **n8n** | Node Wait com retomada |
| Aprovaçêo humana necessária | **n8n** | Padrêo Webhook + Wait |
| Máquina de estados complexa | Híbrido | Orquestraçêo n8n, estado no DB |

**Por que Espera Importa:**

"Espera" em Python:
```python
# Opçêo A: Servidor fica rodando (caro)
time.sleep(259200)  # 3 dias

# Opçêo B: Gerenciamento de estado complexo
# - Salvar estado no banco de dados
# - Configurar agendador
# - Reconstruir contexto na retomada
# - Tratar casos de borda
```

Espera em n8n:
```
[Trigger] → [Processar] → [Wait 3 dias] → [Continuar]
```

---

### Limites de Volume de Dados

| Característica de Dados | Limite | Ferramenta Recomendada |
|------------------------|--------|------------------------|
| Registros por execuçêo | < 5.000 | n8n |
| Registros por execuçêo | > 5.000 | **Python** |
| Tamanho de arquivo | < 20 MB | n8n |
| Tamanho de arquivo | > 20 MB | **Python** |
| Processamento em memória | < 500 MB | n8n (com cautela) |
| Processamento em memória | > 500 MB | **Python** |
| Streaming necessário | Sim | **Python** |
| Processamento em lote | Lotes grandes | **Python** |

**Prevençêo de Crash de Memória:**

n8n roda em Node.js com limites de memória padrêo. Estas operações vêo crashar:
- Carregar PDF de 50MB na memória
- Iterar 10.000 linhas mantendo todas em memória
- Processar arquivos de vídeo
- Payloads JSON grandes

Soluções Python:
- `pandas` com leitura em chunks
- Streaming baseado em generators
- Arquivos mapeados em memória
- Garbage collection explícito

---

### Complexidade de Lógica

| Indicador de Complexidade | Limite | Ferramenta Recomendada |
|--------------------------|--------|------------------------|
| Branches condicionais | 1-2 | n8n IF/Switch |
| Branches condicionais | 3-4 | Bloco de código no n8n |
| Branches condicionais | 5+ | **Python** |
| Condicionais aninhados | Qualquer | **Python** |
| Processamento algorítmico | Qualquer | **Python** |
| Matching fuzzy | Complexo | **Python** |
| Transformações matemáticas | Complexas | **Python** |
| Acumulaçêo de estado em loops | Sim | **Python** |

**O Teto de Complexidade Visual:**

Você ultrapassou quando:
- O canvas parece espaguete
- Linhas cruzando por todo lado
- Nodes empilhados incompreensivelmente
- Precisa dar zoom out para ver a estrutura
- Nêo consegue ler labels dos nodes no zoom utilizável

**O Teste das 20 Linhas:**
> "Essa lógica pode ser expressa em 20 linhas de código legível?"
> Se sim → Use um node Code
> Se precisaria de 50+ nodes → Definitivamente use código

---

### Requisitos de Inovaçêo

| Requisito | Ferramenta Recomendada |
|-----------|------------------------|
| Integrações SaaS padrêo | n8n |
| Bibliotecas de IA recentes (< 6 meses) | **Python** |
| Frameworks experimentais | **Python** |
| GraphRAG, padrões RAG avançados | **Python** |
| Modelos ML customizados | **Python** |
| APIs estáveis e bem documentadas | Qualquer uma |

**A Realidade do Atraso:**
A equipe n8n precisa avaliar → integrar → testar → documentar antes de novas bibliotecas aparecerem como nodes.

Se você precisa de algo lançado no mês passado → use Python.

---

## Padrões de Arquitetura Híbrida

### Padrêo 1: Orquestraçêo n8n + Microsserviço Python

```
┌──────────────────────────────────────────────────┐
│                    Camada n8n                     │
│  ┌─────────┐   ┌─────────┐   ┌─────────┐        │
│  │ Webhook │ → │ HTTP    │ → │ Slack   │        │
│  │ Trigger │   │ Request │   │ Notify  │        │
│  └─────────┘   └────┬────┘   └─────────┘        │
│                     │                            │
└─────────────────────┼────────────────────────────┘
                      │ Chamada API
                      ▼
┌──────────────────────────────────────────────────┐
│               Microsserviço Python                │
│  ┌─────────────────────────────────────────────┐ │
│  │ • Processamento de dados complexo           │ │
│  │ • Operações de IA/ML                        │ │
│  │ • Computaçêo pesada                         │ │
│  │ • Retorna resultado JSON                    │ │
│  └─────────────────────────────────────────────┘ │
└──────────────────────────────────────────────────┘
```

**Use quando**: Precisa de capacidades Python mas quer integrações do n8n

### Padrêo 2: Nodes Code no n8n

```
┌──────────────────────────────────────────────────┐
│                    Workflow n8n                   │
│                                                   │
│  ┌─────────┐   ┌─────────┐   ┌─────────┐        │
│  │ Trigger │ → │ Code    │ → │ Output  │        │
│  │         │   │ (JS/Py) │   │ Node    │        │
│  └─────────┘   └─────────┘   └─────────┘        │
│                                                   │
└──────────────────────────────────────────────────┘
```

**Use quando**: Lógica é complexa mas contida, sem serviço externo necessário

### Padrêo 3: Handoff Orientado a Eventos

```
Workflow n8n A             Serviço Python            Workflow n8n B
┌───────────────┐          ┌───────────────┐          ┌───────────────┐
│ Trigger       │          │               │          │ Webhook       │
│ → Validar     │  ──────► │ Processar     │ ──────►  │ → Transformar │
│ → Enfileirar  │          │ → Computar    │          │ → Notificar   │
└───────────────┘          │ → Callback    │          └───────────────┘
                           └───────────────┘
```

**Use quando**: Processos Python de longa duraçêo, padrões assíncronos

---

## Fluxograma de Decisêo

```
                    INÍCIO
                      │
                      ▼
              ┌───────────────┐
              │ OAuth necess.?│
              └───────┬───────┘
                 Sim  │  Nêo
          ┌───────────┴───────────┐
          ▼                       ▼
    Use n8n para auth      ┌───────────────┐
          │               │ > 5000 registros│
          │               │ ou > 20MB arq.? │
          │               └───────┬───────┘
          │                  Sim  │  Nêo
          │           ┌───────────┴───────────┐
          │           ▼                       ▼
          │     Use Python para          ┌───────────────┐
          │     processamento            │ > 20 nodes de │
          │           │                  │ lógica negócio│
          │           │                  └───────┬───────┘
          │           │                    Sim  │  Nêo
          │           │             ┌───────────┴───────────┐
          │           │             ▼                       ▼
          │           │       Use nodes Code          ┌───────────────┐
          │           │       no n8n                  │ Mantenedores  │
          │           │             │                 │ nêo-técnicos? │
          │           │             │                 └───────┬───────┘
          │           │             │                    Sim  │  Nêo
          │           │             │             ┌───────────┴───────────┐
          │           │             │             ▼                       ▼
          │           │             │        Use n8n               Use qualquer
          │           │             │             │                 (preferência)
          │           │             │             │                       │
          └───────────┴─────────────┴─────────────┴───────────────────────┘
                                          │
                                          ▼
                                   IMPLEMENTAÇêO
```

---

## Anti-Padrões a Evitar

### 1. "n8n Pode Fazer Tudo"
**Realidade**: Workflows visuais têm limites. Forçar lógica complexa cria espaguete impossível de manter.

### 2. "Python É Sempre Melhor"
**Realidade**: Python requer mais infraestrutura, handoff mais difícil, reinventa rodas de OAuth.

### 3. "Vamos Otimizar Depois"
**Realidade**: Decisões de arquitetura se acumulam. Escolha errada de ferramenta no início = migraçêo dolorosa depois.

### 4. "Funciona nos Testes"
**Realidade**: Produçêo tem volume, casos de borda, falhas. Teste com dados realistas.

### 5. "A Demo Ficou Ótima"
**Realidade**: Demos mostram caminhos felizes. Produçêo precisa de tratamento de erros, monitoramento, recuperaçêo.

---

## Cartêo de Referência Rápida

| Fator | n8n | Python | Híbrido |
|-------|-----|--------|---------|
| Serviços OAuth | ✅ | ⚠️ | ✅ |
| Mantenedores nêo-técnicos | ✅ | ❌ | ⚠️ |
| Esperas de vários dias | ✅ | ⚠️ | ✅ |
| Dados grandes (5k+ linhas) | ❌ | ✅ | ✅ |
| Arquivos grandes (20MB+) | ❌ | ✅ | ✅ |
| Algoritmos complexos | ⚠️ | ✅ | ✅ |
| IA de ponta | ❌ | ✅ | ✅ |
| Integrações padrêo | ✅ | ⚠️ | ✅ |
| Prototipagem rápida | ✅ | ⚠️ | ⚠️ |
| Manutençêo longo prazo | ✅ | ⚠️ | ✅ |

**Legenda**: ✅ Recomendado | ⚠️ Possível com ressalvas | ❌ Nêo recomendado

---

## Skills Relacionadas

- **n8n-code-javascript** - Quando nodes Code sêo a resposta
- **n8n-code-python** - Para nodes Code Python
- **n8n-workflow-patterns** - Uma vez escolhida a ferramenta, escolha o padrêo certo
