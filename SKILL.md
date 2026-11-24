---
name: product-copy-audit
description: >-
  Enforces a 3-step positioning, copy audit, and rewrite workflow to turn hype-filled
  or rough text into terse, factual product copy. Use whenever the user wants to
  audit, clean up, or rewrite vibe-coded, AI-generated, or demo/pitch-deck UI copy,
  labels, buttons, empty states, tooltips, or error messages so an app reads like a
  real product. Also use when introducing a product, project, tool, or feature to the
  public (launch posts, public announcements, telling the public about something,
  release notes, changelogs, README intros) or writing, editing, or polishing
  product/app/package/repo descriptions, About sections, feature summaries, taglines,
  store listings, or onboarding and help copy. Do not use for git commit or PR/issue
  descriptions, bug reports, code comments, API/schema specs, or backend refactoring.
---

# Product Copy Audit

Enforce a strict 3-step workflow to turn pitch-deck, demo-grade, or AI-generated copy into terse, factual, utility-first product language.

**Hard gate:** Do not edit files or output final prose until you have completed Step 1, drafted the Step 2 audit table(s), and drafted the Step 3 `Before -> After` diff table(s) (for the active batch when splitting large apps). Include the completed Step 1 guide, all Step 2 audit tables, and all Step 3 diff tables in your response alongside any applied edits or the `Final Assembled Copy` block.

## Step 1: Product Positioning

Before editing any files or drafting copy, inspect the codebase, UI screens/components, package manifests, and any source docs or prompt context to verify real capabilities and infer:
- **Who** the target users are.
- **What job** they are trying to accomplish.

For large apps, list the full inventory of screens, shared components, and locale files in scope here so nothing is skipped later.

Produce a short **Tone & Terminology Guide** covering four items:

1. **Audience & Job-to-Be-Done** — 1–2 concrete sentences describing the user and task.
2. **Voice & Perspective** — Direct, neutral, utility-first phrasing. Use second person only when instructing an action. Zero hype or cheerleading.
3. **Banned Marketing Clichés** — Explicitly forbid slogans, "Why choose X" blocks, self-congratulatory taglines, AI throat-clearing ("In today's fast-paced world..."), and promotional adjectives (`simple`, `smart`, `seamless`, `warm`, `effortless`, `powerful`, `revolutionary`, `next-gen`, `delightful`, `intuitive`, `cutting-edge`).
4. **Core Naming Glossary** — Canonical terms for core objects and actions so every screen and doc uses one word per concept (for example, `Workspace` instead of `Space` or `Hub`; `Save` instead of `Apply` or `Confirm`).

**Confirmation gate:** If the product's audience, positioning, intended tone, or canonical glossary terms are ambiguous—or if required capabilities and constraints cannot be verified from the codebase, source docs, or prompt—stop here and confirm the Tone & Terminology Guide (plus any missing facts) with the user before starting Step 2. Never invent commands, metrics, or compatibility claims.

## Step 2: Screen-by-Screen Copy Audit

Walk through the app one screen or component at a time across every visible UI text surface (headings, nav items, tabs, buttons, field/filter labels, placeholders, tooltips, validation/error messages, toasts, confirmation dialogs, empty and loading states), or walk public copy section by section (headline/summary, intro, capability bullets, setup/CTA). Classify each item into one of three buckets:

- **Keep** — Text slot or element that stays as visible copy (functional labels, CTAs, real data, concrete facts, empty states, or required descriptions), whether already compliant or needing rewrite in Step 3. State in `Reason` if it stays as-is or how it must change.
- **Delete** — Demo-level filler, hero banners inside app screens, slide/pitch-deck persuasion copy, redundant subtitles, marketing fluff, or hype intros.
- **Replace with icon/UI** — Text that communicates faster as a UI element (icon, badge, counter, status indicator, live data) or, in public docs, as a code snippet, terminal output, or badge.

Output a concise screen-by-screen (or section-by-section) Markdown audit table **before** rewriting anything:

```markdown
### Screen / Section: <Name>

| Location / Element | Current Copy | Classification | Reason |
| :--- | :--- | :--- | :--- |
| Header subtitle | "Your smart hub for effortless tasks" | Delete | Pitch-deck filler inside app view |
| Primary CTA | "Get Started Now" | Keep | Core action; shorten to verb-first label |
| Status text | "Item is currently synced" | Replace with icon/UI | Sync icon + sr-only label conveys state |
```

**Special cases for Step 2:**
- **Brand-new public copy (no prior draft):** Plan the minimal factual structure block by block (for example: one-line summary, core commands/capabilities, constraints/compatibility, install/CTA). In the audit table, set `Current Copy` to `— (new)` and classify each planned block (`Keep` for essential factual copy; `Replace with icon/UI` for blocks better shown as code snippets, terminal output, or badges; `Delete` only when explicitly cutting requested or template fluff such as slogans or "Why choose X").
- **Large or multi-screen apps:** If the Step 1 inventory exceeds ~5 screens or ~50 items, split into logical batches (for example: shared navigation/shell first, then one feature area or route group per batch) and execute Step 2 -> Step 3 -> code edits one batch at a time while tracking remaining inventory explicitly. Within a screen, already-compliant `Keep` items may be grouped into one summary row only after verifying each string individually (for example, `Standard controls ("Save", "Cancel", "Email") | Keep | Already terse and glossary-compliant`).

## Step 3: Line-by-Line Rewrite

Process every item from Step 2 in order following the Step 1 Tone & Terminology Guide and glossary (`Keep` items needing cleanup get rewritten; already-compliant `Keep` items stay unchanged; `Delete` items become `— (deleted)`; `Replace with icon/UI` items specify the UI element and accessible label):

- **UI actions, labels, & headings:** 1–3 words. Use verb-first phrasing for action buttons and menu triggers (`Export CSV`, `Add member`, `Filter by date`) and plain nouns without trailing colons for field/filter labels and UI headings (`Status`, `Webhook secret`, `Deliveries`).
- **Empty states:** One neutral line max. State what is absent and, if useful, the single next action (`No invoices yet.` or `No saved filters. Create one to reuse queries.`). No cheerleading.
- **Errors, confirmations, & placeholders:** 1–2 short factual sentences max for errors and confirmations stating what failed or will happen and, when helpful, the next step (`Invalid JSON on line 4.` / `Delete this token? Existing clients will lose access.`); placeholders show format examples only (`name@company.com`), never instructions or hype.
- **Public introductions, announcements, release notes, & descriptions:** State concretely what the thing is, who uses it, and what it does. Use descriptive, factual titles (without an artificial 3-word cap), verifiable constraints, and real commands or capabilities. Turn requested taglines or blurbs into concrete one-line summaries; zero slogans, zero promotional adjectives, zero throat-clearing.

Show a `Before -> After` diff table for each screen or section (set `Before` to `— (new)` for brand-new copy):

```markdown
### Screen / Section: <Name>

| Location / Element | Before | After |
| :--- | :--- | :--- |
| Header subtitle | "Your smart hub for effortless tasks" | — (deleted) |
| Primary CTA | "Get Started Now" | "Create project" |
| Status text | "Item is currently synced" | [Icon / UI: Checkmark icon (`aria-hidden="true"`) + `sr-only` "Synced" + tooltip] |
```

Once the Step 3 diff tables are complete and verified against Step 1, apply the edits cleanly to the codebase—or, when there are no target files to edit (such as standalone posts, release notes, or blurbs), output a clean, ready-to-paste `Final Assembled Copy` block below the table without surrounding table quotation marks and with deleted rows omitted. If the user asked strictly for an audit with no file edits or `Final Assembled Copy` block, stop after the Step 3 tables (or after Step 2 if they requested classification only without proposed rewrites).

## Implementation Guardrails

- **Preserve i18n architecture, keys, and interpolations:** When a project uses locale files (`en.json`, `.xcstrings`, `strings.xml`, `.po`), resolve `t(...)` / key references to the primary locale during Step 2 and edit the locale file rather than hardcoding inline strings. Check all call sites for shared keys before deleting or changing meaning; preserve interpolations, ICU plural/select blocks, `printf` tokens, and rich-text tags (`{count}`, `{{name}}`, `$var`, `%s`, `<0>...</0>`); remove deleted call sites in UI code (and keep localized `t(...)` keys for `sr-only`/`aria-label` text on icon/UI replacements); prune deleted keys across locale files only when no other callers remain, and flag modified keys in secondary locales without guessing translations.
- **Keep replacements accessible and DOM references valid:** When replacing text with an icon or UI indicator, provide `aria-label` or visually hidden `sr-only` text (never `title` or hover tooltip alone), add `aria-hidden="true"` to decorative icons, never rely on color alone for status, and only use icon sets or components already installed. Before deleting a heading or subtitle, verify it is not referenced by `aria-labelledby`, `aria-describedby`, or `htmlFor` and does not break heading hierarchy.
- **Update text-coupled tests:** Search test suites (`*.test.*`, `*.spec.*`, `e2e/`, snapshots) for changed/deleted copy, i18n keys, and text or accessibility selectors (`getByText`, `queryByText`, `findByText`, `getByRole(..., { name })`, `getByLabelText`, `getByPlaceholderText`, `cy.contains`, Playwright `getByText`/`getByRole`, snapshot assertions) and update or report them alongside code edits.
- **Verify after editing:** Run the project's typecheck, lint, i18n check, and affected tests (if configured), and grep modified files for remaining Step 1 banned clichés or broken references.

For cliché-to-product rewrite patterns and compact worked examples, read [examples.md](./references/examples.md).
