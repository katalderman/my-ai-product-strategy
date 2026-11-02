# Cost Curve & Pricing Strategy

## Cost Model

| Cost Category | Per-User/Month | Notes |
|--------------|----------------|-------|
| Inference (primary model) | | |
| Inference (cascading/triage) | | |
| Infrastructure | | |
| Data/storage | | |
| Human-in-the-loop | | |
| **Total AI COGS** | | |

## Cascading Strategy
<!-- Cheap model → frontier model routing logic -->

**Triage model:**
**Frontier model:**
**Routing rule:**
**Expected cascade ratio:**

## Pricing Model

**Current pricing:**
**Proposed AI pricing:**
**Model:** seat-based / usage-based / outcome-based / hybrid

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
| Inference costs 3x | | |
| Heaviest segment doubles | | |
| Model provider raises prices 50% | | |

## Board One-Pager
<!-- Before/After: Old SaaS revenue vs. AI usage revenue for your product -->

**Before (traditional SaaS):**
**After (AI-enabled):**
**Net margin shift:**
