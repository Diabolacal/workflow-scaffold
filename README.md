# Workflow Scaffold

A reusable, project-agnostic scaffold for AI-assisted development workflows in VS Code.

## First-Time Setup (Required)

> **New to this repo?** Follow these steps to configure the scaffold for your project. No manual file editing required.

1. Open this repository in **VS Code**
2. Open **Copilot Chat** (Agent mode recommended — click the dropdown next to the chat input and select "Agent")
3. Open the bootstrap prompt file: [.github/prompts/bootstrap.prompt.md](.github/prompts/bootstrap.prompt.md)
4. Click the **Run** button (play icon) at the top of the prompt file — or copy its contents into Copilot Chat
5. Answer the interactive questions one at a time
6. The scaffold converts itself into your configured project — all `{{PLACEHOLDER}}` values are replaced automatically

**That's it.** After bootstrap completes, commit the changes and start building.

> **Fallback:** If you prefer manual setup, see [docs/SCAFFOLD_NOTES.md](docs/SCAFFOLD_NOTES.md) for step-by-step instructions.

---

## What's Included

- **Agent steering system** — `AGENTS.md` + `.github/copilot-instructions.md` provide guardrails, conventions, and operational rules that AI coding agents automatically pick up
- **Working Memory protocol** — maintain context across long agent sessions and survive automatic summarization
- **Risk classification** — Low/Medium/High risk classes with approval token escalation for sensitive changes
- **Three-tier permission model** — Always do / Ask first / Never do boundaries for agent actions
- **Decision logging** — templates for recording architectural choices
- **Security guidelines** — OWASP-based secure coding practices
- **VS Code config** — settings and extensions tuned for agent workflows
- **Skills** — reusable agent skills for deployment and container operations
- **Cloudflare templates** (optional) — Pages/Workers configuration starters

## Quick Start

1. Copy this scaffold into your project (or use as a template repo)
2. **Run the bootstrap prompt** — see [First-Time Setup](#first-time-setup-required) above
3. Open in VS Code with Copilot enabled — agents automatically load the steering files
4. Start building

> **Manual alternative:** Replace `{{PLACEHOLDER}}` markers by hand — see [docs/SCAFFOLD_NOTES.md](docs/SCAFFOLD_NOTES.md)

## File Structure

```
AGENTS.md                          ← Auto-loaded agent context (VS Code 1.104+)
GITHUB-COPILOT.md                  ← Copilot playbook
llms.txt                           ← AI-readable doc pointer
.github/
  copilot-instructions.md          ← Authoritative guardrails
  security-guidelines.md           ← OWASP security rules
  prompts/
    bootstrap.prompt.md            ← Interactive setup (run this first!)
    rehydrate.prompt.md            ← Context recovery prompt
  skills/deploy/SKILL.md           ← Deploy skill
  skills/docker-ops/SKILL.md       ← Container ops skill
.vscode/
  settings.json                    ← Agent settings
  extensions.json                  ← Recommended extensions
  prompts/plan.prompt.md           ← Planning prompt
docs/
  README.md                        ← Documentation index
  WORKSPACE_ABSTRACT.md            ← Scaffold overview
  SCAFFOLD_NOTES.md                ← Customization guide
  DECISIONS_TEMPLATE.md            ← Decision log format
  COPILOT_MEMORY_GUIDELINES.md     ← Memory guidelines
templates/
  cloudflare/                      ← Optional CF config templates
```

## How It Works

VS Code 1.104+ automatically loads `AGENTS.md` into every Copilot agent conversation. GitHub Copilot also reads `.github/copilot-instructions.md` for repo-wide rules. Together, these files steer AI assistants to:

- Follow your project conventions
- Respect risk boundaries and approval workflows
- Run verification gates (typecheck, build, smoke tests)
- Log decisions and maintain context
- Execute CLI commands directly instead of asking you to run them

## Requirements

- VS Code 1.104+ (for `AGENTS.md` auto-loading)
- GitHub Copilot extension (recommended) or any VS Code-compatible AI agent
- No runtime dependencies — this scaffold contains only markdown, JSON, and configuration files

## License

See [LICENSE](LICENSE) for details.
