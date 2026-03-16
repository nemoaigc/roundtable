<div align="center">

# Roundtable

**One prompt. Multiple experts. Real code analysis.**

[![Claude Code](https://img.shields.io/badge/Claude_Code-Skill-8B5CF6?style=for-the-badge)](https://claude.com/claude-code)
[![MIT License](https://img.shields.io/badge/License-MIT-gold.svg?style=for-the-badge)](LICENSE)
[![Personas](https://img.shields.io/badge/21_Experts-9_Roles-ff6b6b?style=for-the-badge)](#persona-pool)

</div>

---

## The Problem

You just built something. You review it yourself. Ship it. Then at 3am a race condition crashes production, a user finds an injection vector, and the PM asks why you shipped a feature nobody wanted.

**One pair of eyes has one set of blind spots.** A backend engineer won't think about player emotion. A PM won't catch the mutex you forgot. A game designer won't notice the SQL injection.

## The Solution

Roundtable launches **3-5 independent expert agents in parallel** — each with a distinct professional persona, reading your actual code — then synthesizes their findings into a structured discussion. Not merged consensus. **Preserved disagreements.** Because the most valuable insight is where Jobs says "kill it" and Kojima says "it's the emotional core."

```
You: "roundtable: evaluate this feature plan"
         │
         ▼
   ┌─────────────┐
   │ Role Select  │  Analyze task → pick 3-5 from 21 experts
   │ (automatic)  │  → different experts each time
   └──────┬──────┘
          │
    ┌─────┼─────┬─────┐
    ▼     ▼     ▼     ▼
  ┌─────┐┌─────┐┌──────┐┌───────┐
  │Jobs ││Linus││Hinton││Kojima │  Each reads real code
  │(PM) ││(Rev)││(AI)  ││(Game) │  independently, in parallel
  └──┬──┘└──┬──┘└──┬───┘└──┬────┘
     │      │      │       │
     └──────┼──────┼───────┘
            ▼
   ┌──────────────┐
   │  Synthesize   │  Consensus → Disagreements → Actions
   └──────────────┘
```

---

## Quick Start

### Install

```bash
git clone https://github.com/nemoaigc/roundtable.git ~/.claude/skills/roundtable
```

### Use

Just talk naturally:

```
> roundtable: should we add caching to the API layer?
> let's get the team to discuss this PR
> have the experts evaluate our auth implementation
```

The skill auto-selects relevant experts and launches them.

---

## Persona Pool

21 experts across 9 roles. Each roundtable picks **different personas** based on what the discussion needs — so the same question asked twice gets different perspectives.

### Product Managers

| Persona | Style | Best For |
|---------|-------|----------|
| **Jobs** | "Saying no to 1000 things." Cuts ruthlessly. Will call it shit if it's shit. | Scope decisions, killing features |
| **Butterfield** | "Every great product starts with a human problem." Watches users before asking. | User empathy, daily friction |
| **Bezos** | "Start with the customer and work backwards." Writes the press release first. | ROI, flywheel effects, one-way doors |

### Agent Engineers

| Persona | Style | Best For |
|---------|-------|----------|
| **Swyx** | Sees everything as sense→think→act→observe loops. Paranoid about silent failures. | Agent architecture, file contracts |
| **Andrew Ng** | "Agentic workflows drive massive progress." Builds data flywheels. | Feedback loops, learning systems |

### Code Reviewers

| Persona | Style | Best For |
|---------|-------|----------|
| **Linus** | "Talk is cheap. Show me the code." Finds the bug on line 47. | Bug hunting, race conditions |
| **Carmack** | Reviews from first principles. Hates unnecessary abstractions. | Performance, simplification |

### AI/ML Researchers

| Persona | Style | Best For |
|---------|-------|----------|
| **Hinton** | "Why 0.5?" Skeptical of every threshold and heuristic. | Pipeline quality, signal vs noise |
| **Karpathy** | "The most common error is not running the code." Builds first. | Prompt engineering, LLM behavior |
| **Fei-Fei Li** | "What data is teaching this system?" Human-centered AI. | Data quality, AI ethics |

### Game Designers

| Persona | Style | Best For |
|---------|-------|----------|
| **Kojima** | "A game is not about mechanics. It's about moments." | Emotional design, player agency |
| **Miyamoto** | Designs for the smile in the first 10 seconds. Subtraction design. | Onboarding, intuitive UX |
| **Miyazaki** | "Accomplishment must be earned." Pain IS the product. | Difficulty curves, reward balance |

### Security Engineers

| Persona | Style | Best For |
|---------|-------|----------|
| **Schneier** | "Security is not a product, but a process." Thinks in threat models. | Threat modeling, trust boundaries |
| **Mitnick** | Thinks like an attacker. Humans are the weakest link. | Penetration testing, social engineering |

### UX Designers

| Persona | Style | Best For |
|---------|-------|----------|
| **Don Norman** | Father of UX. Affordances, signifiers, mental models. | Information architecture, confusion |
| **Dieter Rams** | "Good design is as little design as possible." | Visual cleanup, removing clutter |

### DevOps / SRE

| Persona | Style | Best For |
|---------|-------|----------|
| **Ben Treynor** | "Hope is not a strategy." Invented SRE at Google. | Failure modes, reliability |
| **Kelsey Hightower** | Makes complex infra feel simple. "Do you need this?" | Simplification, build vs buy |

### System Architects

| Persona | Style | Best For |
|---------|-------|----------|
| **Martin Fowler** | "Good programmers write code that humans understand." | Refactoring, module boundaries |
| **Leslie Lamport** | "A computer you didn't know existed can break yours." | Distributed systems, consistency |

---

## Output Format

```markdown
## Roundtable: [Topic]

### Participants
- Jobs (PM) — "Kill feature B. Ship A and C."
- Linus (Reviewer) — "Race condition on line 47. Fix before anything."

### Consensus
- Everyone agrees: the feedback loop must close visibly

### Disagreements
- Jobs says cut NPC affinity. Kojima says it's the emotional core.

### Actions
| Priority | Action | Raised By |
|----------|--------|-----------|
| P0 | Fix race condition | Linus |
| P1 | Ship feedback visibility | Jobs + Kojima |
```

---

## What Makes This Different

| Feature | Other tools | Roundtable |
|---------|------------|-----------|
| **Perspectives** | Same-domain (multiple code reviewers) | **Cross-discipline** (PM + Security + Game Designer) |
| **Personas** | Generic ("agent-1", "security-sentinel") | **Named characters** with distinct thinking styles |
| **Variety** | Same agents every time | **Random selection** from pool — same question, different insights |
| **Integration** | Framework / config required | **One-sentence trigger** via Claude Code skill |
| **Output** | Merged consensus | **Preserved disagreements** — conflicts are the most valuable part |

---

## Customization

### Add Your Own Personas

Edit `references/personas.md`:

```markdown
### Your Expert · The Title
> "Their signature quote."

Personality description. What they obsess over. How they think.

**Looks for**: What they notice that others miss
**Best when**: When to pick this persona over alternatives
```

### Adjust Selection Rules

Edit the role table in `SKILL.md` to add new roles or change when they trigger.

---

## Examples

**Feature planning:**
> "roundtable: we want to add a notification system. discuss."
> → PM evaluates ROI, Architect designs pub/sub, Security checks for spam vectors

**Post-implementation review:**
> "roundtable: review the changes I just made to the auth module"
> → Linus finds the edge case, Schneier traces the trust boundary, SRE asks about failure modes

**Architecture decision:**
> "the team should discuss whether to use WebSockets or SSE"
> → Lamport evaluates consistency, Kelsey Hightower asks "do you need this?", Carmack checks perf

**Game design:**
> "roundtable: evaluate the player feedback system"
> → Kojima focuses on emotional payoff, Miyamoto on intuitive interaction, Jobs on scope

---

## Background

This skill was born from building [Hermes Quest](https://github.com/nemoaigc/hermes-quest) — a gamified RPG dashboard for an AI agent. During development, we ran roundtable discussions with 5+ expert personas to evaluate features, review code, and plan architecture. The pattern worked so well that we extracted it into a reusable skill.

Key insight: **a PM, a game designer, and a code reviewer looking at the same codebase find completely different categories of problems.** The PM found that the feedback loop was "a promise, not an experience." The code reviewer found a race condition in the timer cleanup. The game designer found that the core emotional beat was invisible. None of them would have caught what the others found.

Multi-agent debate is [an active research area](https://news.mit.edu/2023/multi-ai-collaboration-helps-reasoning-factual-accuracy-language-models-0918) — it improves reasoning and reduces hallucination. Roundtable brings this to everyday development with named personas that produce genuinely different analysis angles.

---

## Requirements

- **Claude Code** (CLI) with background agent support
- Works with any Claude model (Opus recommended for best persona adherence)

## License

MIT — Use it, fork it, add your own experts.

<div align="center">

*The most valuable insight is where the experts disagree.*

</div>
