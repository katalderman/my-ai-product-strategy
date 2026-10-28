# Kill Switch Audit

## Vendor Dependency Assessment

| Dimension | Current State | Risk Level | 48-Hour Action |
|-----------|--------------|------------|---------------|
| **Provider** | Multi-model via a routing gateway; no single frontier lab is a hard dependency, but output quality concentrates in the top 1-2 models for design-to-code tasks | M | Flip routing weights to the next-best model and rerun the eval harness to confirm the quality floor before customer traffic notices |
| **Abstraction** | The gateway is the abstraction; we swapped vendor lock for router lock. No internal interface of our own wrapping the gateway yet | M | Stand up a thin internal client interface over the gateway and hold direct API keys for the top two providers as a bypass path |
| **Routing** | Live multi-model routing with the ability to route per task type (generation vs. schema mapping vs. context retrieval) | L | Predefine fallback chains per task type and run a forced failover drill to prove they work under load |
| **Eval** | Automated eval harness gates model and prompt changes in CI | L | Run the full harness against candidate replacement models and publish the quality delta before flipping traffic |

## Portability Score
**Ready**, with one honest caveat: routing and evals make model swaps cheap, but the AI context layer's prompts and context packing are tuned to specific model behaviors, so "ready" is only as true as the last failover drill. The gateway itself is now the single point of failure this audit exists to catch.

## If the top-routed provider doubles pricing tomorrow:
Shift routing weights to the next-best model that clears eval thresholds; the harness quantifies the quality delta within hours, so the decision is data, not panic. Pin the expensive model only for the task types where the eval gap justifies the cost. At zero customers, token COGS is trivial anyway; the real 48-hour exposure is the router's own pricing and terms, which is why the internal interface in the Abstraction row matters.

## If the primary vendor ships a competing product:
What they can't replicate is the per-customer design-to-deploy context graph: schema mappings, component-to-CMS bindings, what shipped vs. what was rejected, and the correction signal scoped to it. A model vendor sees prompts, not the customer's live content model and production wiring, and multi-model routing means no single lab sees even our full prompt traffic. The caveat: whichever vendor serves a request does see that request's context, so zero-retention agreements with every provider on the routing list are part of the kill switch, not a nice-to-have.
