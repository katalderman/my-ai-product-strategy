# Three-Horizon Roadmap & Board Pitch

## Roadmap

Timeframes compressed per M6: H1 = 0-4 weeks, H2 = 1-3 months, H3 = 3-6 months (one frontier cycle each, not the template's quarterly windows).

### Horizon 1 - Now (0-4 weeks)

Quick wins. Ship with existing capabilities.

| Initiative | Component | Metric | Confidence |
|-----------|-----------|--------|------------|
| Correction capture (accept/edit/reject) on every AI proposal | Moat | 100% of proposals logged; first weekly gold-set audit runs | H |
| Golden dataset to 25 rows incl. red-team adversarial cases, wired to a CI eval gate | Contract | Eval gate catches 100% of seeded regressions pre-deploy | H |
| Confidence UX v1: three tiers, evidence panel, receipts, one-click undo | Contract | 0 sub-50% outputs reach the deploy path in beta | H |
| Onboard 5 design-partner workspaces with live CMS + hosting | Bet | 5 signed, 3 wired to real production | M |

### Horizon 2 - Next (1-3 months)

Bets. Every row has a kill criteria (a number, a date, and a verb).

| Initiative | Component | Metric | Kill Criteria | Confidence |
|-----------|-----------|--------|---------------|------------|
| Production agent runs with metered credits | Margin | 60%+ of partner workspaces run 1+ agent run/week at 92%+ golden accuracy | If <3 of 5 partners route a production deploy through agent runs by week 10, stop metering and rebuild as a draft-only copilot | M |
| Hybrid pricing live ($45 seat + $1.50/run beyond 10 included) | Margin | Implied revenue $52.50+/user; agent-run margin 70%+ at 80/20 cascade | If credits attach to <10% of seats by month 3, fold agent runs into a $60 seat and re-test | M |
| Official Zapier/Make integration for CMS content sync | Guardrails | 20%+ of workspaces install; listed in both directories | If <5% install by month 3, deprioritize to a docs recipe | M |
| Correction loop v2: weekly promotion of repetitive corrections into workspace context | Moat | Repeat-correction rate falls 30% in 8 weeks | If repeat-correction rate is flat after 8 weeks, corrections are not signal; re-scope what we capture | M |

### Horizon 3 - Bet (3-6 months)

Moonshots. High uncertainty, high potential.

| Initiative | Component | Metric | Confidence |
|-----------|-----------|--------|------------|
| Anonymized cross-workspace mapping intelligence (opt-in) | Moat | New-workspace time-to-first-deploy down 50% for the opt-in cohort | L |
| Governance pack as GTM: model cards, screen-shareable eval dashboard, policy one-pager | Guardrails | In 100% of sales conversations; 2 mid-market deals cite it | L |

**Mapping notes:** all 12 backlog initiatives map to a strategy component (1 Bet, 3 Moat, 2 Margin, 3 Contract, 3 Guardrails), none unmapped.
## AI Bet Evaluation (six lenses)

- **Bet Validation:** strongest evidence is the $55/user/month adjacent spend and the shadow-AI workarounds; weakest is zero live customers, so demand is inferred, not observed. Verdict: fund with gates.
- **Defensibility:** the context graph plus scoped correction loop is credible but currently architecture, not data (flywheel 7/20). H1 exists to make it real before the incumbents close the wedge.
- **Pricing Alignment:** economics hold only with routing discipline (71% margin at 80/20 vs 42.2% uncascaded); the cascade ratio is a standing operational dependency, monitored per tier.
- **Trust & Reliability:** the contract is explicit and measurable; open gaps are the partner red-team session and fairness/bias testing (the maturity scorer's weakest dimension at 1/5).
- **Impact & Scale:** governance is strong for stage; the Network loop is deliberately missing (workspace isolation is the privacy promise), which caps compounding until the opt-in aggregation layer in H3.
- **Capability Gaps:** 2 engineers plus a founder-PM must ship the correction store, eval CI, agent runs, and one integration in 12 months; scope risk is real and bounded by the H2 kill criteria.
- **Weakest sentence, rewritten:** "The AI context layer is our differentiator" became "Our differentiator is the correction loop scoped to each workspace's design-to-deploy graph, instrumented before the first customer; the context layer alone is an architecture claim, not a moat."
## Board Pitch

**Thesis (1 sentence):** Shipframe turns a design file into running production (CMS, content, and deploys included) for small SaaS teams with no front-end developer, and every correction a team makes teaches its workspace.

**The case:**

- **Why now:** Generation went commodity (v0, Figma Make), which killed "design-to-code" as a moat but created the opening: prospects now duct-tape ChatGPT, v0, and Zapier around their design tool at ~$55/user/month, and nobody owns the design-to-CMS-to-deploy graph those tools lose between steps. Figma, Framer, and Vercel have each validated the wedge publicly, but each attacks from one side only.
- **What's defensible:** Not generation. The per-workspace context graph (design wired to the live content model and deploy history) plus a correction loop scoped to it, signal Figma and Vercel structurally cannot see. Vendor-portable by design: multi-model routing, eval-gated model swaps, kill switch audited Ready.
- **The economics:** $45 seat plus $1.50 per production agent run beyond 10 included. $52.50 implied revenue per user against $5.04 AI COGS at 80/20 routing, 71% gross margin. Stress-tested: a 3x inference shock holds at 48.6% because routing, not pricing, absorbs it, and the heaviest 20-25% of users fund their own agent runs.

**The risks:**

- **Trust / failure modes:** A fabricated schema binding is our Air Canada: it ships broken production code. The contract: 92% golden-set accuracy, <1% fabricated bindings with auto-rollback at >2%, and sub-50% confidence output cannot reach production, structurally.
- **Scale / governance:** Agents touch production, so deploys and schema migrations are never auto at any confidence; tool calls are allow-listed, rate-limited, and logged; workspaces are isolated; EU AI Act limited risk, GDPR with zero-retention agreements across every routed provider.
- **Competitive:** Our wedge is the incumbents' published roadmap and our flywheel is honestly 7/20 today. H1 exists to make the correction loop real before scale; if the H2 kill criteria fire, we stop before the spend compounds.

**The ask:** $900K over 12 months: $550K engineering (2 senior FTE), $250K inference plus eval/HITL tooling, $100K design-partner GTM. Team: 2 engineers plus me as PM. Hard review at month 6 against the H2 kill criteria: if production agent runs haven't reached 60% weekly usage across design partners, we stop the agent bet and refocus on the copilot canvas.

**Coaching notes (audience: CEO + leadership team):**

- Opening line: "Our prospects already pay $55 a month per user to duct-tape three AI tools around their design tool. I'm asking for $900K to replace that duct tape with the product, with kill criteria that stop us at month 6 if I'm wrong."
- 60-second version: thesis, the $55 adjacent-spend proof, 71% margin at 80/20 routing, the correction-loop moat plan, $900K with a month-6 gate.
- Hardest question: "What are we giving up to fund this?" Answer: two senior engineers off the core roadmap for 12 months; the month-6 gate caps the downside at half the ask, and the eval and routing infrastructure is reusable by every other AI initiative even if Shipframe stops.

## M1 Baseline vs. Now

Your 3-sentence AI strategy from Module 1 vs. what you'd say now:

**M1 baseline:** Shipframe is an AI design copilot product intended for a product designer at a small SaaS team who also owns the marketing site, working without a dedicated front-end developer. The AI generates production-ready page layouts from the team's real CMS content model and existing component library, not from a blank canvas.

**Now:** We're betting on Shipframe: AI design-to-production for small SaaS teams without front-end developers, because generation went commodity while the design-to-CMS-to-deploy graph did not. The moat is each workspace's context graph plus a correction loop scoped to it (7/20 today; H1 makes it real), priced as a $45 seat plus metered agent runs at 71% gross margin behind a multi-model kill switch. It ships with a reliability contract (92% golden accuracy, auto-rollback on fabricated bindings), tiered-confidence UX, and governance we can show in procurement. Live in the repo.
