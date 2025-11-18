---
name: zapier-workflows
description: Manage and trigger pre-built Zapier workflows and MCP tool orchestration. Use when user mentions workflows, Zaps, automations, daily digest, research, search, lead tracking, expenses, or asks to "run" any process. Also handles Perplexity-based research and Google Sheets data tracking.
---

# Zapier Workflows Skill

## The Problem This Solves

**Zapier MCP gives Claude access to 8,000+ individual tools** (every Zapier action), but there are critical limitations:

❌ **No memory** - Claude doesn't remember which tools YOU use or why
❌ **No context** - Doesn't know when to use specific tools for your workflows
❌ **Only one-off actions** - Can't trigger your complex, multi-step Zaps
❌ **Fresh start every session** - All context lost between conversations

### The Two Types of Zapier Automation

**1. MCP Tools (One-Off Actions)**
- Individual Zapier actions (Add row to sheet, Send email, etc.)
- Available via Zapier MCP at https://mcp.zapier.com/mcp/servers
- Great for flexible, on-the-fly automation
- **Problem:** 8,000+ choices with no guidance on which to use or when

**2. Multi-Step Zaps (Webhook-Triggered)**
- Complex workflows you've built in Zapier dashboard
- Multiple actions chained together, pre-optimized
- Triggered via webhook URL (POST request)
- **Problem:** Claude can't trigger these - they're not in the MCP

## What This Skill Does

**This skill solves both problems** by giving Claude persistent memory for your Zapier workflows:

✅ **Remembers your MCP tool preferences** - "Use Google Sheets for expenses, Notion for tasks"
✅ **Knows when/why to use each tool** - "Search with Perplexity when researching, not Google"
✅ **Triggers multi-step Zaps** - "Run my daily digest" = webhook POST to your complex Zap
✅ **Self-learning** - Claude updates the skill as you teach it, never forgets
✅ **Cross-session persistence** - Works across all conversations (global install)

### What You Get

**For Multi-Step Zaps:**
- Store webhook URLs and what they do
- Trigger complex workflows just by asking
- Remember when/why to use each Zap
- Document costs, timing, outputs

**For MCP Tools:**
- Document which tools you prefer for which tasks
- Build reusable workflow patterns
- Store tool-specific preferences (sheet names, formats, etc.)
- Create multi-tool orchestration sequences

**Self-Learning:**
- Claude automatically updates skill files when you teach it
- Changes persist forever (global install) or per-project (local install)
- No manual editing required - just talk to Claude

## Installation & Setup

### Installation Location

**Global (`~/.claude/skills/`) - RECOMMENDED:**
- Learned patterns persist across ALL projects
- One Zap library for everything
- Preferences carry over to all projects

**Project-level (`./.claude/skills/`):**
- Learned patterns ONLY in this project
- Isolated from other projects
- Useful for project-specific workflows

### Prerequisites

**Required:**
- Claude Code
- Zapier account (for webhooks and MCP tools)

**Optional:**
- Additional MCP tools based on your workflows (Perplexity Search, Google Sheets, etc.)

### Setting Up Zapier MCP

To connect Zapier's MCP tools to Claude Code:

1. **Go to Zapier MCP servers:**
   - Visit https://mcp.zapier.com/mcp/servers
   - Login to your Zapier account if prompted

2. **Create a new MCP server:**
   - Click "New MCP Server" button (top left)
   - In "MCP Client (required)" dropdown, select **Claude Code**
   - Give your server a name (e.g., "My Zapier Tools")

3. **Add tools:**
   - Click "Add tools" button
   - Select as many Zapier actions as you want (each becomes an MCP tool)
   - Common tools: Run Zap, Add Row to Google Sheets, Send Email, etc.

4. **Connect to Claude Code:**
   - Click "Connect" button
   - You'll see a command like this:
   ```bash
   claude mcp add zapier https://mcp.zapier.com/api/mcp/mcp -t http -H "Authorization: Bearer ZjFmZGJkN..................1NjBhYzc2MDRlYg=="
   ```
   - Copy and run this command in your terminal

5. **Restart Claude Code:**
   - Close and reopen Claude Code
   - Your Zapier MCP tools are now available

**Tip:** You can add more tools later by editing your MCP server in Zapier and running the connect command again.

### Creating Webhook-Triggered Zaps

For pre-built, optimized workflows that you want to trigger on-demand:

1. **In Zapier dashboard:**
   - Create a new Zap
   - Choose "Webhooks by Zapier" as trigger
   - Select "Catch Hook"
   - Copy the webhook URL provided

2. **Build your workflow:**
   - Add whatever actions you want (API calls, data processing, etc.)
   - Test and optimize the Zap

3. **Document it in this skill:**
   - Tell Claude about the new Zap (webhook URL, what it does, trigger phrases)
   - Claude will add it to `references/zaps.md` automatically
   - Now you can trigger it by just asking Claude!

**Webhook vs MCP Tools:**
- **Webhooks:** Pre-built, multi-step Zaps you trigger with a POST request. Great for complex, optimized workflows.
- **MCP Tools:** Individual Zapier actions called directly. Great for flexible, on-the-fly automation.

## Self-Improvement Protocol

**CRITICAL: This skill can and should edit itself to learn from user feedback.**

When the user teaches you something new or corrects your approach:

1. **Identify what to update:**
   - New Zap to document → Edit `references/zaps.md`
   - MCP tool preference → Edit `references/mcp-patterns.md`
   - New workflow pattern → Edit `references/mcp-patterns.md`

2. **Make the edit using Claude Code tools:**
   - Read the file first with the **Read** tool
   - Update with the **Edit** tool (specify exact `old_string` and `new_string`)
   - Confirm the change to the user

3. **Update format:**
   ```markdown
   User: "Use Apollo instead of Clearbit for company data"
   Claude: [uses Read tool on references/mcp-patterns.md]
           [uses Edit tool to update the preference]
           "Updated! I'll use Apollo for company enrichment from now on.
            This change is now permanent in the skill."
   ```

**What to capture in skill updates:**
- ✅ Tool preferences (which tool for which task)
- ✅ Workflow sequences (step-by-step patterns)
- ✅ Error handling approaches
- ✅ Data formatting requirements
- ✅ New Zaps and their details
- ❌ One-off requests (don't clutter the skill)
- ❌ Temporary context (use memory instead)

## Decision Logic

### When to Use Webhook-Triggered Zaps

Use webhooks when:
- Task is complex, multi-step, and already refined
- User mentions a specific Zap name (check `references/zaps.md`)
- Deterministic execution is critical
- Task involves 5+ API calls or complex orchestration
- Cost/time efficiency matters (pre-built Zaps are optimized)

### When to Use MCP Tool Orchestration

Use MCP tools when:
- Task is simple (1-3 actions)
- Flexibility is needed (parameters change)
- Testing a new workflow pattern
- User explicitly asks to use specific MCP tools

## Execution Pattern

1. **Listen for triggers:** Workflow names, "run", "trigger", "search", "research", etc.
2. **Check references:** Use Read tool on appropriate reference file for details
3. **Check prerequisites:**
   - **If MCP tools needed but not available:** Provide Zapier MCP setup instructions (see below)
   - **If webhook URL needed but not in references:** Provide webhook extraction instructions (see below)
4. **Execute:**
   - **For webhook-triggered Zaps:** Use Bash tool with curl to POST to webhook URL (webhooks are created in Zapier dashboard with "Catch Hook" trigger)
   - **For MCP tool workflows:** Call the appropriate Zapier MCP tool directly (configured via https://mcp.zapier.com/mcp/servers)
5. **Confirm:** Tell user what happened in natural language
6. **Learn:** If user corrects you, use Edit tool to update the skill files

## Setup Detection & Instructions

### If Zapier MCP Not Detected

When user requests MCP tool functionality but Zapier MCP is not connected, tell them:

```
"I don't see the Zapier MCP tools connected. Here's how to set them up:

1. Go to https://mcp.zapier.com/mcp/servers
2. Login to your Zapier account
3. Click 'New MCP Server' (top left)
4. Select 'Claude Code' in the MCP Client dropdown
5. Give it a name (e.g., 'My Zapier Tools')
6. Click 'Add tools' and select the Zapier actions you want
7. Click 'Connect' and copy the command shown
8. Run that command in your terminal (it looks like):
   claude mcp add zapier https://mcp.zapier.com/api/mcp/mcp -t http -H "Authorization: Bearer [your-token]"
9. Restart Claude Code

Once setup, I'll be able to use those Zapier actions directly!"
```

### If User Wants to Add a Webhook-Triggered Zap

When user mentions creating or adding a multi-step Zap for webhook triggering, provide these instructions:

```
"To get your webhook URL from an existing Zap:

1. Go to your Zap in the Zapier dashboard
2. Make sure the trigger is a 'Webhooks by Zapier' node
3. In the 'Trigger Event' dropdown, select 'Catch Hook'
4. Go to the 'Test' tab
5. Copy the 'Webhook URL' shown
6. Give me that URL and tell me:
   - What the Zap does (step-by-step)
   - What trigger phrases you want to use
   - Any other details (timing, cost, etc.)

I'll add it to my knowledge so you can trigger it anytime just by asking!"
```

## Quick Reference

- **All Zaps:** See `references/zaps.md`
- **MCP Patterns:** See `references/mcp-patterns.md`
- **Common workflows:** Both files contain examples

## Usage Examples

**Triggering a Zap:**
```
User: "Run my daily digest"
Claude: [uses Read tool on references/zaps.md for webhook details]
        [uses Bash tool to trigger webhook with curl POST]
        "Started your Daily AI Digest. You'll get the report via email
         in ~3 minutes, with SMS alerts for any high-priority items."
```

**Using MCP orchestration:**
```
User: "Research the latest on quantum computing"
Claude: [uses Read tool on references/mcp-patterns.md]
        [calls Perplexity Search MCP tool]
        [analyzes results, identifies gaps]
        [calls Perplexity Search again for deeper dive]
        "Here's what I found... [summary]"
```

**Learning and updating:**
```
User: "No, when tracking expenses use my 'Personal Budget' sheet, not 'Expenses'"
Claude: [uses Read tool on references/mcp-patterns.md]
        [uses Edit tool to update the Google Sheets section]
        "Got it - updated the skill. I'll use 'Personal Budget' sheet
         for expense tracking from now on."
```

## Important Notes

- **Webhooks don't need payloads** - Zaps get their data from Zapier Tables
- **Always read reference files** before executing - they contain critical details
- **Update skill files** when learning something new - don't just remember it for this conversation

## Claude Code Tools Used

This skill uses the following Claude Code tools:

- **Read** - To view reference files (zaps.md, mcp-patterns.md)
- **Edit** - To update skill files with new workflows, patterns, or preferences
- **Bash** - To trigger Zapier webhooks using curl POST requests
- **MCP Tools** - To call Perplexity Search, Google Sheets, and other integrations
