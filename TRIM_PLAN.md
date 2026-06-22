# Gut Health Screen — Trim & Refocus Plan (co-design DRAFT for sign-off)

> Status: **proposal only.** No schema/engine changes have been made. This is the
> keep/cut/merge sheet to review before any edits to `gut_screen.html`.
> Code comments that say "See TRIM_PLAN" refer to this file.

## 1. Goal

Two asks, one move:

- **Make it more of a *gut* screen + its connected systems** (not a whole-body
  symptom inventory).
- **Cut length / completion time** (currently 52 scored items + drivers).

The lever for both is the same: **every item must earn its place** — it should
change an output (feed a *pattern*, move a *triage tier*, or belong to the *GI
core band*). Items that only nudge the overall Index magnitude are dilution: the
Index is GI-core-dominant and screens are capped, so they barely move the band
and they change no guidance.

## 2. Decisions locked (this round)

- **Sleep (SL)** → relocate to the **drivers/modifiers** block (it's a modifier,
  not a gut symptom). Leaves the scored Index; stays visible as context.
- **Remove entirely:** Oral/ENT (OR), Hormonal/urogenital (HR), and broad
  Metabolic (weight, glucose, thyroid). No gut-specific engine pathway; whole-body
  review that dilutes the screen's identity and time budget.

## 3. The audit — what each item feeds

Across all 12 patterns, only the **GI** and **IM** *domain scores* are read by the
engine; everything else is consumed (if at all) only by **named items**. So an
item with no named consumer and a domain band nothing reads = pure inventory.

| Domain | Items | Verdict | Why |
|---|---|---|---|
| **GI core** (GSRS) | 15 | **KEEP** | Validated spine; drives band + bowel/reflux/bloating patterns + triage. (Indigestion 4→2 flagged for empirical collapse, §6.) |
| **IM** immune/food | 5 | **KEEP** | All earn place: `food_react`→bloating+inflammatory; `allergies`/`histamine`→histamine; `infections`/`joint`→IM band (read by inflammatory pattern). |
| **BG** brain-gut | 5 | **KEEP 3, WIRE-IN 2** | `anxiety`/`mood`→stress pattern; `headache`→histamine. `brainfog`/`fatigue` feed nothing today — keep (signature gut-brain symptoms) **only if** wired into the stress/gut-brain pattern; else cut. |
| **NU** nutrient | 4 | **KEEP** | All four → nutrient-malabsorption pattern → Tier-1 refer. |
| **SK** skin/yeast | 5 | **DEPENDS on candida (§6)** | `thrush`/`itch`/`nails`/`yeast`→candida pattern; `skin` feeds nothing. If candida is cut, SK collapses to 1 general gut-skin item. |
| **ME** metabolic | 4 | **CUT 3, decide 1** | `weight`/`glucose`/`thyroid` = **CUT** (locked). `cravings`→candida only (see §6). |
| **SL** sleep | 4 | **RELOCATE → driver** (locked) | No pattern reads it; it's a modifier. |
| **OR** oral/ENT | 4 | **CUT** (locked) | Nothing reads it. |
| **HR** hormonal | 6 | **CUT** (locked) | Nothing reads it; all optional/often N/A. |

**Dead-weight identified:** 20 of 52 scored items feed no pattern and no triage
decision (SL 4, OR 4, HR 6, ME weight/glucose/thyroid 3, BG brainfog/fatigue 2,
SK skin 1).

## 4. Resulting scored schema (under locked decisions)

| | Before | After |
|---|---|---|
| GI core | 15 | 15 (→13 if Indigestion collapsed, §6) |
| IM | 5 | 5 |
| BG | 5 | 3–5 (per brainfog/fatigue decision) |
| NU | 4 | 4 |
| SK | 5 | 1–4 (per candida decision) |
| ME | 4 | 0–1 |
| SL | 4 | **0 scored** (→ drivers) |
| OR | 4 | 0 |
| HR | 6 | 0 |
| **Scored total** | **52** | **~28–32** |

Plus drivers (unchanged + Sleep): Bristol, PSS-4, pain NRS/region, meds, lifestyle,
**+ sleep**. Net default completion target: **~3 minutes.**

## 5. Pattern plan: 12 → ~8

| Pattern | Action |
|---|---|
| constipation_dominant / diarrhoea_dominant / mixed_bowel | **KEEP** (drive triage Tier 2) |
| reflux_upper_gi | **KEEP** |
| bloating_fermentation | **KEEP** |
| stress_driven | **KEEP** (consider absorbing BG brainfog/fatigue, §3) |
| post_disruptor | **KEEP** (strongest probiotic rationale → Tier 3) |
| nutrient_malabsorption | **KEEP** (→ Tier 1) |
| lifestyle_modifiable | **KEEP** (→ Tier 4) |
| histamine_intolerance | **MERGE → inflammatory_immune** (same IM items; keep histamine sub-flag) |
| inflammatory_immune | **KEEP** (absorbs histamine) |
| candida_yeast | **CUT or demote** (speculative "-leaning"; leans on SK items being trimmed) |

Result: ~8 patterns, each tied to retained items and to a triage tier.

## 6. Open decisions for co-design sign-off

1. **Candida pattern** — cut entirely, or keep as a low-confidence optional? This
   determines whether SK keeps 3–4 items + `me_cravings`, or collapses to 1.
2. **BG brainfog / fatigue** — wire into the gut-brain (stress) pattern so they
   earn their place, or cut? (Recommend wire-in — strong face validity.)
3. **Indigestion collapse (15→13)** — `rumbling`/`burping`/`gas` almost certainly
   co-vary. Provisional: keep `bloating` + `gas`, drop `rumbling`. Confirm
   empirically from pilot data (§7) before cutting GSRS items.

## 7. Phase-2 empirical trim (after pilot data)

The pilot CSV already exports every item, cluster, pattern, and triage input — so
once N is sufficient we can trim *with evidence*, not opinion:

- Drop items with **near-zero variance** (everyone answers the same).
- Within a cluster, drop items with **high inter-item correlation** (redundant —
  e.g. the Indigestion trio).
- Keep any item that **flips a pattern or triage tier** across real respondents.

## 8. Implementation steps (only when approved)

1. Bump `SCHEMA_VERSION` (stored visits are version-tagged; old data survives).
2. Remove OR/HR/broad-ME items from `QUESTIONS`; remove their `SECTIONS` entries.
3. Move SL items into the drivers block (render + extras), out of `secNorm`.
4. Merge `histamine_intolerance` into `inflammatory_immune`; resolve candida.
5. Apply BG wire-in / Indigestion decisions from §6.
6. Re-run the unit + jsdom suites; confirm triage tiers and the CSV header update.

## 9. Risk note

Cutting *screen* domains is low-risk for the headline band: the Index is
GI-core-weighted and screen domains are capped, so removing SL/OR/HR/ME shifts the
overall % only slightly and never changes the GI-dominance logic. The main effect
is a shorter, sharper, more clearly *gut-focused* instrument.
