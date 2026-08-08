# Governing a Software-Engineering Objective Across 53+ Hours of Active Execution

**An internal-production case study based on Build Ops**  
**Tony Guillaro | AI Systems & Forward-Deployed Engineer**  
**Public, non-proprietary work sample | Updated August 2026**

Build Ops is a bounded, long-running software-engineering and orchestration system that I designed, integrated into my development environment, and use in active internal production while building Nerva. It turns explicitly scoped objectives into governed, multi-stage work against a real codebase while preserving the durable operating state, evidence, and authority boundaries needed to keep extended execution accountable.

This case study explains the operational problem, design choices, and observed behavior without disclosing source code, internal component names, prompts, schemas, thresholds, topology, security mechanisms, or Nerva's proprietary architecture.

## The operational problem

Short coding-agent sessions can be useful, but meaningful engineering objectives rarely fit inside one uninterrupted prompt-and-response loop. Work spans repository discovery, dependency checks, planning, implementation, testing, runtime and browser verification, technical investigation, version-control operations, blockers, and resumed execution. As the runtime grows, so does the risk of context loss, silent scope drift, unsupported completion claims, unsafe actions, and an inability to explain what happened.

The problem I set out to solve was therefore not simply:

> How can an agent keep working longer?

It was:

> How can a software-engineering system make useful progress over extended periods while remaining bounded, inspectable, interruptible, traceable, and recoverable?

## What I put into production

I designed Build Ops to translate an explicit engineering objective into a governed work sequence that can include:

- repository and dependency preflight;
- planning and decomposition;
- implementation against the real codebase;
- automated tests and static validation;
- runtime and browser verification;
- Git and GitHub operations;
- technical investigation; and
- evidence-backed closeout.

The system is part of my day-to-day engineering workflow. It is not an unrestricted coding loop and it is not allowed to treat activity as completion. The objective, authority, available tools, execution budget, validation requirements, and consequential actions remain bounded throughout the operation.

## The governing design choices

### 1. Scope must remain explicit

Build Ops begins from a defined objective and acceptance posture rather than an open-ended instruction to improve a codebase. Work orders and finite execution and delegation budgets constrain how far the system may decompose or extend the assignment.

### 2. Capability is not authority

Tool availability does not grant blanket permission to use a tool in every way. Scoped access, command-safety controls, checkpoints, and human approval for consequential actions determine what the system may do during a particular operation.

### 3. Durable operating state must outlive any run

Persistent sessions and linked context and state handoffs preserve the explicitly scoped objective, active task, current action and its rationale, technical state, source changes, artifacts, decisions, validation evidence, execution history, and next safe action. A resumed run continues from known technical and operational state rather than reconstructing the objective from a conversational summary or depending on one continuously expanding conversation.

### 4. Execution cannot certify itself

Producing code or receiving a successful command response is not sufficient evidence of completion. Build Ops carries validation artifacts through the operation and supports independent checks of the resulting behavior before closeout.

### 5. A blocker is a controlled state, not a reset

When execution reaches a condition it cannot safely resolve within its authority, it stops at the boundary, exposes the blocker and retained evidence, and waits for intervention. Once the blocker is addressed, the same objective can resume from preserved state.

## Observed cumulative operation

At an August 8, 2026 snapshot, one current engineering objective had accumulated **53 hours, 49 minutes, and 44 seconds of active execution across linked runs**. The objective was still in progress, so 53+ hours is a recorded floor rather than a final total.

This is a cumulative record of active work on the same objective, not a claim that one process ran continuously or unattended. The total comes from turn-level runtime records covering reasoning, tool use, reviews, file work, and subagent coordination. Inactive gaps between runs are excluded, and parallel subagent work is included within run wall-clock time without being double-counted.

The duration itself is not the achievement. Throughout the operation, Build Ops retained the goal, active task, current action, prior decisions and changes, technical state, artifacts, validation evidence, execution history, and next safe action. I could inspect progress, stop or redirect the work, address blockers, and resume from a known state without silently changing the objective or discarding accountability.

Elapsed time alone does not determine progress or completion. Progress is represented by source-backed state, artifacts, decisions, validation evidence, and safe next actions. Completion requires evidence; the system cannot declare itself finished merely because it remained active or produced code.

## What this demonstrates

Build Ops demonstrates an approach to meaningful engineering autonomy that is:

- **Bounded:** explicit scope, authority, tools, and finite budgets limit the operation;
- **Stateful:** the objective, current work, evidence, and next safe action survive run boundaries;
- **Context-disciplined:** continuity comes from durable operating state and deliberate handoffs, not an indefinitely expanding conversation;
- **Observable:** progress, artifacts, decisions, tests, and execution records remain available for inspection;
- **Interruptible:** I can pause, stop, or redirect work when conditions change;
- **Traceable:** retained provenance connects the objective to changes, evidence, and decisions;
- **Recoverable:** blockers and resumed runs remain part of one durable operational history; and
- **Evidence-backed:** closeout depends on validation rather than agent narration alone.

The broader engineering lesson is that longer runtime is not the same as reliable autonomy. Extended operation becomes useful only when the system can retain truth, respect authority boundaries, expose uncertainty, stop safely, and resume from evidence-bearing state.

## My role

I designed the Build Ops architecture, framework, harness, and Nerva-specific governance model; integrated its runtime into my development environment; and operate it as part of my production engineering workflow. My work spans the system model, authority boundaries, execution controls, durable state and provenance, validation posture, operator oversight, and recovery path.

## Public scope and intellectual-property boundary

This case study presents verified operating behavior and product-level engineering reasoning only. It intentionally omits implementation details that would expose or enable reconstruction of Build Ops or Nerva, including source code, prompts, internal frameworks, services, schemas, policy ordering, thresholds, routes, infrastructure, security mechanisms, and proprietary orchestration logic.
