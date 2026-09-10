# 02 · Super Hearing — prompts

**Context:** You joined Rook two weeks ago as PM on Dispatch.
Release 4.2 shipped on 12 August, just before you arrived, and
landed badly. Last session you built a context file and met the
company.

You still do not know what actually went wrong.

At the end of the session, ask Claude Code to save the prompts you
wrote yourself below — not the starter prompt. The closing slide has
the exact prompt to paste. By Module 6 this file is a prompt library
built from your own questions.

---

### 1.

analyze Tickets file - give me a brief summary of them. let's think of an emergency coordination center system, like 911- I need to classify the tickets based on type/emergency level 0, 1 or 2- 0 is life thretening and absolute urgent, 1 needs to be done by specialized unit and 2 by a common practitioner. use this same logic in order to classify the tickets

### 2.

Act as a Senior Product Manager investigating a possible systemic problem in Rook Dispatch.
We see two recurring issues:

1. Callout offers expire before responders can realistically react.
2. Some responders then experience long quiet periods with few or no future callouts.

I want to know whether these are connected.
Important routing logic:

* responder ranking uses proximity, availability, capability match, and recent acceptance history
* a timeout or decline lowers recent acceptance history
* lower recent acceptance history lowers future routing priority

Possible feedback loop:
Short timeout
→ responder misses callout
→ acceptance history worsens
→ routing priority drops
→ responder receives fewer future callouts
→ long quiet period
Use the Rook files already in the project, especially:

* callout-history.csv
* interviews
* support tickets T-001 to T-020

Do not assume this hypothesis is correct. Try to confirm or disprove it.
Please:

1. Analyze the tickets and group them into:
   * Level 0: callout expires / responder cannot react in time
   * Level 1: responder is available but receives unusually few or no callouts
   * Level 2: normal usability or operational issue
2. Identify responders who appear in both Level 0 and Level 1 problems.
3. Analyze callout-history.csv for:
   * weekly pings sent
   * pings taken
   * take rate
   * responder-level trends
   * responders whose take rate drops before their future callout volume drops
4. Check whether the product logic, code, configuration, or roadmap changes could explain this pattern, especially:
   * Ping timeout tuning
   * Change to who gets pinged
   * Availability Confidence
5. Evaluate these hypotheses:
   * H1: timeout is too short for realistic human response
   * H2: missed/expired callouts reduce routing priority and create a negative feedback loop
   * H3: low callout volume is caused by another routing factor
   * H4: the system assumes users are paying continuous attention
   * H5: routing may work as designed but users cannot understand why callout distribution is uneven

For each hypothesis give:

* supporting evidence
* contradicting evidence
* missing evidence
* confidence: High / Medium / Low

Finish with:

* the main problem statement
* the most likely causal chain
* what we still do not know
* the 3–5 most important things Product should investigate next

Final verdict:
Is there evidence of a self-reinforcing:
timeout → lower acceptance history → lower routing priority → fewer future callouts
loop?
Answer:

* Yes — strong evidence
* Possibly — incomplete evidence
* No — evidence points elsewhere

Be skeptical and separate correlation from causation.

### 3.

you have read both folders interveiws and tickets - how do they agree or disagree? which hypothesis are supported by which. this is important because tickets tell one story - what is the reason for the call dispatch and interviews are opinions of the pain points of users. present the results in table

### 4.

how do you reconcile these to different piles of data?
