---
name: interactive-courseware-html
description: Convert teaching PPT/PPTX/PDF slides, lecture notes, and courseware into polished, student-facing interactive HTML lessons. Use when Codex is asked to transform educational slides or PDFs into HTML pages with preserved figures, copyable code, interactive demos, animations, quizzes, AI-labeled explanations, AI-generated extension exercises, practice links, and validation.
---

# Interactive Courseware HTML

## Workflow

1. Locate the source slides/PDF and any requested reference HTML.
2. Extract lesson content with available local tools. Preserve the teaching intent and all important source content, but reorganize for a student-facing web lesson instead of mirroring slide structure.
3. If a reference HTML is supplied, inspect its CSS and component patterns first. Reuse its visual language: background, sections, headings, code blocks, tables, tags, prompt boxes, links, and responsive behavior.
4. Preserve important figures, plots, diagrams, screenshots, comparison images, dates, labels, units, and filenames from the source material. Extract images into a sibling asset folder when needed.
5. Convert legible code screenshots into real selectable `<pre><code>` blocks. Pair copyable code with the corresponding output image when useful.
6. Build a single HTML entry file unless the user asks for multiple pages or a larger project. Use embedded CSS and JS; keep extracted assets in sibling folders.
7. Add meaningful interactions suited to the topic: simulators, animations, state transitions, quizzes, matching tasks, revealable answers, short checks, or practice prompts.
8. Add a one-click copy button to every multi-line code block.
9. Keep all visible copy learner-facing. Do not mention delivery logistics, implementation notes, or source-file internals in the page.
10. Mark AI-provided teaching content explicitly and tastefully. Use `AI 解答` for collapsed AI explanations and `AI 生成` as a small note/badge for generated extension exercises or reference answers.
11. Verify the generated page with a local browser/server when possible. Check layout, interactions, image loading, copy buttons, links, code syntax, and mobile/desktop overflow.

## Page Structure

Use the actual lesson topic to choose sections, but prefer this pattern:

- Title: lesson name plus a concise subtitle about the concepts and practice.
- Sticky navigation: anchors to major sections.
- Concept introduction: explain why the topic matters.
- Main lesson sections: teach concepts with examples, code, tables, figures, diagrams, and interactions.
- Source figures and examples: preserve useful source visuals, but label them naturally for learners.
- Classroom quiz/practice: interactive checks with scoring or feedback.
- Summary: compact recap of key distinctions.
- Extension exercise: final practice section with an AI-generation badge when created by Codex.

Do not create a marketing landing page. The first viewport should feel like a useful lesson page.

## Visual Standard

Follow `references/page-patterns.md` for the established visual style, component rules, AI badges, links, and responsive behavior.

Default style:

- Background: light gray-blue gradient.
- Content blocks: white rounded sections with soft shadows and subtle borders.
- Titles: deep navy/blue; section title has a rose accent underline.
- Code blocks: dark background with light monospace text.
- Info boxes: blue-violet for important notes, cyan for AI answers, yellow for warnings, green for summaries.
- Navigation and controls: compact, rounded, high-contrast, responsive.

## Interaction Standard

Each lesson should include at least two meaningful interactions when the source material permits:

- Concept simulator, such as set operations, slicing/indexing, function execution, loop tracing, data mutation, branch flow, or parameter tuning.
- Animated explanation, such as index highlighting, flow diagrams, state transitions, or step-by-step output.
- Quiz/check, such as matching operations to code, multiple-choice checks, fill-in prompts, or revealable answers.
- Practice link, if the user provides one. Make primary class-practice links visually prominent; make platform links capsule-style pills.

Interactions should work without external libraries unless the existing project already uses them or the user explicitly approves dependencies.

## Figure And Code Preservation

- Preserve plots, diagrams, comparison images, and historically or pedagogically important figures from the source deck.
- Extract source images to an asset folder named after the output, for example `chapter_06_assets/`.
- Do not use captions like `PPT 原图`, `original slide image`, or implementation-facing labels. Use learner-facing labels such as `运行左侧代码得到的图像`, `PNG 放大 500%`, or the figure's actual title.
- If a slide shows a code screenshot and an output figure, reconstruct the screenshot as a real copyable code block and place it beside the output figure.
- Preserve source-specific details such as dates, ranges, labels, units, smoothing windows, and filenames. Do not substitute invented values unless the user asks for a simplified demo.
- For comparison pairs, include every side of the comparison.

## AI Content Rules

- Use a collapsed information block for AI explanations after classroom questions:
  - Summary text: `AI 解答`
  - Body: direct answer and reasoning, concise enough for learners.
- Use a small note/badge for generated content:
  - Example heading: `延伸练习 <span class="title-note">AI 生成</span>`
  - Example reference answer: `参考答案 <span class="title-note">AI 生成</span>`
- Do not overclaim certainty. AI explanations should be framed as reference guidance when multiple approaches are valid.

## Practice Links

If the user supplies links:

- Put a primary class-practice link after the quiz/check section using `.resource-link`.
- Put a secondary practice-platform link in or near the extension exercise heading using `.platform-pill`.
- Use the user's exact URLs. Do not hardcode course-specific URLs into new pages unless the user provides them.

## Validation

After editing:

1. Search the HTML for teacher-facing or implementation-facing phrases such as `分享给学生`, `可直接`, `老师`, `投屏`, `请学生`, `PPT 原图`, `original slide`, and `implementation`.
2. Extract visible code blocks and parse or run syntax checks where possible. For Python, use `ast.parse` for code blocks that are intended to be valid Python. Treat syntax errors as blockers.
3. Check generated/demo code as well as static snippets. If UI controls produce library code, verify displayed parameter values are real values for that library.
4. Check that every multi-line code block has a visible copy button after page load.
5. Check that every referenced `<img>` exists and loads. In browser validation, verify `img.complete && img.naturalWidth > 0`.
6. Confirm key anchors, buttons, links, quiz controls, AI labels, extension exercises, and reference answers exist.
7. Preview with Browser if available. For `file://` limitations, start a local static server and open `http://127.0.0.1:<port>/...`.
8. Exercise representative controls and inspect page width for horizontal overflow on desktop and mobile widths.
9. Stop any local server started only for validation.

## Delivery

Return the path(s) to the generated HTML page(s), briefly summarize the interactions added, and mention validation results. Mention limitations only when something could not be verified.

