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

## 2026-08-27 — Stage 2 Specification Review

**AI tool:** Claude (Anthropic)

**Task:**  
Before any workbook was built, asked Claude to review my Stage 2 model specification for ambiguity, implementation risk, and any place where a model builder would have to guess rather than follow the spec.

**AI contribution:**  
Claude identified four issues, which I reviewed and approved as corrections to the spec:

- **Division-by-zero risk at zero beds.** `BLENDED_LABOR_RATE = TOTAL_LABOR_COST / TOTAL_LABOR_HRS` would return `#DIV/0!` when all three bed counts are zero. Because the audit requires running Solver from a `0 / 0 / 0` starting point, this would have failed my own structural check prohibiting error values. The formula now reads `IF(TOTAL_LABOR_HRS = 0, 0, TOTAL_LABOR_COST / TOTAL_LABOR_HRS)`.
- **Ambiguous "standalone" marginal-cost schedules.** The spec did not state what the other two crops were doing while one crop's schedule was being calculated. It now states explicitly that each standalone schedule holds the other two crop quantities at zero.
- **Blended labor rate not reported.** It was calculated but never surfaced as an output, making it hard to audit. It was added to the Outputs section.
- **Sequence risk.** Claude flagged that building `model.xlsx` before the spec was committed would show the workbook predating its own specification in the Git history, inverting the order Stage 2 grades.

**My verification / decisions:**  
I read and reviewed the specification myself before approving any changes. I questioned the frontmatter date and decided to keep `2026-08-23`, because that is the date I originally began writing the spec and it accurately reflects when the work started. I questioned the divergence between the Claude working branch and `main`, and decided that only the corrected spec commits should be moved onto current `main` rather than merging the stale branch, so that no existing `main` history — including my earlier `BIO.md` revert — would be disturbed. I approved each technical clarification individually, and I withheld authorization to build the workbook until the corrected spec was committed to `main`.

**What I learned:**  
*(to be written by Michelle)*
