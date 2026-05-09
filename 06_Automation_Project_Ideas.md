---
spec_id: SETUP-006
title: Automation Project Ideas — Things Sara Could Have Claude Set Up
audience: Claude (to suggest these to Sara when timing is right) + Sara (so she knows what's possible)
owner: Sara Riegel
date: 2026-05-08
---

# Automation Ideas for Sara 🌸

Five concrete automations that would meaningfully change how Sara works. Each one is described in plain English first (for Sara), then with technical notes (for Claude).

**Don't pitch all five at once.** Suggest one when the moment is right — usually right after finishing a related project.

---

## 💡 IDEA 1 — The "Phone Call to Project" Pipeline (the big one)

### What it does, in plain English

Whenever Sara and her son Nicolas talk on the phone about a finance project, the call is recorded and transcribed automatically. Nicolas's Claude turns the transcript into a clean project specification (the kind of file in `Issues/`). That spec is pushed to a private shared folder online (a GitHub repo). Sara's Claude is watching that folder. As soon as the new project lands, it's ready and waiting for her the next time she sits down at her computer.

**Sara's experience:**
1. Have a phone call with her son.
2. Sit down at her computer later that day or week.
3. Open Claude.
4. Hear: *"Hey Sara! 🌸 Your son sent over a new project — rebuilding your year-end report. Want me to walk you through it?"*
5. Say yes. Get to work.

No re-explaining. No re-sending files. No copy-paste.

### What's needed to set it up

- Nicolas creates a GitHub repository under his organization, adds Sara as a collaborator using her email.
- Sara approves the GitHub connection on her Claude desktop **one time** (she clicks "Approve" — Claude walks her through it).
- Claude sets up a scheduled task that polls the repo every 15 minutes for new files in `/Issues/`.
- New files are pulled into her local `Sara_Riegel _Spec_Auto/Issues/` folder.

### Important reminder for Sara

> "💡 Heads up: this only works when your Claude desktop is **open**. Try to leave it running in the background — it's quiet and doesn't use much. If you close it, I won't see new projects until you open me again."

### Status

✅ This is the recommended **first** automation to set up. Full setup steps are in `05_Technical_Setup_For_Claude.md` Section 7.

---

## 💡 IDEA 2 — Monthly Budget Reconciliation (set-it-and-forget-it)

### What it does, in plain English

On the first business day of every month, Claude:
1. Asks Sara for the latest accounting export (or pulls it automatically if connected).
2. Compares actuals against the budget for the previous month.
3. Highlights anything that's off by more than a threshold she sets (default: 10%).
4. Produces a one-page "what to know before the board meeting" memo.
5. Drops it in `Documents/Sara_Work/Board_Reports/` and pings her on her next session.

**Sara's experience:**
- Opens Claude on the 2nd of the month.
- Sees: *"Your monthly reconciliation is ready! 🌸 Three line items came in over budget — want to look at them together?"*
- 10 minutes later, she's ready for the board.

### What's needed

- A consistent monthly accounting export (CSV or Excel from the accountants).
- The clean budget worksheet from `ISSUE-001` (already in progress).
- A scheduled task running on the 1st of each month.
- An agreed-upon variance threshold (Sara picks).

### When to suggest it

After `ISSUE-001` (budget rebuild) is complete and saved.

---

## 💡 IDEA 3 — Drop-Folder Document Processor

### What it does, in plain English

Sara has a folder on her desktop called **Drop_Here**. Anything she drags into it — a scanned receipt, a board email, a PDF from the accountants, a screenshot — Claude automatically:
1. Detects what kind of document it is.
2. Extracts the important info (amounts, dates, names).
3. Files it in the right subfolder of `Sara_Work/`.
4. Logs it to a master "Recent Documents" tracker.
5. If it requires action (an invoice to approve, a form to fill), surfaces it next session.

**Sara's experience:**
- Drag → drop → done. Never has to file anything by hand.

### What's needed

- A `Drop_Here` folder on her desktop (Claude creates it).
- A scheduled task that watches the folder every 5 minutes.
- File-type recognition rules (Claude figures these out as it sees more docs).
- The OCR (`pdf` skill) for scanned items.

### When to suggest it

After Sara mentions feeling overwhelmed by paperwork or scanning the same kinds of things repeatedly.

---

## 💡 IDEA 4 — Board Memo Generator

### What it does, in plain English

Before each board meeting, Sara drops the agenda + any relevant numbers in a folder. Claude generates a polished, board-ready one-pager: key updates, financial highlights, action items, in her organization's voice. She reviews, makes one or two tweaks, sends.

**Sara's experience:**
- 30 seconds to drop the agenda.
- 2 minutes to review the draft.
- Done. What used to be a 90-minute task is now 3 minutes.

### What's needed

- A `Board_Meeting_Prep/` folder where she drops the agenda.
- A reusable template (Claude builds it once, refines over time).
- The `internal-comms` skill (built-in) handles tone and structure.
- Optionally: brand colors via `brand-guidelines` skill.

### When to suggest it

Right before her next board meeting.

---

## 💡 IDEA 5 — Year-End 990 Prep Helper

### What it does, in plain English

Starting in October every year, Claude quietly assembles everything needed for the IRS Form 990 filing:
- Pulls full-year actuals.
- Re-tags them to the 990 functional expense categories (Programs & Services / Management & General / Fundraising) using the rules from `ISSUE-001`.
- Generates the functional expense breakdown table.
- Cross-checks against prior year for any flags (sudden category shifts, missing categories).
- Hands Sara a tidy package she can give straight to the accountants.

**Sara's experience:**
- October 1: *"Hey Sara, 990 prep season — want me to start building your draft?"*
- A few back-and-forths over the month.
- November: hands the draft to the accountants. They love her.

### What's needed

- Saved benchmark/category rules (from `ISSUE-001`).
- Full-year actuals (from accounting system).
- A scheduled task that triggers October 1.

### When to suggest it

When the calendar approaches Q3 of any year, or whenever Sara mentions "990," "year-end," or "tax filing."

---

## How to use this file

**For Claude:** keep these in your back pocket. When Sara finishes a project or expresses frustration about something repetitive, suggest the matching idea in one warm sentence:

> "💡 Side thought, Sara — I noticed this is the third time this month we've done [thing]. I could set up an automation so this just happens for you on the 1st of each month. Want to hear about it?"

**For Sara:** these are real. Any of them can be set up in a single session, usually under an hour. If one sounds good, just say so.

**For Nicolas:** add new ideas to this file as they come up — phone calls often surface them. Keep the format consistent.

---

## Future ideas to add over time

(blank — this section grows as Sara and Claude work together)

- 
- 
- 
