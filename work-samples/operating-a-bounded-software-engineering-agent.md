# Operating a Bounded Software-Engineering Agent for 26.4 Hours

**An internal-production case study based on Build Ops**  
**Tony Guillaro | AI Systems & Forward-Deployed Engineer**  
**Public, non-proprietary work sample | August 2026**

Build Ops is a bounded, long-running software-engineering and orchestration system that I designed, integrated into my development environment, and use in active internal production while building Nerva. It turns explicitly scoped objectives into governed, multi-stage work against a real codebase while preserving the evidence, state, and authority boundaries needed to keep extended execution accountable.

This case study explains the operational problem, design choices, and observed behavior without disclosing source code, internal component names, prompts, schemas, thresholds, topology, security mechanisms, or Nerva's proprietary architecture.

## The operational problem

Short coding-agent sessions can be useful, but meaningful engineering objectives rarely fit inside one uninterrupted prompt-and-response loop. Work spans repository discovery, dependency checks, planning, implementation, testing, runtime and browser verification, technical investigation, version-control operations, blockers, and resumed execution. As the runtime grows, so does the risk of context loss, silent scope drift, unsupported completion claims, unsafe actions, and an inability to explain what happened.

The problem I set out to solve was therefore not simply:

> How can an agent keep working longer?

It was:

> How can a software-engineering agent make useful progress over extended periods while remaining bounded, inspectable, interruptible, traceable, and recoverable?

## What I put into production

I designed Build Ops to translate an explicit engineering objective into a governed work sequence that can include:

- repository and dependency preflight;
- planning and decomposition;
- implementation against the real codebase;
- automated tests and static validation;
- runtime and browser verification;
- Git and GitHub operations;
- technical investigation;
- evidence-backed closeout.

The system is part of my day-to-day engineering workflow. It is not an unrestricted coding loop and it is not allowed to treat activity as completion. The objective, authority, available tools, execution budget, validation requirements, and consequential actions remain bounded throughout the operation.

## The governing design choices

### 1. Scope must remain explicit

Build Ops begins from a defined objective and acceptance posture rather than an open-ended instruction to improve a codebase. Work orders and finite execution and delegation budgets constrain how far the system may decompose or extend the assignment.

### 2. Capability is not authority

Tool availability does not grant blanket permission to use a tool in every way. Scoped access, command-safety controls, checkpoints, and human approval for consequential actions determine what the system may do during a particular operation.

### 3. State must survive the session

Persistent sessions, linked context handoffs, work orders, source changes, test results, decisions, validation records, and execution logs preserve the operation across checkpoints and blockers. A resumed run continues from retained technical and operational state rather than reconstructing the objective from a conversational summary.

### 4. Execution cannot certify itself

Producing code or receiving a successful command response is not sufficient evidence of completion. Build Ops carries validation artifacts through the operation and supports independent checks of the resulting behavior before closeout.

### 5. A blocker is a controlled state, not a reset

When execution reaches a condition it cannot safely resolve within its authority, it stops at the boundary, exposes the blocker and retained evidence, and waits for intervention. Once the blocker is addressed, the same objective can resume from preserved state.

## Observed extended operation

In one observed engineering objective, Build Ops executed across three governed segments:

| Segment | Continuous execution | Transition |
|---|---:|---|
| 1 | 12.5 hours | Reached a blocker and stopped |
| 2 | 7.0 hours | Resumed after intervention; reached a subsequent blocker |
| 3 | 6.9 hours | Resumed again from retained state |
| **Total** | **26.4 hours** | **One bounded objective across three linked segments** |

The important result was not simply the duration. The system preserved the objective, working context, artifacts, decisions, validation evidence, and execution history across both interruptions. I could inspect progress, address each blocker, redirect or stop the operation if necessary, and resume without discarding accountability or starting over.

## What this demonstrates

Build Ops demonstrates an approach to meaningful engineering autonomy that is:

- **Bounded:** explicit scope, authority, tools, and finite budgets limit the operation;
- **Observable:** progress, artifacts, decisions, tests, and execution records remain available for inspection;
- **Interruptible:** I can pause, stop, or redirect work when conditions change;
- **Traceable:** retained provenance connects the objective to changes, evidence, and decisions;
- **Recoverable:** blockers and resumed runs remain part of one durable operational history;
- **Evidence-backed:** closeout depends on validation rather than agent narration alone.

The broader engineering lesson is that longer runtime is not the same as reliable autonomy. Extended operation becomes useful only when the system can retain truth, respect authority boundaries, expose uncertainty, stop safely, and resume from evidence-bearing state.

## My role

I designed Build Ops's architecture and Nerva-specific governance model, integrated its runtime into my development environment, and operate it as part of my production engineering workflow. My work spans the system model, authority boundaries, execution controls, state and provenance behavior, validation posture, operator oversight, and recovery path.

## Public scope and intellectual-property boundary

This case study presents verified operating behavior and product-level engineering reasoning only. It intentionally omits implementation details that would expose or enable reconstruction of Build Ops or Nerva, including source code, prompts, internal frameworks, services, schemas, policy ordering, thresholds, routes, infrastructure, security mechanisms, and proprietary orchestration logic.
