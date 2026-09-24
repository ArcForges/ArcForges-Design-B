# Parallel Delivery Model

> Status: **Authoritative** — Phase 2 (Detailed Specifications)
> Layer: Planning
> Governing authority: [P2-018](../../decisions/phase-2-specification-decisions.md#rule-p2-018) (parallel delivery graph), [D-017](../../decisions/phase-1-foundation-decisions.md#rule-d-017) (planning location), [P2-017](../../decisions/phase-2-specification-decisions.md#rule-p2-017) (validation venue and cadence)
> Data: [`delivery-graph.json`](delivery-graph.json) — the single scheduling source.
> Generated views: [lane catalogues](lanes/) · [obligation traceability](traceability.md) · [substitutes](substitutes.md) · [shared resources](shared-resources.md) · [schedule analysis](schedule-analysis.md). Hand-written companion: [adoption stage](adoption.md).

This document defines how ArcForges implementation work is scheduled and executed by many workers at once. It replaces the retired model in which 447 numbered substeps were advanced one at a time from a single Current task. It changes **how** the accepted product is delivered, never **what** is delivered: every requirement, invariant, permission, recovery path, compatibility obligation, licence obligation and commercial acceptance rule in the current design stays in force, and every work-package substep remains an obligation that must be satisfied with its stated evidence.

## How to use this layer

1. Read the rules below once. They are short and they are the only scheduling rules.
2. To find work, use the Plan repository's execution entry: it computes the ready set from the graph and the execution ledger and explains how to claim, execute and complete a task.
3. To understand one task, open its record in its [lane catalogue](lanes/). The record lists the obligations it satisfies, its typed prerequisites, what it unblocks, its write scope, shared resources, permitted substitutes, validation and completion evidence.
4. To check that an obligation or gate is covered, use [traceability](traceability.md).
5. To change the plan, follow [section 7](#7-changing-the-plan).

---

## 1. Obligations and tasks

| # | Rule |
|---|---|
| <a id="rule-dlv-01"></a>DLV-01 | **Work packages are the obligation catalogue.** Each substep `WP-NN.MM`, each package-level obligation and each named gate keeps its identity, its "what must be fully done", its testing requirements and its completion gate. Obligations are not scheduling units and their numbering implies no order. |
| <a id="rule-dlv-02"></a>DLV-02 | **Delivery tasks are the scheduling units.** A task has one owning repository, one coherent outcome, the obligations (or explicitly named parts of obligations) it satisfies, typed prerequisites, a permitted write scope, declared shared resources, permitted substitutes, external prerequisites where applicable, proportionate validation and completion evidence. Tasks are defined only in [`delivery-graph.json`](delivery-graph.json). |
| <a id="rule-dlv-03"></a>DLV-03 | **Complete coverage.** Every active substep and package obligation maps to at least one task. When a substep is split, each mapped part is named, and the substep is satisfied only when every mapped task is complete. A work package is complete when all of its obligations are satisfied; its closure task, which verifies the package's owned artifacts, depends on every other task mapped to that package. |
| <a id="rule-dlv-04"></a>DLV-04 | **Gates keep their evidence class.** A deferred, open or release gate closes only when every contributing task has recorded the evidence the gate names. A scoped contribution never becomes a global pass, and documentation, fixtures or compilation never close a runtime, device, provider or commercial gate. |
| <a id="rule-dlv-05"></a>DLV-05 | **Sizing is relative.** Task sizes S, M, L and XL are unmeasured relative effort used only for schedule analysis. They create no dates, durations or resourcing commitments. |

## 2. Dependency classes

A prerequisite edge always names the concrete input that is unavailable and why it blocks. "The upstream work package is complete" is never an edge.

| # | Class | Meaning |
|---|---|---|
| <a id="rule-dlv-06"></a>DLV-06 | **contract** (start) | The task cannot be written until a specific Contracts closure — named records, services, codecs and vectors — is published in a Contracts candidate the task can pin. |
| <a id="rule-dlv-07"></a>DLV-07 | **artifact** (start) | The task must compile or compose against a real published artifact (package, runtime, image, deployed binding, migrated schema) and no contract-bound substitute is acceptable, for example because the task's own gate requires the real mechanism. |
| <a id="rule-dlv-08"></a>DLV-08 | **design** (start) | A design decision or profile the task needs does not yet exist. Current design is frozen, so these edges are rare and point to the task that records the missing definition. |
| <a id="rule-dlv-09"></a>DLV-09 | **integration** (completion) | The task may start and deliver its own outcome, but it cannot be complete until the named task is complete, because its own acceptance includes that real scenario. Wider real integration is scheduled as separate integration tasks that start when both real sides exist. |
| <a id="rule-dlv-10"></a>DLV-10 | **release** (start of release tasks only) | A release or commercial-activation task cannot begin until the named task is complete. Release edges never delay implementation tasks. |
| <a id="rule-dlv-11"></a>DLV-11 | **exclusive resource** (not an edge) | Tasks that write the same shared file, registry, sequence, environment, key, publication pointer or heavy build slot declare it with a mode (`append`, `regenerate`, `exclusive`, `read`). The resource owner applies the [published protocol](shared-resources.md) at merge or use time; unrelated tasks are not ordered because of it. Different files inside one module directory are ordinary parallel work resolved by Git. |
| <a id="rule-dlv-12"></a>DLV-12 | **external prerequisite** (not an edge) | Provider accounts, verified domains, hardware-lab devices and signing custody that no task can create are listed on the task with their owning role. A missing external prerequisite leaves the affected acceptance blocked and recorded; it is never passed or removed from scope. |

## 3. Contracts and the semantic foundation

| # | Rule |
|---|---|
| <a id="rule-dlv-13"></a>DLV-13 | **Small shared foundation first.** The accepted foundation schema, safe values and serialization posture of [WP-03.00](../work-packages/03-contract-foundation-and-licence-split.md#rule-wp-03.00)–[WP-03.02](../work-packages/03-contract-foundation-and-licence-split.md#rule-wp-03.02) and the resource/capability descriptor closure of [WP-03.03](../work-packages/03-contract-foundation-and-licence-split.md#rule-wp-03.03) are the only contract prerequisites shared by nearly every consumer. Every other contract area is a separate closure task that can be authored concurrently. |
| <a id="rule-dlv-14"></a>DLV-14 | **Closure readiness unlocks consumers.** A consumer starts when the closure it actually uses is published: its records, services, error mapping, version semantics, authorization fields and positive/negative vectors. Consumers do not wait for unrelated closures. The complete generated-package, compatibility-window and schema gates ([WP-03.05](../work-packages/03-contract-foundation-and-licence-split.md#rule-wp-03.05), [WP-03.06](../work-packages/03-contract-foundation-and-licence-split.md#rule-wp-03.06), [WP-03.90](../work-packages/03-contract-foundation-and-licence-split.md#rule-wp-03.90)) remain mandatory for the Contracts obligations and for every release. |
| <a id="rule-dlv-15"></a>DLV-15 | **One authority per meaning.** Handwritten proto and HTTP-exception schemas in Contracts remain the only wire authority. No consumer invents a DTO, a wire meaning, a second write path or a local copy of a schema for an area whose closure is not published; it waits for the closure or raises a contract change through the Architecture Owner under [PA-02](../implementation-sequence.md#rule-pa-02). |
| <a id="rule-dlv-16"></a>DLV-16 | **Internal boundaries are producer outputs.** Module ports, storage boundaries, transaction ownership, change notifications, lifecycle hooks and composition entry points that consumers build against are named in the producing task's `provides` list. A consumer that needs one depends on that task, not on the whole producing package. Shared transaction families keep one owner and one canonical mutation path however many consumers are built concurrently. |
| <a id="rule-dlv-17"></a>DLV-17 | **Publication is per merge, pinning is per consumer.** Contracts and DesktopPlatform publish every package at one candidate version on each merge to main. A consumer pins the exact candidate produced by the merge of the capability it needs through a reviewed pin update; it never waits for a package closure task, and additive evolution never changes the meaning of a pinned closure. |

## 4. Substitutes and progressive integration

| # | Rule |
|---|---|
| <a id="rule-dlv-18"></a>DLV-18 | **Contract-bound substitutes unlock starting.** A fixture, mock or simulated adapter may stand in for a producer that is not yet available only if it implements the authoritative contract (generated types, recorded vectors or the declared protocol), is visibly test-only, is excluded from release composition and is registered in the [substitute registry](substitutes.md) with its real producer and the task that removes it. The removing task depends on the real producer and on every consumer of the substitute. |
| <a id="rule-dlv-19"></a>DLV-19 | **A substitute proves only its stated scope.** [MK-02](../implementation-sequence.md#rule-mk-02), [MK-03](../implementation-sequence.md#rule-mk-03), [TS-01](../implementation-sequence.md#rule-ts-01) and [TS-02](../implementation-sequence.md#rule-ts-02) remain binding: fixture success is never real integration, runtime, device, provider or commercial evidence, and scaffolding is deleted rather than adapted into production. |
| <a id="rule-dlv-20"></a>DLV-20 | **Integrate progressively.** Each real producer–consumer pair has an integration task that becomes ready as soon as both real sides exist. Integration is not deferred to one final convergence; the family release joins evidence that already exists. |
| <a id="rule-dlv-21"></a>DLV-21 | **Early risk proofs stay early.** Proofs whose failure would invalidate substantial downstream work (Native AOT per runtime, local helper gRPC, Cloudflare Container and D1, Android transport, native decode and synchronisation, editor and store recovery, acquisition throughput, semantic hash) are tasks with few prerequisites and are scheduled before the work that depends on their conclusions. The [must-be-real-early list](../implementation-sequence.md#3-what-may-be-mocked-and-what-may-not) is unchanged. |

## 5. Task lifecycle

| # | Rule |
|---|---|
| <a id="rule-dlv-22"></a>DLV-22 | **Entry condition.** A task becomes claimable only after the [adoption](adoption.md) task of its owning repository is complete, so that its prerequisites and its own state are known. There is no other global barrier: a repository whose adoption is complete proceeds while others are still being adopted. |
| <a id="rule-dlv-23"></a>DLV-23 | **States.** A task is *blocked* until every start prerequisite is satisfied; then *ready*; *claimed* while one worker owns it; *in review* while its pull requests are open; *delivered* when its outcome is merged and any candidate is published but a completion prerequisite is still open; *complete* when its evidence is accepted in the Plan ledger. *Inherited* marks a task satisfied by reviewed existing work during adoption; *superseded* marks a task replaced by a recorded planning change. |
| <a id="rule-dlv-24"></a>DLV-24 | **Satisfying prerequisites.** A contract, artifact or design prerequisite is satisfied when the named task is delivered, because its published outcome exists. A release prerequisite and a completion prerequisite are satisfied only when the named task is complete. This is why a producer whose acceptance includes a consumer scenario never deadlocks with that consumer. |
| <a id="rule-dlv-25"></a>DLV-25 | **Readiness is local.** Any number of ready tasks may run at the same time, in the same or different repositories, subject only to their declared shared resources. A finished lane never waits for an unrelated lane, a numbered order or a wave boundary. |
| <a id="rule-dlv-26"></a>DLV-26 | **Atomic claim with a lease.** A worker claims a ready task by creating the branch `claims/<task-id>` in the Plan repository whose single commit records the claimant, the time and a lease expiry. Creating an existing branch fails, so two workers cannot own one task. The claimant renews the lease by appending a commit; the claim ends when the task completes or the claimant releases it. |
| <a id="rule-dlv-27"></a>DLV-27 | **Resume and takeover.** The claimant resumes an interrupted task from its retained worktree, branch and pull request. After the lease has expired, another worker may take over only by appending a takeover commit to the existing claim branch (a fast-forward that fails if anyone else moved it first) and continues the same branch and pull request. A blocked task records the concrete missing input on its claim; if the block reveals a missing prerequisite or an architecture conflict, it is raised under [WF-03](../implementation-sequence.md#rule-wf-03) and resolved by a planning change, never locally. |
| <a id="rule-dlv-28"></a>DLV-28 | **Completion.** A task is complete when its pull requests are merged with all retained applicable checks green, any producer candidate is published with its receipt, its completion prerequisites are complete, and its ledger record — source commits, candidate identities, validation actually performed, local runtime evidence, substitutes still in use and untested coverage — is reviewed and merged in the Plan repository. |

## 6. Coordination at the narrowest boundary

| # | Rule |
|---|---|
| <a id="rule-dlv-29"></a>DLV-29 | **Repository integration owner.** Each repository has one integration owner role that merges its ready pull requests in any order compatible with declared prerequisites, applies the shared-resource protocols (generated baselines, migration order, host composition, route and binding registration, package inventories, root dependency files), keeps main green and owns publication of that repository's candidates. There is no family-wide merge order. |
| <a id="rule-dlv-30"></a>DLV-30 | **Cross-repository coordination is limited to four cases:** a consumer pin update after a producer publication (owned by the consumer task), exclusive use of a shared deployment or provider environment, release tasks (owned by the Release Engineering Owner), and changes to authoritative design or contracts (owned by the Architecture Owner). |
| <a id="rule-dlv-31"></a>DLV-31 | **Local resources.** Coding and review proceed concurrently. At most one CPU-heavy local build or test runs per workstation at a time and existing caches are reused, as [P2-017](../../decisions/phase-2-specification-decisions.md#rule-p2-017) requires; CI capacity is not limited by this rule. |
| <a id="rule-dlv-32"></a>DLV-32 | **Evidence is reused.** A task reuses valid accepted evidence of its prerequisites and does not repeat an audit, a public download, a consumer execution or a runtime check without a new change or a concrete unresolved finding. Receipts record what was observed and what was not. |

## 7. Changing the plan

| # | Rule |
|---|---|
| <a id="rule-dlv-33"></a>DLV-33 | **One source, generated views.** Planning changes edit [`delivery-graph.json`](delivery-graph.json) and then regenerate every view with the Plan repository's `tools/delivery.py generate`. `tools/delivery.py check` must pass: valid references, satisfiable prerequisites under [DLV-24](#rule-dlv-24), complete substep and package-obligation coverage, substitutes whose removing task depends on the real producer and every consumer, declared shared resources for exact shared files, and current generated views. |
| <a id="rule-dlv-34"></a>DLV-34 | **Recorded, reviewed changes.** Adding, removing or retyping an edge, splitting or merging tasks, or moving obligations between tasks is a planning change reviewed like any other authoritative edit ([WF-02](../implementation-sequence.md#rule-wf-02)). Obligations and acceptance are never removed by a planning change; scope moves only between tasks. |

## 8. Current baseline

Accepted implementation evidence covers [WP-00](../work-packages/00-specification-naming-and-rights-freeze.md#rule-wp-00), [WP-01](../work-packages/01-repository-reconciliation-and-target-layout.md#rule-wp-01), [WP-02](../work-packages/02-build-governance-and-analyzer-policy.md#rule-wp-02) and [WP-03.00](../work-packages/03-contract-foundation-and-licence-split.md#rule-wp-03.00)–[WP-03.02](../work-packages/03-contract-foundation-and-licence-split.md#rule-wp-03.02); their tasks carry the `accepted` baseline with the receipts named in the graph. On 2026-09-23 the user reported that [WP-03.03](../work-packages/03-contract-foundation-and-licence-split.md#rule-wp-03.03) is also complete. No corresponding source, pull request or receipt was present in the Contracts, Design or Plan repositories when this model was written (Contracts main was the WP03.02 merge), so the tasks implementing that substep are open and the [adoption stage](adoption.md) locates and reviews the reported work before recording anything as inherited. No other existing implementation is certified by this document.

## 9. Relationship to other planning documents

- [Implementation dependency model](../implementation-sequence.md) keeps the ordering principles, the binding mock policy, the frozen semantics, roles and the work-package format, restated for task-level scheduling.
- [Work packages](../work-packages/README.md) are the obligation catalogue; each package's section 9 lists its delivery tasks, generated from the graph.
- [Producer artifacts and integration](../producer-artifacts-and-integration.md) defines what each producer must deliver and the evidence classes; the graph schedules those outputs.
- The Plan repository's `arcforges-implementation.md` describes the claim, worktree, review, merge and ledger procedure for workers, and its generated `list.md` holds one self-contained prompt per task.
