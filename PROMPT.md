# Interactive case presentation prompt

Fill in the block below, paste the whole file into an AI agent that can work on your computer, and attach your files. Leave a line blank if you don't have it.

```
CASE OR TOPIC (paste the case verbatim):

ASSIGNED QUESTIONS (if the course gave any):

COURSE AND ACTIVITY (e.g. CVS I, Case 4, group case presentation):

TIME PER PERSON (minutes):

COURSE RULES (paste the instructions verbatim, Thai is fine):

DEADLINE AND HAND-IN FORMAT:

ANSWER-KEY FILES (attached images or slides to check against, never to show):

NEW REPO NAME (e.g. acute-limb-ischemia):

ANYTHING ELSE:
```

---

You are building a graded, interactive case presentation for a medical student at the Faculty of Medicine, Chulalongkorn University. You deliver three things:

1. **A click-through website on GitHub Pages.** The student projects it while talking. Every slide has its own QR code, so classmates open that same slide on their phones and answer along with them.
2. **A tutor view** for the presenter, with all the answers, a line to say on each slide, and a time target per slide.
3. **A hand-in PDF** made from the same slides.

The attached files mix **lecture handouts** (lecture slides, lab directions, lab slides) and **past exam papers**. The past papers are the "AC" MCQ recall files written by senior batches, such as `AC80`, `AC81`, `AC 75–79` and `tAChycardia 81`.

The model result is https://punnawit9285.github.io/acute-limb-ischemia/ (tutor view: `tutor.html`). Its source is https://github.com/Punnawit9285/acute-limb-ischemia, pinned at commit `b8fe16b`. Match its structure, interaction, look and rigour. Change only the content.

## Stage 0: check what you can do

This job needs an agent that works on the student's own computer: Claude Code, Antigravity, Codex or similar. Confirm each of these by running it, never by assuming:

- You can read the attached files from disk. Look in Downloads, the Desktop and the Google Drive sync folder (`~/Library/CloudStorage/GoogleDrive-*/My Drive/GoodNotes/MDCU/...`).
- `node -v` works.
- `gh auth status` shows a logged-in account.
- Chrome exists, for headless checks and the PDF. On this Mac it may be at `~/Desktop/Google Chrome.app` rather than `/Applications`.
- A PDF renderer works: Swift with PDFKit on macOS (`swiftc`), otherwise `pdftoppm`, otherwise PyMuPDF.

Never install a tool or package manager without asking. npm packages inside the project folder are fine.

If you are a plain chat with no access to the computer, say so in one line. Do Stages 1 to 3 as far as the attached files allow, deliver the slide plan, the full `slides.js`, the sources slide and the reference list, and tell the student to run this prompt in an agent to build and publish the site.

## Stage 1: read everything, sort the files

Read every attached file in full before planning. Render the pages and look at them, because extracted text drops figures, labels and printed slide numbers. Sort each file into one of these roles:

| Role | What it is | How to use it |
| --- | --- | --- |
| Lecture handout | Lecture slides, lab directions, lab slides | The main content source. Citable. Crop figures from it. |
| Past paper (AC) | Senior MCQ recall | Shows which concepts get tested. Use its questions verbatim as "Past exam" polls tagged with the AC code (`AC80`). Borrow its figures (films, waveforms, tracings). Cite it as an unpublished recall file. It is never evidence for a medical claim. |
| Answer key | A lecture slide listing the findings, a mechanism flowchart, a "Key Ans" file | Use it to decide what is correct and how the flowchart is wired. **Never reproduce it.** Rebuild it as pieces the audience predicts. |
| The case | The vignette | Use it verbatim. Never paraphrase or correct it. |

Check every past-exam answer against the lecture and against any answer key you can find. Search the student's Drive course folder for files named like `Key Ans` or `Answer Key`. If a recall's answer disagrees with the lecture, tell the student which one you used and why.

Then post a short list: each file and its role, plus anything missing. Ask only for what blocks you: the case text, the assigned questions if the rules mention them, and the name, student ID and group, which only the PDF needs.

## Stage 2: plan the talk

Use this shape. The acute limb ischemia (ALI) slide ids are in brackets.

| # | Slide | Kind | Notes |
| --- | --- | --- | --- |
| – | Cover | `title` | Not counted. QR, title, presenter blanks, website link, PDF button. |
| 1 | Sources and search | `concept` | In Thai. First slide after the cover, said before the case. See Stage 3. |
| 2 | The case: tap the findings | `tap` | The verbatim case with tappable phrases, the correct ones marked. Distractors are age, history, timing and test results. |
| 3–4 | Cause and source | `poll` | Case questions with a real figure, e.g. "Where did this embolus form?" over a chest film. A past-exam question here only if it moves the story. |
| 5–8 | Build the mechanism flowchart | `flowtap`, `flowpoll` | The centrepiece. Each slide asks one question, then reveals the next boxes. Rebuild the answer-key flowchart box by box. |
| 9 | Trace each finding back | `trace` | Tap a finding, its path through the flowchart lights up. **Always include it.** The student called it very important. |
| 10 | Lab link | `poll` | A past-exam or lab question that ties the case to a lab they did. |
| 11 | Take-home | `concept` | Three lines. |
| – | References | `end` | Not counted. APA 7, score, More practice button, Start over. |
| + | More practice | `bonus: true` | The other useful past-exam questions, concept cards with cloze tables, and a `recall` slide that rebuilds the whole flowchart. Off the talk path. |

Rules:

- **Time.** Give each talk slide `t` seconds. The total is the slot minus 5 s (5:55 for 6:00). Name the slide to skip first if the student falls behind and put that in its SAY line.
- **Light slides.** One idea per slide. A question must be quick to read aloud. An explanation has at most 3 or 4 short bullets.
- **Past exam questions.** Only those that build understanding of this case go in the talk. Unrelated ones are cut, and related but non-essential ones go to More practice.
- **Slide limits.** If the course limits slide count and meeting it would make slides dense, do not cram. Build the light talk, report the count against the limit, and let the student decide. Last time a 6-slide cut was rejected as too dense, and the student kept 11 content slides plus the sources and references slides.
- **Citations.** Name sources on the Sources slide and the References slide only. Content slides carry no per-sentence citations. Figure captions still credit their source. A small note is fine for a fact from outside the lecture, e.g. "mnemonic ทางคลินิก นอกสไลด์บรรยาย".
- **Lecture links.** When a lecture topic connects (e.g. LD1 on the lactate slide), add it with a crop of that lecture slide.
- **Comparisons.** When an exam figure shows something abnormal, put a normal one beside it (normal JVP next to the AF exam JVP).

Post the outline as a table (slide, kind, question, figure, seconds), then carry on building. The student can interrupt.

## Stage 3: research and sources (graded)

The professors grade the search itself. Unless the pasted rules say otherwise, assume the CVS I case-presentation rules:

- Every answer comes from credible, appropriate, complete and current sources: textbooks, standard textbooks, journals, articles, research or credible websites.
- One slide states how the information was obtained.
- Citations use a standard format. Use APA 7 unless the student picks another.
- Before presenting, the student states the sources and explains the search:
  - Textbook: title, author, year, edition, and the chapter
  - Journal: article, author, journal, publication date
  - Website: name, author, organisation, last update

Process:

1. **Textbook first.** Look for the student's own copies in Drive, such as *Guyton and Hall Textbook of Medical Physiology* 14th ed. (2021). Find the exact chapters with a PDF text search and record the chapter numbers. Check whether a newer edition exists. If it does and the student doesn't have it, cite the edition you read and put the newer edition's existence in a SAY line.
2. **Journals.** Search PubMed. Record the exact query string, the date you ran it and the result count. Prefer recent open-access reviews. Keep an older paper only for an original figure or mechanism, and give the reason in a SAY line.
3. **Open what you cite.** Cite only sources you actually opened and read. Mark a source read at abstract level only with `[Abstract]` in the reference list. If a source can't be opened (a guideline that returns 403, a paywall), don't cite it. Mention it in a SAY line as "not opened".
4. **Never cite from memory.** Check every author list, year, volume, pages and DOI against PubMed or Crossref. Never invent one.
5. **Course documents.** Cite lab directions, lab slides and lecture slides with the author as printed, title, document type in brackets and department. Use `(ม.ป.ป.)` or `(n.d.)` when there is no date. Cite AC files as `[Unpublished MCQ recall file]`.
6. **Sources and search slide**, in Thai:
   - A table: `สืบค้นเรื่อง` (topic) | `จากแหล่งใด` (source with chapter numbers).
   - A box with the search date, the databases, each PubMed query in `<code>` with its result count, and how sources were chosen ("เลือก review ที่เปิดอ่านได้และเทียบข้อมูลระหว่างแหล่ง").
   - The AI disclosure: "ใช้ Claude (AI) ช่วยสืบค้นและร่างสไลด์ แล้วตรวจการอ้างอิงกับต้นฉบับ". Tell the student they can reword it. Everything on this slide must be true.
7. **References slide.** APA 7. Thai sources first, then the AC files, then English sources in alphabetical order. DOIs as links.
8. **Source map.** Write `SOURCES.md`: for each slide, each claim, its source, and the exact chapter, page or slide number. The student will be asked about it.

## Stage 4: figures

- Use real figures from the course material, cropped to what matters. Render at 2–3× and crop from the render. **No AI-drawn diagrams, no SVG drawings of anatomy or waveforms.**
- Strip the student's GoodNotes handwriting: render with annotations off where possible, otherwise whiten coloured pixels.
- Every caption says what to look at and where the figure came from, e.g. `AC81 Imaging`, `Lab direction ECG, Fig. 10-1`, `Cardiac Biochemistry, slide 62`.
- Turn labelled figures into image occlusion: label boxes placed over the real image, with the key label hidden until the answer shows. The ALI chest film is the model.
- A crop of a lecture slide opens the whole slide when tapped (`data-full`).
- If the course material has no such figure, use a public-domain or CC figure from Wikimedia Commons. Put the credit and licence in the caption, the references and the README.
- Flowcharts are HTML boxes defined in `slides.js`, never images.
- JPG for films and photos, PNG for line art, sensible widths, so the PDF stays under the size limit.

## Stage 5: build the site

Start from the reference engine. Copy it into a new folder, without its history or content:

```bash
git clone https://github.com/Punnawit9285/acute-limb-ischemia.git <scratch>/ref
git -C <scratch>/ref checkout b8fe16b
# copy into the new repo folder: app.js style.css index.html tutor.html live.js config.js
#   package.json .gitignore .nojekyll tools/ vendor/
# do NOT copy: .git, img/, qr-data.js, the PDF, README.md. Write slides.js from scratch.
```

If the repo can't be reached, rebuild the same engine from the spec below.

**Replace everything specific to ALI:**

- The `window.ALI`, `ALI_BASE`, `ALI_QR`, `ALI_PRESENTER`, `ALI_LIVE` and `ALI_MODE` globals, the `ali:` localStorage prefix, the `ali-case4` BroadcastChannel and the live room. Use the new repo's slug, so two decks in one browser never share answers.
- In `app.js`:
  - the PDF filename in `DOWNLOAD`
  - the kicker, `h1` and lede in `renderTitle`
  - the hard-coded image preload list (collect it from the slides instead)
  - `toChip = e[1] === 'atp'` in `drawEdges` (use the node's `chip` flag instead)
- In `index.html` and `tutor.html`:
  - `<title>`, meta description, brand text and the address in the rail
  - the logo. The EKG fits CVS. For another system, pick a minimal topic-appropriate animated mark that never distracts and stops under `prefers-reduced-motion`.
- `config.js`: the new Pages address, empty presenter fields, empty relays.
- `tools/build-pdf.js`: the output filename and PDF title. `package.json`: name and description.
- Keep `style.css`: its tokens, its light and dark themes, and its fonts (Bai Jamjuree, IBM Plex Sans, IBM Plex Sans Thai, IBM Plex Mono). The accent colour may change per organ system.

**Slide kinds in `slides.js`.** Every slide has `id`, `kind`, `sec`, `t`, `tag`, `say`, and optionally `src` and `bonus`.

| Kind | Fields |
| --- | --- |
| `title` | none |
| `concept` | `title`, `html` (`{{text}}` makes a click-to-reveal blank) |
| `poll` | `q`, `o[]`, `a`, `why[]`, plus optional `figHtml`, `figAfter`, `layout: 'fig'` |
| `tap` | `title`, `text` (`[[phrase]]` is tappable, `[[+phrase]]` is tappable and correct), `why[]` |
| `flowtap` | `known[]`, `reveals[]`, `q`, `chips[{t, ok}]`, `why[]` |
| `flowpoll` | `known[]`, `reveals[]`, `q`, `o[]`, `a`, `why[]`, optional `afterChart` |
| `trace` | `traces[{k, t, path[], line, note}]` |
| `recall` | `title` |
| `end` | `title`, `html` |

`slides.js` exports `{slides, sections, flow}`. `sections` is a list of `{k, name}` that `sec` points into. These sections become the tabs. The flowchart is `flow: {nodes, rows, edges, order}`. Nodes have `t`, `col` (a CSS grid span), and optionally `sub`, `hot` and `chip`.

**Behaviour to keep exactly:**

- Tapping an option shows the answer and explanation at once. The audience never waits for a separate reveal step, because the slot is short.
- In tap-all tasks every tap is marked right or wrong at once, and the explanation opens when every correct phrase is found.
- Next never crosses from the talk into More practice. More practice opens from the References slide and its tab.
- Every slide has its own QR code linking to that slide, so a late scan lands on the current page. The QR sits in the side rail on the projector and as a thumbnail on phones, and `Q` enlarges it. Run `npm run qr` after any change to a slide id or the address.
- The tutor view shows all answers, the SAY line and a "by m:ss" target, and follows the deck when open in the same browser.
- Keys: `Space`, `Enter` and `PageDown` reveal the next thing or move on; `←` and `→` move between slides; `PageUp` undoes a reveal; `A`–`E` choose an option; `Q` shows the big QR; `R` resets the slide; `F` goes full screen.
- The References slide shows the score (talk slides only), the More practice button, the Download PDF button and Start over.
- On phones the rail is hidden, and slides read question, then options, then chart, then explanation.
- The cover shows:
  - the title and a one-line lede
  - presenter blanks for name, student ID and group, empty on the website
  - below them, a large clickable link labelled as an interactive website ("Interactive website: เปิดแล้วกดตอบได้เอง เฉลยขึ้นทันที")
  - the Download PDF button and two lines on how to join
- Live vote counts stay **off**. GitHub Pages is static, so leave `live.js` dormant with no relays. Never probe or enable a public relay without the student's say-so.

**Language:**

- Questions and options are in English, exam style. Past-exam questions are verbatim from the AC file.
- Explanations (`why`) are in Thai with English medical terms. Use `→` for chains and bold the key term.
- SAY lines are in English: one or two sentences to say while the slide is up.
- The Sources and search slide is in Thai.

**Technical lessons from last time:**

- Tappable phrases are inline `<span role="button" tabindex="0">`, not `<button>`, which breaks lines on phones.
- Keep class names distinct. `.bar` once collided with an option's vote bar.
- Preload figures and never lazy-load them, so reveals are instant and checks are reliable.
- Blur a control after a mouse click, so the next `Space` doesn't fire twice.
- Zooming an image-occlusion figure must clone its labels.
- Keep `#stage > .card { min-height: 100% }`, so overflow can be detected.

## Stage 6: hand-in PDF

- `npm run pdf` prints the talk slides (no More practice) at 1280×720 from `index.html?pdf=1`, with every answer open. The trace slide lists every path, because a PDF can't be tapped. The build fails if a slide is cut off or the file is over the size limit.
- Build two copies:
  1. **The student's copy**, with `PRESENTER_NAME`, `PRESENTER_ID` and `PRESENTER_GROUP` set in the environment. Save it to `~/Downloads/<Course> Case <N> - <Topic>.pdf`. Never commit it.
  2. **The public copy**, built with those three unset, so the cover has blank lines. Commit it as the Download PDF file.
- **Never write the student ID into any file that gets pushed.**
- Open the PDF and look at every page before calling it done.

## Stage 7: check before publishing

Write the checks as a puppeteer script in your scratch folder, not in the repo. Serve the site on a local port, never 8765 (Anki uses it).

- Every slide at 1280×720, 1440×780, 1280×620, 1920×1080 and a 390×844 phone: no overflow, no broken image, no console error, QR present. Look at the screenshots yourself.
- Decode every QR code (jsQR) and confirm it opens that slide's address.
- Behaviour: a tap shows the answer at once, tap-all works, Next stops at References, the tutor view follows, Start over clears everything.
- If a command is blocked by a safety check, don't work around it. Tell the student.

## Stage 8: publish

- Create a **public** repo under the student's account (`gh repo create <name> --public --source . --push`). Turn on Pages from `main` and `/`, and keep `.nojekyll`.
- Wait for the Pages build. Then run the QR, image and phone checks again against the live address.
- Write a README in the style of the ALI repo: live deck and tutor links, structure and timing, the presenting keys table, editing, building the PDF, and figure credits.
- Set the repo's About box with a description and the deck as homepage.
- Write commit messages as plain sentences. Never commit `node_modules`, the student's PDF or the student ID.

## Stage 9: report

End with:

- the live deck, tutor view and PDF paths
- the talk length, the time budget, the slide count against the course limit, and which slide to skip first
- sources: which were read in full, which only at abstract level, and which were not opened
- what the student must do:
  - open each source and repeat one search, so they can explain it
  - check the AI disclosure wording
  - test a QR code with a real phone
  - press Start over after rehearsing
  - upload the PDF before the deadline
- anything flagged: an exam key that disagrees with the lecture, an unclear figure source, anything you couldn't verify
