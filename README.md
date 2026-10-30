# MATACS-TH-2026-02: AI Proposal Triage Design

**Name:** Shumail Fatima Arshad
**Reference:** MATACS-TH-2026-02
**Time spent:** about 7 hours over 3 days

## How I used AI

I used Claude to explain the brief, to talk through where AI should and should not be used, and to check my drafts of the diagram, prompts and write-up. The design decisions are mine. Where I disagreed with or corrected it:

- The AI suggested running the extraction twice and flagging proposals when the runs disagreed. I removed this, because it doubles the AI cost and would not catch a misreading repeated both times. Step 6 instead checks every fact and quote against the proposal text, and the reviewer is the final check at step 11.
- The AI suggested that an unclear mandatory criterion should be flagged for a person. I decided it must always be ineligible, because mandatory criteria are pass/fail and "not stated" fails them. The reviewer can still contest the result at step 11.
- The AI first said a criteria change would only repeat the scoring steps and that the diagram needed no change. I pointed out that the diagram had no path for this and would re-run the AI extraction, which led to step 2b (reuse saved facts) and the re-score arrow.

## Files

- [WRITEUP.md](WRITEUP.md): answers to the five questions and my assumptions
- [PROMPTS.md](PROMPTS.md): the extraction prompt (step 5) and the explanation prompt (step 10b)
- [ranking.json](ranking.json): my expected ranking of proposals A to E
- [diagram/flow.pdf](diagram/flow.pdf): process flow from upload to ranked output