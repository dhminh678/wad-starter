# IA#2 - Dynamic HTML: make the catalogue work.
## Rubric

**CSC13008 individual assignment** • **5% of the course** • **100 points**

Part B of session 4, finished at home. Start from your own session 4 folder — the starter with Part A done (Session 4 self-check: $8/8$ passed). The tasks B1–B4 and the **Done means** table are in the starter's `README.md`; the `TODO` comments in `app.js` are the specification.

Use your assistant. Nothing in this assignment asks you to type code yourself: it scores what the page does, what you told the assistant, and how you checked what it wrote.

---

### What is scored

| # | Criterion | Points |
|---|---|---|
| 1 | The page behaves as specified (B1–B4) | 45 |
| 2 | Scope: only `index.html` and `app.js` changed | 10 |
| 3 | The brief | 15 |
| 4 | `AI-LOG.md` | 20 |
| 5 | Commit history | 10 |

---

### 1. Behaviour (45 points)

Marked by running your page through the **Done means** table in a browser script — clicking, typing and pressing keys — not by reading the code.

| Points | What it looks like |
|---|---|
| **40–45** | Every row of *Done means* holds: *Add* counts with one listener on the list, *Load more* then *Add* on Belt counts, the sold-out *Add* does nothing, `scarf` and `SCARF` both find one card, `<img src=x onerror=alert(1)>` is shown literally and runs nothing, *Enter* does not reload, no red errors. B4 shows the right total, Belt included. |
| **30–39** | B1, B2 and B3 all hold; B4 is missing or the total is wrong. |
| **15–29** | One of B1–B3 fails. The usual three: one listener per button (*Load more* breaks it), user text inserted with `innerHTML`, the form still reloads the page. |
| **0–14** | Two or more of B1–B3 fail, or the page throws an error on load. |

---

### 2. Scope (10 points)

Your first commit is the untouched starter, so `git diff --stat <first commit>` shows exactly what changed.

| Points | What it looks like |
|---|---|
| **10** | Only `index.html` and `app.js` differ from the starter. |
| **5** | `style.css` and `check.js` are untouched, but other starter files were changed or deleted. |
| **0** | `style.css` or `check.js` was edited — the quickest way for an assistant to reach $8/8$ is to change the check. Or there is no starter commit to compare with. |

---

### 3. The brief (15 points)

Hand in `brief.md`: what you actually gave the assistant, not a summary written afterwards. Several prompts are fine — paste them in order.

| Points | What it looks like |
|---|---|
| **13–15** | States the constraints an assistant breaks when nobody says them: keep every `id` and `class`, do not edit `style.css` or `check.js`, one click listener on the list, user text in with `textContent`, no page reload. Says how done is checked (the table). A stranger could give it and get your result. |
| **8–12** | Describes the task; one or two of those constraints left out. |
| **3–7** | One line: "make the TODOS work". |
| **0–2** | No brief. |

---

### 4. AI-LOG.md (20 points)

One entry per part you gave the assistant (at least B1, B2, B3). The lines we read first are **Changed** and **Rejected**.

| Points | What it looks like |
|---|---|
| **17–20** | Each entry names the tool and the request, and at least one entry records something the assistant got wrong, which row of the table caught it, and what you told it — e.g. "Load more then Add on Belt did nothing; asked for one listener on the list". Specific enough to find in the commits. |
| **10–16** | Honest, with tool and request, but Changed/Rejected say "none" everywhere or stay vague ("fixed some bugs"). |
| **3–9** | One entry for the whole assignment, or clearly written after the fact. |
| **0–2** | Missing, or contradicted by the code or the history. |

> *"Nothing went wrong"* is an acceptable entry if it says which rows you ran.

---

### 5. Commit history (10 points)

| Points | What it looks like |
|---|---|
| **9–10** | The starter commit first, then at least one commit per part (A, B1, B2, B3, B4 if done), each message saying what changed. The log can be checked against the diff. |
| **5–8** | A starter commit and two or three commits that mix several parts. |
| **0–4** | One commit with everything, or no git history in the zip. |

---

## How to submit

Zip your session 4 folder including its hidden `.git` folder, plus `brief.md`, `AI-LOG.md` and `SELF_ASSESSMENT_REPORT.md` at the top level. Name the zip after your student ID and the total you give yourself:

* `<StudentID>_<total>.zip`, for example `24120001_82.zip`

The zip must contain `SELF_ASSESSMENT_REPORT.md`: one row per criterion in this rubric, the marks you claim, and evidence pointing at a file, a row of the **Done means** table, or a commit plus a short *what I did not manage*. The total in that table is the number in the file name. Template in Course documents on Classroom.

A wrong file name costs no marks but delays your result — the grading script matches submissions to the class list by that name.

Turn in from your `<StudentID>@student.hcmus.edu.vn` Google account.

---

## Honesty adjustment

Your self-assessment is compared with the mark you actually earn. The gap is your total minus the mark, on the same 100-point scale.

| Gap | Adjustment |
|---|---|
| **within $\pm 10$** | this is normal calibration — **none** |
| **+11 to +20** | **-3** |
| **+21 to +30** | **-6** |
| **more than +30** | **-10** |
| **-21 or worse** | read the rubric before you score yourself down — **-3** |
| **no SELF_ASSESSMENT_REPORT.md** | **-10**, and the file-name total is ignored |

* A criterion you claim with no evidence line counts as claimed-and-not-done for this comparison.
* The adjustment never takes a submission below 0.

---

## Notes

* Run the whole **Done means** table yourself before you score criterion 1. The marking script runs the same rows.
* Keep every `id` and `class` from the starter: the marking script finds the page's elements by them, exactly as `check.js` does.
* You may be asked to explain any line in class — including lines your assistant wrote. Explaining what a line does and how you checked it is enough; nobody will ask you to write it from memory.