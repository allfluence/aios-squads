# BMAD Method Expansion Packs

## Overview

Expansion packs extend BMAD Method with specialized capabilities for specific use cases. They allow teams to add functionality without cluttering the core workflow.

## Core BMAD Flow

The original BMAD Method follows a simple, proven flow:

```text
Analyst → PM → Architect → SM → Dev
(Brief) → (PRD) → (Architecture) → (Stories) → (Implementation)
```

This core flow remains clean and focused on getting from business requirements to working software.

## Why Expansion Packs?

As BMAD has evolved, we've identified specialized needs that don't fit every project:

- Infrastructure and DevOps workflows
- UX/UI design processes
- Data engineering pipelines
- Security and compliance workflows
- Mobile development patterns
- Real World assistance and workflows without AI Agents development in mind

Rather than complicate the core method, expansion packs let you "opt-in" to additional capabilities.

## Available Expansion Packs

### 1. Infrastructure & DevOps

- **Purpose**: Cloud infrastructure design and platform engineering
- **Adds**: DevOps agent, infrastructure templates, validation checklists
- **Use When**: You need to design and implement cloud infrastructure

### 2. UX/Design (Coming Soon)

- **Purpose**: User experience and interface design workflows
- **Adds**: Design Architect agent, UI component templates
- **Use When**: You need detailed UI/UX design processes

### 3. Data Engineering (Planned)

- **Purpose**: Data pipeline and analytics infrastructure
- **Adds**: Data Engineer agent, ETL templates, data architecture patterns
- **Use When**: You're building data-intensive applications

## Structure of an Expansion Pack

Each expansion pack contains:

```text
expansion-pack-name/
├── README.md           # Overview and usage instructions
├── manifest.yml        # Installation configuration
├── agents/            # Agent configurations (.yml)
├── personas/          # Persona definitions (.md)
├── ide-agents/        # IDE-specific agents (.ide.md)
├── templates/         # Document templates (.md)
├── tasks/            # Specialized tasks (.md)
└── checklists/       # Validation checklists (.md)
```

## Installing an Expansion Pack

### Method 1: NPM Script

```bash
npm run install:expansion <pack-name>
```

### Method 2: Direct Script

```bash
node tools/install-expansion-pack.js <pack-name>
```

### Method 3: Manual

1. Copy files according to manifest.yml
2. Update team configurations as needed
3. Rebuild bundles with `npm run build`

## Creating Your Own Expansion Pack

1. Create a new folder under `expansion-packs/`
2. Add your specialized agents, templates, and tasks
3. Create a manifest.yml defining installation mappings
4. Write a README explaining purpose and usage
5. Test installation process

## Best Practices

1. **Keep Core Simple**: Don't add to core what could be an expansion
2. **Clear Purpose**: Each pack should solve a specific need
3. **Self-Contained**: Packs should work independently when possible
4. **Document Well**: Clear README and usage examples
5. **Version Compatibility**: Note which BMAD version the pack requires

## Future Vision

We envision a library of expansion packs for various industries and use cases:

- Healthcare compliance workflows
- Financial services security patterns
- E-commerce optimization flows
- Gaming development pipelines
- IoT device management

The goal is to keep BMAD's core simple while allowing infinite extensibility through modular expansion packs.
