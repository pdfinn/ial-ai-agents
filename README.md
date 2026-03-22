# AI Agents for Educators

Companion repository for the IAL (Institute for Adult Learning) presentation:
**"Building AI Agents for Educators"**

These are open-source n8n workflow templates designed for Singapore's adult education sector — trainers, curriculum designers, and training providers working with SkillsFuture, WSQ, and CET programmes.

## What's in this repo

### Workflows (importable into n8n)

| Workflow | Nodes | Description |
|----------|-------|-------------|
| `workflows/skillsfuture-lesson-planner.json` | 6 | Four-agent pipeline that generates a complete lesson package: lesson plan, assessment package, tool recommendations, and a compiled final document — all aligned to SSG/WSQ frameworks. |
| `workflows/tsc-competency-finder.json` | 5 | Enter a course topic and sector — the workflow searches 12,000+ real SSG Technical Skills & Competencies (TSCs) and generates learning outcomes mapped to actual Knowledge and Ability statements. |
| `workflows/batch-feedback-analyser.json` | 6 | Paste trainee feedback (one per line) — the workflow classifies each response by theme and sentiment, then generates an actionable summary report with priority improvements. |
| `workflows/course-proposal-drafter.json` | 8 | Three-agent pipeline that drafts the hardest sections of the SSG Course Proposal form: LU/LO structure, K&A mapping, instructional rationale — all grounded in real Skills Framework data. |

### Why n8n, not just a chatbot?

Each workflow does something a chatbot alone cannot:

| Workflow | What n8n adds |
|----------|--------------|
| Lesson Planner | Multi-agent pipeline — each agent builds on the previous output |
| TSC Competency Finder | Searches a real 12,000+ entry SSG competency database — AI can't hallucinate codes |
| Feedback Analyser | Loops over every response individually, aggregates results — processes 50+ items in one click |
| Course Proposal Drafter | Combines real data lookup + multi-agent pipeline + cross-referencing between sections |

### Data files

| File | Description |
|------|-------------|
| `data/tsc-ka-data.json` | All 12,000+ TSC codes with Knowledge & Ability statements from the SSG Skills Framework, covering 42 sectors. Used by the TSC Competency Finder and Course Proposal Drafter workflows. |

### Prompt Templates (copy and use anywhere)

The same prompts used in the workflows, extracted as standalone templates you can use in ChatGPT, Claude, or any LLM:

| Template | What it generates |
|----------|-------------------|
| `templates/lesson-plan-agent.md` | Structured lesson plan with learning outcomes, session flow, differentiation notes, and materials list |
| `templates/assessment-agent.md` | Formative checks, summative assessment with rubric, marking guide, and feedback templates |
| `templates/tools-and-resources-agent.md` | Edtech tool recommendations, AI preparation tips with copy-paste prompts, and OER links |
| `templates/compile-agent.md` | Merges the three sections above into one polished trainer-ready document |
| `templates/competency-mapping-agent.md` | Maps course topics to TSC codes and generates aligned learning outcomes with K&A coverage |
| `templates/feedback-classifier-agent.md` | Classifies trainee feedback by theme, sentiment, and actionability |
| `templates/feedback-report-agent.md` | Generates actionable feedback report with priority improvements |

## Quick Start

### Prerequisites

- [n8n](https://n8n.io) — self-hosted or cloud
- An Anthropic API key (the workflows use Claude Sonnet; you can swap to any model you prefer)

### Setup

1. **Start n8n** (if self-hosting with Docker):
   ```bash
   docker run -d --name n8n -p 5678:5678 -v n8n_data:/home/node/.n8n docker.n8n.io/n8nio/n8n
   ```

2. **Import a workflow:**
   - Open n8n at `http://localhost:5678`
   - Go to **Workflows > Import from File**
   - Select any workflow from the `workflows/` directory

3. **Add your Anthropic credential:**
   - Go to **Credentials > Add Credential > Anthropic**
   - Paste your API key
   - Update the Claude nodes in the workflow to use this credential

4. **Activate the workflow** and visit the form URL shown in the trigger node.

### Using the prompt templates without n8n

Each file in `templates/` contains a system message and a user message template. Copy them into any LLM interface — the output format instructions work with GPT-4, Claude, Gemini, and most capable models.

## Seminar Guide

For the 1-hour IAL seminar, the recommended presentation order is:

| # | Workflow | Time | Purpose |
|---|----------|------|---------|
| 1 | Lesson Planner | 10 min | Warm-up demo — show multi-agent pipeline concept |
| 2 | **TSC Competency Finder** | 20 min | Star of the show — real data + AI. Live demo + walkthrough |
| 3 | Batch Feedback Analyser | 15 min | Different pattern — looping/aggregation. Hands-on exercise |
| 4 | Course Proposal Drafter | 10 min | Teaser — "what you could build next" |
| — | Q&A | 5 min | |

## Design Principles

These workflows were built with a few opinions:

- **Structured output formats** — Every agent specifies the exact Markdown structure it expects. This makes output consistent and composable.
- **Scoped responsibilities** — Each agent does one thing well rather than trying to produce everything in a single prompt.
- **Singapore context** — WSQ levels, SSG frameworks, SkillsFuture Series, multilingual considerations, and local workplace scenarios are baked in.
- **Data-grounded** — Where possible, workflows use real SSG Skills Framework data rather than relying on the AI's training knowledge. This prevents hallucinated competency codes.
- **Practical over impressive** — No unnecessary nodes, no unused integrations. The workflow does what it needs to and stops.

## Adapting for Your Context

The prompts are designed for Singapore adult education but the structure works anywhere. To adapt:

1. Replace WSQ/SSG references with your local framework (e.g., NVQ, AQF, EQF)
2. Update the form dropdowns (domains, levels, learner profiles)
3. Adjust the system messages to reference your curriculum standards
4. Swap the LLM model to whatever your organisation has access to
5. Replace `data/tsc-ka-data.json` with your own competency framework data

## License

MIT — use it, modify it, share it.
