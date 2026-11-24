# Examples & Rewrite Reference

## Cliché-to-Product Cheat Sheet

| Vibe-coded / Pitch-deck Pattern | Problem | Real-Product Rewrite |
| :--- | :--- | :--- |
| "A simple, smart, seamless way to manage X" | Promotional adjectives with zero info | "Manage X from the CLI or web UI." |
| "Why choose Acme?" / "Built with love for modern teams" | Pitch-deck persuasion inside a tool | — (deleted) |
| Hero banner inside logged-in dashboard ("Welcome to your command center!") | Wastes viewport above real data | — (deleted; start at view title + controls) |
| "Nothing here yet! Let's get your journey started!" | Cheerleading empty state | "No deployments yet. Run `deploy` or connect a repo." |
| "Effortlessly synchronize your workflow in real time" | Vague marketing verbs | "Syncs changes automatically every 5s." |
| "Click here to learn more about settings" | Verbose filler | "Settings" or help icon (`aria-label="Settings help"`) |
| "Status: Currently Active" | Redundant prose | `[Icon / UI: Badge "Active"]` |

---

## Example 1: App Screen Audit

### Step 1: Tone & Terminology Guide
- **Audience & Job-to-Be-Done:** Backend developers inspecting failed webhook deliveries and replaying events.
- **Voice & Perspective:** Direct, technical, neutral. No promotional phrasing.
- **Banned Marketing Clichés:** `smart`, `seamless`, `effortless`, `simple`, `powerhouse`, `command center`, `Why choose`, welcome banners.
- **Core Naming Glossary:**
  - `Webhook` (not `Hook` or `Integration`)
  - `Delivery` (not `Dispatch` or `Attempt Log`)
  - `Replay` (not `Retry Now` or `Re-trigger`)

### Step 2: Screen-by-Screen Copy Audit

#### Screen: `DeliveriesPage.tsx`

| Location / Element | Current Copy | Classification | Reason |
| :--- | :--- | :--- | :--- |
| Top hero banner | "Welcome to your smart webhook command center!" | Delete | Demo/pitch-deck hero inside app view |
| Page subtitle | "Effortlessly monitor every event in real time." | Delete | Redundant marketing subtitle |
| Filter label | "Filter by Status:" | Keep | Functional label; strip verb prefix and colon |
| Status cell | "Successfully Delivered" | Replace with icon/UI | Status badge with `200 OK` conveys state directly |
| Action button | "Re-trigger Event Now" | Keep | Needs glossary alignment (`Replay`) and shortening |
| Empty state | "Looks like your webhook stream is sparkling clean!" | Keep | Replace cute filler with neutral fact |

### Step 3: Line-by-Line Rewrite

#### Screen: `DeliveriesPage.tsx`

| Location / Element | Before | After |
| :--- | :--- | :--- |
| Top hero banner | "Welcome to your smart webhook command center!" | — (deleted) |
| Page subtitle | "Effortlessly monitor every event in real time." | — (deleted) |
| Filter label | "Filter by Status:" | "Status" |
| Status cell | "Successfully Delivered" | `[Icon / UI: Status badge (role="status") with green dot (aria-hidden="true") + 200 OK]` |
| Action button | "Re-trigger Event Now" | "Replay" |
| Empty state | "Looks like your webhook stream is sparkling clean!" | "No deliveries match this filter." |

---

## Example 2: Public Introduction / Project Description

### Step 1: Tone & Terminology Guide
- **Audience & Job-to-Be-Done:** Engineers evaluating an open-source CLI tool that trims oversized JSON logs before shipping them to storage.
- **Voice & Perspective:** Factual, concise, scannable. State inputs, outputs, and limits plainly.
- **Banned Marketing Clichés:** `blazingly fast`, `next-gen`, `game-changer`, `simple yet powerful`, `seamless`, "In today's data-driven world...".
- **Core Naming Glossary:**
  - `Trim` (not `Optimize` or `Sanitize`)
  - `Log stream` (not `Pipeline` or `Data highway`)

### Step 2: Section-by-Section Copy Audit

#### Section: `README.md` Intro & About

| Location / Element | Current Copy | Classification | Reason |
| :--- | :--- | :--- | :--- |
| Opening tagline | "LogTrim: The next-gen, blazingly fast log optimizer!" | Delete | Pure hype, says nothing concrete |
| Intro paragraph | "In today's cloud-native world, teams struggle with bloated logs. LogTrim seamlessly transforms your data pipeline." | Keep | Must be rewritten to state actual function |
| Feature bullet 1 | "Smart & effortless JSON field dropping" | Keep | Strip adjectives, state exact behavior using `Trim` |
| Support line | "Works out of the box with zero friction!" | Keep | Required I/O & config scope slot; replace hype with exact behavior |

### Step 3: Line-by-Line Rewrite

#### Section: `README.md` Intro & About

| Location / Element | Before | After |
| :--- | :--- | :--- |
| Opening tagline | "LogTrim: The next-gen, blazingly fast log optimizer!" | — (deleted) |
| Intro paragraph | "In today's cloud-native world, teams struggle with bloated logs. LogTrim seamlessly transforms your data pipeline." | "LogTrim trims unused keys and oversized fields from newline-delimited JSON log streams before ingestion." |
| Feature bullet 1 | "Smart & effortless JSON field dropping" | "Trim oversized fields and unused keys by JSONPath rule" |
| Support line | "Works out of the box with zero friction!" | "Reads stdin, outputs NDJSON to stdout; zero config required for default size limits." |

#### Final Assembled Copy (`README.md` Intro & About)

```markdown
LogTrim trims unused keys and oversized fields from newline-delimited JSON log streams before ingestion.

- Trim oversized fields and unused keys by JSONPath rule
- Reads stdin, outputs NDJSON to stdout; zero config required for default size limits.
```
