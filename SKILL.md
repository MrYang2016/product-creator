---
name: product-creator
description: >-
  Use when the user has a digital-product idea (course, template, system,
  download, newsletter offer) and wants step-by-step guidance to build and sell
  it, or to resume an existing idea folder under
  /home/box/agent-data/digital-products/.
---
# product-creator

Based on Hussain Ibarra, [How to build a profitable digital product (in 7 steps)](https://x.com/HussainIbarra/article/2108563595676299429) (status: https://x.com/HussainIbarra/status/2108563595676299429). Keep this source URL in every product folder’s `SOURCE.md`.

Guide the user one step at a time. They bring the idea; you run the process, write artifacts into the folder, and advance progress only after they confirm that step’s output.

## Folder root (required)

All ideas live under:

`/home/box/agent-data/digital-products/<idea-slug>/`

- `<idea-slug>`: kebab-case from the idea (ASCII letters/numbers/hyphens), e.g. `newsletter-system`, `branding-board-course`.
- One idea → one folder. Never mix two ideas in one folder.
- List existing ideas with `ls /home/box/agent-data/digital-products/` before creating a new slug. If the slug exists, treat as resume unless the user insists on a new idea (then pick a distinct slug).

### Folder layout (create on first run)

```
/home/box/agent-data/digital-products/<idea-slug>/
  SOURCE.md          # article URL + one-line idea
  IDEA.md            # raw idea from the user
  PROGRESS.md        # current step (1–7), status, next action
  01-sawdust.md
  02-dream-customer.md
  03-promise.md
  04-curriculum.md
  05-case-study.md
  06-sales-page.md
  07-traffic.md
```

`PROGRESS.md` minimum fields:

```markdown
# Progress
- idea-slug:
- current_step: 1
- status: in_progress | blocked | done
- last_updated: YYYY-MM-DD (Asia/Shanghai)
- next_action: one concrete sentence
- completed_steps: []
```

## On every invoke

1. **Parse intent**
   - New idea: user states what they want to build/sell.
   - Resume: user names the idea, slug, or says “继续 xxx”.
   - If ambiguous and multiple folders exist, list slug + `IDEA.md` first line and ask which to open (widget or short list).
2. **New idea path**
   - Derive `<idea-slug>` (ask once if unclear).
   - `mkdir -p` the folder; write `SOURCE.md`, `IDEA.md`, empty step files if useful, and `PROGRESS.md` at step 1.
   - Tell the user the folder path.
3. **Resume path**
   - Read `PROGRESS.md` + the current step’s file.
   - Continue from `current_step` / `next_action`; do not restart from step 1 unless asked.
4. **Pace**
   - Work **one step per turn** (or finish the open sub-task of the current step).
   - After the user accepts the step’s artifact, update that step’s `.md`, bump `PROGRESS.md`, then offer the next step.
   - Prefer Chinese for user-facing guidance unless they write in another language.
5. **Do not** push tool-specific CTAs from the source article (e.g. a named product builder). Map actions to plain deliverables: package existing material, write curriculum, draft sales page, plan traffic.

## The 7 steps (coach the user through these)

### 1. Sell your sawdust → `01-sawdust.md`
Goal: productize a system they already use and barely notice.

Ask / capture:
- What system do they already run in files, boards, notes, or workflows?
- Who already pays (or would pay) for that system as a kit, template, method, presets, or process?
- What raw assets already exist (docs, boards, checklists, code, prompts)?

Write: inventory of assets, proposed product form (course / download / template pack / AI-assisted guide), and “why this is sawdust not a brand-new invention.”

Gate to step 2: clear product form + asset list.

### 2. Create your Dream Customer → `02-dream-customer.md`
Goal: one Customer Avatar. “If you’re selling to everyone, you’re selling to no one.”

Ask / capture:
- If selling to a past self, **which year/version** (each has different problem, skill, budget)?
- Hell → Heaven for that one avatar (concrete, not vague).

Write: avatar name/version, Hell, Heaven, budget/skill constraints, and what “done” looks like for them.

Gate to step 3: one Hell → Heaven pair.

### 3. Write your promise → `03-promise.md`
Goal: specificity. Vague promises don’t sell.

Formula:

`Helping [WHO] go from [HELL] to [HEAVEN] so they can [BENEFIT(s)].`

Also draft a sharper headline-style promise (optional named mechanism only if they have one; do not invent fake framework names).

Gate to step 4: user-approved promise sentence.

### 4. Create your curriculum → `04-curriculum.md`
Goal: steps of the transformation. Overdelivering on the promise is enough; extra content overwhelms.

Decision rule from the promise:
- 3–5 major milestones = modules
- Each milestone: 3–5 action steps = lessons

Typical arc (adapt, don’t force):
1. Know what to build (problem → offers → pick → promise)
2. Build the product (structure, results, bonuses)
3. Get customers (leads, conversations, offer page, payment)
4. Collect social proof (delivery, results, case studies)

Prefer an implementable path (checklists, templates, guided practice) over theory-only dumps. If they want an “AI guide of themselves,” note it as an optional delivery layer, not a required vendor.

Gate to step 5: module/lesson outline locked.

### 5. Become your own case study → `05-case-study.md`
Goal: proof. Free client work is only to prove competence; self-results count if they demonstrate the promised outcome.

Ask / capture:
- Can they get themselves (or already have) the result the promise sells?
- What specific numbers/artifacts prove it?
- If not, the smallest proof plan (self-run or free work) before selling at scale.

Write: case-study bullet points usable on a sales page.

Gate to step 6: at least one concrete proof story or an explicit “proof plan before launch.”

### 6. Write your sales page → `06-sales-page.md`
Goal: structure + clear copy. They don’t need to be a copywriter; fill the sections.

Required sections (adapt wording; keep order):
1. **Promise** — headline sells the outcome; subheadline adds timeframe / mechanism / numbers if real
2. **Problem** — specific avatar pain (not generic “keep reading if…” lists)
3. **Process** — why this path is different; sell what each phase gets them
4. **Features + benefits** — each module: what they learn + benefit (pain’s opposite)
5. **Proof** — social proof or self case study; few, big, specific
6. **Price** — state it; frame as math (one result pays for it)
7. **Guarantee** — clear, friendly risk reversal
8. **CTA** — recap promise, price, hell-of-inaction vs heaven-of-action, one button
9. **FAQ** — what it is; who for; when results; top objections; refund; buy again

Gate to step 7: draft page the user accepts as “good enough to put live.”

### 7. Send traffic → `07-traffic.md`
Goal: people will not find the product by themselves. Traffic is the lever when revenue is low—often without changing the offer.

Two levers:
1. Increase promotion frequency (what you sell, what to do, how to buy, when).
2. Create more content so promos are a smaller share of posts (more content = more room to sell without feeling spammy).

Capture a simple weekly plan: content cadence, promo slots, where the link lives, and a rough click → conversion sanity check.

Gate to done: traffic plan written; set `PROGRESS.md` status to `done` (or `in_progress` if they want ongoing weekly iteration—then `next_action` is the next promo/content block).

## Framing to keep light (optional, not steps)

Only if the user is stuck on “should I even start”:
- Downside is usually small vs staying stuck.
- Digital products: near-zero marginal cost, instant delivery; distribution is attention.
- Don’t turn this into a pep talk every run.

## Done criteria for a run

- Folder path reported to the user
- Current step artifact saved
- `PROGRESS.md` updated
- Clear one-line `next_action` for the next invoke
