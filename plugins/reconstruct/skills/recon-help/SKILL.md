---
name: recon-help
description: "Tutorial and quick reference for Reconstruct workflow"
user-invocable: true
disable-model-invocation: false
context: main
version: v0.5
---

# Reconstruct Help - Hackathon Edition

Get help with Reconstruct workflow. This guide is designed for hackathon participants!

## Usage

```
/recon-help           → Show this quick reference
/recon-help tutorial  → Full tutorial walkthrough
/recon-help [topic]   → Help on specific topic
```

---

## Quick Reference

### Three Agents, Three Jobs

| Agent | What It Does | When To Use |
|-------|--------------|-------------|
| **Constructor** | Product planning & architecture | Building a new app from scratch |
| **Manager** | Creates implementation plans | Breaking down features into tasks |
| **Worker** | Writes the actual code | Executing a specific task plan |

### Commands

| Command | Agent | Purpose |
|---------|-------|---------|
| `/recon-setup` | Setup | Connect workspace to project (one-time) |
| **Constructor Chat** | Constructor | Plan product in UI, creates Context Cloud docs |
| `/recon-manager` | Manager | Create capsule + task plan |
| `/recon-worker` | Worker | Execute the plan with your approval |
| `/recon-help` | Help | This help |

### Docs

| Need | Link |
|------|------|
| Get started | https://reconstruct.app/docs/quickstart |
| First project guide | https://reconstruct.app/docs/guides/first-project |
| Core concepts | https://reconstruct.app/docs/concepts |
| Cursor commands | https://reconstruct.app/docs/integrations/cursor-commands |
| Troubleshooting | https://reconstruct.app/docs/guides/troubleshooting |

### Typical Hackathon Workflow

**Option A: Starting from scratch (greenfield)**
```
1. Constructor Chat (in UI) → Define product, get architecture
2. /recon-manager           → Pick first feature, create plan
3. Open new chat
4. /recon-worker            → Execute the plan
5. Return to manager, say "done", pick next feature
```

**Option B: Adding to existing code**
```
1. /recon-setup      → Connect project (once)
2. /recon-manager    → Describe feature, create plan
3. Open new chat
4. /recon-worker     → Execute the plan
5. Return to manager, say "done"
```

---

## Tutorial Mode

**If user said `/recon-help tutorial`:**

### Welcome to Reconstruct! 👋

Reconstruct helps you build products faster with specialized AI agents. Perfect for hackathons!

**🎯 The Big Picture:**

Think of Reconstruct like a dev team:
- **Constructor** = Product Manager (defines what to build)
- **Manager** = Tech Lead (breaks down how to build it)
- **Worker** = Developer (writes the code)

**Key Concepts:**

1. **Context Cloud** - Shared project knowledge (architecture, decisions, patterns)
2. **Capsule** - A scoped workspace for one feature (has safety guardrails)
3. **Plan** - Step-by-step instructions for the worker
4. **Session** - Active work context (connects everything together)

**Three Agents:**

| Agent | Role | What They Know |
|-------|------|----------------|
| **Constructor** | Product planner | User needs, architecture, full vision |
| **Manager** | Feature planner | Existing code, patterns, planning |
| **Worker** | Code writer | Only the current task plan |

**Why Three Agents?**

- **Separation of concerns**: Planning ≠ Implementation
- **Focused context**: Each agent sees only what it needs
- **Human oversight**: You approve at each transition
- **Speed**: Constructor can define multiple features while Worker implements the first

---

### Let's Try It!

**For a brand new hackathon project:**
```
Step 1: Open Constructor Chat (in the UI)
        Tell it your idea, it creates architecture docs
Step 2: Pick your first feature  
Step 3: Run /recon-manager to create a plan for that feature
Step 4: Open a new chat → Run /recon-worker
Step 5: Worker shows you each change, you approve
Step 6: Return to manager, say "done", pick next feature
```

**For adding to existing code:**
```
Step 1: Run /recon-setup (one time only)
Step 2: Run /recon-manager, describe your feature
Step 3: Manager creates capsule + plan
Step 4: Open new chat → /recon-worker executes it
Step 5: Return to manager when done
```

**Pro tip:** Constructor can plan 3-4 features while Worker implements feature #1. Parallel work FTW!

---

## Topic Help

**If user said `/recon-help [topic]`:**

### Topics

**constructor** - Product planning agent:
- Runs in the Constructor Chat (UI)
- Defines product vision, architecture, tech stack
- Creates Context Cloud documentation
- Can plan multiple features in one session
- Does NOT write code (planning only)
- **Use when:** Starting a new project or planning major features

**manager** - Implementation planning agent:
- Creates detailed task plans for specific features
- Explores codebase to understand patterns
- Defines capsules (what files can be touched)
- Hands off to worker for execution
- Does NOT write code (planning only)
- **Use when:** You know what to build, need execution plan

**worker** - Code execution agent:
- Writes the actual code changes
- Shows you each change before applying
- Follows the manager's plan exactly
- Can only modify files in the capsule scope
- **Use when:** You have an approved plan ready to execute

**capsules** - Scoped workspaces:
- `allowed_path_patterns` - Where agent CAN work
- `forbidden_path_patterns` - Where agent CANNOT work
- `guardrails` - Safety rules (no deleting DB migrations, etc.)
- `task_summary` - What this capsule is for
- **Think of it as:** A safety fence around one feature

**context-cloud** - Shared project knowledge:
- Architecture decisions
- Code patterns and conventions
- Tech stack and dependencies
- User flows and requirements
- **Think of it as:** Your project's single source of truth

**sessions** - Active work tracking:
- Links manager plan to worker execution
- Max 2 active sessions per project (keeps focused)
- Archive when feature is complete

**plans** - Step-by-step instructions:
- Created by manager, executed by worker
- Single-step (simple) or multi-step (complex)
- Includes file paths, expected changes, validation steps

**errors** - Common issues:
- "MCP not configured" → Check API key in Cursor settings
- "No session" → Run `/recon-manager` first
- "2 session limit" → Archive an old session
- See `/recon-help recovery` for more

**recovery** - When things go wrong:
- Check state with preferences.json + get_session
- Most issues fixed by re-running setup or manager
- Nuclear option: delete `.reconstruct/` and start fresh

---

## Still Stuck?

```
1. Open https://reconstruct.app/docs/guides/troubleshooting
2. Check reconstruct.app dashboard for project state
3. Review capsule settings in dashboard
4. Try /recon-sync to refresh context
5. Delete .reconstruct/ and run /recon-setup fresh
```
