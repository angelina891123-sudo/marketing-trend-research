# QA Types, Internal Human Gates, and State Machine

This is the Layer 1 (internal) detail behind the Gate 1/2/3 + 2 Optional Review Points the user actually sees (see SKILL.md). Keep this bookkeeping even though the user doesn't see the labels.

## The 20 modules, by layer

**Governance/Control** (run continuously, not sequential steps): Human Gate Controller (records real approvals only — never fabricate a token), Dependency/Consistency Checker (propagates staleness when upstream data changes), Cross-Artifact Consistency Checker.

**Research**: MOD-R-01 Research Brief (defines scope/window/dimensions/trend-count target; gated) → MOD-R-02 Evidence Discovery (broad WebSearch/WebFetch against the brief; not gated, but every concrete number needs a fetch-verification trail or it's UNVERIFIED and can't proceed).

**Evidence**: MOD-E-01 Evidence Validation & Scoring (five-dimension score, claim strength, Campaign Specificity, CORE/SUPPORTING/CONTEXT/EXCLUDE; not gated) → MOD-E-02 Targeted Gap Recovery (a bounded, repeatable research loop for a specific identified gap; **is** gated — a human decides whether to open a new loop; each loop must attack the gap from a genuinely new angle, never repeat a failed strategy).

**Trend**: MOD-T-01 Trend Candidate Clustering (group findings by shared underlying change; compute Independent Evidence Family Count; not gated *unless* the result is PROVISIONAL, see below) → MOD-T-02 Trend Scoring Gate (five-dimension score + qualification; gated on CONDITIONAL/borderline/all-PROVISIONAL results) → MOD-T-03 Trend Merge (resolve overlapping candidates; gated — merge reasoning needs a human nod, and the merge/evidence-base update happens atomically) → MOD-T-04 Open Gap Discovery (final pre-closure check: scan for any overlooked opportunity cluster meeting the Opportunity Gate — ≥2 findings, ≥2 independent sources, real distinctiveness, real marketing significance).

**Insight**: MOD-I-01 Insight Generation → MOD-I-02 Quality Gate → MOD-I-03 Acceptance (gated: accept / rewrite / abandon).

**Strategy**: MOD-S-01 Strategy Translation (proposal draft) → MOD-S-02 Human Review (an adversarial rubric, self-checked by the AI first; gated on a borderline self-check score or real strategic ambiguity) → MOD-S-03 Revision.

**Delivery**: MOD-D-01–D-05 (Report / Rendering / Deck / Cross-Artifact Consistency — automated QA, only escalates to a human on failure) → MOD-D-06 Final Delivery Readiness Check (includes the Audience-Fit self-check, see QA types below) → gated final approval.

## The 6 QA types

| Type | Runs when | Checks | Blocks next stage? | Needs a human? |
|---|---|---|---|---|
| **Local QA** | Every module finishes | Evidence traceability, schema completeness, text density, visual overflow — single-object checks | Yes | No (unless 3 straight retries fail) |
| **Cross-Artifact QA** | Insight complete; Report/Deck complete | Do trends in the same batch use consistent schema depth/order? | Yes | No (mechanical comparison) |
| **Dependency QA** | Any canonical write; pre-delivery | Merge integrity, registry consistency, "lost insight" check (did a merge silently drop a high-value finding?) | Yes | Yes, if it changes a qualification/confidence result |
| **Semantic QA** | Strategy draft; Report/Deck draft | Fact vs. inference boundary; is a Campaign-Specificity claim honest?; did a specific media-tool name leak into a *recommendation* context?; is a known limitation still visible or did formatting quietly drop it? | Yes | **Yes, always** — flags NEEDS_REVIEW rather than auto-failing (keyword scanning alone has too many false positives here) |
| **Delivery QA** | Rendering; Deck render | Actual visual overflow/clipping, source-ID completeness, no duplicate page roles, version consistency across Report/Proposal/Deck | Yes | Yes (final visual check can't be 100% automated) |
| **Audience Fit / Business Usability QA** (GUARDED) | Just before final delivery approval, as an AI self-check | Is there a clear, decision-ready statement a business reader can act on? Can the key insight be grasped within the first few paragraphs? Could a reader mistake governance/traceability detail for the actual conclusion? | Yes | Yes — **GUARDED: logic complete, not yet triggered in a real run as of this writing.** If your run is the first to genuinely reach this check, note what happened. |

## Internal Human Gates (8 total — these get bundled into the user-facing Gate 1/2/3 per SKILL.md, but each is tracked individually underneath)

None of these can be skipped without a real approval token — "no approval, no continue" applies to all eight, no exceptions.

| Gate | Fires when | Decision | If approved | If rejected |
|---|---|---|---|---|
| Research Closure Gate | Pre-closure check (MOD-T-04) done | Accept closure (with a specific closure-state classification) / reopen a loop | Proceeds to Insight, or closes the pipeline entirely if the closure state is terminal | Opens MOD-E-02 |
| **PROVISIONAL Gate** | T-01 produces a PROVISIONAL candidate | Approve into scoring / reject / request more recovery attempts | Enters scoring capped at CONDITIONAL | Stays REJECTED, falls through to the Closure Gate |
| Trend Merge Gate | Overlap detected | Approve merge / don't | Both trends' evidence bases sync atomically | Both candidates go back to scoring |
| Core Trend Selection Gate | Post-closure | Accept the trend count found / keep researching | Proceeds to Insight | Opens a new research loop |
| Insight Acceptance Gate | Insight quality-gated | Accept / rewrite / abandon | Proceeds to acceptance | Routes back to gap-research or insight generation depending on severity |
| Campaign Relevance Gate | Before insight generation, once specificity stats exist | Accept the campaign-specific evidence ratio / demand more | Insight generation proceeds with honest labeling | Opens a loop focused specifically on campaign-exclusive evidence |
| Proposal Storyline Gate | Strategy self-review done | Accept / require major revision | Proceeds to rendering | Proceeds to revision |
| Final Delivery Gate | Delivery QA passed | Approve delivery / require fixes | Campaign closes, artifact marked delivered | Returns to the specific delivery module that needs fixing |

## The PROVISIONAL path — four conditions, all must hold

A candidate with only one evidence family is normally a hard REJECT. There's exactly one narrow exception: **all four** of these must be true simultaneously (not "mostly true," not "close enough") —

1. Exactly one family has CORE-level evidence, and that family shows a consistent direction across ≥2 time points (not a single snapshot).
2. A second, *named* candidate family exists that would be raw evidence data (not structural background) if accessible — but it's currently capped at CONTEXT ONLY specifically because of a **documented accessibility failure**, not because it's out of the research window and not because it duplicates family one.
3. You've actually exhausted ≥3 independent access attempts on that second family per the accessibility protocol, with a record of each attempt.
4. Formal Finding-relationship analysis has **not** already classified that second family as measuring a different population/construct/definition than family one. (If it has — if they're genuinely not comparable — this path is closed, full stop, no matter how promising conditions 1–3 look.)

If all four hold, the candidate becomes PROVISIONAL, requires its own gate approval, and — even if approved — its trend score can never exceed CONDITIONAL. This has come close to triggering in real testing (conditions 1–2 satisfied) but has not yet actually qualified in any real run to date (condition 4 or 3 has failed each time). Don't relax any of the four because a case "feels close" — that pressure is exactly when the check matters most.

## State machine

Ten states: `NOT_STARTED → IN_PROGRESS → QA_PENDING → (HUMAN_REVIEW_REQUIRED → APPROVED | REJECTED) → COMPLETED`, plus `REWORK_REQUIRED` (QA failed, redo), `BLOCKED` (can't even start — missing an upstream dependency or approval token, distinct from having a broken output), and `STALE` (was COMPLETED, but upstream data changed since).

A module can never mark itself COMPLETED without the approval token its gate requires — attempting to is a hard architecture violation, not an ordinary QA failure, and should stop everything and surface to the user immediately.
