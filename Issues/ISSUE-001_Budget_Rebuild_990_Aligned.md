---
issue_id: ISSUE-001
title: Budget Worksheet Rebuild — 990-Aligned, Rolled-Up Categories
owner: Sara Riegel
author: Sara's Spec Writer (Hello Kitty edition)
source_call: SaraR-NicM-convo-problem1-5-8-26
date: 2026-05-08
status: Ready to implement
audience: Sara (non-technical finance user), executed by Claude
prerequisite_for_claude: Read `../01_How_Claude_Works_With_Sara.md` and `../02_About_Sara.md` before starting. Apply teacher mode and human-in-the-loop confirmation throughout.
---

# 1. Problem Statement

Sara is rebuilding the organization's annual budget worksheet because:

1. The **old worksheet's General Ledger (GL) account numbers no longer match** the numbers the accountants are currently using in the live accounting system.
2. The old worksheet has **too much line-by-line detail** (e.g., one line per chairman stipend, one line per individual conference) which makes the budget hard to read, hard to roll up, and hard to reconcile.
3. Sara wants the budget to **map cleanly to IRS Form 990 functional expense categories** ("benchmarks") — Programs & Services, Management & General, and Fundraising — because that is how the org reports to the public.

She has already started rolling up duplicate accounts manually (e.g., all chairman stipends → one line; all office expenses → one line; all meetings/conferences → one line; salary + wages + taxes + benefits + insurance → one line). She wants Claude to take it the rest of the way without her having to "touch a damn thing" beyond confirming the data is right.

**Plain-English goal:** Take the messy old budget + the new GL chart of accounts, and produce a clean, simplified, 990-aligned budget worksheet that Sara can hand to the board.

---

# 2. User Stories

**US-1 — Import what I already have**
> *As Sara, I want to drop my existing budget files and the new chart of accounts into a folder, and have Claude pick them up automatically, so I don't have to copy/paste anything.*

**US-2 — Map old accounts to new accounts**
> *As Sara, I want Claude to match each old GL account number to the new GL account number (or flag it if there's no match), so I don't have to do this line by line.*

**US-3 — Roll up the noise**
> *As Sara, I want repetitive small line items (chairman stipends, individual conferences, individual office supplies) to be combined into one summary line per category, so the budget is readable.*

**US-4 — Tag every line to a 990 benchmark**
> *As Sara, I want every budget line tagged Programs & Services, Management & General, or Fundraising, so I can see exactly how the budget will appear on the 990 functional expense breakdown.*

**US-5 — Show me before you save it**
> *As Sara, I want Claude to show me the proposed rollups and mappings side-by-side with the originals before anything is finalized, so I stay in control.*

**US-6 — Friendly, not scary**
> *As Sara, I want the assistant to sound warm and encouraging (Hello Kitty vibe — emojis okay, no jargon dumps), so I'm not intimidated by the tech.*

**US-7 — Reusable next year**
> *As Sara, I want the rules I confirm (rollup categories, naming conventions, benchmark tags) to be saved, so next year's budget rebuild is mostly automatic.*

---

# 3. Inputs

| # | Input | Format | Source | Required? |
|---|-------|--------|--------|-----------|
| I-1 | Old budget worksheet | .xlsx / .csv | Sara's shared folder | Yes |
| I-2 | Current chart of accounts (new GL numbers) | .xlsx / .csv / .pdf | From accountants | Yes |
| I-3 | Sara's draft rollup categories (Operations, Mission, Programs, etc.) | .xlsx or notes | Sara | Yes |
| I-4 | Prior-year actuals (optional, for reasonableness check) | .xlsx / .csv | Accounting system export | No |
| I-5 | Sara's naming convention notes | text / verbal | Sara | No |

If any required input is missing, Claude must **stop and ask Sara in plain English** what file to use — no guessing.

---

# 4. Outputs

| # | Output | Format | Where it lands |
|---|--------|--------|----------------|
| O-1 | Clean rebuilt budget worksheet | .xlsx | `/Sara_Budget/2026/Budget_Final_v{n}.xlsx` |
| O-2 | Mapping report (old GL → new GL, with confidence + flags) | .xlsx with two tabs: `Mapped` and `Needs Review` | Same folder |
| O-3 | Rollup summary (what got combined into what, and why) | .xlsx tab `Rollup Log` inside O-1 | Same folder |
| O-4 | 990 benchmark view (totals by Programs / Mgmt / Fundraising) | .xlsx tab `990 View` inside O-1 | Same folder |
| O-5 | Plain-English change summary for Sara | .md or chat message | Returned in chat |
| O-6 | Saved rules file (for next year) | `sara_budget_rules.json` | `/Sara_Budget/_rules/` |

---

# 5. Workflow

```
[Sara drops files in folder]
        ↓
[Claude detects new files] → confirms with Sara: "I see Old_Budget_2025.xlsx and
                                                   New_Chart_of_Accounts.xlsx —
                                                   ready to start? 🌸"
        ↓
[Step 1: Read & profile both files] — count rows, list columns, flag blanks
        ↓
[Step 2: Match old GL → new GL]
   • Exact match → auto-map
   • Close match (name similarity ≥ 0.85) → propose, ask Sara to confirm
   • No match → flag in "Needs Review"
        ↓
[Step 3: Apply rollups] using Sara's category rules
   (e.g., "all 6121x chairman stipends → 'Chairman Stipends — Total'")
        ↓
[Step 4: Tag each rolled-up line to a 990 benchmark]
   Programs & Services | Management & General | Fundraising
        ↓
[Step 5: Show Sara a side-by-side preview]
   LEFT: original lines  |  RIGHT: proposed clean lines
   Sara approves / edits / rejects per row
        ↓
[Step 6: Save final files + rules + change summary]
        ↓
[Done — Claude reports totals, flags anything weird]
```

---

# 6. Acceptance Criteria

A run is **successful** when ALL of these are true:

- [ ] Every line item in the old budget is either mapped, rolled up, or explicitly flagged in `Needs Review` (no silent drops).
- [ ] Every line in the new budget has a valid current-GL account number.
- [ ] Every line is tagged with exactly one 990 benchmark: Programs & Services, Management & General, or Fundraising.
- [ ] Salary, wages, taxes, benefits, insurance appear as **one combined line** (not separate).
- [ ] Repetitive small items (chairman stipends, individual conferences, office supplies) are **rolled up to one line per category**.
- [ ] Sara sees a preview and clicks "looks good" before any final file is written.
- [ ] Total of new budget = total of old budget ± a tolerance Sara approves (default ±$0.01 unless Sara overrode a value).
- [ ] Rules file is saved so next year's run can re-use the categories and tags.
- [ ] Sara receives a one-paragraph plain-English summary of what changed.

---

# 7. UI / UX Notes (non-tech, friendly)

- **Tone:** warm, upbeat, Hello-Kitty-friendly. Emojis okay (🌸 ✅ 📊 ⚠️). Never use words like "schema," "regex," "hash," "diff," "delta" without translating.
- **One question at a time.** Never dump a wall of questions at Sara.
- **Always show the original next to the proposed change.** Two-column compare. No "trust me" edits.
- **Confirmations are big and obvious.** "Save this version? Yes / No / Show me again."
- **If something looks off, surface it BEFORE saving.** Example: *"Heads up Sara — the new total is $4,200 lower than the old total. Want me to show you the lines that changed?"*
- **Never delete an original file.** New versions get a `_v2`, `_v3` suffix. Sara can always go back.

---

# 8. Edge Cases

| Case | What Claude does |
|------|------------------|
| Old GL number has no equivalent in new chart | Flag in `Needs Review`, ask Sara: "Should this become X, Y, or be retired?" |
| Same old account splits into two new accounts | Show Sara the split, let her assign $$ proportions or copy whole amount to one. |
| Two old accounts merge into one new account | Auto-sum; show Sara the math. |
| Line item with $0 budgeted | Keep but flag — Sara may want to remove. |
| Negative budget number | Always flag — confirm it's a credit/offset, not a typo. |
| Account name in old file is ambiguous (e.g. "Misc") | Do not auto-map. Send to `Needs Review`. |
| Sara's rollup rule conflicts with new chart structure | Show conflict, ask Sara which wins. Do not silently override. |
| File is a scanned PDF (not a real spreadsheet) | Run OCR, show Sara the extracted table, ask her to confirm before using. |
| New chart of accounts updates mid-project | Re-run mapping, show Sara only the lines that changed. |

---

# 9. Success Metrics

- **Time saved per budget cycle:** target ≥ 80% reduction vs. fully manual rebuild.
- **Lines requiring manual touch:** target ≤ 10% of total lines after first pass (the rest auto-mapped or auto-rolled).
- **Reconciliation accuracy:** new budget total matches the agreed-upon source total to the penny (or to Sara-approved adjustment).
- **Sara's confidence:** Sara can explain the resulting budget to the board without referencing Claude's working notes.
- **Re-use:** next year's run completes with ≥ 90% of categories already auto-tagged from the saved rules file.

---

# 10. Constraints / Do-Nots

- Do **not** alter Sara's rollup categories or benchmark assignments without confirmation.
- Do **not** invent GL account numbers. If unknown, flag.
- Do **not** introduce new financial domain rules that Sara didn't provide.
- Do **not** transmit the budget data outside Sara's approved environment.
- Do **not** assume PII handling — this dataset is budget numbers only (Sara confirmed: no SSNs, no individual donor PII).
- Do **not** auto-finalize. Always preview → confirm → save.

---

# 11. Hand-off Prompt (paste-ready for Claude)

> You are Sara's friendly finance assistant 🌸. Sara is rebuilding her org's annual budget. In the folder `/Sara_Budget/2026/` you'll find her old budget worksheet and the accountants' new chart of accounts. Follow SPEC-001 exactly:
>
> 1. Read both files, confirm with Sara what you found.
> 2. Map every old GL account to the new chart. Auto-map exact matches; ask Sara about close matches; flag anything unmatched.
> 3. Roll up repetitive lines per Sara's categories (chairman stipends, office expenses, meetings & conferences, salary+wages+taxes+benefits+insurance as ONE line).
> 4. Tag every rolled-up line to a 990 benchmark: Programs & Services, Management & General, or Fundraising.
> 5. Show Sara a side-by-side preview. Get her ✅ before saving.
> 6. Save `Budget_Final_v{n}.xlsx` with tabs: `Budget`, `Mapping`, `Rollup Log`, `990 View`, `Needs Review`.
> 7. Save Sara's confirmed rules to `/Sara_Budget/_rules/sara_budget_rules.json` so next year's run is faster.
> 8. Give Sara a short, plain-English summary of what changed and anything she should double-check.
>
> Tone: warm, encouraging, no jargon. One question at a time. Never overwrite originals — version everything. Human-in-the-loop on every meaningful decision.

---

# 12. Open Questions for Sara (resolve before first run)

1. What folder on your computer should the assistant watch for new files?
2. Are the prior-year actuals available, and do you want Claude to sanity-check the new budget against them?
3. Do you want the assistant to email/Slack/text you when a run is ready for your review, or just hold it in the folder?
4. Who else (if anyone) is allowed to approve the preview besides you?
