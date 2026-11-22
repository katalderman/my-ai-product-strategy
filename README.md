# Shipframe: Living AI Product Strategy

> Shipframe is an AI design-to-production platform (canvas + native CMS + hosting + AI context layer) for product designers at small SaaS teams who also own the marketing site and work without a dedicated front-end developer. A design file becomes running production, and every correction a team makes teaches its workspace.

---

## Strategy at a Glance

| Component | Module | Status | Key Artifact |
|-----------|--------|--------|-------------|
| **The Bet** | M1 | [x] | `01-the-bet/` |
| **The Moat** | M2 | [x] | `02-the-moat/` |
| **The Margin** | M3 | [x] | `03-the-margin/` |
| **The Contract** | M4 | [x] | `04-the-contract/` |
| **The Guardrails** | M5 | [x] | `05-the-guardrails/` |
| **The Pitch** | M6 | [x] | `06-the-pitch/` |

---

## The Bet (M1)

**What we're building, for whom, why now.**

- **Product:** Shipframe: integrated design platform (Figma competitor with native backend, CMS, and hosting integration plus built-in AI context)
- **AI Value Archetype:** Creator + Orchestrator (generation on the canvas; agent runs that ship to production)
- **Vulnerability Scores:** Moat 3/5 · Data 2/5 · Platform 2/5
- **Top Risk:** Our core wedge (design-to-production integration) is not a gap in the market, it is the published roadmap of Figma, Framer, and Vercel; the AI context layer is our only differentiator and it needs customer scale we don't have yet.
- **Confidence:** M (high on platform exposure, medium on moat: switching-cost-after-adoption is unproven with zero customers)
- **Prototype:** https://lovable.dev/preview/IiAdpP90alpst9BL3fVTsinJlqAPaR19
- **Kill Criteria:** If <3 of 5 design partners route a production deploy through agent runs by week 10 of H2, stop the agent bet and rebuild as a draft-only copilot.

→ Details: [`01-the-bet/`](01-the-bet/)

---

## The Moat (M2)

**Why this won't get copied in 6 months.**

- **Data Flywheel Score:** 7/20 ("No flywheel. Data goes in and gets thrown away.")
- **Weakest Loop:** Correction and Network, tied at 1/5
- **Top Encroachment Threat:** Figma (Dev Mode, Make, and Sites: building our wedge from the position of already owning the designers)
- **Encroachment Defense:** Instrument the Correction loop now, scoped to the per-workspace design-to-CMS-to-deploy context graph that Figma and Vercel structurally cannot see, so corrections feed our Domain Context loop instead of a symmetric data race Figma wins on volume.
- **Vendor Portability:** Ready (multi-model router, eval-gated swaps, zero-retention agreements with every routed provider)

→ Details: [`02-the-moat/`](02-the-moat/)
---

## The Margin (M3)

**Will this make money or bleed it?**

- **Gross Margin (current):** 42.2% uncascaded (caution zone)
- **Gross Margin (AI-adjusted):** 71.0% at 80/20 routing; 75.2% blended under hybrid pricing
- **Pricing Model:** hybrid (seat base + metered agent runs)
- **Pricing Today → Tomorrow:** $45/seat/month flat → $45 base plus $1.50 per production agent run beyond 10 included per seat. Implied revenue $52.50/user/month. Posture: Penetrate.
- **Total AI COGS / unit:** $5.04/user/month at 80/20 cascade ($18.00 uncascaded; total COGS $13.04)
- **Cascading Strategy:** Triage tier (Haiku / GPT-mini class) for filler; frontier (Opus / GPT-5 class) reserved for agent runs and context-heavy generation; 80% cheap / 20% frontier behind the existing router
- **Net Margin Shift:** Minus 7 points of margin percentage vs. plain SaaS, plus $2.46 gross profit per user, and revenue scales with work delivered: the heaviest 20-25% of users pay for their own agent runs. A 3x inference shock holds at 48.6% with routing; dies at -37.8% without.
- **Break-even at:** every seat is gross-profitable from day one ($13.04 COGS vs. $45 seat); the gate is agent-run credit attach, not volume
- **Packaging:** Leader = context-aware canvas (bundled) · Filler = triage-tier suggestions (bundled) · Killer = agent runs (metered add-on; ~20-25% of users, under the 70% rule)

→ Details: [`03-the-margin/`](03-the-margin/)

---

## The Contract (M4)

**Why users will trust a probabilistic system.**

- **Reliability Target:** 92% on the golden set, weekly LLM-as-Judge + rule-based schema validation; <1% fabricated bindings with auto-rollback at >2%; p95 <800ms suggestions / <30s agent runs; drift <0.5% per 4 weeks
- **Golden Dataset:** 10 rows (25 by H1 exit), 4 adversarial: prompt injection via canvas text layers, review-gate bypass, script injection through CMS data, hallucinated schema binding (our Air Canada case)
- **Confidence UX:** Tiered: >90% auto-apply with receipts and undo; 50-90% renders as a proposal with an evidence panel and the alternative mapping; <50% blocked from the deploy path and routed to review
- **HITL Architecture:** Triggers: confidence <50%, any safety/injection flag, anything touching a production deploy in a reviewed workspace. Corrections feed the weekly gold-set audit and the M2 correction loop; HITL share tracked as a shrinking queue.
- **Failure Mode Coverage:** 4 adversarial classes covered; partner red-team pending, candidates staged (multilingual content, concurrent edits mid-run, bulk deletions, token conflicts, provider timeout mid-deploy)

→ Details: [`04-the-contract/`](04-the-contract/)
---

## The Guardrails (M5)

**What breaks when this scales, and what compounds.**

- **Compounding System:** honest status 0 active / 1 broken / 2 missing. Recursive Learning missing (correction store ships as a launch blocker), Cross-Domain Transfer broken (the context graph compounds within a workspace but nothing learns from usage yet), Network Intelligence missing by design (workspace isolation). Freeze-test verdict: scaling, not compounding, until the correction loop ships.
- **Governance Posture:** one-page policy covering canvas generation, schema mapping, and production agent runs. Maturity: 13/25 (Developing); weakest dimension Fairness.
- **Autonomy Boundaries:** filler and >90%-confidence canvas edits auto-apply with undo; production deploys and schema migrations need human approval at any confidence; bulk deletion and cross-workspace access never auto.
- **Escalation Triggers:** confidence <50%; safety/injection flags; anything touching deploys or migrations; 3 rejected proposals; reviewed workspaces route every agent run to the queue.
- **Audit Cadence:** real-time tool-call log (eng on-call) · weekly eval vs. golden set (PM: Kat) · monthly human review of 50 runs + all escalations, quarterly policy review (founder + security counsel)
- **Shadow AI Audit (user-side):** 5 workarounds: 3 build / 1 partner / 1 ignore; ~$55/user/month adjacent spend on ChatGPT + v0 + Zapier; dominant signal: capability gap
- **Agent Boundaries:** design-to-production agent CAN generate pages/flows, draft migrations, prepare deploy previews; CANNOT execute deploys, run migrations, bulk-delete, or read outside its workspace. Allow-listed, rate-limited, fully logged; per-workspace memory only.
- **Regulatory Exposure:** EU AI Act limited risk; GDPR with data minimization and zero-retention DPAs across the routing list; SOC 2 roadmap before enterprise deals

→ Details: [`05-the-guardrails/`](05-the-guardrails/)

---

## The Pitch (M6)

**How this gets funded, shipped, and adopted.**

- **Horizon 1 (Now, 0-4 weeks):** correction capture on every proposal · golden set to 25 rows + CI eval gate · confidence UX v1 · 5 design-partner workspaces live
- **Horizon 2 (Next, 1-3 months):** metered production agent runs · hybrid pricing live · Zapier/Make integration · correction loop v2. Every bet has a kill criteria.
- **Horizon 3 (Bet, 3-6 months):** opt-in cross-workspace mapping intelligence · governance pack as GTM
- **Board Narrative:** Thesis: Shipframe turns a design file into running production for small SaaS teams with no front-end developer, and every correction a team makes teaches its workspace. Case: $55/user/month adjacent spend proves demand; the context graph + scoped correction loop is what incumbents can't see; 71% gross margin survives a 3x cost shock.
- **Ask:** $900K · 12 months ($550K eng, $250K inference + eval/HITL tooling, $100K design-partner GTM) · 2 senior eng + founder-PM · hard review at month 6 against the H2 kill criteria
- **Key Strategic Change:** from "the AI context layer is our differentiator" to "our differentiator is the correction loop scoped to each workspace's design-to-deploy graph, instrumented before the first customer"

→ Details: [`06-the-pitch/`](06-the-pitch/)
