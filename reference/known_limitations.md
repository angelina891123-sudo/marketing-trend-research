# What's Actually Been Validated (read this before promising a client an outcome)

This skill was built and tested across 6 real campaigns before packaging. Here's the honest state of validation as of packaging (2026-09-13, Human Decision B). Update this file if a future real run changes any of this — that's the point of it.

## Validated in real use

- **The full Research → Evidence → Trend → Insight → Strategy → Delivery pipeline, end-to-end**, including a real Final Report + Proposal + Executive Deck delivery: validated by the original flagship campaign (2026 Taiwan Double 11 e-commerce trend research) — evidence was abundant in that domain and the pipeline reached full delivery.
- **Independent Evidence Family discipline, Research Closure Model (all its distinctions), the PROVISIONAL path's four conditions, contradictory-evidence classification (definition/population/temporal difference)**: validated across multiple pilots (streaming subscriptions, media-platform trend scan, AI-marketing adoption) including cases that came *close* to qualifying for the PROVISIONAL exception without actually meeting all four conditions — the mechanism held up under real pressure to relax it, not just in theory.
- **Gate 1 (Research Brief Confirmation)**: validated including a "modify, don't approve yet" path — a user changing the scope at Gate 1 is handled correctly (re-present, don't assume approval).
- **The Optional Review Points, specifically Research Wrap-up Review**: validated, including firing twice in the same campaign (first-pass rejection, then again after a follow-up research loop still came up short) and correctly treating a single human response as satisfying two different underlying internal decisions at once (not asking the same thing twice).
- **MOD-E-02 Targeted Gap Recovery**: validated as a human-gated, repeatable loop that must attack a gap from a genuinely new angle each time.
- **Plain-language user-facing presentation** (no registry field names, no internal ID/mechanism vocabulary leaking into what the user sees): validated across every gate/checkpoint actually triggered so far.

## GUARDED — logic complete, not yet triggered in real use

- **Gate 2 and Gate 3's consolidated presentation** (bundling 5 and 6 underlying internal checkpoints into a single user-facing moment): the underlying individual mechanisms have precedent (from the flagship campaign, before this consolidated presentation existed), but the *consolidated* experience itself has never actually fired in a real run. Two dedicated attempts to reach it (a short-window media-trend scan, and a 6-month AI-marketing-adoption scan chosen specifically to be evidence-rich) both legitimately closed at Research Closure before reaching it — see "A real finding, not a tooling gap" below.
- **The Audience-Fit/Business-Usability self-check** (runs just before final delivery): same status — written, never actually exercised.
- **The Trend-Score CONDITIONAL sub-classification (was the failure evidence-weak, or an access/structural limitation?)**: written, never actually exercised — every real REJECTED case so far failed the *family-count* threshold outright rather than reaching a borderline score that would need this finer classification.

**If your run is the first to genuinely reach any of these**, write a short note here (what triggered it, what it looked like, whether it worked as designed) rather than silently proceeding — that's how this list gets updated instead of staying permanently theoretical.

## A real finding, not a tooling gap: evidence availability varies enormously by topic

Two separate attempts to reach Gate 2/3 — one a 2-week cross-platform news scan, one a 6-month single-domain industry-adoption study deliberately chosen for its apparent evidence richness — both ended in honest Research Closure. In both cases, the best-fitting evidence existed but fell just outside the research window, and same-window alternatives measured a different population/construct than what was actually being asked. This is not the same failure twice — the two closures were correctly classified under different Research Closure states (`NO VALID TREND CANDIDATE` vs. `EVIDENCE GAP PERSISTS`) for principled reasons.

The practical takeaway for whoever uses this skill next: **how rich a topic's evidence base is depends heavily on the topic itself**, not on how carefully the research is run. Retail/e-commerce consumer trend research (the domain this skill was originally built for) has abundant, frequently-published, named-institution data in most markets. Narrower or faster-moving domains (a specific platform's product changes, a specific industry's tool-adoption rate) may simply not have the kind of fresh, independently-corroborated, market-specific data this skill's evidence bar requires within a short window — and a competent run of this skill on such a topic may correctly and repeatedly conclude "no trend found," which is the honest answer, not a sign the skill needs fixing.

If a user wants higher odds of a rich pipeline reaching Gate 2/3, steer them toward broader consumer/retail-behavior topics with a longer window (6+ months, ideally 1-2 years) and manage expectations explicitly for narrower or faster-moving topics.
