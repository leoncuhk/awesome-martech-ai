<div align="center">

# Awesome Martech AI

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

A curated guide to marketing AI decisions: customer data, prediction, causal measurement, constrained optimization, activation and agent workflows. Resources are organized by what they help a practitioner decide and what evidence supports them.

<br>

<a href="assets/martech-ai-stack.png"><img src="assets/martech-ai-stack.png" alt="Original Martech AI stack overview with five core layers, technical modules and agent orchestration" width="1200"></a>

</div>

<br>

The original stack illustration is retained as a module overview. Its feedback loop is conceptual: observed logs return to Data, while measured evidence and uncertainty inform Intelligence and decisions. Causal learning requires a valid design and assumptions; see [the detailed explanation](think/five-layers-cognitive-cycle.md).

**Scope:** a technical knowledge framework for marketing AI, not a complete census of marketing software. Customer service and sales are included where they connect to customer relationships and growth.

**Review baseline:** 2026-09-30. Product functionality, implementation, commercial scale and causal impact require different evidence. See [evidence standards and review notes](docs/evidence-review.md). Catalog links are learning/navigation resources; inclusion is not a performance endorsement.

## Contents

**Part I — The Martech AI Stack**

- [Introduction](#introduction)
- [Stack Map and Design Approach](#stack-map-and-design-approach)
- [Data Layer](#data-layer)
- [Intelligence Layer](#intelligence-layer)
- [Decision Layer](#decision-layer)
- [Activation Layer](#activation-layer)
- [Measurement Layer](#measurement-layer)
- [Platforms and MLOps](#platforms-and-mlops)

**Part II — The Agent Era**

- [Four Forms of Marketing Agents](#four-forms-of-marketing-agents)
- [Lifecycle Decisioning](#lifecycle-decisioning)
- [LLM Agent Leverage Points](#llm-agent-leverage-points)
- [Agent-Building Frameworks](#agent-building-frameworks)
- [Frontier (2025/2026)](#frontier-20252026)

**Part III — Applied and References**

- [Interactive Demos](#interactive-demos)
- [Industry Playbooks](#industry-playbooks)
- [Original Research and Notes](#original-research-and-notes)
- [Books](#books)
- [Research Papers](#research-papers)
- [Community and Conferences](#community-and-conferences)
- [Related Lists](#related-lists)
- [Contributing](#contributing)

---

# Part I — The Martech AI Stack

## Introduction

Marketing AI combines rules, predictive models, causal inference, optimization and generative workflows. These coexist rather than succeeding one another in clean historical eras: Google's [production CTR engineering paper](https://research.google/pubs/ad-click-prediction-a-view-from-the-trenches/) was published in 2013.

The working objective is **long-term incremental value under budget, consent, fulfillment and customer-experience constraints**. A likely buyer is not necessarily a persuadable buyer; delivered actions are not necessarily valuable actions; a feedback loop is not necessarily a valid causal learning loop.

This repository organizes the field into three parts:

- **Part I — The Stack.** Five core responsibilities, supported by Platforms and MLOps, with the methods and tools that live in each.
- **Part II — The Agent Era.** A vertical layer cutting across the stack: marketing agent products and workflows, four overlapping operational forms and independent system descriptors, and where LLM reasoning has structural leverage.
- **Part III — Applied and References.** Industry playbooks, original research, books, papers, and community resources.

Entry selection prioritizes deployed systems with disclosed traction, peer-reviewed or production-engineering published work, and material that substantively reframes how practitioners approach a problem.

This list is the marketing-side companion to [awesome-quant-ai](https://github.com/leoncuhk/awesome-quant-ai) and [recsys-papers](https://github.com/leoncuhk/recsys-papers).

## Stack Map and Design Approach

### The Stack

```text
┌──────────────────────────────────────────────────────────────────────┐
│  Agents & Workflows (cross-cutting)                                  │
│  planning · creative · conversational · media buying · operations    │
└──────────────────────────────────────────────────────────────────────┘
┌──────────────────────────────────────────────────────────────────────┐
│  Measurement  ← A/B · Incrementality · MMM · Attribution             │
│  Activation   ← Paid media · CRM · Push · Conversation · Site        │
│  Decision     ← NBA · RTB · Allocation · Targeting & offers          │
│  Intelligence ← ML · Causal · RL · Embeddings · Foundation Models    │
│  Data         ← CDP · Events · Identity · Consent & provenance       │
└──────────────────────────────────────────────────────────────────────┘
┌──────────────────────────────────────────────────────────────────────┐
│  Platforms & MLOps: pipelines · feature stores · model serving       │
│  Experimentation infrastructure · observability · governance         │
└──────────────────────────────────────────────────────────────────────┘
```

These are logical responsibilities, not mandatory service or product boundaries. Activation produces observed outcomes and action logs for Data; Measurement adds experimental records and evidence with uncertainty for Intelligence and policy review. Platforms and MLOps support all five. Agents and workflows orchestrate work across them. Selection, interference and missing counterfactuals can bias learning even when all arrows are connected.

### Cross-Layer Domain Views

Three terms recur in marketing-AI literature — **User Intelligence**, **Advertising Systems**, **Growth Engine** — that are not stack layers. They are **domains that cut across multiple layers**. Naming which layers each domain touches resolves much of the apparent ambiguity in the field:

| Domain | Data | Intelligence | Decision | Activation | Measurement |
|---|:---:|:---:|:---:|:---:|:---:|
| User Intelligence | ● | ● | ● |  |  |
| Advertising Systems | ● | ● | ● | ● | ● |
| Growth Engine | ● | ◐ | ● | ● | ● |

- **User Intelligence** — builds the system's model of the user. Lives in Data (CDP, identity), Intelligence (LTV, propensity, embeddings), and Decision (audience selection). Recommender systems are a heavy sub-area; see [recsys-papers](https://github.com/leoncuhk/recsys-papers).
- **Advertising Systems** — matches and delivers ads. Uses Data (requests, exposure and conversion logs), Intelligence (ranking models such as DIN/DLRM), Decision (bids and pacing), Activation (delivery), and Measurement (experiments and outcome reporting).
- **Growth Engine** — orchestrates actions to lift business metrics. Lives in Decision (NBA, budget allocation), Activation (channel orchestration), and Measurement (closed-loop experimentation). Often draws on the Intelligence layer (propensity, uplift) without owning it.

The table shows common responsibilities, not exclusive ownership. Growth systems still require customer and execution data. Uplift estimation can inform any of these domains; fitting an effect model belongs to Intelligence, choosing an action belongs to Decision, and evaluating a policy belongs to Measurement. Identify both the business question and the responsibility before placing a resource.

The rest of Part I is organized by layer rather than by domain.

### Design Approach

A defensible Martech AI system is built around the loop, not around a model:

1. **Define the growth objective.** Pick one north-star outcome (revenue, retained user months, qualified pipeline). Define guardrail metrics (margin, NPS, brand). Specify its population, horizon, costs and minimum worthwhile improvement.
2. **Identify the decision surface.** What is the system actually choosing? An audience, a creative, a bid, a message, a timing, a channel mix? The decision determines the method.
3. **Pick the right method for the decision type.** Prediction (supervised) ≠ causation (uplift / DiD / synthetic control) ≠ sequential decision (bandits / RL) ≠ generation (LLM). Mismatched methods are a recurring cause of failed projects.
4. **Establish a measurement regime first.** Choose a suitable holdout, geo, switchback or observational design before launching; combine experiments and MMM where their estimands align.
5. **Build the data contract.** Identity resolution, event taxonomy, consent state. The model is downstream of the data contract.
6. **Ship the minimum closed loop.** Connect data, a simple policy, authorized delivery and evaluation; validate the complete action before adding model complexity.
7. **Iterate on the bottleneck layer.** Diagnose data, modeling, decisions, delivery and evidence separately; improve the measured bottleneck.
8. **Govern the agent.** When LLM agents enter the loop, evaluate accuracy and bounded authority together. Define what the agent may decide, what requires human review, and what is forbidden.

### Paradigm Comparison

| Paradigm | Decision type | Data requirements | Where it fits |
|---|---|---|---|
| Rule engines | Conditions / thresholds | Explicit business state and constraints | Eligibility, compliance and hard guardrails |
| Supervised ML | Outcome prediction | Representative labeled outcomes and known delays | CTR/CVR/LTV, propensity |
| Causal / Uplift | Intervention contrasts | Randomized data or defensible identification and overlap | Treatment targeting, incrementality |
| Multi-armed bandits | Exploration and exploitation | Actions, assignment probabilities and mature rewards | Creative, headlines, subject lines |
| Reinforcement Learning | Sequential policy | Transitions, rewards and interaction/policy logs; simulator when used | Bidding, pacing, next best action |
| LLM workflows / agents | Context interpretation and tool use | Context, tools, task evaluations and bounded permissions | Strategy, creative workflows, customer interaction |

Data volume and latency are workload-specific. Distinguish model learning from live action selection; measure serving latency, tool costs and freshness for the intended workload. Retrieval prepares context and still requires evaluation.

### Method Suitability and Baselines

| Method | Suitable conditions and data | Baseline | Main failure risk |
|---|---|---|---|
| Prediction | Stable target, representative labeled outcomes, known delay | Rules / simple calibrated model | Selection and target leakage; prediction mistaken for uplift |
| Uplift / causal estimation | Defined treatment, randomized data or defensible identification, overlap | No action / randomized rule policy | Confounding, weak overlap, interference |
| Bandits | Repeatable actions, observable rewards, exploration permitted | Fixed allocation | Delayed rewards, changing arms, unsafe exploration |
| RL | Sequential effects, logged policies, valid simulator or safe evaluation | Rules / myopic policy | Simulator bias and unsupported off-policy extrapolation |
| MMM | Time/geo variation, controls, spend/outcome consistency, lag assumptions | Simpler aggregate model plus experiments | Collinearity, confounding, extrapolating response curves |
| LLM workflows / agents | Context-heavy tasks, verifiable tools, bounded permissions | Fixed workflow / human process | Wrong facts, unauthorized actions, cost and latency |

Predefine the estimand, observation window, business threshold and guardrails. Measure at the randomization unit; inspect carryover, interference and mature outcomes. A fixed-window experiment monitors safety during operation and estimates efficacy at the planned analysis time.

### Metrics and Units

| Metric | Definition to declare | Common confusion |
|---|---|---|
| CTR / CVR | Clicks or conversions divided by a specified eligible denominator | Different exposure, click or assigned-user denominators are not interchangeable. |
| Absolute conversion effect | Treatment conversion rate minus control rate, in percentage points | A 2 pp increase from 10% to 12% is 20% relative lift. |
| Relative lift | `(treatment − control) / control`, for a defined outcome; needs a nonzero denominator | A positive point estimate can still miss the business threshold. |
| Attributed ROAS | Credited revenue / spend under an attribution rule and window | Credit is not a counterfactual effect. |
| iROAS | Incremental net revenue / positive incremental marketing spend, for a compatible contrast and horizon | Average contrast return is not the return on the next dollar. |
| Incremental contribution | Incremental net revenue minus incremental product/fulfillment and marketing costs | Revenue lift can be unprofitable; deduct discounts/refunds once. |
| CLV / LTV | Expected customer value over a declared horizon and discount/cost convention | Predicted value is not the causal value of an intervention. |

ROI definitions differ across sources. State the exact formula and cost coverage before comparing values. The [demo source ledger](demos/incrementality-measurement/sources.md) separates eBay's revenue-based ROI convention from its own iROAS and contribution metrics.

## Data Layer

The data substrate that everything else stands on: customer events, identity resolution, consent state, and privacy-preserving joins with external data.

### Customer Data Platforms

- [Segment](https://segment.com/) — A commercial CDP for event collection and downstream routing.
- [RudderStack](https://www.rudderstack.com/) — Customer-data infrastructure with an open-source collection/router component; warehouse-oriented product scope varies.
- [Hightouch](https://hightouch.com/) — Reverse ETL from warehouse to activation tools; the composable-CDP pattern.
- [Fivetran Activations (formerly Census)](https://fivetran.com/docs/activations/overview) — Managed reverse ETL from warehouse data to business tools; reviewed 2026-09-30.

### Identity and Event Schema

- [Snowplow](https://snowplow.io/) — Open-source behavioral data pipeline; explicit event schemas.
- Identity graphs and resolution are typically built on top of CDP outputs; vendor offerings include LiveRamp, Adobe RTCDP, and the warehouse-native pattern (BigQuery / Snowflake) with deterministic + probabilistic matching.

### Clean Rooms and Privacy

- [Google Ads Data Hub](https://www.thinkwithgoogle.com/products/ads-data-hub/) — Privacy-preserving query layer over Google's first-party data.
- [AWS Clean Rooms](https://aws.amazon.com/clean-rooms/) — Cross-party data collaboration without raw data sharing.
- [Snowflake Data Clean Rooms](https://www.snowflake.com/en/product/features/data-clean-rooms/) — Native clean-room workloads inside the Snowflake warehouse.

## Intelligence Layer

The modeling layer: predictive ML, causal inference, reinforcement learning, embeddings, and foundation models. This is where the marketing system's beliefs about users, items, and outcomes are produced.

### Machine Learning Foundations

- [Pattern Recognition and Machine Learning](https://www.microsoft.com/en-us/research/people/cmbishop/prml-book/) by Christopher Bishop — Reference for probabilistic ML used in ranking, CTR, and propensity models.
- [The Elements of Statistical Learning](https://hastie.su.domains/ElemStatLearn/) by Hastie, Tibshirani, Friedman — Free PDF; tree ensembles and regularization used heavily in marketing ML.
- [Deep Learning](https://www.deeplearningbook.org/) by Goodfellow, Bengio, Courville — The reference text for deep architectures behind modern ad ranking and embeddings.

### Causal Inference and Uplift

Marketing decisions change exposures, offers or timing. Causal evidence connects these interventions to outcomes; predictive scores answer a different question.

- [Causal Inference: The Mixtape](https://mixtape.scunning.com/) by Scott Cunningham — Free book; DiD, IV, RDD, synthetic control with applied code.
- [Causal Inference for The Brave and True](https://matheusfacure.github.io/python-causality-handbook/) by Matheus Facure — Python-first applied causal inference textbook.
- [Trustworthy Online Controlled Experiments](https://experimentguide.com/) by Kohavi, Tang, Xu — The Microsoft/LinkedIn/Booking playbook for A/B testing at scale.
- [CausalML](https://github.com/uber/causalml) by Uber — Uplift trees and meta-learners for heterogeneous treatment-effect estimation.
- [EconML](https://github.com/py-why/EconML) by Microsoft — Double ML, DR-learner, heterogeneous treatment effects.
- [DoWhy](https://github.com/py-why/dowhy) — Causal effect estimation framework with explicit assumption modeling.
- [Uplift Modeling for Multiple Treatments](https://arxiv.org/abs/1908.05372) — Zhao and Harinen (Uber): multiple treatments, treatment costs and extensions of X/R-learners; identification assumptions still apply.

### Reinforcement Learning

- [Reinforcement Learning: An Introduction](http://incompleteideas.net/book/the-book-2nd.html) by Sutton & Barto — Free PDF; baseline for bandits, contextual bandits, and policy learning used in bidding and NBA.
- [Spinning Up in Deep RL](https://spinningup.openai.com/) by OpenAI — Educational implementations and explanations of PPO/SAC/DDPG; not evidence of deployment in a particular bidder.

### User Modeling

LTV, propensity, segmentation, embeddings — the user representations that feed Decision-layer choices.

- [PyMC-Marketing](https://github.com/pymc-labs/pymc-marketing) — Bayesian customer-lifetime models and MMM; evaluate model assumptions and applicability.
- [Lifetimes](https://github.com/CamDavidsonPilon/lifetimes) by Cam Davidson-Pilon — Historical Python library for non-contractual CLV; archived 2024-06-28, with its repository referring users to PyMC-Marketing.
- [Customer Lifetime Value at Meta](https://www.facebook.com/business/help/1730784113851988) — Meta's official guide to predictive LTV in their ad system.
- [USE: Universal Sentence Encoder](https://tfhub.dev/google/universal-sentence-encoder/4) — Baseline for user/content embeddings.
- [Two-Tower Models for Retrieval](https://research.google/pubs/sampling-bias-corrected-neural-modeling-for-large-corpus-item-recommendations/) — Google/YouTube research on large-corpus retrieval with sampling-bias correction.

### Ranking and Retrieval

The models that score and rank impressions, items, and audiences. Recommender-system models overlap heavily with marketing ranking; see [recsys-papers](https://github.com/leoncuhk/recsys-papers) for the full literature.

- [Deep Interest Network (DIN)](https://arxiv.org/abs/1706.06978) — Alibaba's attention-based CTR model, deployed in production at scale.
- [DIEN](https://arxiv.org/abs/1809.03672) — Sequential extension of DIN.
- [DLRM](https://arxiv.org/abs/1906.00091) — Meta's open-source deep learning recommendation model.
- [DCN-V2](https://arxiv.org/abs/2008.13535) — Deep & Cross Network v2 for feature crosses.

### Foundation Models for Marketing

Pretrained tabular models and sequence-modeling references. A transformer architecture alone is not a broadly pretrained foundation model; transfer to customer-event data needs validation.

- [TabPFN](https://github.com/PriorLabs/TabPFN) — Foundation model for small-to-mid tabular datasets.
- [SASRec](https://arxiv.org/abs/1808.09781), [BERT4Rec](https://arxiv.org/abs/1904.06690) — Transformer architectures for sequential recommendation; adaptation to customer-event tasks requires validation.

## Decision Layer

Given a user model and an inventory, which action does the system take? Bid amount, audience, creative, channel, message, timing.

### Bidding and Pacing

- [Real-Time Bidding by Reinforcement Learning in Display Advertising](https://arxiv.org/abs/1701.02490) — Cai et al.: Shanghai Jiao Tong University, UCL, MediaGamma and Vlion; budget-constrained bidding modeled as sequential decisions.
- [Google Research — Market Algorithms](https://research.google/teams/market-algorithms/) — Google's umbrella research program on auction optimization, pacing, budget-constrained mechanism design, and online matching for display advertising.
- [An Efficient Deep Distribution Network for Bid Shading in First-Price Auctions](https://arxiv.org/abs/2107.06650) — Zhou et al. (2021): distribution modeling, bid optimization and reported Verizon Media DSP evaluation; results are system-specific.

### Next Best Action

- [Pega Customer Decision Hub](https://www.pega.com/products/decision-hub) — Reference architecture for enterprise NBA.
- [Artwork Personalization at Netflix](https://netflixtechblog.com/artwork-personalization-c589f074ad76) — 2017 engineering account of contextual-bandit artwork selection; an application-specific production reference.
- [Uber Engineering Blog — AI & ML](https://www.uber.com/blog/engineering/ai/) — Discovery portal for AI/ML engineering articles; cite individual articles for deployment claims.

### Budget and Audience Allocation

Channel-budget optimization may use experimentally calibrated MMM response curves; customer-level targeting may use uplift evidence. They operate at different units and need compatible objectives and assumptions. Tooling below includes aggregate modeling and budget optimization.

- [Robyn](https://facebookexperimental.github.io/Robyn/) — Meta open-source MMM with budget optimizer.
- [Meridian](https://developers.google.com/meridian/docs/basics/meridian-introduction) — Google open-source Bayesian MMM with response curves, uncertainty and constrained budget optimization; causal interpretation depends on assumptions.

## Activation Layer

Channels through which chosen actions reach customers. Products may also learn policies or choose actions internally; the layer describes responsibility, not an exclusive vendor category. See [agent forms](#four-forms-of-marketing-agents).

**Action contract:** define eligible customer/offer/order states, consent, frequency, inventory, permissions, spend limits, idempotency, safe retries, rollback and human escalation. Log actual exposure and failures separately from proposed actions.

### Paid Media Surfaces

The major buying surfaces are Google Ads, Meta Ads, Amazon Ads, TikTok Ads, retail-media networks (Walmart, Target, Instacart), and the open programmatic ecosystem (DSPs, SSPs, exchanges). Each ships with built-in automated decisioning. See the agent forms in Part II for control points and evidence boundaries.

### CRM and Lifecycle Messaging

- [Iterable](https://iterable.com/) — Programmable channel orchestration; reference platform for lifecycle messaging.
- [Braze (BrazeAI)](https://www.braze.com/product/brazeai) — BrazeAI (formerly Sage AI) for AI-driven personalization and journey optimization.
- [Customer.io](https://customer.io/) — Developer-friendly lifecycle messaging.
- [OneSignal](https://onesignal.com/) — Push and in-app messaging.
- [BulkPublish](https://github.com/azeemkafridi/bulkpublish-api) — Public SDKs, API specification, MCP server and agent skills for drafting, scheduling and publishing social posts through a hosted service; connected accounts and credentials required. Source/vendor capability reference, with unverified business effects; [source review](docs/community-resource-reviews.md#bulkpublish), 2026-09-30.

### Creative Production and DCO

- [Multi-Armed Bandits for Creative Optimization](https://research.facebook.com/publications/bandit-optimization/) — Meta's approach to creative testing at scale.
- [Dynamic Creative Optimization](https://www.thinkwithgoogle.com/marketing-strategies/automation/dynamic-creative-optimization/) — Google's framework for combinatorial creative.

## Measurement Layer

How the system knows whether activation worked: experimentation, incrementality, MMM, attribution. The measurement regime determines what can be learned and therefore what can be optimized.

### Experimentation Platforms

- [GrowthBook](https://github.com/growthbook/growthbook) — Open-source experimentation and feature flagging with Bayesian and frequentist engines.
- [Eppo](https://www.geteppo.com/) — Warehouse-native experimentation, used by Twitch and DraftKings.
- [Statsig](https://statsig.com/) — Feature flags and experiments, free tier for startups.
- [PlanOut](https://github.com/facebook/planout) by Meta — Origin assignment framework; still relevant for orthogonal experimental design.
- [Optimizely](https://www.optimizely.com/) — Long-running commercial experimentation platform.

### Switchback and Geo-Experiments

- [Switchback Experiments at Lyft](https://eng.lyft.com/experimentation-in-a-ridesharing-marketplace-b39db027a66e) — Marketplace-aware experimental design.
- [CausalImpact (Bayesian Structural Time Series)](https://research.google/pubs/inferring-causal-impact-using-bayesian-structural-time-series-models/) — Google's Bayesian structural time-series approach.

### Incrementality

Related demo: [Incrementality Measurement](demos/incrementality-measurement/) connects evidence to conditional decisions using public cases, synthetic scenarios and a reproducible randomized-user analysis.

- [Incrementality, Bidding, and Attribution](https://research.facebook.com/publications/incrementality-bidding-and-attribution/) — Meta's case for incrementality testing over multi-touch attribution.

### Marketing Mix Modeling

- [Robyn](https://facebookexperimental.github.io/Robyn/) — Meta, open-source automated MMM.
- [Meridian](https://developers.google.com/meridian/docs/basics/meridian-introduction) — Google Bayesian MMM; experiment-informed priors, lag/saturation modeling and posterior uncertainty.
- [LightweightMMM](https://github.com/google/lightweight_mmm) — Historical resource; unsupported since the Meridian transition announced 2025-01-29.
- [PyMC-Marketing MMM](https://www.pymc-marketing.io/) — PyMC-Labs, Bayesian MMM with explicit priors.

### Attribution

Attribution assigns credit under a chosen rule or model. Use it for reporting and diagnostics; identifying incremental effects requires a suitable experiment or defensible causal assumptions. MMM is also assumption-dependent and is not automatically causal.

## Platforms and MLOps

The substrate that runs across every layer above: feature stores, ML platforms, experimentation infrastructure, governance.

### Feature Stores

- [Feast](https://github.com/feast-dev/feast) — Open-source feature store for training/serving consistency.
- [Tecton](https://www.tecton.ai/) — Commercial feature platform with real-time path.

### ML Platforms

- [MLflow](https://github.com/mlflow/mlflow) — Open-source experiment tracking and model registry.
- [Weights & Biases](https://wandb.ai/) — Commercial experiment tracking, evaluation, and observability.

### Governance

Record data lineage, allowed use, consent, deletion, access controls and model/policy versions across the stack. Warehouse controls and dedicated consent products can support this responsibility. Clean rooms limit data access; they do not automatically remove confounding or establish incremental impact.

---

# Part II — The Agent Era

Agents and workflows can connect responsibilities across the stack. Their ecosystem position, technical mechanism and delegated authority must be described separately.

## Four Forms of Marketing Agents

<div align="center">
<a href="assets/marketing-agent-classes.png"><img src="assets/marketing-agent-classes.png" alt="Four forms of marketing agents: platform automation, independent cross-surface agents, conversational/service agents and agent-mediated discovery; lifecycle decisioning and system descriptors span forms" width="1200"></a>
</div>

The original four categories are retained as **typical operational forms**: platform-owned automation, independent cross-surface agents, conversational/service agents and agent-mediated discovery. They describe ecosystem positions and workflows, and can overlap. A product can operate across channels, interact with customers and support discovery simultaneously. Record customer, task, data access, action control, technical mechanism, autonomy and evidence/maturity independently. See the [English essay](think/marketing-agent-classes.md) and [Chinese version](think/marketing-agent-classes.zh.md).

### Form 1 — Platform-Owned Automation

Automation inside an ad buying surface. Distinguish specific businesses that own user attention from businesses aggregating third-party supply; large groups may do both. Product descriptions below are navigation, not proof of causal performance.

**Owned attention:**

- [Google Performance Max / Smart Bidding](https://ads.google.com/home/campaigns/performance-max/) — Automated campaigns inside Google Ads.
- [Meta Advantage+](https://www.facebook.com/business/ads/meta-advantage-plus) — Automated campaign capabilities inside Meta surfaces.
- [Amazon Advertising](https://advertising.amazon.com/) — Sponsored advertising and DSP buying capabilities.
- [TikTok Smart+](https://ads.tiktok.com/business/en-US/blog/smart-plus-ai-powered-ad-solution) — TikTok campaign automation.
- [Tencent Ads](https://e.qq.com/) — Tencent-owned app inventory belongs here; external supply should be documented separately.
- [Alibaba Mama](https://www.alimama.com/) — Alibaba-owned commerce inventory belongs here; external-network business needs separate analysis.

**Aggregated supply and buying infrastructure:**

- [AppLovin](https://www.applovin.com/axon/) — Mobile-ad network and buying optimization reference.
- [Moloco](https://www.moloco.com/) — ML-based buying and retail-media infrastructure.
- [Mobvista / Mintegral](https://www.mobvista.com/) — Programmatic network and SSP/DSP infrastructure reference.
- [Criteo](https://www.criteo.com/) — Commerce-media and retargeting infrastructure reference.
- [The Trade Desk](https://www.thetradedesk.com/) — Independent DSP with buying control across exchanges; also fits independent orchestration.

Supply control and data access are potential advantages, not a profitability ranking. Compare gross versus net revenue, publisher payments, margins, retention and operating costs before drawing economic conclusions.

### Form 2 — Independent Cross-Surface Agents

External products integrating channels, business objectives and creative/operational workflows. Listed capability is public product positioning; quantitative outcomes require separate dated evidence and a baseline.

- [Albert.ai](https://albert.ai/) — Cross-channel advertising automation reference.
- [Ryze AI](https://ryze.ai/) — Advertising operations and optimization reference.
- [Jellyfish](https://www.jellyfish.com/) — Agency workflows and marketing operations reference.
- [Muze AI](https://muzeai.com/) — Advertising automation product reference.
- [Uplane](https://www.ycombinator.com/companies/uplane) — YC profile describes business-outcome-oriented marketing automation.
- [Absurd](https://www.ycombinator.com/companies/absurd) — AI creative/video advertising product reference.
- [Lapis](https://www.ycombinator.com/companies/lapis) — Current YC profile describes advertising creation and operation; earlier launch material describes AI-search analytics. Reviewed 2026-09-30; no supported claim of native ChatGPT ad placement.

### Form 3 — Conversational & Service Agents

Customer service, sales and proactive relationships can span conversations and time. Resolution, task correctness and incremental customer value need separate evaluation.

- [Sierra Horizon](https://sierra.ai/blog/horizon) — Vendor announcement dated 2026-07-16 describes proactive, long-horizon customer interactions; capability evidence does not prove business lift.
- [Decagon](https://decagon.ai/) — Customer-interaction agent reference.
- [Intercom Fin](https://www.intercom.com/fin) — Customer-service agent reference.
- [Cresta](https://cresta.com/) — Agent assistance and customer-interaction automation.
- [Ada](https://www.ada.cx/) — Customer-service automation reference.
- [Cognigy](https://www.cognigy.com/) — Contact-center conversational platform reference.
- [Parloa](https://www.parloa.com/) — Contact-center conversational platform reference.
- [Hermes](https://www.buildwithhermes.com/integrations) — Vendor-described voice-agent platform for agencies, combining voice providers, CRM and per-client billing; private-beta product reference, with unverified deployment and business effects; [source review](docs/community-resource-reviews.md#hermes), 2026-09-30.

### Form 4 — Agent-Mediated Discovery

Keep **answer visibility (GEO/AEO), human-facing ads in AI interfaces, agent-assisted purchases, and structured agent-to-agent exchanges** separate. Their audiences, permissions and evaluation methods differ.

- [Profound](https://www.tryprofound.com/) — AI-answer visibility product reference; mentions are not purchases.
- [Daydream](https://withdaydream.com/) — Search/content optimization reference; evaluate its specific workflow before assigning an AI-commerce role.
- [Scrunch AI](https://www.scrunchai.com/) — AI-discovery analysis and optimization reference.
- [Sitefire](https://www.ycombinator.com/companies/sitefire) — YC profile describes visibility analysis, content optimization and CMS actions, not paid AI-channel placement; reviewed 2026-09-30.

Discovery shifts are hypotheses to track, not proof that SEO/SEM must be entirely rewritten or that a category has no scale. Sample a defined query distribution repeatedly, record model/version, and connect visibility to qualified demand with an appropriate evaluation.

## Lifecycle Decisioning

First-party activation, retention, renewal and reactivation deserve explicit attention. Choose whether to contact, channel, time, frequency and offer under eligibility and consent constraints, then measure incremental long-term contribution and negative feedback.

- [BrazeAI Decisioning Studio](https://www.braze.com/product/brazeai-decisioning-studio) — Official documentation describes first-party data, custom KPIs, channel/incentive/frequency decisions and constraints; reviewed 2026-09-30. This spans several stack responsibilities and operational forms; vendor-described functionality is not independent efficacy evidence.
- [Hightouch AI Decisioning](https://hightouch.com/docs/ai-decisioning/overview) — Official documentation describes reinforcement-learning-based message/channel/timing decisions and connected delivery; reviewed 2026-09-30. The product’s agent terminology does not establish LLM-directed planning or general incremental lift.
- [Lifecycle Activation and Retention Playbook](playbooks/lifecycle-activation.md) — Rule baseline, no-contact control, eligibility, delayed outcomes and execution constraints.

## LLM Agent Leverage Points

Context-heavy strategy, creative iteration and tool-mediated customer work are plausible LLM use cases. Compare with fixed workflows, rules and human processes; measure quality, cost, latency and incremental value. Ecosystem position does not establish whether a product uses classical ML, LLMs or both.

**Two evaluation tracks:** (1) facts, policy compliance, tool correctness, idempotency, authorization and handoff; (2) incremental qualified sales, retention or contribution, with opt-outs, complaints and refunds. Commercial scale, task success and causal improvement cannot substitute for one another.

## Agent-Building Frameworks

- [LangGraph](https://github.com/langchain-ai/langgraph) — Graph-based agent orchestration; common substrate for multi-step marketing agents.
- [Claude Agent SDK](https://code.claude.com/docs/en/agent-sdk/overview) — Anthropic's SDK for tool-using agents; choose permissions and evaluations for the intended workflow.
- [OpenAI Responses API](https://developers.openai.com/api/docs/guides/migrate-to-responses) — Current agent/tool integration entry point, with Conversations for persistent state; Assistants API sunset 2026-08-26 per the [official migration guide](https://developers.openai.com/api/docs/assistants/migration). Reviewed 2026-09-30.
- [CrewAI](https://github.com/crewAIInc/crewAI) — Multi-agent role-based orchestration framework.
- [NotFair Plugin](https://github.com/nowork-studio/notfair-plugin) — MIT-licensed marketing skills for ads, GA4 and Search Console; live account operations depend on an OAuth-connected hosted MCP. Skills/tool integration reference, with unverified business effects; [source review](docs/community-resource-reviews.md#notfair-plugin), 2026-09-30.

## Frontier (2025/2026)

Research questions that cut across responsibilities. Dates describe the review horizon, not a guaranteed adoption forecast.

### Privacy and Measurement

Consent changes and limits on identifiers motivate experiments, aggregate models and controlled data collaboration. Clean rooms constrain access; they do not remove confounding. See Data and Measurement.

### Foundation Models on Customer Data

Tabular and sequence models may reduce modeling effort, but customer-event transfer, calibration and decision value must be validated on representative data. Compare with simple tabular baselines before adopting a foundation model.

### AI-Assisted Experimentation

Agents can draft hypotheses, check contracts and prepare creative tests. Keep randomization, estimands, exclusions, analysis code and approvals auditable; automated experiment generation can create multiple-testing and selection problems.

### Discovery and Agent Commerce

Structured product data, citations, AI-interface ads and authorized purchases create different opportunities. Distinguish observed capabilities from hypotheses about displacement and agent-to-agent markets. Measure consent, task completion, transaction errors and incremental business value separately.

---

# Part III — Applied and References

## Interactive Demos

- [Incrementality Measurement Demo](demos/incrementality-measurement/) — English interactive learning prototype: public evidence, NOVA scenario branches, experiment feasibility, auditable budget comparisons and a reproducible synthetic randomized-user analysis. No live integrations or advertising execution.

## Industry Playbooks

These are implementation guides, not claims of deployments by named companies. Each connects a business question to data, a baseline, method conditions, execution constraints, evaluation and failure criteria.

- [Lifecycle Activation and Retention](playbooks/lifecycle-activation.md) — Eligibility, no-contact controls, frequency, incremental contribution and delayed negative outcomes.
- [Conversational Sales and Service](playbooks/conversational-sales.md) — Customer state, authorized actions, handoff and separate task/business evaluations.
- [Cross-Channel Resource Allocation](playbooks/cross-channel-allocation.md) — Experiment/MMM roles, marginal response, uncertainty and staged budget execution.

### Production Research and Case Evidence

- [Google — Ad Click Prediction: a View from the Trenches](https://research.google/pubs/ad-click-prediction-a-view-from-the-trenches/) — KDD 2013 production CTR engineering; prediction quality is not intervention effectiveness.
- [Alibaba — Deep Interest Network](https://arxiv.org/abs/1706.06978) — Published ranking architecture and deployment discussion; evaluate targeting policies separately.
- [eBay — Paid Search Field Experiments](https://faculty.haas.berkeley.edu/stadelis/BNT_ECMA_rev.pdf) — Historical experiments distinguish intent from causal search-ad effects; effect sizes are context-specific.
- [Airbnb — 2020 Form 10-K](https://www.sec.gov/Archives/edgar/data/1559720/000155972021000010/airbnb-10k.htm) — Filed marketing expenditures and strategy, not a randomized estimate of channel return; see the Demo's [source ledger](demos/incrementality-measurement/sources.md).

Engineering portals such as [Uber](https://www.uber.com/blog/engineering/ai/) and [Meituan](https://tech.meituan.com/) are discovery starting points. Cite a specific article before attributing architecture or effects to a company. A company homepage alone does not establish a deployment case.

## Original Research and Notes

Long-form analyses written for this repository.

- [Four Forms of Marketing Agents](think/marketing-agent-classes.md) — Operational positions, control points and workflows with independent descriptors for customer, task, data, control, technology, autonomy and evidence; economic advantages are hypotheses to test. ([中文版 / Chinese version](think/marketing-agent-classes.zh.md))
- [The Five Layers as a Decision and Learning Cycle](think/five-layers-cognitive-cycle.md) — Functional responsibilities, provenance, action contracts and evidence with uncertainty; explains why logged feedback alone does not establish causal learning. ([中文版 / Chinese version](think/five-layers-cognitive-cycle.zh.md))

## Books

- [Trustworthy Online Controlled Experiments](https://experimentguide.com/) by Kohavi, Tang, Xu — Reference text for A/B testing at scale.
- [Lean Analytics](https://leananalyticsbook.com/) by Croll & Yoskovitz — The growth-funnel framing that still informs modern NBA.
- [Hooked](https://www.nirandfar.com/hooked/) by Nir Eyal — Behavioral mechanics behind retention and lifecycle design.
- [The Mom Test](http://momtestbook.com/) by Rob Fitzpatrick — How to learn what marketing should actually optimize for.
- [Marketing Metrics](https://www.amazon.com/Marketing-Metrics-Definitive-Measuring-Performance/dp/0137058292) by Farris, Bendle, Pfeifer, Reibstein — Canonical reference for metric definitions across marketing functions.

## Research Papers

### Foundational

- [Estimating Causal Effects of Treatments in Randomized and Nonrandomized Studies](https://doi.org/10.1037/h0037350) — Rubin (1974), a foundational treatment-effect reference; identification assumptions must match the application.
- [The Predictron](https://arxiv.org/abs/1612.08810) — DeepMind research on learned internal models for value prediction; a conceptual RL reference, not a demonstrated ad-pacing deployment.

### Recommender Systems

See [leoncuhk/recsys-papers](https://github.com/leoncuhk/recsys-papers) for a maintained list covering retrieval, ranking, sequential, and LLM-based recommendation.

### Ad Systems

- [Deep Interest Network](https://arxiv.org/abs/1706.06978), [DIEN](https://arxiv.org/abs/1809.03672), [DLRM](https://arxiv.org/abs/1906.00091), [DCN-V2](https://arxiv.org/abs/2008.13535).

### LLM Agents for Marketing (emerging)

- [Generative Agents: Interactive Simulacra of Human Behavior](https://arxiv.org/abs/2304.03442) — Research on simulated interactive characters; not evidence of a deployed marketing agent or incremental sales.
- [AgentBench](https://arxiv.org/abs/2308.03688) — Benchmarking agent capabilities; useful for agent evaluation in marketing tasks.

## Community and Conferences

### Communities

- [r/marketing](https://www.reddit.com/r/marketing/), [r/AdOps](https://www.reddit.com/r/adops/), [r/GrowthHacking](https://www.reddit.com/r/GrowthHacking/) — Reddit communities.
- [MeasureCamp](https://www.measurecamp.org/) — Unconference for measurement and experimentation practitioners.
- [Locally Optimistic](https://locallyoptimistic.com/) — Data and analytics community with strong Martech presence.

### Conferences

- [The MarTech Conference](https://martechconf.com/), [Iterable Activate](https://www.iterable.com/activate/), [Affiliate Summit](https://www.affiliatesummit.com/), [ACM SIGKDD](https://www.kdd.org/).

## Related Lists

- [awesome-quant-ai](https://github.com/leoncuhk/awesome-quant-ai) — Companion list for quantitative investment AI.
- [recsys-papers](https://github.com/leoncuhk/recsys-papers) — Recommender systems literature.
- [awesome-causal-inference](https://github.com/matteocourthoud/awesome-causal-inference) — Curated causal inference libraries, resources, and industry applications.
- [awesome-llm-apps](https://github.com/Shubhamsaboo/awesome-llm-apps) — General LLM app patterns; some relevant to agent design.

## Contributing

Contributions are welcome. This list is **curated, not comprehensive**. Additions need substantive relevance and claim-matched evidence; product capability, implementation, traction and causal impact are reviewed separately.

- Prefer open source, published work, or systems with disclosed traction.
- Disclose affiliation if you built it.
- One PR per resource or tightly related batch; format: `- [Name](url) — One-sentence description ending with a period.`

Include direct sources, evidence type, limitations and a review date for material claims. See [CONTRIBUTING.md](CONTRIBUTING.md) for the full guidelines.

---

<div align="center">

If you find this project useful, please consider giving it a star.

</div>
