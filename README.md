# prompt-mage

Most AI work stalls not because the model is too weak, but because the prompt is too big. A single prompt trying to do five things produces five mediocre results at best, and a tangled mess at worst. You end up re-running the same work, getting inconsistent outputs, and spending more time managing the AI than doing the actual work.

prompt-mage fixes that. You give it your raw ideas, goals, and any files or resources you are working with. It audits what you have, strips out redundancy, sequences the work correctly, assigns the right AI model to each step, and hands you back a complete Prompt Kit: a numbered set of ready-to-run prompts that build on each other and get you to a finished deliverable. Each prompt does exactly one thing. Each one tells you exactly what to feed it and exactly what it will produce. No drift, no wasted effort, no context confusion.

It does not matter what state your input is in. prompt-mage handles the full spectrum equally well: a few lines of rough ideas scribbled in a note, a detailed and highly structured brief, a library of existing prompts you want reorganized, messy documents with no clear output goal, a single complex prompt that needs to be decomposed, or an entire folder of files and reference material. Whatever you bring, in whatever condition, prompt-mage processes it and produces a clean, structured kit. You do not need to clean up your thinking before you start.

prompt-mage also delivers a HOW-TO guide alongside every kit so you know exactly how to run each prompt, in what order, with what inputs, and what you will have in hand when it is all done.

---

## QUICK START - USING WITH CLAUDE CHAT

prompt-mage is designed to run as a dedicated Claude Project. This is the correct and intended way to use it in Claude Chat. Do not paste PROMPT.md into a general-purpose chat or mix it with other work. Give it its own project so it stays focused and its instructions are always active.

### Setup (one time)

1. In Claude.ai, create a new Project and name it prompt-mage
2. Open PROMPT.md from this repo and copy the full contents
3. Paste into the Project Instructions field and save
4. Set the default model to claude-sonnet-4-6

That is the only setup you will ever do. prompt-mage is now installed and ready.

### Running it

Open a new chat inside the prompt-mage project. prompt-mage will greet you and walk you through the entire intake process step by step - no additional instructions needed. It will ask for your prompts, your external links, and your files in order, confirm everything back to you, show you a plan, and wait for your approval before building anything.

When it delivers your Prompt Kit, take it and use it elsewhere. Run each prompt in its own separate project or chat, dedicated to that task. The prompt-mage project is only for generating kits, not for running them.

### One rule

Use a new chat inside the prompt-mage project each time you want to generate a new kit. Do not reuse an old chat. Old conversation history will interfere with intake for a new set of goals.

---

## SKILL INSTALL - USING WITH CLAUDE CODE

Install prompt-mage as a named skill so you can call it by name from any Claude Code session.

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

From any Claude Code session:

    claude skill prompt-mage

Claude Code loads the instructions and walks you through intake the same way as Claude Chat.

### Passing files and directories

Single file:

    claude skill prompt-mage --file /path/to/file.xlsx

Multiple files:

    claude skill prompt-mage --file /path/to/file1.pdf --file /path/to/file2.csv

Full directory:

    claude skill prompt-mage --dir /path/to/project/folder

For URLs or cloud links, paste them inline in your prompt text during intake and describe what each contains.

### Running kit prompts in Claude Code

Each prompt in your kit specifies its required inputs and expected output. For prompts that depend on prior outputs, save the prior output to a temp file and pass it at the next step:

    claude --file /tmp/prompt1-output.txt "Paste Prompt 2 text here"

Review each output before proceeding. Do not chain steps without verification.

---

## How the prompt works

prompt-mage runs a structured six-stage intake and build process. It does not skip stages and does not rush ahead. Here is what happens internally at each stage.

Stage 0 - Introduction: prompt-mage opens with a clear explanation of the process and tells you exactly what it is going to ask for before asking for anything.

Stage 1 - Prompt intake: you paste your raw goals and ideas, one batch at a time. prompt-mage confirms each submission and gives you a full list to review before moving on.

Stage 2 - External resources: you provide any URLs, Dropbox links, Google Drive links, or other external references. prompt-mage logs each one with a description and which goal it serves.

Stage 3 - File uploads: you upload files in batches of up to 3 at a time. prompt-mage confirms each batch and builds a complete file registry before proceeding.

Stage 4 - Processing: prompt-mage runs a full audit of everything it has received. It flags oversized prompts (OVERSIZED), duplicate work (REDUNDANT), unclear output targets (AMBIGUOUS), and steps that do not contribute to the goal (UNNECESSARY). It maps dependencies, identifies parallel execution opportunities, and assigns a model to every step.

Stage 5 - Plan review: before building anything, prompt-mage presents a top-level plan showing every prompt it intends to create, what each does, what it depends on, and what model it will use. You confirm or revise before it builds.

Stage 6 - Delivery: prompt-mage delivers the full Prompt Kit followed immediately by the HOW-TO guide. The HOW-TO is a per-prompt step-by-step execution guide including what to attach, what to paste from prior steps, what the output should look like, and what to do if something goes wrong. It ends with a Completion Checklist that states exactly what you will have in hand when the full chain is done.

---

## Model selection

prompt-mage assigns one of three models to each step and uses the cheapest model that can do the job correctly.

haiku: fast, low cost. Used for file reading, data extraction, summarization, formatting, classification, and low-stakes drafts.

sonnet: the default for most real work. Used for financial modeling, business writing, structured analysis, planning, research, and anything requiring moderate multi-step reasoning. If you are unsure which model a task needs, it is sonnet.

opus: reserved for tasks that genuinely cannot be broken into discrete steps and require simultaneous reasoning across multiple truly interdependent variables. If prompt-mage assigns opus to more than one step in a kit, it stops and tells you the problem needs further decomposition. In practice, most business and financial work runs entirely on sonnet.

---

## Example inputs

The following examples show the range of inputs prompt-mage can handle, from a simple idea to a complex operational brief.

---

Example 1 - B2C subscription service (simple, user story style)

    I want to figure out why customers are cancelling after the first month. I have survey responses and cancellation data. I want to understand the main reasons and come up with ideas to fix it.

prompt-mage will:
- Identify two distinct tasks: analysis and ideation
- Sequence them so findings from the analysis feed the ideation step
- Assign haiku to data extraction and sonnet to synthesis and recommendations
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
- Assign haiku to data extraction from meter logs, sonnet to ranking models and carbon impact analysis, and confirm whether opus is genuinely needed or whether cross-model dependencies can be resolved with well-structured sonnet prompts and explicit context passing

---

## Repository structure

    prompt-mage/
      PROMPT.md      <- The full prompt. Paste into Claude Project Instructions or install as a Claude Code skill.
      README.md      <- This file.

---

## Requirements

- Claude Pro account required for Projects in Claude Chat
- Claude Code CLI required for skill install
- Recommended default model: claude-sonnet-4-6
