# L01 — Introduction to Machine Learning

> *Meet Sarah Chen. It's her second week as a Customer Experience Analyst at NorthStar Retail. January 2023.*
> By the end of this lesson you will have run a machine learning model yourself, know when ML is the right tool, and understand the full workflow from a business problem to a deployed model — seen through Sarah's first real project on the job.

---

## Before you start — environment setup

> **If this is your first time with this course, do this before anything else.**
>
> Follow the [**Setup Guide →**](./setup.md) to install the Python environment. It takes 10–15 minutes. The same environment works for all 10 lessons.

---

## What you will be able to do by the end

- **Explain** what Machine Learning is and how it differs from traditional rule-based programming
- **Identify** the three main categories of ML (supervised, unsupervised, reinforcement) and give a business example of each
- **Recognise** when ML is the right tool — and when a simpler approach is better
- **Describe** the standard ML workflow: problem framing → data → model → evaluation → deployment
- **Run** a pre-built ML model end-to-end and interpret its output in business terms

---

## Monday morning at NorthStar

You are **Sarah Chen**, newly hired as a Customer Experience Analyst at **NorthStar Retail**, a mid-sized online clothing store. Early in your second week, **Aisha Patel** from Customer Service walks in with a USB drive containing 10,000 customer reviews. Your manager, **Priya Raman**, says:

> *"By Friday, I need to know which of these are positive, which are negative, and whether the negative ones are mostly about sizing, quality, or delivery. Please."*

Reading 10,000 reviews by hand would take a full work-week. Hiring a team is not on the table. Is there a faster way?

**In under 5 minutes — before you even come to class — you will answer this question with a working model.** Then, in class and after, you will understand *how* it worked and when to trust it.

---

## How class time is structured (~3 hrs)

| Phase | Time | Format |
|---|---|---|
| Concept walkthrough | ~90 min | Instructor presents core concepts; learners follow along using the interactive key-concepts page in [`interactive/`](./interactive/) |
| Hands-on code-alongs | ~90 min | Three notebooks (~25–30 min each) — Core sections only |
| (Self-study after class) | self-paced | Each notebook has a 🟡 Extension section for going deeper |

**Why this structure?** Realistic 3-hour pacing means ~1.5 hours of concepts + ~1.5 hours of coding *including Q&A and environment troubleshooting*. Each in-class notebook ends at a clearly marked 🟡 Extension boundary — anything below the line is for self-study, not class time.

---

## How this lesson works

*This lesson uses experiential learning: you try, reflect, understand, then apply.* The three parts below each use the same rhythm, so ideas arrive with increasing depth and in different business contexts. If you miss one part, you still get the core idea twice.

### Part 1 — Before class: self-study (~25 min)

**Goal:** experience the magic first. Arrive at class with a felt sense of what ML can do — and a question you want answered.

**Start here →** [**pre-class.md**](./pre-class.md)

You will:

- Open and run `01_monday_morning.ipynb` (~15 min) — Sarah's Monday, a rule-based attempt, a working ML model
- Reflect on what surprised you
- Watch a short intro video and preview the key concepts
- Try three mini-exercises with sample answers

### Part 2 — In class: instructor + hands-on notebooks (~3 hrs)

**Goal:** deepen the concepts with the instructor and build real skill.

**Interactive walkthroughs →** open [`interactive/key-concepts.html`](./interactive/key-concepts.html) for an in-browser tour of the core ideas, and [`interactive/mcqs.html`](./interactive/mcqs.html) for a 10-question self-check quiz.

**Notebooks — run in order:**

| # | Notebook | What you explore |
|---|---|---|
| 02 | [`02_what_is_ml.ipynb`](./notebooks/02_what_is_ml.ipynb) | Running a pre-trained sentiment model · what ML is · what it isn't |
| 03 | [`03_three_categories.ipynb`](./notebooks/03_three_categories.ipynb) | The 3 categories of ML · picking the right one for a business problem |
| 04 | [`04_ml_workflow.ipynb`](./notebooks/04_ml_workflow.ipynb) | The ML workflow · framing a new problem end-to-end |

Each notebook opens with a business scenario, guides you through the code with **Pause & Predict** prompts, and ends with reflection questions. Read every markdown cell, not just the code.

### Part 3 — After class: assignment (self-paced)

**Goal:** transfer what you learned to a completely new domain.

Sarah goes on secondment to NorthStar's partner **Lakeside Bank**. **Tom Bradley**, Lakeside's Head of Analytics, has a similar problem with a different kind of data. You will apply what you learned to solve it.

**Start →** [`notebooks/assignment.ipynb`](./notebooks/assignment.ipynb)

**Further reading →** [**reference.md**](./reference.md)

---

## Core vs Optional — what this lesson teaches

This is a 3-hour class, so we focus on the 2–3 topics that are most used in real-world ML projects. Other related topics are valuable but live in a separate **self-study notebook**:

**🟢 Core (taught in class):**

- The mental model of supervised / unsupervised / reinforcement learning
- Regression vs classification and their standard metrics
- Running a pre-trained ML model end-to-end

**🟡 Optional (self-study, not assessed):**

- Polynomial features, KNN deep-dive, a minimal neural network from scratch, and deeper train/test split theory live in [`notebooks/optional_extensions.ipynb`](./notebooks/optional_extensions.ipynb). These are for curious learners only — skipping them will not affect your understanding of later lessons.

This lesson is **L01 of 10** in the DSAI M3 Machine Learning & GenAI course. Later lessons build on what you do here.

---

## File map

```
README.md                    ← You are here
setup.md                     ← One-time environment setup (do this first)
pre-class.md                 ← Before-class self-study guide (75 min)
reference.md                 ← Further reading and glossary
environment.yml              ← Python environment for all 10 lessons
interactive/
  key-concepts.html          ← Interactive in-browser walkthrough of L01 key concepts
  key-concepts-ntu.html      ← NTU-branded version of the key-concepts walkthrough
  mcqs.html                  ← 10-question self-check quiz
notebooks/
  01_monday_morning.ipynb    ← Sarah's pre-class story (~15 min, before class)
  02_what_is_ml.ipynb        ← What is ML? (in class)
  03_three_categories.ipynb  ← Three categories of ML (in class)
  04_ml_workflow.ipynb       ← The full ML workflow (in class)
  assignment.ipynb           ← Lakeside Bank secondment (after class)
  optional_extensions.ipynb  ← 🟡 Optional self-study: polynomial features, KNN, mini-NN, train/test theory
```
