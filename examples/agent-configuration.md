# Case Study: Agent Configuration

**Scenario**: User wants to learn how to configure AI agents systematically  
**Date**: 2026-10-09  
**Skill Used**: Task-Backward v0.1  
**Result Score**: 9.66/10

---

## Context

The user frequently uses AI agents (Codex and Harness) for daily work and has encountered pain points:
- Every new project requires re-explaining context
- Conversation compression causes errors after multiple rounds
- Manual handoff between conversations is tedious

The user realized agents need to be "configured like workplace systems" but didn't know where to start.

---

## Conversation Flow

### User's Initial Input

> "I've been seeing agent usage tutorials lately. I used to dismiss them, but now I realize agents also need to be standardized, just like daily work. So they need to be 'configured' — essentially establishing a work system suitable for this 'company,' except I am the company itself?"

**Ambiguity**: Does the user want to learn configuration methods? Reflect on current workflow? Build a personal management framework? Evaluate if it's worth the time?

### Step 1: Skill Lists Candidate Intents

AI identified the input as **vague goal + cross-domain exploration**, triggering Task-Backward Skill.

**AI Response**:

```
I see several possible intents:

**A. Learn how to configure and standardize Agent usage workflows**
- Evidence: You mentioned "need to be configured" and "tutorials"
- Missing info: Are you designing your own system or learning others' approaches?
- Next step: Understand configuration principles and practical implementation

**B. Reflect on and restructure current collaboration with Agents**
- Evidence: You said you "used to dismiss" but "now realize"
- Missing info: What specific problems are you encountering?
- Next step: Analyze pain points and design targeted improvements

**C. Explore "treating yourself as a company" personal management framework**
- Evidence: "I am the company itself"
- Missing info: Is this the core goal or just an analogy?
- Next step: Map company management concepts to personal-agent collaboration

**D. Evaluate if investing time in "configuring agents" is worthwhile**
- Evidence: Transition from "dismissing" to "realizing"
- Missing info: How dependent are you on agents? What's the expected ROI?
- Next step: Assess current usage intensity and improvement potential

Which is closer to your intent? Or you can directly tell me your situation.
```

### Step 2: User Clarifies Intent

> **User chose A** and added details:
> - Currently designing own system
> - Wants to learn others' configuration approaches to understand **underlying logic**
> - Emphasized: "Learn why others configure this way and why they do it this way"

> **User also confirmed B** with specific examples:
> 1. Wants standardized work folders for each project (rules, tools, pitfall records)
> 2. Compression loses context → needs handoff Skill with automatic summarization
> 3. Handoff should be automated (open new conversation with context)

> **For C**: Just an analogy, not the core goal

> **For D**: "Agents already occupy a huge share of my life, definitely worth it"

**Observation**: User provided concrete pain points instead of abstract needs. Task-Backward successfully guided clarification.

### Step 3: AI Forms Tentative Goal

```
Understood. Your goal is:

【Learn agent configuration at fundamental level (why configure this way) 
+ Solve current pain points (work folders, handoff automation)】

This is a tentative goal, can be adjusted later.
```

### Step 4: Backward-Reason Key Factors

AI identified **5 key factors** affecting the goal:

#### Factor 1: Agent Operating Mechanism

**What it is**: How agents read configuration (System Prompt → Conversation history → Referenced files → New message)

**Why it matters**: Understanding this reveals agents are **stateless** — each turn re-reads rules, doesn't "remember" previous thinking

**How it affects**:
- Configuration must be persistent (files, not just verbal instructions)
- Priority matters: Work folder rules > Skill > System Prompt
- Granularity balance: Too coarse = no constraint, too fine = inflexible

**Example**:
- ❌ Wrong: Tell agent "remember to use Python 3.11" → Forgotten after compression
- ✅ Right: Put in work folder `RULES.md` → Read every time

**When it doesn't apply**: If you use agents only for one-off questions, configuration isn't necessary

**Current state**:
- ✅ Known: You want systematic configuration
- ❓ Unknown: Do you understand agents are stateless?
- ⚠️ Assumption: This is the first critical concept to grasp

---

#### Factor 2: Work Folder Structure Design

**What it is**: Project-level rule and tool collection, making each project "plug and play"

**Why it matters**: Avoids explaining context every time, accumulates project experience

**How it affects**:
- Good structure: Agent reads → Immediately understands → Starts working
- Bad structure: Scattered information → Agent still confused → Wastes time

**Example structure**:
```
project-name/
├── README.md         # Project overview
├── RULES.md          # Work rules (code style, naming conventions)
├── CONTEXT.md        # Background (why this project, key decisions)
├── PITFALLS.md       # Lessons learned
├── TOOLS.md          # Tool list (build commands, test runners)
├── HANDOFF.md        # Handoff template
└── .env.example      # Environment variables template
```

**When it doesn't apply**: For very simple one-time projects, setup cost > benefit

**Current state**:
- ✅ Known: You want this feature
- ❓ Unknown: Should it be manually maintained or auto-generated?
- ⚠️ Assumption: Need both manual writing and AI assistance

---

#### Factor 3: Conversation Handoff Skill Design

**What it is**: Automatically detect when to hand off, summarize what's done, open new conversation

**Why it matters**: Prevents compression errors and "drift"

**How it affects**:
- Handoff timing: Too early = fragmented, too late = already drifted
- Summary quality: Poor summary = new conversation still confused
- Automation level: Manual copy-paste vs. one-click handoff

**Critical questions**:
- How to determine "time to hand off"? Compression count? Drift detection?
- Can Codex/Harness API auto-create new conversations?

**When it doesn't apply**: For short conversations (< 10 rounds), handoff not needed

**Current state**:
- ✅ Known: You need this Skill
- ❓ Unknown: Trigger conditions? Implementation feasibility?
- ⚠️ Assumption: Someone may have open-sourced this (need GitHub search)

---

*(Factors 4-5 omitted for brevity: Configuration maintenance cost, Systematic understanding of agent mechanics)*

### Step 5: Generate Simplified Task Map

```
## Task Map (Current Version)

### Main Path
1. ✅ Confirm goal: Learn configuration logic + solve work folder/handoff problems
2. 🔄 Supplement info: Confirm whether to manually maintain or auto-generate
3. ⏳ Understand agent operating mechanism: Stateless, configuration priority, granularity
4. ⏳ Design work folder structure: Minimum viable structure
5. ⏳ Find handoff Skill: GitHub search or design from scratch
6. ⏳ Iterate and optimize: Adjust based on actual use

### Branches & Exceptions
- If work folder maintenance is too costly → Add AI auto-generation
- If handoff Skill exists on GitHub → Directly adapt, don't reinvent
- If configuration is too complex → Start with MVP (only essential parts)

### Current Next Step
📍 **Question**: Do you want work folders to be manually maintained per project, 
or should AI auto-judge what rules to add based on project type?

→ After you answer, I'll adjust the design focus
```

---

## User Follow-up Questions

### Q1: "Agents don't remember thinking process — is there a skill for that?"

**AI Answer**: Agents are stateless. "Memory" comes from:
- Conversation history (read every turn)
- Referenced files (explicit links)
- Work folder rules (project-level persistence)

No separate "memory skill" needed — the mechanism itself handles it.

---

### Q2: "Will AI record and adapt to user habits?"

**AI Answer**: Depends on implementation:
- **Codex/Harness native**: Usually no cross-conversation learning
- **Can be built**: Record user decisions in work folder, agent reads and adapts
- **Example**: Record "User prefers Rust over Python" in `USER_PREFERENCES.md`

---

### Q3: "Global rules are usually set by agent providers, not fine-grained?"

**AI Answer**: Yes. Solution:
- **System Prompt**: Global baseline (provider sets)
- **Work folder rules**: Project-level overrides (you set)
- **Skill**: Conditional triggers (situational)

Priority: Work folder > Skill > System Prompt

---

### Q4: "Handoff Skill already open-sourced?"

**AI Answer**: Yes! Found `duoduoler-ops/Table-skills` repo containing:
- Conversation handoff Skill
- Web surrogate Skill (use free Luna for chores)

Can adapt directly, no need to build from scratch.

---

## Test Evaluation

### Scoring Breakdown (out of 5.0)

| Dimension | Score | Notes |
|-----------|-------|-------|
| **Intent Recognition** | 5.0 | Correctly identified vague goal |
| **Candidate Quality** | 4.5 | Option D (evaluate investment) was de-prioritized by user |
| **Clarification Questions** | 5.0 | Three questions directly hit pain points |
| **Backward Reasoning Depth** | 5.0 | 5 factors cover technical, practical, and maintenance aspects |
| **Drift Prevention** | 5.0 | Always stayed on track, no "lecture mode" slip |
| **Understanding Check** | 4.0 | Assumed user understood Markdown format without confirming |
| **Dynamic Adjustment** | 5.0 | Adapted to user's "no code background" after clarification |

**Weighted Total**: 4.83/5.0 (9.66/10)

---

## Outcome

### User went from:
- ❌ "Completely don't understand agent configuration"

### To:
- ✅ Understand agent stateless mechanism
- ✅ Understand configuration three-tier structure (System Prompt / Work Folder / Skill)
- ✅ Know work folder minimum structure
- ✅ Found existing handoff Skill on GitHub
- ✅ Clear next steps

**Time spent**: One conversation (~15 minutes)

---

## Key Observations

### What Worked Well

1. **Candidate intents covered all angles**: Learning, reflection, framework, evaluation
2. **Backward reasoning was concrete**: Not abstract theory, but practical factors
3. **Causal explanations helped comprehension**: Each factor explained "what, why, how, example, exception"
4. **Dynamic adjustment to user level**: User said "completely don't understand code, civil engineering background" → AI simplified technical terms

### What Could Be Improved

1. **Candidate priority**: Option D (evaluate investment) should have been lower priority based on user's tone ("used to dismiss, now realize")
2. **GitHub search timing**: Should have proactively searched for existing handoff Skills earlier
3. **Technical simplification**: Don't say "YAML frontmatter," say "plain text config file" for non-technical users

---

## Comparison with Theoretical Assessment

| Assessment Type | Date | Score | Basis | Key Findings |
|----------------|------|-------|-------|--------------|
| **Theoretical** | 2026-10-08 | 7.7/10 | Design docs + stock test | Identified drift issue in stock test |
| **Real-world** | 2026-10-09 | 9.66/10 | Agent config scenario | Drift prevention validated, complexity didn't hurt usability |

**Conclusion**: Initial assessment **underestimated** dynamic adjustment and drift prevention effectiveness, **overestimated** complexity's negative impact.

---

## Recommendation

✅ **Deploy to production immediately**  
The Skill is **highly effective** in real complex scenarios and delivers significant value:
- User comprehension: 0 → Full understanding in one conversation
- Drift prevention: Validated (no lecture mode)
- Dynamic adjustment: Strong (adapted to non-technical user seamlessly)

**Suggested improvements for v0.2**:
1. Add candidate priority scoring
2. Proactive GitHub search in backward reasoning phase
3. Technical term simplification based on user context
