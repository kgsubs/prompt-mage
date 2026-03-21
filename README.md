# prompt-mage

Tell Claude to do something complex in one prompt and you get a messy, incomplete result. Break that same task into a series of focused steps and you get exactly what you asked for.

prompt-mage does the breaking down for you. Give it your goal - rough notes, a brief, files, whatever you have - and it builds you a step-by-step Prompt Kit: a numbered list of ready-to-run prompts, each focused on one task, in the right order, with instructions on exactly how to use them.

---

## QUICK START - USING WITH CLAUDE CHAT

### Step 1 - Create your prompt-mage workspace (one time, 5 minutes)

Claude Projects let you save a set of instructions that stay active across every conversation. You will create one Project just for prompt-mage and never need to set it up again.

1. Go to claude.ai and sign in
2. Click Projects in the left sidebar
3. Click New Project and name it prompt-mage
4. Click Set Instructions (or the pencil icon near the top of the project)
5. Open PROMPT.md from this repo, copy all the text, and paste it into the instructions field
6. Save
7. Set the model to claude-sonnet-4-6

That is it. Setup is done.

### Step 2 - Use it

1. Open a new chat inside your prompt-mage project
2. prompt-mage will greet you and ask for your goals, files, and any links - one step at a time
3. Follow its prompts. It will confirm everything back to you and show you a plan before building anything
4. When it delivers your kit, each prompt is ready to copy and run

### Step 3 - Run your prompts

Take each prompt from your kit and run it in its own separate new chat. Do not run them inside the prompt-mage project - that workspace is only for building kits.

Each new kit needs a fresh chat inside the prompt-mage project. Do not reuse an old one.

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
