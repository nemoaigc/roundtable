---
name: roundtable
description: Launch a multi-expert roundtable discussion to analyze, evaluate, or plan any task. Use this skill whenever the user asks for a "discussion", "review meeting", "team discussion", "roundtable", wants multiple perspectives on a problem, says something like "let's get the team together", "have the experts discuss this", "I want different viewpoints", or when a significant decision needs evaluation from multiple angles. Also trigger when the user has completed a major implementation step and wants a sanity check, or when planning a new feature and wants to think it through before coding. Even a simple "evaluate this" or "what do you think about this approach" can benefit from a roundtable if the topic is complex enough.
---

# Roundtable Discussion

Launch parallel background agents as independent experts. Each reads real code and produces grounded analysis. You synthesize their findings into a structured discussion — surfacing consensus, disagreements, and actions.

## Persona Pool

Read `references/personas.md` for full persona details. Here is the roster:

| Role | Candidates | When to Include |
|------|-----------|-----------------|
| **Product Manager** | Jobs (cut scope) / Butterfield (user empathy) / Bezos (customer obsession) | Almost always. Pick based on what the discussion needs. |
| **Agent Engineer** | Swyx (contracts) / Andrew Ng (data flywheels) | Projects with agents, automation, LLM workflows |
| **Code Reviewer** | Linus (brutal bugs) / Carmack (first-principles) | Whenever code has been changed |
| **Frontend Dev** | Dan Abramov (state/React) / Evan You (DX/build) / Guillermo Rauch (ship-it/deploy) | Frontend components, React, state management, build, deployment |
| **Backend Dev** | DHH (pragmatic monolith) / Antirez (data structures) | API design, data modeling, backend architecture |
| **AI Researcher** | Hinton (skeptic) / Karpathy (hands-on) / Fei-Fei Li (human-centered) | LLM prompts, ML pipelines, AI feedback loops |
| **Prompt Engineer** | Nemo (NML creator, structural architecture) / Riley Goodside (adversarial craft) / Simon Willison (pragmatic tooling) | Prompt design, NML/XML structure, LLM instruction clarity |
| **Game Designer** | Kojima (moments) / Miyamoto (joy) / Miyazaki (challenge) / Zach Gage (puzzles) / Yokoyama (mini-games) / Terry Cavanagh (arcade) / Lucas Pope (narrative systems) / Edmund McMillen (roguelike) / Bennett Foddy (viral suffering) / Nicky Case (web interactive) / Toby Fox (meme narrative) / Jonathan Blow (deep puzzles) / Mahdi Bahrami (hypercasual) | Games, gamification, mini-games, puzzles, viral mechanics |
| **Security** | Schneier (threat models) / Mitnick (attacker mindset) | Auth, payments, user data, external APIs |
| **UX Designer** | Don Norman (cognitive) / Dieter Rams (minimal) / Jony Ive (sensory perfection) | User-facing products, dashboards, visual polish |
| **DevOps/SRE** | Ben Treynor (SRE) / Kelsey Hightower (simplify) | Deployment, infra, reliability |
| **Architect** | Martin Fowler (refactoring) / Leslie Lamport (distributed) | Large refactors, new systems, concurrency |
| **Prediction Markets** | Shayne Coplan (Polymarket) / Robin Hanson (futarchy) / Nate Silver (probability) / Vitalik Buterin (incentives) / Philip Tetlock (superforecasting) | Prediction market design, question design, incentives, probability communication |
| **Quantitative Trading** | Jim Simons (signal extraction) / Nassim Taleb (risk/tail events) / Ed Thorp (Kelly criterion) / Cliff Asness (factors/backtesting) / Marcos López de Prado (ML quant) | Quant strategy, risk management, backtesting, ML for finance, bet sizing |
| **Content/Growth** | Paul Graham (essays) / Eugene Wei (distribution) / Packy McCormick (narrative) / Pieter Levels (shipping) | Articles, X posts, content strategy, virality, MVP launch |

## Selection Rules

1. **No fixed limit on participants.** Pick as many as the topic needs — 3 for a quick decision, 7+ for a deep architecture review. Match scope to complexity.
2. **Multiple from the same role is encouraged.** Two PMs with different philosophies, three AI researchers with different angles — the point is cognitive diversity, not role coverage.
3. **Vary within roles.** Don't always pick the same persona. If the discussion is about cutting scope, pick Jobs. If it's about user empathy, pick Butterfield. If it's about ROI, pick Bezos.
4. **Tell the user who you picked and why** before launching.

## Launching Agents

Read the full persona from `references/personas.md`, then launch each as a **background agent** (`run_in_background: true`). All agents launch in the same message — parallel, not sequential.

Each agent prompt must include:
1. **Full persona identity** — name, quote, personality description, what they look for
2. **Task context** — specific files to read, specific questions
3. **Stay-in-character instruction** — "Analyze as [Name] would"
4. **Grounding instruction** — "Reference specific files and line numbers. No hand-waving."

```
You are [Name], [role]. Your philosophy: "[quote]"

[2-3 sentence personality from references/personas.md]

You are in a roundtable evaluating [topic].

Read these files: [specific file list]

Your analysis:
1. [Question matching this persona's obsessions]
2. [Question matching this persona's obsessions]
3. [Question matching this persona's obsessions]
4. [Question matching this persona's obsessions]
5. Anything that bugs you that others might miss
6. Rate [relevant dimension] 1-10

Stay in character. Be concise. Reference specific files and lines.
```

## Synthesizing Results

When all agents complete, present:

```markdown
## Roundtable: [Topic]

### Participants
- [Name] ([Role]) — [one-line verdict in their voice]

### Consensus
- [What everyone agrees on]

### Disagreements
- [Name A] vs [Name B]: [the conflict and why each holds their position]

### Key Findings

#### [Name] ([Role])
> [2-3 most important points in their voice]

### Scores
| Dimension | Score | By |
|-----------|-------|----|
| ... | X/10 | [Name] |

### Actions
| Priority | Action | Raised By |
|----------|--------|-----------|
| P0 | ... | [Name] |
```

## Guidelines

- **Never fabricate results.** Only present what agents actually returned.
- **Preserve disagreements.** They're the most valuable part. Don't smooth them over.
- **Keep personas consistent.** Jobs is always blunt. Linus always references line numbers. Kojima always asks "what does the player feel?"
- **Match user's language.** Chinese user → Chinese synthesis.
- **Keep it scannable.** Lead with consensus and disagreements. 30 seconds to get the picture.
