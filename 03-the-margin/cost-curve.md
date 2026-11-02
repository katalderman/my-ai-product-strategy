# Cost Curve & Pricing Strategy

## Cost Model

Inputs from the Margin Calculator: 1,000 AI requests per user per month, $0.018 blended cost per request before routing, $45 revenue per user per month.

| Cost Category | Per-User/Month | Notes |
|--------------|----------------|-------|
| Inference (primary model) | $3.60 | 20% of requests on frontier models (agent runs, context-heavy generation) at $0.018/request |
| Inference (cascading/triage) | $1.44 | 80% of requests on cheap models (filler suggestions, classification, embeddings) at ~$0.0018/request |
| Infrastructure | $5.00 | We host customer production sites: CDN, builds, deploy pipeline |
| Data/storage | $2.00 | Design files, per-workspace context graph, embedding store (embeddings get called more than you think) |
| Human-in-the-loop | $1.00 | Eval review and agent-run QA sampling |
| **Total AI COGS** | **$5.04** | At 80/20 routing. Uncascaded it is $18.00. Total COGS including non-AI rows: $13.04, which is a 71.0% gross margin at $45/user |

## Cascading Strategy
<!-- Cheap model → frontier model routing logic -->

**Triage model:** Small/cheap tier (Haiku or GPT-mini class) behind the existing multi-model router.
**Frontier model:** Opus or GPT-5 class, reserved for agent runs and context-heavy generation.
**Routing rule:** Filler always runs cheap (naming, design lint, schema suggestions, alt text). Context-graph generation starts cheap and escalates to frontier only when the eval harness scores the task above a complexity threshold or the user retries. Agent runs plan on frontier and execute sub-steps on cheap models. Embeddings are pinned to the cheapest embedding model and cached.
**Expected cascade ratio:** 80% cheap / 20% frontier

## Pricing Model

**Current pricing:** $45/seat/month flat (launch hypothesis: positioned against Figma's org tier, justified by bundling canvas plus CMS plus hosting)
**Proposed AI pricing:** Strategy posture: Penetrate (win share against Figma pre-adoption, optimize costs relentlessly). Structure: $45/seat base plus $1.50 per production agent run (a page or flow generated and shipped to production) beyond 10 included per seat per month. Implied revenue per user: $52.50/month at an estimated 5 billable runs per user blended across the base.
**Model:** hybrid (seat base + metered agent runs)

## Packaging Decision: Leader / Filler / Killer

**Leader (what they come for):** The context-aware canvas: the design surface where AI reads the workspace's design-to-CMS-to-deploy graph, so every edit and generation respects the live content model. This is the core intelligence and the whole wedge; it is bundled into every seat because without it we are just another canvas.

**Filler (bumps perceived value, cheap to serve):** Lightweight suggestions on the triage model: component and layer naming, design lint and accessibility checks, CMS schema field suggestions, alt text and microcopy. Pennies per call, touched by nearly everyone, bundled without metering.

**Killer (heavy inference, too spiky to bundle):** Agent workflows: generate a full page or flow from a prompt, build the CMS schema from a finished design, run a design-to-production migration, batch asset generation. Long multi-model runs on frontier models; cost per run is orders of magnitude above a suggestion call.

**% of users touching the Killer:** ~20-25% (hypothesis, zero customers). Power users and dev-leaning teams trigger agent runs; most designers consume the output of someone else's run.

**Bundle or add-on:** Add-on. Under the 70% rule this is not close: metered agent credits on top of the seat price, with a small included allowance so every user experiences at least one agent run. Bundling it would mean the heaviest 20% of users burning frontier tokens subsidized by everyone else's subscriptions.

**Revisit trigger:** Instrument agent-run usage from day one (same telemetry build as the correction loop). If real usage crosses 70% of weekly actives, fold it into the base plan and raise the seat price instead.

## Stress Tests

| Scenario | Impact on Margin | Response |
|----------|-----------------|----------|
| Inference costs 3x | 42.2% drops to -37.8% with no routing; stays at 48.6% at an 80% cascade | Cascading is the shock absorber, not pricing. Raise the cascade ratio, lean on caching and prompt optimization, flip router weights to the next-best model per the kill switch audit |
| Heaviest segment doubles | 2.2% uncascaded; 59.8% at an 80% cascade | Metered agent credits mean heavy users fund their own usage; the bundle only carries filler, which costs pennies |
| Model provider raises prices 50% | ~22% uncascaded; ~65% at an 80% cascade (derived from calculator inputs) | Multi-model router shifts traffic to the next-best model inside 48 hours; the eval harness quantifies the quality delta before the flip |

## Board One-Pager
<!-- Before/After: Old SaaS revenue vs. AI usage revenue for your product -->

**Before (traditional SaaS):** $45/seat, $8.00 COGS, 82.2% gross margin, $37.00 gross profit per user. Classic canvas economics, but nothing Figma can't match, and no AI differentiation.
**After (AI-enabled):** $52.50 blended revenue per user (hybrid: seat plus metered agent runs), $13.04 total COGS at 80/20 routing, 75.2% gross margin, $39.46 gross profit per user.
**Net margin shift:** Minus 7 points of margin percentage, plus $2.46 gross profit per user, and revenue now scales with work delivered: the heaviest 20-25% of users pay for their agent runs instead of being subsidized by everyone else. Under a 3x cost shock we stay profitable (48.6%) because routing absorbs the spike. Lower margin percentage, higher gross profit, survivable stress tests: that is the trade we are asking the board to approve.
