# Evidence Rules, Trend Formation, and Research Closure

## 1. Source tiering — define fresh per topic

Never reuse another campaign's named source list. Redefine, for the actual topic:

- **Tier 1**: official/government data, the entity's own self-published material, listed-company disclosures, a platform's own newsroom/blog.
- **Tier 2**: credible named research bodies, industry associations, and trade media that directly verify a Tier-1 source (not just repeat it).
- **Tier 3**: agency/vendor blogs, unnamed commentary, promotional case studies with no independent verification.
- **Context Only**: right topic, wrong market — data with no breakout for the market actually being researched. Usable as background/comparison, never as evidence for that market's trend.

`content_nature` (editorial / sponsored / press release / official self-published / peer-reviewed) is a separate axis from tier — score them independently. A press release isn't automatically low-tier; a blog post isn't automatically Tier 3 if it's the entity's own official channel.

## 2. Independent Evidence Family — the concept that matters most

**Source count ≠ Finding count ≠ Independent Evidence Family count.** Ten articles about the same survey are one family. The question is always: *is this a genuinely separate underlying dataset, survey wave, research project, or fieldwork event* — not "how many URLs mention this."

A normal trend candidate needs **≥2 independent CORE-evidence families**. Below that, it's REJECTED — no exceptions except the PROVISIONAL path (see `qa_and_gates.md`, four conditions, all must hold, no relaxing them because a case looks close).

Practical traps to watch for (all observed in real testing):

- The same organization announcing two different things in one press release/news batch is **one family**, not two, even though they're different Finding IDs.
- A cross-platform "pattern" where each individual data point only reaches Context-Only status (e.g., two global-only announcements from two different companies) does **not** add up to a valid family, no matter how many companies are involved — Context-Only evidence cannot be the evidence base for a trend.
- Two real, in-window, Tier-1, market-specific data points can still fail to corroborate each other if they measure a genuinely different population or construct (e.g., "consumer behavior toward AI ads" vs. "employers' marketing-role AI-skill hiring demand" are related in theme but are not two measurements of the same phenomenon). Do the actual comparison — population, definition, metric, question wording, collection period — before deciding two findings corroborate each other. Don't assume corroboration just because both mention "AI" and "marketing."

## 3. Campaign Specificity — six levels, redefine the content per topic

The framework is fixed; what qualifies for each level is not — write fresh definitions in the Research Brief for every new campaign.

1. **CAMPAIGN-SPECIFIC** — squarely about the exact thing being researched, in the exact market and window.
2. **SEASONAL CONTEXT** — tied to a recurring calendar event/season relevant to the campaign (not applicable to every campaign type — say so if it doesn't apply rather than forcing something into this slot).
3. **ANNUAL MARKET SIGNAL** — a recurring, non-campaign-specific data point (e.g., an annual industry survey) with a fresh update inside the window.
4. **BROADER MARKET TREND** — relevant background across the space but not specific to the exact question.
5. **BROADER TECHNOLOGY TREND** — cross-industry technology context.
6. **STRUCTURAL BACKGROUND** — established structural facts about the market. **Can support explanation/context but can never, by itself or in combination with more of the same, stand as trend evidence** — and don't let evidence "demoted" here as an escape hatch when it fails trend scoring on its own merits.

## 4. Research Closure — seven legitimate outcomes

Closure is a real, valid, and often correct outcome — not a failure state. Six of the seven states below are explicitly non-failure and must never be reported to a user as if the process broke.

| State | Roughly means | When to use it |
|---|---|---|
| **SUCCESS** | Found what was asked, cleanly | Full pipeline proceeds normally |
| **PARTIAL** | Found something real but not the full scope asked for | Proceeds to Insight for what was found; the gap is documented honestly |
| **NO VALID TREND CANDIDATE** | Clustering was attempted, evidence-family thresholds weren't met, and **no gap-recovery loop was attempted** (or none was warranted) | First-pass rejection without a prior E-02 loop |
| **EVIDENCE GAP PERSISTS** | Same symptom as above, but a targeted gap-recovery loop (MOD-E-02) *was* run and the gap remained | Use this instead of NO VALID TREND CANDIDATE once you've actually tried and failed to close the gap — the distinction matters for anyone reading the closure record later |
| **INSUFFICIENT PUBLIC EVIDENCE** | The topic genuinely has little to no traceable public evidence at all (not "exists but doesn't cluster" — actually sparse) | Distinguish this from the two states above: this is about evidence *existing*, not about it *qualifying* |
| **RESEARCH QUESTION NOT ANSWERABLE** | The question as posed can't be resolved with available public evidence regardless of effort (e.g., requires private/proprietary data) | Different from a data gap — this is a framing problem, flag it back to whoever set the research question |
| **SOURCE ACCESS LIMITATION** | A specific, identifiable source is blocked at the domain/publisher level (confirmed via ≥3 access attempts), and that blockage is the actual bottleneck | Distinguish from generic thinness — this state points at a fixable-in-principle technical problem, not an evidence-doesn't-exist problem |

**Never skip straight to closure without running MOD-T-04's Open Gap Discovery Report first** — a final scan for any overlooked cluster (≥2 findings, ≥2 independent sources, real distinctiveness, real marketing significance) that might have been missed. Only after that scan comes back empty is closure actually justified.

**When presenting closure to a user**: state plainly what was found, why it doesn't (yet) support a trend, and give them a real choice — dig deeper with a new angle, or accept closure — without steering the answer toward "keep going" just to produce something. A well-documented closure, correctly classified, is a complete and useful deliverable on its own.
