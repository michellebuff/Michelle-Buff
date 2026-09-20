# Perfect Competition — Stage 3 Analysis

## 1. Why tomatoes stop at 10 beds

Tomatoes remain profitable at the margin through bed 10. At bed 10, the tomato price is $8,800 (Marginal Analysis!I16) and the marginal cost is $8,248.59 (Marginal Analysis!H16), leaving a marginal contribution of $551.41. However, the marginal cost rises to $9,390.72 at bed 11 (Marginal Analysis!H17), which is greater than the $8,800 price. Therefore, the farmer stops at 10 beds because the eleventh bed would reduce profit. This can also be seen in the tomato marginal-cost chart (analysis/figures/tomato-mc-vs-price.png).

## 2. Which constraints bind and what relaxing them is worth

Carrot and mesclun bed constraints are binding because the optimized plan uses their full limits: 20 carrot beds and 30 mesclun beds (Optimization!B25:D25 and Optimization!B27:D27). The tomato-cap, total-bed, and temporary-worker constraints are slack because the optimized plan is below their limits (Optimization!B23:D23, Optimization!B28:D28, and Optimization!B29:D29). Because these constraints are slack, relaxing them would not increase profit under the current plan, so their shadow prices are $0. Relaxing a constraint means increasing its maximum by one bed and rerunning Solver. When the carrot cap increased from 20 to 21 beds, optimized profit increased by $352.49. Increasing the mesclun cap from 30 to 31 beds increased profit by $246.47. Because the carrot cap has the larger shadow price, I would relax the carrot constraint first. The carrot marginal-cost chart (`analysis/figures/carrot-mc-vs-price.png`) supports this conclusion by showing that the carrot cap binds while marginal cost remains below price at the cap. I calculated these shadow prices by changing each cap in the workbook, rerunning Solver, and comparing the new profit to the original optimized profit of $42,761.66 (Optimization!B11).

## 3. Why tomato marginal cost dips around bed 6

Tomato marginal cost dips around bed 6 because the farmer’s more expensive labor reaches its available limit at $34.72 per hour (Inputs!B11), and cheaper temporary labor begins covering the additional labor needed at $17.36 per hour (Inputs!B15). The labor-hour shift can be seen in Marginal Analysis!C11:D12. This causes marginal cost to fall from $7,660.86 at bed 5 (Marginal Analysis!H11) to $4,906.28 at bed 6 (Marginal Analysis!H12). This relationship can also be seen in the tomato marginal-cost chart (analysis/figures/tomato-mc-vs-price.png).

## 4. Why grow crops that appear unprofitable alone?

Carrots and mesclun may appear unprofitable when the entire farm fixed cost of $20,000 is assigned to each crop separately. However, the short-run decision should compare price with average variable cost. At the selected quantities, carrot price is $2,094 compared with AVC of $1,918.45, while mesclun price is $2,700 compared with AVC of $2,430.74. (Marginal Analysis! Variable-cost columns) Because the price exceeds AVC for both crops, each additional bed covers its variable production cost and contributes toward the farm’s unavoidable fixed cost. Therefore, the optimizer grows both crops to their allowed limits even though assigning the full fixed cost to each crop makes their individual ATC appear higher than price.

## 5. Revisit the Stage 1 hypothesis

My original hypothesis predicted 20 carrot beds, 30 mesclun beds, and 14 tomato beds (docs/briefs/perfect-competition-brief.md). The optimized result was 20 carrot beds, 30 mesclun beds, and 10 tomato beds (Optimization!B6:B8). I correctly predicted the carrot and mesclun caps, but I overestimated tomato production by four beds. The error came from assuming tomatoes’ high price justified continuing production without comparing each bed’s marginal cost with its price. At bed 11, tomato marginal cost was $9,390.72 (Marginal Analysis!H17) compared with a price of $8,800, and the later beds remained above price. The model showed me that maximizing the number of beds is not the same as maximizing profit.

I understand that total labor costs generally increase as the number of beds increases because tending more beds requires more labor, time, and physical effort. However, marginal cost does not always increase smoothly. In Section 3, tomato marginal cost falls between beds 5 and 6 because cheaper temporary labor begins covering the additional work. This distinction helped me understand that total costs can rise while the cost of producing one additional bed can temporarily fall. In this model, time and labor are money.
