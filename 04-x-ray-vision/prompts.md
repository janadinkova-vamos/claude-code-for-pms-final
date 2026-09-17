# 04 · X-Ray Vision — prompts

**Context:** You joined Rook two weeks ago as PM on Dispatch.
Release 4.2 shipped on 12 August, just before you arrived, and
landed badly. Last session the numbers showed you what happened: a
ping used to wait ninety seconds and now it waits sixty, people
missed pings they used to catch, and missing one counts the same as
turning one down — so four responders stopped hearing from us
altogether.

At the end of the session, ask Claude Code to save the prompts you
wrote yourself below — not the starter prompt. The closing slide has
the exact prompt to paste. By Module 6 this file is a prompt library
built from your own questions.

---

### 1.

Act as a Senior Product Manager joining Rook Dispatch for the first time.
Do not investigate Release 4.2 yet.
Your first task is to help me understand the product itself from the repository.
Rook Dispatch is responsible for getting the right superhero to an emergency. It determines who is eligible, close enough and available enough to help, then contacts responders.
Analyze the repository and reconstruct the product from a Product Management perspective.
I want to understand:

* Who are the primary users and stakeholders?
* What Jobs To Be Done does Dispatch solve for each of them?
* What is the core end-to-end user journey?
* What happens from the moment an emergency enters the system until a responder accepts or the system escalates?
* What are the most important product decisions made during that journey?
* What does "success" appear to mean for Dispatch?
* Where are the critical moments of truth in the experience?
* Which failures would create the greatest user or operational impact?
* What other Rook products or systems depend on Dispatch?

Do not infer a 4.2 root cause.
For every conclusion, identify:

* evidence from the repository,
* whether it is a fact or hypothesis,
* what remains unclear.

Output:

1. Product purpose
2. Primary users/personas
3. Jobs To Be Done
4. End-to-end dispatch journey
5. Critical product decisions
6. Likely success metrics
7. Critical failure points
8. Dependencies with other systems
9. Open product questions I should clarify with stakeholders

Finish with a simple:
Emergency → Decision → Contact → Response → Escalation → Resolution
journey map showing what happens at each stage.

### 2.

Now act as a Senior Product Manager working closely with Engineering.
Using the product understanding from the previous analysis, inspect the repository to explain how Rook Dispatch actually implements the core product experience.
Do not investigate Release 4.2 yet.
Focus specifically on the decision system that determines:

* which responders are eligible,
* how availability is determined,
* how proximity is calculated,
* how responders are ranked,
* who gets contacted first,
* how responders are contacted,
* how long the system waits,
* what happens when someone does not respond,
* how retries and escalation work,
* when the dispatch process ends.

Trace the relevant code path end-to-end.
For each step explain:

1. Product rule
2. Technical implementation
3. Inputs/data used
4. Output/decision produced
5. Dependencies
6. Potential failure modes
7. User impact if that step behaves incorrectly

Identify:

* business rules embedded in code,
* hard-coded thresholds,
* configuration values,
* fallback logic,
* edge cases,
* asynchronous processes,
* external services,
* assumptions that may not be obvious to a PM.

Create a simplified architecture and decision-flow diagram in text.
I should finish this analysis able to explain to another PM or executive:
"This is how Rook Dispatch decides who to contact and what happens next."
Clearly distinguish confirmed repository behavior from assumptions.

### 3.

Now that we understand both the product and its implementation, investigate Release 4.2, shipped on 12 August.
The goal is to identify where the behavior introduced by 4.2 diverged from the intended product experience.
Compare the last stable version before 4.2 with Release 4.2.
Focus on changes affecting the critical product journey previously identified, especially:

* eligibility,
* availability,
* proximity,
* responder ranking,
* contact order,
* contact method,
* retry behavior,
* timeout logic,
* escalation,
* fallback behavior.

For each change identify:

1. What the product did before 4.2
2. What it does after 4.2
3. Which part of the user journey changed
4. Which user or stakeholder is affected
5. Expected behavior
6. Potential unintended behavior
7. Likely metric impact
8. Evidence from the code
9. Confidence level

Then construct a:
Release 4.2 Impact Tree
Release change
→ system behavior
→ user experience
→ responder behavior
→ dispatch outcome
→ business/operational impact

Do not conclude that a change caused the reported decline unless the repository provides sufficient evidence.
Instead, end with the 3–5 strongest hypotheses that should now be tested against:

* weekly metrics,
* responder feedback,
* complaints,
* operational data.

For each hypothesis state what evidence would confirm or disprove it.

### 4.

Open the folder 00-rook/code/dispatch-routing/. This is the part of our software that decides who gets asked to take a job. I have never read code before and I am not going to start now. Walk me through what happens from the moment something goes wrong somewhere to the moment a responder's phone buzzes, in plain English, no jargon. Then tell me which file each step lives in. please explain as if I am 5

### 5.

Has anything in this code changed recently? Walk me through what's different, and why it would matter to a responder. HELP me understand it in a more simple way, considering that I have a very strong PM background but no code experience.

### 6.

can you explain in visual way

### 7.

so basically  because one of the main changes was response time from 90 to 60, it shifted the whole priorization and work logic behind the job delivery. it this correct?

### 8.

make a decision map of before and after. do write the pros and cons of before and after the release

### 9.

show me where in the code there is a proof for your feedback.

### 10.

Based on what I found, the reason some responders are getting no pings at all is ___, because ___. state my hypothesis as a senior product manager

### 11.

can you prove this with the actual data?

### 12.

Using `callout-history.csv`, test the hypothesis from Lab A that Release 4.2 changed how callouts are distributed across responders.
Compare responder-level `pings_sent` before and after the 12 August release.
Tell me:

* which responders received materially fewer callouts,
* which received materially more,
* whether the distribution became more uneven after 4.2,
* and whether the data supports or contradicts the hypothesis that the new routing weights concentrated callouts on a smaller group of responders.

Do not assume causation from correlation. Give me the clearest evidence and any contradictions in the data.

### 13.

Find me the part of this code that takes points off somebody when they miss a ping or turn one down. Show it to me and explain it in plain English. Then find me every single thing in this code that puts points back on. walk step by step what happens when someone doesn't get a ping - what is the lifecycle of gaining and losing points. can you get the points back?

### 14.

what happens when a superhero goes on vacation? what happens with their score?

### 15.

exactly when you go on vacation, you dont get promoted
