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
