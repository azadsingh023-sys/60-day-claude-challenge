Day 3, I learned Role Based Prompting. This is beneficial to get focused response.

Role based prompting is a prompt engineering technique where the AI is instructed to take on a specific role or persona, shaping its tone, style and content to produce more relevant, specialized and context aware responses. Its key aspects include:

Assigning roles like a teacher, doctor or any specific persona.
Guiding responses based on the role’s knowledge and communication style.
Produces more relevant and context-specific outputs.
Improving clarity and alignment with user expectations.

Alright, pulling up a chair — let's talk about this like we're in a founder standup, not an ITIL classroom.

## Here's the thing about Problem Management

Every founder learns this lesson the hard way, usually around month 8: **firefighting doesn't scale.**

You know the drill. Something breaks. Customer complains. You (or your one overworked ops person) jump on it, patch it, ship it, move on. Feels productive. Feels like you're "responsive." But then it breaks *again*. Same thing. Different day. And you patch it again. And your team starts normalizing this as just... how things are.

That's the trap. **Incident Management is triage. Problem Management is the fix that makes triage unnecessary.**

## The founder mental model

Think of it like this:

- **Incident = the fire.** Put it out. Customer's happy again. Ship's not sinking today.
- **Problem = the faulty wiring causing the fires.** Nobody wants to deal with it because it's not urgent — until you realize you've had six "urgent" fires this quarter, all from the same wiring.
- **Known Error = you've found the wiring, you know it's bad, you just haven't rewired it yet** — so you leave a note taped to the breaker: "if this trips, flip it back, we're fixing it next sprint."
- **Workaround = the tape and the note.** Buys you time. Doesn't solve anything long-term.

Founders who never build a "problem management" muscle end up running their whole company on workarounds. Every "temporary fix" becomes permanent because nobody circles back. That's technical debt — but for people, process, and infrastructure, not just code.

## Why this actually matters for a startup

1. **Your best engineers are expensive firefighters if you let them be.** Every hour spent re-fixing the same VPN issue or the same billing bug is an hour not spent building product.
2. **Customers forgive one outage. They don't forgive the same outage three times.** Trust compounds — or erodes — based on whether you learn.
3. **It's a discipline, not a tool.** You don't need ServiceNow or a fancy KEDB to start. You need one habit: after every recurring fire, someone asks "why does this keep happening?" *out loud, in writing, tracked somewhere.*

## The minimum viable version of this for a small team

- Any time the same incident happens 2+ times → it graduates from "annoying" to "a Problem" — give it a doc, not just a Slack thread.
- Do a lightweight root cause pass (5 Whys is genuinely enough at small scale).
- Write down the workaround so it's not locked in one person's head.
- Actually schedule the real fix — treat it like a roadmap item, not an afterthought.
- Close the loop publicly so the team sees cause → fix → done. That's how the habit sticks.

## The founder gut-check

If you're constantly saying "yeah that's a known issue, just do X" — congratulations, you already have Known Errors and Workarounds. You just don't have the discipline layer on top that turns "known issue we shrug about" into "known issue we're actively killing."

That shift — from *tolerating* recurring pain to *systematically eliminating it* — is the whole point of Problem Management. It's not bureaucracy. It's how you stop spending your best people's time paying the same tax over and over.

Want me to riff on how this maps to a scrappy team using just a spreadsheet or Notion instead of a full ITSM tool?

==================================================

Alright, dev hat on. Let's talk about this the way I'd explain it to a backend engineer, not a process person.

## The core idea, in engineering terms

Incident Management is your **exception handler**. Something throws, you catch it, you return a response to the user, life goes on.

Problem Management is you actually **reading the stack trace, finding the root cause, and fixing the bug** — instead of just wrapping every call site in another try/catch.

If you only ever handle exceptions and never fix the underlying bug, you're accumulating technical debt in your *operations*, the same way you'd accumulate it in your codebase by patching symptoms instead of refactoring the broken function.

## Mapping the vocabulary to dev concepts

| ITIL term | Dev equivalent |
|---|---|
| **Incident** | A thrown exception / a failed request in prod |
| **Problem** | The actual bug in the code causing it |
| **Root Cause Analysis** | Debugging — stack trace, logs, git blame, bisecting |
| **Known Error** | A filed, triaged bug ticket with root cause identified, but not yet fixed |
| **Workaround** | A hotfix / feature flag / retry logic — patches the symptom, doesn't touch root cause |
| **Permanent fix** | The actual PR that resolves the root cause |
| **Change Management** | Your PR review + deploy pipeline |
| **KEDB (Known Error Database)** | Your bug tracker (Jira, GitHub Issues) — a queryable place so nobody re-discovers the same bug from scratch |

## The workflow, dev-style

1. **Incident happens** — 500 errors spike, on-call gets paged, you restart the pod or roll back. Service restored. That's it, that's incident management — pure "get it green again."
2. **Pattern shows up** — this is the third time this pod's OOM-killed this month. Someone (hopefully) says "this isn't a one-off, this is a Problem."
3. **RCA / debugging** — you actually profile it, find the memory leak in that one service, maybe it's an unclosed DB connection pool.
4. **Known Error logged** — ticket filed: "Confirmed leak in `OrderService`, connections not released on timeout path. Workaround: bump memory limit + restart via cronjob. Fix: pending, needs connection pool refactor."
5. **Workaround ships fast** — maybe a memory limit bump, a scheduled restart, a feature flag to bypass the code path. Buys time, doesn't fix anything.
6. **Permanent fix goes through the normal SDLC** — branch, PR, tests, review, deploy. Root cause actually eliminated.
7. **Problem closed** — ticket closed, known error retired, workaround removed since it's no longer needed.

## Why devs should actually care about this (not just ops)

- **Without it, you're the one paged repeatedly for the same thing.** RCA is what breaks that cycle — it's literally in your self-interest to push for it instead of just eating the pages.
- **A Known Error Database is basically a shared "gotchas" doc for your team** — new engineer doesn't have to rediscover "oh yeah that flaky test always fails on Fridays because of timezone handling."
- **Workarounds that never get promoted to real fixes are the definition of tech debt.** If you've ever seen a `// TODO: hack, fix properly later (2019)` comment still in prod — that's an unmanaged known error.

## The one-line version

**Problem Management is just "root-causing and fixing bugs" formalized into a repeatable process** — so that fixing something once actually means it stays fixed, instead of your team quietly building a folklore of workarounds nobody wrote down.

Want me to go through how this maps onto something like Sentry/PagerDuty + Jira as an actual toolchain, since that's probably closer to what you'd wire up day-to-day?

===========================================

<img width="1254" height="1254" alt="ChatGPT Image Jul 28, 2026, 10_47_06 AM" src="https://github.com/user-attachments/assets/2d601abd-9215-4311-8165-d449e6a738c4" />
