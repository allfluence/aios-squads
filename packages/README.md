# AIOS Method Expansion Packs

Expansion packs extend AIOS-Method beyond traditional software development, providing specialized agent teams, templates, and workflows for specific domains and industries. Each pack is a self-contained ecosystem designed to bring the power of AI-assisted workflows to any field.

## Naming Convention

All expansion-packs follow the same naming convention as the core framework (`aios-core/`):

- **Agent-specific tasks:** Use `{agent-id}-{task-name}.md` format
  - Example: `youtube-specialist-collect-youtube.md`, `blog-writer-generate-blog-post.md`
- **Shared tasks:** Use `{task-name}.md` format (NO prefix)
  - Example: `collect-all-sources.md`, `execute-mmos-pipeline.md`

This convention ensures consistency across the entire AIOS ecosystem and makes it easy to identify which agent owns which task.

## Available Packs

### Open-Source Packs (Included in `aios-fullstack`)

1. **ETL** - Data collection and extraction workflows
   - Public tool for data collection from multiple sources
   - Agents: data-collector, document-specialist, social-specialist, web-specialist, youtube-specialist, zlibrary-harvester
   - Tasks: 10 tasks for collecting and processing data

2. **expansion-creator** - Tool for creating new expansion packs
   - Allows community to create and submit expansion packs via PRs
   - Template and workflow for pack creation

### Private Packs (Separate Repository)

The following packs have been moved to a private repository (`aios-expansion-packs`):
- **creator** (CreatorOS) - Content generation workflows
- **innerlens** - Personality analysis and psychometric profiling
- **mmos-mapper** - Cognitive architecture mapping and AI personality cloning
- **aios-infrastructure-devops** - Infrastructure and DevOps automation
- **meeting-notes** - Meeting organization and note-taking
- **hybrid-ops** - Hybrid operations expansion pack

**Installation:** See [Private Expansion Packs Installation Guide](../docs/migration/repository-setup-instructions.md)

## Migration History

**2025-11-12:** Applied naming convention migration (Story 4.5.3)
- All agent-specific tasks now use `{agent-id}-` prefix
- All agent dependencies updated
- 100% compliance achieved across all 6 packs
