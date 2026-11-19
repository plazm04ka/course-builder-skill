---
name: course-builder
description: Builds training courses for a specific client, from brief to finished materials (code-animated videos, photo collages with voiceover and editing, PDF, Word, slides, interactive pages). Runs a step-by-step interview with forms (language/topic/goals → duration and depth → the learner and their concrete question → format → source materials), then deep critical research on the topic, a course plan, suggested fixes and a risk review. Use this skill whenever the user wants to make, design, assemble or sell a course, training program, online school, lesson, workshop, webinar series, study guide, e-learning module or curriculum for a client, even if the word "course" isn't used (for example "we need to train employees on X", "the client wants training videos", "make a 5-lesson program").
license: MIT (bundled unslop skill is CC-BY-4.0, Damir Sokolovsky)
---

# Course Builder

This skill takes a course order from the first contact to a production plan. The core idea: **a course is an answer to a specific person's specific question**. Anything that doesn't help that person get the answer is extra, even if it is "interesting" or "academically correct". So first we find out who that person is and what their question is, and only then think about content and format.

The work has five phases:

1. **Interview**: 5 questions strictly one at a time, each as a form (`AskUserQuestion`).
2. **Deep research**: critical, everything questioned.
3. **Course draft**: structure, lessons, formats, volume.
4. **Fixes and risk review**: what can be improved, where the risks are.
5. **Production**: after approval, in the chosen formats.

Reply in the user's language (not to be confused with the language of the course itself, which is asked separately).

---

## Phase 1. Interview

### How to ask

- Each question is a separate `AskUserQuestion` call. Wait for the answer before asking the next: the previous answer changes the options in the next one (for example, duration options for kids differ from those for corporate training).
- One call may combine 2–4 sub-questions if they cover one topic (question 1 works that way: language + goals). Don't mix different interview topics in one call.
- Options are concrete and fitted to what is already known, not abstract templates. The user always has an "Other" field for their own answer, so don't add an "other" option.
- If the answer is already in the user's first message, don't ask again; confirm briefly ("Topic: X, got it") and move on. Asking for known things wastes the client's time.
- If the user answers vaguely, don't push; take it as a hypothesis and mark it for checking in Phase 2.
- Before each question, one line of context: why we're asking.

### Question 1: language, topic and client goals

If the topic isn't in the first message, ask for it first in one line of plain text (a topic can't be guessed with options). Then the form:

- **Course language**: offer the likely languages plus a multilingual version, fitted to the conversation language.
- **Client goal** (multiSelect): sell the course as a product / train their own staff or customers / lead magnet / build expertise (personal brand) / certification or regulatory requirement.

The goal shapes everything else: a course product must sell with its first lesson, a corporate course must be assessable, a lead magnet must be short and lead to the next step.

### Question 2: duration and depth

- **Total volume**: mini (under 1 hour) / short (2–5 hours) / medium (6–20 hours) / large (20+ hours, modules).
- **Pace and density**: one lesson = 3–7 minute micro-learning / 15–30 minutes / long 45+ minute lectures / modules with practice breaks.
- **How much practice**: theory only / theory + exercises / mostly practice / with assessment (quizzes, final project).

Fit the options to the goal from question 1 (don't offer a large course first for a lead magnet).

### Question 3: who takes the course and what their question is

This is the most important question. A course without a concrete learner is a textbook, and nobody finishes textbooks.

- **Who the learner is** (3–4 plausible profiles derived from the topic and goal): for example, for "investing": "beginner 25–35 with no savings", "business owner with a safety cushion", "bank employee".
- **Entry level**: from zero / some basics / practitioner who wants structure / expert who needs a narrow upgrade.
- **The learner's concrete question**: phrase 3–4 options in the learner's words, as a first-person question ("How do I …, so that …?"). This becomes the course promise.

After the answer, write one sentence: **"[Who] comes with the question [which one], and after the course can [do what, concretely]"**. Show it to the user. It is the foundation; every later decision is checked against it.

### Question 4: format and materials

A multiSelect form:

- **Animated videos**: animation/motion graphics made with code (Remotion/HTML animation in Claude Code), with voiceover.
- **Photo collage + voiceover + editing**: a slideshow of images with effects, voiceover and subtitles, edited by Claude.
- **PDF course / workbook**: a laid-out document with exercises.
- **Word course (.docx)**: an editable document the client can change themselves.

If more options are needed (.pptx slides, interactive HTML page with quizzes, talking head/avatar, audio course/podcast, text lessons for a platform like Teachable), ask a second sub-question in the same form or rely on "Other". For video, ask in a second sub-question who does the voice: synthetic voice / the client's voice / no voice (captions only).

Details for each format (what can realistically be made, with what, how much effort, and the pitfalls) are in `references/formats.md`. Read it before promising a format.

### Question 5: source materials

- **Does the client have an academic/expert base**: yes, ready materials (lectures, books, guides, papers) / partly, notes and experience / no, only an understanding of the topic.

Then:
- **If yes**: ask for the files or paths. Read everything before the research: the client's materials are the main source of their voice and expertise, and the course shouldn't contradict them without a clear reason.
- **If no**: ask for a rough topic outline: "which 5–10 topics/blocks do you see in the course, even just as a list". It is raw material, not a plan. You will research based on it.

---

## Phase 2. Deep research

The goal is to understand the topic better than the client described it and to find where their picture is incomplete or wrong. The method is in `references/research.md`; read it before starting.

Key principle: **during research, everything is questioned**, including the client's wording, popular "truths" in the niche and your own first conclusions. Skepticism is a research tool, not course content: the finished course gets verified conclusions, stated confidently and clearly, without endless caveats.

In short:
- If the `deep-research` skill or WebSearch is available, use it; look for primary sources (studies, standards, official documentation), not retellings.
- For each topic in the outline, ask: is it true? is it for this audience? what's missing? what's outdated? what's disputed?
- Separate **consensus** (can be stated) from **disputed** (present as disputed or remove) and from **myths** (worth debunking if the audience believes them).
- Look for what the client didn't mention but without which the learner won't get their answer (gaps).
- Look for what the client wants to include but which doesn't answer the learner's question (ballast).

The result of this phase is a short summary for the user (not for the course): what was confirmed, what is in doubt, what to add, what to remove, key sources.

---

## Phase 3. Course draft

Build the draft with the template in `references/course-plan-template.md`. The essentials:

- The course promise (the sentence from question 3).
- Modules → lessons. Each lesson has: a goal (what the learner can do after it), key ideas, practice, format, duration.
- Order follows the learner's question, not textbook logic: the first lesson should deliver a tangible result quickly, or the learner drops out.
- The volume must match the duration from question 2; if it doesn't, say so plainly and suggest what to cut or expand.
- For video formats, estimate the number and length of videos; for documents, the approximate page count.

Show the full draft. If the user wants to share it with the client, it can be formatted as a document or page.

---

## Phase 4. Fixes and risk review

Right after the draft, without waiting to be asked, give two blocks:

**Suggested fixes**: 3–7 concrete suggestions, each with a reason: "Move lesson 4 to the start, because …", "Replace the video in module 3 with a PDF checklist: it's reference material people revisit rather than watch".

**Possible problems**: go through the checklist in `references/problems.md` and name only the risks that are real for this course, with a fix for each: volume vs. duration mismatch, vague audience, legal and YMYL risks (health, finance, law), image and music rights, video production complexity, outdated material, no way to check results, and so on.

Then ask (with a form) what to do: accept the plan / make fixes / revisit the audience or format. Repeat the cycle until the plan is approved.

---

## Phase 5. Production

Only after the plan is approved. Start with one pilot lesson in the chosen format and show it: fixing one lesson is cheaper than fixing twenty. Then scale.

Routing by format (details in `references/formats.md`):
- PDF → `pdf` skill; Word → `docx` skill; slides → `pptx` skill.
- Code animation and vertical video editing → Remotion / the `it-reelsmaker` skill if available; horizontal videos → Remotion + ffmpeg.
- Voiceover → the ElevenLabs connector (`creative_generate_speech`) if connected; otherwise prepare a script for a voice actor.
- Interactive with quizzes → HTML artifact.

### Visuals without the "AI look": unslop

Everything visual made with code (HTML pages, interactives, PDF layout via HTML, animation scenes, covers) goes through the **unslop** skill (by Damir Sokolovsky, CC BY 4.0). It finds the typical signs of generated design (purple gradients, glows, emoji labels, shouty copy, uneven spacing) and gives the course its own character drawn from the world of its topic.

- If `unslop` is in the skills list, call it via Skill. If not, read `../unslop/SKILL.md` (next to this skill in the repository) and follow it.
- On the pilot lesson: the full unslop process. Fill its Direction section from the course passport (Product = the course promise, World = the world of the topic); it becomes the design system for the whole course. Show the direction together with the pilot.
- For the remaining lessons: a short audit against `../unslop/references/signs.md` and fixes for what it finds, with no new redesign, so the course looks consistent.
- Details in section 10 of `references/formats.md`.

Each video's script is written before the visuals: voiceover text → storyboard → visuals → edit. Get the script approved by the user before spending time on rendering.
