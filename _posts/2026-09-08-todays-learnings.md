---
layout: post
title: "Today's learnings September 8 2026"
date: 2026-09-08
category: daily
tags: [reading, agents, coding, distribution, small-models]
---

*A collection of things I learned today. Each section has a link to the original source so you can read more.*

---

## Give Your Coding Agents a Memory You Own

*Article: [Give Your Coding Agents a Memory You Own](https://huggingface.co/blog/funes) by the Funés team*

Coding agents forget everything between sessions. This article talks about building a memory system that saves every turn of every session. The agent can then search its own past work.

Coding agents already produce the record we keep losing. They leave behind a dense account of not just what changed, but why. The problem is that this record is usually thrown away at the end of a session.

The tool they built, Funés, saves each turn on your computer using a local index. When a task touches a past decision, the agent can search for it on its own. It returns the original text, not a summary, and shows exactly where it came from. This is important because summaries flatten the findings that matter.

The local memory is a database file on your computer. The shared memory is a private dataset on Hugging Face that you own. Before publishing, it scans every piece of text and removes anything that looks like a secret.

One command turns the record into a memory the next agent can read, on whichever computer you happen to be on.

---

## Distribution for PMF

*Blog: [Distribution for PMF](https://goyalayus.github.io/blog/distribution-for-pmf.html) by Ayush*

Most founders struggle with finding the 100 people who have the potential to love your product. Ayush talks about the three ways to find them.

You can do it manually. You cold email people, try to get intros, do physical marketing. You can burn investor money to buy distribution through paid sponsorships or ads. Or you can use your own distribution, like a Twitter following.

The flaw in the third approach: suppose you were building a developer tool and your Twitter following helped, but you did not find product-market fit. Now you want to build construction software. None of your followers belong to this space. What do you do?

I liked this because it made me realize that distribution is not transferable. You have to find the people who already have the problem you are solving.

---

## How to use Agentic Coding Tools like Claude Code Effectively

*Guide: [How to use Agentic Coding Tools like Claude Code Effectively](https://www.artificialintelligencemadesimple.com/p/how-to-use-agentic-coding-tools-like) by Devansh (AI Made Simple)*

This is the most practical guide to Claude Code I have read. It is based on over 300 hours of experiments in real deployments.

The main idea: controlling what the agent sees matters more than how you word your prompt. Dirty context produces garbage regardless of how clever your prompt is. Clean context lets mediocre prompts succeed. More context is often worse.

> "If you don't control context, you don't control outcomes. Claude Code doesn't reward clever prompting. It rewards system design."

The terminal-first design is not a limitation. It is the point. Running alongside your shell gives Claude access to CLI tools, scripts, CI hooks, parallel worktrees, and headless automation that IDE-embedded assistants cannot touch.

Rules I want to remember:

- Keep CLAUDE.md under 50 lines. A bloated CLAUDE.md does not just waste tokens. It actively degrades performance by introducing distractors.
- If you have been going back and forth with Claude for more than 15-20 turns on a single task, something is wrong. Either the task needs decomposition, or you need to reset.
- Specify the what, be loose on the how. "Add rate limiting, max 5 attempts per 15 minutes" beats a detailed implementation spec.
- Use git worktrees to run multiple Claude instances in parallel, each with separate context windows working on independent tasks.

The guide also covers failure modes. Claude starts coding before understanding the problem. You debug for an hour, then switch to a new feature without clearing context. Claude drags forward assumptions from the debugging session. The fix is to use /clear between unrelated tasks.

---

## Small Models Have Arrived

*Blog: [Small Models Have Arrived](https://calv.info/small-models-have-arrived) by Calvin French-Owen*

It is weird we are not seeing more consumer AI companies. The answer is token costs.

With the previous generation of models, you would spend about one dollar to get anywhere. Charging thirty dollars a month is untenable for a consumer app. Now, with newer small models, the average cost is around ten cents.

Think of the people you interact with daily. Nine times out of ten, you want someone who is super responsive and just handles things for you. Most of the work at companies today is spent this way. Hiring skews heavily toward the fast, cheap, and good-enough archetype.

There is a lot of work to make fast, cheap, good-enough models a reality for business. But the cost curve is moving in the right direction.

---

## References

- Funés team. "Give Your Coding Agents a Memory You Own." Hugging Face Blog. [https://huggingface.co/blog/funes](https://huggingface.co/blog/funes)
- Ayush. "Distribution for PMF." Ayush's Blog. [https://goyalayus.github.io/blog/distribution-for-pmf.html](https://goyalayus.github.io/blog/distribution-for-pmf.html)
- Devansh. "How to use Agentic Coding Tools like Claude Code Effectively." AI Made Simple. [https://www.artificialintelligencemadesimple.com/p/how-to-use-agentic-coding-tools-like](https://www.artificialintelligencemadesimple.com/p/how-to-use-agentic-coding-tools-like)
- French-Owen, C. "Small Models Have Arrived." [https://calv.info/small-models-have-arrived](https://calv.info/small-models-have-arrived)

---

*This post is a collection of things I learned today. Each section has a link to the original source so you can read more.*
