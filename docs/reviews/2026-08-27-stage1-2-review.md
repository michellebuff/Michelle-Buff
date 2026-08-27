<!-- PR TARGET: https://github.com/michellebuff/Michelle-Buff | Stage 1.2 (8 pts) -->
# Stage 1.2 review — spec, build, audit

**Held — not entered. Spec-side: 57 of the 62.5 points available before a workbook exists.**

**Spec:** [`capabilities/marginal-analysis/spec.md`](https://github.com/michellebuff/Michelle-Buff/blob/main/capabilities/marginal-analysis/spec.md)

> Graded early, at the instructor's request. Stage 1.2 is not due until 6 September and nothing was required yet. You have a specification and no workbook, which is exactly the right state to be in at this point — the stage is deliberately sequenced spec first. I am not entering a score, because 37.5 of the 100 points on this stage are for a workbook that does not exist yet and a number computed against those would say something false about the work. What follows is where the spec-side points stand and what to fix before you build.

| Criterion | Earned | Notes |
|---|---|---|
| Spec completeness — inputs, structure, calculation flow | 35 / 37.5 | This is a genuinely good specification and it gets three things right that have already cost other people real money in this cohort. First, your inputs table stores relationships rather than results: FARMER_FIELD_RATE is "50000 / 1440" and CAR_HRS is "2.50 / 3", not $34.72 and 0.833. The instruction underneath — "Derived values must be calculated from the underlying source values at full precision and must not be replaced with rounded hard-coded values" — is the single sentence that separates a workbook that reconciles from one that is a few dollars off for reasons nobody can find. Second, your labor function is right: q x HRS_PER_BED x SEASON_WEEKS x (1 + DIM_PCT)^q, with "labor must not be modeled as a simple linear function" stated explicitly. Third, and this is the one I would not have expected, you specified that the standalone marginal-cost schedules must be independent of the mix — "evaluated independently, with the other two crop quantities set to zero... not affected by the bed counts Solver selects." Two and a half points off for a small omission: TEMP_HOURS_PER_WORKER is 1,440 and FARMER_FIELD_RATE divides by 1,440 as well, and the second 1,440 is the farmer's total paid hours — a different quantity that happens to share a value. Sourcing it as "Derived from farmer salary and paid hours" is right, but the number itself is your derivation from 40 hours a week over 36 weeks, and the input table is the one place where derived and given should be visibly different. |
| Spec validation rules | 22 / 25 | Written before the build, which is what makes them tests rather than explanations. The published check figures are in as acceptance criteria — the mix, 60 beds, the profit, and all three standalone crossings — and you added the sentence that makes them safe: "They must not be hard-coded into calculated result cells or used to force Solver to produce the expected answer." That is the failure mode that nearly got past the strongest submission in this cohort, caught in advance. Two Solver starting points, the q = 1 hand check at 99 hours, structural checks on formulas and error cells, and the instruction not to force marginal cost to rise are all present. Three points off for two gaps. There is no tolerance on any figure — "approximately $42,762" cannot pass or fail, and $42,761.66 and $42,700 both satisfy it. Give each check a band: dollars to $1, hours to 0.01, quantities exact. And your only hand check is tomatoes at q = 1, which a wrong model can still pass; see the note below. |
| Workbook satisfies the contract | 0 / 25 | No workbook yet, and none was due. Nothing is lost here — this is simply the part of the stage you have not reached. |
| Audit note | 0 / 12.5 | The section exists with the right four questions — what was checked, what it was intended to catch, what was found, what was done about it — and it is empty, correctly, because there is nothing to audit yet. Writing the audit template before the build is the right order. |
| **Spec-side subtotal** | **57 / 62.5** | the part that can be earned before a workbook exists |

> Where this leaves you: 57 of 62.5 on the two spec criteria. The remaining 37.5 — 25 for a workbook that satisfies the contract and 12.5 for the audit note — become available once model.xlsx exists and you have audited it.

### The one thing I'd add before you build

Your q = 1 hand check asks for 99 hours from 1 x 2.50 x 36 x 1.10. It is a good check and it will not catch the most likely error in this model.

Here is why. Suppose a builder writes the labor function as base x 36 x (1 + rate) and sums down the column, applying the penalty to the marginal bed rather than to the whole crop. At q = 1 that returns exactly 99 hours and your check passes. At q = 10 it returns 990 hours where the correct function returns 2,334. The model is then wrong by more than a thousand hours on one crop and every downstream number is wrong with it, and nothing in your Checks sheet goes red.

This is not hypothetical. It is the defect in one of the two completed workbooks in this cohort, and that workbook's Solver returns a loss where the case returns a $42,762 profit.

The fix is one row: add a second anchor at q = 10. Tomato labor at 10 beds must be 10 x 2.50 x 36 x 1.10^10 = 2,334.4 hours. A model that gets the exponent wrong fails that immediately. One check that can only pass is worth less than two that can disagree.

### What else is worth tightening

- Put tolerances on every acceptance figure. "Approximately" is not a test. Profit within $1, hours to two decimals, bed counts exact, crossings within one bed. The reason this matters more than it sounds: without a band, a result that is close gets accepted by judgment, and the judgment is made by the person who wants it to pass.

- Add the labor figures to the acceptance table. The case publishes about 5,277 total labor hours and roughly 3.16 temporary workers at the optimum. Those two catch a whole class of error that the profit figure alone can hide, because profit is a difference of large numbers and two offsetting mistakes can land on it.

- Say what happens when a check fails. The rule that makes this stage work is: correct the spec and regenerate, do not patch the workbook by hand. Write that down. Otherwise the first failure gets fixed in the sheet, the spec quietly stops describing what exists, and the document you are graded on becomes fiction.

- Your Structure section names five sheets but not what a reader would see on each. Adding one line per sheet about layout — where the decision cells are, where the constraint flags live — costs you nothing and is the difference between a spec someone can build from and a spec someone has to interpret.

### Why the zero-hours guard is the best line in this spec

You wrote: BLENDED_LABOR_RATE = IF(TOTAL_LABOR_HRS = 0, 0, TOTAL_LABOR_COST / TOTAL_LABOR_HRS), and then "The zero-hours guard is required, not optional. Solver must be run from a 0 / 0 / 0 starting point as part of the audit, and an unguarded division would return #DIV/0! at that point — which would fail the structural check prohibiting error values."

That is three separate requirements reasoned into agreement with each other: the Solver protocol, the formula, and the acceptance criterion. You noticed that one of your own rules would break another one and you resolved it in the spec rather than discovering it mid-build. Most defects in models are exactly this shape — two reasonable requirements that quietly conflict — and they are almost always found the expensive way.

Keep doing that pass. Read your own spec asking "which of these rules fight each other," and write down what you find. It is worth more than any amount of additional detail.

### What happens next

Fix the two anchors and the tolerances first, then build. The order matters: a check figure added after a disappointing result is not a check, it is a negotiation.

When you audit the workbook, record at least three checks in the Audit Findings section, each naming what it would have caught, plus any defects you found and how you fixed them. That section is 12.5 of the 100 points and it is the one most people leave empty, because by the time the model works nobody wants to write down what was wrong with it.

---

### How to work this review

Treat this PR the way an analyst treats feedback from a senior reviewer — a review is a proposal to engage with, not a checklist to rubber-stamp.

1. **Read it yourself first.** Form your own view before you change anything. Disagreeing *with a documented reason* is a legitimate, senior response.
2. **Stress-test it with an LLM.** Paste this review and your spec into your assistant and ask it to (a) explain anything you are unsure of, and (b) argue the *other side* — where might the reviewer be wrong, and what would you give up by making each change.
3. **Then correct the spec, not the workbook.** This is the rule that makes the stage work: when a check fails, you fix the specification and regenerate, so the document keeps describing what was actually built.
4. **Close the loop.** Reply in this thread with what you changed and what you pushed back on, then commit and push.

*Nothing here is final. Stage 1.2 is not due until 6 September, and the stage is re-graded from scratch at the deadline.*

— Adam
