# Interactive Courseware HTML Codex Skill

Convert teaching slides, PDFs, and lecture materials into polished, student-facing interactive HTML courseware.

This repository contains a reusable Codex Skill template for educators who want to turn static courseware into readable web lessons with interactive demos, quizzes, copyable code, AI-labeled explanations, extension exercises, and browser validation.

## What This Skill Does

- Extracts and reorganizes lesson content from PPT/PPTX/PDF files.
- Preserves important source figures, diagrams, code-output examples, dates, labels, and units.
- Converts legible code screenshots into real selectable `<pre><code>` blocks.
- Adds one-click copy buttons to multi-line code examples.
- Designs interactive learning moments such as simulators, animations, quizzes, revealable answers, and practice prompts.
- Clearly labels AI-provided teaching content with `AI 解答` or `AI 生成`.
- Validates generated pages for code syntax, missing assets, broken links, copy buttons, and responsive layout.

## Repository Structure

```text
courseware-html-skill-template/
├── README.md
├── LICENSE
├── .gitignore
├── skill/
│   ├── SKILL.md
│   ├── agents/
│   │   └── openai.yaml
│   └── references/
│       └── page-patterns.md
└── examples/
    └── prompts.md
```

## Install Locally

Copy the `skill/` folder into your Codex skills directory and rename it if desired:

```bash
mkdir -p ~/.codex/skills
cp -R skill ~/.codex/skills/interactive-courseware-html
```

Then start a new Codex session. The skill should trigger when you ask Codex to convert teaching PPT/PDF material into interactive HTML courseware.

## Example Prompt

```text
Use the interactive-courseware-html skill to convert Chapter 6 lecture slides into four student-facing HTML pages.
Preserve all important slide content, convert code screenshots into copyable code blocks, add classroom quizzes,
AI-labeled explanations, extension exercises, and validate the generated pages in a browser.
```

More examples are in [examples/prompts.md](examples/prompts.md).

## Customization

Before using this in your own course, edit `skill/SKILL.md` and `skill/references/page-patterns.md`:

- Replace default colors with your course or institution style.
- Change AI labels if your class uses a different disclosure convention.
- Add your own practice-platform link pattern.
- Add language-specific validation rules. For example, parse Python snippets with `ast.parse`, or run JavaScript snippets with a local runtime.
- Add course-specific interaction ideas in the reference file.

## Publishing Notes

Do not commit private lecture slides, student data, paid textbook content, school-only links, or assets that you do not have permission to redistribute.

The skill is designed as a reusable template. Put examples in `examples/`, but keep the `skill/` folder itself concise so Codex can load it efficiently.

