# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

Claude Code plugin marketplace containing multiple plugins with skills for code review, agent delegation, research, and Google services integration. Plugins are distributed via the `/plugin marketplace add dotneet/claude-code-marketplace` command.

## Repository Structure

```
.claude-plugin/marketplace.json  # Marketplace catalog (root)
<plugin-name>/
  .claude-plugin/plugin.json     # Plugin manifest
  skills/<skill-name>/
    SKILL.md                     # Skill definition (frontmatter + instructions)
    references/                  # Reference docs for the skill
```

## Plugins

| Plugin | Skills |
|--------|--------|
| review-tool | typescript-react-reviewer, code-modularization-evaluator |
| agent-call | call-claude, call-codex, call-cursor-agent |
| agent-session | suggest-agent-rules |
| research | perplexity-search (requires `PERPLEXITY_API_KEY`), context7 (requires `CONTEXT7_API_KEY`) |
| google | google-calendar |

## Reference Documentation

Official Claude Code documentation for plugins and skills is available in `.claude/docs/`:
- `skills.md` - Skill creation guide
- `plugin-marketplaces.md` - Marketplace creation and distribution guide

## Development Commands

```bash
# Validate marketplace and plugin structure
/plugin validate .

# Test locally
/plugin marketplace add ./
/plugin install <plugin-name>@dotneet-marketplace
```

## Creating New Skills

1. Create `skills/<skill-name>/SKILL.md` with YAML frontmatter:
   ```yaml
   ---
   name: skill-name
   description: "Trigger description for the skill"
   ---
   ```
2. Add detailed instructions and reference docs in `references/` directory
3. Update plugin.json if needed

## Creating New Plugins

1. Create `<plugin-name>/.claude-plugin/plugin.json`:
   ```json
   {
     "name": "plugin-name",
     "description": "Plugin description",
     "version": "1.0.0",
     "author": { "name": "Author Name" }
   }
   ```
2. Add skills under `<plugin-name>/skills/`
3. Register in `.claude-plugin/marketplace.json` plugins array
