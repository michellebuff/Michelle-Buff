<!-- PR TARGET: https://github.com/michellebuff/Michelle-Buff | Stage 1.2 (8 pts) -->
# Stage 1.2 review — spec, build, audit

**Spec-side 61 out of 62.5 — held, not entered. The workbook is not due until 6 September and none was expected yet.**

**Spec:** [`capabilities/marginal-analysis/spec.md`](https://github.com/michellebuff/Michelle-Buff/blob/main/capabilities/marginal-analysis/spec.md)

> Re-graded 2026-08-31. Your previous spec-side result was 57 of 62.5. You closed both gaps I named and the validation section is now full marks — it is one of the two best in the cohort and it caught something before I could tell you about it.

| Criterion | Earned | Notes |
|---|---|---|
| Spec completeness — inputs, structure, calculation flow | 36 / 37.5 | Up from 35. The derived-input rule is now explicit and enforced — FARMER_PAID_HOURS as 40 x SEASON_WEEKS, FARMER_FIELD_RATE from salary over paid hours, TEMP_RATE from salary over hours, and carrot labor as 2.50 / 3 rather than the displayed 0.833 — with the rule stated underneath that derived values must never be replaced with rounded hard-coded ones. A workbook in this cohort has that exact defect live right now and its profit is $13 off because of it. The non-monotonic crossing rule is new and correctly stated as an upward scan to the first crossing. The zero-hours guard on the blended rate is the detail I want to point at: you required it, and you wrote down why — Solver must run from 0/0/0 as part of the audit, an unguarded division returns #DIV/0! at that point, and that would fail your own structural check. A rule with its reason attached survives a builder who thinks it is unnecessary. The remaining point and a half is that TEMP_WORKERS_NEEDED has no rounding rule stated — you clearly intend fractional, since your acceptance figure is 3.165 workers, but a builder could reasonably read the constraint as a headcount and round up. |
| Spec validation rules | 25 / 25 | Full marks, up from 22, and every one of the three gaps I named is closed. Every acceptance figure now carries a tolerance. The Solver two-starting-point procedure is specified. And the labor anchor at q = 10 is in, with the reason written into the spec rather than left implicit: "This second check verifies that the 10% diminishing-return factor is compounded across the full crop quantity rather than applied only once." That is exactly right, and it is the check that catches the one defect a q = 1 anchor cannot see. |
| Workbook satisfies the contract | 0 / 25 | No workbook yet, and none was due. Nothing is lost here — this is what the stage expects at this point, and writing the specification first is the entire method. |
| Audit note | 0 / 12.5 | Correctly a stub, and the stub already names the four questions each finding must answer: what was checked, what the check was intended to catch, what was found, and what action was taken. The second of those is the one most people leave out and it is the one that makes a finding evidence rather than a note. |
| **Spec-side subtotal** | **61 / 62.5** | the part that can be earned before a workbook exists |

### The rule that matters most in your spec

"If any validation check fails because the specification is incomplete or ambiguous, the specification must be corrected and committed before the workbook is regenerated. The workbook must not be manually patched to force a passing result."

That is the whole discipline of this stage in two sentences, and you are the only person who wrote it down as a rule rather than following it implicitly. The reason it matters: a workbook patched by hand still passes its checks, and the spec beside it now describes a model that does not exist. Six months later the spec is the only documentation and it is wrong.

Hold yourself to it when the first check fails, because that is when it will feel expensive.

### The MC dip

Your structural checks include "The tomato marginal-cost dip around six beds should be visible and noted for later analysis, but it should not be artificially created or explained in the model." Both halves of that are right and the second half is the subtle one.

A model that expects a dip can be nudged into producing one. Requiring the dip to be visible and explicitly forbidding yourself from explaining it in Stage 2 is how you keep the observation independent of the interpretation. Stage 3 is where the explanation goes.

### What to do next

Build it. The specification is ready and there is nothing left to decide in it.

One sequencing suggestion: build the standalone marginal-cost schedules before the optimization. They are the part your Stage 1.1 brief is a prediction about, they do not depend on Solver, and if they are wrong every downstream number is wrong in a way that is hard to see. The q = 1 and q = 10 anchors both live in that block, so you can validate the engine before anything else is built on top of it.

Then Solver from both starting points, then the Farm Profit Lab cross-check on one intermediate value, then the audit. Your spec already says to correct the spec rather than the workbook when something fails — that is the sentence to reread at that point.

### One organizational note

Your spec frontmatter still reads status: draft and date: 2026-08-23, and the document has moved substantially since then. Update both when you commit the version you build from — the date on a spec is a claim about when its decisions were made, and yours were made later and better.

### A note on the point value, new as of today

This stage is now worth **15 points** rather than the 8 in the stage brief, and **Stage 1.3** — the analysis, the memo, and the prompt log — is now worth **15** as well. Cases 2 and 3 have been dropped for this cohort, so Case 1 *is* the case.

In practice: this stage and the next one are together worth **30 of the 35 points** on the case. Stage 0 and Stage 1.1 are 2.5 each. The weight has moved onto the build and the analysis, which is where the work actually is.

Nothing about the grading changes — the score is still out of 100 and converted at the end. The stage brief and the case page still show the old numbers; they have not been updated yet.

---

### How to work this review

Treat this PR the way an analyst treats feedback from a senior reviewer — a review is a proposal to engage with, not a checklist to rubber-stamp.

1. **Read it yourself first.** Form your own view before you change anything. Disagreeing *with a documented reason* is a legitimate, senior response.
2. **Stress-test it with an LLM.** Paste this review and your spec into your assistant and ask it to (a) explain anything you are unsure of, and (b) argue the *other side* — where might the reviewer be wrong, and what would you give up by making each change.
3. **Then correct the spec, not the workbook.** This is the rule that makes the stage work: when a check fails, you fix the specification and regenerate, so the document keeps describing what was actually built.
4. **Close the loop.** Reply in this thread with what you changed and what you pushed back on, then commit and push.

*Nothing here is final. Stage 1.2 is not due until 6 September, and the stage is re-graded from scratch at the deadline.*

— Adam
