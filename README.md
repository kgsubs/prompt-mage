# prompt-mage

A prompt architecture skill for Claude. Feed it your raw ideas and goals. Get back a structured, step-by-step prompt kit that organizes your work, assigns the right AI model to each step, flags anything that is too vague or overcomplicated, and eliminates redundant effort.

---

## What it does

- Ingests one or more raw prompts, no matter how rough
- Accepts files, folders, Dropbox links, Google Drive links, URLs, or pasted content
- Audits your prompts before building the kit - flags anything oversized, redundant, or ambiguous
- Produces a numbered Prompt Kit: each step has a clear purpose, a recommended model, and is ready to paste and run
- Assigns Haiku, Sonnet, or Opus to each step based on actual complexity - never defaults to expensive models unless genuinely required
- Ends with execution notes and a confirmation of what you will have in hand when the full kit is complete

---

## Repository structure

    prompt-mage/
      PROMPT.md      <- The copy-paste ready prompt. Use this in both modes below.
      README.md      <- This file.

---

## QUICK START - USING WITH CLAUDE CHAT

Two options. Option A for one-off use, Option B if you will use prompt-mage regularly.

### Option A - Paste and go

Copy the full contents of PROMPT.md and paste it as your first message in any new Claude chat. prompt-mage activates immediately and guides you from there.

### Option B - Claude Project (recommended)

Create a new Project, paste the full contents of PROMPT.md into the Project Instructions, and save. Every new chat inside that project runs prompt-mage automatically - no pasting required.

Use a new chat within the same project for each discrete prompt in the kit. Clean context per step prevents earlier outputs from bleeding into unrelated work.

Create a new project when switching to a completely different domain or client. The PROMPT.md instructions stay the same - just reinstall into the new project.

---

## SKILL INSTALL - USING WITH CLAUDE CODE

This mode installs prompt-mage as a named skill in your Claude Code environment so you can call it by name from any working session.

### Install

Clone the repo:

    git clone https://github.com/YOUR_USERNAME/prompt-mage.git

Copy the skill file into your Claude Code skills directory:

    ~/.claude/skills/prompt-mage/PROMPT.md

If you maintain a custom skills path, copy it there and confirm your Claude Code config points to it.

Verify the install:

    claude skills list

You should see prompt-mage in the output.

### Run

From any Claude Code session, call the skill by name:

    claude skill prompt-mage

Claude Code will load the prompt-mage instructions and prompt you for input.

### Passing input and files

For a single file:

    claude skill prompt-mage --file /path/to/your/file.xlsx

For multiple files:

    claude skill prompt-mage --file /path/to/file1.pdf --file /path/to/file2.csv

For a full directory:

    claude skill prompt-mage --dir /path/to/project/folder

For a URL or cloud link, paste it inline in your prompt text and describe what it contains.

### How to run each prompt in the kit - Claude Code

The Prompt Kit output is identical to Claude Chat. For execution in Claude Code:

- Run standalone prompts as individual claude commands or sessions
- For dependent prompts, save the prior output to a temp file and reference it at the next step:

    claude --file /tmp/prompt1-output.txt "Paste your Prompt 2 text here"

- Use --file flags to attach required resources at each step as specified in the kit
- Review each output before proceeding. Do not chain steps automatically without verification.

---

## What you will have at the end of a complete prompt chain

When you have run all prompts in the kit in sequence, you will have:

A set of discrete verified outputs - one per prompt step. Each output is a finished work product for that task: a financial model, a written brief, a ranked list, a feasibility summary, or whatever the step specified.

A completed deliverable that matches your original stated goal, built from modular parts that were each checked before the next step ran.

If the kit specified a final synthesis step, that step will combine prior outputs into a single consolidated document, report, or model ready for review or distribution.

The Execution Notes in your kit will tell you explicitly when the chain is complete and exactly what you should have in hand at that point. Do not consider the work done until you reach that confirmation.

---

## Example inputs

The following examples show the range of inputs prompt-mage can handle, from a simple idea to a complex operational brief.

---

Example 1 - B2C subscription service (simple, user story style)

    I want to figure out why customers are cancelling after the first month. I have survey responses and cancellation data. I want to understand the main reasons and come up with ideas to fix it.

prompt-mage will:
- Identify two distinct tasks: analysis and ideation
- Sequence them so findings from the analysis feed the ideation step
- Assign haiku to the data extraction and sonnet to the synthesis and recommendations
- Tell you to upload your survey file and cancellation export before running step one

---

Example 2 - Consumer packaged goods launch (moderate, operational brief)

    We are launching a new line of personal care products. I need to figure out our retail pricing strategy, understand what margin we need to hit to make the DTC channel viable, write a one-page brief for our contract manufacturer, and put together a competitive positioning summary. I have a cost breakdown sheet and three competitor SKU lists I scraped last week.

prompt-mage will:
- Flag that pricing strategy, margin modeling, manufacturer brief, and competitive positioning are four separate workstreams
- Build a sequenced kit where the margin model informs the pricing decision before any external brief is written
- Register the cost sheet and competitor SKUs as resources and assign them to the correct steps
- Keep the manufacturer brief on haiku, run the margin and pricing work on sonnet

---

Example 3 - Renewable energy project feasibility (complex, multi-domain)

    We are evaluating whether to develop a 4MW ground-mount solar facility on agricultural land we lease in two counties. I need a site feasibility summary, a financial model covering CapEx, interconnection costs, and a 20-year IRR projection under three incentive scenarios (current ITC, reduced ITC, no ITC), an assessment of permitting risk by county, and a one-page executive summary for our equity partner. The land lease terms, utility interconnection queue data, and a preliminary equipment quote are in the attached folder.

prompt-mage will:
- Audit the prompt and confirm it contains five discrete deliverables with shared data dependencies
- Build the kit so the financial model is not started until site feasibility and interconnection data are resolved
- Run permitting risk assessment in parallel with the financial model since neither depends on the other
- Assign sonnet across all financial and document tasks, flag the IRR sensitivity analysis as a candidate for opus only if all three incentive scenarios must be modeled simultaneously in a single output
- Register all three attached resources and map each to the step that requires it

---

Example 4 - Sustainable optimization of existing production operations (complex, specified operational)

    Our primary manufacturing line runs three shifts producing 180,000 units per week. Energy consumption is our largest controllable cost. I need to: audit our current consumption baseline by shift and by equipment zone using the attached 12-month interval meter data and maintenance logs; identify the top five optimization opportunities ranked by implementation cost and payback period; model the carbon reduction impact of each opportunity against our current Scope 2 reporting baseline; determine whether any opportunities qualify for utility demand response incentives in our ISO zone; and produce a phased implementation roadmap with cost, timeline, and assigned owner fields ready for ops review. Our current energy contracts, equipment specs, and last year's sustainability report are in the linked Dropbox folder.

prompt-mage will:
- Flag that this prompt contains an audit, a ranking model, a carbon impact model, a regulatory eligibility check, and an implementation roadmap - five workstreams, some interdependent
- Build the kit so the consumption audit and baseline establishment run first, since every downstream step depends on that output
- Sequence the carbon modeling and demand response eligibility check in parallel after the top five opportunities are ranked
- Hold the roadmap generation as the final step, explicitly dependent on all prior outputs
- Register the interval meter data, maintenance logs, energy contracts, equipment specs, and Dropbox folder contents as named resources with step assignments
- Assign haiku to data extraction from meter logs, sonnet to ranking models and carbon impact analysis, and confirm whether opus is genuinely needed or whether the cross-model dependencies can be resolved with well-structured sonnet prompts and explicit context passing

---

## Model selection

prompt-mage assigns one of three models to each step in your kit:

haiku
- Fast and cheap
- Used for: reading files, summarizing, formatting, simple lists, data extraction

sonnet
- Smart and efficient
- Used for: financial analysis, business writing, planning, research, most real work
- Default for anything requiring moderate reasoning

opus
- Most powerful, highest cost
- Used only when a task genuinely cannot be broken into smaller steps AND requires simultaneous reasoning across multiple interdependent variables
- If prompt-mage assigns opus to more than one step, it will stop and tell you the problem needs further decomposition

In practice: most business and financial modeling work runs entirely on sonnet. Opus is rare.

---

## Tips

- Rougher inputs are fine. prompt-mage is designed to handle messy, half-formed ideas.
- If a prompt gets flagged as OVERSIZED or AMBIGUOUS, read the flag before proceeding. It will save you time downstream.
- Paste prior prompt outputs directly into the next chat as instructed. Context does not carry automatically between separate Claude conversations.
- If a step produces output that looks wrong, do not proceed to the next step. Fix it first.
- The Execution Notes at the end of every kit will tell you when the chain is complete and what you should have in hand.

---

## Requirements

- Claude Pro account (for Projects in Mode 1)
- Claude Code installed (for Mode 2)
- Recommended default model: claude-sonnet-4-6
- Opus available if prompt-mage determines it is genuinely needed (rare)
