# Perfect Competition — Engagement Brief

## The Problem

The farm is deciding how to divide its limited planting capacity among tomatoes, carrots, and mesclun to earn the most profit. The farm cannot control market prices or the production characteristics given in the case. It can choose how many beds of each crop to plant, but that choice is limited by the total number of beds, crop-specific caps, labor availability, and increasing labor costs caused by diminishing returns.

## Hypothesis

- **Carrots: 20 beds** — max the cap
- **Mesclun: 30 beds** — max the cap
- **Tomatoes: 14 beds** — remaining capacity, because I predict tomato's much higher revenue still outweighs its rapidly increasing labor cost through those beds

Carrot and mesclun marginal costs stay below their respective prices until their caps.

Tomato's high selling price outweighs its steeper labor penalty through approximately 14 beds.

## Revision — 2026-09-21 (response to Stage 1.1 review, PR #2)

Added after Professor Stauffer's Stage 1.1 review. The problem statement and hypothesis above are unchanged: the 20 carrot / 30 mesclun / 14 tomato prediction stands as originally committed on 2026-08-23.

### Where the 14-bed estimate came from

The 14-bed tomato estimate came from the land constraint rather than from a tested marginal-cost calculation. After assuming carrots would be planted to their 20-bed cap and mesclun to their 30-bed cap, I had 14 of the farm's 64 beds remaining, so I assigned those beds to tomatoes. I then justified that choice by saying tomato's higher price would continue to outweigh its increasing labor cost, but I had not actually tested the marginal cost of the 14th bed. Using the case calculations, the 14th tomato bed would have a marginal cost of approximately **$13,826**, which is well above the **$8,800** market price. Before building the model, I could have calculated the expected marginal cost at or near bed 14 and compared it with price. Doing that would have shown that my 14-bed estimate was really based on remaining capacity rather than on the marginal-profit rule.

### How I would know I was wrong

I would know my original hypothesis was wrong if the optimized result placed tomatoes at their 20-bed cap, placed tomatoes substantially below my 14-bed estimate, or caused either carrots or mesclun to finish below their respective caps. Any of those outcomes would show that the economic tradeoffs were different from what I predicted before building the model. In particular, a tomato result far below 14 would indicate that rising marginal cost became binding sooner than I expected, while carrots or mesclun finishing below their caps would show that I had overestimated the profitability of maximizing those crops.
