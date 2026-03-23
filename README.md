# prompt-mage
### Super simple, totally magic.

Getting great results from Claude is not about writing the perfect prompt. It is about breaking your goal into the right steps. prompt-mage does that for you.

Tell it what you want. Paste in rough notes, a quick idea, a detailed brief, a pile of files - anything. prompt-mage figures out the steps, puts them in the right order, assigns the best Claude model to each one, and hands you back a ready-to-run Prompt Kit with instructions on exactly how to use it.

No prompt engineering. No copy-paste gymnastics. No losing track of what goes where. Just give it your goal and let it do the thinking.

It works for anything:

- Business: strategy, financial modeling, market research, product launches, investor materials
- Creative: writing, worldbuilding, screenplays, narrative games, album and release concepts
- Engineering: technical documentation, system design, code architecture, hardware specifications
- Personal: life planning, decision frameworks, research projects, personal organization
- Legal and compliance: policy analysis, regulatory research, compliance workflows
- Academic: literature reviews, thesis structuring, grant writing, study design
- Marketing and brand: campaign planning, content strategy, brand development, design briefs
- Physical projects: construction planning, renovation scoping, fabrication workflows, event production

If your goal is complex enough to require more than one step, prompt-mage can structure it.

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


## EXAMPLES

The following examples show the range of inputs prompt-mage can handle, from a simple idea to a complex operational brief.

---

Example 1 - B2C SUBSCRIPTION SERVICE (simple, user story style)

```
I want to figure out why customers are cancelling after the first month. I have survey responses and cancellation data. I want to understand the main reasons and come up with ideas to fix it.
```

prompt-mage will:
- Identify two distinct tasks: analysis and ideation
- Sequence them so findings from the analysis feed the ideation step
- Assign haiku to data extraction and sonnet to synthesis and recommendations
- Tell you to upload your survey file and cancellation export before running step one

---

Example 2 - MESSY CREATIVE PROJECT (rough, multi-format input)

```
ok so i have this idea for a concept album. its about a guy who slowly realizes he might be living in a simulation. starts hopeful then gets paranoid then kind of peaceful at the end. i have voice memos, some lyrics i scribbled in my notes app, a playlist of reference tracks, a few pages of world-building stuff i wrote at 2am, and a folder of images i want to use for the visual identity. i dont know where to start or what order to do things in.
```

prompt-mage will:
- Normalize the input across formats: voice memos, scattered notes, reference material, visuals, and world-building fragments
- Identify five distinct workstreams: narrative arc, tracklist and song structure, lyrical development, visual identity, and production reference brief
- Flag that the narrative arc must be established before lyrics or tracklist can be structured - surfaces this as a required first step the user has not identified
- Sequence world-building and reference playlist analysis in parallel since neither depends on the other
- Register all uploaded files and voice memo transcripts as resources and assign each to the correct step
- Assign haiku to transcription and reference sorting, sonnet to narrative structure and lyric drafts, and hold opus consideration for the final thematic synthesis if arc and lyrics need to be reconciled simultaneously

---

Example 3 - LIVE DIGITAL ART SHOW (complex, multi-domain production brief)

```
We are producing a one-night live digital art show in a 400-person venue. The show features six artists doing real-time generative work projected across three synchronized screens, a live ambient score composed and performed on stage, and an interactive installation in the lobby where audience phones connect to a local network and feed data into one of the projections. I need to: define the full technical infrastructure for the three-screen sync system and the phone-to-projection data pipeline; write the artist brief that explains the technical constraints and creative parameters each artist must work within; build the production timeline from load-in through strike; identify every vendor category we need to source (AV, networking, power, venue liaison, tech crew); draft the audience-facing experience description for ticketing and press; and create a contingency plan for the three most likely technical failure scenarios during the live show. We have a venue tech spec sheet, a rough budget, and notes from a planning call with two of the artists.
```

prompt-mage will:
- Flag that this contains six discrete deliverables across technical, creative, production, and communications domains - some tightly interdependent
- Establish that the technical infrastructure definition must come first, since the artist brief, data pipeline spec, and contingency plan all depend on what the system can actually do
- Run vendor category identification and production timeline build in parallel once the infrastructure is defined, since neither depends on the other
- Hold the artist brief until infrastructure is confirmed - prevent it from being written against assumptions that the tech spec may invalidate
- Sequence the contingency plan last, after infrastructure and timeline are complete, since failure scenarios must be written against actual system design and show flow
- Assign the audience-facing copy as an independent step that can run at any point after the experience concept is clear
- Register the venue tech spec, budget, and planning call notes as resources and map each to the steps that require them
- Assign haiku to vendor list extraction and timeline formatting, sonnet to infrastructure spec, artist brief, contingency planning, and press copy - flag opus only if the three-screen sync and phone data pipeline require simultaneous multi-variable system design that cannot be cleanly separated

---

Example 4 - CONSUMER PACKAGED GOODS LAUNCH (moderate, operational brief)

```
We are launching a new line of personal care products. I need to figure out our retail pricing strategy, understand what margin we need to hit to make the DTC channel viable, write a one-page brief for our contract manufacturer, and put together a competitive positioning summary. I have a cost breakdown sheet and three competitor SKU lists I scraped last week.
```

prompt-mage will:
- Flag that pricing strategy, margin modeling, manufacturer brief, and competitive positioning are four separate workstreams
- Build a sequenced kit where the margin model informs the pricing decision before any external brief is written
- Register the cost sheet and competitor SKUs as resources and assign them to the correct steps
- Keep the manufacturer brief on haiku, run the margin and pricing work on sonnet

---

Example 5 - RENEWABLE ENERGY PROJECT FEASIBILITY (complex, multi-domain)

```
We are evaluating whether to develop a 4MW ground-mount solar facility on agricultural land we lease in two counties. I need a site feasibility summary, a financial model covering CapEx, interconnection costs, and a 20-year IRR projection under three incentive scenarios (current ITC, reduced ITC, no ITC), an assessment of permitting risk by county, and a one-page executive summary for our equity partner. The land lease terms, utility interconnection queue data, and a preliminary equipment quote are in the attached folder.
```

prompt-mage will:
- Audit the prompt and confirm it contains five discrete deliverables with shared data dependencies
- Build the kit so the financial model is not started until site feasibility and interconnection data are resolved
- Run permitting risk assessment in parallel with the financial model since neither depends on the other
- Assign sonnet across all financial and document tasks, flag the IRR sensitivity analysis as a candidate for opus only if all three incentive scenarios must be modeled simultaneously in a single output
- Register all three attached resources and map each to the step that requires it

---

Example 6 - SUSTAINABLE OPTIMIZATION OF EXISTING PRODUCTION OPERATIONS (complex, specified operational)

```
Our primary manufacturing line runs three shifts producing 180,000 units per week. Energy consumption is our largest controllable cost. I need to: audit our current consumption baseline by shift and by equipment zone using the attached 12-month interval meter data and maintenance logs; identify the top five optimization opportunities ranked by implementation cost and payback period; model the carbon reduction impact of each opportunity against our current Scope 2 reporting baseline; determine whether any opportunities qualify for utility demand response incentives in our ISO zone; and produce a phased implementation roadmap with cost, timeline, and assigned owner fields ready for ops review. Our current energy contracts, equipment specs, and last year's sustainability report are in the linked Dropbox folder.
```

prompt-mage will:
- Flag that this prompt contains an audit, a ranking model, a carbon impact model, a regulatory eligibility check, and an implementation roadmap - five workstreams, some interdependent
- Build the kit so the consumption audit and baseline establishment run first, since every downstream step depends on that output
- Sequence the carbon modeling and demand response eligibility check in parallel after the top five opportunities are ranked
- Hold the roadmap generation as the final step, explicitly dependent on all prior outputs
- Register the interval meter data, maintenance logs, energy contracts, equipment specs, and Dropbox folder contents as named resources with step assignments
- Assign haiku to data extraction from meter logs, sonnet to ranking models and carbon impact analysis, and confirm whether opus is genuinely needed or whether cross-model dependencies can be resolved with well-structured sonnet prompts and explicit context passing


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

Claude Code loads the instructions and walks you through the same intake process as Claude Chat.

### Passing files and directories

Single file:

    claude skill prompt-mage --file /path/to/file.xlsx

Multiple files:

    claude skill prompt-mage --file /path/to/file1.pdf --file /path/to/file2.csv

Full directory:

    claude skill prompt-mage --dir /path/to/project/folder

For URLs or cloud links, paste them inline during intake and describe what each contains.

### Execution modes

After your kit is built and the plan is confirmed, prompt-mage will ask how you want to run it. Claude Code supports all three modes:

AUTO-RUN: prompt-mage generates an Orchestration Mega Prompt. Paste it into Claude Code once. It runs the full kit automatically - sequential steps in order, parallel steps simultaneously, all outputs saved to named files on disk, automated validation gates between dependent steps. Completion report delivered at the end. Hands-off once started.

ATTENDED AUTO-RUN: same automated execution, but Claude Code stops after each prompt - or after each parallel batch - and displays the full output for your review. You type GO to advance, NO-GO to retry the current step, or PARTIAL to selectively rerun prompts in a batch. Nothing advances without your explicit approval. No copy-paste, no context management, full control at every checkpoint.

MANUAL: full Prompt Kit plus HOW-TO guide delivered. You run each prompt yourself.

---

## Risks by execution mode

### AUTO-RUN

The highest-risk mode. Understand these before using it.

Directional correctness is not checked. The automated validation gates confirm that each output matches the expected format and general content description. They do not catch a result that is technically well-formed but factually wrong, built on a bad assumption, or headed in the wrong direction. If prompt 3 produces a subtly incorrect financial figure and you are not watching, prompts 4 and 5 build on that figure without question. The error propagates silently until the completion report.

Cascade failure is real. Each prompt's output feeds the next. A wrong output that passes its validation gate becomes the input for the next step. By the time you review the completion report, multiple downstream outputs may be compromised. Fixing one step may require rerunning several.

Validation gates have limits. They check structure and surface content, not judgment. A market analysis that is confidently written but misses a key variable will pass a gate. A financial model with a wrong formula in a clean format will pass a gate.

When to use it: tasks where inputs are precise, expected outputs are unambiguous, and errors are easy to spot at the end. Data extraction, reformatting, classification, and well-defined single-domain modeling are reasonable candidates. High-stakes decisions, novel analysis, or anything where directional correctness matters as much as format correctness are not.

Recommendation: always review every output file in the completion report before acting on any result.

---

### ATTENDED AUTO-RUN

Significantly lower risk than auto-run. The remaining risks are honest.

You are reviewing outputs, not inputs. You see what Claude produced. You do not see the full prompt-plus-context that generated it unless you look at the source files. If a context file from a prior step was malformed or truncated, the current output may look reasonable while being built on bad data. The GO gate does not verify what went in, only what came out.

Parallel batch review can be shallow under time pressure. When three prompts complete simultaneously and display their outputs for batch review, there is a human tendency to scan rather than read. Approving a batch quickly is easy. This is the same risk as approving any document without reading it carefully.

Judgment fatigue over long kits. A kit with eight or ten steps requires eight or ten deliberate reviews. Attention degrades. Steps toward the end of a long run are more likely to receive less scrutiny than steps at the beginning.

Retry does not reset context. If you NO-GO a step and rerun it, the retry uses the same input context as the first attempt. If the problem is in the context file from a prior step rather than the prompt itself, retrying will produce the same wrong result. You must inspect the context file directly to diagnose this.

When to use it: most real work. The risk profile is close to manual for output quality, with significantly less operational overhead. The key discipline is actually reading each output before typing GO.

---

### MANUAL

The lowest-risk mode. The risks are operator risks, not system risks.

Context ingestion error. You are responsible for copying the correct output from the correct prior step and pasting it into the correct chat. Getting this wrong - pasting the wrong output, truncating it, or pasting it in the wrong position - produces a downstream prompt running on bad context with no warning. This is the most common failure mode in manual operation.

Step sequencing error. Running prompts out of order or skipping a step because the output looked unnecessary is easy to do and hard to detect. The HOW-TO guide specifies the sequence clearly. Deviating from it is a user choice with user consequences.

Output loss. If you close a chat without saving the output, that step must be rerun. There is no recovery mechanism.

When to use it: any situation where you want complete visibility and control, where the stakes are high enough that you want to read and understand every output before it becomes input for the next step, or where you do not have Claude Code available.

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

## Repository structure

    prompt-mage/
      PROMPT.md      <- The full prompt. Paste into Claude Project Instructions or install as a Claude Code skill.
      README.md      <- This file.

---

## Requirements

- Claude Pro account required for Projects in Claude Chat
- Claude Code CLI required for skill install
- Recommended default model: claude-sonnet-4-6
