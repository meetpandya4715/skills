---
name: repo-x-ray
description: Inspect a software repository and generate a comprehensive, evidence-backed Mermaid diagram set for fast orientation and deeper understanding. Use when analyzing an unfamiliar codebase, explaining architecture to a human, preparing onboarding material, reviewing repo structure and execution flow, or mapping apps, services, monorepos, SDKs, CLIs, event-driven systems, data pipelines, ML repos, or infrastructure/devtool repositories. Save the final analysis as Markdown plus rendered SVG diagram files inside the analyzed repository.
---

# Repo X-Ray

Inspect the repository before drawing anything. Generate a comprehensive set of diagrams that gives a human an accurate mental model quickly and then fills in the important deeper views.
Explore broadly across the repo's applicable diagram families, ground every diagram in repo evidence, and skip output only when it is redundant or weakly supported.

## Core Principles

1. Inspect before diagramming.
2. Prefer coarse structure before deep detail.
3. Ground claims in code and config, not folder names alone.
4. Generate comprehensive coverage of distinct, evidence-backed diagram types automatically.
5. Do not ask the user which diagrams to include.
6. Add deep diagrams only when they answer a distinct question.
7. Prefer multiple scoped diagrams over one dense graph.
8. Mark inferred structure clearly instead of presenting it as fact.

## Diagramming Workflow

1. Inspect the repository.
2. Classify the repo into one or more archetypes.
3. Build a candidate diagram list.
4. Generate core-coverage diagrams for system boundary, internal structure, repo responsibility, and main execution path.
5. Expand with every additional diagram type that is materially supported by the repo and answers a distinct question.
6. Skip any diagram that is redundant, weakly supported, or mostly repeats another diagram in a different format.

### Core-Coverage Selection Rule

Start with diagrams that cover:
- system boundary
- major internal structure
- repo, package, or module responsibility
- main execution path

There is no fixed diagram cap. After core coverage is complete, keep adding diagrams as long as each one reveals a materially different aspect of the repository.

### Expansion Rule

Add an additional diagram whenever it answers a question the existing diagram set does not already answer, such as:
- how routes map to handlers
- how auth actually works
- how events and workers interact
- how training differs from inference
- how packages depend on each other in a monorepo
- how deployment topology differs from code structure

If an additional diagram mostly restates another diagram, skip it.

## Inspection Protocol

Inspect deliberately and stop when you have enough evidence to explain the repo well. Do not scan the entire tree by default.

### 1. Inspect High-Signal Files First

Inspect these first when present:
- `README` and top-level docs
- package manifests such as `package.json`, `pyproject.toml`, `Cargo.toml`, `go.mod`
- workspace config such as `pnpm-workspace.yaml`, `turbo.json`, `nx.json`
- build and toolchain config
- Dockerfiles and compose files
- deployment and infra files
- CI workflows

Treat these files as informative but not definitive. Docs may be stale. Manifests show dependencies, not active runtime usage.

### 2. Identify Real Entry Points

Find where execution begins:
- frontend bootstrap files
- server startup files
- route definitions
- CLI entry points
- worker or job runners
- schedulers or cron registrations
- training scripts
- inference or serving startup files

Entry points matter more than directory names.

### 3. Map Structural Boundaries

Determine the responsibility of:
- top-level packages and directories
- apps versus packages versus shared libraries
- domain modules
- adapters and integrations
- generated code areas
- config-heavy areas
- tests, scripts, examples, and benchmarks

Do not mistake a folder tree for architecture. Identify what each area is for.

### 4. Verify Runtime Wiring from Code

Inspect actual execution paths:
- request flow
- route-to-handler mapping
- service wiring
- provider and dependency setup
- event publication and consumption
- background job dispatch
- model loading and invocation
- plugin registration
- middleware and auth chains

Use runtime wiring to validate whether the documented architecture is real.

### 5. Inspect Persistence and Contracts

Look for:
- schema definitions
- migrations
- ORM models
- GraphQL schemas and resolvers
- OpenAPI specs
- gRPC or protobuf definitions
- DTOs and contract types
- storage abstractions

Persistence and contracts often reveal the true system shape.

### 6. Inspect Operational Behavior

Look for:
- env and config loading
- feature flags
- secret providers
- CI and CD workflows
- infrastructure manifests
- observability hooks
- retry and failure handling
- health and readiness checks

Operational complexity often lives outside the main application code.

### 7. Separate Training from Inference When Relevant

For ML and data repos, inspect separately:
- ingestion and preprocessing
- training entry points
- evaluation paths
- checkpoint and export logic
- inference and post-processing
- experiment tracking and artifact storage

Do not assume the training graph explains production inference.

### 8. Record Evidence Strength

Tag architectural claims as:
- `explicit`: directly visible in code or config
- `inferred`: likely from conventions or naming, but not directly proven
- `uncertain`: plausible but weakly supported

Prefer fewer diagrams and stronger caveats when evidence is thin.

## Exclusions and Noise Control

Unless they are central to the repo's behavior, skip or deprioritize:
- `node_modules`
- build outputs such as `dist`, `build`, `.next`, `.turbo`, `coverage`
- vendored dependencies
- generated clients and compiled assets
- caches and temp directories
- huge fixture or snapshot directories
- lockfiles beyond quick dependency confirmation

Do not let generated or third-party material dominate the analysis.

## Repo Classification

Classify the repo into one or more of these archetypes:
- frontend application
- backend service or API
- full-stack application
- library or SDK
- CLI tool
- monorepo
- event-driven or worker-based system
- data pipeline or ETL
- ML training repo
- ML inference or serving repo
- infrastructure, platform, or devtool repo
- plugin or extension framework

Use classification to guide candidate diagrams, not to force mandatory ones.

## Candidate Diagram Types

### Core Diagrams
These are the main core-coverage candidates:
1. `System Context`
2. `High-Level Architecture`
3. `Repo Structure / Responsibility Map`
4. `Main Runtime Flow`
5. `Primary Sequence Diagram`

Do not treat all five as mandatory. Include the ones the repo supports, then continue into the other categories below whenever they reveal additional structure.

### Frontend-Focused Diagrams
- `Route / Navigation Map`
- `Component Hierarchy`
- `Frontend State / Data Flow`

### Backend and Service Diagrams
- `API Surface / Route-to-Handler Map`
- `Layer / Boundary Diagram`
- `Data Model / ER Diagram`
- `Auth / Authorization Flow`

### Async and Worker Diagrams
- `Event / Message Flow`
- `Job Orchestration / Worker Flow`
- `State Machine`

### Library, SDK, and Framework Diagrams
- `Public API Surface`
- `Extension Point / Plugin Architecture`
- `Class / Interface Relationships`

### CLI Diagrams
- `Command Hierarchy`
- `CLI Execution Flow`

### Monorepo Diagrams
- `Workspace / Package Relationship`
- `Ownership / Boundary Map`

### Data and ML Diagrams
- `Data Lineage / Transformation Pipeline`
- `Training Pipeline`
- `Inference Pipeline`
- `Model Composition`
- `Experiment / Artifact Lifecycle`

### Operations Diagrams
- `Deployment / Runtime Topology`
- `CI / CD Pipeline`
- `Config / Environment Dependency`
- `Observability / Error Path`

## Diagram Selection Rules

Start from these questions:
1. What system boundary matters most?
2. What are the major internal pieces?
3. How is the repo organized by responsibility?
4. What is the main execution path?

Generate every distinct diagram that is materially supported by the repo and answers a different explanatory question. Do not impose a fixed numeric cap.

### Typical Core-Coverage Defaults
Treat these as starting points, not requirements or limits:
- deployable application: `System Context`, `High-Level Architecture`, `Main Runtime Flow`, `Repo Structure / Responsibility Map`
- library or SDK: `Public API Surface`, `High-Level Architecture`, `Repo Structure / Responsibility Map`, `Main Runtime Flow` for representative usage
- CLI tool: `Command Hierarchy`, `CLI Execution Flow`, `Repo Structure / Responsibility Map`, optional `System Context` if it integrates with external systems
- monorepo: `Workspace / Package Relationship`, `Ownership / Boundary Map`, `Repo Structure / Responsibility Map`, one runtime or architecture diagram for the most important app or service

### Redundancy Rules
Avoid generating both of these unless they reveal materially different information:
- `Main Runtime Flow` and `Primary Sequence Diagram`
- `High-Level Architecture` and `Layer / Boundary Diagram`
- `Repo Structure / Responsibility Map` and `Workspace / Package Relationship`
- `API Surface` and `Command Hierarchy`

If two diagrams answer the same question, keep the clearer one.

### Deep-Diagram Triggers
Generate deep diagrams when the repo clearly contains the relevant structure:
- frontend-heavy repo: routes, screens, state stores, server-state or client-state architecture
- backend-heavy repo: routes, handlers, domain layers, persistence, auth
- event-driven repo: brokers, topics, queues, workers, retries, DLQs
- framework repo: public exports, stable extension points, important abstractions
- ML repo: distinct training and inference paths, multi-stage model composition, artifacts
- ops-heavy repo: real deployment manifests, release workflows, config-driven behavior, observability plumbing

## Diagram-Type Guidance

Prefer these Mermaid mappings:
- `flowchart TD` or `flowchart LR` for architecture, flow, workspace, deployment, CI/CD, and config
- `sequenceDiagram` for time-ordered interactions
- `classDiagram` for object-oriented relationships
- `erDiagram` for entities and schemas
- `stateDiagram-v2` for lifecycle and status transitions

Keep quality high:
- give every diagram a clear title
- answer one main question per diagram
- keep labels short
- use consistent naming
- distinguish internal and external systems
- split dense diagrams instead of forcing one large graph

Use roughly 6-12 nodes for overview diagrams and 8-20 nodes for medium-detail diagrams. Split diagrams when readability breaks down.

## Inspection Targets by Diagram

Before generating a diagram, inspect the evidence most relevant to it.
- `System Context`: docs, integration code, service clients, env, infra manifests
- `High-Level Architecture`: entry points, top-level modules, routing, service wiring, major adapters
- `Repo Structure / Responsibility Map`: top-level layout, workspace config, entry points, scripts, tests, generated areas
- `Main Runtime Flow`: representative entry point, main use-case path, side effects, outputs
- `Primary Sequence Diagram`: exact scenario chosen, ordering in code, async boundaries, retries
- `Route / Navigation Map`: router config, page and layout files, protected-route logic
- `Component Hierarchy`: key screens, containers, shared UI packages, composition
- `Frontend State / Data Flow`: stores, contexts, query hooks, mutations, fetch utilities
- `API Surface`: route definitions, handlers, middleware, validation, service calls
- `Layer / Boundary Diagram`: actual dependency direction, boundaries, adapters, services, repositories
- `Data Model / ER Diagram`: schema, migrations, ORM models, repositories, domain entities
- `Auth / Authorization Flow`: login flow, session or token handling, middleware, provider integration, role checks
- `Event / Message Flow`: broker config, producer and consumer code, topic or queue names, retries, DLQ handling
- `Job Orchestration / Worker Flow`: scheduler registrations, dispatch code, workers, artifact handling
- `State Machine`: explicit statuses, transition logic, retry, cancellation, failure handling
- `Public API Surface`: exports, public modules, SDK entry points, examples
- `Extension Point / Plugin Architecture`: registries, middleware, provider interfaces, registration points
- `Class / Interface Relationships`: important abstractions only, interfaces, base classes, implementations
- `Command Hierarchy`: CLI registration, parser definitions, command groups
- `CLI Execution Flow`: one representative command from parse to side effects
- `Workspace / Package Relationship`: workspace config, package boundaries, internal dependencies
- `Ownership / Boundary Map`: domain split, shared packages, dependency direction
- `Data Lineage`: ingestion, transforms, intermediate artifacts, derived outputs
- `Training Pipeline`: configs, trainers, augmentation, dataloaders, checkpoints, evaluation
- `Inference Pipeline`: serving code, preprocess, model load, postprocess, response contract
- `Model Composition`: multi-stage orchestration, retrieval, reranking, planners, workers, ensembles
- `Experiment / Artifact Lifecycle`: config sources, run tracking, checkpoints, exports, reports
- `Deployment / Runtime Topology`: Docker, Kubernetes, Helm, Terraform, functions, ingress, network boundaries
- `CI / CD Pipeline`: workflow files, release scripts, artifact publishing, deploy steps
- `Config / Environment Dependency`: env loaders, config files, feature flags, secret providers, runtime consumers
- `Observability / Error Path`: logs, metrics, traces, retries, dead letters, alerts, health checks

## Output Contract

Produce output in this order.

Persist outputs to disk inside the analyzed repository:
- `docs/repo-xray/report.md`: full written report including the same Mermaid blocks shown in the response
- author each diagram as Mermaid first and keep that Mermaid source only inside `report.md`
- render each diagram to SVG after authoring the Mermaid block in `report.md`
- when rendering Mermaid to SVG with `mmdc`, prefer a white background by default, for example `--backgroundColor white`, unless the user explicitly requests a different background
- `docs/repo-xray/diagrams/NN-short-name.svg`: one rendered SVG file per diagram, ordered to match the report
- do not leave separate `.mmd` files behind; `report.md` is the canonical Mermaid source
- create `docs/repo-xray` and `docs/repo-xray/diagrams` if they do not exist
- overwrite prior `repo-xray` outputs for the same repo rather than creating ambiguous duplicates
- mention the saved paths in the final response

### A. Repo Summary
Include:
- repo type or types
- main purpose
- main entry points
- major technologies
- key subsystems
- major external integrations

### B. Inspection Summary
Include:
- the files and areas that were most informative
- what was explicit versus inferred
- what remains uncertain

### C. Chosen Diagram Set
List:
- which diagrams were selected for core coverage
- which additional diagrams were added beyond core coverage
- why each one was selected
- which candidates were skipped because they were redundant, weakly supported, or low value

### D. Diagrams
Use the same schema for every diagram:

```md
### <Diagram Title>
- Type: <flowchart | sequenceDiagram | classDiagram | erDiagram | stateDiagram-v2>
- Question answered: <the main question this diagram answers>
- Why included: <why this repo needs this diagram>
- Scope: <what is included and excluded>
- What to notice first: <the main takeaway>
- Evidence basis:
  - Explicit: <facts directly visible in code or config>
  - Inferred: <reasonable inferences, if any>
  - Uncertain: <weakly supported points, if any>
- Confidence: <high | medium | low>

```mermaid
...
```

Short interpretation: <2-4 sentences>
```

### E. Final Synthesis
Summarize:
- how the repo is structured
- what the main execution path is
- where complexity is concentrated
- what a new contributor should read first

## Recommended Coverage Bundles

Use these defaults only when they fit. Start here, then continue generating any additional diagram types that the repo clearly supports and that explain a distinct aspect of the system.

### Small Utility or Tiny Repo
- `Repo Structure / Responsibility Map`
- `Main Runtime Flow`
- optional `Public API Surface` or `CLI Execution Flow`

### Backend API Service
- `System Context`
- `High-Level Architecture`
- `Main Runtime Flow`
- `API Surface / Route-to-Handler Map`
- optional `Data Model / ER Diagram` or `Auth / Authorization Flow`

### Frontend App
- `System Context`
- `High-Level Architecture`
- `Route / Navigation Map`
- `Main Runtime Flow`
- optional `Frontend State / Data Flow`

### Full-Stack App
- `System Context`
- `High-Level Architecture`
- `Main Runtime Flow`
- `Repo Structure / Responsibility Map`
- optional one of `Route / Navigation Map`, `API Surface`, or `Deployment / Runtime Topology`

### Library or SDK
- `Public API Surface`
- `High-Level Architecture`
- `Repo Structure / Responsibility Map`
- `Main Runtime Flow` for representative usage
- optional `Extension Point / Plugin Architecture`

### CLI Tool
- `Command Hierarchy`
- `CLI Execution Flow`
- `Repo Structure / Responsibility Map`
- optional `Config / Environment Dependency` or `System Context`

### Monorepo
- `Workspace / Package Relationship`
- `Ownership / Boundary Map`
- `Repo Structure / Responsibility Map`
- one runtime or architecture diagram for the most important app or service
- optional `System Context` if the repo exposes a clear deployable system boundary

### Event-Driven System
- `System Context`
- `High-Level Architecture`
- `Event / Message Flow`
- `Job Orchestration / Worker Flow`
- optional `State Machine`

### ML Training Repo
- `High-Level Architecture`
- `Data Lineage / Transformation Pipeline`
- `Training Pipeline`
- `Experiment / Artifact Lifecycle`
- optional `Model Composition`

### ML Inference or Serving Repo
- `System Context`
- `High-Level Architecture`
- `Inference Pipeline`
- `Deployment / Runtime Topology`
- optional `Observability / Error Path`

### Data Pipeline or ETL Repo
- `System Context`
- `Data Lineage / Transformation Pipeline`
- `Job Orchestration / Worker Flow`
- `Repo Structure / Responsibility Map`
- optional `Deployment / Runtime Topology`

## Final Quality Checklist

Before finalizing, verify:
- inspection happened before diagram generation
- all materially supported, non-redundant diagram families were considered
- no arbitrary numeric cap constrained the output
- each diagram answers a distinct question
- no diagram is overloaded
- generated and vendored code did not dominate the analysis
- training and inference are separated when relevant
- runtime topology and code architecture are not conflated
- inferred relationships are marked clearly
- the result would help a new engineer understand where to start

If not, revise.

## Invocation Template

When asked to analyze a repo, follow this instruction:

> Analyze the repository and generate a comprehensive, evidence-backed diagram set for understanding it. Inspect high-signal files, real entry points, architectural boundaries, runtime wiring, persistence or contracts, and operational behavior. Separate explicit evidence from inferred structure. Classify the repo, generate core-coverage diagrams automatically, and then add every additional diagram type that is materially supported by the repo and answers a distinct question not already covered. Prefer scoped diagrams over dense graphs. Do not ask the user which diagrams to include. Do not generate diagrams that are redundant or weakly supported by the repo. When converting Mermaid diagrams to SVG with `mmdc`, prefer a white background unless the user explicitly requests otherwise.
