# Decisions Log

## D0: Project name and license
- **Question:** What do I call the project, and which license do I use for my own code?
- **Options:**
  - Name A: `money-mule-detector` (clear and easy to search, though generic) [opinion]
  - Name B: a shorter graph/risk name (such as `mule-graph-risk`, or rename later if needed) [opinion]
  - License A: MIT (short, simple, permissive) [opinion]
  - License B: Apache-2.0 (permissive, includes an express patent grant) [opinion]
  - License C: no license (others cannot legally reuse the code) [opinion]
- **Choice:** Name: `money-mule-detector` (working name). License: MIT (matches `LICENSE` in the repo root; covers my code only, not third-party datasets or papers). [opinion]
- **Why:** The name tells recruiters and other developers what the project does right away without guessing. MIT is short and permissive, so people can read, run, and build on the code easily. [opinion]
- **What would change my mind:** If the project expands noticeably beyond mule detection (such as identity signals, risk decisions, and multi-app API integration) and a sharper name fits better, I can rename it. If I bring in a dependency under a copyleft license (like GPL/AGPL) that requires compatible licensing, I would reconsider. [opinion]
- **Date:** 2026-11-25

## D1: Four transaction graph patterns to detect
- **Question:** Which 4 patterns will I detect first?
- **Options:** The eight patterns in the IBM paper: fan-in, fan-out, bipartite, stack, random, cycle, scatter-gather, gather-scatter.
- **Choice:** Fan-in, fan-out, cycle, scatter-gather.
- **Why:** Fan-in and fan-out are simple shapes that work with rules first. Cycle and scatter-gather show money being layered across accounts. Four patterns is enough for one person to build well.
- **Risk I found in review:** Honest users also make these shapes. Payroll is a fan-out. A market seller is a fan-in. Nigerian thrift groups like ajo or esusu may look like cycles [opinion, check this]. The shape alone is not enough. I also need amount, speed and account age.
- **What would change my mind:** If a pattern is too rare in the data, or gives too many false alerts even with amount, speed and account age, I will swap it for another pattern.
- **Date:** 2026-11-26

## D2: Nigerian signals to model
- **Question:** Which Nigerian identity and device signals will I model?
- **Options:** shared device, BVN reuse, new-account bursts, fast pass-through, agent cash-out.
- **Choice:** One device used on accounts of different people. New accounts that appear together. Money that passes through fast. BVN is context only, not proof.
- **Why:** One BVN on many accounts is normal. It is one person. A device or phone shared across different people is a stronger warning. CBN rules on device binding and new accounts point at the same signals.
- **Honest data rule:** My generator makes the data, so it can make the answer too easy. If I plant shared devices only in mule rings, the model will learn the trick. I will add honest cases, like a family sharing one phone, plus noise.
- **What would change my mind:** If a signal adds noise and does not separate rings from normal users, I will drop it or swap it for agent cash-out.
- **Date:** 2026-11-26

## D3: One-sentence thesis
- **Question:** What is my thesis in one sentence?
- **Options:**
  - A (broad): A fraud-risk service should follow money trails because AI can fake a person.
  - B (product): An API that finds mule rings from transaction graphs and shared device and ID signals, and returns allow, step-up or hold with reasons.
  - C (narrow): A batch tool that helps fraud analysts investigate rings after the fact, with no live decisions.
- **Choice:** B. DRAFT: "AI can fake a person, but it cannot hide the money trail. My API finds mule rings from transaction graphs and shared device and ID signals, then returns allow, step-up or hold, with reasons."
- **Why:** The $129M case shows attackers fooling people but still leaving a trail across accounts and crypto. Nigerian rules already push for device and ID checks. I will not claim to detect deepfakes.
- **Test:** Say it in 15 seconds. Change any word you would not say.
- **What would change my mind:** If graph features plus identity signals do not beat simple rules in my tests, I will narrow it to option C.
- **Date:** 2026-11-26

## D4: Main user persona
- **Question:** Who is my main user: a fraud analyst or a developer integrating the API?
- **Options:**
  - Option A: Developer integrating the API (calls the risk service from apps like PayMesh and a second demo app to score transactions and act on allow/step-up/hold decisions) [opinion]
  - Option B: Fraud analyst (uses the dashboard to inspect mule rings, graph links, and alert reasons during investigations) [opinion]
- **Choice:** Developer integrating the API as the primary user, with the fraud analyst dashboard supporting review and inspection of flagged rings. [opinion]
- **Why:** Making the integrating developer the primary user keeps the core product focused on a clean, reusable risk API that multiple apps can call to enforce allow, step-up, or hold decisions inline. At the same time, including clear reason codes and a ring graph view helps analysts understand why a transaction or cluster was flagged rather than treating the score as a black box. Starting with one clear primary persona helps me stay focused within my solo build timeline. [opinion]
- **What would change my mind:** If during prototyping I find that graph-level ring inspection and analyst review workflows are far more compelling or easier to demonstrate clearly than inline API integration across two demo apps, I would flip the primary focus to the fraud analyst. [opinion]
- **Date:** 2026-11-26