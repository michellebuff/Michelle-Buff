---
type: spec
capability: marginal-analysis
engagement: perfect-competition
date: 2026-08-23
status: draft
built_with: "Claude Code, from this file"
---

# Marginal Analysis — Model Specification

## Purpose

Build an Excel model that determines the most profitable mix of tomato, carrot, and mesclun beds for the farm while staying within its land, crop, and labor constraints.

The model must show how marginal cost changes as additional beds of each crop are planted, compare marginal cost with the fixed market price for each crop, and use Solver to identify the crop mix that maximizes total season profit.

## Inputs — the named contract

| Name | Value | Unit | Source |
|---|---:|---|---|
| `SEASON_WEEKS` | 36 | weeks | Case scenario |
| `FIXED_COSTS` | 20000 | USD/season | Case scenario |
| `MAX_TOTAL_BEDS` | 64 | beds | Case scenario |
| `FARMER_FIELD_HOURS` | 720 | hours/season | Case scenario |
| `FARMER_FIELD_RATE` | 34.72 | USD/hour | Case scenario |
| `MAX_TEMP_WORKERS` | 4 | workers | Case scenario |
| `TEMP_HOURS_PER_WORKER` | 1440 | hours/season | Case scenario |
| `TEMP_RATE` | 17.36 | USD/hour | Case scenario |
| `TOM_MAX_BEDS` | 20 | beds | Case scenario |
| `TOM_PRICE` | 8800 | USD/bed | Case scenario |
| `TOM_HRS` | 2.50 | hours/week/bed | Case scenario |
| `TOM_FERT` | 880 | USD/bed | Case scenario |
| `TOM_DIM` | 0.10 | decimal (10.0% per bed) | Case scenario |
| `CAR_MAX_BEDS` | 20 | beds | Case scenario |
| `CAR_PRICE` | 2094 | USD/bed | Case scenario |
| `CAR_HRS` | 0.833 | hours/week/bed | Case scenario |
| `CAR_FERT` | 440 | USD/bed | Case scenario |
| `CAR_DIM` | 0.025 | decimal (2.5% per bed) | Case scenario |
| `MES_MAX_BEDS` | 30 | beds | Case scenario |
| `MES_PRICE` | 2700 | USD/bed | Case scenario |
| `MES_HRS` | 1.25 | hours/week/bed | Case scenario |
| `MES_FERT` | 880 | USD/bed | Case scenario |
| `MES_DIM` | 0.0125 | decimal (1.25% per bed) | Case scenario |

Diminishing-return inputs are stored as decimals so that `(1 + DIM_PCT)^q` can reference the named range directly without a unit conversion step.

## Structure

The workbook should contain clearly labeled sheets or regions for:

1. **Inputs** — all named assumptions from the case.
2. **Farm P&L** — crop quantities, revenue, labor, fertilizer, fixed costs, total costs, and profit.
3. **Marginal Analysis** — standalone marginal-cost schedules for tomatoes, carrots, and mesclun.
4. **Optimization** — the three crop bed-count decision variables, Solver objective, and all constraints.
5. **Checks** — validation results and pass/fail checks for the finished model.

## Calculation Logic

### Labor

For each crop and quantity `q`:

`LABOR_HRS(q) = q × HRS_PER_BED × SEASON_WEEKS × (1 + DIM_PCT)^q`

The exponential diminishing-return term must be included. Labor must not be modeled as a simple linear function.

Total farm labor is:

`TOTAL_LABOR_HRS = TOM_LABOR_HRS + CAR_LABOR_HRS + MES_LABOR_HRS`

The farmer's own hours are used first:

`FARMER_HRS_USED = MIN(TOTAL_LABOR_HRS, FARMER_FIELD_HOURS)`

Temporary labor covers the remaining requirement:

`TEMP_LABOR_HRS = MAX(TOTAL_LABOR_HRS - FARMER_FIELD_HOURS, 0)`

Temporary workers required:

`TEMP_WORKERS_NEEDED = TEMP_LABOR_HRS / TEMP_HOURS_PER_WORKER`

Labor cost:

`FARMER_LABOR_COST = FARMER_HRS_USED × FARMER_FIELD_RATE`

`TEMP_LABOR_COST = TEMP_LABOR_HRS × TEMP_RATE`

`TOTAL_LABOR_COST = FARMER_LABOR_COST + TEMP_LABOR_COST`

For the crop P&L, labor should be allocated using the blended farm labor rate:

`BLENDED_LABOR_RATE = TOTAL_LABOR_COST / TOTAL_LABOR_HRS`

### Revenue and fertilizer

For each crop:

`CROP_REVENUE = CROP_BEDS × CROP_PRICE`

`CROP_FERT_COST = CROP_BEDS × CROP_FERT`

Total revenue and fertilizer costs are the sums across all three crops.

### Profit

`VARIABLE_COSTS = TOTAL_LABOR_COST + TOTAL_FERT_COST`

`TOTAL_COSTS = VARIABLE_COSTS + FIXED_COSTS`

`PROFIT = TOTAL_REVENUE - TOTAL_COSTS`

### Marginal cost

Create a standalone marginal-cost schedule for each crop from zero beds through that crop's maximum number of beds.

For each additional bed:

`MC(q) = VARIABLE_COST(q) - VARIABLE_COST(q - 1)`

Marginal cost should be compared with that crop's fixed market price.

Do not force marginal cost to increase with every bed. The labor and wage formulas should determine the actual shape of the marginal-cost curve.

## Conventions

- The farm is a price taker. Crop prices are fixed inputs and cannot be changed by the farm.
- The only decision variables are the number of tomato, carrot, and mesclun beds planted.
- Bed quantities must be whole numbers and cannot be negative.
- Farmer labor is always used before temporary labor.
- Temporary labor begins only after the farmer's 720 field hours are exhausted.
- Labor is allocated to crops in the P&L using the blended labor rate for the farm.
- Fixed costs are included in total profit but excluded from marginal cost because they do not change when one additional bed is planted.
- The farm may leave beds unused if planting another bed would reduce total profit.
- The model must not assume beforehand that marginal cost always rises. It must calculate the marginal-cost pattern from the specified labor function.

## Optimization

Use Excel Solver to maximize `PROFIT`.

Changing variables:

- `TOM_BEDS`
- `CAR_BEDS`
- `MES_BEDS`

Use **GRG Nonlinear** with integer decisions.

Constraints:

- `TOM_BEDS >= 0`
- `TOM_BEDS <= 20`
- `CAR_BEDS >= 0`
- `CAR_BEDS <= 20`
- `MES_BEDS >= 0`
- `MES_BEDS <= 30`
- `TOM_BEDS + CAR_BEDS + MES_BEDS <= 64`
- `TEMP_WORKERS_NEEDED <= 4`
- All three bed-count variables must be integers.

## Validation Rules

The finished workbook must pass the following checks.

### Labor formula hand-check

At `q = 1`, one tomato bed must require:

`1 × 2.5 × 36 × 1.10 = 99 hours`

If the workbook does not return 99 hours, the labor calculation fails validation.

### Farm Profit Lab cross-check

At least one intermediate marginal-cost value from the workbook must be independently compared with the Farm Profit Lab.

### Solver starting-point check

Solver must be run from both:

- `0 / 0 / 0`
- `20 / 0 / 0`

The results must be compared to determine whether Solver is reaching the same optimum from different starting points.

### Published acceptance criteria

Source: Stage 2 page published check figures.

| Check | Expected Result |
|---|---|
| Optimal crop mix | 10 tomato, 20 carrot, 30 mesclun |
| Total beds planted | 60 |
| Season profit | approximately $42,762 |
| Standalone Tomato P ≈ MC | approximately 10 beds |
| Standalone Carrot P ≈ MC | approximately 10 beds |
| Standalone Mesclun P ≈ MC | approximately 6 beds |

These values are acceptance tests. They must not be hard-coded into calculated result cells or used to force Solver to produce the expected answer.

### Structural checks

- Every calculated cell must contain a formula rather than a pasted value.
- Formulas must consistently reference the named inputs.
- There must be no `#REF!`, `#DIV/0!`, or `#NAME?` errors.
- All land, crop-cap, and labor constraint checks must pass.
- The tomato marginal-cost dip around six beds should be visible and noted for later analysis, but it should not be artificially created or explained in the model.

## Outputs

The workbook must clearly report:

- tomato beds;
- carrot beds;
- mesclun beds;
- total beds planted;
- unused beds;
- total revenue;
- total labor hours;
- farmer labor hours used;
- temporary labor hours used;
- temporary workers required;
- total labor cost;
- total fertilizer cost;
- total variable cost;
- fixed costs;
- total costs;
- total season profit;
- marginal-cost schedule for each crop;
- market price versus marginal cost for each crop;
- Solver solution;
- status of all land, crop-cap, and labor constraints;
- validation check results.

## Audit Findings

This section will be completed after the workbook is generated.

For each audit test, record:

- what was checked;
- what the check was intended to catch;
- what was found;
- what action was taken if the model failed the check.
