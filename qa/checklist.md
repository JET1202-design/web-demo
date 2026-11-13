# Harbor Press — QA Checklist

Checked against `index.html` and live browser inspection at localhost:3737.

---

## 1. Copy matches copy.md exactly — PASS

Every visible text string was verified against copy.md via accessibility tree snapshot.

| Element | Expected (copy.md) | Rendered |
|---|---|---|
| Nav logo | Harbor Press | ✅ Harbor Press |
| Nav links | Titles, Workshops, Visit, Contact | ✅ All four present |
| Hero headline | Print the brief before you print the page. | ✅ Exact |
| Hero subhead | A small press for short books, workshop notes, and type you can hold. | ✅ Exact |
| Primary CTA | See this season's titles | ✅ Exact |
| Secondary CTA | Book a studio visit | ✅ Exact |
| Press paragraph | We set type by hand when the page needs weight… | ✅ Verbatim |
| Season heading | This season | ✅ Exact |
| Title 1 | Field Notes from the Harbor: a 48-page walk along the docks. | ✅ Exact |
| Title 2 | Workshop Booklets: one brief, one afternoon, one finished signature. | ✅ Exact |
| Title 3 | Type Specimens: a folder of faces we actually keep in the case. | ✅ Exact |
| Visit paragraph | Harbor Press is at 14 Dock Street. Visits are by appointment… | ✅ Verbatim |
| Footer | Harbor Press, 14 Dock Street. Visit by appointment. No fake reviews, no invented awards. | ✅ Verbatim |

---

## 2. Typography is not a default AI look — PASS

Computed via `preview_inspect`:

- Body: `font-family: "Source Sans 3", Georgia, serif` — not Inter, Roboto, Arial, or system-ui
- Hero h1: `font-family: Fraunces, Georgia, serif`
- Section headings: Fraunces (`.season__h2`, `.season__item-title`)
- Nav logo: Fraunces
- No fallback to system-ui anywhere in the font stack

---

## 3. Banned patterns absent — PASS

| Pattern | Status |
|---|---|
| Purple-on-white gradient | ✅ Not present. Background is flat `rgb(244, 239, 230)` |
| Text gradient | ✅ Not present. No `background-clip: text` anywhere in CSS |
| Three equal feature cards | ✅ Not present. "This season" items are plain grid blocks with no card chrome |
| Pill badges above headline | ✅ Not present |
| Fake testimonials | ✅ Not present |
| Invented logos or made-up client names | ✅ Not present |
| ALL-CAPS tracked eyebrow labels | ✅ Not present |
| Arrow → on button text | ✅ Not present. Buttons read "See this season's titles" and "Book a studio visit" |
| Numbered markers on non-sequence items | ✅ Not present. Season titles have no numbers |

---

## 4. Design rules (CLAUDE.md) followed — PASS

| Rule | Evidence |
|---|---|
| Fraunces for headlines | Computed `font-family: Fraunces, Georgia, serif` on h1 and h2 |
| Source Sans 3 for body | Computed `font-family: "Source Sans 3", Georgia, serif` on body |
| Ink #1C1917 | Computed `color: rgb(28, 25, 23)` on body |
| Paper #F4EFE6 | Computed `background-color: rgb(244, 239, 230)` on body |
| Accent rust #9A3412 | Computed `background-color: rgb(154, 52, 18)` on `.hero__cta-primary` |
| Rule line #D6C7B2 | Used as `--offset` in `border-top` on nav, section rules, footer |
| Left-aligned hero | Computed `text-align: start` on `.hero__h1`; hero has no `text-align: center` |
| Tokens in one place | All six values defined in `:root` at top of `<style>`, referenced via `var()` throughout; button hover uses `--harbor-hover`, not a bare hex |
| One motion item | Hero h1 `fadeIn` animation only; `prefers-reduced-motion` media query present at line 102 |
| No second palette | No hardcoded color literals outside `:root` (hover color moved to `--harbor-hover` in consistency pass) |

---

## 5. Local preview works — PASS

Page is served at `http://localhost:3737` via `npx serve` (configured in `.claude/launch.json`). Screenshot confirmed the page renders in the Browser pane. The page also opens directly as a file — `index.html` has no build step or server-side dependency.

---

## 6. Site is not published — PASS

No deploy step was run. No hosting service was configured. No exports folder was created. `localhost:3737` is a local dev server only; it is not reachable from outside this machine.
