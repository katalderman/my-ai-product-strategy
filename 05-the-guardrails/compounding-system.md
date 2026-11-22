# Compounding System Design

## Feedback Loops


| Loop | Input | Output | Compounds? | Status |
|------|-------|--------|-----------|--------|
| Recursive Learning | Accept/edit/reject on every AI proposal + reviewer corrections from the HITL queue | Better per-workspace generation quality, repetitive corrections tuned out first | Y | missing |
| Cross-Domain Transfer | The per-workspace design-to-CMS-to-deploy context graph | Design edits improve schema mapping and deploy config quality for the same customer | Y | broken |
| Network Intelligence | Cross-customer patterns (anonymized component/schema mappings) | Better default mappings and templates for every new workspace | N | missing |

**Broken loop identified by partner:** Recursive Learning: correction capture is designed (M2 fix plan, M4 HITL architecture) but nothing is instrumented or shipping, corrections today would go nowhere. Confirmed by partner in the peer challenge: accept/edit/reject events are not captured anywhere today (named flow: proposal corrections to the correction store), so every correction a user makes is thrown away (concrete failure), and a three-month freeze would cost us nothing, which is the definition of a broken flywheel (measurable consequence).
**Fix plan:** Ship the correction store before first customer: accept/edit/reject events write to it from day one, weekly job promotes repetitive corrections into the golden set and per-workspace prompt context. Owner: Kat. Already specced in 04-the-contract HITL section; this makes it a launch blocker, not a backlog item.

## Context Connectivity
<!-- How does knowledge flow across teams and domains? Where does it silo? -->
**How knowledge flows:** Within one workspace, connectivity is the product: the context graph links design, CMS schema, and deploys, so a correction in one domain should improve the others. Internally, eval-harness results inform routing weights manually.

**Where it silos:** By design, nothing crosses customers (per-workspace isolation is the privacy promise), so Network Intelligence is missing until an anonymized aggregation layer exists. Internally, eval results don't auto-update prompts or routing; a human carries every learning across.


## Governance Policy
<!-- Governance Policy, Integrated design platform v0.9 (pre-launch) -->


**Scope:** Customer-facing AI in the design platform: canvas generation and filler suggestions, CMS schema mapping, and production agent runs (page/flow generation, schema migrations, deploy previews). Excludes: Internal eval tooling and the LLM-as-Judge pipeline (separate internal policy). No internal-employee AI-use policy is covered here; that is IT/CISO scope.

**Autonomy boundaries:** Filler suggestions (naming, lint, alt text) and canvas edits at >90% confidence, with one-click undo, auto. Production deploys and CMS schema migrations, at any confidence, even >95%, human approval required. Bulk deletion of components or content; any cross-workspace data access, never auto.

**Escalation triggers:** (1) Confidence <50% on any generation. (2) Safety or injection flag: instructions embedded in canvas text layers, script payloads in CMS values. (3) Any action touching a production deploy or schema migration. (4) User requests review, or rejects the same proposal 3 times. (5) Workspace has required reviews enabled: every agent run routes to the review queue.

**Audit cadence:** Real-time, Tool-call log: every agent call recorded with reasoning and result (Eng on-call). Weekly, Automated eval vs. golden set + hallucination/schema-validator run (PM: Kat). Monthly, Human review of 50 random agent runs + all escalations; every third month is the full policy review (Founder + security counsel).

**Regulatory exposure (EU AI Act / other):** EU AI Act (productivity/design tooling, non-prohibited); GDPR (customer content flows through prompts); DPAs and zero-retention agreements with every model provider on the routing list; SOC 2 roadmap before enterprise deals.. Risk tier: limited. Controls: Data minimization in prompts; no training on customer content; zero-retention with all routed providers; per-workspace isolation (no shared memory across customers); full tool-call logging with 12-month retention; multi-model kill switch per the M2 audit..

## Agent Topology
<!-- If using agents: what can each agent do? What can't it do? Who approves what? -->
Design-to-production agent: CAN generate pages/flows on canvas, draft CMS schema migrations, prepare deploy previews. CANNOT execute production deploys, run schema migrations, bulk-delete, or read outside its workspace. Approval owner: workspace reviewer (customer side); safety flags escalate to our on-call. Tool calls allow-listed (schema read, canvas write, deploy-preview) and rate-limited, every call logged. Memory: short-term per run + the per-workspace context graph; shared cross-customer memory is a hard no.



## Shadow AI Audit


## Discover, User-Side Workarounds
- Prospects paste design frames into ChatGPT/Claude to generate production React code, then hand-wire CMS fields | source: User interview | signal: Capability gap | freq: H | spend: $20/mo | decision: Build
- Teams run v0 or Cursor on exported designs to scaffold components, losing all design-file bindings | source: Forum/Reddit | signal: Capability gap | freq: H | spend: $20/mo | decision: Build
- Zapier/Make recipes syncing CMS entries from spreadsheets after design changes | source: Zapier/Make | signal: Workflow gap | freq: M | spend: $15/mo | decision: Partner
- Copywriters run page copy through ChatGPT for SEO titles and meta descriptions before publishing | source: User interview | signal: Capability gap | freq: M | spend: $0/mo | decision: Build
- Designers ask Claude to sanity-check AI-generated schema mappings before accepting them | source: User interview | signal: Trust gap | freq: L | spend: $0/mo | decision: Ignore

## Pattern Assessment
- Workarounds found: 5
- Build candidates: 3
- Partner candidates: 1
- Ignore decisions: 1
- Adjacent spend: $55/mo
- Dominant signal: Capability gap

## Action Plan
### Build
Design-to-production code generation with live CMS bindings (rows 1-2): this IS the core product; the workarounds validate the wedge and define the quality bar (v0-level output, plus the bindings they lose). SEO titles and meta descriptions (row 4): cheap filler extension on the triage tier, ships with launch.

### Partner
Official Zapier/Make integration for CMS content sync (row 3): workflow glue is not our moat; an official integration closes the gap and puts us in their recipe directories as an acquisition channel. OAuth app + webhook triggers on content-model changes.

### Ignore + Monitor
Claude sanity-checks of schema mappings (row 5): not a feature to build. It is a trust signal; the fix is the M4 confidence UX and evidence panel, not more capability. Monitor post-launch: if prospects still double-check our mappings with another model, the reliability contract is not landing.

## Roadmap Brief
Based on your audit: 5 user-side workarounds discovered.
Decisions: 3 build · 1 partner · 1 ignore · 0 TBD.
Estimated adjacent spend: $55/mo across surveyed users.
Dominant signal: Capability gap.

Recommended next step: Capability gaps dominate, users want something your product does not do. Strongest near-term move is building one or two of these natively before a competitor does.

Sequence the Build column by frequency × strategic relevance. Confirm Partner candidates with the external tools' partnership teams. Re-run this audit each quarter, workarounds shift fast.

| Workaround | Signal Source | Frequency | Decision |
|------|-------|-----------|----------|
| Prospects paste design frames into ChatGPT/Claude to generate production React code, then hand-wire CMS fields | User interviews (capability gap) | H | build |
| Teams run v0 or Cursor on exported designs to scaffold components, losing all design-file bindings | Forum/Reddit (capability gap) | H | build |
| Zapier/Make recipes syncing CMS entries from spreadsheets after design changes | Zapier directory (workflow gap) | M | partner |
| Copywriters run page copy through ChatGPT for SEO titles and meta descriptions before publishing | User interviews (capability gap) | M | build |
| Designers ask Claude to sanity-check AI-generated schema mappings before accepting them | User interviews (trust gap) | L | ignore (fix is M4 confidence UX, not a feature) |

**Workarounds found:** 5 (pre-launch: signals from prospect discovery, Reddit, and the Zapier directory, not support tickets)
**Build candidates:** 3 (design-to-code with live CMS bindings is the core product; SEO/meta copy is a cheap filler extension)
**Adjacent spend:** ~$55/user/month (ChatGPT Plus + v0 + Zapier) paid externally for things the product will do natively



Responsible AI Maturity Scorer, Module 5

Total: 13/25, Developing
Some practices in place. Gaps will surface under scrutiny.
Weakest: Fairness

Compliance: 2/5
1 = no formal compliance, 5 = certified and audited

Transparency: 4/5
1 = black box, 5 = full explainability + audit trails

Fairness: 1/5
1 = no bias testing, 5 = continuous monitoring + remediation

Privacy: 3/5
1 = minimal consent, 5 = privacy-by-design + user controls

Accountability: 3/5
1 = no owner, 5 = RACI defined + incident playbooks
