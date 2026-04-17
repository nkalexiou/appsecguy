---
title: "Threat Modeling in the Age of AI — Time to Rethink the Process"
date: 2026-04-17
categories:
  - AppSec
  - AI
  - Threat Modeling
description: "Threat modeling has always been about context. AI is changing what that context can unlock — here's how I'm thinking about the combination."
tags:
  - Threat Modeling
  - AI
  - AppSec
  - DevSecOps
---

Threat modeling isn't one-size-fits-all. Never was, never will be. The threat landscape for a SaaS application is fundamentally different from a Windows desktop app running locally on a machine — and both of those are worlds apart from something like an MCP server. Context matters, a lot. The tech stack matters. The use case matters. If you're not anchoring your threat modeling to those specifics, you're probably producing something generic enough not easily consumable by the product teams.

<!-- more -->

## Context matters

Over the years and across a lot of workshops, I always align with the [Threat Modeling Manifesto](https://www.threatmodelingmanifesto.org/) principles. But — and this is the part that actually makes it work — I've always tried to align the process with the perspectives of the people in the room. The devs, the architects, the ops folks. Give them space to raise the risks themselves, voice what worries them, talk through what they're actually building.

That human-driven approach does something important: it advances the team's own understanding of what they're building and what can go wrong. Threat modeling as a learning exercise, not just a compliance checkbox. Done right, the team walks out of that room seeing their own system differently.

Threat modeling is, at its core, a team process. It's not something you hand off to a security person and get a report back. The value is in the conversation.

Is it perfect? No. It's still only as good as the knowledge and experience in the room and just a step in the process of security releases and products. But it's better than nothing — and for a long time, that framing was enough.

## AI is changing the game

What now then? That framing isn't quite enough anymore. AI is rapidly reshaping what threat modeling can look like, and honestly, what it should look like.

Take the concept of threat models as code. Tools like [pytm](https://github.com/OWASP/pytm) have been around for a while, letting you define your system architecture programmatically and generate threat models from it. Solid idea. But with LLMs that can actually understand context and reason about threat scenarios? That concept gets a completely different dimension. You're getting something that can interpret the design and surface context-aware threats.

There are projects already moving in this direction. On the more experimental side:

- [pytm](https://github.com/OWASP/pytm)
- [DragonGPT](https://owasp.org/www-project-dragongpt/) (OWASP Incubator)
- [StrideGPT](https://github.com/mrwadams/stride-gpt)

DragonGPT from the OWASP incubator is still finding its footing, but the idea is there. StrideGPT is a more mature example — it directly integrates LLMs into the STRIDE analysis process, and it's genuinely useful. These tools are pointing at where this is all heading: AI not as a replacement for the process, but as an accelerator and a value-multiplier.

## Where is this going

The main path forward is deeper integration of AI capabilities in the threat modeling process — particularly in the post-workshop analysis phase.

Here's what I mean. A workshop with a team is still valuable. You get the context, the edge cases, the "yeah but actually we do this weird thing in prod" moments that no LLM is going to surface on its own. But once you've got that raw material — the design, the data flows, the assumptions, the concerns raised in the room — that's where AI can accelerate the analysis. Feed it to an LLM with the right framing and you get threat coverage that would take a human analyst days to produce, across multiple attack categories and threat actor profiles.

Speed matters. Coverage matters. And LLMs are genuinely good at both when they're given the right context to work with.

The team conversation gives the AI something real to analyze. The AI gives the team something they couldn't have produced alone. That combination is where the value is. The one billion dollar question is: *"How do you fuse the two worlds together in a continuous manner?"*

## My bottom line

I still believe threat modeling is a team process. I still think the human conversation is irreplaceable for building shared understanding and surfacing the nuances that live inside people's heads. Integrate AI where it's meaningful. Keep the human conversation where it's irreplaceable.
