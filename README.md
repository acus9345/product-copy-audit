# product-copy-audit

An Antigravity skill that enforces a 3-step positioning, copy audit, and line-by-line rewrite workflow for UI copy and public product descriptions.

## When it triggers

- Auditing or rewriting vibe-coded, AI-generated, or demo/pitch-deck UI text (labels, buttons, headings, empty states, tooltips, error messages, confirmation dialogs)
- Introducing a product, project, tool, or feature to the public (launch posts, public announcements, release notes, changelogs, README intros)
- Writing, editing, or polishing product, app, package, or repository descriptions, About sections, feature summaries, one-line taglines, store listings, or onboarding and help copy

Does not trigger for git commit or PR/issue descriptions, bug reports, code comments, API or schema specs, or backend refactoring.

## Workflow

1. **Product Positioning:** Inspects the codebase, UI screens, manifests, and docs before editing to infer target users and their job-to-be-done, outputs a 4-part **Tone & Terminology Guide** (Audience, Voice & Perspective, Banned Marketing Clichés, Core Naming Glossary), and pauses for confirmation if audience, tone, glossary terms, or required facts are ambiguous.
2. **Screen-by-Screen Copy Audit:** Walks each UI screen/component or public copy section (batching apps over ~5 screens or ~50 items), classifies every string into **Keep**, **Delete**, or **Replace with icon/UI**, and outputs audit tables before rewriting.
3. **Line-by-Line Rewrite:** Rewrites remaining copy into 1–3 word UI actions/labels/headings, one-line neutral empty states, and factual public copy; prints `Before -> After` diff tables; then applies edits cleanly (preserving i18n keys/interpolations, accessible `aria-label`/`sr-only` labels, DOM references, and text-coupled tests) or outputs a copy-ready `Final Assembled Copy` block.

## Install

### Global (macOS / Linux)

```bash
git clone https://github.com/acus9345/product-copy-audit ~/.gemini/config/skills/product-copy-audit
```

### Global (Windows PowerShell)

```powershell
git clone https://github.com/acus9345/product-copy-audit "$env:USERPROFILE\.gemini\config\skills\product-copy-audit"
```

### Workspace only

```bash
git clone https://github.com/acus9345/product-copy-audit .agents/skills/product-copy-audit
```

## Files

| File | Purpose |
| :--- | :--- |
| `SKILL.md` | Skill frontmatter, 3-step workflow gates, and i18n/accessibility/test guardrails |
| `references/examples.md` | Cliché-to-product rewrite table plus worked UI screen and `README.md` audit examples |

## License

MIT
