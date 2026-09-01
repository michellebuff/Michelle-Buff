# AI Prompt Log

This log documents meaningful uses of AI during development of this portfolio and related analytical work. Entries focus on the task, the AI's role, my review, and corrections made through human verification.

## 2026-08-18 — Portfolio Repository Setup

**AI tool:** ChatGPT (OpenAI)

**Task:**  
Used ChatGPT to help interpret the portfolio repository requirements and build the initial GitHub folder and file structure.

**AI contribution:**  
Generated the repository skeleton, explained the purpose of the required files and folders, and assisted with GitHub workflow concepts including add, commit, push, and `.gitignore`.

**My verification:**  
Reviewed the proposed structure against the professor's instructions before using it and confirmed that the repository was organized by capability rather than by course or semester.

**What I learned:**  
Git tracks files rather than empty folders, so each otherwise-empty directory requires a file such as a short `README.md`.

## 2026-08-18 — `.gitignore` Review

**AI tool:** ChatGPT (OpenAI)

**Task:**  
Asked ChatGPT to generate and refine a `.gitignore` suitable for a public portfolio containing Excel workbooks, Markdown files, CSV data, and exported images.

**AI contribution:**  
Created exclusion rules for operating-system files, Microsoft Office temporary files, editor backups, environment files, credentials, and private folders.

**My verification:**  
Compared the generated rules with the professor's provided `.gitignore` guidance and confirmed that deliverable formats such as `.xlsx`, `.md`, `.png`, and `.csv` were not excluded.

**What I learned:**  
A `.gitignore` prevents matching files from entering Git history, but it does not inspect the contents of files or determine whether information is sensitive.

## 2026-08-18 — Instructor Collaborator Verification

**AI tool:** ChatGPT (OpenAI)

**Task:**  
Asked ChatGPT to help verify whether the instructor had been added as a GitHub collaborator.

**What AI got wrong:**  
ChatGPT initially interpreted a GitHub `read` permission result as evidence that the instructor had collaborator access.

**How I caught it:**  
I questioned the result because the repository was public, meaning a user could have read access without being an explicit collaborator.

**Correction:**  
We determined that the permission result did not prove collaborator status. I checked GitHub directly and added the instructor through the repository collaborator settings.

**What I learned:**  
Tool output must be interpreted in context. A technically true result can still support the wrong conclusion if the surrounding system behavior is not considered.

## 2026-08-18 — Professional Bio and Resume

**AI tool:** ChatGPT (OpenAI)

**Task:**  
Used ChatGPT to help draft and organize `BIO.md` and `RESUME.md` from my career history.

**AI contribution:**  
Helped structure my professional experience, improve clarity, translate military and technical experience into business language, and format both documents in Markdown.

**My verification and edits:**  
Corrected employment timelines, expanded my Global Force Information Management experience, clarified my progression from Business Analyst to Product Owner and program operations support, revised descriptions of my current work, removed personally identifying contact information from the public resume, and edited the final language until it accurately reflected my experience and voice.

**Disclosure:**  
Both documents contain an AI-assistance disclosure.

## 2026-08-18 — Personal AI Collaboration Standards

**AI tool:** ChatGPT (OpenAI)

**Task:**  
Developed `AGENTS.md` to define how I want AI systems to work with me.

**AI contribution:**  
Helped organize my preferences into standards for explanation, verification, research, tone, GitHub safety, and human review.

**My decisions:**  
I specifically required AI to explain unfamiliar topics in plain language, show its logic and assumptions, challenge me when necessary, preserve my voice, use appropriate humor, and allow me to review significant repository changes before they are committed.

**Working principle:**  
**Specify → Review → Challenge → Verify → Decide**

## 2026-08-23 — Stage 1 Hypothesis Stress-Test

**AI tool:** Claude (Anthropic)

**Task:**  
Before committing the Stage 1 engagement brief for the Perfect Competition case, asked Claude to attack my planting-mix hypothesis (14 tomato beds, 20 carrot beds, 30 mesclun beds) — name implicit assumptions, unsupported claims, and check whether the hypothesis was falsifiable, without rewriting it.

**AI contribution:**  
Claude pointed out that my tomato bed count (14) was actually a leftover from maxing out carrot and mesclun beds first, rather than a number derived from tomatoes' own marginal cost against its own price. It also flagged that I hadn't stated, as an assumption, that carrot and mesclun marginal costs stay below their respective prices all the way out to their bed caps — and pushed me to tie each number to a specific economic mechanism instead of a general "feels safer/cheaper" argument.

**My verification / what I did with it:**  
Yes, I kept my "leftover" tomato logic as my stated hypothesis. I expect the marginal costs of carrots and mesclun to stay below their respective prices until they reach their caps, and I believe tomatoes' much higher selling price will outweigh their steeper labor penalty for the remaining 14 beds. I understand that the model may prove those assumptions wrong, but I think it is still a fair prediction to commit to before doing the analysis.

**What I learned:**  
I learned that marginal analysis adds specificity to a decision because it looks at whether each additional unit is still worth producing. A number can sound reasonable, like using the 14 leftover beds for tomatoes, without actually showing that the 14th tomato bed is profitable. Marginal analysis forces me to compare the benefit of each additional bed to its added cost instead of relying only on what seems reasonable.

## 2026-08-26 — Stage 2 Specification Review

**AI tool:** Claude (Anthropic)

**Task:**  
Before any workbook was built, asked Claude to review my Stage 2 model specification for ambiguity, implementation risk, and any place where a model builder would have to guess rather than follow the spec.

**AI contribution:**  
Claude reviewed and implemented four issues I brought forward for verification and correction:

- **Division-by-zero risk at zero beds.** `BLENDED_LABOR_RATE = TOTAL_LABOR_COST / TOTAL_LABOR_HRS` would return `#DIV/0!` when all three bed counts are zero. Because the audit requires running Solver from a `0 / 0 / 0` starting point, this would have failed my own structural check prohibiting error values. The formula now reads `IF(TOTAL_LABOR_HRS = 0, 0, TOTAL_LABOR_COST / TOTAL_LABOR_HRS)`.
- **Ambiguous "standalone" marginal-cost schedules.** The spec did not state what the other two crops were doing while one crop's schedule was being calculated. It now states explicitly that each standalone schedule holds the other two crop quantities at zero.
- **Blended labor rate not reported.** It was calculated but never surfaced as an output, making it hard to audit. It was added to the Outputs section.
- **Sequence risk.** Building `model.xlsx` before the spec was committed would show the workbook predating its own specification in the Git history, inverting the order Stage 2 grades. The spec-first sequence was preserved.

**My verification / decisions:**  
I read and reviewed the specification myself before approving any changes. I questioned the frontmatter date and decided to keep `2026-08-23`, because that is the date I originally began writing the spec and it accurately reflects when the work started. I questioned the divergence between the Claude working branch and `main`, and decided that only the corrected spec commits should be moved onto current `main` rather than merging the stale branch, so that no existing `main` history — including my earlier `BIO.md` revert — would be disturbed. I approved each technical clarification individually, and I withheld authorization to build the workbook until the corrected spec was committed to `main`.

**What I learned:**  
A strong specification should remove ambiguity before a model is built. Small details—such as handling a zero-value case or defining what "standalone" means—can create major errors later if they are left for the builder to interpret.

## 2026-08-31 — Stage 2 Workbook Build and Audit

**AI tool:** Claude (Anthropic)

**Task:**  
Generate `capabilities/marginal-analysis/model.xlsx` from my committed specification at `capabilities/marginal-analysis/spec.md`, then verify the result myself in desktop Excel before anything was committed.

**AI contribution:**  
Claude built the workbook from the specification — five worksheets, named ranges for every input, live formulas in every calculated cell, and the published check figures written in as acceptance criteria rather than hard-coded results. After I identified a presentation defect against the Stage 1.2 requirements, Claude added the conditional-formatting requirement to the spec, committed the spec change first, and regenerated the workbook from the revised specification.

**My verification / decisions:**  
I audited the workbook manually in desktop Excel.

- Labor hand-checks passed: tomato labor at `q = 1` returned 99 hours and at `q = 10` returned approximately 2,334.37 hours.
- Solver was run from both `0 / 0 / 0` and `20 / 0 / 0`. Both starting points reached 10 tomato, 20 carrot, and 30 mesclun beds with a season profit of approximately $42,761.66.
- Excel initially had "Ignore Integer Constraints" enabled, which produced a fractional result. The workbook's whole-number check caught it. I disabled that option and reran Solver successfully.
- I independently cross-checked the marginal cost of the 11th tomato bed using the Farm Profit Lab. Variable cost rose from $61,827 at 10 beds to $71,218 at 11 beds, giving a marginal cost of $9,391. The workbook reports $9,390.72, which matches after rounding.
- Formula spot-checks and structural checks passed.

I then updated the specification to require green/red conditional formatting on constraint-check status cells, and the workbook was regenerated from the revised spec. I rechecked the regenerated workbook manually and all acceptance criteria passed.

**What I learned:**  
I learned that selecting the correct fields and settings in Solver is critical. During the first 0/0/0 run, I did not realize there was an option to ignore integer constraints, and that caused Solver to return a fractional result. Catching that helped me better understand how important it is to review both the Solver setup and the model's validation checks.

I also learned how powerful AI can be for building complex workbooks and how much time it could save me in my own work. At the same time, this made me think more seriously about the risk of losing some cognitive reasoning and creative problem-solving skills if we rely too heavily on AI. AI can do a tremendous amount of the technical work, but we still need to understand the process well enough to question the output, verify the quality, and step in when something is wrong.

## 2026-08-31 — Stage 1.2 Reviewer Feedback and Finalization

**AI tools:** ChatGPT (OpenAI) and Claude (Anthropic)

**Task:**  
Reviewed Professor Stauffer's updated Stage 1.2 feedback, compared it against my completed specification and workbook, and closed the loop on the remaining documentation issues before final submission.

**AI contribution:**  
ChatGPT helped me interpret the review, distinguish between feedback that required a model change and feedback that only required documentation clarification, and refine my response to the professor. Claude made the final documentation-only updates to `spec.md` after I approved them.

**My verification / decisions:**  
I reviewed the professor's comments myself before making changes. I kept the completed workbook unchanged because the remaining issues did not affect the model logic. I updated the specification status and date, clarified that `TEMP_WORKERS_NEEDED` represents a fractional full-time-equivalent requirement rather than a rounded headcount. The TEMP_WORKERS_NEEDED clarification documented the fractional-FTE behavior already present in the audited workbook, so no workbook regeneration was required. Finally I documented the tomato marginal-cost dip for Stage 3 without explaining it prematurely.

I also responded to the review by documenting what I changed, where I made a different analytical decision, and what the audit caught. The final workbook remained consistent with the specification and all previously completed validation and Solver checks.

**What I learned:**  
Reviewer feedback is not just a checklist to follow. I need to understand what problem each comment is trying to solve, decide whether it affects the specification, the model, or only the documentation, and make the smallest change that keeps all three consistent. I also learned that closing the loop with a reviewer is part of the analytical process because it shows not only what changed, but why I agreed or disagreed with the feedback.
