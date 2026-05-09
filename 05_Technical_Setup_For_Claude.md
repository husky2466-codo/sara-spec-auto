---
spec_id: SETUP-005
title: Technical Setup — Plugins, Skills, Connections, File Structure
audience: Claude (running on Sara's desktop)
owner: Sara Riegel
date: 2026-05-08
status: Run on first session OR when Sara says "let's get fully set up."
priority: Do as much of this AUTOMATICALLY as possible. Only involve Sara when she absolutely has to click something.
---

# Technical Setup for Sara's Claude 🌸

This file tells you (Claude) everything that needs to be installed, connected, configured, and arranged on Sara's desktop so she can use AI the way a power user would — without her ever needing to understand the backend.

**Default rule:** if Desktop Commander or any MCP gives you the ability to do it yourself, **do it yourself.** Tell Sara what you did after, in one sentence. Only walk her through clicks for things you genuinely cannot do (OAuth approvals, plugin marketplace installs, granting permissions).

---

## 0. Pre-flight check — what's already installed?

Before doing anything else, **check what's already on her machine.** Don't assume.

Run, in this order:
1. `list_granted_applications` — see what computer-use access exists.
2. Use Desktop Commander (`mcp__Desktop_Commander__*`) tools to list installed plugins, skills, and MCP connections.
3. Check the working folder structure exists (`/Sara_Riegel _Spec_Auto/`).
4. Check her Documents folder for an existing `Sara_Work/` folder.

Report back to Sara in plain English:

> "Quick check done! 🌸 Here's what you've already got: ✅ Desktop Commander, ✅ Excel skill, ✅ Word skill. Here's what we should add: ⚠️ GitHub connection (so your son can push projects to me automatically), ⚠️ Scheduled Tasks (so I can check on things automatically). Want me to set those up?"

If you don't actually know how to check something — say so. Don't fake it.

---

## 1. Required plugins / skills — the must-haves

These are essential. If any are missing, install them or walk Sara through it.

| Skill / Plugin | Why Sara needs it | Auto-install? |
|---|---|---|
| **Desktop Commander** | Lets you read/write files, move things around her computer, set up folders, run small scripts. This is your superpower. | Walk her through if missing — it's a one-click install from the plugin marketplace. |
| **xlsx skill** | Building, reading, editing Excel budgets. Essential. | Should be built-in. Verify it triggers correctly. |
| **docx skill** | Board memos, letters, reports. Essential. | Built-in. Verify. |
| **pdf skill** | Reading scanned documents, filling PDF forms, generating board-ready PDFs. | Built-in. Verify. |
| **schedule skill** | Sets up recurring tasks (monthly close, weekly check-ins, the GitHub poll). | Built-in. Verify. |
| **internal-comms skill** | Board updates, status reports, FAQs. | Built-in. Verify. |

If any are missing, here's the script for Sara:

> "I noticed you're missing one tool I'd love to have for you — it's called [name]. It would let me [thing it does in plain English]. Want to add it? I'll show you exactly which buttons to click. Takes about 30 seconds."

---

## 2. Recommended plugins / skills — the nice-to-haves

Add these once she's comfortable. Don't push all at once.

| Skill / Plugin | Why | When to suggest it |
|---|---|---|
| **canvas-design** | Pretty PDF posters, board reports with visual polish | After she wants a deliverable that "looks nice for the board" |
| **theme-factory** | Consistent branded look across her docs | When she has 2+ recurring deliverables |
| **brand-guidelines** | If her org has brand colors, apply them | If she mentions org branding |
| **data:create-viz** | Charts from her budget data | When she has multi-year data to visualize |
| **data:build-dashboard** | Live dashboard of org finances | Once she's comfortable with everything else |

---

## 3. Required MCP connections — what to wire up

These are external services Claude connects to. Some require Sara to log in once (OAuth) — you cannot do that for her.

### 3.1 GitHub (THE BIG ONE — for auto-spec sync from her son)

**Why:** Her son Nicolas runs phone-call transcripts through his own Claude, generates a spec file, and pushes it to a shared GitHub repo. Sara's Claude watches that repo, pulls new specs into `/Issues/` automatically, and starts working on them when she opens the desktop app.

**What you (Claude) do:**
1. Check if a GitHub MCP is already installed.
2. If not, install/connect it. Sara will need to click "Approve" once — walk her through that single click.
3. Once connected, save the repo URL (her son will provide it: something like `github.com/nicolas-org/sara-specs`).
4. Set up a **scheduled task** (`mcp__scheduled-tasks__create_scheduled_task`) that polls the repo every 15 minutes for new files in the `/Issues/` folder.
5. When a new file appears, pull it down to her local `/Sara_Riegel _Spec_Auto/Issues/` folder and notify Sara on next session: *"Hey Sara! 🌸 Your son sent over a new project — want me to walk you through what it is?"*

**Sara's part:** Click "Approve GitHub" one time. Done.

**The OAuth/token piece:** Nicolas will set up the repo and add Sara as a collaborator (or add her to his org). She'll log in to GitHub once via the connector approval flow. After that, you handle everything.

### 3.2 Gmail (for board emails — later)

**Why:** Drafting replies to board members, sending finished reports.

**Auto?** Sara approves once via OAuth. Don't push this until she asks for email help.

### 3.3 Google Calendar / Apple Calendar (for the "task calendar" Nic mentioned)

**Why:** So Sara can see her project queue as a calendar instead of a list. New issues = new calendar entries.

**Auto?** Sara approves once. Add it later when she's ready.

### 3.4 File system access (her local folders)

**Why:** Read/write to her Documents, Downloads, and the Sara_Riegel_Spec_Auto folder.

**Auto?** With Desktop Commander, this is mostly already there. Verify access by listing `~/Documents/` once.

---

## 4. File structure — set this up automatically

Use Desktop Commander to create this on her machine. Don't ask first — just do it and tell her.

```
~/Documents/
└── Sara_Work/                          ← All Claude outputs land here
    ├── Budgets/
    │   ├── 2026/
    │   └── _Templates/
    ├── Board_Reports/
    ├── Letters_and_Memos/
    ├── Scanned_Documents/              ← Drop scans here, Claude OCRs
    ├── _Archive/                       ← Old versions live here forever
    └── _Rules/                         ← Your saved preferences + rules

~/Projects/Sara_Riegel _Spec_Auto/      ← Already exists; this is the project hub
    ├── 00_START_HERE_CLAUDE.md
    ├── 01_How_Claude_Works_With_Sara.md
    ├── 02_About_Sara.md
    ├── 03_First_Time_Setup_Walkthrough.md
    ├── 04_AI_Best_Practices_For_Sara.md
    ├── 05_Technical_Setup_For_Claude.md  (this file)
    ├── 06_Automation_Project_Ideas.md
    ├── Issues/                          ← New problems land here (manual or via GitHub)
    │   └── Done/                        ← Move completed issues here
    └── _Sync/                           ← GitHub clone target (created by you when GitHub is wired up)
```

After creating, tell Sara:

> "I set up your office space! 🌸 Everything we work on will live in `Documents > Sara_Work`. New projects from your son will appear in `Sara_Riegel_Spec_Auto > Issues`. You don't need to remember any of this — I'll always tell you where a file is."

---

## 5. Auto-configurable settings (do these without asking)

Set these defaults silently. Tell Sara afterward in one summary sentence.

| Setting | Default value |
|---|---|
| Default save location | `~/Documents/Sara_Work/` (organized by category) |
| Versioning style | `_v1`, `_v2`, `_v3` suffixes |
| Originals | Never overwrite. Always copy first. |
| Confirmation level | High — show before/after on every save |
| Tone preset | Warm, Hello-Kitty-friendly, plain English |
| Notification method | Hold in folder; mention next session |
| Time zone | Match her system clock |
| Currency format | USD with commas, two decimals |

---

## 6. Things Sara MUST do herself (cannot automate)

Be honest about these. Walk her through each one click-by-click. Confirm at every step.

1. **One-time plugin marketplace approval** — if she needs to install a plugin, she clicks "Install."
2. **OAuth login screens** — for GitHub, Gmail, Calendar. She types her password (you cannot see it, ever).
3. **Granting Claude desktop permissions** — macOS permissions for file access, screen recording, etc. Walk her through System Settings.
4. **Keeping Claude desktop OPEN** — for the GitHub auto-sync to work, the desktop app needs to be running. Remind her gently and often.

When walking her through one of these, the format is always:

> "Okay Sara, the next step is one I can't do for you — but I'll guide you. 🌸
> 
> 1. Look at the top-right corner of your screen — see the little [thing]? Click it.
> 2. A box will pop up that says [exact words]. Click 'Approve.'
> 3. Tell me when you've done that and I'll keep going."

**One step at a time. Wait for her confirmation between each.**

---

## 7. The auto-spec sync flow (end-to-end, what to set up)

This is the big workflow. Once configured, it runs forever.

```
[Nic & Sara talk on phone]
        ↓
[Call gets transcribed → Nic gets a transcript file]
        ↓
[Nic's Claude reads transcript → generates ISSUE-XXX spec]
        ↓
[Nic pushes spec to GitHub repo: github.com/<org>/sara-specs/Issues/]
        ↓
[Sara's Claude (scheduled task, every 15 min) polls the repo]
        ↓
[New file detected → pull to /Sara_Riegel _Spec_Auto/Issues/]
        ↓
[Sara opens Claude → Claude says: "Your son sent over a new project — ready to take a look? 🌸"]
        ↓
[Sara says yes → Claude reads spec + operating manual → executes with confirmations]
        ↓
[Done → Claude moves spec to Issues/Done/ AND commits result back to GitHub]
```

**Your setup tasks for this flow:**

1. ✅ Confirm GitHub MCP is installed and authenticated (Sara approves once).
2. ✅ Save the repo URL Nicolas gives her (ask her: *"Did your son send over a GitHub link? Paste it here when you can."*)
3. ✅ Create a scheduled task to poll the repo every 15 minutes.
4. ✅ Create the local sync folder (`/Sara_Riegel _Spec_Auto/_Sync/`).
5. ✅ Create the `/Issues/Done/` folder if missing.
6. ✅ Test the loop end-to-end: have Nicolas push a test file, confirm it lands locally, confirm Sara sees a notification on next open.

Tell Sara, in plain English:

> "Big setup done! 🌸 Here's what just happened: any time your son and you talk through a problem and he records it, his computer turns it into a project file and quietly drops it in our shared folder online. As long as your Claude desktop is open, I'll see it within 15 minutes and have it ready for you when you next come to your screen. **One important thing:** I can only do this if your Claude desktop stays open. Try to leave it running in the background — it doesn't use much."

---

## 8. Health check — run this monthly

Set up a scheduled task that runs the first of every month and reports to Sara on next session:

- ✅ All plugins still installed?
- ✅ All MCP connections still authenticated?
- ✅ GitHub poll is still working?
- ✅ Folder structure intact?
- ⚠️ Anything missing or broken? Surface it gently.

Format:

> "Monthly check-in 🌸 — everything's working great except: [thing]. Want me to fix it? I think it'll take about [time]."

---

## 9. When Claude is unsure

You will hit things you don't recognize. Apply the rule from `01_How_Claude_Works_With_Sara.md`:

- Don't fake it.
- Tell Sara: *"I'm not 100% sure how to do this part. Let me find out."*
- Then: search docs, ask the user, or escalate to Nicolas via a note in `Issues/`.

Sara should never think you're guessing. If you're guessing — say it.

---

## 10. Quick reference — what runs where

| Thing | Where it lives | Who maintains it |
|---|---|---|
| Operating manual | `01_How_Claude_Works_With_Sara.md` | Nicolas (rarely updated) |
| Sara's profile | `02_About_Sara.md` | Nicolas |
| Setup walkthrough | `03_First_Time_Setup_Walkthrough.md` | Nicolas |
| AI best practices | `04_AI_Best_Practices_For_Sara.md` | Nicolas |
| Technical setup (this) | `05_Technical_Setup_For_Claude.md` | Nicolas |
| Project ideas | `06_Automation_Project_Ideas.md` | Nicolas + you, as ideas come up |
| Active projects | `Issues/ISSUE-XXX_*.md` | Auto-generated from phone calls |
| Completed projects | `Issues/Done/` | You move them after wrap |
| Sara's deliverables | `~/Documents/Sara_Work/` | You |
| Sara's saved rules | `~/Documents/Sara_Work/_Rules/` | You |
| GitHub sync | `_Sync/` (mirror of remote) | Scheduled task |

---

That's the full technical picture. Set up what you can, walk Sara through the rest, and report status in one warm summary at the end. 🌸
