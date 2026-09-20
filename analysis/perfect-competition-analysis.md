# Perfect Competition — Stage 3 Analysis

## 1. Why tomatoes stop at 10 beds

Tomatoes remain profitable at the margin through bed 10. At bed 10, the tomato price is $8,800 (Marginal Analysis!I16) and the marginal cost is $8,248.59 (Marginal Analysis!H16), leaving a marginal contribution of $551.41. However, the marginal cost rises to $9,390.72 at bed 11 (Marginal Analysis!H17), which is greater than the $8,800 price. Therefore, the farmer stops at 10 beds because the eleventh bed would reduce profit. This can also be seen in the tomato marginal-cost chart (analysis/figures/tomato-mc-vs-price.png).

## 2. Which constraints bind and what relaxing them is worth

Carrot and mesclun bed constraints are binding because the optimized plan uses their full limits: 20 carrot beds and 30 mesclun beds (Optimization!B25:D25 and Optimization!B27:D27). The tomato, total-bed, and temporary-worker constraints are slack because the optimized plan remains below those limits. The tomato-cap, total-bed, and temporary-worker constraints are slack because the optimized plan is below their limits (Optimization!B23:D23, Optimization!B28:D28, and Optimization!B29:D29). Relaxing a constraint means increasing its maximum by one bed and rerunning Solver. When the carrot cap increased from 20 to 21 beds, optimized profit increased by $352.49. Increasing the mesclun cap from 30 to 31 beds increased profit by $246.47. Because the carrot cap has the larger shadow price, I would relax the carrot constraint first. I calculated these shadow prices by changing each cap in the workbook, rerunning Solver, and comparing the new profit to the original optimized profit of $42,761.66 (Optimization!B11).

## 3. Why tomato marginal cost dips around bed 6

<!--
Evidence to supply:
- The labor hours/rate split at beds 5-6 (Marginal Analysis!C11:D12): farmer's 720 hours
  run out around bed 5, temp labor covers bed 6 onward.
- The rate gap driving the dip: FARMER_FIELD_RATE $34.72/hr (Inputs!B11) vs. TEMP_RATE
  $17.36/hr (Inputs!B15).
- Explain, in your own words, why a cheaper marginal input taking over can make MC fall
  even though total hours are still rising.
- Reference figures/tomato-mc-vs-price.png.
- Optional: Checks!B36:B38 shows this same mechanism also fires for carrots (beds 17-18)
  and mesclun (beds 14-15) — worth noting if you want to show it's not tomato-specific.
-->

## 4. Why grow crops that appear unprofitable alone?

<!--
Evidence to supply:
- Carrots and mesclun at their optimal quantities: AVC $1,918.45 vs. naive full-fixed-cost
  ATC $2,918.45 vs. price $2,094 (carrots); AVC $2,430.74 vs. naive ATC $3,097.41 vs. price
  $2,700 (mesclun).
- Why P vs. AVC is the right comparison instead of P vs. ATC — fixed costs are sunk
  regardless of the planting decision.
- Tie to the airline half-empty-route parallel from the Stage 3 page if useful.
-->

## 5. Revisit the Stage 1 hypothesis

<!--
Evidence to supply:
- Quote the original hypothesis from docs/briefs/perfect-competition-brief.md (20 carrot /
  30 mesclun / 14 tomato beds).
- State the actual result (10/20/30) — which parts were right (carrots, mesclun exact) and
  which were wrong (tomatoes, off by 4 beds).
- Use the tomato MC data at beds 11-14 (all MC > price) to explain specifically why the
  14-bed tomato prediction failed, not just that it did.
-->
