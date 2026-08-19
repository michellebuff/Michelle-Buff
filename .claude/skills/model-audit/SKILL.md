---
name: model-audit
description: Audit analytical models, spreadsheets, calculations, and decision analyses for formula integrity, assumptions, units, logic, and decision usefulness.
---

# Model Audit

Use this skill when reviewing or validating a quantitative model, spreadsheet, calculation, or decision analysis.

## Goal

Make the model understandable, defensible, and useful for decision-making. Do not treat a number as correct just because the spreadsheet calculated it.

## Workflow

### 1. Define the decision

Start by stating in plain English:

- What question is the model trying to answer?
- What decision will the result support?
- What output or metric matters most?

If the decision is unclear, clarify it before auditing the mechanics.

### 2. Separate inputs, assumptions, calculations, and outputs

Identify which values are:

- **Source data** — values taken from a provided or trusted source.
- **Assumptions** — values chosen because the answer is not directly known.
- **Calculations** — formulas that transform inputs and assumptions.
- **Outputs** — results used to support a conclusion or decision.

Never disguise an assumption as a fact.

### 3. Audit the mechanics

Check for:

- Hard-coded numbers where a formula or cell reference should be used.
- Incorrect cell references or broken links.
- Sign errors, especially positive versus negative cash flows or changes.
- Unit mismatches such as dollars versus thousands, percentages versus decimals, or monthly versus annual values.
- Incorrect totals, averages, growth rates, margins, or percentages.
- Formulas that do not copy consistently across rows or columns.
- Inputs that appear twice, are omitted, or are counted more than once.

Independently recalculate important results or spot-check them whenever practical.

### 4. Audit the logic

Ask whether the model behaves the way the underlying concept says it should.

- If an input increases, should the output rise, fall, or remain unchanged?
- Does the model produce sensible results at very high, very low, or zero values?
- Are short-run and long-run effects being mixed together?
- Are correlation and causation being confused?
- Are accounting identities, economic relationships, or statistical rules being applied correctly?

Flag any result that is mathematically possible but logically suspicious.

### 5. Test sensitivity

Identify the assumptions that matter most and test how the conclusion changes when they move.

When useful, test:

- A reasonable low case.
- The current or base case.
- A reasonable high case.
- Any threshold where the recommended decision changes.

Do not create false precision. If the answer depends heavily on an uncertain assumption, say so.

### 6. Explain the result in plain English

After checking the model, explain:

1. What the numbers say.
2. Why they say it.
3. Which assumptions drive the result.
4. What could change the conclusion.
5. What decision the evidence supports while keeping the final judgment with the human reviewer.

Use step-by-step explanations for unfamiliar concepts and define technical terms when needed.

### 7. Give an audit verdict

End with a short audit summary using these categories:

- **Passes:** what appears sound.
- **Issues:** errors, weak assumptions, or unsupported claims.
- **Fixes:** specific corrections needed.
- **Open questions:** information still needed before relying on the model.

## Standards

- Never invent missing values, sources, formulas, or assumptions.
- Distinguish verified facts from estimates and assumptions.
- Preserve formulas and traceability whenever possible.
- Do not replace a formula with a pasted answer merely to make the output match an expected number.
- Challenge results that do not make conceptual sense, even if the math technically works.
- If modifying a model or file, summarize exactly what changed so the human reviewer can verify it.
- The model supports the decision; it does not make the decision for the user.
