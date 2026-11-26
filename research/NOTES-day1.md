# Day 1 Notes: Understanding the Problem (RQ1 to RQ4)
Date: 2026-11-26

## Block 1.1: Laundering Basics & Core Concepts
- **Money mule definition:** Someone who transfers or moves illegally acquired money on behalf of someone else [verified — FBI IC3 PSA191204; Europol Money Muling page].
- **Mule types:**
  - *Unwitting / unknowing:* Unaware they are part of a larger fraud/laundering scheme [verified — FBI IC3 PSA191204].
  - *Witting:* Ignores obvious red flags or acts willfully blind to their money-movement activity [verified — FBI IC3 PSA191204].
  - *Complicit:* Aware of their role and actively participates (often receiving a commission or cut) [verified — FBI IC3 PSA191204; Europol].
- **Cybercrime link:** More than 90% of money mule transactions identified in European operations were linked to cybercrime [verified — Europol Money Muling page].
- **Three stages of money laundering:**
  - *Placement:* Introducing illicit funds from criminal activities (e.g., extortion, loan sharking, gambling, kidnapping, robbery, embezzlement, drugs, smuggling) into the financial system [verified — IBM AMLworld paper, Section 3.3].
  - *Layering:* Moving illicit funds through the financial system across accounts/transactions to conceal their origin [verified — IBM AMLworld paper, Section 3.3].
  - *Integration:* Spending or deploying the laundered funds so they appear to come from legitimate sources [verified — IBM AMLworld paper, Section 1 & 3.3].
- **Why graphs over relational tables alone:** Relational tables are standard for storing transactions, but financial transaction graphs (with accounts as nodes and directed transactions as edges) expose connectivity and multi-hop interaction patterns that single-row views miss [verified — IBM AMLworld paper, Section 1].

## Block 1.2: Transaction Graph Patterns & Recruited Mules Observation
- **Eight AML patterns modeled in IBM AMLworld (drawn by hand):** `fan-out`, `fan-in`, `gather-scatter`, `scatter-gather`, `simple cycle`, `random`, `bipartite`, and `stack` [verified — IBM AMLworld paper, Section 3.2 & Figure 2].
- **Observation — Launderer-controlled vs. recruited mule accounts:**
  - In the IBM synthetic generator, a single laundering entity controls all accounts in a pattern [verified — IBM AMLworld paper].
  - In real mule schemes, many accounts belong to recruited individuals rather than one operator [opinion].
  - **How this changes detection:**
    1. Don't rely on single-owner assumptions; look for coordinated timing and fast pass-through windows across accounts [opinion].
    2. Look for behavioral shifts relative to an account's own normal history (sudden pass-through spikes or new recipients) since recruited mules mix everyday spending with mule transfers [opinion].
    3. Pair graph shapes with shared identity/device links (shared devices, BVN-style ID links, new-account bursts, shared cash-out endpoints) to separate mule rings from normal peer-to-peer splits [opinion].
    4. Weight short time-and-hop velocity, not just static graph topology [opinion].

## Block 1.3: Nigerian Fraud Context (Losses, CBN Rules, Identity, Liability)
- **Fraud loss figures:**
  - *2024:* ₦52.26 billion in fraud losses across 70,111 cases [verified — Vanguard, Jan 22, 2026, citing NIBSS MD Premier Oiwoh].
  - *2025:* ₦25.85 billion in fraud losses (down 51% YoY) across 67,518 cases (down 4% YoY). Internet banking recorded ₦13.37 billion across 4,507 cases; social engineering accounted for 47% of fraud volume and ₦17.84 billion in losses; Lagos accounted for over 63% of fraud volume [verified — Vanguard, Jan 22, 2026].
  - *Q1 2025 (FITC data):* Fraud losses jumped 603% YoY to ₦3.29 billion across 12,347 reported cases alongside ₦284.99 trillion in instant payments volume [verified — TechCabal, Dec 2, 2025 & Mar 13, 2026].
- **CBN & NIBSS requirements and initiatives:**
  - *Response times:* Target reducing fraud response times to under 30 minutes (and notifying counterparty institutions within 30 minutes on cross-institution APP fraud) [verified — Vanguard, Jan 22, 2026; TechCabal, Dec 2, 2025].
  - *Onboarding & liveness (March 12, 2026 circular; July 1, 2026 deadline):* Mandatory liveness verification and real-time BVN/NIN validation for account opening and reactivation [verified — TechCabal, Mar 13, 2026].
  - *Device binding & 24-hour cap:* Mobile banking apps restricted to one active device at a time, extra MFA for new-device logins/migrations, and a ₦20,000 inflow/outflow cap for the first 24 hours after mobile app activation [verified — TechCabal, Mar 13, 2026].
  - *Real-time monitoring & reporting:* Predictive/real-time enterprise fraud monitoring (with AI/ML recognized in compliance standards), zero tolerance for non-reporting, and industry watchlists [verified — Vanguard, Jan 22, 2026; TechCabal, Mar 13, 2026].
- **BVN & NIBSS Person of Interest Portal:**
  - *BVN:* 11-digit biometric financial identifier linking an individual's accounts across banks for real-time validation; in a graph, shared BVNs can act as hub/star links or cross-institution bridges, though legitimate multi-account ownership means it is a context signal rather than standalone proof [verified definition; opinion on graph modeling].
  - *NIBSS Person of Interest Portal:* Central watchlist/database (built with CBN, NFIU, and security agencies) holding records/photos of 3,417 flagged individuals since 2019, integrated with industry watchlists and over 214,000 PEPs [verified — Vanguard, Jan 22, 2026].
- **Who pays (draft APP fraud guidelines & 2024 directive):**
  - *Draft APP fraud framework (Nov 26, 2025):* Customers report within 72 hours; banks acknowledge within 24 hours, investigate within 14 working days, and refund within 48 hours of conclusion (16 working days total across institutions) [verified — TechCabal, Dec 2, 2025].
  - *Liability:* If an institution fails to flag/freeze due to inadequate systems, that institution bears the cost; if neither customer nor institutions are at fault (and customer is eligible), banks share the refund equally [verified — TechCabal, Dec 2, 2025].
  - *Receiving-bank debiting:* In 2024, CBN instructed NIBSS to debit commercial banks receiving fraud proceeds [verified — TechCabal, Dec 2, 2025].

## Block 1.4: The $129M AI Impersonation Case & Fourthline Survey
- **What was fooled:** Employees (including accounting staff) were deceived by spoofed CEO emails, AI-cloned executive voices/video calls ("super intelligence"), and impersonated law-firm attorneys pushing secret wire transfers [verified — DOJ SDNY Press Release 26-317, Nov 5/6, 2026; CBS News, Nov 6, 2026].
- **What stayed traceable:** International wire transfers to bank accounts across multiple countries (US, Spain, Portugal, Greece, UAE, Singapore, Austria, Slovakia, China), subsequent conversion to cryptocurrency, and distribution among conspirators [verified — DOJ SDNY Press Release 26-317].
- **Where a risk engine could act:** Flagging abnormal high-value wires or sudden beneficiary changes, detecting rapid cross-account pass-throughs and crypto off-ramp patterns, and triggering step-up verification or holds instead of trusting front-end voice/video calls [opinion].
- **Fourthline Fraud & Authentication Report 2026:** 78% of surveyed Europeans (6,000 adults across UK, France, Germany, Spain, Italy, Netherlands; Aug 15–31, 2026) said they would accept a slower, more thorough verification process if it meaningfully reduced fraud risk [verified — Fourthline Report 2026]. *(Note: European sample, not Nigeria—use only as supporting evidence on friction tolerance, not local proof [opinion]).*

## Day 1 Reflection (Block 1.5)
- **What I learned:** Single transfers often look ordinary in isolation, whereas network structure, timing velocity, and shared identity/device signals reveal coordinated mule activity [opinion].
- **What surprised me:** How strongly recent CBN rules (device binding, 24-hour new-app caps, 30-minute response targets) align with graph and velocity signals—and that most surveyed consumers actually accept extra verification friction when it protects against fraud.
- **What I still need to check (Day 2):** How the IBM AML-Data CSV columns are structured, what percentage of rows are labeled laundering, and what identity/device fields are missing that my synthetic generator will need to add [unverified].