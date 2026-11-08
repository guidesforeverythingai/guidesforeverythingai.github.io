# Guides for Everything: Style Guide

How every manual in the series should look, read, and be built. Follow this so a new volume sits on the shelf as part of the same family.

The design lives in three places. Change them only for a deliberate, series-wide redesign, and rebuild every manual afterwards:

| File | Holds |
|---|---|
| `styles/manual.css` | Colours, type, page layout, every component |
| `templates/manual.html` | Page skeleton: cover, inside cover, contents, body |
| `build.mjs` | Markdown rendering and the generated cover art (`coverArt()`) |

A single manual's look comes only from its front matter. Never style one manual by editing the shared files.

---

## 1. The idea

A **bookshop series**: calm, trustworthy, printed-feeling manuals for complete beginners.

- **One family, many faces.** Every volume shares one layout. Each gets its own two colours and cover pattern.
- **Print first.** US Letter, white paper, low ink. The PDF is the product; the website shows it off.
- **Quiet confidence.** Generous white space, a classic serif title, and no stock photos, gradients, emoji or clip art.

---

## 2. Covers

Every cover uses the same skeleton. Only the colours, the pattern and the words change.

```
GUIDES FOR EVERYTHING                    VOL. 07   ← series (left), volume (right)

          [ generated cover art, top ~60% of page ]

[ A BEGINNER'S MANUAL ]                            ← kicker, outlined box
Notion                                             ← title, Fraunces 62pt
One workspace for notes, docs, projects…           ← subtitle, Inter 15pt
─────────────────────────────────────────────
For complete beginners · October 2026 edition · Print edition · US Letter
```

**Rules**
- **White background.** It's the default and is toner-friendly: cover art uses only about 2–5% ink. Use `cover: dark` only for a special edition, never as the norm.
- **Title:** at most about 3 short lines. Use `title_html` with `<span class="soft">&amp;</span>` to colour a joining word.
- **Subtitle:** one sentence of 6–16 words with no full stop. It says what the reader will be able to do.
- **Kicker:** `A Beginner's Manual` by default. Use `A Field Guide` for directories and `A Power-User's Guide` for advanced volumes.
- **Art is generated, never drawn or downloaded.** Pick a `motif`; the pattern is seeded from the file name, so it's unique and repeatable.

### Cover motifs

| `motif` | Looks like | Suits |
|---|---|---|
| `orbits` | Rings around a centre | A core tool, an "everything" overview |
| `grid` | Field of dots and squares | Platforms, infrastructure, settings |
| `waves` | Flowing lines | Creative work, flows, markets |
| `blocks` | Stacked bars | Data, money, building things |
| `network` | Connected nodes | Automation, agents, integrations |
| `pages` | Fanned note cards | Writing, documents, knowledge |

Vary motifs between volumes that sit next to each other on the shelf.

---

## 3. Colour

Each manual sets exactly two colours in its front matter:

- **`accent`**: the manual's identity. It colours headings' numbers, step circles, rules, links, the kicker and the volume label. Choose a **mid-tone** that reads on white and prints well: not neon, and not near-black. Darker text uses of it are generated automatically (`--accent-ink`).
- **`accent2`**: a contrasting highlight used only in the cover art. Pick a different hue family, often warm against cool.

**Uniqueness rule:** no two volumes share the same `accent`. These pairs currently clash and should be re-coloured when next touched:
- GitHub and AI APIs (`#1F883D`)
- MCP and Python for AI (`#2F6FDE`)
- AWS and Custom Assistants (`#C2410C`)

**Fixed colours** (never change per manual):

| Token | Value | Used for |
|---|---|---|
| Ink | `#1b1d24` | Body text |
| Ink 2 | `#3a3e4b` | Secondary text |
| Muted | `#6a6f7d` | Running heads, captions |
| Rule | `#e2e0da` | Lines and table borders |
| Tip | `#17805a` on `#edf8f2` | `[!TIP]` callouts |
| Note | `#2459c9` on `#eef3fd` | `[!NOTE]` |
| Important | `#6d3fd1` on `#f4effd` | `[!IMPORTANT]` |
| Warning | `#a95a07` on `#fff6e6` | `[!WARNING]` |
| Caution | `#bf2630` on `#fdf0f0` | `[!CAUTION]` / `[!DANGER]` |

Callout colours mean the same thing in every manual, so never use them as a manual's accent.

---

## 4. Type

Four typefaces, each with one job. All are self-hosted and all are SIL Open Font License.

| Role | Font | Where | Size |
|---|---|---|---|
| Display | **Fraunces** | Cover title, chapter titles | Cover 62pt, chapter 33pt |
| Body | **Source Serif 4** | Paragraphs | 10.6pt, line height 1.52 |
| Interface | **Inter** | Section headings, labels, tables, running heads | H2 14.5pt, H3 11.2pt |
| Code | **JetBrains Mono** | Code, commands, file names | Ligatures off |

- The first paragraph after a chapter title is a larger **lead-in** (12.4pt), so write it as a welcoming one- or two-sentence summary.
- Small labels (kickers, callout heads, running heads) are Inter, **uppercase and letter-spaced**.
- Don't add fonts, and don't use bold or italic for decoration.

---

## 5. Pages

- **US Letter (8.5 × 11 in)**, margins 0.95 / 0.9 / 0.85 / 0.9 in (top, right, bottom, left).
- **Running heads:** manual name on the top left, current chapter on the top right, series bottom left, page number bottom right.
- **Front matter, in order:** cover, inside cover (blurb, reading legend and disclaimer), contents with real page numbers, then the body.
- Each chapter starts on a new page, numbered "Chapter N", with N.M section numbers. Directories set `chapter_break: false` so they flow.
- **The book always ends with** a Quick Reference chapter, then `# Glossary {.unnumbered}`.

---

## 6. Components

Write these in Markdown; the build styles them. The full syntax is in `content/_template.md`.

| Need | Write | Use it for |
|---|---|---|
| Chapter summary | `:::summary In this chapter` | Opening every chapter: 3–5 bullets |
| Steps | `:::steps Title` + numbered list | Any procedure: a bold step title ending in a period, then detail |
| Callouts | `> [!TIP]`, `NOTE`, `IMPORTANT`, `WARNING`, `CAUTION` | Asides. Use at most about two per page, and `CAUTION` only for money, data or access at risk |
| Checklist | `:::checklist` | Closing each chapter: "I can…" items |
| Cheatsheet | `:::cheatsheet` | Boxed one-page reference |
| Dense table | `:::compact` + table | Directories and long reference lists |
| Code | ```` ```bash ````, ```` ```json title=file.json ```` | Commands and files: lines ≤ 80 chars, blocks ≤ ~45 lines |
| Prompt | ```` ```prompt ```` | Text to paste into an AI tool |
| Price badge | `{{Free}}` `{{Freemium}}` `{{Paid}}` | Tool listings |
| Menu path | `[[Settings > Privacy > Data]]` | Every click path |
| Key | `<kbd>Ctrl</kbd>` | Keyboard shortcuts |
| Glossary | `:::glossary` with `Term` / `: definition` | The final chapter; it sorts itself |

**Tables:** 5 columns or fewer, with short cells. Long tables split across pages automatically.

---

## 7. Voice

- **For complete beginners.** Explain every term the first time it appears, and add it to the glossary.
- **Warm, hopeful, plain English.** Encourage the reader; never talk down to them or hype the tool.
- **Show, then tell.** Each chapter gives the reader something to do: steps, an example, a prompt to paste, or a checklist.
- **Honest.** Say clearly what costs money, what can go wrong, and what still prompts or fails.
- **Accurate and dated.**
  - Check every command, setting, menu path, price and plan against the official docs before printing it, and set `edition` to the month you checked.
  - If you can't verify something, describe it generally rather than guess.
- **Typography:** use typographic quotes (applied automatically) and an en dash for ranges (2–5), and keep "Claude Code", "GitHub" and other product names in their official capitalisation.
- **Headings:** sentence case, short, and no full stops. Never start a heading with a digit (`## 1. Setup` breaks the build); write `## Step one: setup` or drop the number.

---

## 8. Adding a manual

1. **Copy** `content/_template.md` to `content/<slug>.md`, using a short kebab-case slug, which becomes the file and URL name.
2. **Fill in the front matter:**
   - `title`, `subtitle`, `kicker`, `audience`, `blurb`;
   - the next free `volume` number, since no two manuals may share one;
   - `edition`, the month you checked the facts;
   - a unique `accent`, a contrasting `accent2`, and a `motif`.
3. **Write chapters** using the components above, ending with Quick Reference and the Glossary.
4. **Build:** run `node build.mjs <slug>`. The PDF, cover image and site card all update.
5. **Check:**
   - run `pdftoppm -png -r 50 output/<slug>.pdf /tmp/<slug>` and look at every page;
   - make sure there are no near-empty pages, stranded headings, or tables and code running off the page;
   - make sure the cover title fits and the art doesn't sit under the top labels.

## 9. Before you publish: checklist

- [ ] The cover is white, the title fits, and the subtitle is one sentence with no full stop
- [ ] `accent` is unique in the series, and the `volume` number is unique
- [ ] Every chapter has a summary, something to do, and a closing checklist
- [ ] Every new term is explained and is in the glossary
- [ ] Facts are checked against official docs, and `edition` is set to this month
- [ ] Callouts are colour-correct (`CAUTION` only for real risk)
- [ ] There are no headings starting with a digit, no code lines over 80 characters, and no tables over 5 columns
- [ ] You've built the manual and looked at every page
