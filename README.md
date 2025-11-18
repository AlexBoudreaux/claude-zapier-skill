# Zapier Workflows Skill for Claude Code

A self-learning skill that gives Claude Code persistent memory for your Zapier automations.

## The Problem

Zapier MCP gives Claude access to 8,000+ tools, but:
- No memory of which tools you use or why
- Can't trigger your complex, multi-step Zaps
- Forgets everything each session

## The Solution

This skill provides persistent memory for both webhook-triggered Zaps and MCP tool preferences. Claude learns as you teach it and never forgets.

## Quick Start

### Installation

**Global (Recommended)** - Learned patterns persist across all projects:
```bash
git clone https://github.com/alexboudreaux/claude-zapier-skill.git
cp -r claude-zapier-skill/.claude/skills/zapier-workflows ~/.claude/skills/
```

**Project-Level** - Learned patterns only in this project:
```bash
git clone https://github.com/alexboudreaux/claude-zapier-skill.git
cp -r claude-zapier-skill/.claude/skills/zapier-workflows ./.claude/skills/
```

### Setup Zapier MCP

1. Go to https://mcp.zapier.com/mcp/servers
2. Create new MCP server for Claude Code
3. Add tools you want to use
4. Run the connection command provided
5. Restart Claude Code

See `.claude/skills/zapier-workflows/SKILL.md` for complete setup instructions.

## What You Get

- **Webhook-triggered Zaps**: Trigger multi-step workflows just by asking
- **MCP Tool Memory**: Claude remembers which tools to use and when
- **Self-Learning**: Claude updates the skill as you teach it
- **Persistent Memory**: Never forgets across sessions

## Features

- Store webhook URLs for complex, multi-step Zaps
- Document when/why to use specific MCP tools
- Build reusable workflow patterns
- Auto-updates as you teach Claude new preferences
- Works globally (if installed at `~/.claude/skills/`)

## Documentation

See [SKILL.md](.claude/skills/zapier-workflows/SKILL.md) for:
- Complete setup guide
- Self-learning protocol
- Usage examples
- Troubleshooting

## License

MIT License - See [LICENSE](.claude/skills/zapier-workflows/LICENSE)

## Contributing

This skill is designed to be customized and extended. PRs welcome for improvements to the self-learning system or documentation.
