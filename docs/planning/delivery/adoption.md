# Adoption Stage

> Status: **Authoritative** — Phase 2 (Detailed Specifications)
> Layer: Planning
> Governing authority: [P2-018](../../decisions/phase-2-specification-decisions.md#rule-p2-018) (decision 6), [DLV-22](README.md#rule-dlv-22)
> Tasks: the [adoption lane](lanes/adoption.md) of the [delivery graph](delivery-graph.json)

The adoption stage is the one-time reconciliation between the implementation that already exists and the task structure of the [delivery model](README.md). It is **defined here and not executed by the planning change that introduced it**. Nothing in this document certifies existing implementation as conforming: it defines who reviews what, against which evidence standard, and what the review must record before normal parallel execution begins in each repository. Section 4 lists observations made while the plan was researched; they are inputs to the reviewers, not review results.

## 1. Responsibilities

| # | Rule |
|---|---|
| <a id="rule-adp-01"></a>ADP-01 | **Review against the new definitions.** For every delivery task owned by a repository, the adoption reviewer compares the repository's main branch, open pull requests and accepted receipts with the task's outcome, obligations or named parts, write scope, validation and evidence fields. |
| <a id="rule-adp-02"></a>ADP-02 | **Classify each task exactly once:** *inherited* — accepted or newly reviewed evidence satisfies every mapped obligation part; *inherited with adjustment* — the existing work stands but concrete named changes remain, recorded as the task's remaining scope; *gap* — the outcome does not exist, although scaffolding may; *conflicting* — existing work contradicts current design and is raised under [D-001](../../decisions/phase-1-foundation-decisions.md#rule-d-001) before dependent work proceeds. |
| <a id="rule-adp-03"></a>ADP-03 | **Evidence standard for inheritance.** Only reviewed evidence counts: an accepted receipt, or merged source with its retained applicable CI results and publication receipts that the reviewer checks against the task's evidence field. Hello World bootstraps, probes, generated contracts without their vectors, historical dated reviews and unmerged branches are never inherited as completed product behavior. Reported but unevidenced work is located and reviewed like any other task completion, or stays open. |
| <a id="rule-adp-04"></a>ADP-04 | **Map results to the new structure.** Each inherited result names the task and part it satisfies. Existing work that serves an obligation mapped to another repository's task is recorded for that repository's reviewer, not silently claimed. Required adjustments that do not fit an existing task's scope become a planning change that adds a task; obligations never move out of scope. |
| <a id="rule-adp-05"></a>ADP-05 | **Record, then open the repository.** Results are written to the Plan ledger: one record per inherited task and one adoption report per repository with its classification table. When a repository's adoption task is complete, its tasks become claimable under the normal readiness rule. Repositories are adopted independently; none waits for an unrelated repository's review. |
| <a id="rule-adp-06"></a>ADP-06 | **No verification cycle.** Adoption reuses existing receipts and CI results. It performs no public downloads, repeated publication checks, installed-consumer runs, device or hosted runtime tests, and it does not rebuild products except where a task's own evidence field requires a local check that has never been run, under [P2-017](../../decisions/phase-2-specification-decisions.md#rule-p2-017). |

## 2. Stage structure

The baseline freeze runs once; the repository reviews then run in parallel, alongside the documentation reconciliation.

| Task | Owner | Scope |
|---|---|---|
| Baseline freeze | Plan | Record each repository's main head, open pull requests and branches, the latest published candidate per registry, the ledger skeleton and the location of any reported but unmerged work. |
| Repository adoption (one per implementation repository) | That repository's integration owner | Apply [ADP-01](#rule-adp-01)–[ADP-05](#rule-adp-05) to every task owned by the repository and produce its adoption report and ledger records. |
| Documentation reconciliation | Design and Plan | Resolve documentation findings that affect adoption decisions, confirm the generated views match the graph, and record which repositories have completed adoption. |

Exit: a repository's adoption is complete when its report is merged in the Plan ledger with a classification for every owned task. Normal execution in that repository starts immediately under [DLV-22](README.md#rule-dlv-22); tasks whose prerequisites live in a repository not yet adopted stay blocked only on those prerequisites.

## 3. Ledger records produced by adoption

| Record | Location in Plan | Content |
|---|---|---|
| Baseline | `ledger/adoption/baseline.md` | Repository heads, open pull requests, latest candidates, reported-work locations |
| Repository report | `ledger/adoption/<repository>.md` | One row per owned task: classification, evidence references, remaining scope, conflicts raised |
| Inherited task | `ledger/tasks/<task-id>.md` with `status: inherited` | Obligation parts satisfied, receipts and source commits relied on, untested coverage carried forward |
| Planning change | Design and Plan pull requests | New or adjusted tasks for adjustments that do not fit existing scope |

## 4. Observations recorded while planning (unreviewed inputs)

Recorded 2026-09-23 from the repositories' main branches. These are facts for the reviewers to confirm, not classifications.

| Repository (main head) | Observed state | Known adjustment candidates |
|---|---|---|
| Contracts (`e6c4a77`) | Accepted foundation, serialization posture and the 22 published package identities; foundation records include ResourceRef, ResourceVersionRef, BlobRef and ArtifactRef; no capability, action, context, version or health descriptor records, no oversized-body reference record and no business service definitions beyond the bootstrap examples. The user-reported WP03.03 completion was not present in main, branches, worktrees or pull requests. | Locate and review the reported WP03.03 work; shard the shared constraint files before concurrent closures; consumer repositories still pin pre-foundation candidates. |
| DesktopPlatform (`fe8476d`) | Accepted build governance, dependency admission and lockstep NuGet publication; building-block projects are placeholders; native families are probe-level (version, build and error exports) with no instruments library; no downstream consumer of its packages. | Its design-policy check validates the retired work-package graph and serial order; it must be replaced by delivery-graph validation before the Design pin moves (see section 5). |
| ArcNotes (`268c329`), ArcScope (`5e68634`), ArcSlate (`1214224`) | Native AOT bootstraps with accepted build identity and dependency policy; no product domain code. | None beyond adopting the accepted build baseline. |
| Cloud (`ce0a32a`) | Bootstrap Native AOT host and deployment pipeline with build-once, serialized deployment; no product modules, D1 plans, R2 lifecycle or backup code. | Pin the current Contracts candidates when module work starts. |
| AI (`233d1e3`) | Bootstrap Worker and Workflow scaffolding with dependency admission; no Harness behavior. | None beyond the accepted baseline. |
| Web (`120f209`) | Working static-site generator and canonical-host Worker; the Account and Chat application is a placeholder. | Update the stale Contracts SDK pin when the first consumer task starts. |
| Mobile (`d32df20`) | Android bootstrap with the development package identity and a preview-only shared module; transport probe client. | Package identity migration to the permanent Android identity is an existing obligation of the Android foundation task. |
| Design (this repository) | DesktopPlatform's existing corpus checker reports 26 link-label errors and 39 unclassified identifier occurrences that predate the delivery model (mostly links labelled with the validation-policy decision that point to the policy document). | Restore citation integrity before the DesktopPlatform pin moves; the delivery model added no new occurrences. |

## 5. Required documentation-tool adjustment

DesktopPlatform's `eng/design_graph.py` and `eng/design_policy.py` validate the work-package header and section 9 tables, the retired package-level forward and reverse tables, the serial execution line and edge counts, and derive the set of active invariant owners from that serial order. Under [P2-018](../../decisions/phase-2-specification-decisions.md#rule-p2-018) the corresponding specification in [design policy export](../../architecture/29-design-policy-export.md) now requires validation of the delivery graph instead. The DesktopPlatform adoption review records this as an adjustment, and the replacement is implemented through its specification-integrity policy task before DesktopPlatform moves its pinned Design commit. Until then the existing pin remains valid for its glossary and invariant exports.
