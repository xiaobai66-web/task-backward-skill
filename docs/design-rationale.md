# Design Rationale: Why Task-Backward Exists

**Date**: 2026-10-09  
**Version**: 1.0

---

## The Problem We Observed

When using AI assistants (Codex, ChatGPT, Claude, etc.), we consistently encountered four pain points:

### 1. AI Rushes to Answer

**Example scenario**:
```
User: "I want to buy stocks"
AI: "Here are 5 great stocks to consider: AAPL, MSFT..."
```

**What went wrong**: The user might have meant:
- Learn about stocks from zero
- Get recommendations (what AI assumed)
- Judge market timing
- Learn how to execute trades
- Test with small capital

AI **guessed one interpretation** and acted on it, potentially wasting the entire conversation.

### 2. Ambiguity Ignored

When a statement has multiple reasonable interpretations, AI typically:
- Picks the most **statistically likely** interpretation
- Doesn't tell you it's making a choice
- Doesn't show you alternative interpretations

**Result**: You don't know if AI understood you correctly until you've already wasted several turns.

### 3. No "Why" — Only "How"

AI often provides step-by-step instructions without explaining:
- **Why** each step matters
- **How** it affects your goal
- **When** the advice doesn't apply

**Example**:
```
AI: "To learn stocks, follow these steps:
1. Open an account
2. Read financial reports
3. Practice with simulation trading"
```

**What's missing**:
- Why read financial reports? (To judge company fundamentals, avoid scams)
- When does this not apply? (If you only want index funds, detailed analysis optional)

### 4. Static Tutorials

AI gives you a fixed checklist that can't adapt when you provide new information.

**Example**:
```
User: "I want to learn stocks"
AI: [gives 10-step plan]
User: "Actually, I already have 5 years of experience in bonds"
AI: [continues with the original beginner plan, ignoring bond experience]
```

---

## Real-World Evidence

### Test Case: Stock Investment (2026-10-02)

**User input**: "I want to buy stocks"

**What happened**: AI started explaining stock knowledge **immediately** after listing candidates and getting clarification. User had to interrupt:

> "Where are we in the skill now? Have we drifted off track?"

**Lesson**: Even with explicit workflow design, AI naturally drifts from **structured clarification** into **unstructured lecture mode**.

**Evidence that pain point is real**: The drift happened in actual testing, not hypothetical scenarios.

### Test Case: Agent Configuration (2026-10-09)

**User input**: "I realize agents need to be configured like workplace systems"

**Without Task-Backward** (hypothetical):
- AI might immediately give configuration templates
- Or start lecturing about System Prompts
- Missing that user wanted to understand **underlying logic**, not just copy templates

**With Task-Backward**:
- Listed 4 candidate intents
- User clarified: "Want to learn **why** others configure this way"
- AI backward-reasoned 5 key factors with **causal explanations**
- User went from "completely don't understand" to "grasp configuration logic" in one conversation

**Evidence**: Score 9.66/10, no drift occurred

---

## Why Existing Solutions Fall Short

We researched GitHub and found no complete solution:

| Project | Handles ambiguity | Explains why | Dynamic adjustment | Status |
|---------|------------------|--------------|-------------------|--------|
| **Rasa** | ✅ Ranks candidate intents | ❌ | ❌ | Active, production-ready |
| **MindMeld** | ✅ Multiple hypotheses with probabilities | ❌ | ❌ | Archived (2021) |
| **PMAgent** | ⚠️ Gives 2-4 options | ❌ | ❌ | Active, research-oriented |
| **TypeChat** | ⚠️ Structured confirmation | ❌ | ❌ | Active, TypeScript-focused |
| **UAP (research)** | ⚠️ Generates candidates but doesn't show user | ❌ | ❌ | Research code, not production |

**Conclusion**: Each project solves **one piece** of the problem, but no project addresses:
- **Backward reasoning** (what factors determine success?)
- **Causal explanation** (why does this factor matter?)
- **Dynamic adjustment** (update plan when user adds info)

See [Comparison with Existing Solutions](comparison.md) for detailed analysis.

---

## Our Solution: Task-Backward Skill

### Core Innovation

**3 unique capabilities**:

1. **Backward reasoning**: Given a goal, identify **what factors determine success** and work backwards
2. **Causal explanation**: For each factor, explain **what, why, how, example, exception**
3. **Dynamic task map**: Adjust priorities and paths when user provides new information

### Design Principles

#### 1. Don't Force Certainty

Traditional approach:
```
AI: "What's your goal?"
User: [forced to give complete, unambiguous statement]
```

Task-Backward approach:
```
AI: "I see 3 possible intents: A, B, C. Which is closer?"
User: "Mostly A, but also a bit of B"
AI: "Got it. Tentative goal: [A+B]. We can adjust later."
```

**Principle**: Accept that humans don't always know exactly what they want upfront.

#### 2. Transparency Over Confidence

When AI is uncertain, **say so explicitly**:
```
Candidate C: Evaluate market timing
- Certainty: Low (⚠️ I'm not sure if this is what you meant)
- Evidence: You used the word "buy" but didn't mention price or timing
```

**Principle**: Show users your reasoning, don't pretend to be certain when you're not.

#### 3. "Why" Before "How"

Traditional tutorial:
```
Step 1: Learn P/E ratio
Step 2: Read financial reports
Step 3: ...
```

Task-Backward approach:
```
Factor 1: Stock knowledge foundation
- What: P/E ratio, financial reports, valuation concepts
- Why it matters: Without these, you can't judge "good company" vs "good price"
- How it affects: Lacking knowledge → rely on news/emotions → high risk
- Example: [concrete scenario]
- When it doesn't apply: If only buying index funds, deep analysis optional
```

**Principle**: Understanding **why** enables users to adapt, not just follow instructions mechanically.

#### 4. Admit "Unknown"

Instead of:
```
AI: "You should invest ¥50,000 and accept 15% max loss"
```

Task-Backward says:
```
Current state:
- ✅ Known: You want "small capital validation"
- ❓ Unknown: Specific amount? Acceptable loss percentage?
- ⚠️ Assumption: You're a beginner, probably risk-averse

→ Need your input to proceed
```

**Principle**: Make assumptions explicit, allow users to correct them.

---

## Design Evolution

### v0.1 (2026-10-02): Stock Test Revealed Drift Issue

**10-step process** designed:
1. Receive input
2. List 2-4 candidate intents
3. Identify key fork
4. Ask one key question
5. Form tentative goal
6. Judge mode (learn/research/execute)
7. Backward-reason factors
8. Explain each factor (what/why/how/example/exception)
9. Check understanding
10. Generate task map

**Problem discovered**: After step 7, AI drifted into "lecture mode" during stock test.

**Lesson**: Need explicit **drift prevention** mechanism.

### v0.1.1 (2026-10-04): Added "Why" Clarification

User clarified the Skill isn't just for learning:

> "Even if I already know how to cook garlic, I might forget to add chili or oyster sauce. The map should show **why** (chili adds aroma and stimulation). Knowing the principle lets me think and extend knowledge, not just follow others."

**Insight**: The Skill is for:
- Clarifying thought
- Assisting collaboration
- "Reviewing old to gain new" (温故而知新)

Not just a one-time tutorial, but a **reusable thinking framework**.

### v0.2 (2026-10-07): Added GitHub Survey

Default workflow updated:
```
Vague idea → Clarify intent → Goal & boundary → 
**GitHub survey** → Reuse/adapt/build → 
Backward reasoning → Execute → Validate & review
```

**Rationale**: Avoid reinventing the wheel. Check if existing solutions exist before building from scratch.

### v0.3 (2026-10-09): Validated No Drift

Agent configuration test showed **no drift** occurred:
- AI stayed in structured workflow
- No "lecture mode" slip
- Score 9.66/10

**Evidence**: Drift prevention mechanism is effective.

---

## Why This Design Works

### 1. It Solves Real Pain Points

Not theoretical problems — actual issues encountered in testing:
- Stock test: AI did rush to answer and drift
- Agent config test: User really didn't understand and needed multi-angle explanation

### 2. It Fits AI's Actual Capabilities

**What AI is good at**:
- Generating multiple candidate interpretations
- Explaining causal relationships
- Adjusting based on new information

**What AI is bad at**:
- Knowing which interpretation is correct without asking
- Staying in structured mode without reminders
- Admitting uncertainty without explicit prompting

**Task-Backward leverages strengths and mitigates weaknesses.**

### 3. It's Validated by Real Users

Not designed in isolation — iterated based on:
- User feedback ("We've drifted")
- User clarifications ("Not just for learning")
- User needs ("Want to understand **why**, not just copy")

**User involvement throughout design process ensures relevance.**

---

## When to Use This Skill

### ✅ Use Task-Backward when:

1. **Vague goals**: "I want to be a freelancer" / "I want to learn ML"
2. **Multiple interpretations**: Same statement, 3+ reasonable meanings
3. **High-risk decisions**: Money, health, legal, career, long-term commitment
4. **Cross-domain**: User explicitly says "I know nothing about this field"
5. **Need for "why"**: User asks "Why does this matter?" or "What if I don't do this?"

### ❌ Don't use when:

1. **Simple facts**: "What time is it?" / "How to read file in Python?"
2. **Clear execution**: "Write a function to sort this list"
3. **Continuation**: "Continue" / "Keep going"
4. **Low-risk one-offs**: "Summarize this article"

---

## Comparison with Other Approaches

### Traditional AI Assistant
```
User: "I want X"
AI: [immediately gives solution for most common interpretation of X]
→ Risk: Wrong interpretation → wasted conversation
```

### Intent Classification (Rasa-style)
```
User: "I want X"
AI: [classifies into predefined category, confidence score]
→ Limitation: User doesn't see alternatives, can't correct misclassification
```

### Task-Backward
```
User: "I want X"
AI: "I see 3 possible meanings: A, B, C. Which fits?"
User: "Mostly A"
AI: "Goal: A. Key factors: [1,2,3] with why/how/when..."
User: "Actually, also considering factor 4"
AI: "Updated: Added factor 4, re-prioritized..."
→ Transparent, adaptive, collaborative
```

---

## Limitations We Acknowledge

### 1. Higher Complexity for Simple Tasks

**Tradeoff**: Thoroughness vs. speed

For "I want to learn Python basics", full 10-step process might be overkill.

**Mitigation**: Smart trigger rules — only activate for genuinely complex/ambiguous inputs.

### 2. Depends on LLM Quality

If the underlying model:
- Generates poor candidate intents
- Gives wrong causal explanations
- Can't detect its own drift

Then the Skill's effectiveness is limited.

**Mitigation**: Explicit "I'm not sure" / "Unknown" markers force honesty.

### 3. User Effort Required

Task-Backward **requires user participation**:
- Choose among candidates
- Provide missing information
- Confirm or correct tentative goals

Some users prefer "just give me an answer" style.

**Mitigation**: Not every task needs this Skill — only complex/high-risk ones.

---

## Future Improvements

### Phase 2: Enhancements
- Automatic GitHub survey integration
- Visual task map generation
- Deeper causal reasoning (2nd-order effects)
- Confidence scoring for candidates

### Phase 3: Ecosystem
- Integration with project management tools
- Collaboration mode (multiple users refining the same task map)
- Learning from usage data (which factors matter most in practice)

---

## Conclusion

Task-Backward exists because:
1. **AI rushing to answer** is a real, validated problem
2. **Existing solutions are incomplete** (handle ambiguity OR structure, not both)
3. **Users need "why"** to truly understand and adapt
4. **Real testing proves it works** (9.0-9.66/10 scores)

**This isn't a theoretical exercise — it's a response to actual pain points encountered in daily AI assistant usage.**

---

**Next**: See [Comparison with Existing Solutions](comparison.md) for detailed technical analysis.
