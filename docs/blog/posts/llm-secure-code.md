---
title: "I Asked Claude to write a feature. It introduced two security bugs. Now what?"
date: 2026-05-13
categories:
  - AppSec
  - AI
description: "Claude wrote a security bug, fixed it when I pointed it out, then introduced a different security bug."
tags:
  - AI
  - AppSec
  - Secure Coding
  - DevSecOps
---

So I've been building new features for [suricatajs](https://github.com/nkalexiou/suricatajs), my open source project, using Claude. And I had one of those experiences that I think every developer working with LLMs is going to run into sooner or later — if they haven't already.

Short version: Claude wrote a security bug, caught it when I pointed it out, then fixed it with a different security bug.

Let me tell you the story.

<!-- more -->

## The Setup

Among other changes, I needed a simple REST API protected by an API key. Claude generated the implementation, the unit tests, and the integration tests. Everything in a few minutes. Looked clean. Tests were green.

Almost.

## Manual Testing Saves the Day (Again)

I wanted to do a quick sanity check so I tested if authentication works up the API, so I tested without setting an API key at my client. It just... let me in. That was not great, so I asked the LLM to fix the authentication bypass error.

Here os the error: 

```python
def require_api_key(api_key: str = Security(_api_key_header)) -> str:
    configured = {k for k in os.getenv("API_KEYS", "").split(",") if k}
    if not configured:
        return ""  # <-- here's your problem
    ...
```

The logic was: if `API_KEYS` isn't set, `configured` ends up as an empty set, and the function just returns an empty string and moves on. All requests succeed silently. 

Default accept instead of default deny. 

The tests never caught it because `API_KEYS` was always set. 


## The Fix That Wasn't Quite Right

Claude acknowledged the problem and applied a fix: If `API_KEYS` isn't configured, reject the request.

Then I tested again. Great, not access without a key set, but there was something more. Why was the HTTP error code at the client so verbose? 

```json
{
  "detail": "API_KEYS not configured — set the API_KEY environment variable"
}
```

A look at the server, showed no ifnromation about the underlying problem. So in short: information leakage at the client, and lack of logging at the server. 

I pushed back on this and Claude responsed — "Correct. That's an information leak — server config details don't belong in API responses." — and fixed it.

## Where This Leaves Us

Security hasn't gotten easier just because we have faster tools. In some ways it's gotten harder — because the velocity of code being produced has gone up.

LLMs are genuinely useful for development. But they're not security-centric in many ways - even when using specialized skills, such as the superpowers skill from Claude which I was using for this example. They can certainly fix the bug you point at without noticing the one they introduced in the process.

That means the human in the loop still has to care. You have to test the unhappy paths. You have to read the error responses. You have to think about what an attacker sees, not just what the happy-path test suite validates.

We need faster and better tooling to catch up with the new bug surface that LLM-assisted development is creating. Static analysis, DAST, proper secret scanning, security-focused code review checklists — none of that goes away. If anything, it becomes more important.

---

suricatajs is available on [GitHub](https://github.com/nkalexiou/suricatajs). 
