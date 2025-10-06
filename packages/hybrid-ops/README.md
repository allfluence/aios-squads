# Hybrid-Ops Expansion Pack

**Versão**: 1.0.0
**Autor**: Pedro Valério
**Slash Prefix**: hybridOps
**Tipo**: Sistema META de Fábrica de Processos

---

## Visão Geral

Hybrid-Ops é um expansion pack de **Fábrica de Processos** que contém 9 agentes META que CRIAM e IMPLEMENTAM processos híbridos humano-agente, em vez de executá-los. Este pack resolve o problema fundamental de nomenclaturas conflitantes entre equipes de operações (que falam "tarefas/processos") e desenvolvedores de IA (que falam "agentes/workflows").

## Propósito

Este expansion pack conecta gerenciamento de processos operacionais com implementação de agentes de IA, fornecendo uma estrutura unificada que funciona tanto no ClickUp quanto em YAML para agentes de IA.

**Problemas Resolvidos:**

1. **Nomenclaturas Conflitantes** - Equipes de operações e desenvolvedores de IA usam linguagem diferente para os mesmos conceitos
2. **Processos Não-Executáveis** - Documentação de processos para humanos não se traduz em workflows executáveis por agentes
3. **Lacuna na Migração Humano→Agente** - Sem caminho claro para migrar progressivamente tarefas de execução humana para agente
4. **Falta de Quality Gates** - Sem validação formal antes de handoffs de tarefas, causando retrabalho
5. **Silos Operacionais** - Operações usa ClickUp, Dev usa YAML/código - não se comunicam

---

## Arquitetura: Processo de Criação em 9 Fases

O expansion pack hybrid-ops usa um **workflow sequencial de 9 fases** coordenado por 9 agentes META especializados:

```
Fase 1: Discovery & Mapeamento      → process-mapper
Fase 2: Arquitetura de Processo     → process-architect
Fase 3: Design de Executores        → executor-designer
Fase 4: Criação de Workflows        → workflow-designer
Fase 5: Definições de Tasks         → workflow-designer
Fase 6: Design de QA Gates          → qa-architect
Fase 7: Implementação ClickUp       → clickup-engineer
Fase 8: Geração de Agentes          → agent-generator
Fase 9: Compliance & Documentação   → compliance-validator + doc-generator
```

### Sequenciamento dos Agentes META

Cada agente META recebe output da fase anterior e passa para a próxima:

1. **process-mapper** → Captura estado atual, identifica oportunidades de automação
2. **process-architect** → Projeta estrutura do processo (fases, tasks, dependências)
3. **executor-designer** → Atribui executores (humano/agente/híbrido) com balanceamento de carga
4. **workflow-designer** → Cria workflows universais + definições completas de tasks
5. **qa-architect** → Projeta quality gates para handoffs críticos
6. **clickup-engineer** → Configura ClickUp com 20 custom fields AIOS-PM
7. **agent-generator** → Gera definições de agentes AIOS para agentes identificados
8. **compliance-validator** → Valida processo contra padrões AIOS-PM (escala de 100 pontos)
9. **doc-generator** → Gera suite completa de documentação

---

## Estrutura do Pack

```
expansion-packs/hybrid-ops/
├── agents/                          # 9 agentes META
│   ├── process-mapper.md
│   ├── process-architect.md
│   ├── executor-designer.md
│   ├── workflow-designer.md
│   ├── qa-architect.md
│   ├── clickup-engineer.md
│   ├── agent-generator.md
│   ├── compliance-validator.md
│   └── doc-generator.md
├── checklists/                      # Checklists de validação
│   ├── installation-checklist.md
│   ├── structure-validation-checklist.md
│   └── agent-review-checklist.md
├── config.yaml                      # Configuração do pack
├── data/                           # Knowledge bases
│   ├── aios-pm-compliance-checklist.md
│   └── aios-pm-kb.md
├── README.md                       # Este arquivo
├── tasks/                          # Tasks de orquestração (9 arquivos)
│   ├── discover-process.md
│   ├── design-architecture.md
│   ├── design-executors.md
│   ├── design-workflows.md
│   ├── create-task-definitions.md
│   ├── design-qa-gates.md
│   ├── implement-clickup.md
│   ├── generate-agents.md
│   └── validate-compliance.md
└── templates/                      # 10 templates YAML
    ├── process-discovery-tmpl.yaml
    ├── process-definition-tmpl.yaml
    ├── executor-definition-tmpl.yaml
    ├── workflow-tmpl.yaml
    ├── task-definition-tmpl.yaml
    ├── qa-gate-tmpl.yaml
    ├── clickup-config-tmpl.yaml
    ├── agent-definition-tmpl.yaml
    ├── compliance-report-tmpl.yaml
    └── process-readme-tmpl.yaml
```

---

## ⚙️ Por Que Não Há Diretório `workflows/`?

### Entendendo a Diferença: Workflows vs Tasks no AIOS

**Workflows (.yaml) - Core AIOS**
- Orquestração de ALTO NÍVEL para ciclo COMPLETO de projetos
- Guiam decisões: "Devo usar greenfield ou brownfield?"
- Contêm decision trees complexas
- Coordenam múltiplos agentes ao longo de TODO um projeto
- **Exemplo**: `.aios-core/workflows/greenfield-fullstack.yaml`
- **Usado por**: `@aios-master` e `@aios-orchestrator`

**Tasks (.md) - Expansion Packs**
- Roteiros de OPERAÇÕES ESPECÍFICAS executáveis
- Instruções passo-a-passo para domínios especializados
- Sequências lineares ou workflows de fase única
- **Exemplo**: `tasks/discover-process.md`
- **Usado por**: Agentes individuais durante seu trabalho

### Por Que Hybrid-Ops Não Precisa de `workflows/`

✅ **Estrutura Atual é CORRETA**

1. **Sequência Linear Única**
   - Hybrid-ops tem UMA abordagem: processo de 9 fases
   - Não há caminhos alternativos ou decision trees
   - Sempre: Fase 1 → Fase 2 → ... → Fase 9

2. **Padrão de Expansion Pack**
   - NENHUM expansion pack oficial tem `workflows/`
   - `expansion-creator`: ❌ Sem workflows/
   - `hybrid-ops`: ❌ Sem workflows/
   - Expansion packs focam em **domínios específicos**
   - Core AIOS foca em **ciclos de projeto**

3. **Tasks São Suficientes**
   - Cada task coordena uma fase específica
   - Orquestração acontece através dos 9 task files
   - Agentes executam tasks diretamente via comando

### Quando Você PRECISARIA de `workflows/`

Você só precisaria criar `workflows/` SE o hybrid-ops tivesse:

```yaml
# Cenário hipotético futuro com múltiplas abordagens:
workflows/
├── simple-process-creation.yaml    # 5 fases simplificadas
├── complex-process-creation.yaml   # 9 fases completas
└── migration-process.yaml          # Migrar processo existente
```

Com decision tree tipo:
```
"Seu processo tem mais de 20 tasks?"
├─ SIM → complex-process-creation.yaml
└─ NÃO → simple-process-creation.yaml
```

**Status atual v1.0.0**: Uma única abordagem = Tasks são suficientes ✅

### Comparação Visual

| Feature | Core AIOS | Hybrid-Ops |
|---------|-----------|------------|
| **Propósito** | Guiar PROJETOS completos | Criar PROCESSOS híbridos |
| **workflows/** | 6 arquivos (greenfield/brownfield) | 0 arquivos (não necessário) |
| **tasks/** | 15+ utility tasks | 9 phase tasks |
| **Decision Trees** | Sim (qual approach usar) | Não (sequência linear) |
| **Padrão** | Orquestração de projeto | Operação especializada |

---

## O Que Está Incluído

### 1. Tasks de Fase (9 arquivos)

Cada task corresponde a uma fase do processo de criação:

#### Fase 1: Discovery & Mapeamento
**`tasks/discover-process.md`**
- Captura estado atual e identifica oportunidades de automação
- Ativação: `@hybridOps:process-mapper *start-discovery`

#### Fase 2: Arquitetura de Processo
**`tasks/design-architecture.md`**
- Projeta estrutura de alto nível com fases, tasks, dependências
- Ativação: `@hybridOps:process-architect *start-architecture`

#### Fase 3: Design de Executores
**`tasks/design-executors.md`**
- Atribui tasks a executores humano/agente/híbrido com balanceamento de carga
- Ativação: `@hybridOps:executor-designer *start-executor-design`

#### Fase 4: Criação de Workflows
**`tasks/design-workflows.md`**
- Cria workflows universais executáveis por humanos E agentes
- Ativação: `@hybridOps:workflow-designer *start-workflow-design`

#### Fase 5: Definições de Tasks
**`tasks/create-task-definitions.md`**
- Gera definições completas de tasks com data contracts
- Ativação: `@hybridOps:workflow-designer *start-task-definitions`

#### Fase 6: Design de QA Gates
**`tasks/design-qa-gates.md`**
- Projeta quality gates de validação para handoffs críticos
- Ativação: `@hybridOps:qa-architect *start-qa-design`

#### Fase 7: Implementação ClickUp
**`tasks/implement-clickup.md`**
- Projeta configuração completa do ClickUp com 20 custom fields AIOS-PM
- Ativação: `@hybridOps:clickup-engineer *start-clickup-config`

#### Fase 8: Geração de Agentes
**`tasks/generate-agents.md`**
- Gera definições de agentes AIOS para agentes identificados na Fase 3
- Ativação: `@hybridOps:agent-generator *start-agent-generation`

#### Fase 9: Validação de Compliance
**`tasks/validate-compliance.md`**
- Valida processo completo contra padrões da metodologia AIOS-PM
- Ativação: `@hybridOps:compliance-validator *start-validation`

### 2. Agentes META (9 arquivos)

#### Fase 1: Discovery & Mapeamento
**`agents/process-mapper.md`** (346 linhas)
- Captura estado atual e identifica oportunidades de automação
- Comandos: `*discover-process`, `*map-current-state`, `*assess-automation-opportunities`
- Outputs: Documento de discovery, mapa de processo, avaliação de automação
- Ativação: `@hybridOps:process-mapper`

#### Fase 2: Arquitetura de Processo
**`agents/process-architect.md`** (460 linhas)
- Projeta estrutura de processo de alto nível com fases, tasks, dependências
- Comandos: `*design-process`, `*define-phases`, `*identify-tasks`, `*map-dependencies`
- Outputs: YAML de definição de processo, lista de tasks, grafo de dependências
- Ativação: `@hybridOps:process-architect`

#### Fase 3: Design de Executores
**`agents/executor-designer.md`** (542 linhas)
- Atribui tasks a executores humano/agente/híbrido com balanceamento de carga
- Comandos: `*design-executors`, `*assign-tasks`, `*balance-workload`, `*create-hybrid-executors`
- Outputs: Definições de executores, matriz de atribuição, matriz RACI, relatório de carga
- Ativação: `@hybridOps:executor-designer`

#### Fase 4 & 5: Workflow & Definição de Tasks
**`agents/workflow-designer.md`** (655 linhas)
- Cria workflows universais executáveis por humanos E agentes
- Gera definições completas de tasks com data contracts
- Comandos: `*create-workflow`, `*create-task-definitions`, `*design-data-contracts`, `*map-handoffs`
- Outputs: Arquivos de workflow (1 por task), YAML de definição de task, schemas de data contract
- Ativação: `@hybridOps:workflow-designer`

#### Fase 6: Design de QA Gates
**`agents/qa-architect.md`** (644 linhas)
- Projeta quality gates de validação para handoffs críticos
- Comandos: `*design-qa-gates`, `*create-validation-criteria`, `*configure-decision-logic`
- Outputs: Definições de QA gate, regras de validação, caminhos de escalação
- Ativação: `@hybridOps:qa-architect`

#### Fase 7: Implementação ClickUp
**`agents/clickup-engineer.md`**
- Projeta configuração completa do ClickUp com 20 custom fields AIOS-PM
- Comandos: `*design-clickup-config`, `*create-custom-fields`, `*configure-automations`, `*setup-views`
- Outputs: Guia de setup do ClickUp, configuração de custom fields, regras de automação
- Ativação: `@hybridOps:clickup-engineer`

#### Fase 8: Geração de Agentes
**`agents/agent-generator.md`** (879 linhas)
- Gera definições de agentes AIOS para agentes identificados na Fase 3
- Comandos: `*generate-agents`, `*create-agent`, `*define-agent-persona`, `*design-agent-commands`
- Outputs: Arquivos de definição de agentes AIOS (formato markdown)
- Ativação: `@hybridOps:agent-generator`

#### Fase 9: Validação de Compliance
**`agents/compliance-validator.md`** (733 linhas)
- Valida processo completo contra padrões da metodologia AIOS-PM
- Comandos: `*validate-process`, `*calculate-compliance-score`, `*create-action-plan`
- Outputs: Relatório de compliance (pontuação de 100 pontos), lista de issues críticos, plano de ação
- Ativação: `@hybridOps:compliance-validator`

#### Fase 9: Geração de Documentação
**`agents/doc-generator.md`** (580+ linhas)
- Gera suite completa de documentação para o processo
- Comandos: `*generate-documentation`, `*create-quick-start-guides`, `*generate-diagrams`, `*create-troubleshooting-guide`
- Outputs: README, guias de quick start, diagramas, docs de troubleshooting
- Ativação: `@hybridOps:doc-generator`

### 3. Templates (10 arquivos)

Todos os templates usam formato YAML com workflows de elicitação:

1. **`process-discovery-tmpl.yaml`** - Documentação de discovery da Fase 1
2. **`process-definition-tmpl.yaml`** - Definição de estrutura de processo da Fase 2
3. **`executor-definition-tmpl.yaml`** - Especificações de executor da Fase 3
4. **`workflow-tmpl.yaml`** - Instruções de workflow universal da Fase 4
5. **`task-definition-tmpl.yaml`** - Especificações completas de task com data contracts da Fase 5
6. **`qa-gate-tmpl.yaml`** - Configuração de quality gate da Fase 6
7. **`clickup-config-tmpl.yaml`** - Guia de implementação ClickUp da Fase 7
8. **`agent-definition-tmpl.yaml`** - Especificações de agente AIOS da Fase 8
9. **`compliance-report-tmpl.yaml`** - Relatório de validação de compliance da Fase 9
10. **`process-readme-tmpl.yaml`** - Geração de documentação da Fase 9

### 4. Data & Knowledge Base (2 arquivos)

**`data/aios-pm-compliance-checklist.md`** (584 linhas)
- Sistema de pontuação de compliance de 100 pontos
- 7 categorias de validação:
  - Estrutura de Processo (20 pontos)
  - Definições de Tasks (15 pontos - Crítico)
  - Executores (15 pontos - Crítico)
  - Data Contracts (15 pontos - Crítico)
  - QA Gates (10 pontos)
  - Configuração ClickUp (10 pontos)
  - Documentação (5 pontos)
- Limites de grade: Excelente (90-100%), Bom (75-89%), Aceitável (60-74%), Ruim (<60%)
- Níveis de severidade de issue: Crítico, Major, Minor
- Usado por: agente compliance-validator

**`data/aios-pm-kb.md`** (500+ linhas)
- Knowledge base abrangente da metodologia AIOS-PM
- Seções:
  - Fundamentos (Processo, Fase, Task, Executor, Workflow, Data Contract, QA Gate, Handoff)
  - Camadas de Arquitetura de Processo (6 camadas)
  - Padrões Arquiteturais (Linear, Paralelo, Condicional, Iterativo)
  - Design Patterns (Estrutura de Processo, Atribuição de Executor, Execução Híbrida, Data Contracts, QA Gates)
  - Best Practices (Do's e Don'ts com exemplos)
  - Padrões de Compliance
  - Guia de Troubleshooting
  - Guias de Integração (ClickUp, AIOS)
  - Glossário Completo
- Usado por: Todos os 9 agentes META como referência

### 5. Checklists de Validação (3 arquivos)

**`checklists/installation-checklist.md`**
- Processo de instalação passo-a-passo
- Validação de registro de agentes e tasks
- Verificação de estrutura de diretórios
- Critérios de sucesso

**`checklists/structure-validation-checklist.md`**
- Sistema de pontuação de compliance completo
- Validação de items críticos (50 pts), major (30 pts), minor (20 pts)
- Validação de cross-references
- Comandos de validação
- Meta: ≥95% compliance

**`checklists/agent-review-checklist.md`**
- Padrões de qualidade de agentes
- Validação de seções obrigatórias
- Validação específica por agente para todos os 9 agentes
- Sistema de pontuação de qualidade (100 pontos)
- Template de sign-off de revisão

---

## Começando

### Instalação

```bash
# Instalar expansion pack
npm run install:expansion hybrid-ops

# Ou manualmente
node tools/install-expansion-pack.js hybrid-ops
```

### Quick Start: Crie Seu Primeiro Processo Híbrido

1. **Ativar a fase de discovery**:
```
@hybridOps:process-mapper *start-discovery
```

2. **Seguir o workflow guiado de 9 fases**:
   - Fase 1: Discovery com process-mapper
   - Fase 2: Arquitetura com process-architect
   - Fase 3: Design de executores com executor-designer
   - Fase 4-5: Workflows & tasks com workflow-designer
   - Fase 6: QA gates com qa-architect
   - Fase 7: Setup ClickUp com clickup-engineer
   - Fase 8: Geração de agentes com agent-generator
   - Fase 9: Validação de compliance & documentação

3. **Estrutura de output**:
```
output/processes/{process_id}/
├── discovery.md                      # Fase 1
├── process-definition.yaml           # Fase 2
├── executors/                        # Fase 3
│   ├── executor-1.md
│   └── executor-2.md
├── workflows/                        # Fase 4
│   ├── task-1.md
│   └── task-2.md
├── tasks/                           # Fase 5
│   └── task-definitions.yaml
├── qa-gates/                        # Fase 6
│   └── gate-definitions.yaml
├── clickup/                         # Fase 7
│   └── clickup-setup-guide.md
├── agents/                          # Fase 8
│   └── agent-1.md
├── compliance-report.md             # Fase 9
└── docs/                           # Fase 9
    ├── README.md
    ├── QUICKSTART-HUMAN.md
    ├── QUICKSTART-AGENT.md
    ├── QUICKSTART-MANAGER.md
    └── TROUBLESHOOTING.md
```

---

## Exemplos de Uso

### Exemplo 1: Criar Processo de Onboarding de Cliente

```
Usuário: Crie um processo híbrido para onboarding de cliente

Agente: Vou usar o workflow de criação de processo híbrido

@hybridOps:process-mapper *discover-process

[Elicitação interativa segue para todas as 9 fases]

Output Final:
- 5 fases definidas (Coleta de Dados → Validação → Config Sistema → Boas-vindas → Handoff)
- 23 tasks atribuídas a 4 executores (3 humanos, 1 agente)
- 2 QA gates em handoffs críticos
- Configuração completa do ClickUp com 20 custom fields
- 1 agente de validação gerado
- 94% compliance score (Excelente - Pronto para Produção)
- Suite completa de documentação
```

### Exemplo 2: Migrar Processo Existente para Híbrido

```
Usuário: Tenho um processo manual no ClickUp. Ajude-me a migrá-lo para execução híbrida.

Agente: Vou mapear seu processo existente e identificar oportunidades de automação.

@hybridOps:process-mapper *map-current-state
@hybridOps:process-mapper *assess-automation-opportunities

[Mapeamento de processo identifica 8 tasks adequadas para automação por agente]

Agente: Encontrei 8 tasks com potencial de automação ALTO. Vamos redesenhar com executores híbridos.

@hybridOps:executor-designer *create-hybrid-executors

[Cria executores agente-primário, humano-fallback para essas 8 tasks]
[Processo continua por todas as 9 fases]
```

### Exemplo 3: Validar Compliance de Processo

```
Usuário: Verifique se nosso processo atende aos padrões AIOS-PM

Agente: Vou executar validação de compliance.

@hybridOps:compliance-validator *validate-process

Compliance Score: 82/100 (Bom)

Issues Críticos: 0
Issues Major: 2
- Falta output schema em 1 task
- 2 tasks faltando quality checklists

Issues Minor: 3
- Gate recomendado após Fase 1
- Documentação incompleta

Recomendação: Corrigir 2 issues major antes do go-live.
```

---

## Funcionalidades Principais

### Metodologia AIOS-PM Unificada
- Estrutura única funciona no ClickUp (operacional) e YAML (executável por agente)
- Conceitos core: Executor, Task, Workflow, Data Contract, QA Gate, Handoff
- Caminho de migração progressiva de execução humano→híbrido→agente

### Suporte a Executor Híbrido
Três tipos de executor:
1. **Humano**: Execução tradicional de task
2. **Agente**: Execução totalmente automatizada
3. **Híbrido**: Agente-primário com humano-fallback (triggers de escalação, thresholds de confiança)

### Quality Gates
- Gates bloqueantes previnem propagação de dados ruins
- Gates de warning sinalizam preocupações para revisão
- Gates informacionais fornecem trilha de auditoria
- Matriz de decisão: PASS / CONCERNS / FAIL / WAIVED

### Data Contracts
- Schemas explícitos de input/output (formato JSON Schema)
- Mapeamentos de handoff com regras de transformação
- Validação antes de handoffs
- Verificações de type safety e compatibilidade de fields

### Workflows Universais
- Instruções executáveis por humanos E agentes
- Formato claro e passo-a-passo
- Sem linguagem específica de humano, sem código específico de agente
- Validação orientada por exemplos

### Sistema de Compliance de 100 Pontos
- 7 categorias de validação
- Categorias críticas requerem ≥85% (Tasks, Executores, Data Contracts)
- Mínimo de 90% overall para deploy em produção
- Validação automatizada com recomendações acionáveis

---

## Referência de Comandos

### Comandos Slash

Ativar agentes individuais META:
```
/hybridOps:process-mapper
/hybridOps:process-architect
/hybridOps:executor-designer
/hybridOps:workflow-designer
/hybridOps:qa-architect
/hybridOps:clickup-engineer
/hybridOps:agent-generator
/hybridOps:compliance-validator
/hybridOps:doc-generator
```

### Ativação de Agentes

```
@hybridOps:process-mapper
@hybridOps:process-architect
@hybridOps:executor-designer
@hybridOps:workflow-designer
@hybridOps:qa-architect
@hybridOps:clickup-engineer
@hybridOps:agent-generator
@hybridOps:compliance-validator
@hybridOps:doc-generator
```

### Comandos Comuns

```
*help                              # Mostrar capacidades do agente
*start-discovery                   # Fase 1: Discovery
*start-architecture                # Fase 2: Arquitetura
*start-executor-design             # Fase 3: Atribuição de executor
*start-workflow-design             # Fase 4: Criação de workflow
*start-task-definitions            # Fase 5: Definições de task
*start-qa-design                   # Fase 6: QA gates
*start-clickup-config              # Fase 7: Setup ClickUp
*start-agent-generation            # Fase 8: Geração de agente
*start-validation                  # Fase 9: Validação de compliance
*generate-documentation            # Fase 9: Documentação
```

---

## Usuários Alvo

### Primário: Implementadores de Processo-para-Agente
- Entende processos de negócio
- Familiarizado com ClickUp ou ferramentas similares
- Quer implementar IA mas não é desenvolvedor hardcore
- Precisa de documentação que funcione para humanos E agentes
- Nível: Intermediário

### Secundário: Tech Leads
- Desenvolvendo agentes de IA que se conectam com operações da empresa
- Precisam de integração estruturada com ferramentas operacionais
- Querem caminho de migração progressiva para automação
- Nível: Avançado

---

## Dependências

Este expansion pack requer:

- **Framework Core AIOS-FULLSTACK** (v4+)
- **Conta ClickUp** (para integração operacional)
- **Node.js 18+** (para ferramentas CLI)
- **GitHub CLI** (opcional, para workflows avançados)

---

## Best Practices

### Do's ✅
- Use o workflow completo de 9 fases para criação abrangente de processo
- Comece com discovery para entender estado atual
- Projete executores ANTES de workflows (saiba quem executa antes de definir como)
- Use executores híbridos para tasks sendo migradas para automação
- Adicione QA gates em handoffs críticos
- Valide compliance antes de deploy em produção
- Gere documentação para todos os stakeholders

### Don'ts ❌
- Pular fases (cada uma se baseia nos outputs anteriores)
- Atribuir agentes a tasks sem lógica de escalação
- Criar workflows com linguagem específica de humano ou agente
- Pular data contracts (quebra cadeias de handoff)
- Deploy de processos < 90% compliance
- Esquecer de atualizar configuração do ClickUp quando processo muda

---

## Troubleshooting

### Issues de Criação de Processo

**Issue**: Agente não entende minha descrição de processo
**Solução**: Use `*discover-process` do process-mapper com exemplos detalhados

**Issue**: Muitas tasks geradas
**Solução**: Use `*define-phases` do process-architect para agrupar tasks relacionadas

**Issue**: Desbalanceamento de carga entre executores
**Solução**: Use comando `*balance-workload` do executor-designer

### Issues de Integração

**Issue**: Custom fields do ClickUp não sincronizando
**Solução**: Verifique se configuração de field corresponde exatamente a clickup-config-tmpl.yaml

**Issue**: Agente não consegue executar workflow
**Solução**: Verifique se workflow usa linguagem universal (sem termos específicos de humano)

### Issues de Compliance

**Issue**: Processo pontuou < 90%
**Solução**: Execute `*validate-process` para ver issues específicos, siga plano de ação

**Issue**: Categoria crítica < 85%
**Solução**: Foque em Tasks, Executores ou Data Contracts (categorias críticas)

---

## Histórico de Versões

- **v1.0.0** (Release Inicial)
  - 9 agentes META para criação de processo
  - 10 templates YAML
  - Metodologia AIOS-PM com sistema de compliance de 100 pontos
  - Knowledge base completa
  - Suporte a executor híbrido (humano/agente/híbrido)
  - Sistema de QA gate com matrizes de decisão
  - Integração ClickUp com 20 custom fields
  - Padrões de migração progressiva

---

## Contribuindo

Para contribuir com este expansion pack:

1. Siga padrões da metodologia AIOS-PM
2. Teste todos os agentes META com processos de amostra
3. Valide precisão da pontuação de compliance
4. Documente novos padrões em aios-pm-kb.md
5. Atualize templates se estrutura mudar

---

## Suporte

Para issues, questões ou solicitações de features:

- **GitHub Issues**: Crie issue no repositório AIOS-FULLSTACK
- **Documentação**: Veja `data/aios-pm-kb.md` para metodologia detalhada
- **Exemplos**: Verifique `/output/processes/` para exemplos completos de processo

---

**Pronto para conectar suas operações com agentes de IA? Vamos começar! 🚀**

_Versão: 1.0.0_
_Compatível com: AIOS-FULLSTACK v4+_
_Autor: Pedro Valério_
_Licença: MIT_
