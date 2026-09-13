# Registry Reference

Six registries. Canonical ones (Source, Finding, Trend, Insight, Decision/Human Gate) are the source of truth — derived artifacts (Report/Proposal/Deck) never write back to them. Keep these as actual tracked records (files, or a structured note) for any non-trivial campaign, not just in your head — the discipline below only works if the records are real and checkable.

## Campaign Config fields (collected at intake)

| Field | Required? | Notes |
|---|---|---|
| `campaign_name` | Required | |
| `business_context` | Required | Who this is for and why |
| `primary_market` / `secondary_market` | Required / Optional | Secondary is background-only, not actively researched unless specified |
| `research_objective` | Required | The core business question, plus the expected trend-count range |
| `research_window` | Required | Primary window + narrow exception rule for "old thing, genuinely new development" — never used to relabel stale news as fresh |
| `research_dimensions` | Required | The specific angles/topics to cover |
| `research_questions` | Required | Concrete questions the research must answer |
| `campaign_specificity_definition` | Required (system default available) | Six-level framework — reuse the *framework*, redefine the *content* per topic |
| `source_priority` | Required | Tier 1/2/3 definitions, redefined per topic — never copy another campaign's named source list |
| `inclusion_criteria` / `exclusion_criteria` | Required | |
| `expected_trend_count` | Required | A range; 0 must be an explicitly valid value |
| `final_audience` | Required | Who reads the output |
| `required_deliverables` | Required | Report / Proposal / Deck, any combination; Proposal/Deck are conditional on there being a real trend to build them from |
| `trend_scoring_thresholds` | Optional (system default) | Default: Total≥70 / Evidence Strength≥14 / Market Relevance≥14 / ≥2 CORE findings / ≥2 independent evidence families |
| `media_product_boundary` | Fixed, not configurable | Never recommend specific media tools/placements |
| `language` | Required | |

## 1. Source Registry

Records where a piece of evidence came from and how much to trust it.

- **Required**: Source ID, name, publisher, publish date, content type, market, original URL, source tier, scope status, five-dimension quality score, canonical label, `content_nature` (EDITORIAL / SPONSORED / PRESS_RELEASE / OFFICIAL_SELF_PUBLISHED / PEER_REVIEWED — independent of source tier, don't conflate them), `publisher_accessibility_status` (FULLY_ACCESSIBLE / PARTIALLY_ACCESSIBLE / SYSTEMICALLY_BLOCKED / UNKNOWN — a domain-level blockage goes into a persistent cross-campaign log, see "Accessibility" below).
- **Optional**: `cited_original_source` (if this is a secondhand report, name what it's reporting on), `known_discrepancy` (an unresolved number/fact conflict with another source — record it, don't quietly rationalize it away).
- **Rules**: one record per real underlying source (don't create a new ID just because it's cited again); a source's tier is judged by the actual document you obtained, not inherited from the reputation of whoever it's citing; `SPONSORED`/`PRESS_RELEASE` content_nature does not automatically mean low tier — score the two dimensions independently.
- **Accessibility protocol**: before declaring a domain/publisher SYSTEMICALLY_BLOCKED, try ≥3 independent access paths (different URL forms, cached/archived versions, a second outlet quoting the same primary content) — don't downgrade to "inaccessible" after one failed fetch. If you do confirm systemic blocking, record it somewhere durable (a project-level file, not buried in one campaign's folder) so future campaigns don't waste time rediscovering it.

## 2. Finding Registry

One independent evidentiary claim per record.

- **Required**: Finding ID, the statement itself, which research dimension it addresses, Source ID, market, the actual evidence/statistic, claim strength (A/B/C), evidence role (CORE / SUPPORTING / CONTEXT ONLY / EXCLUDE), verification status, the fetch-verification trail, `campaign_specificity` (the six-level classification — never leave blank), first-discovered phase (write once, never overwrite), and **`evidence_family_id`** (see "Independent Evidence Family" in `evidence_and_closure.md` — this is the single most important field to get right).
- **Optional**: `relationship_to_other_findings` — DEFINITION_DIFFERENCE / TRUE_CONTRADICTION / POPULATION_DIFFERENCE / TEMPORAL_DIFFERENCE / NON_COMPARABLE_SIGNAL. Only fill this in after actually checking population, definition, metric, question wording, and collection period — never mark it from a gut feeling, and never "resolve" a contradiction by picking a side.
- **Rules**: global/out-of-region evidence with no local corroboration caps at CONTEXT ONLY, full stop. Evidence Role labels come only from this fixed vocabulary — never invent an in-between tier.

## 3. Trend Registry

- **Required**: Trend ID, name, narrative role (CORE MARKET TENSION / BUSINESS TENSION / ENABLING TREND / MARKET CONTEXT), supporting Finding IDs grouped by evidence role, five-dimension trend score, current confidence, status, **Independent Evidence Family Count** (deduplicated by `evidence_family_id` across supporting findings — this must be ≥2 for a normal CANDIDATE/QUALIFIED trend).
- **Status values**: CANDIDATE / QUALIFIED / MERGED / REJECTED / **PROVISIONAL** (single-family, documented access limitation — rare, gated, capped at CONDITIONAL score, see `evidence_and_closure.md` §2) / FINAL / EMERGING_SIGNAL / ABANDONED.
- **Rules**: a merge must update the merged-away trend's status AND the surviving trend's evidence base in the same step, never as two separate edits; thresholds don't flex because a campaign "needs" a trend; a single evidence family can never directly qualify a trend — PROVISIONAL is the only narrow exception, and even then the score ceiling is CONDITIONAL, never QUALIFIED.

## 4. Insight Registry

Structured record of every Trend/Market Tension/Enabling Trend/Decision Insight — not a free-form narrative doc.

- **Required**: Insight ID, artifact type (TREND / MARKET TENSION / ENABLING TREND / DECISION INSIGHT), the schema fields that type requires, a fact/inference tag on every claim, insight confidence, marketing-implication confidence.
- **Rules**: must trace to at least one real Trend ID or Finding ID — never conjured from nothing. Never write correlation as causation. Never "downgrade" a research unit to Decision-Insight/STRUCTURAL-BACKGROUND status just because it failed Trend scoring — that's using the escape hatch to dodge the threshold, which defeats the point of having one.

## 5. Decision / Human Gate Registry

Every gate request, what the AI recommended, what the human decided, and the approval token.

- **Rule that matters most**: an approval token can only be produced by an actual human response — the AI never generates one for itself, and no module can mark itself COMPLETED without the token its gate requires.
- Decisions are append-only history, not overwritten — you always have the full decision trail.

## 6. Artifact Registry

Version-tracks every rendered deliverable against a snapshot of the four canonical registries at render time.

- If any upstream registry has moved since a deliverable was rendered, that deliverable is `is_stale` — check this before calling anything "final." A `superseded` artifact (explicitly replaced by a newer version after human review) is a separate flag from staleness and also blocks a DELIVERED status.
