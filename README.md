# Sara Riegel — Spec Auto 🌸

A private repository that powers **Sara Riegel's Claude desktop assistant**.

This repo holds (a) the operating manual and behavioral specs that tell Claude how to work with Sara — a non-technical finance chair who is new to AI — and (b) project specifications generated from phone calls between Sara and her son Nicolas.

---

## How it works

```
[Phone call between Nic and Sara]
        ↓
[Transcript generated]
        ↓
[Nic's Claude turns transcript → ISSUE-XXX spec]
        ↓
[Spec pushed to this repo's /Issues/ folder]
        ↓
[Sara's Claude pulls latest from this repo]
        ↓
[Sara opens her Claude → "your son sent over a new project, want to look?"]
        ↓
[Sara approves → Claude executes per spec, with confirmations at every step]
```

The whole point: Sara never has to re-explain a project, re-send a file, or copy-paste anything. She just opens Claude and the next project is ready.

---

## Repo structure

```
.
├── README.md                              ← you are here
├── For_Sara_OPEN_THIS_FIRST.md            ← the doc Sara ingests once to bootstrap her Claude
├── 00_START_HERE_CLAUDE.md                ← entry point for Claude — read order
├── 01_How_Claude_Works_With_Sara.md       ← Claude's operating manual (overrides defaults)
├── 02_About_Sara.md                       ← Sara's profile
├── 03_First_Time_Setup_Walkthrough.md     ← 5-min onboarding Claude walks Sara through
├── 04_AI_Best_Practices_For_Sara.md       ← Habits Claude drip-feeds Sara over time
├── 05_Technical_Setup_For_Claude.md       ← Plugins, MCPs, file structure, GitHub sync setup
├── 06_Automation_Project_Ideas.md         ← Five concrete automations Sara could enable
└── Issues/
    ├── ISSUE-001_Budget_Rebuild_990_Aligned.md
    └── Done/                              ← Completed issues moved here after wrap
```

---

## Roles

- **Sara Riegel** — the user. Finance chair, non-technical. Works in Claude desktop.
- **Nicolas Myers** — owner / spec writer. Generates issues from phone-call transcripts.
- **Sara's Claude** — the executor. Reads from this repo, follows the operating manual, walks Sara through everything.

---

## For Sara — what to do

If your son just sent you here, **don't read this file.** Open the file called **`For_Sara_OPEN_THIS_FIRST.md`** instead. That one is written for you. 🌸

---

## For Nicolas — pushing a new issue

1. Run a phone-call transcript through your spec-writer Claude.
2. Save the resulting spec as `Issues/ISSUE-XXX_short_name.md`.
3. `git add Issues/ISSUE-XXX_*.md && git commit -m "Add ISSUE-XXX: <title>" && git push`
4. Sara's Claude will pick it up on the next sync (within ~15 min if her desktop is open).

---

## Privacy

This repository is **private**. Do not commit:
- Sara's actual budget numbers, financial data, or organization names beyond what's in spec context
- PII (donor info, employee SSNs, bank account numbers)
- API keys, tokens, or credentials of any kind
- Original phone-call audio (transcripts → specs only; raw audio stays local)

The `.gitignore` enforces most of this automatically. If you're unsure, leave it out.
