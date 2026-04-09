# Chapter 8 — Where Does AI Actually Belong?

> Status: 🔲 Not started

## Purpose
Challenge every assumption about where AI adds value before committing to an agentic architecture. The question is not "how do we use AI?" but "where does AI produce better outcomes than deterministic code, and is that margin worth the added complexity, latency, and cost?"

---

## 8.1 The Evaluation Framework
*For each proposed AI touchpoint, answer:*

1. What is the input? What is the decision?
2. Can this be expressed as a deterministic rule? If yes, should it be?
3. What does AI add — pattern recognition, natural language reasoning, ambiguity handling?
4. What is the latency tolerance for this decision?
5. What is the cost (API calls, inference time) at scale?
6. What is the failure mode if the AI is wrong or unavailable?

---

## 8.2 Proposed AI Touchpoints — Evaluation Table

| Component | Proposed Role | Deterministic Alternative | Decision |
|---|---|---|---|
| Regime detection | Classify market condition | Rule-based VIX/ATR/trend thresholds | TBD |
| Risk reasoning | Evaluate position sizing in context | Fixed rules per config | TBD |
| Price action monitoring | Narrative interpretation of tape | Pattern rules | TBD |
| Pre-market scenario generation | Bull/bear narrative | Mechanical level-based | Already exists |
| Signal filtering | Context-aware suppression | Cooldown + window rules | TBD |

---

## 8.3 The Principle
*State the agreed principle for when AI is used vs. deterministic logic.*

> Draft: Use AI where the decision requires reasoning over ambiguous, multi-factor context that cannot be fully enumerated as rules. Use deterministic code for everything that can be made explicit.

---

## 8.4 Components That Survive the Filter
*After evaluation, the AI components that are worth building.*

---

## 8.5 Components That Don't
*Proposed AI uses that are better served by rules.*

---

## 8.6 Open Questions from This Chapter
