# Designing the Command Layer for Agentic Work

**An engineering reasoning brief based on Nerva**  
**Tony Guillaro | AI Systems & Forward-Deployed Engineer**  
**Public, non-proprietary work sample | August 2026**

Nerva is an original, proprietary product architecture in active development. This brief explains how I framed its central systems problem, converted failure modes into design invariants, weighed competing operational goals, and designed for recovery. It deliberately omits source code, internal component names, schemas, thresholds, topology, prompts, routes, security mechanisms, and implementation recipes.

## The design question

> How can an AI system act with useful autonomy while keeping human intent, authority, operational truth, evidence, and recovery coherent when the real world diverges from the plan?

I began with a simple observation: the AI industry was increasing the ability to reason and act faster than it was increasing the ability to command and verify that work. A model can propose a plan. An agent can call a tool. A workflow can advance. A dashboard can show activity. None of those facts establishes who authorized an effect, whether the external state actually changed, what evidence supports the result, or how the system should recover when the outcome is uncertain.

## 1. Start with failure modes, not features

I did not begin by asking which agents, models, or interface components Nerva should contain. I began by mapping the category errors that repeatedly make agentic systems unreliable:

- A plan is treated as execution.
- Access to data or a tool is treated as permission to use it.
- Agent activity is treated as verified completion.
- A successful API response is treated as a reconciled real-world outcome.
- The intelligence performing the work is also trusted to certify its own result.
- Error detection is treated as recovery.
- A conversational transcript is treated as durable operational truth.

These errors become more dangerous as systems gain more agents, longer runtimes, broader data access, external integrations, and financial or operational consequences. Adding intelligence does not resolve the problem. In several cases, it increases the blast radius.

That changed the product question from "How do I orchestrate more capable agents?" to "What operating relationship must remain coherent while any eligible intelligence acts?"

## 2. Convert the failure map into invariants

Once the failure modes were explicit, I defined a small set of meanings the system could not be allowed to blur:

1. **Work must outlive the conversation.** Consequential work needs durable identity, scope, state, decisions, evidence, and recovery history.
2. **Capability must remain separate from authority.** An actor can know how to do something without being permitted to do it.
3. **Operational state must be source-backed.** Interface color, model confidence, and agent narration cannot manufacture reality.
4. **Completion must be claim-specific and evidence-backed.** Producing an artifact is not the same as proving the requested outcome.
5. **Oversight must be independent of execution.** The actor doing the work cannot be the only judge of whether its work is safe or supported.
6. **Failure must remain inside the product model.** Partial effects, unknown outcomes, contradiction, containment, correction, and safe resumption cannot disappear behind a generic error state.

These invariants led to an Operation-centered model. The primary object is the accountable work itself - not the chat, agent, workflow, or model. Models, agents, tools, people, and workflows participate in an Operation, but none owns its truth merely by participating.

The conceptual path is:

**Intent -> relevant context -> durable Operation -> bounded authority -> execution -> visible state -> evidence -> independent challenge -> resolution or recovery**

The sequence is less important than the separation of responsibility. Authority permits an attempt; it does not prove success. Evidence supports a claim; it does not retroactively authorize the action. Oversight can challenge or hold work; it does not gain the right to execute it.

## 3. Make the tradeoffs explicit

The difficult part was not selecting one desirable property. It was preserving several properties that naturally pull against one another.

| Engineering tension | Design choice | Reasoning |
|---|---|---|
| Autonomy vs. interruption | Govern in proportion to consequence | Approval for every step creates fatigue. Routine bounded work should continue, while irreversible, sensitive, broad, costly, or externally consequential actions receive stronger control. |
| Flexibility vs. consistent truth | Keep models and providers interchangeable beneath one operational contract | Provider choice can change capability, latency, privacy, or cost. It must not change what authority, evidence, completion, or recovery mean. |
| Simple UX vs. operational honesty | Change presentation depth, not underlying truth | A personal user and an enterprise operator can see different levels of detail without receiving different definitions of state. Unknown remains unknown. Partial remains partial. |
| Extensibility vs. integrity | Admit capabilities through governed, observable, revocable boundaries | Installing an agent, connector, workflow, or tool expands capability; it does not grant blanket data access or execution authority. |
| Speed vs. resilience | Design the recovery path before trusting the happy path | A fast system that cannot distinguish partial success, unknown external state, and duplicate-effect risk is not operationally fast once something fails. |

This reasoning also rejected two common extremes. One is unrestricted autonomy, where capability quietly becomes permission. The other is approval theater, where a human is asked to click through so many low-value decisions that the important ones become invisible. The goal is useful autonomy under human authority - not constant supervision and not silent self-authorization.

## 4. Design the failure path first

Consider an Operation that updates a set of external records. The external provider becomes unavailable after accepting some requests.

A naive workflow retries everything. That can duplicate effects. Another naive workflow marks the entire run failed, discarding confirmed progress. A third trusts the last local response and reports success despite an unknown external outcome.

My reasoning path is different:

1. **Contain:** Stop dependent continuation before uncertainty expands.
2. **Partition state:** Separate confirmed effects, confirmed failures, unknown outcomes, and unattempted work.
3. **Preserve truth:** Keep the original objective, input version, scope, authority, and external responses attached to the Operation.
4. **Reconcile:** When the provider returns, inspect actual external state before deciding whether any retry is safe.
5. **Revalidate:** Confirm that context, target scope, connector eligibility, authority, and duplicate-effect posture are still valid.
6. **Resume narrowly:** Execute only the remaining eligible work or present the human with consequence-aware recovery choices.
7. **Prove the final posture:** Attach evidence to each material claim and retain the recovery history.

The key decision is to treat uncertainty as a legitimate operational state. The interface should never turn "request accepted" into "effect confirmed," "cancel requested" into "cancelled," or "repair started" into "recovered" until the source-backed state supports that claim.

## 5. Translate the architecture into customer delivery

This method is directly applicable to forward-deployed engineering. In a customer environment, I would not begin with a generic agent stack and force the workflow around it. I would:

1. Map the actual operation, stakeholders, systems, data movement, decision rights, and external consequences.
2. Identify where the current process loses truth: ambiguous ownership, stale context, duplicate work, unverifiable outcomes, brittle integrations, or invisible recovery.
3. Define the acceptance criteria and failure postures before optimizing the happy path.
4. Separate the responsibilities of models, agents, tools, people, policy, evidence, and external systems.
5. Build the smallest end-to-end path that produces observable value inside real customer constraints.
6. Harden the successful path with explicit boundaries, diagnostics, evidence, rollback or correction, runbooks, and reusable implementation patterns.

That is how I tackle ambiguous systems problems: start with the real operation, find the semantic and technical failure boundaries, define invariants, make tradeoffs visible, implement across the stack, and stay accountable through deployment and recovery.

## Public scope and intellectual-property boundary

This public brief presents product-level reasoning only. It omits source code, internal services, schemas, policy order, thresholds, prompts, routes, security mechanisms, infrastructure, and self-improvement machinery. It shows how I framed the system - not how to reconstruct it.
