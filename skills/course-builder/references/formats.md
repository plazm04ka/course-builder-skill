# Course formats: what can be made and how

Read this before promising a format to the client. For each one: when it fits, how it is made, effort, and pitfalls.

## Contents
1. Animated videos (code animation)
2. Photo collage + voiceover + editing
3. PDF course / workbook
4. Word course (.docx)
5. Slides (.pptx)
6. Interactive HTML page
7. Audio course
8. Avatar / talking head
9. Choosing a format per lesson
10. Visual quality (unslop)

---

## 1. Animated videos (code animation in Claude Code)

**Fits:** explaining processes, diagrams, cause and effect, abstract concepts; intro lessons; course products where packaging matters.

**How it is made:**
1. Script: voiceover text split into scenes (1 scene ≈ 1 idea, 5–15 seconds).
2. Voiceover: ElevenLabs (`creative_generate_speech`) or the client's own voice. The voiceover sets the timing, so record it before animating.
3. Animation: Remotion (React components → mp4) or HTML/CSS/SVG animation recorded to video. Style is motion graphics: shapes, icons, text, charts, simple geometric characters.
4. Word-level subtitles from the voiceover transcript.
5. Music: licensed only, or generated with commercial rights.
6. Render: 1920×1080 for the course, 1080×1920 for vertical teasers.

**Effort:** high. For a 20-video course, budget time for a pilot and for templating (shared scene components, one set of colors and fonts).

**Pitfalls:**
- "Cartoons" in the sense of studio character animation cannot be made with code at an acceptable level. Tell the client honestly that the result will be motion graphics / infographics, and show it on the pilot.
- Needs Node.js, Remotion and ffmpeg. Check the environment before promising.
- Edits to animation cost more than edits to text, so get the script approved first.
- Animation frames are also an interface: run the scene style through unslop (section 10), or the videos will look "generated" (purple gradients, glows, emoji).

## 2. Photo collage + voiceover + editing

**Fits:** stories, case studies, historical topics, overviews; when video has to be quick and cheap.

**How it is made:**
1. Voiceover script → shot list (what is on screen for each line).
2. Images: client's photos / licensed stock / generated (disclosed where trust matters).
3. Edit in ffmpeg or Remotion: Ken Burns effect (slow zoom/pan), transitions, titles, captions with key points.
4. Voiceover, subtitles, music bed, loudness mix (around −14 LUFS for online; check the course platform's requirements).

**Effort:** medium.

**Pitfalls:** image rights (no images from search results without a license); monotony in long videos, so mix in diagrams and text cards.

## 3. PDF course / workbook

**Fits:** reference material, checklists, exercises, anything people come back to; companion to videos.

**How it is made:** the `pdf` skill (or HTML → PDF; in that case run the HTML layout through unslop). Structure: cover, contents, lessons with goals, exercises with space for answers, final check, sources.

**Effort:** low–medium. **Pitfalls:** PDFs are hard to edit. If the client will update the material, suggest Word.

## 4. Word course (.docx)

**Fits:** the client wants to edit, adapt and hand it to instructional designers; corporate procedures.

**How it is made:** the `docx` skill. Heading styles (for an automatic table of contents), one lesson template, comments for the client wherever their expertise is needed.

**Effort:** low. **Pitfalls:** layout is simpler than PDF, so don't promise magazine design.

## 5. Slides (.pptx)

**Fits:** the client will teach live sessions or webinars; a base for screen recordings.

**How it is made:** the `pptx` skill. One slide, one idea; speaker notes with the full text.

## 6. Interactive HTML page

**Fits:** quizzes, drills, calculators, clickable diagrams; self-assessment.

**How it is made:** an HTML artifact (questions, instant feedback, progress), then an unslop pass. If learner results must be collected, use the artifact database or an external LMS.

## 7. Audio course

**Fits:** learning on the go; topics without visuals (thinking, communication, languages).

**How it is made:** a script written for the ear (short sentences, key ideas repeated), voiceover, mix, one mp3 per lesson.

## 8. Avatar / talking head

AI avatars (HeyGen, Synthesia) only with the consent of the person whose face/voice is used, and with disclosure. For filming the client, prepare a teleprompter script and shot plan; edit with the `it-reelsmaker` skill or ffmpeg.

## 9. Choosing a format per lesson

Pick the format for the lesson's job, not one format for the whole course:

| Lesson job | Best format |
|---|---|
| Explain a process or abstraction | animation |
| Tell a story or case | photo collage with voiceover, talking head |
| Give reference material people return to | PDF / checklist |
| Practice a skill | exercise + interactive quiz |
| Material will change often | Word / text on the platform |

A mixed course (video explanation + PDF summary + quiz) is almost always better than a single-format one. Suggest that combination if the client picked one format, but don't insist.

## 10. Visual quality (unslop)

Any course visual made with code (HTML pages, interactives, PDF layout via HTML, Remotion scenes, lesson covers) looks "AI-made" by default. The `unslop` skill (in this repository: `skills/unslop/`, by Damir Sokolovsky, CC BY 4.0) fixes that.

How to use it in a course:
- **Set the direction once for the whole course**, following the Direction section of `unslop/SKILL.md`: Product = the course and its promise; Character; World = the world of the course topic (a gardening course: soil, paper, green; a cybersecurity course: terminal, night shift). This direction becomes the course design system: colors, fonts, icon and scene style. Get it approved together with the pilot lesson.
- **Pilot lesson:** run the full unslop process (audit against `references/signs.md` → passes). Then reuse the resulting tokens as the template for the other lessons.
- **Every later piece:** a short check against `references/signs.md` (polish mode), not a full redesign.
- If `unslop` is installed as a plugin, call it via Skill; if not, read `skills/unslop/SKILL.md` from this repository directly.
- Keep unslop's attribution in any copy or adaptation (a condition of the CC BY 4.0 license).
