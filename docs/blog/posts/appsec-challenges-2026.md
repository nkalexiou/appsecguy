---
title: "Random Thoughts on AppSec Challenges in 2026"
date: 2026-06-02
categories:
  - AppSec
description: "AI everywhere. Tools, processes, and consequences."
tags:
  - AppSec
  - AI
  - DevSecOps
  - Threat Modeling
  - Supply Chain
---

AI everywhere. Tools, processes, and consequences.

<!-- more -->

## The transition to AppSec platforms

Building a security program around siloed tools has never been great, but for a long time it was just how things were done. SAST here, DAST there, SCA somewhere else — each with its own dashboard, its own noise, and its own way of telling you something is probably wrong.

The problem with that model is scale and communication effectiveness. The more teams you support, the more findings pile up, and the harder it gets to communicate a coherent risk picture to anyone who needs to act on it.

What AI makes newly tempting is unification: not just presenting findings in one place, but actually triaging them, pushing mitigations directly to Github, and helping teams prioritize.

## Custom tools on the rise

The cost of building software has dropped significantly. I've been building custom tooling to automate parts of my day-to-day work and catch bugs, or add features in commercial tools that are simply ignored by the vendors. Things I always wanted proprietary products to do but never did.

Small scripts and automation workflows that would have taken a sprint to build a few years ago now take an afternoon. That changes what's worth building vs. what's worth buying.

## Threat modeling

Still relevant. More relevant, actually. The surface area has grown and the threat vocabulary needs to keep up.

MCP servers, prompt injections, AI model poisoning, indirect context manipulation — these concepts need to be part of the threat modeling conversation now, not eventually. The [OWASP AI Top 10](https://owasp.org/www-project-top-10-for-large-language-model-applications/) is a useful starting point for structuring that thinking.

On the process side, AI is genuinely helping here too. Preparing for a threat modeling session — understanding an architecture beforehand, surfacing relevant threats, structuring material for review — takes less time than it used to.

## Supply chain security

Wow, what a ride so far.

Account takeovers and malware targeting CI pipelines have gone from edge cases to a regular part of the job. The attack surface is wide and the blast radius from a single compromised dependency or poisoned pipeline can be significant.

Handling this well requires two things working together: broad controls that cover your supply chain attack surface (what's in your pipeline, what can reach it, what it can reach), and smart policies that add friction where it matters — version cooldowns, dependency approval gates, pinned hashes. Neither alone is enough. Defense in depth is appropriate here as well.

## LLM-generated code as a vulnerability source

The speed at which developers can now produce working code has changed expectations permanently.

The problem is that LLM-generated code fails in specific ways that aren't always caught by the instincts developers have built reviewing human-written code. I ran into this firsthand working on projects of my own.

You must embrace the velocity, but you also have to build the guardrails into the flow itself — quality checks, security review, and critically, automated review by an AI on the code changes themselves. AI reviewing AI-generated code isn't redundant; it's a different kind of attention applied at a different point in the process. You can do that at Pull Request level, or at coding in IDE. Anthropic's coding superpowers are a useful example of what this paradigm looks like.

---

That's a few threads worth watching in 2026 so far. I'll try to revisit the list at year end.
