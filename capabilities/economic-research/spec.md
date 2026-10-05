---
type: spec
capability: economic-research
engagement: research-paper
date: 2026-10-05
status: draft
built_with: "Claude Code, from this file"
---

# Taiwan-Shock Recovery — Model Specification

## Purpose

This model will show how the U.S. and China's GDP gap versus each country's no-war path will be impacted in post-war years 2–5, and whether the U.S. will recover faster than China, as predicted in my hypothesis (docs/briefs/research-brief.md).

The model is a scenario, not a forecast. Published estimates cover only the year-one hit (Welch et al., 2024), so years 2–5 are built from cited evidence on how stimulus and labor supply shape recovery.

## Inputs — the named contract

| Name | Value | Unit | Source |
|---|---:|---|---|
| `CONFLICT_YEAR` | 2027 | year | Scenario assumption: PLA readiness goal (LaGrone, 2021); no fixed timeline (ODNI, 2026) |
| `CHN_G_2026` … `CHN_G_2031` | 4.4, 4.0, 4.0, 3.7, 3.3, 3.3 | % real GDP growth | IMF (2026) |
| `US_G_2026` … `US_G_2031` | 2.3, 2.1, 2.1, 1.9, 1.8, 1.8 | % real GDP growth | IMF (2026) |
| `CHN_SHOCK_Y1` | −16.7 | % below baseline in year one | Welch et al. (2024), war scenario with U.S. involved |
| `US_SHOCK_Y1` | −6.7 | % below baseline in year one | Welch et al. (2024), same scenario |
| `BASE_RECOVERY_RATE` | 0 | share of remaining gap closed per year without stimulus | Wars: no recovery after a decade (Benmelech & Monteiro, 2026); banking crises: no rebound to trend (Abiad et al., 2009) |
| `STIM_PER_10PTS` | 5 | % of GDP of stimulus per 10 points of year-one loss | Assumption; tested 0–10 in Sensitivity |
| `FISCAL_EFFECT` | 1.5 | points of loss avoided per 1% of GDP of stimulus | Abiad et al. (2009) — verify against the PDF before final |
| `CHN_AGING_PENALTY` | 0.30 | decimal | Chen et al. (2025): monetary stimulus output effect 30%+ smaller in aging China |
| `US_AGING_PENALTY` | 0.38 | decimal | Basso & Rachedi (2021): U.S. aging cut the spending multiplier 38% (1980–2015) |
| `CHN_WAP_2027` / `CHN_WAP_2031` | 983.812239 / 958.656955 | million, ages 15–64 (projected) | World Bank, Population estimates and projections (2026) |
| `US_WAP_2027` / `US_WAP_2031` | 220.751816 / 221.795554 | million, ages 15–64 (projected) | World Bank, Population estimates and projections (2026) |
| `CHN_LABOR_FACTOR` | `CHN_WAP_2031` / `CHN_WAP_2027` | ratio | Derived: workforce change during the war and recovery years |
| `US_LABOR_FACTOR` | `US_WAP_2031` / `US_WAP_2027` | ratio | Derived |
| `CHN_WAP_2015` / `CHN_WAP_2025` | 988.372117 / 980.126399 | million, ages 15–64 | World Bank (WDI) — Sensitivity only |
| `US_WAP_2015` / `US_WAP_2025` | 214.000880 / 220.498172 | million, ages 15–64 | World Bank (WDI) — Sensitivity only |

Derived values are calculated from source values at full precision, never hard-coded.
Stimulus scales with the size of each country's hit so that a smaller hit does not count as faster recovery; the hypothesis requires the recovery gap to be distinct from the year-one hit.

## Channels

- **In the math:** stimulus effectiveness (aging penalties) and labor supply (working-age population trend).
- **Written argument only:** fiscal room and pensions, export controls and trade. These shape the discussion but are not given numbers.

## Structure

The workbook must contain six worksheets named exactly:

1. **Inputs** — every named input above, with units and sources.
2. **Baseline** — each country's no-war real GDP index, 2026 = 100, grown at IMF rates through 2031.
3. **Scenario** — the year-one gap in 2027, then the gap in 2028–2031 (years 2–5).
4. **Recovery** — the share of the year-one loss recovered by year 5, side by side, plus the falsifier result.
5. **Sensitivity** — recovery shares across ranges of `STIM_PER_10PTS`, `BASE_RECOVERY_RATE`, and both aging penalties, including the break-even point where the two countries tie. Must also show the result using the 2015–2025 labor factors (`WAP_2025` / `WAP_2015`) alongside the main 2027–2031 result.
6. **Checks** — hand-checks, structural checks, and pass/fail results.

## Calculation Logic

### Baseline

`BASE_2026 = 100`
`BASE_t = BASE_{t−1} × (1 + G_t / 100)` for t = 2027…2031

### Stimulus and effectiveness

`STIM = STIM_PER_10PTS × |SHOCK_Y1| / 10` (% of GDP)
`EFFECTIVENESS = (1 − AGING_PENALTY) × LABOR_FACTOR`
`RECOVERY_PTS = STIM × FISCAL_EFFECT × EFFECTIVENESS` (total points of gap closed by year 5)

### Gap path

`GAP_2027 = SHOCK_Y1`
For t = 2028…2031:
`GAP_t = MIN(0, GAP_{t−1} × (1 − BASE_RECOVERY_RATE) + RECOVERY_PTS / 4)`

Stimulus effects are spread evenly over years 2–5, and the gap cannot turn positive.

Scenario GDP: `SCEN_t = BASE_t × (1 + GAP_t / 100)`

### Recovery and falsifier

`RECOVERED_5 = 1 − GAP_2031 / GAP_2027`

**Falsifier (from the brief):** if China's `RECOVERED_5` ≥ the U.S. `RECOVERED_5`, the hypothesis is wrong. The Recovery sheet shows the rule next to a PASS/FAIL cell.

## Acceptance Criteria (Checks sheet)

1. Baseline 2031 index matches a hand calculation of compounded IMF growth for each country.
2. With both aging penalties = 0 and both labor factors = 1, the two countries recover the same share (proves the model isn't rigged).
3. With `STIM_PER_10PTS` = 0 and `BASE_RECOVERY_RATE` = 0, both `RECOVERED_5` values equal 0.
4. No gap value is positive.
5. Every input cell references the Inputs sheet; no hard-coded numbers in formulas.
6. Sensitivity reports the break-even aging penalty for China at which the two countries tie.
7. Sensitivity shows the 2015–2025 labor-factor result next to the main result.

## Known Limitations

- The aging penalties measure different things: China's is monetary stimulus (Chen et al., 2025), the U.S. one is fiscal spending (Basso & Rachedi, 2021). The Sensitivity sheet shows how the result changes if either is dropped.
- `FISCAL_EFFECT` comes from banking crises, not wars.
- Years 2–5 are a reasoned scenario; no published model covers them.

## Process Note

Before this spec was locked on 2026-10-05, draft versions of these formulas were test-run while inputs were still being chosen. Those runs showed the result is sensitive to the U.S. aging penalty and to which years define the labor factor. Two choices were then made on their merits and fixed here before the model is built:

- The U.S. aging penalty stays in, so both countries are treated the same way.
- The labor factor uses the projected 2027–2031 workforce, because recovery happens in those years. The earlier 2015–2025 version is kept as a sensitivity row rather than replaced.

The model will be built and run only from this committed version.
