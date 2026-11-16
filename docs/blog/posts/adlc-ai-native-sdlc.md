---
title: "Cloudflare's ADLC and Anthropic's AI-native SDLC: what they are and what they change"
date: 2026-11-16
categories:
  - AppSec
  - AI
  - DevSecOps
description: "Two vendors, one diagnosis, two different cures. What the Agent Development Lifecycle and the AI-native SDLC mean for AppSec."
tags:
  - AI
  - AppSec
  - DevSecOps
  - SDLC
---

Within three weeks of each other, Cloudflare and Anthropic both published their take on the same question: what happens to the software development lifecycle when agents do the building?

They agree on the problem, they propose solutions and it is interesting for AppSec.

<!-- more -->

## The SDLC is changing, fast

The way we build software is changing rapidly, and the biggest change is where the time goes. It's no longer in coding. It's in verifying and testing what was implemented. The speed at which a solution is implemented is insane and the cost is negligible. The question is whether it is done correctly. 

There is a growing distance between the developer and the code. At the same time, the need to hold the architectural oversight, to keep the link to the business and to the thing you are actually building, and of course to move fast, has never been bigger. Meanwhile everything around the code, like review, testing, deployment and maintenance, has to also run at the speed code is written, or at least keep up with it. Anthropic's playbook says it well: "code is no longer the bottleneck".

## Cloudflare's ADLC: software factories

Cloudflare's claim is that the SDLC is for software teams and the ADLC, their Agent Development Lifecycle, is for software factories. A factory takes an input, say a production error, a customer bug report or a feature idea, and builds, deploys and manages the software without a human approving each step.

The post asks what the platform underneath has to look like for that to work, and lists seven properties. Everything needs to be programmatic, with an API an agent can call and no ClickOps. It has to scale horizontally, so each agent gets its own production-like preview environment. Bugs have to be reproducible, events have to push work to agents instead of humans watching dashboards, and every change has to be atomic, so it can be tested, released and reverted on its own. Agents need a controlled way to get more access when they need it. And the whole thing should learn from experience, like engineers do. Interesting huh? 

The glue is Workflows that can run anywhere from minutes to weeks. A CI/CD pipeline becomes a Workflow, and Agent Traces records agent sessions as OpenTelemetry traces so the factory can learn from them. The proof point is a factory that triages, reproduces, verifies and fixes issues for the Astro open source project. 

What I appreciated is that Cloudflare is honest about the hard part. They compare it to self-driving cars, where going from "works most of the time" to some number of nines past 99% is where the real work is. I can confirm that and sometimes it's painful. 

For security, the way I read it, it becomes part of the workflow. It has to live with those same properties: programmatic, scalable, and applied to atomic changes. A security check that a human has to run by hand, or that only works on a big batch of changes, doesn't fit in a factory or any modern SDLC to be honest. Peer code reviews requirements read like fossils in a museum nowadays.

## Anthropic's AI-native SDLC: the same stages, as a loop

Anthropic keeps the six classic stages (plan, design, build, test, deploy, maintain) and changes who does the work. Agents execute, and humans get involved where it's required.

It becomes a loop. Every stage ends by committing an artifact to version control, and the next stage starts by reading it: `intent.md` for plan, `spec.md` for design, `plan.md` for build. The commit history becomes your audit trail. The engineer approves the plan before any code is written, and in deploy a layered agentic review runs on every PR, with humans kept for regulated and critical code.

What matters most to me is the governance part. Skills are advisory. They make the agent likely to follow a policy but don't force it. Hooks are deterministic, they can allow, ask or block an action, and managed settings let admins set rules engineers can't override. The principle is that the agent can act up to the production gate and cannot pass it.

## So what actually changes

Both proposals replace a chain of human handoffs with a continuous loop run by agents. Humans stop doing and checking every step, and decide at specific points instead. A few shifts I would point to:

- **The bottleneck moves.** Code is cheap, so planning, verification and operations is where the effort goes. 
- **Handoffs become artifacts or events.** A committed `spec.md` kicks off the next stage in Anthropic's version. In Cloudflare's, an event kicks off an agent.
- **Humans change role.** From writing and checking everything, to approving and owning the policy.
- **Controls get enforced as the work happens.** Not in a review meeting after the fact.

And the loop closes on itself. Anthropic's maintain stage feeds a breached monitoring threshold back in as a new `intent.md`, and Cloudflare's agents learn from recorded sessions.

## Why this matters for AppSec

The control objectives of the SDLC survive. What changes is who, or what, enforces them.

**Agents are principals.** They need their own identity, short-lived credentials and least privilege, like anyone else touching your systems.

**Advisory is not enforced.** A prompt or a skill shapes behavior, it doesn't guarantee it, and that is true everywhere, not just in one vendor's tooling. This is exactly why gates with AppSec controls make sense. If a policy has to hold, put something deterministic behind it.

**Review has to scale with output.** Reading every line stops working at agent volume. Agentic review plus humans on the critical paths is a reasonable answer.

**The pipeline is a new attack surface.** Specs, plans, skills and hook configs now steer what ships, so they need the same change control as code. We've already seen so many demonstrated attacks in all big conferences, since 2025 to say the least. 

---

Sources, all read in November 2026:

- [The Agent Development Lifecycle has arrived on Cloudflare](https://blog.cloudflare.com/agent-development-lifecycle/) (Cloudflare, 4 August 2026)
- [The AI-native SDLC playbook](https://claude.com/blog/the-ai-native-sdlc-playbook) (Anthropic, Louis Claxton, 21 August 2026)
