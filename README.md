
# RouteIQ
RouteIQ is an intelligent inference control plane that automatically routes each AI workload to the most suitable open model on Nebius Token Factory. It optimizes the complete inference transaction—prompt, model selection, output efficiency, cost, latency, and quality—while providing measurable evidence for every routing decision.
# RouteIQ

**Every workload deserves the right model.**

## Live Demo

-   **Live app:** https://route-wise-iq.lovable.app/
-   **Demo video --- RouteIQ: Cost Efficient Model Selection:**
    https://www.loom.com/share/0fb58bf696584561afbba466779e1ae9

RouteIQ is an evidence-driven AI inference control plane for open
models. It routes each workload to the least expensive / lowest-latency
eligible model that can satisfy the required quality, while escalating
to deeper reasoning only when necessary.

## Problem

AI products often send very different workloads through the same
high-capability model. A banking intent classification, a JSON
extraction task, a document review, and a difficult multi-step reasoning
problem do not necessarily need the same model. That creates hidden
inference waste: unnecessary cost, latency, and capability.

Open/open-weight models are not automatically free to serve. Hosted
inference still consumes GPU infrastructure and tokens, so model
selection has real economic consequences.

## Solution

RouteIQ sits between the application and **Nebius Token Factory**.

`Request → Capability Gate → Task/Complexity/Freshness → Evidence-aware Routing → Nebius Token Factory → Telemetry → Learning`

RouteIQ selects:

-   a routing profile: **Fast / Balanced / Deep**
-   an exact eligible Nebius model
-   whether current external retrieval is required
-   the most defensible quality/cost/latency trade-off based on
    available evidence

## Core features

-   **Auto routing** across eligible Nebius models
-   **Exact-model recommendation** with an explanation of why it was
    selected
-   **Live telemetry:** routing, retrieval, inference and total latency;
    input/output/total tokens
-   **Cost engine** using matched upstream-provider pricing references
-   **Quality × Cost** and **Quality × Latency** trade-off views
-   **Accuracy ranking** from RouteIQ's own benchmark runs
-   **Token efficiency** analysis
-   **Manual model challenge:** force another eligible model and compare
-   **Adaptive Routing Evidence:** learn bounded, workload-specific
    preferences
-   **Benchmark Lab:** BANKING77 and GSM8K
-   **Freshness gate:** Tavily only when current external information is
    actually required
-   **Persistent route history** for reproducible demo evidence

## Architecture

``` text
Customer App
    |
    v
RouteIQ
    |-- Capability Gate
    |-- Task Family
    |-- Complexity
    |-- Freshness Gate
    |-- Benchmark Evidence
    |-- Cost / Latency Evidence
    |-- Adaptive Routing Evidence
    |
    v
Nebius Token Factory
    |
    v
Response + Telemetry
    |
    +--> Runtime History
    +--> Benchmark Evidence
    +--> Business Impact
```

### Pricing provenance

Inference remains on **Nebius Token Factory**.

For the hackathon MVP, RouteIQ can enrich Nebius-discovered models with
pricing/context metadata referenced from the Requesty Nebius model
catalog:

`https://www.requesty.ai/models/nebius`

The UI should clearly distinguish:

-   **Inference:** Nebius Token Factory
-   **Pricing reference:** Requesty Nebius catalog
-   **Measured quality:** RouteIQ benchmark results
-   **Measured latency/tokens:** RouteIQ runtime telemetry
-   **User preference:** Adaptive Routing Evidence

Prices must never be guessed. Ambiguous or unmatched model versions
remain `Unavailable`.

## Benchmarks

### BANKING77

Banking customer-support intent classification across 77 intents. Used
to test whether simpler workloads can avoid unnecessary Deep inference
while retaining correctness.

### GSM8K

Multi-step mathematical reasoning. Used to test when escalation to a
stronger reasoning model is justified.

The central experiment compares:

1.  **Fast-only control**
2.  **Deep-only control**
3.  **RouteIQ Auto**

RouteIQ chooses its route before seeing benchmark ground truth.

## Key metrics

-   Quality retained
-   Estimated inference cost
-   Cost avoided vs Deep-only control
-   Average and P95 latency
-   Input / output / total tokens
-   Deep calls avoided while correct
-   Necessary escalations
-   Quality per dollar
-   Cost per correct answer
-   Routing corrections learned

## Adaptive Routing Evidence

A user can challenge RouteIQ's recommendation by forcing another
eligible model.

After both results exist, RouteIQ asks which response was better:

-   RouteIQ recommendation
-   Forced model
-   About the same

This feedback is stored as **workload-specific routing evidence**. It
adjusts future routing scores in a bounded way. RouteIQ does **not**
claim to train or fine-tune the underlying model.

## Demo flow

1.  Enter a simple banking-support request.
2.  RouteIQ recommends a profile and exact Nebius model.
3.  Inspect latency, tokens, cost and evidence.
4.  Open the model trade-off view.
5.  Force another eligible model.
6.  Compare both outputs and select the preferred result.
7.  Run BANKING77.
8.  Inspect Quality × Cost / Quality × Latency and Deep Calls Avoided.
9.  Run or inspect GSM8K to show necessary escalation.
10. Open Business Impact.

## Demo customer

**FinAssist AI** is a fictional B2B fintech SaaS demo customer with
mixed customer-support, research and operations workloads. The use case
illustrates how RouteIQ can avoid over-provisioned inference for simple
tasks while preserving escalation for complex reasoning.

## Product principle

> **Fast when sufficient. Deep when necessary.**

RouteIQ does not assume the biggest model is best for every request. It
measures routing decisions, exposes the trade-offs, and learns from
evidence.

## Hackathon scope

The MVP intentionally excludes:

-   authentication / organizations
-   billing and subscriptions
-   multi-provider inference
-   fine-tuning
-   custom model hosting
-   vector database / complex RAG
-   voice agents / avatars / TTS
-   expensive 3D visualization

The focus is a small, credible and measurable routing control plane
centered on Nebius Token Factory.

## Presentation

Project lead: **Hossam Elshahaby**

Pitch deck: `RouteIQ_Hackathon_Pitch.pptx`\
Project description: `RouteIQ_Project_Description.pdf`
