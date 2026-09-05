<!-- PR TARGET: https://github.com/michellebuff/Michelle-Buff | Stage 1.2 -->
# Stage 1.2 review — spec, build, audit

**Spec:** [`capabilities/marginal-analysis/spec.md`](https://github.com/michellebuff/Michelle-Buff/blob/main/capabilities/marginal-analysis/spec.md)

> Re-graded 2026-09-02 against your 1 September build. You have been reviewed on this before.5 with no workbook, which was the correct state at the time. The workbook now exists, it passes every check you wrote for it, and every value in it agrees with mine to the digit. This is the second full-marks submission in the cohort and it earned it on a different strength than the first.

| Criterion | Where it stands |
|---|---|
| Spec completeness — inputs, structure, calculation flow | Stronger this pass, and everything this criterion asks for. The remaining point and a half was TEMP_WORKERS_NEEDED having no rounding rule, and you closed it in one sentence that says the value is a fractional full-time-equivalent, must not be rounded up, and that the Solver constraint applies to the fractional value. That is the ambiguity gone. You also added a requirement I did not ask for and would not have thought to — that constraint-status cells must use conditional formatting so passes read green and failures read red — and you added it the right way round, by amending the specification first and regenerating the workbook from it. |
| Spec validation rules | Unchanged at everything this criterion asks for. Every acceptance figure carries a tolerance with a reason, the two-starting-point Solver procedure is specified, and the q = 10 labor anchor is in with its purpose written down. |
| Workbook satisfies the contract | Fifty-six named ranges, zero error cells, every calculated cell a formula, and numeric literals only where they belong — case inputs, q index columns, the three decision cells, and the acceptance targets. Every figure reconciles: profit $42,761.66, labor 5,277.2161 hours, 3.1647 temp workers, blended rate $19.7298, marginal cost $8,248.59 at tomato bed 10 and $9,390.72 at bed 11, crossings 10 / 10 / 6. FARMER_FIELD_RATE and TEMP_RATE are derived formulas and CAR_HRS is TOM_HRS/3 rather than 0.833, which is the defect that cost another workbook in this cohort a failed check. And you went past the contract: three identity checks (labor hours reconcile, variable plus fixed equals total, crop revenue sums to total) that catch a class of error the acceptance figures cannot. |
| Audit note | Five findings, each answering all four of the questions your own stub said a finding must answer. Two of them are real discoveries rather than confirmations — see below. The Farm Profit Lab cross-check is there and done properly: $61,827 to $71,218 across tomato beds 10 to 11 gives $9,391 against your workbook's $9,390.72. |

### The integer-constraint finding, which is the best thing in this submission

"Excel initially had 'Ignore Integer Constraints' enabled, which produced a fractional tomato result. The workbook's integer check flagged the result as non-integer."

Read what happened there. Solver returned an answer. The answer was wrong in a way that is almost invisible — a bed count of 10.0000001 displays as 10 — and it was wrong because of a setting buried in Solver's Options dialog that most people never open. Nothing about the output announced it.

It was caught because you had written a check for it before you ran anything. Not because you noticed, not because it looked odd, but because the specification said whole beds and you built a cell that tests whether the beds are whole. That is what a validation rule is for: it catches the failure you would not have been looking for.

The general version of this is worth carrying well past this course. The checks that pay for themselves are the ones written before you know what the answer looks like, because after you know, you write checks that the answer passes.

### The other thing that separates this workbook

Your Checks sheet has a row nobody else has: "Marginal-cost shape — beds where MC falls below the prior bed," counted programmatically per crop. It returns 1 for tomatoes and 2 each for carrots and mesclun.

You did not explain it — the specification says to note it and leave it for Stage 1.3, and you followed your own rule. But you built a cell that measures it, which means the observation is a number rather than an impression, and in Stage 1.3 you will be reasoning from data instead of from memory.

When you get there: the dip happens where the marginal labor source changes. The farmer's 720 hours are consumed first, so the bed that exhausts them is partly priced at her $34.72 an hour, and the next bed is entirely at the temporary rate of $17.36. A cost curve that falls in the middle looks like a bug and is not one.

### The rule from your spec that I keep quoting

"If any validation check fails because the specification is incomplete or ambiguous, the specification must be corrected and committed before the workbook is regenerated. The workbook must not be manually patched to force a passing result."

You wrote that before you had a workbook, and then this pass you had a real chance to break it — the constraint-status formatting was missing and the fast fix was to colour the cells by hand. Your audit records the other choice: "The specification was updated to require visible green/red constraint-status formatting and the workbook was regenerated from the revised specification."

That is the discipline this stage exists to teach, and following it when it costs you something is the only test of whether you have it.

### Stage 1.3

You have three things to write about and they are all already in your repository: the integer-constraint finding, the marginal-cost dip with the labor-source explanation behind it, and the comparison between your committed brief and what the model returned.

One standing rule: do not revise the brief to match the model. If they disagree, that is the finding.

---

### How to work this review

Treat this PR the way an analyst treats feedback from a senior reviewer — a review is a proposal to engage with, not a checklist to rubber-stamp.

1. **Read it yourself first.** Form your own view before you change anything. Disagreeing *with a documented reason* is a legitimate, senior response.
2. **Stress-test it with an LLM.** Paste this review and your spec into your assistant and ask it to (a) explain anything you are unsure of, and (b) argue the *other side*.
3. **Then correct the spec, not the workbook.** When a check fails, you fix the specification and regenerate, so the document keeps describing what was actually built.
4. **Close the loop.** Reply in this thread with what you changed and what you pushed back on, then commit and push.

*Your score and the per-criterion breakdown are in your Lamaku comment, not here — this repository is public.*

— Adam
