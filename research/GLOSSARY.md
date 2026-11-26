# Glossary

Sources in brackets. Verify the starred terms on Day 2.

1. **Money laundering:** Moving illegal money through accounts and transfers to hide where it came from. [IBM paper]
2. **Money mule:** A person who moves illegal money for someone else. [FBI IC3, Europol]
3. **Unwitting mule:** A person tricked into moving stolen money, for example by a fake job offer. [FBI IC3]
4. **Witting mule:** A person who ignores clear warning signs and moves the money anyway. [FBI IC3]
5. **Complicit mule:** A person who knows the money is illegal and helps, often for a fee. [FBI IC3]
6. **Mule ring:** A group of linked accounts that move illegal money together. My working term for this project.
7. **Placement:** Stage 1. Illegal money enters the financial system. [IBM paper 3.3]
8. **Layering:** Stage 2. Money moves through many accounts to hide its origin. [IBM paper 3.3]
9. **Integration:** Stage 3. The money is spent or used so it looks legitimate. [IBM paper 3.3]
10. **Smurfing*:** Splitting money into many small amounts, often across many people or accounts.
11. **Structuring*:** Splitting amounts to stay under a reporting limit. Related to smurfing but not the same.
12. **Transaction graph:** Accounts are nodes. Transfers are directed edges. [IBM paper 1]
13. **Directed multigraph:** A graph where two accounts can have many transfers between them, each with a direction. [IBM paper 1]
14. **Fan-out:** One account sends money to at least 2 different accounts. [IBM paper 3.2]
15. **Fan-in:** At least 2 different accounts send money to one account. [IBM paper 3.2]
16. **Gather-scatter:** One account gathers money from many (fan-in), then sends it to many (fan-out). [IBM paper 3.2]
17. **Scatter-gather:** One account sends money out to the same set of middle accounts, and another account collects it. [IBM paper 3.2]
18. **Cycle:** Money leaves an account and comes back to it through other accounts. [IBM paper 3.2]
19. **Random pattern:** Like a cycle, but the money does not return to the start. [IBM paper 3.2]
20. **Bipartite pattern:** Money moves from one group of accounts to another group. [IBM paper 3.2]
21. **Stack pattern:** A bipartite pattern with one more layer added. [IBM paper 3.2]
22. **Authorised push payment (APP) fraud:** A victim is tricked into sending a real payment to a fraudster. [TechCabal refund article]
23. **BVN (Bank Verification Number):** A Nigerian 11-digit ID that links a person's bank accounts across banks. [Vanguard, TechCabal]
24. **Device binding:** A mobile banking profile works on one device at a time. A new device needs extra checks. [TechCabal liveness article]
25. **Step-up verification:** Asking for extra checks before a risky transfer goes through. [TechCabal liveness article]
