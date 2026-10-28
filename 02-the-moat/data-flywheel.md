# Data Flywheel Map

> Score each loop 1-5. Your weakest loop is where competitors attack first.
> The four loops below are the M2 starting point - adapt if your product has 2 or 6 loops instead of 4.

## Flywheel Loops

| Loop | What It Measures | Score 1 | Score 5 | Score |
|------|------------------|---------|---------|-------|
| **Correction** | Do users fix AI outputs? Is that signal captured and reused? | No capture | Automated retraining | 1/5 |
| **Preference** | Does the product learn individual / team preferences over time? | Stateless | Deep personalization | 2/5 |
| **Domain Context** | Does usage in one area improve quality in adjacent areas? | Siloed | Cross-domain transfer | 3/5 |
| **Network** | Does each new user / team make the product better for everyone? | Isolated | Strong network effects | 1/5 |

### Correction Loop - 1/5
**What you capture today:** Nothing. The AI context layer rides on frontier models, and user edits to AI outputs are not captured, stored, or fed back into anything we train or tune. With zero customers there is no correction signal at all.
**How it compounds:** It doesn't yet. If instrumented, edits to AI-generated output (components rewritten vs. accepted, schema corrections, rejected generations) could improve per-workspace output quality without requiring training-data scale.

### Preference Loop - 2/5
**What you capture today:** Per-workspace context: how a team maps design decisions to CMS schemas and component usage. This is workspace-level personalization by design, but it is hypothesis-stage with no customers behind it, and it is not per-user preference data.
**How it compounds:** Each workspace's context deepens with use, which raises switching costs for that customer. It does not compound across customers.

### Domain Context Loop - 3/5
**What you capture today:** The design-file to content-model to deploy-pipeline graph: proprietary context for each customer that Figma and Vercel cannot see. The strongest loop and the product's only stated differentiator.
**How it compounds:** Usage on the design side improves AI quality in CMS modeling and deploy configuration for the same customer. Capped at 3 because the corpus is tiny and does not aggregate across customers, consistent with the 2/5 Data Advantage score in the three-axis diagnostic.

### Network Loop - 1/5
**What you capture today:** Nothing cross-customer. Context compounds per customer but does not aggregate into anything that improves the product for everyone.
**How it compounds:** It doesn't. The org-level network effects in this market (shared libraries, design systems, every new hire already knowing the tool) belong to Figma.

**Total Flywheel Score: 7/20**
**Weakest Loop:** Correction and Network, tied at 1/5. Scorer readout: "No flywheel. Data goes in and gets thrown away."
**Fix for weakest loop:** Instrument the Correction loop now. It is the only loop fixable pre-scale: capturing how users edit AI-generated output can be built before the first customer, while the Network loop requires a customer base that does not exist yet. See the defense note below for the scoping that makes this defensible against Figma running the same play.

---

## Encroachment Threat Assessment

### 1. Platform Encroachment
**Attacker:** Figma
**Vector:** Dev Mode, Make, and Sites: building the design-to-production wedge from the position of already owning the designers, with org-level network effects (shared libraries, design systems, hiring pool) working against us pre-adoption.
**Time-to-threat:** 6-12 months (the pieces are shipping publicly now)
**% of value at risk:** ~60%. The core wedge is their published roadmap; what survives is the AI context layer for customers already wired into production.

### 2. Vertical Competitor
**Attacker:** Framer
**Vector:** Already is design plus CMS plus hosting with AI features, with years of head start on the integrated model. Competes directly for every pre-adoption deal, where we are "just another canvas."
**Time-to-threat:** Immediate (already in market)
**% of value at risk:** ~40%, concentrated in new-customer acquisition rather than any installed base.

### 3. Adjacent Expansion
**Attacker:** Vercel
**Vector:** v0 approaches the same problem from the code side, sitting on deploy telemetry plus generation data at a volume we cannot match. Foundation models compound this by making "generate the UI" a prompt rather than a tool.
**Time-to-threat:** 12-18 months
**% of value at risk:** ~50%. Devalues the AI context layer itself if generation quality from raw scale beats generation quality from workspace context.

---

## 90-Day Encroachment Plan

*Your partner played the Big Tech attacker. What was their plan to kill you?*

**Attacker:** Figma
**Attack vector (target the weakest loop):** The Correction loop. Their stated plan: double down on native AI capabilities built around correction loops, using the correction and user feedback the product gathers over time to improve output quality, prioritizing the most repetitive corrections first.
**Weeks 1-4 - what they ship:** Correction capture across Make and Dev Mode: log every edit designers make to AI-generated output and start tuning against the most repetitive correction patterns, instantly at a volume we will never see.
**Weeks 5-8 - how they poach users:** They already own the designers. "AI that learns from your team's edits" gets marketed into existing org accounts, bundled into seats teams already pay for, and pushed at our prospects mid-evaluation.
**Weeks 9-12 - why users don't come back:** Output quality visibly improves week over week because millions of users' corrections feed the loop against our zero. Leaving Figma now means giving up shared libraries, design systems, and a better-trained AI.
**Your defense:** Do not fight a symmetric correction-data race; Figma wins that on volume alone. Scope our correction loop to the signal only we can see: corrections to AI output in the context of the customer's live content model and deploy pipeline (schema mappings, component-to-CMS bindings, what shipped vs. what was rejected). Instrument it now, pre-scale, and make per-workspace correction learning visible to the customer inside their first 30 days, so the Correction loop feeds the Domain Context loop (our only 3/5) instead of trying to out-collect Figma on generic edits.
