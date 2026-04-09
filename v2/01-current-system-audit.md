# Chapter 1 — Current System Audit

> Status: 🔲 Not started

## Purpose
Establish an honest, precise picture of v1 before designing v2. We cannot make good architectural decisions without fully understanding what we're replacing and why.

---

## 1.1 Strategy Inventory
*Map each strategy exactly as it runs today — inputs, conditions, execution, exits.*

- [ ] QQQ 0DTE Rejection Strategy
- [ ] QQQ 0DTE Breakout Strategy
- [ ] MNQ Futures Momentum Strategy

---

## 1.2 Shared vs. Unique Logic
*Identify what is genuinely shared across strategies vs. accidentally coupled.*

---

## 1.3 What Works Well
*Things in v1 that should be preserved or ported directly.*

---

## 1.4 What Is Broken or Fragile
*Known bugs, races, fragile assumptions, or things held together with duct tape.*

---

## 1.5 What Is Redundant
*Overlapping logic, duplicate code paths, unnecessary coupling.*

---

## 1.6 Key Decisions Made in v1 (and Whether They Still Hold)
*Decisions that were made under constraints that may no longer apply.*

---

## 1.7 Open Questions from This Chapter
*Questions surfaced during the audit that need to be resolved before proceeding.*
