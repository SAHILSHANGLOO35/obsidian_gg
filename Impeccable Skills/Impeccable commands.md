## 🛠 System — setup & one-time context

|Command|Use when|
|---|---|
|`init`|First thing to run in a project. Gathers design context, writes `PRODUCT.md` and `DESIGN.md` so every later command knows your audience, brand, colors, and type.|
|`document`|You have an existing codebase with no design docs. Generates `DESIGN.md` by reading your actual code.|
|`extract`|Patterns are starting to repeat. Pulls reusable components and tokens into a proper design system.|

## ✏️ Shape — before you write code

|Command|Use when|
|---|---|
|`craft`|Starting something from scratch. Full shape-then-build flow with visual iteration.|
|`shape`|Want a plan/wireframe discussion first, lighter than `craft` — no build yet.|

## 🔍 Evaluate — check what exists

|Command|Use when|
|---|---|
|`audit`|Technical quality check — accessibility, performance, responsive. Scored across 5 dimensions with P0–P3 severity.|
|`critique`|UX design review — hierarchy, clarity, emotional resonance. Runs persona sub-agents scored against Nielsen's heuristics.|

## 🎨 Refine — targeted design fixes

|Command|Use when|
|---|---|
|`typeset`|Text looks like default typography — muddy hierarchy, same-looking sizes, tiny body copy, no kerning attention.|
|`layout`|Spacing, rhythm, or alignment feels off. (Formerly `/arrange`.)|
|`colorize`|Interface is monochromatic/flat and needs strategic color.|
|`animate`|Needs purposeful motion — not decorative jitter.|
|`bolder`|Design reads as safe, boring, or generic — needs more visual confidence.|
|`quieter`|Opposite problem — too loud, needs toning down.|
|`delight`|Functional but forgettable — wants a memorable moment added.|
|`overdrive`|You explicitly want technically extraordinary / showcase-level effects.|

## ✂️ Simplify — subtraction

|Command|Use when|
|---|---|
|`distill`|Ruthless subtraction. Strips to essence — removes competing buttons, redundant info, decorative clutter, extra fonts, extra nav items.|
|`clarify`|Messaging/copy or flow is confusing, not the visuals — sharpens communication.|
|`adapt`|Porting a design to a different platform/context (e.g. native iOS/Android).|

## 🧱 Harden — production readiness

|Command|Use when|
|---|---|
|`harden`|Error handling, i18n, text overflow, edge cases. Also covers first-run flows and empty states.|
|`optimize`|Performance-specific pass.|
|`polish`|Final pass — design system alignment and shipping readiness. Last step before commit.|

---

## Typical workflows

**Small tweak (e.g. a button style):**

```
/impeccable typeset   (only if text/sizing is the issue)
/impeccable polish    (final consistency check)
```

**New feature, start to finish:**

```
/impeccable craft     → build it
/impeccable audit     → find issues
/impeccable layout    → fix spacing (if flagged)
/impeccable typeset   → fix type (if flagged)
/impeccable harden    → edge cases, i18n, errors
/impeccable polish    → final pass before shipping
```

**Existing project, first time using Impeccable:**

```
/impeccable init      → set up PRODUCT.md / DESIGN.md
/impeccable document  → generate DESIGN.md from existing code (if no docs yet)
/impeccable audit     → see where things stand
```

---

## Notes on setup (VS Code + Copilot)

- Copilot in VS Code reads skills from **`.github/skills/`**, **`.claude/skills/`**, and **`.agents/skills/`** — an install landing in `.claude/skills/impeccable` still works fine with Copilot.
- The automatic post-edit design hook is Copilot-specific: `.github/hooks/impeccable.json`. Check it exists if you want _every_ UI edit auto-checked, not just explicit `/impeccable` calls.
- Ephemeral runtime files live in `.impeccable/` (screenshots, session state, caches) — gitignore this. `PRODUCT.md`, `DESIGN.md`, and the skill's own command files should be committed.