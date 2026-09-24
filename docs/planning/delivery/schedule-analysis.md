# Schedule Analysis

> Generated from [the delivery graph](delivery-graph.json) by Plan `tools/delivery.py`; do not edit by hand. Rules and definitions: [delivery model](README.md).

All values below are computed by Plan tools/delivery.py from the current graph. Structural facts (task counts, edge types, chain length, level widths, critical path) are properties of the documented dependencies. Makespans are unmeasured estimates that depend on the stated assumptions. The retired model advanced the same obligations one numbered substep at a time from a single Current task, so its schedule equals the one-worker row; its package-level graph also made each package wait for every upstream package and each substep wait for the previous one.

## Structural facts (computed from the graph)

| Measure | Value |
|---|---|
| Delivery tasks | 529 (6 carried as accepted baseline) |
| Dependency edges by type | artifact 1172, contract 99, design 2, integration(completion) 133, release 42 |
| Remaining work (size units: S=1, M=2, L=4, XL=8) | 1319 |
| Longest dependency chain (levels) | 25 |
| Widest level (tasks whose longest prerequisite chain has equal length) | 66 |
| Critical path length (size units) | 67 |
| Retired model | 447 numbered substeps advanced one at a time from a single Current task |

## Work by lane

| Lane | Tasks | Size units | Owning repositories |
|---|---|---|---|
| [Adoption stage](lanes/adoption.md) | 11 | 14 | AI, ArcNotes, ArcScope, ArcSlate, Cloud, Contracts, Design, DesktopPlatform, Mobile, Plan, Web |
| [Family governance and policy tests](lanes/governance.md) | 16 | 50 | AI, ArcNotes, ArcScope, ArcSlate, Cloud, Contracts, DesktopPlatform, Mobile, Web |
| [Contracts schema closures](lanes/contracts.md) | 25 | 61 | Contracts |
| [Foundation values](lanes/foundation.md) | 7 | 8 | DesktopPlatform |
| [Runtime proofs](lanes/runtime-proofs.md) | 10 | 31 | ArcNotes, ArcScope, ArcSlate, Cloud, DesktopPlatform, Mobile, Web |
| [Desktop platform mechanisms](lanes/platform.md) | 56 | 134 | DesktopPlatform |
| [Native producers and probes](lanes/native.md) | 25 | 54 | DesktopPlatform |
| [Application composition](lanes/app-composition.md) | 8 | 13 | ArcNotes, DesktopPlatform |
| [Embedded assistant](lanes/assistant.md) | 22 | 49 | DesktopPlatform |
| [Execution engine](lanes/execution.md) | 9 | 19 | DesktopPlatform |
| [Application presence and tool bridge](lanes/device-bridge.md) | 12 | 22 | Cloud, DesktopPlatform |
| [ArcNotes](lanes/arcnotes.md) | 35 | 92 | ArcNotes |
| [ArcScope](lanes/arcscope.md) | 27 | 67 | ArcScope |
| [ArcScope Cloud simulator](lanes/simulator.md) | 10 | 36 | ArcScope, Cloud |
| [ArcSlate](lanes/arcslate.md) | 41 | 125 | ArcSlate |
| [Cloud core](lanes/cloud.md) | 60 | 142 | Cloud, DesktopPlatform |
| [Commerce, entitlement and credits](lanes/commerce.md) | 15 | 52 | Cloud |
| [Dynamic policy and configuration](lanes/policy.md) | 11 | 26 | Cloud, DesktopPlatform |
| [Operations, support and trust and safety](lanes/operations.md) | 13 | 35 | Cloud, Web |
| [Knowledge search and retrieval](lanes/search.md) | 8 | 19 | Cloud |
| [Extension platform and integrations](lanes/extensions.md) | 12 | 32 | AI, Cloud, Contracts, DesktopPlatform |
| [Workers AI routing and metering](lanes/ai-routing.md) | 11 | 28 | AI, Cloud |
| [Cloud Harness](lanes/harness.md) | 9 | 38 | AI, Cloud |
| [Android companion](lanes/android.md) | 26 | 63 | Mobile |
| [Web](lanes/web.md) | 31 | 78 | Web |
| [Desktop distribution and update](lanes/updater.md) | 8 | 21 | DesktopPlatform |
| [Release readiness and family release](lanes/release.md) | 11 | 42 | ArcNotes, ArcScope, ArcSlate, Cloud, Contracts, DesktopPlatform, Mobile, Web |

## Critical path

| # | Task | Size | Title |
|---|---|---|---|
| 1 | [ADOPT.01](lanes/adoption.md#task-adopt-01) | S | Freeze the adoption baseline |
| 2 | [ADOPT.03](lanes/adoption.md#task-adopt-03) | M | Adopt Contracts and locate the reported capability and resource closure |
| 3 | [CON.05](lanes/contracts.md#task-con-05) | M | Extension/Connector/LocalBootstrap service schema (annex09 helper closure minus ContentSandbox) |
| 4 | [CON.04](lanes/contracts.md#task-con-04) | L | ContentSandbox service schema (24 methods: session/slot/media/image/PDF/OTIO) |
| 5 | [PLT.09](lanes/platform.md#task-plt-09) | L | Local gRPC transport and framing over Named Pipe/UDS |
| 6 | [PLT.10](lanes/platform.md#task-plt-10) | M | Parent-owned endpoint identity |
| 7 | [PLT.38](lanes/platform.md#task-plt-38) | L | Decision pipeline and the four enforcement points |
| 8 | [PLT.41](lanes/platform.md#task-plt-41) | M | Egress control |
| 9 | [APP.06](lanes/app-composition.md#task-app-06) | M | Context and artifact integration |
| 10 | [AST.03](lanes/assistant.md#task-ast-03) | M | Attachments and provenance |
| 11 | [AST.09](lanes/assistant.md#task-ast-09) | M | Owned-artifact receipt and UX acceptance |
| 12 | [AST.11](lanes/assistant.md#task-ast-11) | L | Cloud client and device runtime (fixture turn endpoint boundary) |
| 13 | [DEV.03](lanes/device-bridge.md#task-dev-03) | M | Owner reauthorization (Device.Runtime local re-authorization) |
| 14 | [DEV.05](lanes/device-bridge.md#task-dev-05) | M | Execution and result deduplication -- Desktop command_log agreement |
| 15 | [DEV.12](lanes/device-bridge.md#task-dev-12) | M | Cross-repo (toolRequestId,attemptId,commandId) agreement between Cloud D1 and Desktop command_log |
| 16 | [DEV.09](lanes/device-bridge.md#task-dev-09) | M | Owned-artifact receipt and real integration |
| 17 | [DEV.13](lanes/device-bridge.md#task-dev-13) | M | Real Harness-planned tool request flowing through the real device bridge end-to-end |
| 18 | [HAR.05](lanes/harness.md#task-har-05) | XL | Own-application execution proof and fixture turn-endpoint removal |
| 19 | [CLOUD.67](lanes/cloud.md#task-cloud-67) | M | Combined AI reopen after Cloud disaster-recovery restore |
| 20 | [REL.06](lanes/release.md#task-rel-06) | XL | Cloud/AI production readiness (deployment, migration, backup, self-host) |
| 21 | [REL.09](lanes/release.md#task-rel-09) | L | Combined disaster drill and operational readiness confirmation |
| 22 | [REL.11](lanes/release.md#task-rel-11) | L | Family release readiness audit and honest statement |

## Level widths

| Level | Tasks |
|---|---|
| 1 | 1 |
| 2 | 10 |
| 3 | 38 |
| 4 | 51 |
| 5 | 53 |
| 6 | 55 |
| 7 | 66 |
| 8 | 41 |
| 9 | 45 |
| 10 | 29 |
| 11 | 22 |
| 12 | 23 |
| 13 | 23 |
| 14 | 21 |
| 15 | 16 |
| 16 | 5 |
| 17 | 8 |
| 18 | 6 |
| 19 | 3 |
| 20 | 1 |
| 21 | 2 |
| 22 | 1 |
| 23 | 2 |
| 24 | 1 |

## Simulated makespan (unmeasured estimate)

Assumptions: task effort is its relative size (S=1, M=2, L=4, XL=8 units, never measured); every worker can execute any task; review, CI, merge-queue and publication latency are not modelled; tasks accepted before this plan count as complete; the adoption tasks run first; a task starts when its start prerequisites and its repository's adoption are complete and finishes no earlier than its completion prerequisites; ready tasks are scheduled longest-remaining-path first. The retired model executed the same work one substep at a time, so its makespan equals the one-worker row. Real throughput will be lower where review capacity, merge queues, shared environments, hardware and provider access, or the single heavy local build slot per workstation become the constraint.

| Workers | Makespan (size units) | Estimated speed-up over one worker |
|---|---|---|
| 1 | 1319 | 1.0× |
| 2 | 660 | 2.0× |
| 4 | 331 | 4.0× |
| 8 | 166 | 7.9× |
| 16 | 85 | 15.5× |
| 32 | 67 | 19.7× |
| 64 | 67 | 19.7× |
| unbounded | 67 | 19.7× |

## Provisional initial ready set

Tasks whose start prerequisites are satisfied once the adoption stage has confirmed the accepted baseline, assuming no other existing work is inherited. The actual first ready set is established by the adoption stage and grows as reviewed existing work is recorded as inherited.

[AND.22](lanes/android.md#task-and-22), [CLOUD.01](lanes/cloud.md#task-cloud-01), [CLOUD.44](lanes/cloud.md#task-cloud-44), [CLOUD.55](lanes/cloud.md#task-cloud-55), [COM.01](lanes/commerce.md#task-com-01), [COM.02](lanes/commerce.md#task-com-02), [COM.05](lanes/commerce.md#task-com-05), [CON.01](lanes/contracts.md#task-con-01), [CON.02](lanes/contracts.md#task-con-02), [CON.05](lanes/contracts.md#task-con-05), [CON.08](lanes/contracts.md#task-con-08), [CON.12](lanes/contracts.md#task-con-12), [CON.13](lanes/contracts.md#task-con-13), [CON.16](lanes/contracts.md#task-con-16), [CON.17](lanes/contracts.md#task-con-17), [CON.18](lanes/contracts.md#task-con-18), [FND.01](lanes/foundation.md#task-fnd-01), [FND.02](lanes/foundation.md#task-fnd-02), [FND.03](lanes/foundation.md#task-fnd-03), [FND.04](lanes/foundation.md#task-fnd-04), [FND.05](lanes/foundation.md#task-fnd-05), [FND.06](lanes/foundation.md#task-fnd-06), [GOV.04](lanes/governance.md#task-gov-04), [GOV.11](lanes/governance.md#task-gov-11), [GOV.14](lanes/governance.md#task-gov-14), [NAT.03](lanes/native.md#task-nat-03), [NAT.06](lanes/native.md#task-nat-06), [NOTES.13](lanes/arcnotes.md#task-notes-13), [NOTES.21](lanes/arcnotes.md#task-notes-21), [OPS.01](lanes/operations.md#task-ops-01), [POL.01](lanes/policy.md#task-pol-01), [PRF.07](lanes/runtime-proofs.md#task-prf-07), [SCOPE.02](lanes/arcscope.md#task-scope-02), [SCOPE.10](lanes/arcscope.md#task-scope-10), [SLATE.01](lanes/arcslate.md#task-slate-01), [SLATE.13](lanes/arcslate.md#task-slate-13), [WEB.01](lanes/web.md#task-web-01), [WEB.08](lanes/web.md#task-web-08)

## Remaining serial dependencies and bottlenecks

- **Adoption stage.** A one-time entry condition: each repository opens when its own adoption review is complete. It adds one review step per repository, run in parallel, and is on every chain once.
- **Contracts merge queue.** Closures are authored concurrently, but every merge to Contracts main publishes all packages at one version, so merges are ordered through one integration owner. Consumers wait only for the closure they use; the descriptor closure and the operation closures their lanes need are the most shared.
- **Cloud foundation chain.** Host pipeline, module boundary and plan bridge, migration runner and physical mapping, identity core, sessions and endpoint mapping precede most Cloud modules and the Harness. It is the densest Cloud prefix and carries must-be-real-early proofs (real email, guarded D1 batches).
- **Assistant and device-bridge chain.** Local helper gRPC and the security decision pipeline precede the assistant Cloud client, the device bridge and the Harness execution proof. The current critical path runs through this chain into the Harness proof and the release tail.
- **Harness fixture removal.** The fixture turn endpoint is deleted only after the desktop assistant, Android and Web consumers each switch to the real Harness, so the Harness proof waits for the slowest consumer switch-over.
- **Release tail.** Cloud and AI production readiness, the combined disaster drill and the family release are necessarily sequential and require every obligation package accepted.
- **External prerequisites.** Hardware-lab devices, provider accounts (mail, payment, payout, push, independent backup storage), store listings and signing custody can block acceptance regardless of worker count. They are recorded on tasks and never passed without evidence.
- **Exclusive resources and review capacity.** The deployed Cloud test environment during live runs, the lockstep publication queues of Contracts and DesktopPlatform, the heavy local build slot per workstation and reviewer availability are not modelled in the makespans and will lower real throughput.
