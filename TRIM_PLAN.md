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

| | Before | After | Note |
|---|---|---|---|
| GI core | 15 | 15 | hold; →13 in phase-2 if Indigestion correlation confirms (§6.3) |
| IM (immune/inflammatory + skin) | 5 | 6 | absorbs `sk_skin` (§6.1) |
| BG | 5 | 5 | brainfog/fatigue wired into gut-brain pattern (§6.2) |
| NU | 4 | 4 | |
| SK | 5 | 0 | candida apparatus cut; `sk_skin` folded into IM (§6.1) |
| ME | 4 | 0 | broad-metabolic cut (locked); `cravings` cut with candida (§6.1) |
| SL | 4 | 0 scored | → drivers (locked) |
| OR | 4 | 0 | cut (locked) |
| HR | 6 | 0 | cut (locked) |
| **Scored total** | **52** | **30** | |

Plus drivers (unchanged + Sleep): Bristol, PSS-4, pain NRS/region, meds, lifestyle,
**+ sleep**. Net default completion target: **~3 minutes.**

## 5. Pattern plan: 12 → 10

| Pattern | Action |
|---|---|
| constipation_dominant / diarrhoea_dominant / mixed_bowel | **KEEP** (drive triage Tier 2; not mergeable — distinct management) |
| reflux_upper_gi | **KEEP** |
| bloating_fermentation | **KEEP** |
| stress_driven → **gut_brain** | **KEEP + EXTEND** (absorbs BG brainfog/fatigue, §6.2) |
| post_disruptor | **KEEP** (strongest probiotic rationale → Tier 3) |
| nutrient_malabsorption | **KEEP** (→ Tier 1) |
| lifestyle_modifiable | **KEEP** (→ Tier 4) |
| inflammatory_immune | **KEEP + EXTEND** (absorbs histamine, §5; + `sk_skin` signal, §6.1) |
| histamine_intolerance | **MERGE → inflammatory_immune** (same IM items; keep histamine sub-flag) |
| candida_yeast | **CUT** (§6.1 — speculative; footprint dismantled) |

Result: **10 patterns** (was 12), each tied to retained items and a triage tier.
*Note: an earlier draft floated "~8" — that would require merging the bowel trio,
which is clinically wrong (constipation vs diarrhoea vs mixed need different
management and map to different triage handling). 10 is the honest floor.*

## 6. Resolved decisions (recommendations baked in)

These were the three open items; recommendation + rationale now locked in for
sign-off. Each is a one-line revert if co-design disagrees.

### 6.1 Candida pattern → **CUT** (and dismantle its item footprint)

`candida_yeast` is the most speculative pattern in the set: "candida overgrowth"
inferred from a symptom cluster (thrush + itch + nails + cravings) is poorly
evidence-supported and is exactly the kind of claim that reads as pseudoscience
and undercuts a *clinical* tool's credibility. It also leans on the SK/ME items
we're trimming.

- **Cut** the `candida_yeast` pattern.
- **Cut** `sk_thrush`, `sk_itch`, `sk_nails`, `sk_yeast` (their only consumer was
  candida) and `me_cravings` (same) — removing ME entirely.
- **Keep the gut–skin axis represented, but make it earn its place:** retain
  **one** item, `sk_skin` (acne/eczema/rashes), and **fold it into the
  `inflammatory_immune` pattern** as an extra signal (atopic skin is an
  immune/inflammatory readout). SK as a standalone section disappears; the item
  lives under the immune/inflammatory domain.

Net: SK 5 → 1 (relocated to IM), ME 4 → 0, one fewer pattern.

### 6.2 BG brain-fog / fatigue → **WIRE-IN** (keep, don't cut)

`bg_brainfog` and `bg_fatigue` are signature gut–brain symptoms with strong face
validity — cutting them would weaken the very axis we're trying to foreground.
The fix is to make them *earn their place*: add both as supporting signals to the
gut–brain pattern (rename `stress_driven` → `gut_brain`, firing on GI-present +
either high psych load **or** prominent brain-fog/fatigue). Cheap, and it turns
two dead-weight items into decision-relevant ones.

### 6.3 Indigestion 4 → **HOLD at 4 for now** (collapse only on data)

`rumbling`/`burping`/`gas` almost certainly co-vary, but these are *validated GSRS*
items — cutting them pre-data risks dropping a real signal and weakening the one
instrument with external validity. **Recommendation: keep all 4 now**, tag for the
phase-2 empirical collapse (§7). Provisional post-data target if correlation
confirms: keep `bloating` + `gas`, drop `rumbling`.

## 7. Phase-2 empirical trim (after pilot data)

The pilot CSV already exports every item, cluster, pattern, and triage input — so
once N is sufficient we can trim *with evidence*, not opinion:

- Drop items with **near-zero variance** (everyone answers the same).
- Within a cluster, drop items with **high inter-item correlation** (redundant —
  e.g. the Indigestion trio).
- Keep any item that **flips a pattern or triage tier** across real respondents.

## 8. Implementation steps (only when approved)

1. Bump `SCHEMA_VERSION` (stored visits are version-tagged; old data survives).
2. Remove OR, HR, broad-ME (weight/glucose/thyroid) items from `QUESTIONS`;
   remove the OR/HR/ME/SK `SECTIONS` entries.
3. Move SL items into the drivers block (render + `extras`), out of `secNorm`.
4. Cut `candida_yeast`; remove `sk_thrush/itch/nails/yeast` + `me_cravings`;
   re-home `sk_skin` under the IM domain and add it as an `inflammatory_immune`
   signal (§6.1).
5. Merge `histamine_intolerance` into `inflammatory_immune` (histamine sub-flag).
6. Rename `stress_driven` → `gut_brain`; add `bg_brainfog`/`bg_fatigue` as
   firing signals (§6.2). Keep Indigestion at 4 (§6.3).
7. Re-run the unit + jsdom suites; confirm triage tiers unchanged and update the
   CSV header (dropped item/pattern columns, renamed pattern).

## 9. Risk note

Cutting *screen* domains is low-risk for the headline band: the Index is
GI-core-weighted and screen domains are capped, so removing SL/OR/HR/ME shifts the
overall % only slightly and never changes the GI-dominance logic. The main effect
is a shorter, sharper, more clearly *gut-focused* instrument.

## 10. Dysbiosis-correlate lens (Dys-R items) — specificity upgrade

### 10.1 The gap and the constraint

GSRS measures GI-symptom **severity**, which is only weakly specific to dysbiosis
(severe IBS-C with an ordinary microbiome scores like antibiotic-shattered
diversity). But **"dysbiosis" has no symptom-based gold standard**, so no item can
be *validated* as dysbiosis-specific without correlating it against stool
sequencing. Achievable goal: add items **mechanistically enriched** for
microbiome-altered phenotypes, keep them in a **separate lens** from the severity
score, and validate against any stool data the pilot collects.

### 10.2 Architecture — a parallel lens, NOT part of the burden score

Dys-R items feed a distinct **"Dysbiosis-correlate / fermentation-phenotype"**
indicator reported *alongside* (never inside) GI Symptom Burden:

> GI Symptom Burden: 45% · *Dysbiosis-correlate signals: 3 (fermentation-type,
> post-infectious onset, recent antibiotics)*

This preserves the reframe's honesty (severity stays severity), directly sharpens
**Triage Tier 3** (microbiome-support candidacy), and strengthens the
`bloating_fermentation` and `post_disruptor` patterns. Until validated against
sequencing, the lens is labelled **"correlate," never a dysbiosis measurement.**

### 10.3 Recommended items (4 new + 2 field upgrades)

**Enhancements to existing fields:**

| id | Item text | Response | Tier | Feeds |
|---|---|---|---|---|
| `dys_stool_var` | "Does your stool type change a lot from day to day (hard one day, loose the next)?" | Never / Sometimes / Often (0–2) | A | mixed_bowel + lens (also derivable across visits via trend) |
| `dys_abx_courses` | "How many courses of antibiotics in the last 12 months?" (upgrades the abx boolean) | 0 / 1 / 2 / 3+ (0–3) | A | post_disruptor (dose-response) → Tier 3 |

**Net-new items:**

| id | Item text | Response | Tier | Feeds |
|---|---|---|---|---|
| `dys_postinfectious` | "Did your gut symptoms first start after food poisoning, a stomach bug, or travel?" | No / Yes / Not sure | B | lens → Tier 3 *(highest-value add)* |
| `dys_food_triggers` | "Are your symptoms reliably triggered by any of these? (select all)" — Onion/garlic · Beans/lentils · Wheat/bread · Dairy · Sugar-free ('-ol') sweeteners · None | multi-select; score = count | B | bloating_fermentation + lens (absorbs separate lactose/fructose/wheat items) |
| `dys_gas_foul` | "Is your wind excessive, or foul / sulfur-smelling ('rotten egg')?" | Not at all → Marked (0–3) | B | bloating_fermentation + lens |
| `dys_fibre_paradox` | "Do fibre, prebiotics, or probiotic supplements make your bloating or gas WORSE?" | No / Yes / Haven't tried | B | bloating_fermentation (fermentation/SIBO phenotype) |

Tier A = strongest stool/microbiome correlates (stool transit/instability is the
#1 covariate of composition; disruptor exposure is a causal antecedent). Tier B =
moderate, mechanistically grounded, not currently captured.

### 10.4 Count impact

+4 new items +2 field upgrades, all in the lens (out of the burden score). Set
against the ~20 low-information items removed in §3–§6, this is still a **net
reduction** (≈30 + 4 ≈ 34 scored, vs 52) with a large specificity gain —
severity-noise traded for dysbiosis-signal.

### 10.5 Validation plan (gates any "dysbiosis" claim)

The pilot CSV already exports per-item data. Once stool sequencing is available
for a subset:
- Test each Dys-R item's correlation with sequencing-defined dysbiosis markers
  (richness/diversity, Enterobacteriaceae, H2S producers, methanogens).
- **Keep** items that correlate; **drop** those that don't (same evidence
  discipline as §7).
- Only after this may the lens graduate from "correlate" to a quantified
  microbiome-risk readout.

### 10.6 Open question for sign-off

Whether to surface the lens as a **signal count** (e.g. "3 dysbiosis-correlate
signals") or a **named phenotype** (e.g. "fermentation-type"). Recommend starting
with the count + contributing-signal list (conservative, transparent) and adding
phenotype labels only once §10.5 validation supports them.
