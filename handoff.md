# Handoff – Italiensk / Sætningsbyggeren 🇮🇹

A small, dependency-free web app for learning to build simple Italian sentences from two
handwritten study notes. Built conversationally with **Claude Code (Opus 4.8)**.

- **Live:** https://strudso.github.io/italian-tables/
- **Repo:** https://github.com/STRUDSO/italian-tables (public, GitHub Pages from `main` / root)
- **Source notes:** two scanned study notes (`.heic`) in the working dir, gitignored.

---

## What this is

From two handwritten tables (verb conjugation + nouns/articles) we built an interactive
"sentence builder": pick **Person · Udsagnsord · Form · Navneord · Tillægsord** and the app
conjugates the verb, picks the correct article, agrees the adjective, and **shows which table
cell each part came from**. Sentences are intentionally allowed to be nonsense — the goal is to
illustrate *construction*, not meaning (see disclaimer on each page).

## Two views shipped

| View | URL | Concept |
|------|-----|---------|
| **A – Fokuseret udsnit** | `/focus/` | A "zoom-in" slice of each table appears under the builder; full tables below highlight the same cells. Now also has **two-way binding**: **hover** a dropdown → spotlight + Danish callout of what it controls; **click** any cell (full tables *and* the focused-slice mini-tables) → that dropdown changes and the sentence rebuilds. |
| **B – Ord-sporing** | `/trace/` | Sentence rendered as colored word-chips. **Hover** a word → source bubble (no scroll). **Click** → scrolls the full table to that cell. All used cells highlighted by default. |

Plus a **`/lab/`** sandbox gallery with 3 interaction experiments built on Fokuseret udsnit
(`click` = reverse-click, `color` = color-link, `hover` = hover-reveal). A 4th "Klik + Hover"
combo was prototyped, chosen, and **promoted to `/focus/`** (then removed from the lab).

Landing page (`/index.html`) is a gallery linking to both, plus a "recipe" of how it was made,
a disclaimer, and an open-source bar (Star/Fork/Kildekode + shields badges).

## Repo structure

```
.
├── index.html          # landing / gallery + recipe + disclaimer + OSS bar
├── focus/index.html    # View A (now = click+hover combo; self-contained)
├── trace/index.html    # View B (self-contained)
├── lab/index.html      # experiments gallery (links to the 3 prototypes)
├── lab/click/          # prototype: reverse-click (table → dropdown)
├── lab/color/          # prototype: color-link (per-dropdown signature colors)
├── lab/hover/          # prototype: hover-reveal (spotlight what a dropdown controls)
├── README.md           # public readme w/ badges
├── LICENSE             # MIT © 2026 STRUDSO
├── handoff.md          # this file
└── .gitignore          # ignores *.heic, *.png, .DS_Store, .nwave/
```

Both view pages are **standalone** — they duplicate the grammar data + logic. There is **no
shared JS module**; a change to the grammar must be applied to *both* files.

## Key implementation notes

- **Grammar data** (in each view's `<script>`): `subjects`, `endings` (are/ere/ire × 6 persons),
  `verbs`, `nouns` (with `pl`/`daPl`), `adjs`, and `forms` (the 3 columns of the noun table).
- **Article logic:** `indefiniteArticle` / `definiteArticle` / `pluralArticle` → `articleFor(n, form)`.
- **Adjective agreement:** `adjForm(a, gender, plural)` — `-o` type varies by gender+number, `-e`
  type by number only.
- **Form selector** drives: article, noun sg↔pl, adjective agreement, and **which table column**
  (0=ubestemt, 1=bestemt ental, 2=flertal) gets highlighted.
- **Adjective table cell IDs** `a-{o|e}-{m|f}-{sg|pl}` are load-bearing — JS targets them. Don't rename.
- **Tables renamed** from "Tabel 1/2" to real names with Italian: *Udsagnsord (i verbi)*,
  *Navneord & artikler (i nomi & gli articoli)*, *Navneord (i nomi)*, *Tillægsord (gli aggettivi)*.

## How to publish changes

```bash
git add -A
git commit -m "type: message"
git push origin main
```

Pages rebuilds automatically (~30–60s). Pretty URLs work because each view is a folder with
`index.html` (`/focus/`, `/trace/`). Verify with:
`curl -s -o /dev/null -w "%{http_code}" <pages-url>/focus/`

---

## Changelog

1. **Initial build** – converted `.heic` photos → transcribed both tables → single `index.html`
   with the two tables, navneord/tillægsord explanations, and an interactive sentence builder.
2. **Published** – created public repo `STRUDSO/italian-tables`, pushed, enabled GitHub Pages.
3. **Builder on top + live highlight** – sticky builder, used cells glow in the full tables.
4. **3 prototypes (parallel agents)** – A (focused slice), B (token tracing), C (spotlight +
   connector lines); landing page turned into a gallery indexing all + classic.
5. **B: hover→bubble, click→scroll** – removed surprise auto-scroll on hover.
6. **Form selector** – ubestemt/bestemt/flertal added to all versions, placed before Navneord;
   drives article + noun number + adjective agreement + correct highlighted column.
7. **B default highlight** – all used cells (verb + article/noun + adjective) lit by default.
8. **Kept A & B only** – removed classic + spotlight; restructured to pretty URLs `/focus/`,
   `/trace/`; added back-to-gallery links.
9. **Open-source polish** – MIT LICENSE, richer README w/ badges, repo description/homepage/topics,
   on-page Star/Fork/Kildekode bar + shields, untracked `.DS_Store`.
10. **Recipe + disclaimer** – landing-page "Opskriften" section; disclaimer (sentences may be
    nonsense) on all pages; OSS bar moved to the bottom.
11. **Renamed tables** – dropped "Tabel 1/2" for real names incl. Italian; converted "Om navneord"
    card into a proper table; unwrapped "Om tillægsord" into a consistent table section.
12. **Landing copy** – removed "Visning A/B" framing; made clear it's the *same tool*, two views.
13. **Endelse-table tracing** – selecting a noun now also highlights the matching row (-o/-a/-e) in
    the "Navneord (i nomi) · køn & flertal" table, column following the Form selector (both views).
14. **Title cleanup** – dropped "Prototype A/B" / "Token lineage" / "Visning A/B" from page titles,
    badges, and footers; consistent naming across both views.
15. **Italian fix** – elided articles in the reference tables now attach with no space
    (`un'arancia`, `l'arancia`, `l'amico`); the built sentence was already correct.
16. **Noun in breakdown** – `/focus/` breakdown line now includes the Navneord chip (was missing).
17. **/lab/ experiments** – 3 prototypes (reverse-click, color-link, hover-reveal) built by parallel
    agents on Fokuseret udsnit; plus a 4th "Klik + Hover" combo.
18. **Combo promoted** – the click+hover combo became the new `/focus/`; focused-slice mini-tables
    made clickable too; "🧪 Eksperimenter" links added at the bottom of `/focus/`; combo removed
    from `/lab/`.

---

## Known issues / offered tweaks

- **Row highlight covers the gender colour.** When a noun is selected, its row in the noun table
  gets the yellow highlight, hiding the pink/blue gender band. *Offered but not yet done:* make the
  row highlight a **border/glow** instead of a background fill so the gender tint stays visible.
- **Logic duplicated across `/focus/` and `/trace/`.** Any grammar change must be made in both
  files. Could be refactored to a shared `app.js` if it grows.

## Ideas / what's next

- Extract shared grammar data + logic into one `app.js` imported by both views.
- Add more verbs / nouns / adjectives (and maybe irregular verbs like `essere`, `avere`).
- Optional "quiz" mode: show Danish, user assembles the Italian.
- Audio (TTS) for the built sentence.
- Toggle to show the literal English/Danish gloss word-by-word.
- The row-highlight-vs-gender-colour tweak above.

## Last change

> Promoted the **click + hover combo to `/focus/`** (two-way binding: hover a dropdown to see what
> it controls, click any cell — including the focused-slice mini-tables — to drive the sentence).
> Added an "🧪 Eksperimenter" links section to `/focus/`, and removed the now-redundant combo from
> `/lab/` (the three remaining prototypes stay as a showcase).
