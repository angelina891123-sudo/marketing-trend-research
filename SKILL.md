---
name: marketing-trend-research
description: Runs a rigorous, evidence-gated marketing/industry trend research workflow for a specific campaign, brand, platform, or industry topic — from a confirmed research brief through source-tiered evidence discovery, independently-verified trend formation, insight generation, strategy translation, to a final trend report / proposal / executive deck. Enforces strict evidence discipline (no fabrication, WebFetch-verified claims, honest "no trend found" outcomes), a fixed Media Product Boundary (stops at marketing implications, never recommends specific media tools/placements), and human-approval gates at the moments that matter. Use when the user asks for a structured, source-verified market/marketing trend research deliverable — not for a quick web-search summary or a single fact lookup.
---

# Marketing Trend Research Skill (Production v1.5)

**Provenance**: Derived from and validated against `00_project/stage_12_workflow_architecture_v1_1.md` and `stage_13_reusable_skill_specification.md` (Production Skill Specification v1.5) in this repository, through 6 test campaigns (the original 2026 Taiwan Double 11 project, Pilot 02 B2B brand trust, Pilot 03 digital health, Pilot 04 streaming subscriptions, Pilot 05 media-platform trend scan, Pilot 05B AI-marketing adoption). Read `reference/known_limitations.md` before relying on this skill for a high-stakes deliverable — it documents exactly what has and has not been validated in real use.

## When to use this skill

Use it when someone asks you to research trends for a specific, scoped topic (a campaign, a brand's category, a platform, an industry) and wants a decision-ready, source-backed deliverable — not when they want a quick answer to one factual question, and not when they've already given you a finished dataset to analyze (that's just analysis, not this workflow).

## Non-negotiable core principles

These apply regardless of topic. Violating any of them is a defect, not a stylistic choice:

1. **No fabrication, no estimation-as-fact.** Every specific number/date/claim must trace to a real source. Prefer direct fetch verification over search-snippet confidence; when only snippet-level confidence is available, say so and downgrade the claim's strength accordingly.
2. **Source tiers, defined fresh per campaign.** Tier 1 = official/government/company self-published or listed-company disclosure. Tier 2 = credible named research bodies / trade media directly verifying a Tier-1 source. Tier 3 = agency blogs, unnamed commentary, unverifiable secondhand paraphrase. Context Only = right topic, wrong market (e.g., global/regional data with no breakout for the market actually being researched) — never presented as evidence for the target market. **Do not reuse another campaign's named source list — redefine tiers for the topic at hand** (see `reference/evidence_and_closure.md` §1).
3. **Independent Evidence Family, not source/article count.** Multiple outlets reporting the *same* underlying survey/announcement/dataset are ONE family, not several. A trend needs ≥2 independent families of CORE-tier evidence to qualify — this is a hard threshold with one narrow, documented exception (see `reference/evidence_and_closure.md` §2, the PROVISIONAL CANDIDATE path — rare, four conditions must ALL hold, never force it to "make a test pass").
4. **Research Closure is a legitimate, honest outcome.** If the evidence doesn't support a trend, say so plainly and stop — do not lower standards, cherry-pick, widen the time window after the fact, or force a cluster to reach the family-count threshold. A well-documented "no valid trend found, here's why" is a successful research outcome, not a failure. Use the 7-state Research Closure Model in `reference/evidence_and_closure.md` §3 to classify *why* it closed — the reason matters for anyone using this later.
5. **Media Product Boundary.** Conclusions stop at "what this means for marketing strategy." Never recommend a specific media tool, ad platform placement, or media-buying product — that decision belongs to whoever executes the strategy, not to this research.
6. **Campaign Specificity, honestly labeled.** Every piece of evidence gets classified on the six-level scale (CAMPAIGN-SPECIFIC / SEASONAL CONTEXT / ANNUAL MARKET SIGNAL / BROADER MARKET TREND / BROADER TECHNOLOGY TREND / STRUCTURAL BACKGROUND) — redefine what each level *means* for the current topic, don't reuse another campaign's definitions verbatim. STRUCTURAL BACKGROUND can support context/explanation but never stands alone as trend evidence.
7. **Never present interpretation as fact.** Keep inference (what you conclude) visibly separate from observation (what a source actually said). If a widely-repeated number can't be traced to a real methodology, flag it, don't repeat it.
8. **Layer 1 / Layer 2 separation.** Internal registries and this skill's technical vocabulary (evidence_family_id, MC/AMEND numbers, Tier labels, Token names, QA type names) are for your own bookkeeping and any final audit-style report. What you *say to the user* during normal execution should be plain language — see "User-facing interaction model" below.

## Step 0 — Campaign intake (produces the Research Brief)

Before any research, collect (or default, then confirm) these fields — do not skip straight to searching:

- `campaign_name`, `business_context`, `primary_market` (+ optional `secondary_market`)
- `research_objective` and `research_questions` (the specific questions this must answer)
- `research_window` (primary window + any exception rule for "old news with a genuinely new in-window development" — be strict about this; don't let stale news get relabeled as fresh)
- `research_dimensions` (the specific angles to cover)
- `campaign_specificity_definition` (six-level framework — content redefined per topic, per principle 6 above)
- `source_priority` (Tier 1/2/3 definitions — redefined per topic, per principle 2 above)
- `inclusion_criteria` / `exclusion_criteria`
- `expected_trend_count` (a range; **0 must always be an explicitly acceptable value**)
- `final_audience` and `required_deliverables` (Report / Proposal / Deck — any combination; Proposal and Deck are conditional on an actual trend existing to build them from)
- `language`

This becomes the Research Brief. See `reference/registries.md` for the full field reference if a campaign config is ambiguous.

## The workflow, by layer

Full module-by-module detail (exact inputs/outputs/QA per step) lives in `reference/qa_and_gates.md`. The shape:

1. **Research** — confirm the Brief; broadly discover candidate evidence against the brief's dimensions (WebSearch + WebFetch; every concrete number needs a fetch-verification trail, not just a search snippet).
2. **Evidence** — score and classify every candidate (source tier, claim strength, Campaign Specificity, CORE/SUPPORTING/CONTEXT/EXCLUDE role). If evidence is patchy, a bounded, human-approved "targeted gap recovery" loop is allowed — each loop must attack the gap from a genuinely new angle, not repeat the same search.
3. **Trend** — cluster findings that share a common underlying change; require ≥2 independent CORE evidence families to qualify a cluster; score qualifying clusters on the five-dimension rubric; merge genuine overlaps; run a final "did we miss anything" gap check before closing the research phase.
4. **Insight** — only for qualified trends: generate the marketing insight, run its own quality/acceptance check.
5. **Strategy** — translate accepted insights into a proposal narrative, checked against the Media Product Boundary and campaign relevance.
6. **Delivery** — render the Final Trend Report and, if applicable, the Proposal and/or Executive Deck; run automated QA (rendering, cross-artifact consistency, content quality) before presenting for final approval.

Governance runs continuously underneath all of this: registries stay internally consistent, merges propagate evidence correctly, nothing gets silently orphaned. See `reference/registries.md`.

## User-facing interaction model (what the person on the other end actually sees)

Don't narrate the 20 internal steps or ask for approval 13 times. Present exactly this:

- **Gate 1 — Research Brief Confirmation** (always shown, blocking). Plain-language: scope, timeframe, what you'll look at, how many trends you expect to find (explicitly including "possibly none"). **Stop and wait for an actual response — approve, modify, or cancel.** If they modify something, update and re-present; do not treat a modification as approval.
- *(silent progress — no approval needed unless something below triggers)* Evidence gathering and trend clustering run automatically.
- **Optional: Research Wrap-up Review** — triggers only when evidence quality genuinely needs a human call (thin/ambiguous evidence, a borderline trend candidate, a key source that couldn't be accessed, a real contradiction in the evidence). Present the honest state and the real options (dig deeper vs. accept closure) — don't steer the answer. If evidence stays thin after a follow-up loop, this can trigger again; that's normal, not a malfunction.
- **Gate 2 — Research & Insight Review** (always shown when reached, blocking). Plain-language summary of what trends were found (or why none were), with an honest confidence read per trend ("well-supported" vs. "limited evidence, treat with caution" — not raw scores or family counts).
- *(silent — AI self-checks its own proposal draft against the adversarial rubric)* Optional: **Proposal Storyline Review** triggers only on a borderline self-check result or a real strategic ambiguity.
- **Gate 3 — Final Delivery Review** (always shown when reached, blocking). The finished deliverables plus a source appendix (10 plain columns: publisher, date, type, market, content, credibility, discovery stage, link — never raw registry field names).
- **Exception-driven interaction**: anything genuinely unusual (contradictory evidence that changes a conclusion, a key source blocked, a QA failure needing judgment) surfaces immediately, in plain language, rather than waiting for the next scheduled checkpoint.

**Never expose to the user**: registry field names, evidence_family_id, MC-xx/AMEND-xx numbers, "GUARDED MODE," "PROVISIONAL," "Tier 1/2/3" as a literal label (describe source quality in plain terms instead), QA type names, or internal token names — unless they explicitly ask to go into technical/audit mode.

## Guarded mechanisms — read before relying on these paths

Two things are architecturally complete but have limited or no real-world trigger history. Treat their absence in a given run as normal, not evidence the run failed:

- **The PROVISIONAL trend / conditional-scoring path** (for a single strong evidence family with a credible-but-currently-inaccessible second family): logic fully specified in `reference/evidence_and_closure.md` §2, but has come close to triggering without actually qualifying in every real test to date. Apply its four conditions literally; don't relax them because a case "feels close."
- **Gate 2 and Gate 3's consolidated presentation** (bundling 5 and 6 underlying internal checkpoints into one user-facing moment) and the pre-delivery "does this actually read like a business document, not a research audit" self-check: GUARDED — the logic is complete and the individual underlying checks have real precedent, but the *consolidated* Gate 2/3 experience itself has not yet been exercised end-to-end in a real run. **If your run is the first to actually reach Gate 2 or Gate 3, write a short note recording what that looked like** (append to `reference/known_limitations.md` or tell the user directly) — this is how the gap eventually closes, not by forcing a topic to manufacture a trend.

See `reference/known_limitations.md` for the full history and exactly which topics/conditions have and haven't been tested.

## Reference files (load as needed, not upfront)

- `reference/registries.md` — full Source / Finding / Trend / Insight registry field schemas, Campaign Config field reference
- `reference/qa_and_gates.md` — the 20 modules in full (purpose/input/action/output/QA/gate per module), the 6 QA types, the internal Human Gate table, the state machine
- `reference/evidence_and_closure.md` — source tiering method, Independent Evidence Family rules, the PROVISIONAL path's four conditions, the six-level Campaign Specificity scale, the seven-state Research Closure model
- `reference/known_limitations.md` — what has actually been validated across 6 real test campaigns, what hasn't, and why (read this before promising a client "this will definitely find a trend")
