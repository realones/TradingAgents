# AI‑Assisted Codebase Learning Kit

Use this pack to guide any AI agent (ChatGPT, Cursor, Copilot, etc.) to teach you a new repository **from shallow to deep**. Copy the master prompt, paste it into your AI, and keep the templates in your repo under `/docs/`.

---

## 1) Master Prompt (copy‑paste)

**Role:** You are my *Codebase Tutor & Guide*. Your job is to teach me a new repository step‑by‑step, asking targeted questions, proposing a learning plan, and verifying my understanding with short quizzes. Start broad, then go deeper.

**Context (fill in):**

* Project name: `<name>`
* Repo: `<link or local path>`
* Tech stack: `<e.g., React + TypeScript + Node/Express + Postgres>`
* My role & background: `<e.g., FE engineer with basic GraphQL>`
* Time available per day/week: `<e.g., 45 min/day, 5 days>`
* Deadlines or goals: `<e.g., ship a bugfix in 1 week>`

**Objectives:**

1. Build a high‑level mental map (modules, services, build/run/test).
2. Identify the primary user flows and the system’s critical path.
3. Learn how to run, test, and debug locally.
4. Understand data model, APIs, config, and CI/CD.
5. Be able to ship a small change with tests.

**Interaction Rules:**

* Drive the process. At each step, ask me 3–5 **specific questions** maximum, then wait.
* Never assume. If context is missing, ask concise questions first.
* Prefer hands‑on tasks (read code, run commands, small edits) over theory.
* Summarize what we learned at the end of each step.
* Give me a short **quiz** (2–4 questions) after each major milestone.
* When you propose commands or scripts, explain what they reveal.
* Keep answers concise; use bullet points and checklists.

**Deliverables you must maintain:**

* `/docs/StudyPlan.md` — living plan with milestones & checklists.
* `/docs/CodebaseMap.md` — modules, entry points, build/run/test, key files.
* `/docs/Glossary.md` — domain & project terms.
* `/docs/Questions.md` — open questions with owner & status.

**Constraints:**

* If you’re unsure, say so and propose how to verify.
* Flag risky steps (e.g., scripts that modify files) and suggest safe read‑only alternatives.
* Redact or avoid secrets; remind me to use `.env` and sample configs.

**Kickoff Now:**

1. Ask me for: (a) stack, (b) package manager/build tool, (c) how to run tests, (d) which part I must contribute to first.
2. Propose a 5‑day learning plan tailored to my answers, with daily goals and artifacts to update.
3. Suggest **repo‑scan commands** (read‑only) and tell me what to paste back.
4. After I paste outputs, synthesize a **Codebase Map** and a **First Task** I can ship.

---

## 2) First‑Session Script (what the AI should do)

1. Confirm goals & constraints in ≤6 bullets.
2. Provide a minimal **Day 0 scan kit** (below) and ask me to paste results.
3. From outputs, draft `/docs/CodebaseMap.md` v0.1.
4. Propose a **5‑day plan** with success criteria & daily quiz.
5. Give me my **first tiny PR** target (doc fix, typo, comment, or harmless refactor) to validate setup.

---

## 3) Day 0 Repo Scan Kit (read‑only)

Use these commands (adapt to your stack). Paste results back to the AI (trim long outputs).

**Language/size/layout**

```bash
# Top‑level view (ignore heavy dirs)
find . -maxdepth 2 -type d | sed 's|^./||' | grep -Ev 'node_modules|.git|dist|build|target|venv|.next|.turbo'

# Code by language
npx cloc . 2>/dev/null || cloc .
```

**Dependency & scripts (JS/TS)**

```bash
cat package.json | jq '{name, scripts, dependencies, devDependencies}'
# Or
jq '.scripts' package.json
```

**Python**

```bash
python -V || python3 -V
cat pyproject.toml 2>/dev/null || cat setup.cfg 2>/dev/null || cat requirements.txt 2>/dev/null
```

**Java/Gradle**

```bash
./gradlew tasks --all | head -n 200
./gradlew test --dry-run
```

**Go/Rust**

```bash
go list -m all | head -n 50
cargo metadata --no-deps -q | head -n 80
```

**Tests & CI**

```bash
rg -n "describe\(|it\(|test\(" -S || grep -R "describe\|it\|@Test" -n .
ls -la .github/workflows 2>/dev/null
```

**Entrypoints & configs**

```bash
rg -n "main\(|createRoot\(|bootstrap\(|FastAPI\(|Flask\(|Express\(|ApolloServer" -S
rg -n "\.env|dotenv|config|settings|application\.yml|application\.yaml" -S
```

---

## 4) Five‑Day Learning Plan (template)

**Day 1 — High‑level map**

* Read top‑level layout, package/build files, README, CI.
* Output: `/docs/CodebaseMap.md` v0.2 with modules & entry points.
* Quiz (examples): What starts the app? Where are tests? How do we run them?

**Day 2 — Run & test**

* Get local run working; run unit tests and 1 integration test.
* Output: Commands & troubleshooting notes in `StudyPlan.md`.
* Quiz: What environment vars are required? What’s the default port?

**Day 3 — Data & APIs**

* Sketch data model and main APIs (graph of types/endpoints).
* Output: Add diagrams or bullet maps to `CodebaseMap.md`.
* Quiz: Which module owns persistence? Where are DTOs/schemas?

**Day 4 — Critical path**

* Trace a primary user flow end‑to‑end (e.g., Sign‑in → Dashboard).
* Output: Sequence of files/functions touched with short notes.
* Quiz: Which functions are most complex? Where are guardrails/tests?

**Day 5 — Ship a tiny change**

* Pick a 30–60 min fix/refactor; add/adjust tests.
* Output: PR link, what changed, before/after behavior.
* Quiz: Risk areas? Rollback plan? Next 2 learning targets.

> If you have more time, extend to Week 2: perf profiling, reliability, domain deep dive, and ownership map.

---

## 5) Files to add to your repo (templates)

### `/docs/StudyPlan.md`

```markdown
# Study Plan

## Objectives
- [ ] High‑level map
- [ ] Run & test locally
- [ ] Understand data & APIs
- [ ] Trace critical path
- [ ] Ship a tiny change

## Schedule
- Start: <date>  End: <date>  Timebox/day: <e.g., 45 min>

## Milestones & Evidence
- Day 1: <notes / links>
- Day 2: <notes / links>
- Day 3: <notes / links>
- Day 4: <notes / links>
- Day 5: <PR link>

## Open Questions
- [ ] Q1 — Owner: <name>  Needed by: <date>
- [ ] Q2 — Owner: <name>  Needed by: <date>
```

### `/docs/CodebaseMap.md`

```markdown
# Codebase Map (living)

## Modules / Packages
- <module>: purpose, key deps, entrypoints

## Build / Run / Test
- Build: <cmd>
- Run: <cmd>
- Test: <cmd or dir>

## Entrypoints & Key Files
- <path>: role

## Data & APIs
- DB: <type>  Key tables/models: <list>
- APIs: <REST/GraphQL/gRPC>; main endpoints/schemas

## CI/CD
- Workflows: <paths>
- Quality gates: <linters/tests/coverage>
```

### `/docs/Glossary.md`

```markdown
# Glossary
- Term: short definition / link to code
```

### `/docs/Questions.md`

```markdown
# Questions (with owners)
- Q: <text>  Owner: <name>  Status: Open/Answered  Link: <issue/doc>
```

---

## 6) “Coach Config” (optional)

Create `.ai/coach-config.json` so any AI tool knows your preferences.

```json
{
  "style": { "concise": true, "bullets": true },
  "cadence": { "questions_per_step": 4, "quiz_after_milestone": true },
  "artifacts": ["/docs/StudyPlan.md", "/docs/CodebaseMap.md", "/docs/Glossary.md", "/docs/Questions.md"],
  "risk_policy": { "mutating_commands": "explain_and_confirm" }
}
```

---

## 7) Question Bank the AI should ask you

* What’s the immediate deliverable you’re on the hook for?
* Which platform(s) matter first (backend, web, mobile)?
* Which package manager/build tool is authoritative?
* How are secrets/env vars managed (sample env, vault)?
* Which tests are considered “blocking” by CI?
* Who can review/answer domain questions?

---

## 8) Small First‑PR Ideas

* Fix a README typo or add missing run/test instructions.
* Add a sample `.env.example` (no secrets).
* Tighten a type/interface, add a missing null‑check.
* Convert one TODO comment into an issue and link it.

---

## 9) Deep‑Dive Menu (pick as you go)

* **Ownership map:** map maintainers to folders/packages.
* **Error budget:** where do failures show up? (logs, metrics)
* **Performance:** trace the slowest endpoint or render.
* **Reliability:** feature flags, retries, timeouts, idempotency.
* **Security:** authN/Z boundaries, data handling, audit.

---

## 10) One‑liner Prompts (for quick asks)

* “Summarize the responsibilities of `/src/server/` in 5 bullets; list top 3 risky files.”
* “Given this test output, what is the smallest change to make it pass safely?”
* “Trace the ‘Create Account’ flow: list functions in call order with file paths.”
* “Generate ripgrep queries to locate all uses of `<term>` and suggest next reads.”

---

## 11) Session Definition of Done (DoD)

* I can run the project and at least one test locally.
* I can describe the main modules and entrypoints.
* I have a merged tiny PR (or a reviewed draft).
* `StudyPlan.md` and `CodebaseMap.md` updated today.

---

### How to use this kit

1. Paste the **Master Prompt** into your AI and fill blanks.
2. Run the **Day 0 Scan Kit**; paste outputs back.
3. Commit the templates under `/docs/`; keep them updated.
4. Aim for one small PR by Day 5.

