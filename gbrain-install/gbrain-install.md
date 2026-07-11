# GBrain Installation Record

Installed gbrain 0.26.0 from https://github.com/garrytan/gbrain

## What was installed

- **gbrain CLI** cloned to `~/gbrain`, linked globally via bun
- **Brain database** initialized at `~/.gbrain/brain.pglite` (PGLite, schema v32)
- **Skills** (34 skills + conventions) installed to `~/.claude/skills/`
- **MCP server** configured at `~/.claude/.mcp.json`
- **PATH** added to `~/.bashrc`: `$HOME/.bun/bin`

## Usage

```bash
# Query the brain
gbrain query "your question"

# Import markdown files
gbrain import ~/notes/

# Health check
gbrain doctor --json

# MCP server (used by Claude Code automatically)
gbrain serve
```

## Next steps

1. Set `OPENAI_API_KEY` for vector search embeddings
2. Import your markdown notes: `gbrain import ~/notes/`
3. Run `gbrain soul-audit` to customize agent identity
4. Optionally install GStack for coding skills
