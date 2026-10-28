# Visual Explainer — Page Patterns

The building blocks a good explainer page is made from, and when to reach for each. Read the
section for the page type you're building. For the look (palette, type, spacing), see
`styles.md`. For a finished page to learn from, open the matching file in `examples/`.

Everything here works in one self-contained HTML file: plain HTML and CSS, with inline SVG
for anything drawn. **No diagram or chart libraries.** They load from the internet, and the
page has to work when it's emailed or opened offline.

---

## The shape of every page: answer, then evidence, then detail

Readers skim. Build the page so a ten-second glance gets the point:

1. **Headline + one-sentence answer.** The heading states the subject. The line under it (or
   a highlighted box) states the conclusion: "Move to the hybrid model", "Three activities
   have no owner", "Step 3 is where the time goes".
2. **The visual.** The flow, table, map or timeline that shows why.
3. **The detail.** Notes, caveats, "what would change our mind", sources.

If the page has no conclusion (a pure reference, like a glossary or a schedule), lead with
whatever the reader looks up most.

## Which pattern for which content

| Content | Pattern | Example file |
|---|---|---|
| Steps in order, who does what | **Swimlane process map** | `process-map.html` |
| A yes/no or low/high branch | **Decision point** inside the process map | `process-map.html` |
| Options, vendors, pros/cons, audits | **Comparison table**, recommendation first | `comparison-table.html` |
| Responsibilities, stakeholders, "who owns this" | **Ownership grid**, gaps first | `ownership-map.html` |
| Phases, milestones, history | **Timeline** (below) | — |
| A framework or mental model | **Cards with varied weight** (below) | — |
| Metrics and status | **Hero numbers + small charts** (below) | the key-numbers strip in `process-map.html` |
| An argument or essay | **Lead paragraph + cards + one pull quote** (below) | — |

When content fits two patterns, pick the one that shows the *point*. A process where the
problem is ownership is an ownership grid, not a flowchart.

---

## Patterns

### Key-numbers strip (hero numbers)
Two to four numbers the reader wants before anything else, big, each with a small label.
Every number answers "compared to what?": a range, a baseline, a before/after, or a share.
A lone "42" is decoration. See the top of `process-map.html`.

### Swimlane process map
One row per owner, one column per stage, each step in its owner's row. Arrows run between
columns. Mark decisions with a different border (dashed) and **name both outcomes in words**.
Steps that only happen on one branch get a third style (dotted). Add a short legend. On a
phone, collapse the lanes into a numbered list and show the owner as a tag on each step.
Beyond about 8 stages or 5 owners it stops being readable. Split it into an overview plus
a detailed section per phase.

### Comparison table
A real `<table>`: options as columns, criteria as rows. The header stays visible while you
scroll. Put the recommendation **above** the table. Highlight the recommended column, and
nothing else. Ratings are small badges that combine a **word, a shape and a colour**
(Strong ● / Partly ◐ / Weak ○), so they still read in greyscale or for colour-blind readers.
**Never emoji.** Right-align numbers and give them `font-variant-numeric: tabular-nums`.
Wrap wide tables in a sideways-scrolling box rather than squashing the columns.

### Ownership grid
Activities as rows, people or teams as columns, two marks only: **Owns** (filled dot) and
**Involved** (ring). Flag rows with no owner, or with two owners, **in words** in the row
itself ("No owner"), then lead the page with those gaps. Group rows by phase with quiet
subheadings.

### Timeline
A vertical line with dated markers and a card beside each. Past items muted, the current one
emphasised, future ones in normal ink. On wide screens cards can alternate sides. Keep them
all on one side if the labels are long. Minimal CSS:

```css
.timeline { position: relative; padding-left: 28px; }
.timeline::before { content: ""; position: absolute; left: 7px; top: 0; bottom: 0; width: 2px; background: var(--rule); }
.event { position: relative; margin-bottom: 24px; }
.event::before { content: ""; position: absolute; left: -26px; top: 6px; width: 12px; height: 12px;
                 border-radius: 50%; background: var(--surface); border: 2px solid var(--accent); }
.event.done { color: var(--ink-dim); }  .event.now::before { background: var(--accent); }
```

### Cards with varied weight
For frameworks, feature lists and "the five things to know". **Vary the weight on purpose.**
The most important card is bigger, or tinted, or spans two columns. Supporting cards are
plain, and reference material is smaller and quieter. A row of identical cards is the most
recognisable generated-page layout (see `styles.md`, anti-AI-tells).

### Callout
One boxed note for a warning, a key insight or "where it stalls": a coloured left border plus
a faint tint. **Use one or two per page.** If everything is called out, nothing is.

### Lead paragraph and pull quote
A slightly larger opening paragraph sets context before the visual. A pull quote lifts out
the single most important sentence: **one per page at most.**

### Section navigation (pages with 4+ sections)
Add a short row of links to each section at the top (`<a href="#costs">Costs</a>`), and
give every section an `id`. On long pages it saves the reader scrolling to find their part.

### Collapsible detail
Anything useful but secondary (methodology, sources, the full list) goes in
`<details><summary>Show the full list</summary>…</details>`. It's built in, works without
JavaScript, and keeps the main page short.

### Simple charts: inline SVG only
Draw bars and lines yourself in inline SVG. It's a few lines, and it needs no library.
See the chart in `comparison-table.html`. **The honesty rules are not optional:**

- **Bars start at zero.** A cut-off baseline makes small differences look huge.
- **Lengths are proportional.** Pick a scale (say 4px per hour) and use it for every bar.
  Leave a comment saying what it is.
- **No 3D, no bubbles for single values.** Doubling a circle's width quadruples its area:
  a 4× picture of a 2× difference.
- **Label bars directly** with their values rather than making the reader look up a scale.
- **Colour is never the only code.** Back it up with a label, position or pattern.
- **Every number answers "compared to what?"**
- **Decoration stays outside the plot.** Background textures, tints and shadows belong on the
  page, never behind or on the bars themselves.

If the data needs more than a handful of bars or one simple line, a table is usually the
better choice.

---

## Keeping the page solid

- **Nothing spills out.** Grid and flex children get `min-width: 0`. Long words and links get
  `overflow-wrap: break-word`. Tables sit in `overflow-x: auto` wrappers. Check it at phone
  width.
- **It prints.** Add a `@media print` block: drop background textures, turn off sticky
  headers, and use `break-inside: avoid` on figures and tables so they don't split across pages.
- **Both themes are deliberate.** Choose the dark palette separately in
  `@media (prefers-color-scheme: dark)`. Don't just invert the light one.
- **Motion is optional and gentle.** A soft fade-in on load at most, wrapped in
  `@media (prefers-reduced-motion: no-preference)`. Nothing pulses, glows or loops.
