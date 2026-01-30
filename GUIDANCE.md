# AI Tour 26 Repository Setup Guide

## For Content Creators

This guide helps you work with GitHub Copilot to prepare your AI Tour 26 repository for publication. Copilot will ask you questions and implement the necessary changes to meet repository requirements.

## For Copilot

When a content creator asks you to "help me prepare my repo" or similar, read this entire file and guide them through each step interactively.

---

## Critical Rules for Copilot

1. **NEVER infer or assume information** the content creator hasn't explicitly provided
2. **DO NOT fill in gaps** with what you think should be there
3. **ALWAYS ask** before making changes - present your proposed change and get approval
4. **Make suggestions**, but only implement them after the creator approves
5. If something is missing, ask: "I don't see [X] in your content. Do you want to add it, or should I proceed without it?"

---

## Step 0: Become an Expert in the Content

Before making any changes, thoroughly read and understand the lab content.

1. Look for lab instructions in common locations: `/docs/`, `/lab/`, `/lab/instructions/`, or root `.md` files
2. Read all modules/exercises to understand what the user will do
3. Note the technologies, tools, and services used
4. Identify any prerequisites or setup requirements

---

## Step 1: Evaluate Home User Requirements

Evaluate the content from the perspective of someone attempting it on their own (outside a guided session).

Ask yourself:
1. **What features does the lab use?** (e.g., Agent Flows, MCP servers, premium connectors)
2. **Can these features be accessed with a trial license, or do some require paid subscriptions?**
3. **Are there any modules that would be blocked for trial users?**

If unsure, research the licensing requirements for the specific technologies.

Work with the content creator to add appropriate notes to the README:
- Be transparent about licensing without being overly specific (details change)
- Use language like "Some modules may require a paid license to complete on your own"
- Highlight that the full lab experience is guaranteed at guided sessions
- Mention potential cloud costs for home users

**Goal:** Set clear expectations so home users don't hit a paywall mid-lab.

---

## Step 2: Set Up Folder Structure

Use these standard folder names for consistency:

| Folder | Purpose |
|--------|---------|
| `/docs/` | Lab documentation and instructions (required for MkDocs) |
| `/src/` | Source code to share with customers |
| `/data/` | Data files used during the session |

Ask the content creator:
- "Are you sharing source code? Should I create a `/src/` folder?"
- "Are there data files? Should I create a `/data/` folder?"
- "Where is your lab content? I'll move it to `/docs/`"

---

## Step 3: Clean Up Documentation Content

### 3a: Remove Placeholder Content

Check `/docs/` for template leftovers:
- Remove `01-demo/` folder if it exists
- Remove `README.md` if it conflicts with `index.md`
- Remove placeholder files from `/docs/artifacts/`

### 3b: Clean Up Skillable/Lab Platform Artifacts

If content was exported from Skillable or another lab platform, search for these artifacts. **Present findings grouped by pattern type and get approval before making changes.**

**Pattern 1: `@lab.*` variables**

Search for `@lab.` in all docs files.

Present: "I found [X] instances of @lab.* variables:
- @lab.Title → Replace with actual session title
- @lab.CloudCredential(...) → Replace with `[Provided by instructor or your own account]`
- @lab.VirtualMachine(...) → Replace with `[Credentials provided by instructor]`

Should I make these replacements?"

**Pattern 2: `+++text+++` auto-type syntax**

Search for `+++` in all docs files.

Present: "I found [X] instances of +++text+++ syntax:
- URLs: Remove markers, make proper links
- User input values: Use bold or code formatting

Should I make these replacements?"

**Pattern 3: `[!note]`, `[!tip]`, `[!alert]` callouts**

Search for `[!` in all docs files.

Present: "I found [X] Skillable-style callouts. Convert to MkDocs syntax:
- `> [!NOTE]` → `!!! note`
- `> [!TIP]` → `!!! tip`
- `> [!ALERT]` → `!!! warning`

Should I convert all of these?"

**Pattern 4: VM-specific paths**

Search for `D:\`, `C:\LabFiles`, or VM desktop references.

Present: "I found [X] VM-specific paths. Options:
- Replace with relative paths
- Add notes for guided sessions only
- Provide alternatives for home users

How would you like to handle these?"

After approved changes, summarize what was done.

---

## Step 4: Create Landing Page

Check if `/docs/index.md` exists and whether it's a proper landing page.

**Signs it's NOT a proper landing page (needs replacement):**
- Starts with step-by-step instructions
- Contains credential placeholders
- Is very long (hundreds of lines)
- Is identical to a lab module file

**Signs it IS a proper landing page (keep it):**
- Has welcome message and session overview
- Describes what user will learn/build
- Contains navigation links to modules
- Is relatively short (under 100 lines)

**A good landing page includes:**
- Workshop title and welcome message
- Overview of what the session covers
- What the user will build (scenario description)
- Learning outcomes
- Technologies used
- Navigation links to lab modules

---

## Step 5: Configure MkDocs

### 5a: Update mkdocs.yml metadata

Replace placeholder values:
- `site_name`: Session code and title
- `site_url`: GitHub Pages URL for this repo
- `site_author`: Content owner names
- `site_description`: "Documentation for [session code]..."
- `repo_name` and `repo_url`: Actual repository

### 5b: Configure navigation

The `nav:` section should have:
- Home pointing to `index.md`
- Lab section with each module in order

### 5c: Verify assets

Check that referenced assets exist:
- `docs/overrides/` folder
- Logo file in theme config
- CSS file in `extra_css`

### 5d: Test the build

Run `mkdocs build` to verify no errors. Run `mkdocs serve` to preview:
- Home page shows landing page (not lab instructions)
- All modules accessible from navigation
- All links work

---

## Step 6: Update README.MD

### 6a: Session Information

Determine session code and title from repo name or existing README. Confirm with creator.

Update:
- Main heading with session code and title
- Session description (2-3 sentences)
- Learning outcomes (3-4 bullet points)
- Technologies used (with links to learn.microsoft.com where helpful)

### 6b: Getting Started Sections

**For guided sessions (LAB/PREL/WRK):**

Add `### 🏫 Getting Started in a Guided Session`:
- VM/environment provided
- Credentials from instructor
- Link to lab instructions
- Note: "Full lab experience guaranteed at AI Tour events"

**For home users:**

Add `### 🏠 Getting Started in Your Own Environment`:
- Link to trial/account signup
- Prerequisites to install
- Clone repo instructions
- Note about licensing and cloud costs

Ask: "Can customers complete this lab in their own environment?"
If no, add: "Note: You may be unable to complete all steps in your own environment because [reasons]."

### 6c: Content Owners

Update the Content Owners table with names and GitHub usernames.

---

## Step 7: Manual Steps (Remind Creator)

These steps require the content creator to complete manually:

1. **GitHub Repo Settings**: Click gear icon ⚙️ in repo, set description, add technology tags
2. **Slides/Recordings**: Link to external hosting (Azure blob storage), do not store in repo

---

## Step 8: Final Review

Before finishing:

1. Run `mkdocs build` one final time to verify no errors
2. Summarize all changes made
3. Ask: "Are you satisfied with all the changes?"
4. Remind about manual steps (repo settings)
5. Ask if they want to delete GUIDANCE.md or keep it for reference

---

## Questions?

If you encounter issues or need clarification, contact your content lead or Mike Kinsman on Teams.
