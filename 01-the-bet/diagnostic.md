# Three-Axis Diagnostic: Your Product

**Product:** Integrated design platform (Figma competitor with native backend,
CMS, and hosting integration plus built-in AI context)
**Role:** Founder / PM

## Contextual Moat: 3/5
**Rationale:** Workflow depth is the whole thesis: the design file is wired to
the content model and the deploy pipeline, so a mature customer can't leave
without unwinding production infrastructure. But that switching cost only
exists AFTER a team routes real infra through us. Pre-adoption, we're just
another canvas, and Figma's org-level network effects (shared libraries,
design systems, every hire already knows it) work against us daily.
**Named attacker:** Figma. Dev Mode, Make, and Sites are them building our
wedge from the position of already owning the designers.

## Data Advantage: 2/5
**Rationale:** Our proprietary signal is per-workspace: how design decisions
map to CMS schemas, component usage, and what actually shipped. That context
compounds for each customer but doesn't aggregate into a training-data moat
at our scale. Frontier labs have more design-to-code data than we will ever
collect, and our "AI context" layer rides on their models.
**Named attacker:** Vercel. v0 sits on deploy telemetry plus generation data
at a volume we can't match, and it approaches the same problem from the
code side.

## Platform Exposure: 2/5
**Rationale:** Exposure is high from three directions at once: Figma expanding
downstream, Vercel expanding upstream, and foundation models making "generate
the UI" a prompt rather than a tool. Worse, our integrations are dependencies:
the CMS and hosting providers we connect to can bundle design themselves or
change API terms. Pivot speed is our one asset as a small team.
**Named attacker:** Framer. It already IS design plus CMS plus hosting with
AI features, with years of head start on the integrated model.

## Top Vulnerability
Our core wedge (design-to-production integration) is not a gap in the market,
it is the published roadmap of Figma, Framer, and Vercel; the AI context layer
is our only differentiator and it needs customer scale we don't have yet.

## Confidence: M
High confidence on platform exposure (the attackers are shipping publicly),
medium on moat because switching-cost-after-adoption is still a hypothesis
with zero customers behind it.
