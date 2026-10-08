# Task-Backward Skill

> **⚠️ Notice: This project is archived**  
> This project has been redesigned into two separate skills with better functionality and clearer structure.  
> **Please visit the new version: https://github.com/xiaobai66-web/ai-intent-skills**  
> 
> This repository is kept as a historical reference and is no longer maintained.

---

**AI often rushes to answer. You say one sentence and it starts talking, but it's answering the wrong question.**

This Skill fixes that.

[中文文档](README_CN.md) | [English](README.md)

---

## What's the Problem

When using AI assistants, you've probably hit these:

- 🚨 **AI rushes ahead** — You say "I want to buy stocks" and it immediately recommends 5 stocks, but you actually wanted to learn first
- 🤷 **Ambiguity ignored** — The same sentence can mean several things, but AI picks one and runs with it without telling you why
- ❓ **Results without reasons** — AI tells you "do market research" but not why it matters or what happens if you skip it
- 📄 **Fixed checklists** — AI gives you a static list that won't adjust when you add new information

This Skill solves these problems.

---

## What It Does

You give it a vague goal (like "I want to start a side business"), and it will:

1. **List possible interpretations** (Do you want to learn how? Already decided and need help choosing what? Want to know if it's legal?)
2. **Ask one key question** to confirm what you actually want
3. **Form a "tentative goal"** that can be revised later (doesn't force you to be 100% clear upfront)
4. **Backward-reason key factors** (side business needs: product selection, customers, location, costs...), explaining each:
   - What it is
   - Why it matters
   - How it affects your goal
   - Example scenarios
   - When you can ignore it
5. **Generate a dynamic task map** that adjusts when you add information
6. **Prevent drift** — Always checks which step it's on, avoids sliding into "lecture mode"

---

## Example: "I want to buy stocks"

### Without Task-Backward

```
User: I want to buy stocks
AI: Here are 5 great stocks to consider...
```
❌ AI assumed you want recommendations. But maybe you wanted to learn first.

### With Task-Backward

```
User: I want to buy stocks

AI: I see several possible intents:
A. Learn from zero (understand what stocks are)
B. Get recommendations (which stocks to buy)
C. Judge timing (is now a good time)
D. Learn how to execute (open account, place order)
E. Small-scale validation (test with a small amount)

The biggest fork: Are you starting from zero, or do you already 
understand stocks and want to take action?

Which is closer to your intent?

User: I want to learn first, build my own judgment, then test with 
a small amount

AI: Got it. Let me backward-reason the key factors for 
"learn → build judgment → validate"...

Key Factor 1: Stock knowledge foundation
- What: Basic concepts (P/E ratio, dividends, market cap)
- Why it matters: Without these you can't read financial reports
- How it affects: Determines whether you can judge "good company"
- Example: A "good company" ≠ "current price worth buying"
- When it doesn't matter: If you only want to follow others' advice, 
  you can skip this

...
```

✅ AI clarified your intent first, then backward-reasoned the factors with full explanations.

---

## Is This Reinventing the Wheel?

**Nope.** I checked GitHub:

| Project | Candidate ranking | Option-based questioning | Structured confirmation | Backward reasoning | Causal explanation | Dynamic adjustment |
|---------|-------------------|--------------------------|-------------------------|-------------------|--------------------|--------------------|
| **Rasa** | ✅ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **PMAgent** | ⚠️ | ✅ | ❌ | ❌ | ❌ | ❌ |
| **TypeChat** | ❌ | ❌ | ✅ | ❌ | ❌ | ❌ |
| **Task-Backward** | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |

The last three features (backward reasoning + causal explanation + dynamic adjustment) are **unique** — no existing GitHub project does all of these.

Full research: [research/github-survey-2026-10.md](research/github-survey-2026-10.md).

---

## Does It Actually Work?

### Test 1: Stock Investment Scenario
- **Input**: "I want to buy stocks"
- **What happened**: AI listed 5 candidates → I said "learn first, then validate" → AI explained "good company ≠ current price worth buying" → Used quiz to check understanding
- **Result**: Avoided the "recommend stocks immediately" error, clarified true intent
- **Score**: 9.0/10

### Test 2: Agent Configuration Scenario
- **Input**: "I keep seeing agent tutorials, used to dismiss them, but now I realize agents need to be configured like workplace systems"
- **What happened**: AI listed 4 candidates → I chose A+B → AI backward-reasoned 5 key factors (agent operating mechanism, work folder structure, handoff skill design, etc.) → Explained each factor
- **Result**: Went from "completely don't understand" to "understand configuration logic" in one conversation
- **Score**: 9.66/10

Full cases: [examples/](examples/).

---

## How to Use

### For Codex Users
1. Copy [skills/codex/SKILL.md](skills/codex/SKILL.md) to your Codex skills directory
2. Restart Codex or reload skills
3. Try: "I want to start a side business"

### For DeepSeek Harness (Kiro) Users
1. Copy [skills/harness/task-backward.md](skills/harness/task-backward.md) to your Harness skills directory
2. Restart Harness or reload skills
3. Try: "I want to learn machine learning"

### When It Triggers

**Will trigger:**
- ✅ "I want to be a freelancer" (vague goal)
- ✅ "I want to learn machine learning" (needs decomposition)
- ✅ "I want to buy stocks" (multiple interpretations + high risk)
- ✅ "Saw AI-generated video, want to build tools" (cross-domain)

**Won't trigger:**
- ❌ "What time is it?" (simple fact)
- ❌ "Help me write a function" (clear execution)
- ❌ "Continue" (context continuation)

---

## Documentation

- [Design Rationale](docs/design-rationale.md) — Why we built this
- [Comparison with Existing Solutions](docs/comparison.md) — Detailed comparison with Rasa, PMAgent, TypeChat, etc.
- [Case Studies](examples/) — Complete conversation logs and analysis

---

## Strengths

1. ✅ **Solves real pain points** — "AI rushing to answer" actually happened in testing
2. ✅ **Complete and validated design** — 10-step process tested in real complex scenarios
3. ✅ **Not reinventing the wheel** — No existing complete solution on GitHub
4. ✅ **Adapts to AI characteristics** — Preserves "unknown" fields, doesn't force AI to pretend certainty

---

## Limitations & Risks

1. ⚠️ **Could be too complex** — Simple questions might get pulled into the 10-step process. Need clear trigger rules.
2. ⚠️ **Understanding checks may interrupt flow** — Only check when introducing new concepts or high-risk misunderstandings
3. ⚠️ **Depends on LLM capability** — Candidate intents may be incomplete, probability scores may be inaccurate
4. ⚠️ **Demo video vs. actual functionality** — Video shows ideal state, actual use may have errors

---

## Roadmap

### Phase 1: MVP (Current)
- ✅ Intent clarification (2-4 candidates)
- ✅ Key question identification
- ✅ Simplified backward reasoning (3-5 factors)
- ✅ Causal explanations
- ✅ Simplified task map

### Phase 2: Enhancements (Planned)
- ⏳ Understanding check mechanism
- ⏳ Dynamic task map visualization
- ⏳ Deeper causal explanation
- ⏳ Automatic GitHub survey

### Phase 3: Polish (Ongoing)
- 🔄 Collect real-world usage data
- 🔄 Identify common drift scenarios
- 🔄 Optimize trigger conditions
- 🔄 Improve candidate quality

---

## Contributing

Contributions welcome! Especially:

- 🐛 Bug reports (drift cases, wrong candidates, etc.)
- 💡 New use cases (domains we haven't tested)
- 📝 Documentation improvements
- 🎯 Trigger condition optimizations

---

## License

MIT License - see [LICENSE](LICENSE)

---

## Acknowledgments

This project came from real pain points encountered while working with AI assistants. Special thanks to:

- **Codex** — For providing the test environment and audit reports
- **GitHub community** — For existing projects (Rasa, PMAgent, TypeChat) that informed our research
- **Early testers** — For validating this skill in stock investment and agent configuration scenarios

---

## Citation

If you use this skill in your research or project, you can cite it like this:

```bibtex
@software{task_backward_skill_2026,
  title = {Task-Backward Skill: Intent Clarification and Backward Reasoning for AI Assistants},
  author = {xiaobai66-web},
  year = {2026},
  url = {https://github.com/xiaobai66-web/task-backward-skill}
}
```

---

**Got questions?** Open an issue or start a discussion!

**Want to see it in action?** Check out [examples/agent-configuration.md](examples/agent-configuration.md) for a complete conversation walkthrough.
