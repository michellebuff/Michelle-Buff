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

## 2026-09-19 — Stage 1.3 Analysis and Decision Memo

**AI tool:** Claude (Anthropic)

**Task:**  
Completed the five sections of `analysis/perfect-competition-analysis.md` and the Stage 3 decision memo in `docs/decisions/perfect-competition-memo.md`. I developed the analysis and decisions, then used Claude to help organize, verify, and commit my writing.

**AI contribution:**  
Claude checked every citation against the audited `model.xlsx` before each commit: tomato marginal cost at beds 10 and 11 against the $8,800 price, the binding and slack constraint rows on the Optimization sheet, the farmer and temporary labor rates, the labor-hour shift between beds 5 and 6, the optimized bed counts, and the $42,761.66 profit. All matched.

Claude also flagged four problems in my drafts, which I then decided how to handle:

- Section 2 contained the same sentence twice, with only the second copy carrying cell references.
- Section 2 did not reference the carrot figure and did not state that slack constraints have a $0 shadow price.
- Section 5 said labor costs "generally increase," which read as a contradiction of Section 3's finding that marginal cost falls between beds 5 and 6.
- Section 5 used a 30-minute-per-bed figure that appears nowhere in the model.

Separately, I pasted my Section 4 paragraph under the Section 3 heading and reused the previous commit message. Claude stopped before writing anything, explained the mismatch, and asked me to confirm, which kept my finished Section 3 paragraph from being overwritten.

**My verification / decisions:**  
I verified that the numbers in the analysis matched the audited workbook and confirmed that the Solver re-runs produced the reported shadow prices. I decided to keep the carrot-first recommendation because relaxing the carrot cap increased profit more than relaxing the mesclun cap. I also decided to remove unsupported wording and clarify the difference between total cost and marginal cost. I verified the cap evidence directly in the workbook by checking carrot bed 20 and mesclun bed 30 marginal costs against their prices, confirming that both caps bind while marginal cost remains below price.

**What I learned:**  
I learned that maximizing the number of beds is not the same as maximizing profit. The key decision is comparing price with marginal cost, while also recognizing that fixed costs are paid at the farm level and that labor-cost changes can affect marginal cost in unexpected ways. I also learned that careful cell verification matters because a small citation or wording error can change the meaning of the analysis.

## 2026-09-20 — BUS 620 Individual Research Paper: Topic Direction and Repository Scaffold

**AI tools:** ChatGPT (OpenAI) and Claude (Anthropic)

**Task:**  
Explored possible topics for the BUS 620 Individual Research Paper and prepared the repository scaffold for the work that follows.

**AI contribution:**  
ChatGPT helped me explore possible research topics. Claude was used only to prepare the repository scaffold: adding `scratch/` to `.gitignore`, creating `capabilities/economic-research/` with a minimal `README.md`, and adding tracked placeholder `drafts/` and `figures/` directories.

**My verification / decisions:**  
I selected China's demographic decline and the legacy of the one-child policy as my current working direction. It is a topic direction only, not yet a thesis or argument. No research brief, specification, analysis, recommendation, or paper prose was generated in this session; those remain mine to write. I reviewed the scaffold changes before they were committed.

**What I learned:**  
I learned that this prompt log is graded as part of Perfect Competition even though I used this one for my BUS Individual Research Paper.  :)

## 2026-09-21 — Stage 1.1 Review Response and Repository Cleanup

**AI tool:** Claude (Anthropic)

**Task:**  
Locate and work Professor Stauffer's Stage 1.1 review, which I had replied to in the pull request thread but never actually acted on in the repository. Revise `docs/briefs/perfect-competition-brief.md` to address the two gaps he identified, and clean up two Stage 0 standards issues in the repository.

**AI contribution:**  
Claude found the review in the open pull request "Stage 1.1 review — engagement brief" and read it alongside my brief, spec, analysis, and memo. It then independently reproduced the tomato marginal-cost schedule from the case formula `q × 2.5 × 36 × 1.10^q` and the farmer and temporary labor rates, without reading values out of the workbook, and cross-checked the result against my audited model. The independent calculation matched at every point I had previously hand-checked: $8,248.59 at bed 10, $9,390.72 at bed 11, and the dip from $7,660.86 to $4,906.28 between beds 5 and 6. It produced the figure my revision needed — a marginal cost of approximately $13,826 for the 14th tomato bed against the $8,800 price.

**What Claude flagged that changed how I did this:**  
The most useful thing Claude did was warn me about a trap I was walking into. Because Stage 3 was already finished and had returned 10 tomato beds, any edit to the brief risked reading as though I had quietly revised my prediction to match my own model. Professor Stauffer's review closes with a standing rule against exactly that. Claude proposed keeping the original hypothesis untouched and adding the new material as a dated revision section instead, so the timeline stays visible rather than hidden.

Claude also flagged that `BIO.md` should not exist. Stage 0 calls for a single bio in `README.md`, and my two versions had drifted apart, with the better-written one sitting in the file a reader never opens.

**My verification / decisions:**  
I decided to keep the 14-bed hypothesis exactly as committed on 2026-08-23. I wrote both new sections myself — the explanation of where 14 came from and the falsification criteria — rather than having Claude draft them, because a hypothesis and its refutation conditions have to be mine for the Stage 3 comparison to mean anything. I reviewed the marginal-cost figure before using it and confirmed it was consistent with the numbers already cited in my analysis. I chose to move the `BIO.md` text into `README.md` rather than the reverse, because it was the stronger draft and its AI-disclosure line was properly formatted.

**What I learned:**  
Replying to a reviewer is not the same as responding to one. I answered Professor Stauffer in the thread in August and genuinely agreed with him, but the brief itself went unchanged for a month, so from the repository's point of view nothing happened. The commit is the response.

I also learned that the timing of a revision carries information. Editing the brief after the model had already contradicted it would have destroyed the one thing that makes the Stage 1 prediction worth anything, which is that it was committed before I knew the answer. Dating the revision and leaving the wrong prediction standing costs nothing and keeps the record honest.

## 2026-09-21 — Research Paper: Testing the One-Child-Policy Framing and Policy Levers

**AI tool:** Claude (Anthropic)

**Task:**  
Stress-tested my working question about the one-child policy's role in China's demographic decline, and talked through possible policy levers.

**AI contribution:**  
Claude pointed out that most of China's neighbors (South Korea, Taiwan, Hong Kong, Japan) reached fertility as low as or lower than China's without a one-child policy. It also noted that China's fertility had already fallen sharply in the 1970s, before the policy existed. It suggested treating Korea as an imperfect comparison and asking what the policy *added* (sex ratio, speed of aging) rather than whether it *caused* the decline. It then outlined the policy levers (retirement age, hukou reform, automation, women's labor force participation, immigration) and noted that pronatalist subsidies have a poor international track record. Claude labeled all figures in this session as from memory, to be verified before use.

**My verification / decisions:**  
I recognized this subject was too broad and it was difficult to narrow down a tighter hypothesis to support the requirements and limitations given. 

**What I learned:**  
I learned building a hypothesis can be difficult. You can't just have a problem. You must have a solution or prove something will happen because of the problem. Or even show how the problem impacts. Also this is an economy paper and I recognized that my desire to do a paper about the one-child policy and how it impacted China may not have been the best topic for a 4 page econ paper as the impacts are still being felt and studied and many of the impacts effect more than the economy. 

## 2026-09-24 — Research Paper: Hukou, Choosing a Reader, and Guns vs. Butter

**AI tool:** Claude (Anthropic)

**Task:**  
Learned how China's hukou (household registration) system works. Decided who my paper is written for, chose a framing, and pulled the first real numbers.

**AI contribution:**  
Claude explained hukou: its origin, why migrants can't easily move their children, and the points-based transfer systems. It found a peer-reviewed study that used city-by-city hukou reform as a natural experiment (Dong, Liang & Zhang, 2023, *China Economic Review*), which reported migrants' childbearing rising about 11% after reform. Claude walked back one of its own earlier objections because of that evidence. It framed three possible readers (Beijing, a company, or Washington) and explained the economics behind "guns vs. butter" and how a "leverage" angle could serve as the U.S. recommendation. It pulled IMF and SIPRI figures through web search. Once I uploaded the IMF working paper (Bonthuis, Cao & Freudenberg, 2026), Claude read it and confirmed the numbers (pension spending 5.4% of GDP in 2024, 15.3% in 2050 without reform, 11.9% with the 2024 reform). It also located a free World Bank copy of *The Elderly and Old Age Support in Rural China* (Cai et al., 2012).

**My verification / decisions:**  
I made the decision to find a hypothesis that was more aligned with my current profession in federal defense. I also decided even though my paper will be about China. My audience is the U.S. Government. 

**What I learned:**  
I learned about guns vs butter. I've heard the term but I got a quick deep dive into what it means and how it impacts a nations economy. I also continued to understand how much narrower my topic needed to be.

## 2026-09-25 — Research Paper: Sources and First Hypothesis Drafts

**AI tool:** Claude (Anthropic)

**Task:**  
Drafted my first hypotheses and sourced the defense-spending ("guns") side of the comparison.

**AI contribution:**  
Claude critiqued my early drafts. They bundled several causes together and predicted a war, which my data could not test. It suggested narrowing to one cause, one measurable outcome, a timeframe, and a test that could prove me wrong. It sourced SIPRI's estimate of China's 2025 military spending ($336B, 1.7% of GDP) against China's official budget (about ¥1.78T, roughly 1.5%), and the U.S. burden (about 3.1%). It pointed out that the IMF's 15.3% pension figure is a 2050 number and a share of GDP, not of the government budget. It traced an article I found back to its primary source, the Chinese Academy of Social Sciences *Pension Fund Actuarial Report 2019–2050* (urban workers' pension savings projected to reach zero in 2035). The first link I shared turned out to be an unrelated article on Brazil. Claude also read and summarized the two PDFs I uploaded.

**My verification / decisions:**  
Since I had somewhat of a hypothesis generally put together I began to collect sources to help me determine what kind of data was out there that could be a main focus to me. 

**What I learned:**  
I learned that most of my hypothesis against the China budget had primarily been driven by their declining population and increase of pension payouts starting at 2035 through 2050. I also continued to focus on hypothesis that would either ask if China would start a war or if China could afford to start a war due to their rapidly aging population. Claude also warned me that due to my profession it could be risky to write a paper predicting a War with China. So instead of focusing on the possibility of War I thought maybe I get the war out of the way and just say it happens...now what.

## 2026-09-28 — Research Paper: Locking the Hypothesis (Stimulus and Recovery After a Taiwan Shock)

**AI tool:** Claude (Anthropic), ChatGPT (OpenAI)

**Task:**  
Worked through several hypothesis versions and settled on a recovery-speed comparison between China and the U.S. after a Taiwan-conflict shock. Found evidence for the mechanism and chose a U.S. recommendation.

**AI contribution:**  
Claude read Figure 9 of the IMF paper (page 27): pension spending is roughly flat until about 2030 and accelerates from the early 2030s. It sourced shock estimates for a Taiwan conflict: Bloomberg Economics (2024; war scenario with the U.S. drawn in: China −16.7%, U.S. −6.7%; one-year blockade: China −8.9%, U.S. −3.3%) and RAND (2016; China −25% to −35%). (Corrected 2026-10-02: the figures Claude first gave for Bloomberg, China −11% and U.S. −6.6%, did not match the article.) It confirmed that no public model covers years 2–5 of the recovery. After I uploaded it, Claude read Chen, Guo & Zhang (2025, *Economic Modelling*), which finds the output effect of monetary stimulus falls more than 30% as China ages, through a weaker investment channel. It explained that "not statistically significant" means no measurable effect, not a negative one. It explained how it compared U.S. policy options and the "what's new" objection to each.

**Where the AI was wrong, and how AI, and myself caught it:**  
Claude claimed China's past rebounds were powered by a young workforce. ChatGPT corrected it: the 2008 rebound ran on stimulus, bank lending and infrastructure, and the working-age population was already shrinking by 2012. I found supporting documentation to back it. Claude also called the 851 million figure China's "labor force". I corrected that to "working-age population (16–59)" and checked it against the National Bureau of Statistics. 

**My verification / decisions:**  
I chose the recovery comparison because it interested me more; I separated the year-one hit from the years 2–5 recovery; I chose to write for the U.S.; I ruled out supply-chain reshoring because cutting supply chains hurts long term; I chose the AI-chip export-control route

**What I learned:**  
After rethinking my approach to the hypothesis I realized the post war direction was a great way to learn about China and the U.S. economy, keep my topic close to my profession, and drill down into some numbers. I am still able to use China's aging population and declined fertility rate in my numbers by using the data to support my hypothesis

## 2026-10-02 — Research Paper: Reconciling Two Hypotheses and Reading Feedback

**AI tool:** Claude (Anthropic)

**Task:**  
Picked the work back up after a break, confirmed which hypothesis is current, and read the instructor's two unread feedback files.

**AI contribution:**  
Claude summarized the earlier sessions. It initially missed the 2026-09-28 work and coached me through a different hypothesis (defense spending held at 1.7% of GDP through 2035). Once the earlier session was re-read, Claude laid the two hypotheses side by side and recommended keeping the Sept 28 version, using the pension figures as supporting evidence. It read both review files (`review/2026-09-21` and `review/2026-09-24`). Both cover Stage 1 only. It pulled out what they imply for the research brief: commit the falsifier before the analysis, scope claims precisely, and keep logging as I go. It also drafted these log entries for my review.

**My verification / decisions:**  
I noticed the mismatch ("I thought we locked this hypothesis in"); I confirmed the Taiwan-recovery hypothesis; I decided Adam's review branches stay off main

**What I learned:**  
I can't work on this project and step away for several days. I spent about 2 hours relearning and familiarizing myself with all of the info I had already spent days scrubbing and finalizing. 

## Reflection — Perfect Competition engagement

AI assisted me with a lot of the economics in this project. It helped to simplify a lot of the complexities that are unfamiliar to me and help explain why tomatoes stop at 10 beds using P=MC, why carrots and mesclun are binding while total beds/temporary labor is slack, why tomato MC dips around bed 6, and several other economic facts within the Perfect Competition work. I had to correct AI a few times regarding my repo in GitHub, there had been work that I thought was committed to main that wasn't and I mistakenly trusted AI, but when I went back the next day I realized I had to reengage AI to commit. I also had to remind AI to reference the 1.3 instructions web page and would feed it the info multiple times to ensure nothing was missed and usually it would find one or two requirements we missed or misinterpreted. I learned that AI is incredibly powerful, to a scary degree, but it’s here and we must learn AI because AI is learning us….very, very, fast. I also learned a lot about economics, for instance my hypothesis was to fill the beds to the maximum capacity. I understood this was risky and I had no factual numbers to back this up. In my reality that would be the mistake a lot of first-time business owners make when starting up. They purchase products or provide a service that is not producing enough revenue to cover the cost of producing the product/service itself (employees, bldg space, supplies, etc.) and therefore are not able to build their profit. This project opened my eyes to marginal cost and how it can help businesses to understand their financial position and potentially look at different options to help maximize profit.
