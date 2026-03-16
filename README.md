<div align="center">

# Roundtable

**One prompt. Multiple experts. Real code analysis.**

**一句话召唤专家团。不是角色扮演，是真正读代码的独立分析。**

[![Claude Code](https://img.shields.io/badge/Claude_Code-Skill-8B5CF6?style=for-the-badge)](https://claude.com/claude-code)
[![MIT License](https://img.shields.io/badge/License-MIT-gold.svg?style=for-the-badge)](LICENSE)
[![Personas](https://img.shields.io/badge/21_Experts-9_Roles-ff6b6b?style=for-the-badge)](#persona-pool)

</div>

---

## What is this?

A Claude Code skill that launches **parallel expert agents** to analyze your code, plan features, or evaluate decisions from multiple professional perspectives — simultaneously.

Say "let's discuss this" or "roundtable: evaluate my architecture", and the skill:

1. **Selects 3-5 experts** from a pool of 21 named personas across 9 roles
2. **Launches them in parallel** as independent background agents (each reads real code)
3. **Synthesizes their findings** into a structured discussion — consensus, disagreements, and actions

这是一个 Claude Code 技能：用一句话召集 3-5 位专家，并行分析你的代码/方案/架构，然后综合成结构化的圆桌讨论结果。

## Why?

One reviewer finds bugs. Five experts from different disciplines find **different categories of problems**.

A PM asks "should we even build this?" while a security engineer asks "what happens with malicious input?" while a game designer asks "does the player feel heard?" — and they all read the same codebase, independently, in parallel.

| Approach | What you get |
|----------|-------------|
| You reviewing alone | Your blind spots stay blind |
| One AI reviewer | One perspective, one set of biases |
| **Roundtable** | PM + Engineer + Researcher + Designer argue it out, surface disagreements |

The most valuable output isn't what everyone agrees on — it's **where the experts disagree**.

---

## Quick Start

### Install

```bash
# Copy to your Claude Code skills directory
git clone https://github.com/YOUR_USERNAME/roundtable.git ~/.claude/skills/roundtable
```

Or download and place manually:

```
~/.claude/skills/roundtable/
├── SKILL.md
└── references/
    └── personas.md
```

### Use

Just talk naturally:

```
> roundtable: should we add caching to the API layer?
> let's get the team to discuss this PR
> have the experts evaluate our auth implementation
> 圆桌讨论：这个方案合理吗
```

The skill auto-selects relevant experts and launches them.

---

## Persona Pool

21 experts across 9 roles. Each roundtable randomly picks **different personas** based on what the discussion needs — so the same question asked twice gets different perspectives.

### Product Managers

| Persona | Style | Best For |
|---------|-------|----------|
| **乔布斯** | "Saying no to 1000 things." Cuts ruthlessly. Will say "this is shit." | Scope decisions, killing features |
| **张小龙** | "好产品是用完即走的。" Treats users as humans, not data. | User psychology, habit design |
| **俞军** | "用户价值 = 新体验 - 旧体验 - 替换成本" Everything is an equation. | ROI analysis, value decomposition |

### Agent Engineers

| Persona | Style | Best For |
|---------|-------|----------|
| **哲** | Sees everything as sense→think→act→observe loops. Paranoid about silent failures. | Agent architecture, file contracts |
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
| **小岛秀夫** | "A game is not about mechanics. It's about moments." | Emotional design, player agency |
| **宫本茂** | Designs for the smile in the first 10 seconds. Subtraction design. | Onboarding, intuitive UX |
| **宫崎英高** | "Accomplishment must be earned." Pain IS the product. | Difficulty curves, reward balance |

### Security Engineers

| Persona | Style | Best For |
|---------|-------|----------|
| **吴翰清** | "Every input is hostile." Traces injection paths. | API security, trust boundaries |
| **Mitnick** | Thinks like an attacker. Humans are the weakest link. | Threat modeling, social engineering |

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

## How It Works

```
You: "roundtable: evaluate this feature plan"
         │
         ▼
   ┌─────────────┐
   │ Role Select  │  Analyze task → pick 3-5 relevant roles
   │ (automatic)  │  → pick persona per role (varies each time)
   └──────┬──────┘
          │
    ┌─────┼─────┬─────┐
    ▼     ▼     ▼     ▼
  ┌───┐ ┌───┐ ┌───┐ ┌───┐
  │乔布│ │Lin│ │Hin│ │小岛│   Each agent runs independently
  │斯  │ │us │ │ton│ │秀夫│   in the background, reading
  │   │ │   │ │   │ │   │   real code and files
  └─┬─┘ └─┬─┘ └─┬─┘ └─┬─┘
    │     │     │     │
    └─────┼─────┼─────┘
          ▼
   ┌─────────────┐
   │  Synthesize  │  Consensus → Disagreements → Actions
   └─────────────┘
```

### Output Format

```markdown
## Roundtable: [Topic]

### Participants
- 乔布斯 (PM) — "Kill feature B. Ship A and C."
- Linus (Reviewer) — "Race condition on line 47. Fix before anything."

### Consensus
- Everyone agrees: the feedback loop must close visibly

### Disagreements
- 乔布斯 says cut NPC affinity. 小岛秀夫 says it's the emotional core.

### Actions
| Priority | Action | Raised By |
|----------|--------|-----------|
| P0 | Fix race condition | Linus |
| P1 | Ship feedback visibility | 乔布斯 + 小岛秀夫 |
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

Edit `references/personas.md` to add domain-specific experts:

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
> → PM evaluates ROI, Architect designs the pub/sub, Security checks for spam vectors

**Post-implementation review:**
> "roundtable: review the changes I just made to the auth module"
> → Linus finds the edge case, Security traces the trust boundary, SRE asks about failure modes

**Architecture decision:**
> "the team should discuss whether to use WebSockets or SSE for real-time updates"
> → Architect compares patterns, SRE evaluates operational cost, UX considers perceived latency

**Game design:**
> "圆桌讨论：玩家反馈系统的设计"
> → 小岛秀夫 focuses on emotional payoff, 宫本茂 on intuitive interaction, PM on scope

---

## Requirements

- **Claude Code** (CLI) with background agent support
- Works with any Claude model (Opus 4.6 recommended for best persona adherence)

---

## License

MIT — Use it, fork it, add your own experts.

<div align="center">

*The most valuable insight is where the experts disagree.*

*最有价值的洞察，藏在专家们的分歧里。*

</div>
