# Page Patterns

## CSS Tokens

Use these tokens or close equivalents:

```css
:root {
  --ink: #1a1a2e;
  --navy: #16213e;
  --blue: #0f3460;
  --accent: #e94560;
  --violet: #5b6abf;
  --line: #e8ecf0;
  --muted: #626b78;
  --paper: #ffffff;
  --soft: #f0f4f8;
  --success: #4caf50;
  --warn: #ffa000;
  --danger: #e53935;
  --code-bg: #1e1e2e;
  --code-text: #cdd6f4;
}
```

## Layout

- Use a centered `.container` with `max-width: 1120px`.
- Use `.section` blocks: white background, 12px radius, 36px padding on desktop, 24px on mobile, soft shadow, subtle border.
- Use responsive grids with `grid-template-columns: repeat(n, minmax(0, 1fr))`.
- Add `min-width: 0` to grid children so code blocks do not force horizontal overflow.
- On small screens, collapse multi-column grids to one column.
- Use `max-width: 100%` and `overflow-x: auto` for wide tables and code blocks.

## Section Title

Deep blue title with rose underline:

```css
.section-title {
  color: var(--blue);
  padding-bottom: 12px;
  border-bottom: 2px solid var(--accent);
  display: inline-block;
}
```

## Information Boxes

- `.highlight-box`: `#eef2ff`, left border `--violet`
- `.warning-box`: `#fff8e1`, left border `--warn`
- `.success-box`: `#e8f5e9`, left border `--success`
- `.error-box`: `#fce4ec`, left border `--danger`
- `.ai-answer`: `#d1ecf1`, left border `#0c5460`, normally used on `<details>`

## AI Badge

Use for inline `AI 生成` notes:

```css
.title-note {
  display: inline-flex;
  align-items: center;
  margin-left: 10px;
  padding: 3px 9px;
  border-radius: 999px;
  background: #d1ecf1;
  color: #0c5460;
  font-size: 0.72rem;
  font-weight: 600;
  vertical-align: middle;
  border: 1px solid #b9dfe6;
}
```

## Links

Use a prominent resource link after a quiz/check:

```css
.resource-link {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  min-height: 42px;
  margin-top: 14px;
  padding: 10px 18px;
  border-radius: 8px;
  background: var(--accent);
  color: #fff;
  font-weight: 700;
  text-decoration: none;
  box-shadow: 0 8px 18px rgba(233, 69, 96, 0.22);
}
```

Use a capsule-style platform link near extension exercises:

```css
.platform-pill {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  margin-left: 10px;
  padding: 5px 12px;
  border-radius: 999px;
  background: #eef2ff;
  color: var(--blue);
  border: 1px solid #c9d2ff;
  font-size: 0.84rem;
  font-weight: 700;
  text-decoration: none;
}
```

## Figure Card

Use for scientific figures and teaching images extracted from the source. Do not call these `PPT 原图` or `original slide image` in visible text.

```css
.source-figure {
  margin: 14px 0;
  background: #fbfcfe;
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  padding: 12px;
}
.source-figure img {
  display: block;
  width: 100%;
  height: auto;
  border-radius: 6px;
  background: #fff;
}
.source-figure figcaption {
  margin-top: 8px;
  color: var(--muted);
  font-size: 0.86rem;
  line-height: 1.5;
}
```

## Copyable Code Blocks

Every multi-line `<pre><code>` block should get a copy icon button in the top-right corner. Attach buttons after page load so static HTML stays readable.

```css
pre {
  position: relative;
  max-width: 100%;
  overflow-x: auto;
}
pre.has-copy { padding-top: 44px; }
pre code { display: block; }
.copy-code {
  position: absolute;
  top: 10px;
  right: 10px;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 30px;
  height: 30px;
  padding: 0;
  border-radius: 8px;
  border: 1px solid rgba(205, 214, 244, 0.22);
  background: rgba(255, 255, 255, 0.08);
  color: #cdd6f4;
}
```

Core JS pattern:

```js
function setupCodeCopyButtons() {
  document.querySelectorAll("pre").forEach((pre) => {
    const code = pre.querySelector("code");
    if (!code || pre.querySelector(".copy-code")) return;
    pre.classList.add("has-copy");
    const button = document.createElement("button");
    button.type = "button";
    button.className = "copy-code";
    button.title = "复制代码";
    button.setAttribute("aria-label", "复制代码");
    button.innerHTML = "copy icon svg";
    button.addEventListener("click", async () => {
      const text = code.innerText;
      if (navigator.clipboard && window.isSecureContext) {
        await navigator.clipboard.writeText(text);
      } else {
        const textarea = document.createElement("textarea");
        textarea.value = text;
        textarea.setAttribute("readonly", "");
        textarea.style.position = "fixed";
        textarea.style.left = "-9999px";
        document.body.appendChild(textarea);
        textarea.select();
        document.execCommand("copy");
        textarea.remove();
      }
      button.title = "已复制";
    });
    pre.appendChild(button);
  });
}
```

## Code And Output Examples

When the source has code plus a resulting figure, prefer a two-column layout:

- Left: real selectable `<pre><code>` block reconstructed from the source.
- Right: output image in `.source-figure`.
- Caption: describe the relationship, such as `运行左侧代码得到的时间序列图`.

For image comparisons, show all sides explicitly. Example: `PNG 放大 500%` and `PDF 放大 1600%` should be side by side, not collapsed into one partial image.

## Copy Rules

- Address learners directly through actions: `动手写代码`, `观察结果`, `提交答案`.
- Avoid teacher-facing or production wording: `可直接分享给学生`, `适合课堂投屏`, `请学生`, `PPT 原图`.
- Use `课堂提问` for conceptual prompts.
- Use collapsed AI answers so answers are not revealed too early.

## Interaction Ideas

- Basic data types: type guessing cards, expression evaluator, conversion pitfalls.
- Conditionals: branch-flow animation, predict-output quiz.
- Loops: step counter, loop trace table, break/continue visualizer.
- Functions: parameter binding animation, return-value tracer.
- Data structures: set operation lab, list mutation console, indexing/slicing visualizer, dictionary lookup map.
- Files/data formats: read/write flow diagram, delimiter parsing demo, schema preview.
- Scientific computing: array shape visualizer, table filtering, dimension selector, code-and-plot comparison.
- Humanities/social science: timeline explorer, source comparison, term-frequency demo.
- Math/statistics: parameter sliders, formula-to-graph visualization, worked-example reveal.

