# 10 Claude Prompts for Students That Actually Work

If you're a student using Claude (Anthropic's AI assistant) for studying, you've probably noticed the gap between "Claude is impressive" and "Claude is actually helping me learn." The difference is almost entirely in the prompt.

Below are 10 prompts I actually use. Each one is engineered with a specific output format and tested against alternatives. They're free — copy them, paste them, adapt them.

---

## 1. Textbook chapter → 6-month memory

The single most useful study prompt I've found. Instead of asking "summarize this chapter," ask for what you'll actually remember in six months.

```
You are reading the following chapter so that I don't have to.

Produce output in exactly this structure:

# Core claim (1 sentence)
The single most important claim of the chapter.

# The 5 ideas that support it
Five sub-claims, each one sentence. Order them from most foundational to most derivative.

# Where it could be wrong
Two honest weaknesses or gaps in the argument. Be specific.

# What to remember in 6 months
Three items. Each item: (a) the concept, (b) one-line example, (c) when I'd reach for it.

# Glossary
Max 8 terms the chapter introduces. Each <15 words.

Chapter:
{{PASTE}}
```

Why it works: the "in 6 months" framing forces Claude to prioritize what matters. The "where it could be wrong" section surfaces what most summaries hide.

---

## 2. Anki cards that don't suck

Most Anki generators give you compound questions that mix two ideas. Use this instead:

```
Generate Anki cards from this material.

Rules (not suggestions):
1. Each card tests ONE atomic fact. No compound questions.
2. Front must be answerable without seeing the back.
3. Prefer cloze cards where context matters; Q/A where standalone.
4. Skip facts I'd already know after reading once.
5. For any number/date/formula, add a "why is it this and not something else" card.

Format:
| Front | Back | Type | Why this card exists |

15-25 cards. Quality bar: I should still want to do the deck a year from now.

Material: {{PASTE}}
```

The "atomic" rule alone separates Anki cards that stick from cards that frustrate.

---

## 3. The essay critic who tells you the truth

LLMs trained on RLHF default to praise. To get useful feedback you have to explicitly disable that:

```
Critique my essay. Behave like a senior writing tutor who's read 10,000 student essays.

In this exact order:

1. **Thesis in one sentence.** State what you think my thesis actually is. If you can't, say so plainly.
2. **The strongest paragraph and why.** Quote a phrase.
3. **The weakest paragraph and why.** Quote a phrase. Name the failure mode (vague, unsupported, off-topic, redundant).
4. **The argument's load-bearing assumption.** What does my essay assume I haven't defended?
5. **Three sentence rewrites.** Pick three sentences at 80% (not the worst — the salvageable ones).
6. **One thing to cut.** Specific. Quote it.

No praise sandwich. No "overall, great start." Go.

Essay: {{PASTE}}
```

The "no praise sandwich" instruction is the unlock. Without it, you get encouragement instead of edits.

---

## 4. Pre-exam blind-spot finder

This catches the topics you don't know you don't know:

```
I have an exam on {{TOPIC}} in {{TIMEFRAME}}.

Syllabus: {{PASTE LIST}}
Topics I feel confident on: {{LIST}}
Topics I've struggled with: {{LIST}}

Identify:

1. Three topics I haven't mentioned that I might be quietly weak on — the topics connecting my weak areas to my strong ones. Exam questions love testing those bridges.
2. For each, a 3-minute drill: one concrete question I can answer right now to test if I actually know it.
3. The one topic I should NOT study more. I've probably over-prepared something. Tell me which.

No padding.
```

The "topic to stop studying" recommendation is rare and valuable.

---

## 5. Concept → 3 analogies

If a concept won't stick, ask for analogies from three different domains:

```
I'm learning {{CONCEPT}} and it's not sticking. Generate three analogies from different domains.

For each:
- Name the source domain (cooking, sports, city planning, etc.)
- List 3 specific correspondences between the source and the concept
- State where the analogy breaks. Every analogy breaks somewhere — name the specific point.

Then pick the strongest. Explain in 2 sentences why it's best for building intuition.

My current mental model: {{1-2 SENTENCES}}
```

Three weak analogies beat one strong one — you build a richer mental model.

---

## 6. The "explain it back" trap

Reverse the usual flow. Explain the concept to Claude, then have it find your gaps.

```
I'm going to explain a concept the way I currently understand it. Your job is NOT to correct me.

Your job is to:
1. Repeat my explanation back in your own words, faithfully — don't sneak in corrections.
2. Point out exactly two places where my explanation glosses over something, uses a word imprecisely, or has a load-bearing assumption I didn't justify.
3. Ask me one question that would resolve the bigger gap.

Concept: {{CONCEPT}}
My explanation: {{YOUR EXPLANATION}}
```

This is the Feynman technique with a sharper edge.

---

## 7. Paper triage

When you have 12 papers to read:

```
I have papers to read for {{PURPOSE}}. I'm going to give you abstracts. Score each on (1) relevance, (2) methodological rigor, (3) likelihood of containing a citation chain worth following.

Then rank them in the order I should read them. Explain in one sentence why.

If two papers look like they'll say the same thing, tell me — I'll only read one.

Purpose: {{}}
Abstracts: {{PASTE WITH --- BETWEEN PAPERS}}
```

"Which order should I read these" beats "should I read this paper."

---

## 8. Jargon decoder

When a passage is dense with field-specific terms:

```
The following passage uses terms from {{DOMAIN}} I don't fully understand. Walk me through it.

For each technical term:
- Define in plain English (max 20 words)
- Explain why the field needed a word for this — what does the term let practitioners do that ordinary language couldn't?
- Note if used loosely vs. precisely in this passage

Then re-render the passage in plain English. Keep technical terms only where stripping them loses precision.

Passage: {{PASTE}}
```

The "why did the field need this word" question reveals the *function* of the term, which builds real intuition.

---

## 9. Reverse quiz

Standard quizzes test recall. Reverse quizzes test understanding:

```
Generate a quiz on {{TOPIC}}.

Half the questions: standard format testing understanding.

Other half: **incorrect-reasoning detectors**. Present a plausible but flawed argument or worked example. Ask me to identify the specific flaw.

Format:
**Question N (type):** [question]
**Answer:** [answer]
**Why this question:** [the misunderstanding it tests for]

10 questions, increasing difficulty.

Topic: {{}}
My current understanding: {{1-2 SENTENCES}}
```

Flaw-detector questions are how exam-writers separate students who memorized from students who understood.

---

## 10. Stress-test your study plan

Before committing to a study plan, run it through this:

```
Here's my study plan: {{PASTE}}
Goal: {{}}
Deadline: {{}}

Critique as if you've watched 100 students try similar plans and only 30 hit their goal:

1. **What's the most likely failure mode?** Be concrete. "Burnout" is too generic — name which week and which subject.
2. **What's missing that I'll regret in week 3?** Probably review time, probably buffer for the topic I haven't started.
3. **What can I cut without affecting the goal?** Most plans are 20% too ambitious.
4. **If I lose 3 days unexpectedly, what's the new plan?**

No general advice. Every point grounded in something specific.
```

The "100 students" framing forces realistic critique instead of optimistic encouragement.

---

## Want 40 more?

These 10 are a free sampler. The full pack has 50 prompts across STUDY, CODE, WRITE, THINK, and SHIP — each one annotated with a "why this works" note explaining the technique.

- **[Free sampler — 5 prompts](https://cwanster8.gumroad.com/l/dwzix)** (PWYW, $0+) — five hand-picked prompts, one from each category, name your price
- **[The Claude Prompt Pack](https://cwanster8.gumroad.com/l/umfabr)** (NZ$19) — full 50-prompt pack
- **[Claude Code Cheatsheet](https://cwanster8.gumroad.com/l/fjsysa)** (NZ$9) — for developers using Claude Code (the CLI), separate companion product

---

*If these were useful, the full pack is more like this.*
