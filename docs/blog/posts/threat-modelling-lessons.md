---
title: "What I've learned (so far) by threat modeling with teams across Europe"
date: 2026-05-12
categories:
  - AppSec
  - Threat Modeling
description: "10+ years of running threat modeling workshops across Europe — condensed into practical points you can use in your next session."
tags:
  - Threat Modeling
  - AppSec
  - Workshops
  - DevSecOps
---

I've been running threat modeling workshops with teams across Europe for over 10 years. Sweden, Norway, Switzerland, Austria, Greece. The differences are real — some teams lean on individual expertise, others on collective knowledge. Group dynamics vary a lot depending on culture, seniority mix, and frankly how much the team trusts the security function.

But the goal is always the same: bring the team together, understand the risks they're facing, and figure out what they can actually do about it.

Different cultures, different dynamics — same pressure to deliver fast and secure. Here's what I've picked up along the way, condensed into practical points you can use in your next workshop.

<!-- more -->

## Set the environment before you start

Make it clear you're doing this *with* them — not for compliance, not for yourself. This is a safe space to speak up, raise concerns, and flag issues without judgment. It's not a checkbox exercise. It's a realistic, pragmatic session focused on what the team *can* and *wants* to fix. That framing matters more than most people realize.

## Deliver the context upfront

What are you doing today? What should they expect? Why does this deserve a few hours of their time?

Senior engineers often walk in late, confused about why they're in the room, and immediately start pushing back. Don't lose them. Ask what their expectations are — then meet their skepticism with direct, factual answers. Security posture, architecture clarity, compliance, customer trust. Be concrete. Don't get defensive.

## Listen first, ask second, then propose

The engineers in the room are the experts in their product. Your primary job, especially early on, is to get them talking. "What are you building and why?" and "What do you think can go wrong?" are usually enough to get things moving. Resist the urge to jump in with your own threat list — let them surface issues first. You'll get better quality output and much stronger buy-in.

## Define the attacker

This is where you bring something the team typically doesn't have: attacker perspective. Walk them through realistic attacker profiles. What does a plausible attack scenario actually look like against their system? Not theoretical — grounded in their stack and use case. This is often the moment the room shifts from passive to engaged.

## Stick to the objective

You have limited time and one of your jobs as moderator is to keep it. Follow the [Threat Modeling Manifesto](https://www.threatmodelingmanifesto.org/) — focus on solving problems, not admiring them. Cut discussions that loop, drift into unrealistic assumptions, or land on solutions the team can't actually implement. It's not easy to interrupt, but it's necessary.

## Utilize your network in the room

Are there security champions or team leads in the session? Use them. Ask them to explain parts of the product, draw attention to edge cases, or push quieter members to contribute. They know the system and the people — lean on that.

## Get the new people in the room

I'm writing this right after a workshop where junior developers raised roughly 30% of the identified issues. Their minds are fresh. They haven't built up assumptions about how things "should" work, and that makes them think more like attackers. I can't stress this enough — make sure they're included and make sure they feel safe to speak up.

## Address the elephants

Don't avoid the known issues. Raise them. Open the harder topics — always with an engineering, solution-oriented mindset. And document what the team *won't* fix and what they *can't* fix right now. That documentation is invaluable for future risk assessments and product conversations. It's not a failure list — it's a risk register.

## Ask for feedback

At the end of the session, ask the team what worked and what didn't. Was the scope too broad? Did the session feel useful? Would they run it differently next time? You'll get honest answers if you've set the right tone from the start — and you'll keep getting better at running these.

---

Threat modeling is one of those activities that looks simple on paper and gets complicated the moment real people are involved. Different cultures, different communication styles, different ideas about what "security" even means in their day-to-day work.

What's stayed constant across all of it: the teams that get the most out of these sessions are the ones that feel like they own the outcome. Your job is to make that happen.

What's been your experience running threat modeling workshops? I'd love to hear what's worked — or what hasn't.
