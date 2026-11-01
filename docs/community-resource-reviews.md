# Community Resource Reviews

Checked 2026-09-30. These reviews examine public first-party material for catalog inclusion. They do not test connected accounts, certify production controls or establish business effects. Review dates apply to the claims below, not the entire product.

## NotFair Plugin

Suggested by Yuting Zhong in [PR #2](https://github.com/leoncuhk/awesome-martech-ai/pull/2). The former `nowork-studio/NotFair` URL redirects to `nowork-studio/notfair-plugin`.

- Evidence: the [repository README](https://github.com/nowork-studio/notfair-plugin/blob/5094263b522165647789e9594406bb3ce096c5fe/README.md), [MIT license](https://github.com/nowork-studio/notfair-plugin/blob/5094263b522165647789e9594406bb3ce096c5fe/LICENSE) and [MCP configuration](https://github.com/nowork-studio/notfair-plugin/blob/5094263b522165647789e9594406bb3ce096c5fe/.mcp.json), revision `5094263` dated 2026-09-25.
- Supported scope: public skill files describe advertising, GA4 and Search Console workflows. Live account operations use one vendor-hosted OAuth connection; platform access depends on connected accounts and exposed capabilities.
- Placement: agent-building inputs and tool integrations, rather than a general orchestration engine. The public skill repository is distinct from the hosted service.
- Limits: no connected-account reproduction, independent effect estimate or security certification. Star counts and an implication that all MCP/backend implementations are open source were removed.

## Hermes

Suggested by `alfredoautomatizaloconia-cloud` in [PR #3](https://github.com/leoncuhk/awesome-martech-ai/pull/3). The README conflict was resolved against the current Form 3 section without reverting the maintainer's framework or demo.

- Evidence: official [integration descriptions](https://www.buildwithhermes.com/integrations) and [operator product page](https://www.buildwithhermes.com/operators), checked 2026-09-30. The pages label themselves last reviewed June 2026; a distinct publication date is not supplied.
- Supported scope: vendor describes bundled voice providers, CRM, calendar connections and per-client billing. The operator page advertises private beta and a future public launch. Inclusion records product positioning, rather than demonstrated general availability or independently verified operation.
- Placement: an agency-oriented customer-interaction platform reference in Form 3. Its tenant isolation, deployment scale, quality checks and compliance controls were not independently inspected.
- Limits: no public code or reproducible deployment evidence was examined. Pricing/usage details differ across product pages, so exact rates, margins, savings and beta testimonials are excluded. Capability descriptions do not establish sales lift or service resolution.

## BulkPublish

Suggested by Muhammad Azeem (`azeemkafridi`) in [PR #5](https://github.com/leoncuhk/awesome-martech-ai/pull/5). The linked repository is published under the contributor's GitHub account; treat it as author/vendor material.

- Evidence: the [repository README](https://github.com/azeemkafridi/bulkpublish-api/blob/a3c568ef983643b3793f92d3638201797a6b5a4b/README.md), [OpenAPI specification](https://github.com/azeemkafridi/bulkpublish-api/blob/a3c568ef983643b3793f92d3638201797a6b5a4b/openapi.json), [MCP documentation](https://github.com/azeemkafridi/bulkpublish-api/blob/a3c568ef983643b3793f92d3638201797a6b5a4b/mcp-server/README.md) and [skill catalog](https://github.com/azeemkafridi/bulkpublish-api/blob/a3c568ef983643b3793f92d3638201797a6b5a4b/skills/social-media-content-skills/README.md), revision `a3c568e` dated 2026-09-29.
- Supported scope: public Python/Node clients, API definitions, MCP integration and readable workflow skills describe draft, scheduling, review and publishing operations. They call the hosted BulkPublish service with account credentials and connected social channels; the repository does not establish that the publishing backend is self-hostable.
- Placement: Activation, for social-content delivery and workflow integration. Planning/review skills are inspectable instructions, rather than independently validated strategy or safety guarantees.
- Limits: no authenticated publishing test, platform-wide coverage audit, reliability measurement or incremental effect estimate. Platform/tool counts, pricing, free-tier superlatives and efficacy claims are excluded.

## MarketMirror

Submitted by its maker, `DarkWorldCoder`, with Codex assistance. This is a first-party source review for an early-product reference, checked 2026-10-31; it is not an independent product evaluation.

- Evidence: the [repository README](https://github.com/DarkWorldCoder/market-mirror/blob/caf28287ebfc7d681672186ae868e861f22c7e32/README.md), [MCP server implementation](https://github.com/DarkWorldCoder/market-mirror/blob/caf28287ebfc7d681672186ae868e861f22c7e32/plugin/skills/market-mirror/scripts/mcp_server.py) and [AGPL-3.0 license](https://github.com/DarkWorldCoder/market-mirror/blob/caf28287ebfc7d681672186ae868e861f22c7e32/LICENSE), revision `caf2828` dated 2026-10-31, plus the [saved dashboard demo](https://darkworldcoder.github.io/market-mirror/demo/), retrieved 2026-10-31. The demo is a mutable public artifact; its fictional Fitloop product, buyers and results are simulated.
- Supported scope: the public documentation and code describe a self-hosted MCP server/CLI for giving AI-generated buyer personas ads, prices and pitches, then inspecting generated responses in an HTML dashboard. Documentation describes reviewing personas and estimated usage before running a simulation; model calls require an engine/provider configuration and may incur costs. These are maker-described capabilities supported by inspectable artifacts, not independent reproduction.
- Placement: AI-assisted experimentation, as an input to hypothesis development and planning a real test. Synthetic objections can suggest what to investigate; they do not replace representative customer evidence, randomized assignment or evaluation of actual outcomes.
- Verification scope: inspected the pinned public documentation, license and MCP implementation and retrieved the saved demo. No fresh simulation, paid model call, provider authentication or connected-account operation was performed for this submission.
- Limits: AI-generated reactions are hypotheses, not real customer feedback, validated demand or sales forecasts. This review establishes no independent predictive accuracy, causal lift, population representativeness, adoption, deployment reliability or security certification. Any business-effect claim needs separately documented real-world evidence.
