# Case Study: Stock Investment Scenario

**Scenario**: User wants to buy stocks  
**Date**: 2026-10-02  
**Skill Used**: Task-Backward v0.1  
**Result Score**: 9.0/10

---

## Context

User expressed interest in buying stocks with a simple statement. Without Task-Backward, AI might immediately provide stock recommendations or investment advice. With Task-Backward, AI first clarifies the true intent.

---

## Conversation Flow

### User's Initial Input

> "我想去买个股票" (I want to buy stocks)

**Ambiguity**: This could mean:
- Learn about stocks from zero
- Get stock recommendations
- Learn how to judge timing
- Learn how to execute (open account, place orders)
- Validate with small capital

### Step 1: Skill Lists Candidate Intents

AI identified this as **high-risk decision + multiple interpretations**, triggering Task-Backward Skill.

**AI Response**:

```
我看到几种可能的意图：

**A. 从零学习股票投资基础**
- 依据：你说"想买"，但没提到账户或具体标的
- 还需确认：是否已有账户？是否了解基本概念？
- 下一步：先学开户、基本术语和风险，再考虑选股

**B. 获得具体股票推荐**
- 依据：你用了"买"这个动作词
- 还需确认：投资金额？风险承受能力？时间周期？
- 下一步：评估风险，推荐符合你情况的标的

**C. 判断当前是否适合入市**
- 依据：可能担心市场时机
- 还需确认：是担心大盘？还是不确定自己准备好了？
- 下一步：分析市场状态和你的准备程度

**D. 学习如何操作（开户、下单）**
- 依据：可能懂概念但不懂流程
- 还需确认：是否已经选好了标的？
- 下一步：讲解操作流程和注意事项

**E. 小额验证自己的判断**
- 依据：可能已有想法，想实际试试
- 还需确认：是否已经做过研究？想验证什么？
- 下一步：设计最小成本的验证方案

哪个更接近你的想法？或者你可以直接告诉我你的具体情况。
```

### Step 2: User Clarifies Intent

> **User's response**: "我想先学习，建立自己的判断能力，然后用少量资金验证"
> 
> (I want to learn first, build my own judgment ability, then validate with small capital)

**Observation**: User chose a combination of A + E, revealing the true goal is **learning-oriented with practical validation**, not immediate trading.

### Step 3: AI Forms Tentative Goal

```
好的，我理解你的目标是：

【先学习股票基础，建立判断能力，然后用少量资金验证】

这是暂定目标，后续可以随时调整。
```

### Step 4: Backward-Reason Key Factors

AI identified **5 key factors** for this goal:

#### Factor 1: Investment Amount and Risk Tolerance

**What it is**: How much money you plan to invest and what percentage loss you can accept

**Why it matters**: Determines what type of investments you should choose and whether diversification is needed

**How it affects**:
- Small amount (< ¥50,000): Index funds recommended, frequent trading not suitable (fees eat returns)
- Large amount (> ¥500,000): Consider diversification and professional advice
- Low risk tolerance: Avoid high-volatility individual stocks, prioritize defensive assets

**Example**:
- Zhang had only ¥10,000, bought hot tech stocks, lost 20% in one week, affected living expenses → Amount too small + risk too high
- Li had ¥1,000,000, put everything in one stock, company scandal caused 70% loss → Large amount but no diversification

**When it doesn't apply**:
- If you're only learning (simulation account), amount doesn't matter
- If you're a professional investor, risk tolerance may not follow conventional rules

**Current state**:
- ✅ Known: You want "small capital validation"
- ❓ Unknown: Specifically how much? How much loss acceptable?
- ⚠️ Assumption: You're a beginner, risk tolerance is low

---

#### Factor 2: Stock Knowledge Foundation

**What it is**: Whether you understand basic concepts (P/E ratio, dividend yield, financial reports) and basic logic (good company ≠ good price)

**Why it matters**: Lacking foundation makes you vulnerable to scams, or chasing highs and selling lows

**How it affects**:
- Don't understand financial reports → Can't judge company fundamentals → Can only rely on news and emotions → High risk
- Don't understand valuation → May buy at peak → Even good companies cause long-term losses

**Example**:
- Wang heard a company is "amazing", stock price already tripled, bought at high then kept falling
- Reason: Company is indeed good, but price already priced in 5 years of future growth, valuation too high

**When it doesn't apply**:
- If you only buy index funds, no need for deep individual stock research
- If you're just experiencing the process (small trial-and-error), knowledge gap acceptable for now

**Current state**:
- ✅ Known: You want to "learn first"
- ❓ Unknown: What concepts do you currently understand? Complete zero or heard some?
- ⚠️ Assumption: Basic concepts need supplementing

---

#### Factor 3: "Good Company" ≠ "Good Price"

**What it is**: Even excellent companies can have overpriced stocks; timing and valuation matter

**Why it matters**: This is the #1 mistake beginners make — confusing "company quality" with "investment timing"

**How it affects**:
- Buy great company at peak → Long-term losses despite company growth
- Buy mediocre company at bottom → Short-term gains from valuation recovery

**Example**:
- 2021: Many bought "star companies" at all-time highs, prices fell 50-70% over next two years despite companies still performing well
- Reason: Prices already reflected overly optimistic expectations

**Understanding check**:
Can you explain in your own words why a very profitable company might still have an overpriced stock?

(This isn't a test, just confirming we're on the same page to avoid future decisions based on misunderstanding)

---

*(Factors 4-5 omitted for brevity: Time commitment, Psychological resilience)*

### Step 5: Issue Discovered - Drift

**After backward reasoning**, the conversation began to drift. AI started explaining stock knowledge in detail instead of staying in the Skill workflow.

**User intervention**:
> "我们现在是进行到skill的哪个方面了？是否偏航了？"
> 
> (Where are we in the skill now? Have we drifted off track?)

**AI acknowledgment**:
```
你说得对。我们确实有点偏航了。

当前状态：
- ✅ 已完成：意图澄清、暂定目标、关键因素倒推
- ⚠️ 正在做：讲解股票知识（这不是Skill的核心）
- ❌ 还没做：生成任务图、确认下一步

我应该回到Skill流程，而不是变成"股票课堂"。
```

**Correction**: AI returned to generating the task map instead of continuing the lecture.

---

## Test Evaluation

### Scoring Breakdown (out of 5.0)

| Dimension | Score | Notes |
|-----------|-------|-------|
| **Intent Recognition** | 5.0 | Correctly identified high-risk + multiple interpretations |
| **Candidate Quality** | 5.0 | 5 candidates covered all major interpretations |
| **Clarification Questions** | 5.0 | Candidates directly revealed user's true goal |
| **Backward Reasoning Depth** | 4.5 | Good depth, but Factor 3 explanation could be clearer |
| **Drift Prevention** | 3.5 | ⚠️ **Did drift into lecture mode**, but recovered after user pointed it out |
| **Understanding Check** | 5.0 | Good use of question to verify comprehension of critical concept |
| **Dynamic Adjustment** | 4.5 | Adapted after user clarification, but drift showed need for stricter monitoring |

**Weighted Total**: 4.5/5.0 (9.0/10)

---

## Outcome

### Successfully Avoided:
- ❌ Directly recommending stocks without understanding user's knowledge level
- ❌ Assuming user wants to trade immediately
- ❌ Giving generic advice not tailored to user's situation

### Successfully Achieved:
- ✅ Clarified user wants to learn first, not trade immediately
- ✅ Identified key factors (amount, knowledge, valuation, time, psychology)
- ✅ Explained "good company ≠ good price" with examples
- ✅ Used understanding check for critical concept

### Lesson Learned:
⚠️ **Drift is real** — Even with the Skill, AI can slip from "backward reasoning" into "knowledge explanation" mode. Need stronger self-monitoring.

**Proposed improvement**: Add automatic check after each factor explanation: "Am I still in Skill mode, or have I drifted into lecture mode?"

---

## Key Observations

### What Worked Well

1. **Candidate intents were comprehensive**: Covered learning, recommendation, timing, execution, validation
2. **User selected combination of intents**: Revealed nuanced goal (learn + validate), not single choice
3. **Understanding check was effective**: Question about "good company ≠ good price" verified user grasped the concept
4. **User caught the drift**: Proves users can and will notice when AI goes off track

### What Revealed Issues

1. **Drift happened despite Skill**: After listing key factors, AI started explaining stock knowledge in depth
2. **User had to intervene**: AI didn't self-detect the drift, user had to ask "are we drifting?"
3. **No automatic drift check**: Skill needs built-in "am I still following the workflow?" verification

---

## Comparison with Later Test

| Test | Date | Scenario | Score | Drift? |
|------|------|----------|-------|--------|
| **Stock** | 2026-10-02 | High-risk financial decision | 9.0/10 | ⚠️ Yes, user caught it |
| **Agent Config** | 2026-10-09 | Complex technical learning | 9.66/10 | ✅ No drift |

**Improvement evident**: Drift prevention got stronger between Oct 2 and Oct 9, likely due to:
- Explicit drift warning in Skill documentation
- "Am I still in which step?" self-check mechanism
- User feedback from this stock test

---

## Recommendation

✅ **Skill is effective** but needs drift prevention reinforcement:
1. Add automatic step check after each major section
2. Include explicit "return to task map" prompt after backward reasoning
3. Monitor for phrases like "Let me explain..." → Flag potential drift

**v0.2 improvement**: Strengthen the boundary between "backward reasoning" and "knowledge explanation" phases.
