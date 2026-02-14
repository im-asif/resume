# Codebase Issue Triage: Proposed Tasks

## 1) Typo fix task
**Issue found:** In the certifications section, `Tweny19` appears to be a typo.

**Task:** Update `Tweny19` to the correct provider name (`Twenty19` or the exact official spelling used on the certificate).

**File:** `content/about.md`

**Acceptance criteria:**
- Certification line is corrected with the proper provider spelling.
- No other resume content is unintentionally changed.

---

## 2) Bug fix task
**Issue found:** `content/projects/architecture.md` opens one Mermaid code fence and then embeds three Mermaid diagram definitions without closing/reopening fences. This causes rendering/parsing problems (only the first diagram is likely treated correctly).

**Task:** Split the architecture page into three properly fenced Mermaid code blocks (one per diagram), each with a short heading:
1. GitOps CI/CD flowchart
2. High-availability deployment topology
3. Monitoring and alerting sequence

**File:** `content/projects/architecture.md`

**Acceptance criteria:**
- Each Mermaid diagram is wrapped in its own ` ```mermaid ` ... ` ``` ` block.
- Hugo page renders all three diagrams correctly.
- Markdown linting passes for fenced code blocks.

---

## 3) Comment/documentation discrepancy task
**Issue found:** `hugo.toml` contains stale/informal comments such as `# <--- FIXED: Now points to the new page` and citation-like placeholders (`[cite: 2, 3]`) that do not match repository documentation style and provide no actionable context.

**Task:** Replace these comments with neutral, maintainable documentation comments (or remove them if redundant), e.g., describing *why* a menu route exists rather than narrating one-time edits.

**File:** `hugo.toml`

**Acceptance criteria:**
- Remove conversational/editorial comments.
- Keep only concise comments that describe configuration intent.
- No functional changes to site navigation.

---

## 4) Test improvement task
**Issue found:** The repository has no automated validation for content quality (broken Markdown structure, frontmatter consistency, links).

**Task:** Add a lightweight CI validation step for content pages, e.g.:
- `markdownlint` for Markdown structure
- `lychee` (or equivalent) for link checking
- `hugo --panicOnWarning` (or strict build mode) for site build validation

**Files:** `.github/workflows/*` (new), optional lint config files.

**Acceptance criteria:**
- CI runs on pull requests.
- A malformed fence/frontmatter error fails CI.
- At least one sample test run is documented in `README.md`.
