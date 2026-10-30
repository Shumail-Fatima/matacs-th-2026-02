## 1. AI vs rules

AI is used in only two places: step 5, which turns messy, varied proposal text into structured facts, and step 10b, which words the explanation for each ranking. Steps 1–4, 2b, 6–9 and 10a are plain code or rules, and steps 11 and 12 are human decisions.

I drew the line here because AI is good at reading text that varies between proposals, while rules are better wherever there is a right answer (pass/fail, arithmetic, sorting): they are exact, repeatable, free, and can’t be talked into things. In short, AI turns text into facts and code turns facts into decisions.

A proposal may contain text meant to manipulate an AI reviewer, but the AI only extracts facts and never scores or ranks, so even a fooled AI cannot change a score. At step 10b the ranking is already fixed before the AI writes a word.

## 2. Consistency and explainability

Would ranking the same proposals twice give the same result? Yes for scoring and ranking. Extraction is the only step that could vary, so the design reduces that and checks its output.

Scoring is fixed code, so unless the extracted facts change, scores never change. Ties are settled at step 10a by higher experience points, then lower price; if still tied, both are shown to the reviewer. At step 10b only the wording can differ, never the order.

At step 5, a fixed prompt, pinned model version and low-randomness setting reduce variation. Extracted facts are saved against a fingerprint of the file (taken at step 1, including any clarification), prompt version and model version, and step 2b reuses them, so ranking the same files again uses identical facts. Step 6 checks every fact against the proposal text: the quote must appear word for word and the number must match it. Any mismatch is flagged.

Explainability: the reviewer sees each criterion’s score and weighted points, with the evidence quote beside each fact, so any number can be checked against the original.

## 3. Human in the loop

Step 11. The reviewer sees the recommended ranking, flagged and ineligible items with reasons, and the evidence quotes. They can confirm or override the ranking, resolve a flagged item, contest or uphold an ineligible result, or re-score under a new criteria version. Every override or reversal needs a written reason.

Missing information. For a flagged proposal, the reviewer can obtain a clarification from the bidder and add it as new evidence. Only that proposal goes back through the loop (to step 3), and the ranking is recalculated; the earlier result stays in the log.

Step 12. The tool only recommends. No award is made unless a person confirms it.

Audit log. At every step it records who did what and when, file fingerprints, criteria, prompt and model versions, extracted facts with quotes, scores, flags, and any override with its reason.

## 4. Changing criteria

Criteria are versioned: an admin edit is saved as a new version and never overwrites the old one. A run uses the version stamped at step 2 from start to finish, so all its proposals are scored consistently even if an edit happens mid-run. Earlier results keep their label, “scored under criteria version X”.

At step 11 the reviewer can choose to re-score under the new version, which restarts the run at step 2. Step 2b checks whether verified facts are saved for each file fingerprint, prompt version and model version, including every field the new criteria need. If so, the proposal skips reading and extraction and re-enters at step 7, so only the rule steps 7 to 10 repeat, with no new AI cost; results are labelled “scored under criteria version Y”. Otherwise (new file, changed file, newly required fact) it goes through steps 3 to 6.

The reviewer compares the before and after rankings and decides which to use. Once an award is confirmed, its criteria are locked so the record stays accurate.

## 5. Risks

| **Risk**                             | **Safeguard**                                                                                                                                                       |
|--------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Wrong extraction                     | Step 6 checks each fact against the proposal text: quote word for word, number matching the quote. Mismatches are flagged. |
| Made-up facts                        | The prompt requires not_stated and an exact quote; step 6 rejects any quote not in the text.                                                                        |
| Manipulation (Proposal C)            | Three layers: step 4 scan, the prompt’s data-only rule, code-only scoring. Flag, log, send to a human.                                                              |
| Bias                                 | Only the admin’s criteria are extracted and scored; company name and size are not.                                                      |
| Cost                                 | Extract once, reuse saved facts at step 2b, cap file size at step 1.                                                                                                |
| Missing or unclear data (Proposal D) | Never guess. A missing value behind a hard limit is flagged (proposal D); a missing, unclear or failed mandatory criterion is ineligible (proposal B).              |
| AI failure or wrong file             | Unusable AI output fails step 6 and is flagged; a wrong file fails step 7 and is ineligible.                                                                                           |
| Over-reliance                        | A human decides at step 12; all reasons and evidence are visible.                                                                                                   |

Limits: the step 4 scan can be dodged by rewording, which is why the other layers exist. Verification cannot catch a real quote that is misread, so step 11 is the final check.

## Assumptions

- C is flagged and not scored: suspected manipulation always goes to a person. Ranking it with a warning would also be defensible.
- D is flagged because a missing value behind a hard limit could change the ranking. A missing detail on a scored item earns low points instead.
- A mandatory criterion that is missing, unclear or failed makes the proposal ineligible, with no further scoring.
- Price and timeline use adjustable anchors ($195,000 and 8 weeks) stored in the criteria, not the code.
- Ties: higher experience points, then lower price, then both shown to the reviewer.
- Installs are counted as stated; borderline dates are left to the reviewer.
- Over-limit bids are flagged, not rejected.
