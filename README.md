# Interactive Case Presentation Prompt

Handcrafted by: Punnawit Wasinrat<br>
Medical student, Faculty of Medicine, Chulalongkorn University, Thailand

**One prompt that turns a case and your course files into a graded, interactive case presentation.** Give an AI agent the case, your lecture handouts and your past exam papers (AC files). You get back:

- **A click-through website on GitHub Pages.** Every slide has its own QR code, so classmates scan it and answer on their phones while you present. Tapping a choice shows the answer at once.
- **A tutor view** with every answer, a line to say on each slide, and a time target per slide.
- **A hand-in PDF** of the same slides, with every answer open. The build checks the course size limit.
- **A Sources and search slide and an APA reference list** built only from sources the AI actually opened, with the PubMed queries, dates and result counts.

**→ Get the prompt: [PROMPT.md](PROMPT.md)**

**Example result:** [Case 4: Acute limb ischemia](https://punnawit9285.github.io/acute-limb-ischemia/) ([tutor view](https://punnawit9285.github.io/acute-limb-ischemia/tutor.html), [source](https://github.com/Punnawit9285/acute-limb-ischemia))

## What you need

- **An AI agent that can work on your computer:** Claude Code, Antigravity, Codex or similar. It reads your PDFs, crops figures, builds the site and pushes it. In a plain web chat you only get the slide plan and content, without a website.
- **A GitHub account** with the GitHub CLI logged in (`gh auth login`).
- **Node.js** and **Google Chrome**.

## How to use it

1. Put your files where the agent can find them, e.g. in Downloads:
   - the lecture handouts (lecture slides, lab directions, lab slides)
   - the past exam papers (AC files)
   - any answer-key images
2. Open [PROMPT.md](PROMPT.md) and fill in the block at the top:
   - the case (verbatim) and the assigned questions
   - the time per person and the deadline
   - the course rules, pasted as they are
   - a name for the new repo
3. Paste the whole file into the agent, attach the files, and send.
4. Give your name, student ID and group when it asks. They go only on the PDF cover in your Downloads folder, never into the public repo.
5. When it's done, open each source it cites and repeat one search yourself, so you can explain the method to your professor.

## What it keeps from the example

- **Talk shape:** sources and search first, then the case, then the mechanism flowchart built one box at a time, then tracing each finding back, a lab link and three take-home lines. References come last. Extra past-exam questions sit in a **More practice** section after the talk.
- **Light slides:** one idea per slide. Sources appear only on the first and last slides, and figure captions credit their source.
- **Real figures:** cropped from your course files, never AI drawings. Answer-key slides are used only to check answers and are rebuilt as boxes the audience predicts.
- **Strict sourcing:** it cites only what it opened, marks abstract-only sources, and checks every DOI. It also writes a `SOURCES.md` showing where each claim on each slide came from.
- **Language:** Thai explanations with English terms, and English questions in exam style.
