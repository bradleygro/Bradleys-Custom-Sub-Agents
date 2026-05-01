# Claude Code Sub-Agents

A collection of custom sub-agents for [Claude Code](https://docs.anthropic.com/en/docs/claude-code/overview) — each one a specialized AI persona you can invoke mid-task to get focused expertise without switching tools or losing context.

---

## What Is a Sub-Agent?

Sub-agents are markdown files that define a specialized version of Claude with a specific role, communication style, toolset, and behavior. When invoked inside Claude Code, a sub-agent takes over the conversation to handle a focused task — then hands control back.

Think of them as expert collaborators you can summon by name.

---

## Available Sub-Agents

| Agent | File | Purpose |
|---|---|---|
| 🧭 Marty Mentor | `marty-mentor.md` | Product management coaching grounded in Marty Cagan's SVPG Product Model — keeps you honest about discovery, outcomes, and cross-functional collaboration |

---

## Installation

### Step 1 — Clone or download this repository

```bash
git clone https://github.com/<your-username>/<your-repo-name>.git
```

Or download individual `.md` files directly from the repository.

### Step 2 — Place the file in your Claude Code agents directory

Claude Code looks for sub-agent definitions in a specific location depending on your intended scope:

**Project-level** (available only within a specific project):
```
your-project/
└── .claude/
    └── agents/
        └── marty-mentor.md
```

**Global** (available across all Claude Code sessions):
```
~/.claude/agents/marty-mentor.md
```

Create the directory if it doesn't exist:

```bash
# Project-level
mkdir -p .claude/agents

# Global
mkdir -p ~/.claude/agents
```

Then move the `.md` file into place:

```bash
cp marty-mentor.md .claude/agents/marty-mentor.md
```

### Step 3 — Verify Claude Code can see it

Start a Claude Code session and run:

```
/agents
```

Your sub-agent should appear in the list.

---

## Invoking a Sub-Agent

You can invoke a sub-agent in two ways:

**By name in your prompt:**
> "Use the Marty Mentor to review my approach to this discovery sprint."

**With the slash command:**
```
/agent marty-mentor
```

Claude Code will hand off to the sub-agent for that task. When the task is complete, control returns to the main Claude Code session.

You can also ask Claude Code to invoke the right sub-agent automatically — it will select based on the `description` field in each agent's frontmatter.

---

## Best Practices

**Be specific when invoking.** Sub-agents perform best when given a concrete situation to respond to, not an abstract question. Instead of "review my product thinking," try "I'm about to commit to building this feature without a prototype — can the Marty Mentor pressure-test my approach?"

**Provide relevant context upfront.** Sub-agents don't retain memory of your prior Claude Code session. Give them the context they need: what you're working on, what decision you're facing, and what you've done so far.

**Use sub-agents for a focused task, then return.** They're designed for depth on a specific question, not as a full-session replacement. Invoke, get the input you need, then continue your work.

**Let the agent challenge you.** These agents are designed to ask hard questions, not validate your existing plan. The value is in the friction — sit with pushback before dismissing it.

**Don't stack multiple sub-agents in one invocation.** If you need multiple perspectives (e.g., user research + product strategy), run them sequentially with clear handoffs between them.

---

## Sub-Agent File Structure

Each `.md` file in this repository follows the same format:

```markdown
---
name: agent-name
description: When to invoke this agent. Used by Claude Code for auto-selection.
tools: Read, Grep, Glob, Bash   # tools the agent can access
model: inherit                   # inherits the model from your Claude Code session
color: blue                      # label color in the UI
---

# Agent Title

[Persona definition, role, communication style, and coaching frameworks]
```

The YAML frontmatter controls how Claude Code registers and triggers the agent. The body of the file defines who the agent is and how it behaves.

---

## Contributing

Have a sub-agent you've built and want to share? Open a pull request. Please follow the existing file structure and include a clear `description` field — that's what Claude Code uses to decide when to invoke your agent automatically.

---

## Resources

- [Claude Code Documentation](https://docs.anthropic.com/en/docs/claude-code/overview)
- [Claude Code Sub-Agents Guide](https://docs.anthropic.com/en/docs/claude-code/sub-agents)
- [Anthropic Prompt Engineering Docs](https://docs.claude.com/en/docs/build-with-claude/prompt-engineering/overview)
