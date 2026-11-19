# course-builder-skill

A Claude Code skill that guides building a training course for a specific client:

1. **Interview with forms, one question at a time:** language, topic and goals → duration and depth → who the learner is and their concrete question → format (code-animated videos, photo collage with voiceover and editing, PDF, Word, slides, interactive…) → existing source materials (if none, a rough topic outline).
2. **Deep critical research** on the topic, everything questioned (in the research, not in the course).
3. **Course draft** from a template.
4. **Fixes and risk review**: volume, audience, rights, YMYL, production.
5. **Production**: pilot lesson first, then scale; visuals go through **unslop**.

## Install

As a Claude Code plugin:

```bash
claude plugin marketplace add plazm04ka/course-builder-skill
claude plugin install course-builder@course-builder-skill
```

Or manually: copy `skills/course-builder` and `skills/unslop` into `~/.claude/skills/`.

## Structure

```
skills/
├── course-builder/
│   ├── SKILL.md
│   └── references/
│       ├── formats.md              # formats and how to produce them
│       ├── research.md             # critical research method
│       ├── problems.md             # risk checklist
│       └── course-plan-template.md # course plan template
└── unslop/                         # design skill, see below
```

## Credits

`skills/unslop` is the **unslop** skill created by Damir Sokolovsky ([@heydamir](https://x.com/heydamir)), original: https://github.com/heydamir/unslop. Included unchanged (except for removing `agents/openai.yaml`) under [CC BY 4.0](skills/unslop/LICENSE). It is used so that course visuals don't look AI-generated.

Everything else is MIT.
