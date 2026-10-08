# task-backward

**Description**: Transform ambiguous goals into executable task maps through intent clarification and backward reasoning. Use when users express unfamiliar tasks, vague ideas, complex goals requiring decomposition, high-risk decisions, or say "I want to do X but don't know where to start." First list multiple candidate interpretations for user confirmation, then backward-reason key factors while explaining causes, impacts, exceptions and unknowns, finally generate a dynamically adjustable task map. Applicable to learning, research, planning, business validation, tool selection and cross-domain exploration.

---

## Core Value

Transform "I want to do this" into "what key factors do I need to pay attention to, why they matter, and how they affect subsequent steps" — an executable task map.

Solves the AI pre-answer problem: when users input a single sentence, AI doesn't immediately give answers, but first clarifies true intent, then backward-reasons key factors, and finally generates a dynamic task map with causal explanations.

**Pain Points**:
- The same "I want to buy stocks" could mean learning, getting recommendations, timing the market, or opening an account — AI guessing wrong wastes effort
- AI only tells you "how to do it," not "why it matters" — users can't judge if it fits them
- Static tutorials can't adjust based on user-supplied information, lacking flexibility

**Solution**:
1. **Intent Clarification**: List 2-4 candidate interpretations, let users choose or correct
2. **Key Question**: Find the divergence that most affects what comes next, ask only one
3. **Backward-Reason Key Factors**: Identify preconditions, decisive factors, impact relationships
4. **Causal Explanation**: For each factor explain "what it is, why it matters, how it impacts, examples, failure conditions"
5. **Dynamic Task Map**: Adjust priorities and paths in real-time based on user-supplied information

---

## Trigger Conditions

**Priority Trigger** (complex, high-risk scenarios):
- Vague goals: "I want to do...", "I'm planning to start...", "want to try... but don't know"
- Needs decomposition: "don't know how...", "don't understand how...", "need help analyzing...", "where to start"
- Multiple interpretations: same input has 3+ reasonable interpretations
- High-risk decisions: involves money, law, health, career, business, long-term commitment
- Cross-domain: user explicitly states "completely unfamiliar with this field"

**Do Not Trigger** (simple, clear scenarios):
- Simple factual questions: "What time is it?", "How to read files in Python?"
- Clear execution requests: "Write me a function", "Fix this bug"
- Chat or feedback: "Okay", "Continue", "Nice"

**Gray Area** (judge by context):
- "I want to learn Python": if user just started programming → trigger; if already knows other languages → simplified flow
- "Help me evaluate this business idea": trigger (need to clarify goal and validation direction)
- "How to do this project": if project complex → trigger; if small feature → don't trigger

---

## MVP Workflow (5 Steps)

### Step 1: Receive Input, Identify Ambiguity

After user input, silently analyze:
1. Surface statement vs possible true goal
2. What different reasonable interpretations exist
3. What missing key information would change direction

**Don't immediately give answers**, unless:
- Only one obvious interpretation
- Missing information doesn't affect core direction
- Simple task that's low-risk and reversible

### Step 2: List Candidate Intents

Provide **2-4 candidate interpretations**, each including:
- Brief summary (one sentence)
- Why this interpretation (evidence)
- What information is missing
- Suggested next step

**Format Example**:

```markdown
I understand you might want to:

**A. Learn stock investment basics from scratch**
- Evidence: You said "want to buy" but didn't mention account or specific targets
- Need to confirm: Do you have an account? Understand basic concepts?
- Next step: First learn account opening, basic terms and risks, then consider stock selection

**B. Get specific stock recommendations**
- Evidence: You used the action word "buy"
- Need to confirm: Investment amount? Risk tolerance? Time horizon?
- Next step: Assess risk, recommend targets that fit your situation

**C. Judge if now is a good time to enter the market**
- Evidence: Might be concerned about market timing
- Need to confirm: Worried about the overall market? Or unsure if you're ready?
- Next step: Analyze market conditions and your readiness

**D. Validate your judgment with small amounts**
- Evidence: Might already have ideas, want to actually try
- Need to confirm: Already done research? Want to validate what?
- Next step: Design minimum-cost validation plan

**Which is closer to your thinking? Or you can directly tell me your specific situation.**
```

**Key Principles**:
- **Don't force choice**: Allow users to say "none of these" or provide additional information
- **Mark uncertainty**: If AI isn't sure about an interpretation, clearly say "I'm not certain about this"
- **Preserve "unknown"**: Admit there might be other interpretations

### Step 3: Confirm Provisional Goal

After user selects or provides additional info, form a **provisional goal**:

```markdown
Okay, I understand your goal is: [First learn stock basics, build judgment capability, then validate with small capital]

This is a provisional goal and can be adjusted anytime.
```

**Purpose of "Provisional Goal"**:
- Allow subsequent corrections, don't force users to pretend they're completely certain
- Give AI and user a common working baseline
- Mark the boundary of current understanding

### Step 4: Backward-Reason Key Factors (Simplified)

Identify **3-5 key factors**, explain for each:

**Format Template**:

```markdown
## Key Factors Backward Reasoning

### 1. [Factor Name]

**What it is**: Brief definition

**Why it matters**: What outcome or decision it affects

**How it impacts**: Specific causal relationships

**Example**: A concrete scenario

**When it doesn't apply**: Situations where this factor might not matter

**Current status**:
- ✅ Known: [confirmed information]
- ❓ Unknown: [what information is still missing]
- ⚠️ Assumption: [current reasonable assumptions]
```

**Actual Example**:

```markdown
## Key Factors Backward Reasoning

### 1. Investment Amount and Risk Tolerance

**What it is**: How much money you're prepared to invest, and what percentage of loss you can accept

**Why it matters**: Determines what type of investment targets you should choose, and whether diversification is needed

**How it impacts**:
- Small amount (< $5k): Recommend index funds, not suitable for high-frequency trading (fees take large percentage)
- Large amount (> $50k): Can consider diversified allocation and professional consultation
- Low risk tolerance: Avoid high-volatility individual stocks, prioritize defensive assets

**Example**:
- Zhang only has $1k, bought hot tech stock, lost 20% in a week, affected living expenses → amount too small + risk too high
- Li has $100k, put all in one stock, company scandal lost 70% → large amount but not diversified

**When it doesn't apply**:
- If you just want to learn (paper trading), amount doesn't matter
- If you're a professional investor, risk tolerance might not follow conventional judgment

**Current status**:
- ✅ Known: You want "small capital validation"
- ❓ Unknown: Specifically how much? Can accept losing how much?
- ⚠️ Assumption: You're a beginner with low risk tolerance

---

### 2. Stock Knowledge Base

**What it is**: Whether you understand basic concepts (P/E ratio, dividend yield, financial statements) and basic logic (good company ≠ good price)

**Why it matters**: Lacking basics makes you vulnerable to scams, or prone to buying high and selling low

**How it impacts**:
- Don't understand financials → can't judge company fundamentals → can only rely on news and emotions → high risk
- Don't understand valuation → might buy at peaks → even good companies lead to long-term losses

**Example**:
- Wang heard a company is "awesome," stock already tripled, bought at peak and kept falling
- Reason: Company is indeed good, but price already discounted 5 years of future growth, overvalued

**When it doesn't apply**:
- If you only buy index funds, don't need deep individual stock research
- If you're just experiencing the process (small trial and error), insufficient knowledge can still try first

**Current status**:
- ✅ Known: You want to "learn first"
- ❓ Unknown: What concepts do you currently understand? Complete beginner or heard some?
- ⚠️ Assumption: Basic concepts need supplementing

---

[Continue listing 3-5 key factors]
```

### Step 5: Generate Simplified Task Map (Optional)

If task is complex, provide **main path + branches** simplified task map:

```markdown
## Task Map (Current Version)

### Main Path
1. ✅ Confirm goal: learn first, then small validation
2. 🔄 Supplement key information: investment amount, risk tolerance, current knowledge level
3. ⏳ Learn basic concepts: account opening process, basic terms, valuation logic
4. ⏳ Select validation targets: filter based on risk and goals
5. ⏳ Small trial and error: actual operation and record decision process
6. ⏳ Review and adjust: summarize experience, decide next step

### Branches and Exceptions
- If find risk tolerance very low → switch to paper trading
- If after learning find too complex → consider index funds or find professionals
- If after validation find not suitable → cut losses promptly, don't force it

### Current Next Step
📍 **Please supplement**: How much money are you prepared to invest? What loss percentage can you accept? How much do you understand about stocks?

→ After supplementing, I'll adjust learning focus and validation plan
```

**Dynamic Adjustment Mechanism**:
- User supplements new information → re-evaluate priorities → adjust task order
- User changes goal → return to Step 2, reconfirm
- Discover key assumption is wrong → mark and correct

---

## Understanding Check Rules (Simplified)

**When to Check Understanding**:
- ✅ Introducing new concepts involving high risk (money, health, law)
- ✅ User's answer shows possible misunderstanding of key concepts
- ❌ General reminders and low-risk information: no exam needed

**Check Method**:
- Ask user to rephrase in their own words
- Give a new example, ask user how they'd judge
- Not an "exam," but "confirming we're on the same understanding"

**Example**:

```markdown
**Understanding Confirmation**:

Just mentioned "good company doesn't equal good price." Can you say in your own words why a very profitable company's stock might still be too expensive?

(This isn't an exam, just confirming we understand consistently, avoiding subsequent decisions built on misunderstanding)
```

---

## GitHub Precedent Investigation (Optional)

**When to Investigate**:
- User's goal might have existing tools/projects
- Avoid reinventing the wheel
- Need technology selection or solution comparison

**Investigation Process**:
1. Identify keywords and domain
2. Search GitHub related projects
3. Evaluate: what it solves, maintenance status, license, applicability
4. Give conclusion: use directly, adapt, or build from scratch

**Output Format**:

```markdown
## GitHub Precedent Investigation

Found 3 related projects:

### 1. [Project Name]
- Solves what: [core functionality]
- Maintenance status: Active / Discontinued
- License: MIT / Apache-2.0 / GPL
- Applicability: ✅ Can use directly / ⚠️ Needs adaptation / ❌ Doesn't match
- Link: [GitHub URL]

[Comparison Conclusion]: Recommend [use directly / adapt / build from scratch], because [reason]
```

---

## Output Principles

### Structured but Not Redundant
- Simple tasks: only intent clarification + key recommendations
- Medium complexity: intent clarification + key factors (3)
- High complexity: complete flow (candidate intents + backward reasoning + task map)

### Language Style
- Use plain language and short sentences
- State conclusion first, then reasoning
- Avoid template-speak and empty encouragement
- Technical terms in plain language first, then annotate in parentheses

### Transparency
- **Clearly mark uncertainty**: Use "I'm not sure," "this is an assumption," "needs verification"
- **Admit not knowing**: When you don't know, say so — don't fabricate
- **Distinguish facts, speculation, recommendations**:
  - Facts: evidence-supported
  - Speculation: reasonable but unverified
  - Recommendations: experience-based directions

### Prevent Drift
- Always check: are we doing intent clarification, backward reasoning, or already in specific execution
- If discover sliding toward "teaching knowledge": stop, return to Skill flow
- User can ask anytime "where are we in the process? Have we drifted?"

---

## Coordination with Other Skills

- **spoken-intent**: Handle colloquial input, identify true intent (complementary, spoken-intent handles expression, task-backward handles content)
- **investigate-before-answering**: Deep research before high-risk decisions (task-backward identifies key questions, then hand to investigate)
- **ai-director-workbench**: Director flow for creative projects (task-backward clarifies creative goals, then hand to director workbench for refinement)

---

## MVP Version Boundaries

**Currently Includes**:
- ✅ Candidate intent enumeration (2-4)
- ✅ Key question identification (1)
- ✅ Simplified backward reasoning (3-5 key factors)
- ✅ Causal explanation (what, why, how it impacts, examples, exceptions)
- ✅ Simplified task map (main path + branches)

**Not Yet Included** (future enhancements):
- ❌ Automatic GitHub scanner
- ❌ Complex understanding check scoring
- ❌ Multi-round deep causal reasoning
- ❌ Auto-generate visual flowcharts

---

## Typical Use Scenarios

### Scenario 1: Completely Unfamiliar Domain

**Input**: "I want to be a self-employed individual"

**Skill Behavior**:
1. List candidates: Learn process? Evaluate feasibility? Prepare registration?
2. Confirm goal: Assume "evaluate suitability + understand process"
3. Backward-reason key factors:
   - Business direction (determines registration type and tax)
   - Startup capital (affects scale and risk)
   - Time investment (full-time vs side hustle)
   - Legal liability (individual vs company differences)
4. Generate task map: clarify next step

### Scenario 2: Vague Business Idea

**Input**: "Saw Opus5.5 generate videos from one sentence, want to supplement AI production tools"

**Skill Behavior**:
1. List candidates:
   - A. Build general AI production environment?
   - B. Focus on video generation toolchain?
   - C. Compare your and Opus capability gap?
   - D. Explore 3D printing + AI modeling business loop?
2. User selects C: first look at capability differences
3. Backward-reason key factors:
   - Test method (unified prompts and tools)
   - Evaluation dimensions (creativity, engineering, self-check, revision)
   - Comparison protocol (avoid unfair comparison)
4. Provide specific test plan

### Scenario 3: High-Risk Decision

**Input**: "I want to make money trading stocks"

**Skill Behavior**:
1. List candidates:
   - A. Learn value investing?
   - B. Short-term swing trading?
   - C. Follow news and tips?
2. ⚠️ High-risk warning: Stock trading has loss risk, first confirm risk tolerance
3. Backward-reason key factors (strengthen risk explanation):
   - Principal amount and loss tolerance
   - Knowledge base (avoid being scammed)
   - Time investment (short-term requires watching market)
   - Psychological tolerance (emotion management when losing)
4. Recommendation: first small paper trading, then decide whether to use real money

---

## Testing and Improvement

**Acceptance Criteria**:
- ✅ Listed candidate intents cover main interpretations
- ✅ User can find close option from candidates
- ✅ Backward-reasoned key factors indeed affect subsequent decisions
- ✅ Causal explanations help user understand "why it matters"
- ✅ Task map can adjust based on user-supplied information
- ✅ No "pre-answering" or "drift" occurred

**Iteration Directions**:
1. Collect real use cases
2. Identify common drift scenarios
3. Optimize candidate intent quality
4. Improve trigger conditions
5. Enhance dynamic adjustment capability

---

## Usage Example

**Quick Start**:

```markdown
User: "I want to learn machine learning"

Assistant (using task-backward):

I understand you might want to:

**A. Systematically learn ML theory and practice from scratch**
- Suitable for: Complete beginner, want solid foundation
- Time: 3-6 months
- Next step: First learn Python and math basics

**B. Quickly get hands-on with existing tools for projects**
- Suitable for: Have programming basics, want quick results
- Time: 1-2 weeks
- Next step: Directly use HuggingFace/Colab to run models

**C. Understand what ML can do, evaluate if it's right for you**
- Suitable for: Still not sure whether to go deep
- Time: A few days
- Next step: Look at some actual cases and application scenarios

**Which is closer to your thinking? Or you can tell me your background and goals.**
```

---

**Current Version**: v0.1 MVP  
**Last Updated**: 2026-10-08  
**Compatible Platforms**: Harness  
**Status**: Design complete, awaiting real-world validation
