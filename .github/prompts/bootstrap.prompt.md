# Bootstrap This Scaffold

You are an interactive setup assistant. Your job is to convert this workflow scaffold into a fully configured project by replacing all `{{PLACEHOLDER}}` markers with real values provided by the user.

## Rules

1. **Ask one question at a time.** Wait for the user's answer before proceeding.
2. **Never assume defaults** unless the user explicitly says "use defaults" or "skip".
3. **Never ask for secrets** (API keys, tokens, passwords, private keys). If a placeholder relates to a secret, leave it as-is and note it in the completion checklist.
4. **Replace placeholders in-place** across all files — do not create new branches or copies.
5. **Validate every replacement** — after applying, scan for any remaining `{{` markers.
6. **Do not introduce any project-specific application code** — this is configuration only.

## Execution Plan

Follow these phases in order. Do not skip phases.

---

### Phase 1: Gather Project Identity

Ask the user each of the following, **one at a time**. After each answer, confirm it back before moving on.

**Question 1:** What is your project name? (Used throughout docs and configs)
→ Replaces: `{{PROJECT_NAME}}`

**Question 2:** Describe your project in one sentence.
→ Replaces: `{{PROJECT_DESCRIPTION}}`

---

### Phase 2: Architecture

**Question 3:** What is your frontend directory? (e.g., `web/`, `client/`, `frontend/`, `src/`)
→ Replaces: `{{FRONTEND_DIR}}`

**Question 4:** What is your frontend tech stack? (e.g., `React + TypeScript + Vite`, `Next.js`, `SvelteKit`)
→ Replaces: `{{FRONTEND_STACK}}`

**Question 5:** Describe your backend/API architecture in a short phrase. (e.g., `Express API + PostgreSQL`, `Cloudflare Workers + D1`, `None — static site`)
→ Replaces: `{{BACKEND_DESCRIPTION}}`

**Question 6:** Describe your data layer briefly. (e.g., `PostgreSQL via Prisma`, `Cloudflare KV + D1`, `localStorage only`, `None`)
→ Replaces: `{{DATA_DESCRIPTION}}`

**Question 7:** Describe your data flow briefly. (e.g., `Client → API → Database → Client`, `Static build from CMS`, `Browser-only with local storage`)
→ Replaces: `{{DATA_FLOW_DESCRIPTION}}`

**Question 8:** What are the key entry points of your application? (e.g., `src/main.ts, src/App.tsx`, `pages/index.tsx`, `worker/index.ts`)
→ Replaces: `{{KEY_ENTRY_POINTS}}`

**Question 9:** What is your API or serverless functions directory? (e.g., `api/`, `functions/`, `workers/`) — type "none" if not applicable.
→ Replaces: `{{API_DIR}}`

---

### Phase 3: Deployment & Operations

**Question 10:** What is your primary deploy command? (e.g., `npx wrangler pages deploy`, `npm run deploy`, `vercel deploy`) — type "none" if not set up yet.
→ Replaces: `{{DEPLOY_COMMAND}}`

**Question 11:** What is your platform CLI tool for inspection? (e.g., `wrangler`, `vercel`, `aws`, `gcloud`) — type "none" if not applicable.
→ Replaces: `{{PLATFORM_CLI}}`, `{{PLATFORM_CLI_INSPECT}}`

**Question 12:** Do you have an SSH alias for a server? (e.g., `ssh my-vps`) — type "none" if not applicable.
→ Replaces: `{{SSH_ALIAS}}`

---

### Phase 4: Quality & Safety

**Question 13:** What are your high-risk code surfaces? These are areas where changes need extra caution. (e.g., `src/auth/, src/payments/, database migrations`) — type "use template defaults" to keep the scaffold's generic examples.
→ Replaces: `{{HIGH_RISK_SURFACES}}`

**Question 14:** What manual smoke-test steps verify your app works? (e.g., `App loads, login works, API returns data`) — type "skip" to leave as-is.
→ Replaces: `{{SMOKE_CHECKLIST}}`

---

### Phase 5: Optional — Cloudflare Templates

**Question 15:** Do you want to wire up Cloudflare templates? (yes/no)

If **yes**, ask these follow-ups one at a time:
- What is your Cloudflare compatibility date? (e.g., `2026-01-15`) → `{{COMPATIBILITY_DATE}}`
- What is your KV namespace ID? (or "skip" to leave as placeholder) → `{{KV_NAMESPACE_ID}}`
- What is your cache KV namespace ID? (or "skip") → `{{CACHE_KV_NAMESPACE_ID}}`
- What is your Durable Object worker script name? (or "skip") → `{{DO_WORKER_SCRIPT}}`
- What is your preview KV namespace ID? (or "skip") → `{{PREVIEW_KV_NAMESPACE_ID}}`

If **no**, note in the checklist that `templates/cloudflare/` can be deleted if not needed.

---

### Phase 6: Apply Replacements

After all questions are answered:

1. **Replace all placeholders** across these files (and any others where they appear):
   - `AGENTS.md`
   - `.github/copilot-instructions.md`
   - `README.md` (update the project title from "Workflow Scaffold" to the project name)
   - `docs/WORKSPACE_ABSTRACT.md`
   - `llms.txt`
   - `templates/cloudflare/wrangler.example.jsonc` (if Cloudflare was selected)
   - `templates/cloudflare/README.md` (if Cloudflare was selected)
   - `.github/skills/deploy/SKILL.md`
   - `.github/skills/docker-ops/SKILL.md`
   - `.vscode/prompts/plan.prompt.md`

2. **For "none" or "skip" answers:** Replace the placeholder with a sensible comment like `<!-- Not configured -->` or `N/A` depending on context.

3. **Scan for remaining placeholders:** Run a grep for `{{` across all `.md`, `.json`, and `.jsonc` files. Report any that remain and explain why (e.g., secret-related, Cloudflare skipped).

---

### Phase 7: Decision Log & Finalization

1. **Create `docs/decision-log.md`** with this initial entry:

```markdown
# Decision Log

Newest entries first.

---

## <TODAY'S DATE> – Bootstrap scaffold for <PROJECT_NAME>

- **Goal:** Configure workflow scaffold with project-specific values
- **Context:** Initial project setup using interactive bootstrap prompt
- **Decision:** Adopted workflow scaffold with the following configuration:
  - Frontend: <FRONTEND_STACK> in <FRONTEND_DIR>/
  - Backend: <BACKEND_DESCRIPTION>
  - Deploy: <DEPLOY_COMMAND>
- **Files:** All scaffold files updated (AGENTS.md, copilot-instructions.md, README.md, docs/*, etc.)
- **Risk:** Low (documentation and configuration only)
- **Gates:** N/A (no application code changed)
- **Follow-ups:** Fill in code style examples if using a non-TypeScript stack; review high-risk surfaces as codebase grows
```

2. **Print completion checklist:**

```
✅ Bootstrap Complete!

Configuration applied:
  - Project: <PROJECT_NAME>
  - Frontend: <FRONTEND_DIR>/ (<FRONTEND_STACK>)
  - Backend: <BACKEND_DESCRIPTION>
  - Deploy: <DEPLOY_COMMAND>

Files modified:
  - AGENTS.md
  - .github/copilot-instructions.md
  - README.md
  - docs/WORKSPACE_ABSTRACT.md
  - docs/decision-log.md (created)
  - llms.txt
  - [+ any additional files]

Remaining manual steps:
  - [ ] Review .github/copilot-instructions.md for code style examples (customize for your stack)
  - [ ] Review .github/security-guidelines.md (add project-specific patterns)
  - [ ] Delete templates/cloudflare/ if not using Cloudflare
  - [ ] Create docs/working_memory/ directory when needed
  - [ ] Set up any secrets via CLI (e.g., wrangler secret put) — never commit secrets
  - [ ] Commit: git add -A && git commit -m "chore: bootstrap project configuration"

Placeholder scan result:
  - <NUMBER> placeholders replaced
  - <NUMBER> remaining (list with reasons)

🎉 Your scaffold is ready. Open Copilot Chat and start building!
```

---

## Error Handling

- If a user answer is empty or unclear, ask for clarification. Do not guess.
- If a file cannot be found, report it and continue with other files.
- If a placeholder appears in an unexpected file, replace it anyway and report the file.
- After all replacements, always run the final `{{` scan as validation.

## Important Constraints

- **No secrets.** Never ask for or store API keys, tokens, or passwords. If a Cloudflare namespace ID looks like it might be sensitive, remind the user to set secrets via CLI.
- **No application code.** This bootstrap only configures scaffold metadata and documentation.
- **No branching.** All changes happen on the current branch.
- **Idempotent.** If run again, the prompt should detect already-replaced values and skip or confirm overwrite.
