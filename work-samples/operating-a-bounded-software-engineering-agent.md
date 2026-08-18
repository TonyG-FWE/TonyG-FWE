# Designing and Operating a Governed AI Engineering System

**An engineering reasoning and operational-validation brief based on Build Ops**  
**Tony Guillaro | Founder | Product, Systems & Agentic AI Engineer**  
**Public, non-proprietary work sample | Updated August 2026**

Build Ops is an active internal-production, bounded software-engineering and orchestration system that I designed, integrated into my development environment, and use while building Nerva. It carries explicitly scoped objectives through real, multi-stage engineering work while preserving the operating state, authority boundaries, evidence, and recovery context required to keep extended execution accountable across linked runs.

Build Ops is not Nerva, is not Nerva's core product architecture, and is not a generic coding-agent loop. The framework, harness, and governed operating model are the engineering achievement. Extended runtime is evidence that the model works; keeping a model active for a long time is not the objective.

This brief explains why I had to build the system, the recurring failures it addresses, the public-safe operating model I implemented, how I validate it under real engineering conditions, and what the work demonstrates about production agent infrastructure.

It deliberately omits source code, prompts, internal component names, schemas, policy ordering, thresholds, topology, security mechanisms, deployment details, and proprietary orchestration logic.

## What Build Ops is

**Build Ops is a governed engineering-execution system for carrying a defined software objective across investigation, planning, implementation, validation, runtime verification, version-control operations, interruption, and recovery without allowing the work to lose its scope, state, or accountability when agents, tools, and sessions change.**

It can coordinate work against a real codebase that includes:

- repository and dependency preflight;
- technical investigation;
- planning and decomposition;
- implementation;
- automated testing and static validation;
- runtime and browser verification;
- Git and GitHub operations;
- artifact and evidence capture;
- blocker handling; and
- evidence-backed closeout.

The system is part of my day-to-day engineering environment. It is not an unrestricted instruction to keep coding, and it cannot treat activity, generated code, or a successful command response as proof that the objective has been completed.

## Why I had to build it

Short coding-agent sessions can be useful. Meaningful engineering objectives are different.

Real work spans repository discovery, dependencies, competing implementation paths, architectural decisions, code changes, tests, runtime behavior, browser behavior, version-control state, failures, blocked dependencies, review findings, corrections, and resumed execution. Once that work crosses multiple runs, agents, tools, and context windows, the primary problem is no longer code generation.

The first thing that repeatedly broke was **continuity and operational truth**.

Existing systems would:

- lose constraints between sessions;
- drift from the original objective;
- operate on stale repository or dependency assumptions;
- repeat investigation or discard prior decisions;
- collide with parallel or resumed work;
- continue after a blocker without sufficient authority or evidence;
- mistake a running process for healthy progress;
- treat generated code, a passing command, or a confident summary as completion; or
- stop without preserving enough accountable state to resume safely.

The apparent solution was often a longer prompt, larger context window, another summary, or another retry. Those approaches delayed the failure without solving it.

Through repeated use, failure, repair, and rebuilding, I concluded that the missing capability was not a better loop. It was an operating model for governed engineering continuity.

## The engineering question

> How can an AI-assisted software-engineering system make useful progress across extended, multi-stage work while remaining bounded, coordinated, inspectable, interruptible, traceable, recoverable, and evidence-backed?

That question changes the architecture.

The center of the system cannot be the conversation. It has to be the accountable engineering objective and the durable state required to carry it safely from intent to verified result.

## 1. Start with failure modes, not longer runtime

I began by separating failure modes that ordinary coding-agent workflows often blur:

- A prompt is not a durable objective.
- A task assignment is not execution authority.
- Tool availability is not permission to use every command or surface.
- A plan is not implementation.
- A running agent is not necessarily healthy.
- A heartbeat is not proof of progress.
- A reported change is not a verified repository state.
- Generated code is not a validated outcome.
- A passing test is not proof that the complete objective is satisfied.
- A checkpoint is not automatically a safe resume point.
- Parallel work is not coordinated merely because multiple agents are active.
- A stopped process is not a recovered operation.
- A released work boundary is not completion.

These distinctions matter more as execution becomes longer, more parallel, more autonomous, or more consequential.

## 2. Convert the failure map into invariants

From that failure map, I defined a set of operating rules the system should not be allowed to blur.

### 1. The objective must remain explicit

Build Ops begins from a bounded objective, defined scope, exclusions, acceptance posture, and evidence requirements. The system is not authorized to improve the repository generally or silently expand the assignment because it finds adjacent work.

### 2. Work state must outlive every model session

The objective, active work, technical state, decisions, artifacts, evidence, blockers, and next safe action cannot depend on one conversation remaining available or understandable.

### 3. Capability must remain separate from authority

An agent or tool may be capable of modifying a file, running a command, changing a branch, or interacting with GitHub without being authorized to do so in the current operation.

### 4. Active work must be coordinated, not merely concurrent

Multiple agents, resumed runs, and human changes can collide. Safe concurrency requires explicit ownership, dependency awareness, bounded work surfaces, and consistency checks across active work.

### 5. Progress must be source-backed

Agent narration, elapsed time, and status labels do not manufacture progress. Progress must be represented by inspectable technical state, artifacts, decisions, tests, runtime evidence, or resolved blockers.

### 6. Execution cannot certify itself

The actor producing the work cannot be the only judge of whether the work is correct, complete, or safe. Closeout requires evidence appropriate to the exact completion claim and, where necessary, independent validation.

### 7. Blockers and uncertainty are controlled states

A blocker is not a reason to forget the operation or improvise outside its boundaries. Contradiction, missing evidence, stale state, unclear ownership, and failed validation must be able to stop the work without destroying continuity.

### 8. Safe resumption requires reconciliation

Reloading context is not enough. Before work resumes, the system must reconcile the preserved objective and decisions against the current repository, dependencies, active work, tool state, evidence, and remaining authority.

### 9. Completion must be evidence-backed

The system may report partial progress, unresolved risk, or insufficient evidence. It may not convert activity into completion for the sake of a clean status.

## 3. Organize the engineering operation around one accountable chain

At a public-safe level, the operating chain is:

**Explicit objective -> preflight -> investigation -> plan and bounded work assignment -> implementation -> automated validation -> runtime or browser verification -> evidence review -> closeout, correction, or recovery**

The stages can overlap or repeat, but their meanings remain distinct.

A plan does not prove code was written. A code change does not prove runtime behavior. A passing command does not prove the requested outcome. Evidence can support a completion claim, but it does not retroactively authorize an action that was outside scope.

This separation lets the system adapt without losing accountability.

## 4. Preserve durable operating state across linked runs

Build Ops does not depend on keeping one model inside an indefinitely expanding conversation.

Across linked runs, it preserves the durable state needed to continue from a known technical and operational position, including:

- the explicitly scoped objective;
- the active task and current action;
- why the current action is being taken;
- current repository, dependency, and runtime state;
- prior decisions and changes;
- artifacts and provenance;
- blockers and dependencies;
- validation evidence and unresolved findings;
- execution and handoff history; and
- the next safe action.

This allows an operation to stop completely and later resume without silently rewriting the goal, reconstructing the work from a conversational summary, repeating completed investigation, or discarding prior decisions.

The model can change. The session can end. A tool can become unavailable. The accountable objective and its evidence-bearing state remain.

## 5. Add an air-traffic-control function for active engineering work

Durable memory alone is not enough once work becomes multi-run or multi-actor.

A long-running engineering system needs an **air-traffic-control function** for the codebase: a way to know who or what is working on which surface, under what scope, with which dependencies, from which technical state, and with what evidence of liveness and progress.

At the public-safe level, Build Ops uses concepts such as:

- explicit ownership of affected repository and runtime surfaces;
- scoped work records binding the objective, dependencies, allowed and forbidden operations, and acceptance criteria;
- bounded execution, delegation, retry, and handoff budgets;
- liveness and progress records with stale-run or stall detection;
- checkpoints and accountable resume records;
- consistency validation across active-work records;
- retained evidence linking assignments, changes, tests, and reviews; and
- fail-closed behavior when ownership, state, dependencies, or evidence are contradictory or stale.

The governing distinctions are deliberate:

- Assigned is not launched.
- Launched is not running.
- Running is not healthy.
- A heartbeat is not progress.
- Reported progress is not proof.
- A work boundary is not authority.
- A released boundary is not completion.
- One valid record does not make the overall active state coherent.

This control function reduces collision, duplicate work, dependency bypass, stale continuation, split-brain implementation, and unsupported completion claims without forcing all work through one serial bottleneck.

## 6. Bound tools, commands, surfaces, and budgets

Build Ops treats engineering capability as something that must be scoped for the current objective.

The system can constrain:

- which repositories, branches, worktrees, files, services, or runtime surfaces are eligible;
- which tools and command classes may be used;
- how far an objective may be decomposed;
- how many retries, handoffs, or delegated work paths are allowed;
- which actions require a checkpoint or human approval; and
- which blockers require fail-closed escalation rather than improvisation.

Human approval remains required before consequential or irreversible actions outside the standing authority of the operation.

The goal is not to ask for approval on every low-risk step. It is to prevent convenience, tool availability, or agent confidence from silently expanding authority.

## 7. Validate behavior, not merely generated code

Build Ops carries validation through the engineering operation rather than treating it as a final checkbox.

Depending on the objective, validation can include:

- automated tests;
- static analysis and type checking;
- repository and diff inspection;
- dependency and configuration validation;
- runtime execution;
- browser verification;
- API or integration checks;
- regression and edge-case testing;
- artifact inspection;
- independent review; and
- evidence-backed comparison with the acceptance criteria.

A successful command proves only that the command returned successfully. A passing test proves only what that test actually covers. A browser render proves only what was rendered under the tested conditions.

Completion therefore remains claim-specific. The system must preserve what has been validated, what has not, what evidence conflicts, and what still requires judgment or recovery.

## 8. Design interruption and recovery into the operating model

Consider a long-running objective with partial code changes, active delegated work, and a stalled run.

A naive system may restart from an old summary, duplicate changes, overwrite newer work, or continue from a checkpoint whose assumptions are no longer valid.

Build Ops is designed to take a different path:

1. **Stop expansion:** Prevent dependent work from continuing while ownership or state is uncertain.
2. **Preserve the objective:** Retain the scope, acceptance posture, decisions, artifacts, evidence, and unresolved blocker.
3. **Inspect current reality:** Reconcile the preserved state with the actual repository, branches, work surfaces, dependencies, tests, runtime state, and active assignments.
4. **Classify the posture:** Separate confirmed work, invalidated assumptions, stale assignments, unresolved changes, and remaining eligible work.
5. **Revalidate authority and dependencies:** Confirm that the next action is still permitted and technically valid.
6. **Resume narrowly:** Continue only the work that remains safe, or redirect, reassign, roll back, or request human judgment.
7. **Retain the recovery history:** Keep the interruption, decision, correction, and resulting evidence attached to the same objective.

The important rule is simple:

> **No reconciliation, no safe continuation.**

Recovery is not starting over. It is returning the operation to a known, accountable state from which work can continue safely.

## 9. Observed cumulative operation

At an August 8, 2026 snapshot, one active engineering objective had accumulated **53 hours, 49 minutes, and 44 seconds of active execution across linked runs**. The objective was still in progress, so the recorded duration was a floor rather than a final total.

This was cumulative active work on the same objective, not one process generating continuously and not a claim of 53 unattended hours.

The runtime record covered reasoning, tool use, reviews, file work, and subagent coordination. Inactive gaps between runs were excluded. Parallel work was included within run wall-clock time without being counted again as separate elapsed time.

The duration itself is not the achievement.

The meaningful result is that the objective retained its goal, active task, current action, decisions, technical state, artifacts, evidence, execution history, blockers, and next safe action across linked runs. I could inspect the work, stop it, redirect it, address blockers, and resume from a known state without silently changing the objective or discarding accountability.

Elapsed time did not define progress. Source-backed changes, decisions, validation evidence, resolved blockers, and safe next actions did.

## 10. Operationally validate the governing model

Build Ops is validated not only by whether individual scripts, checks, or engineering tasks succeed, but by whether the complete operating model behaves correctly under extended work.

The operational questions include:

- Does the objective survive model and session changes?
- Does current work remain inside the defined scope?
- Can the system detect stale or contradictory active state?
- Can multiple work paths proceed without colliding or bypassing dependencies?
- Does a blocker stop unsafe continuation without destroying progress?
- Can the operation be interrupted and redirected without losing its history?
- Does resumption reconcile against current technical reality?
- Are completion claims tied to specific evidence?
- Can the system expose partial, unknown, or insufficiently validated outcomes instead of reporting false completion?
- Can a person intervene at the level of decisions and exceptions rather than continuously watching every action?

The 53+ hour objective is one concrete record showing that the system can preserve governed continuity beyond a short-lived coding session. The broader achievement is the implemented framework and harness that make that continuity bounded, observable, interruptible, redirectable, traceable, recoverable, and evidence-backed.

## 11. Translate recurring failures into reusable system capabilities

I do not treat each agent failure as an isolated prompt problem.

When a failure repeats, I ask whether it should become:

- a stronger state contract;
- a narrower authority boundary;
- a new preflight or validation check;
- a stale-state detector;
- a coordination or ownership rule;
- a checkpoint or reconciliation requirement;
- a bounded retry or handoff rule;
- an operator-visible warning;
- a reusable runbook; or
- a permanent regression test.

That is how the system compounds engineering knowledge. A hard failure should make the next objective safer and easier to operate rather than becoming another one-off workaround.

## 12. Application to production agent and observability systems

The same operating principles apply to agents working over production telemetry, customer environments, or consequential infrastructure.

An agent reading logs, metrics, traces, session replays, deployment events, and configuration state can create a convincing explanation before proving that the evidence is complete, current, and causally related. It can also act on stale telemetry, mix time windows, overlook contradictory signals, or recommend remediation outside its authority.

A production-minded agent system therefore needs:

- exact source, query, time-window, and environment provenance;
- explicit representation of missing, delayed, sampled, or contradictory evidence;
- durable state across long investigations;
- bounded tool and remediation authority;
- competing-hypothesis testing before causal closure;
- checkpoints before consequential action;
- observability of the agent's own state and decisions;
- independent validation of material claims; and
- safe recovery when the diagnosis or external state remains uncertain.

Build Ops gave me direct experience turning those principles into an operating system for real engineering work rather than leaving them as theoretical guidelines.

## What this work demonstrates

Build Ops demonstrates my ability to:

- recognize when recurring agent failures indicate a systems problem rather than a prompting problem;
- design and operate a bounded AI engineering framework against a real codebase;
- preserve operational continuity across models, tools, agents, and sessions;
- coordinate active work without defaulting to either uncontrolled concurrency or one-worker serialization;
- make scope, authority, dependencies, progress, evidence, and recovery explicit;
- design for interruption, stale state, collision, contradiction, reconciliation, and safe resumption;
- validate complete engineering outcomes rather than accepting generated artifacts at face value;
- convert repeated failures into reusable platform capabilities; and
- use AI as an engineering force multiplier while retaining direct accountability for architecture, judgment, validation, and release decisions.

## My role

I personally designed the Build Ops system model, framework, harness, operating boundaries, durable-state and handoff approach, coordination controls, validation posture, operator-intervention model, and recovery path. I integrated it into my development environment and use it as part of active internal production while building Nerva.

AI agents perform bounded investigation, implementation, validation, and tool work inside that environment. I remain responsible for the objective, architecture, scope, authority, acceptance criteria, interpretation of evidence, and final engineering decision.

## Relationship to Nerva

Build Ops is internal engineering infrastructure supporting the development of Nerva.

It is not Nerva, is not a required dependency of Nerva's core architecture, and should not be read as a public description of Nerva's proprietary implementation. Build Ops artifacts and terminology do not automatically become Nerva product doctrine.

Its relevance is concrete: it demonstrates that I have designed and operated bounded, observable, recoverable agentic systems against real software and real engineering constraints.

## Public scope and intellectual-property boundary

This case study presents public-safe system behavior, engineering reasoning, validation principles, and verified operating evidence only.

It omits source code, prompts, internal services and component names, schemas, policy ordering, scoring, thresholds, routes, security mechanisms, deployment topology, proprietary coordination mechanisms, and Nerva's internal architecture.

It explains the problem I encountered, the operating model I designed, the behavior I implemented, and the evidence that the system works across long-running engineering execution.

It does not explain how to reconstruct Build Ops or Nerva.