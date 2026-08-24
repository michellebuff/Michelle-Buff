<!-- PR TARGET: https://github.com/michellebuff/Michelle-Buff | Stage 1.1 (2.5 pts) -->
# Stage 1.1 review — engagement brief · **90 / 100** (A-) · 2.25 / 2.5 pts

**Brief:** [`docs/briefs/perfect-competition-brief.md`](https://github.com/michellebuff/Michelle-Buff/blob/main/docs/briefs/perfect-competition-brief.md)

| Criterion | Earned | Notes |
|---|---|---|
| Problem restated in your own voice | 27 / 30 | Compact and accurate. You draw the line between what the farm cannot control (prices, the production characteristics) and what it can (how many beds of each crop), and you list the four things that limit the choice. It is short, but nothing in it is filler. |
| Hypothesis names a specific mix | 25 / 25 | Carrots 20, mesclun 30, tomatoes 14, laid out as three lines with a reason attached to each. Easy to check, easy to be wrong about — which is the point. |
| Economic mechanism | 24 / 25 | Two sentences that do a lot of work: "Carrot and mesclun marginal costs stay below their respective prices until their caps" and "Tomato's high selling price outweighs its steeper labor penalty through approximately 14 beds." That is the P = MC rule applied per crop, with the cap-versus-economics distinction implied correctly. What keeps it from full marks is that the tomato number is asserted rather than reasoned — you say roughly 14 without saying what about the 10% rate puts the crossing near 14 rather than near 8 or 18. |
| Falsifiability and process | 14 / 20 | The mix is precise enough to be refuted, but there is no section naming what would count as refutation. The brief is also on the short side at 146 words against the stage's "half a page to a page." Brief committed 2026-08-23 at 09:56; your spec started at 10:16. Correct order, correct path — twenty minutes is thin, but it is the right way round. |
| **Final** | **90 / 100** | earned on merit |

### What I'd fix first

- Show where 14 comes from. You do not need the model for this — you need one line of arithmetic. Tomato labor for q beds is q x 2.5 x 36 x 1.10^q hours. Work out roughly what the 14th bed costs in labor and fertilizer against the $8,800 price and see whether 14 is where the crossing lands or whether you have picked the number that fills the remaining beds. If it turns out 14 was chosen because 20 + 30 + 14 = 64, that is worth knowing before Stage 2, because it means your prediction is about the land constraint rather than about marginal cost.

- Add a "How I would know I was wrong" section. Name the outcomes: tomatoes at their 20-bed cap, tomatoes far below 14, or either of carrots and mesclun finishing short of its cap.

### Looking ahead to Stage 2

Your brief is frozen now. Your prompt log already records a hypothesis stress-test session, which is the step this stage asks for and which most of the cohort skipped — the discipline that matters next is leaving the brief alone once the model contradicts it.

Your spec is already started in capabilities/marginal-analysis/. The reasoning in this brief is what belongs in it.

---

### How to work this review

Treat this PR the way an analyst treats feedback from a senior reviewer — a review is a proposal to engage with, not a checklist to rubber-stamp.

1. **Read it yourself first.** Form your own view before you change anything. Disagreeing *with a documented reason* is a legitimate, senior response.
2. **Stress-test it with an LLM.** Paste this review and your brief into your assistant and ask it to (a) explain anything you are unsure of, and (b) argue the *other side* — where might the reviewer be wrong, and what would you give up by making each change.
3. **Then write the changes yourself.** For a brief, this matters more than usual: a hypothesis you did not generate cannot be honestly compared against your model in Stage 3, and that comparison is the entire point of writing the brief first.
4. **Close the loop.** Reply in this thread with what you changed and what you pushed back on, then commit and push.

*One standing rule for this stage: do not revise your hypothesis to match what your model later tells you. If the model contradicts the brief, that is a finding, not an error — Stage 3 asks you to explain the gap, and a brief quietly edited to be right afterwards has nothing left to explain.*

— Adam
