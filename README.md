# Task-Backward Skill

**Transform vague goals into actionable task maps through intent clarification and backward reasoning.**

[中文文档](README_CN.md) | [English](README.md)

---

## The Problem

When working with AI assistants, you've probably experienced:

- 🚨 **AI rushes to answer** — You say one sentence, AI immediately gives an answer, but it's answering the wrong question
- 🤷 **Ambiguity ignored** — The same sentence can mean multiple things, but AI only picks one interpretation without telling you
- ❓ **No "why"** — AI tells you *what* to do, but not *why* it matters or *how* it affects your goal
- 📄 **Static tutorials** — AI gives you a fixed checklist that can't adapt when you provide new information

**This Skill solves these problems.**

---

## What It Does

**Task-Backward** is an AI skill that:

1. **Lists candidate interpretations** (2-4 options) when you describe a vague goal
2. **Asks one key question** to identify the most critical fork in the road
3. **Forms a "tentative goal"** that can be revised later (doesn't force you to be certain)
4. **Backward-reasons key factors** (3-5 factors) with explanations:
   - What it is
   - Why it matters
   - How it affects your goal
   - Example scenarios
   - When it doesn't apply
5. **Generates a dynamic task map** that adjusts when you add new information
6. **Prevents drift** — Always checks which step it's on, avoids sliding into "lecture mode"

---

## Example: "I want to buy stocks"

### Without Task-Backward
```
User: I want to buy stocks
AI: Here are 5 great stocks to consider...
```
❌ AI assumed you want stock recommendations. But maybe you wanted to learn first.

### With Task-Backward
```
User: I want to buy stocks

AI: I see several possible intents:
A. Learn from zero (understand what stocks are)
B. Get stock recommendations (which stocks to buy)
C. Judge timing (when to buy)
D. Learn how to execute (open account, place order)
E. Small-scale validation (test with small amount)

The biggest fork: Are you starting from zero, or do you already 
understand stocks and want to take action?

Which is closer to your intent?

User: I want to learn first, build my own judgment, then test with 
small capital

AI: Got it. Let me backward-reason the key factors for 
"learn → build judgment → validate"...

Key Factor 1: Stock knowledge foundation
- What: Basic concepts (P/E ratio, dividends, market cap)
- Why it matters: Without these you can't read financial reports
- How it affects: Determines whether you can judge "good company"
- Example: A "good company" ≠ "current price worth buying"
- When it fails: If you only want to follow others' advice, 
  this knowledge is optional

...
```

✅ AI clarified your intent first, then backward-reasoned the factors with explanations.

---

## Is This Reinventing the Wheel?

**No.** We researched GitHub and found:

| Project | Candidate ranking | Option-based questioning | Structured confirmation | Backward reasoning | Causal explanation | Dynamic adjustment |
|---------|-------------------|--------------------------|-------------------------|-------------------|--------------------|--------------------|
| **Rasa** | ✅ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **PMAgent** | ⚠️ | ✅ | ❌ | ❌ | ❌ | ❌ |
| **TypeChat** | ❌ | ❌ | ✅ | ❌ | ❌ | ❌ |
| **Task-Backward** | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |

The last three features (backward reasoning + causal explanation + dynamic adjustment) are **unique innovations** not found in existing projects.

See [research/github-survey-2026-10.md](research/github-survey-2026-10.md) for details.

---

## Real-World Validation

### Test 1: Stock Investment Scenario
- **Input**: "I want to buy stocks"
- **Result**: AI listed 5 candidate intents → User clarified "learn first, then validate" → AI explained "good company ≠ current price worth buying" → Used quiz to check understanding
- **Outcome**: Avoided the error of "directly recommending stocks", clarified true intent
- **Score**: 9.0/10

### Test 2: Agent Configuration Scenario
- **Input**: "I keep seeing agent tutorials, I used to dismiss them, but now I realize agents need to be configured like workplace systems"
- **Result**: AI listed 4 candidate intents → User chose A+B → AI backward-reasoned 5 key factors (agent operating mechanism, work folder structure, handoff skill design, etc.) → Explained each factor
- **Outcome**: User went from "completely don't understand" to "understand configuration logic" in one conversation
- **Score**: 9.66/10

See [examples/](examples/) for complete case studies.

---

## Quick Start

### For Codex
1. Copy [skills/codex/SKILL.md](skills/codex/SKILL.md) to your Codex skills directory
2. Restart Codex or reload skills
3. Try: "I want to start a side business"

### For DeepSeek Harness (Kiro)
1. Copy [skills/harness/task-backward.md](skills/harness/task-backward.md) to your Harness skills directory
2. Restart Harness or reload skills
3. Try: "I want to learn machine learning"

### Trigger Conditions

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
- [Case Studies](docs/case-studies.md) — Complete conversation logs and analysis

---

## Strengths

1. ✅ **Solves real pain points** — "AI rushing to answer" happens in actual testing
2. ✅ **Complete and validated design** — 10-step process tested in real complex scenarios
3. ✅ **Backed by GitHub research** — No existing complete solution available
4. ✅ **Adapts to AI characteristics** — Preserves "unknown" fields, doesn't force AI to pretend certainty

---

## Limitations & Risks

1. ⚠️ **High complexity** — May pull users into 10-step process for simple questions. Need clear trigger rules.
2. ⚠️ **Understanding checks may interrupt flow** — Only check when introducing new concepts or high-risk misunderstandings
3. ⚠️ **Depends on LLM capability** — Candidate intents may be incomplete, probability scores may be inaccurate
4. ⚠️ **Video demo vs. actual functionality** — Demo shows ideal state, actual use may have errors

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

This project was inspired by real-world pain points encountered while working with AI assistants. Special thanks to:

- **Codex** — For providing the test environment and audit reports
- **GitHub community** — For existing projects (Rasa, PMAgent, TypeChat) that informed our research
- **Early testers** — For validating this skill in stock investment and agent configuration scenarios

---

## Citation

If you use this skill in your research or project, please cite:

```bibtex
@software{task_backward_skill_2026,
  title = {Task-Backward Skill: Intent Clarification and Backward Reasoning for AI Assistants},
  author = {[Your Name]},
  year = {2026},
  url = {https://github.com/[your-username]/task-backward-skill}
}
```

---

**Got questions?** Open an issue or start a discussion!

**Want to see it in action?** Check out [examples/agent-configuration.md](examples/agent-configuration.md) for a complete conversation walkthrough.
