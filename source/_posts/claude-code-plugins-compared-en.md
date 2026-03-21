---
title: Claude Code plugins compared
date: 2026-03-21
tags:
    - agentic-coding
categories:
    - EN
---

I recently tried four Claude Code plugins, one after another, asking each to implement the same feature. Here's what I found.
<!-- more -->

All of them produced working code — no obvious losers here. But the *development experience* differed significantly.

---

### 1. "Raw" Claude Code in Planning Mode

**Flow:** enable planning mode → describe the feature → Claude asks questions → plan is ready → turn off planning mode → implement.

**Pros:**
- Great at collecting requirements — asks sharp, relevant questions
- Token-efficient: the lowest cost of all approaches

**Cons:**
- Asks several questions at once, which makes answering awkward
- Won't remind itself to run tests, linters, or do a code review unless you tell it to

**Conclusion:** Very smart, but needs manual steering. After the code is written, you have to prompt it explicitly for the next steps: run tests, check linting, review the diff. Not a dealbreaker, but it's on you.

---

### 2. Superpowers

**Flow:** `/superpowers:brainstorming` → `/superpowers:write-plan` → `/superpowers:execute-plan`

**Pros:**
- Asks questions one by one during brainstorming, with suggested answers — genuinely pleasant UX
- Completes the full development cycle on its own: code review, style checks, tests, pull request — no reminders needed
- Advanced: uses subagents, parallelizes tasks, works in isolated git worktrees

**Cons:**
- Installs a large number of skills, many of which you may never need
- Context-hungry — you'll burn tokens fast

**Conclusion:** Powerful, but bloated. Personally, I'd rather add skills consciously, one by one, only when actually needed. The good news: you can cherry-pick individual skills directly from their repo.

---

### 3. feature-dev (official Claude Code plugin)

**Flow:** `/feature-dev` — that's it, one command.

**Pros:**
- Runs subagents in parallel for codebase analysis and code review
- Handles the full cycle end-to-end: tests, review, pull request — without reminders
- Conducts a quality analysis at the end and suggests concrete improvements

**Cons:**
- Asks all questions at once, which is less convenient to answer
- Made a couple of incorrect assumptions about business logic — had to correct them mid-implementation

**Conclusion:** The sweet spot for small-to-medium features in existing repositories. Simple, complete, and doesn't get in your way.

---

### 4. SpecKit and OpenSpec

Both follow a spec-driven, documentation-first approach with multi-step flows (propose → explore → apply, etc.).

**Pros:**
- Thorough: generates specs, plans, architecture docs
- May be worth it for greenfield projects

**Cons:**
- Generates a lot of markdown files you likely don't need
- Takes long, asks fewer clarifying questions than you'd expect, and makes assumptions
- Overkill for day-to-day work in an existing codebase

**Conclusion:** Not for everyday feature development in existing projects. Consider for greenfield only.

---

### Bottom line

- **Brownfield (existing) projects:** use `feature-dev` or plain planning mode. Both work well, `feature-dev` requires less manual prompting.
- **Greenfield projects:** SpecKit or OpenSpec might be worth exploring.
- **Superpowers:** too much overhead for my taste — but you can always copy individual skills from their repo when needed.
