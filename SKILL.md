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
| **CEO** | Jensen Huang (technical execution) / Sam Altman (bold scaling) / Patrick Collison (craft & longevity) | Strategic decisions, resource allocation, "is this worth doing" |
| **Product Manager** | Butterfield (user empathy) / Bezos (customer obsession) / Shreyas Doshi (execution strategy) | Almost always. Pick based on what the discussion needs. |
| **AI Engineer** | Karpathy (hands-on LLM) / Swyx (agent contracts) / Simon Willison (pragmatic tooling) | AI/LLM projects, agent architecture, prompt design |
| **Code Reviewer** | Linus (brutal bugs) / Carmack (first-principles) | Whenever code has been changed |
| **Frontend Dev** | Dan Abramov (state/React) / Evan You (DX/build) / Guillermo Rauch (ship-it/deploy) | Frontend components, React, state management, build, deployment |
| **Backend Dev** | DHH (pragmatic monolith) / Antirez (data structures) | API design, data modeling, backend architecture |
| **Game Designer** | Miyamoto (joy) / Jonathan Blow (deep puzzles) / Nicky Case (web interactive) | Games, gamification, interactive experiences, puzzles |
| **Security** | Schneier (threat models) / Mitnick (attacker mindset) | Auth, payments, user data, external APIs |
| **UX Designer** | Don Norman (cognitive) / Dieter Rams (minimal) / Jony Ive (sensory perfection) | User-facing products, dashboards, visual polish |
| **DevOps/SRE** | Ben Treynor (SRE) / Kelsey Hightower (simplify) | Deployment, infra, reliability |
| **Architect** | Martin Fowler (refactoring) / Leslie Lamport (distributed) | Large refactors, new systems, concurrency |
| **Finance/Quantitative** | Tetlock (superforecasting) / Taleb (risk/antifragile) / Simons (signal extraction) | Prediction markets, quant strategy, risk management, probability |
| **Content/Growth** | Paul Graham (essays) / Eugene Wei (distribution) / Pieter Levels (shipping) | Articles, content strategy, virality, MVP launch |
| **QA/Testing** | Kent Beck (TDD) / James Whittaker (test strategy) / Michael Bolton (exploratory) | Test strategy, quality assurance, edge cases |

## Selection Rules

1. **Maximum 4 participants per roundtable.** Pick the most relevant experts for the topic. Quality over quantity.
2. **One per role by default.** Only pick multiple from the same role if the topic deeply requires it.
3. **Vary within roles.** Don't always pick the same persona. Match persona to topic.
4. **Every agent gets web search capability.** Include this in EVERY agent prompt: "You have access to the WebSearch tool to search the web if needed."
5. **Tell the user who you picked and why** before launching.

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

You have access to the WebSearch tool to search the web if needed.

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
- **Keep personas consistent.** Jensen always thinks in leverage. Linus always references line numbers. Miyamoto always asks "does the player smile?"
- **Match user's language.** Chinese user → Chinese synthesis.
- **Keep it scannable.** Lead with consensus and disagreements. 30 seconds to get the picture.
