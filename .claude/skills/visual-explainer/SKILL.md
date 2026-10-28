---
name: visual-explainer
description: >-
  Generate a beautiful, self-contained HTML page that visually explains an idea,
  process, comparison, timeline, or dataset. Use when the user wants to explain
  something visually, map a process or who-owns-what, compare options, build a
  timeline, or turn dense information into something scannable and shareable.
  Produces a single scrollable HTML page — for a multi-slide deck use the Slides
  skill; for a print-ready PDF document use PDF Create; for a static PNG/PDF art
  object use Canvas Design.
version: 1.2.0
---

# Visual Explainer

Generate a self-contained HTML file that turns an idea, process, or dataset into a visual page. The output is a single `.html` file the user can open in any browser, email, or publish.

**When to use this skill:**
- "Explain this process visually"
- "Show who owns what" / "map the stakeholders"
- "Create a comparison of these options"
- "Turn this into a visual one-pager"
- "Make a timeline of this project"
- "Help me explain this concept to my team"

## What's in this skill's folder

| File | Read it when |
|---|---|
| `references/styles.md` | Always. It has the five styles and the list of tells that make a page look AI-generated |
| `references/patterns.md` | Always. It covers the building blocks (process maps, tables, timelines, charts) and when to use each |
| `examples/process-map.html` | Building a process, workflow or approval path |
| `examples/comparison-table.html` | Comparing options, vendors or approaches, or writing up an audit |
| `examples/ownership-map.html` | Mapping responsibilities, stakeholders, or who owns what |

The examples are finished pages. **Open the matching one before you write anything** and copy its patterns, not its content.

---

## How to build one

### 1. Get the inputs, and find the answer

Pin down three things (ask if the user hasn't said):

- **Content** — the raw notes, data or document to work from.
- **Audience** — team, executives, clients, general public? A page for a CEO looks different from one for new hires.
- **Purpose** — inform, persuade, compare, or explain?

Then find **the one-sentence answer** the page exists to deliver, such as "Step 3 is where the time goes" or "Go with the hybrid option". It becomes the first thing on the page. If you can't find one, ask the user what they want the reader to take away.

### 2. Pick the page type, and open its example

| The content is… | Build a… | Start from |
|---|---|---|
| Steps in order, with owners | Swimlane process map | `examples/process-map.html` |
| Options to choose between | Comparison table, recommendation first | `examples/comparison-table.html` |
| Responsibilities or stakeholders | Ownership grid, gaps first | `examples/ownership-map.html` |
| Phases, milestones, history | Timeline | `references/patterns.md` § Timeline |
| A framework or mental model | Cards with varied weight | `references/patterns.md` § Cards |
| Metrics or status | Key-numbers strip + simple charts | `references/patterns.md` |

Pick the type that shows **the point**, not just the content. A process whose real problem is that nobody owns step 4 should be an ownership grid.

### 3. Pick a style and commit to it

Choose the style that fits, or use the one the user asks for. Take the palette, type and spacing from `references/styles.md` and apply the whole system. Don't half-apply it.

| Style | Best for | Feel |
|-------|----------|------|
| **Editorial** | Reports, proposals, thought pieces | Refined, generous whitespace, serif headings |
| **Blueprint** | Processes, technical flows, systems | Precise, technical-drawing feel, monospace labels |
| **Paper/Ink** | Friendly explanations, informal content | Warm, approachable, cream backgrounds |
| **Clean** | Data tables, comparisons, matrices | Minimal, content-forward |
| **Dashboard** | Metrics, KPIs, status overviews | Data-dense, cards and numbers |

### 4. Generate the page

One HTML file, built in this order: **answer, then the visual, then the detail** (see `references/patterns.md`).

- **Give things different weight on purpose.** The answer and the key visual dominate. Supporting detail is quieter, and reference material is smallest. A page where every section gets equal treatment looks like a template.
- **Use real structure.** Use a real `<table>` for anything in rows and columns, and word-plus-shape badges for ratings (never emoji, never colour alone).
- **Draw charts and connectors in inline SVG or CSS.** Don't use chart or diagram libraries: they load from the internet and break offline.
- **Make it work everywhere.** It should be responsive down to phone width, support dark and light mode via `prefers-color-scheme`, and print cleanly.
- **Keep it fully self-contained.** Inline all CSS, embed images as data URIs, and add no external links for fonts or scripts. It must work offline.

### 5. Check it before you hand it over

- **Squint test.** Blur your eyes. Can you still see what matters most, and where each section starts?
- **AI-tells test.** Go through the avoid-list in `references/styles.md`. Two or more tells means redo the styling, not patch it.
- **Answer test.** Could someone who reads only the top of the page say what it concludes?
- **Completeness.** Is everything the user gave you represented, and nothing invented? A pretty page that drops a point has failed.
- **Chart honesty.** If there are numbers, check that bars start at zero, lengths are proportional, there's no 3D, and every number is compared to something. Rules are in `references/patterns.md`.
- **Both themes, phone width, print.** Nothing should clip or spill out, and the dark theme should look chosen rather than broken.

### 6. Save and hand off

Save to the user's workspace and tell them the exact path. They can open it (double-click, or drag it into a browser), share it (email the file, or publish it with the Here.now skill), or edit the HTML directly.

---

## Examples of requests

- **"Explain our hiring process"** → a swimlane process map: stages across, owners down, the screening decision marked with both outcomes, and a callout on where candidates drop out.
- **"Compare these three vendors"** → a comparison table with the recommendation on top, rated criteria, a cost row, and "what would change our mind".
- **"Who's responsible for what in onboarding?"** → an ownership grid that leads with the activities nobody owns.
- **"Visualize our Q2 roadmap"** → a timeline with monthly milestones, done items muted, the current one highlighted, and dependencies noted.
- **"Turn these meeting notes into a visual summary"** → a one-pager with decisions up top, action items with owners in a table, and discussion points in quieter cards.

---

## Tips to pass on to the user

- **Be specific about what to include.** "Show the three pricing tiers with features and target customer for each" beats "visualize our product".
- **Say who's looking.** The audience changes the design.
- **Say what you want them to take away.** "The point is that step 3 is too slow" gets a far better page than "make this visual".
- **Flag format constraints.** "Make it print as a single page" or "this is for a big screen in a meeting."
- **Keep the ones you like.** Save a page you're happy with into this skill's `examples/` folder, and future pages will learn from it.

---

## Gotchas

- **Self-contained or it breaks.** Inline every stylesheet, embed images as data URIs, and use system font stacks (or `@font-face` with embedded data). A `<link>` to a CDN or Google Font makes the file fail the moment it's opened offline or emailed. The same goes for chart and diagram libraries.
- **Always include `<meta charset="utf-8">`.** Without it, em-dashes, curly quotes, and arrows render as mojibake — a common and ugly failure.
- **The default look is the enemy.** All-blue palettes, oatmeal beige, title-then-italic-subtitle, and rows of identical emoji cards all scream "AI made this". `references/styles.md` has the full avoid-list. Apply it.
- **One accent, from a real scale.** Pulling arbitrary hex values and three competing accents is what makes a page look loose. Commit to one style's palette and its type/spacing scales.
- **Match density to audience.** An exec one-pager and a team explainer are not the same page — don't ship a wall of text as a "visual" explainer.
- **Don't invent numbers to fill a chart.** If the user's material has no figures, use a table or a diagram instead. The example pages say their numbers are made up; yours can't be.

---

## Pairs well with

- **Here.now** — publish the visual to a shareable URL instantly
- **Slides** — when the user needs a multi-slide presentation instead of a single page
- **PDF Create** — convert the HTML to a print-ready PDF for formal sharing
- **Research Brief** — get the information first, then visualize it
