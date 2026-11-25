# Decisions Log

## D0: Project name and license
- **Question:** What do I call the project, and which license do I use for my own code?
- **Options:**
  - Name A: `money-mule-detector` (clear and easy to search, though generic)
  - Name B: a shorter graph/risk name (such as `mule-graph-risk`, or rename later if needed)
  - License A: MIT (short, simple, permissive)
  - License B: Apache-2.0 (permissive, includes an express patent grant)
  - License C: no license (others cannot legally reuse the code)
- **Choice:** Name: `money-mule-detector` (working name). License: MIT (matches `LICENSE` in the repo root; covers my code only, not third-party datasets or papers).
- **Why:** The name tells recruiters and other developers what the project does right away without guessing. MIT is short and permissive, so people can read, run, and build on the code easily.
- **What would change my mind:** If the project expands noticeably beyond mule detection (such as identity signals, risk decisions, and multi-app API integration) and a sharper name fits better, I can rename it. If I bring in a dependency under a copyleft license (like GPL/AGPL) that requires compatible licensing, I would reconsider.
- **Date:** 2026-11-25