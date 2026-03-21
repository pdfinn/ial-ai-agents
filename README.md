# AI Agents for Educators

Companion repository for the IAL (Institute for Adult Learning) presentation:
**"Building AI Agents for Educators"**

These are open-source n8n workflow templates designed for Singapore's adult education sector — trainers, curriculum designers, and training providers working with SkillsFuture, WSQ, and CET programmes.

## What's in this repo

### Workflows (importable into n8n)

| Workflow | Description |
|----------|-------------|
| `workflows/skillsfuture-lesson-planner.json` | Three-agent pipeline that generates a complete lesson package: lesson plan, assessment package, and tool recommendations — all aligned to SSG/WSQ frameworks. |

### Prompt Templates (copy and use anywhere)

The same prompts used in the workflows, extracted as standalone templates you can use in ChatGPT, Claude, or any LLM:

| Template | What it generates |
|----------|-------------------|
| `templates/lesson-plan-agent.md` | Structured lesson plan with learning outcomes, session flow, differentiation notes, and materials list |
| `templates/assessment-agent.md` | Formative checks, summative assessment with rubric, marking guide, and feedback templates |
| `templates/tools-and-resources-agent.md` | Edtech tool recommendations, AI preparation tips with copy-paste prompts, and OER links |

## Quick Start

### Prerequisites

- [n8n](https://n8n.io) — self-hosted or cloud
- An OpenAI API key (the workflows default to GPT-4o-mini; swap to any model you prefer)

### Setup

1. **Start n8n** (if self-hosting with Docker):
   ```bash
   docker run -d --name n8n -p 5678:5678 -v n8n_data:/home/node/.n8n docker.n8n.io/n8nio/n8n
   ```

2. **Import the workflow:**
   - Open n8n at `http://localhost:5678`
   - Go to **Workflows > Import from File**
   - Select `workflows/skillsfuture-lesson-planner.json`

3. **Add your OpenAI credential:**
   - Go to **Credentials > Add Credential > OpenAI**
   - Paste your API key
   - Update the three LLM nodes in the workflow to use this credential

4. **Activate the workflow** and visit the form URL shown in the Trainer Input Form node.

### Using the prompt templates without n8n

Each file in `templates/` contains a system message and a user message template. Copy them into any LLM interface — the output format instructions work with GPT-4, Claude, Gemini, and most capable models.

## Design Principles

These workflows were built with a few opinions:

- **Structured output formats** — Every agent specifies the exact Markdown structure it expects. This makes output consistent and composable.
- **Scoped responsibilities** — Each agent does one thing well rather than trying to produce everything in a single prompt.
- **Singapore context** — WSQ levels, SSG frameworks, SkillsFuture Series, multilingual considerations, and local workplace scenarios are baked in.
- **Practical over impressive** — No unnecessary nodes, no unused integrations. The workflow does what it needs to and stops.

## Adapting for Your Context

The prompts are designed for Singapore adult education but the structure works anywhere. To adapt:

1. Replace WSQ/SSG references with your local framework (e.g., NVQ, AQF, EQF)
2. Update the form dropdowns (domains, levels, learner profiles)
3. Adjust the system messages to reference your curriculum standards
4. Swap the LLM model to whatever your organisation has access to

## License

MIT — use it, modify it, share it.
