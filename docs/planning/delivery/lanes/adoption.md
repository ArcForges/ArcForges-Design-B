# Adoption stage — delivery tasks

> Generated from [the delivery graph](../delivery-graph.json) by Plan `tools/delivery.py`; do not edit by hand. Rules and definitions: [delivery model](../README.md).

One-time reconciliation of existing implementation with this graph; see the adoption stage document.

Tasks: 11 · Owning repositories: AI, ArcNotes, ArcScope, ArcSlate, Cloud, Contracts, Design, DesktopPlatform, Mobile, Plan, Web · Integration owner(s): AI integration owner, ArcNotes integration owner, ArcScope integration owner, ArcSlate integration owner, Cloud integration owner, Contracts integration owner, Design integration owner, DesktopPlatform integration owner, Mobile integration owner, Plan integration owner, Web integration owner

| Task | Title | Kind | Size | Start prerequisites | Baseline |
|---|---|---|---|---|---|
| [ADOPT.01](#task-adopt-01) | Freeze the adoption baseline | adoption | S | none | not-started |
| [ADOPT.02](#task-adopt-02) | Adopt DesktopPlatform | adoption | M | [ADOPT.01](#task-adopt-01) (artifact) | not-started |
| [ADOPT.03](#task-adopt-03) | Adopt Contracts and locate the reported capability and resource closure | adoption | M | [ADOPT.01](#task-adopt-01) (artifact) | not-started |
| [ADOPT.04](#task-adopt-04) | Adopt ArcNotes | adoption | S | [ADOPT.01](#task-adopt-01) (artifact) | not-started |
| [ADOPT.05](#task-adopt-05) | Adopt ArcScope | adoption | S | [ADOPT.01](#task-adopt-01) (artifact) | not-started |
| [ADOPT.06](#task-adopt-06) | Adopt ArcSlate | adoption | S | [ADOPT.01](#task-adopt-01) (artifact) | not-started |
| [ADOPT.07](#task-adopt-07) | Adopt Cloud | adoption | M | [ADOPT.01](#task-adopt-01) (artifact) | not-started |
| [ADOPT.08](#task-adopt-08) | Adopt AI | adoption | S | [ADOPT.01](#task-adopt-01) (artifact) | not-started |
| [ADOPT.09](#task-adopt-09) | Adopt Web | adoption | S | [ADOPT.01](#task-adopt-01) (artifact) | not-started |
| [ADOPT.10](#task-adopt-10) | Adopt Mobile | adoption | S | [ADOPT.01](#task-adopt-01) (artifact) | not-started |
| [ADOPT.11](#task-adopt-11) | Reconcile Design and Plan documentation for adoption | adoption | S | [ADOPT.01](#task-adopt-01) (artifact) | not-started |

## Tasks

<a id="task-adopt-01"></a>

### ADOPT.01 — Freeze the adoption baseline

**Outcome.** The Plan ledger records, for every repository, the main head, open pull requests and branches, the latest published candidate per registry, and the location of any reported but unmerged work (including the reported [WP-03.03](../../work-packages/03-contract-foundation-and-licence-split.md#rule-wp-03.03) completion), so every repository review starts from the same frozen inputs.

| Field | Value |
|---|---|
| Owning repository | Plan (`C:\MyFile\Projects\Plan-B`); integration owner: Plan integration owner |
| Kind / size | adoption / S |
| Obligations | [P2-018](../../../decisions/phase-2-specification-decisions.md#rule-p2-018) — adoption stage: baseline inputs |
| Provides | adoption baseline record; ledger skeleton |
| Start prerequisites | none |
| Completion prerequisites | none |
| Unblocks | [ADOPT.02](#task-adopt-02), [ADOPT.03](#task-adopt-03), [ADOPT.04](#task-adopt-04), [ADOPT.05](#task-adopt-05), [ADOPT.06](#task-adopt-06), [ADOPT.07](#task-adopt-07), [ADOPT.08](#task-adopt-08), [ADOPT.09](#task-adopt-09), [ADOPT.10](#task-adopt-10), [ADOPT.11](#task-adopt-11) |
| Write scope | `Plan:ledger/adoption/baseline.md`<br>`Plan:ledger/README.md` |
| Validation | Read-only inspection of repositories, pull requests and registry receipts already recorded; no builds, downloads or runtime checks ([P2-017](../../../decisions/phase-2-specification-decisions.md#rule-p2-017)). |
| Completion evidence | Baseline record with exact commit identities per repository, open pull request list, latest candidate identities and the reported-work locations; reviewed and merged in the Plan repository. |
| Baseline (unreviewed unless accepted) | not-started |

<a id="task-adopt-02"></a>

### ADOPT.02 — Adopt DesktopPlatform

**Outcome.** Every delivery task owned by DesktopPlatform is classified inherited, inherited with adjustment, gap or conflicting against the recorded baseline, with ledger records for inherited tasks and a recorded adjustment list, including the replacement of the design-policy graph check that still validates the retired work-package graph.

| Field | Value |
|---|---|
| Owning repository | DesktopPlatform (`C:\MyFile\Projects\ArcForges\DesktopPlatform`); integration owner: DesktopPlatform integration owner |
| Kind / size | adoption / M |
| Obligations | [P2-018](../../../decisions/phase-2-specification-decisions.md#rule-p2-018) — adoption stage: DesktopPlatform review |
| Provides | DesktopPlatform adoption report |
| Start prerequisites | **artifact** [ADOPT.01](#task-adopt-01) — frozen baseline record. *Why:* classification must use the same frozen repository heads and receipts as every other repository review |
| Completion prerequisites | none |
| Unblocks | none |
| Write scope | `Plan:ledger/adoption/DesktopPlatform.md`<br>`Plan:ledger/tasks/*.md` |
| Validation | Review of merged source, retained CI results and receipts only; no new builds, downloads or runtime checks unless a task's evidence field requires a never-run local check ([P2-017](../../../decisions/phase-2-specification-decisions.md#rule-p2-017)). |
| Completion evidence | Adoption report with one classification row per owned task, evidence references for inherited tasks, adjustment list and any conflicts raised under [D-001](../../../decisions/phase-1-foundation-decisions.md#rule-d-001). |
| Baseline (unreviewed unless accepted) | not-started |

<a id="task-adopt-03"></a>

### ADOPT.03 — Adopt Contracts and locate the reported capability and resource closure

**Outcome.** Every delivery task owned by Contracts is classified against the recorded baseline; the work the user reported as completing [WP-03.03](../../work-packages/03-contract-foundation-and-licence-split.md#rule-wp-03.03) is located and reviewed like any task completion, and is recorded as inherited only if its source, retained checks, publication receipt and vectors satisfy the task's evidence field.

| Field | Value |
|---|---|
| Owning repository | Contracts (`C:\MyFile\Projects\ArcForges\Contracts`); integration owner: Contracts integration owner |
| Kind / size | adoption / M |
| Obligations | [P2-018](../../../decisions/phase-2-specification-decisions.md#rule-p2-018) — adoption stage: Contracts review, including the reported [WP-03.03](../../work-packages/03-contract-foundation-and-licence-split.md#rule-wp-03.03) completion |
| Provides | Contracts adoption report |
| Start prerequisites | **artifact** [ADOPT.01](#task-adopt-01) — frozen baseline record including the reported-work location. *Why:* the reported completion was not present in any repository when the plan was written; its location must be recorded before it can be reviewed |
| Completion prerequisites | none |
| Unblocks | none |
| Write scope | `Plan:ledger/adoption/Contracts.md`<br>`Plan:ledger/tasks/*.md` |
| Validation | Review of merged source, retained CI results and publication receipts only ([P2-017](../../../decisions/phase-2-specification-decisions.md#rule-p2-017)). |
| Completion evidence | Adoption report with classification rows, the reviewed evidence for any inherited closure, and adjustments. |
| Baseline (unreviewed unless accepted) | not-started |

<a id="task-adopt-04"></a>

### ADOPT.04 — Adopt ArcNotes

**Outcome.** Every ArcNotes delivery task is classified; bootstrap scaffolding is recorded as scaffolding, never as product completion.

| Field | Value |
|---|---|
| Owning repository | ArcNotes (`C:\MyFile\Projects\ArcForges\ArcNotes`); integration owner: ArcNotes integration owner |
| Kind / size | adoption / S |
| Obligations | [P2-018](../../../decisions/phase-2-specification-decisions.md#rule-p2-018) — adoption stage: ArcNotes review |
| Provides | ArcNotes adoption report |
| Start prerequisites | **artifact** [ADOPT.01](#task-adopt-01) — frozen baseline record. *Why:* classification uses the frozen baseline |
| Completion prerequisites | none |
| Unblocks | none |
| Write scope | `Plan:ledger/adoption/ArcNotes.md`<br>`Plan:ledger/tasks/*.md` |
| Validation | Review only ([P2-017](../../../decisions/phase-2-specification-decisions.md#rule-p2-017)). |
| Completion evidence | Adoption report with classification rows and adjustments. |
| Baseline (unreviewed unless accepted) | not-started |

<a id="task-adopt-05"></a>

### ADOPT.05 — Adopt ArcScope

**Outcome.** Every ArcScope delivery task is classified; bootstrap scaffolding is recorded as scaffolding, never as product completion.

| Field | Value |
|---|---|
| Owning repository | ArcScope (`C:\MyFile\Projects\ArcForges\ArcScope`); integration owner: ArcScope integration owner |
| Kind / size | adoption / S |
| Obligations | [P2-018](../../../decisions/phase-2-specification-decisions.md#rule-p2-018) — adoption stage: ArcScope review |
| Provides | ArcScope adoption report |
| Start prerequisites | **artifact** [ADOPT.01](#task-adopt-01) — frozen baseline record. *Why:* classification uses the frozen baseline |
| Completion prerequisites | none |
| Unblocks | none |
| Write scope | `Plan:ledger/adoption/ArcScope.md`<br>`Plan:ledger/tasks/*.md` |
| Validation | Review only ([P2-017](../../../decisions/phase-2-specification-decisions.md#rule-p2-017)). |
| Completion evidence | Adoption report with classification rows and adjustments. |
| Baseline (unreviewed unless accepted) | not-started |

<a id="task-adopt-06"></a>

### ADOPT.06 — Adopt ArcSlate

**Outcome.** Every ArcSlate delivery task is classified; bootstrap scaffolding is recorded as scaffolding, never as product completion.

| Field | Value |
|---|---|
| Owning repository | ArcSlate (`C:\MyFile\Projects\ArcForges\ArcSlate`); integration owner: ArcSlate integration owner |
| Kind / size | adoption / S |
| Obligations | [P2-018](../../../decisions/phase-2-specification-decisions.md#rule-p2-018) — adoption stage: ArcSlate review |
| Provides | ArcSlate adoption report |
| Start prerequisites | **artifact** [ADOPT.01](#task-adopt-01) — frozen baseline record. *Why:* classification uses the frozen baseline |
| Completion prerequisites | none |
| Unblocks | none |
| Write scope | `Plan:ledger/adoption/ArcSlate.md`<br>`Plan:ledger/tasks/*.md` |
| Validation | Review only ([P2-017](../../../decisions/phase-2-specification-decisions.md#rule-p2-017)). |
| Completion evidence | Adoption report with classification rows and adjustments. |
| Baseline (unreviewed unless accepted) | not-started |

<a id="task-adopt-07"></a>

### ADOPT.07 — Adopt Cloud

**Outcome.** Every delivery task owned by Cloud (core, commerce, policy, operations, simulator, search and catalog modules) is classified against the recorded baseline, distinguishing the bootstrap host and deployed probe from product modules.

| Field | Value |
|---|---|
| Owning repository | Cloud (`C:\MyFile\Projects\ArcForges\Cloud`); integration owner: Cloud integration owner |
| Kind / size | adoption / M |
| Obligations | [P2-018](../../../decisions/phase-2-specification-decisions.md#rule-p2-018) — adoption stage: Cloud review |
| Provides | Cloud adoption report |
| Start prerequisites | **artifact** [ADOPT.01](#task-adopt-01) — frozen baseline record. *Why:* classification uses the frozen baseline |
| Completion prerequisites | none |
| Unblocks | none |
| Write scope | `Plan:ledger/adoption/Cloud.md`<br>`Plan:ledger/tasks/*.md` |
| Validation | Review of merged source, retained CI and deployment receipts only ([P2-017](../../../decisions/phase-2-specification-decisions.md#rule-p2-017)); a deployment receipt is not a live test. |
| Completion evidence | Adoption report with classification rows and adjustments. |
| Baseline (unreviewed unless accepted) | not-started |

<a id="task-adopt-08"></a>

### ADOPT.08 — Adopt AI

**Outcome.** Every delivery task owned by AI is classified; the bootstrap Worker and Workflow scaffolding is recorded as scaffolding, never as Harness completion.

| Field | Value |
|---|---|
| Owning repository | AI (`C:\MyFile\Projects\ArcForges\AI`); integration owner: AI integration owner |
| Kind / size | adoption / S |
| Obligations | [P2-018](../../../decisions/phase-2-specification-decisions.md#rule-p2-018) — adoption stage: AI review |
| Provides | AI adoption report |
| Start prerequisites | **artifact** [ADOPT.01](#task-adopt-01) — frozen baseline record. *Why:* classification uses the frozen baseline |
| Completion prerequisites | none |
| Unblocks | none |
| Write scope | `Plan:ledger/adoption/AI.md`<br>`Plan:ledger/tasks/*.md` |
| Validation | Review only ([P2-017](../../../decisions/phase-2-specification-decisions.md#rule-p2-017)). |
| Completion evidence | Adoption report with classification rows and adjustments. |
| Baseline (unreviewed unless accepted) | not-started |

<a id="task-adopt-09"></a>

### ADOPT.09 — Adopt Web

**Outcome.** Every delivery task owned by Web is classified, including the existing static-site generator and canonical-host Worker.

| Field | Value |
|---|---|
| Owning repository | Web (`C:\MyFile\Projects\ArcForges\Web`); integration owner: Web integration owner |
| Kind / size | adoption / S |
| Obligations | [P2-018](../../../decisions/phase-2-specification-decisions.md#rule-p2-018) — adoption stage: Web review |
| Provides | Web adoption report |
| Start prerequisites | **artifact** [ADOPT.01](#task-adopt-01) — frozen baseline record. *Why:* classification uses the frozen baseline |
| Completion prerequisites | none |
| Unblocks | none |
| Write scope | `Plan:ledger/adoption/Web.md`<br>`Plan:ledger/tasks/*.md` |
| Validation | Review only ([P2-017](../../../decisions/phase-2-specification-decisions.md#rule-p2-017)). |
| Completion evidence | Adoption report with classification rows and adjustments. |
| Baseline (unreviewed unless accepted) | not-started |

<a id="task-adopt-10"></a>

### ADOPT.10 — Adopt Mobile

**Outcome.** Every delivery task owned by Mobile is classified, including the development package identity and the preview-only shared module.

| Field | Value |
|---|---|
| Owning repository | Mobile (`C:\MyFile\Projects\ArcForges\Mobile`); integration owner: Mobile integration owner |
| Kind / size | adoption / S |
| Obligations | [P2-018](../../../decisions/phase-2-specification-decisions.md#rule-p2-018) — adoption stage: Mobile review |
| Provides | Mobile adoption report |
| Start prerequisites | **artifact** [ADOPT.01](#task-adopt-01) — frozen baseline record. *Why:* classification uses the frozen baseline |
| Completion prerequisites | none |
| Unblocks | none |
| Write scope | `Plan:ledger/adoption/Mobile.md`<br>`Plan:ledger/tasks/*.md` |
| Validation | Review only ([P2-017](../../../decisions/phase-2-specification-decisions.md#rule-p2-017)). |
| Completion evidence | Adoption report with classification rows and adjustments. |
| Baseline (unreviewed unless accepted) | not-started |

<a id="task-adopt-11"></a>

### ADOPT.11 — Reconcile Design and Plan documentation for adoption

**Outcome.** Documentation findings that affect adoption decisions are resolved or scheduled (including the pre-existing corpus citation drift recorded in the adoption stage document), the generated views are confirmed current, and the ledger identifies the repositories whose adoption is complete.

| Field | Value |
|---|---|
| Owning repository | Design (`C:\MyFile\Projects\ArcForges-Design-B`); integration owner: Design integration owner; also touches Plan |
| Kind / size | adoption / S |
| Obligations | [P2-018](../../../decisions/phase-2-specification-decisions.md#rule-p2-018) — adoption stage: documentation reconciliation |
| Provides | documentation reconciliation record |
| Start prerequisites | **artifact** [ADOPT.01](#task-adopt-01) — frozen baseline record. *Why:* reconciliation uses the frozen baseline |
| Completion prerequisites | none |
| Unblocks | none |
| Write scope | `Design:docs/**`<br>`Plan:ledger/adoption/documentation.md` |
| Validation | Documentation consistency and link review, delivery graph check and the existing corpus integrity check; no product builds ([P2-017](../../../decisions/phase-2-specification-decisions.md#rule-p2-017)). |
| Completion evidence | Reconciliation record with checker results and any planning-change pull requests. |
| Baseline (unreviewed unless accepted) | not-started |
