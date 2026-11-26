# Flotilla — Rokko Reuse Audit
Status: DRAFT | Date: YYYY-MM-DD | Auditor: | Owner review: pending

## 0. Executive decision
- Recommended migration strategy:
- Why this preserves the most existing value:
- Highest-risk unknown:
- First deliverable and acceptance gate:
- Reuse assessment: counts by KEEP/ADAPT/WRAP/REPLACE/NEW/DEFER; scope and weighting method. No invented reuse percentage.

## 1. Evidence and scope
| Repository/component | Local root (local report only) | Branch/commit | Dirty state | License | Inspected/built/tested | Missing evidence |
|---|---|---|---|---|---|---|
| Rokko player | | | | | | |
| SDK | | | | | | |
| Library | | | | | | |
| Instrument sources | | | | | | |
| FM-1 / related assets | | | | | | |

Environment: OS/arch, compilers, dependencies, DAW/hardware versions, audit date. Explain limitations. Cite repo-relative paths and lines with revision. Mark dirty evidence. Never include secrets.

## 2. Current architecture (as implemented)
Diagram of package → library/loader → runtime → DAW/audio/MIDI and UI/bridge; include browser, CLI, validator, state/preset/cache. Explain threading, ownership, safety, and hardcoded assumptions. Distinguish actual implementation from documentation.

## 3. Reuse matrix (one row per meaningful component)
| ID | Component/function | Source path:line / revision | Status: observed/tested/etc. | Decision | Exact reuse/change | Dependencies | License | Risk | Effort range/confidence | Preservation test |
|---|---|---|---|---|---|---|---|---|---|---|

Cover native player/FFI, UI shell, Wasmtime, ABI, audio/MIDI, transport, parameters, state, preset/automation/cache, HTML bridge/kit, web/worklet, CLI, validator/render, templates, build/CI, library/signing, graphics, example instruments, assets, FM-1 export. Include existing regressions/fixes from history. For REPLACE, explain why KEEP/ADAPT/WRAP fail. For NEW, state evidence of absence. Report component counts and effort/risk weighting; do not imply LOC equals value.

## 4. Requirements traceability
| Owner survey ID / requirement | Existing support + evidence | Gap | Minimum delta | Acceptance test | Priority | Open decision |
|---|---|---|---|---|---|---|

Cover all 60 survey IDs as grouped in README, plus HPL, free use, creator-owned package license, static Pages template. Label proposed design details as proposals, not owner approvals.

## 5. Strategy comparison
| Strategy | Preserved assets | Compatibility | Effort/confidence | Ongoing maintenance | Safety/license risk | Rollback | Verdict |
|---|---|---|---|---|---|---|---|

A: clone/split with small delta. B: shared/extracted core. C: new ABI with V1 adapter. Add alternatives only when evidence warrants. Explain why selected path wins and why rejected alternatives lose.

## 6. Proposed technical architecture
- Reuse boundaries and repo layout (proposed, not implemented).
- ABI/version negotiation; deterministic declaration→generated glue; supported language/toolchain path.
- Audio/MIDI/transport and DAW constraints.
- Parameter identity, actions, state versioning, presets, assets, sample recording and offline restoration.
- HTML/GFX bridge, per-profile selection and fallback, input mapping.
- Resource/capability model, overload vs emergency interruption; native vs browser differences.
- Multi-instrument packages, local install, distributed catalog and author Pages deployment.
- Native FM-1 exporter path, source availability, device-specific limits and tests.

For each, specify what stays unchanged, what changes, which interface owns it, and what remains undecided.

## 7. Licensing / provenance
| Component | Current license & evidence | Owner/third party | Proposed treatment | Obligations / HPL compatibility | Blocker |
|---|---|---|---|---|---|

Separate HPL platform, permissive author-facing code, independent packages, native export/runtime bundling and independent compatible hosts. Explicitly list inherited notices and unresolved rights. No relicensing performed.

## 8. Risks and validation evidence
| Risk | Likelihood/impact | Current mitigation/evidence | Proposed mitigation | Blocking milestone |
|---|---|---|---|---|

| Test ID | Command/environment | Expected | Actual | PASS/FAIL/NOT RUN | Log/evidence |
|---|---|---|---|---|---|

Include load/init hangs, runaway DSP, bad pointers/buffers, nonfinite and dangerous audio, malformed archives, malicious HTML/network, state mismatch, host incompatibilities, native hardware risks. Include regression tests for known existing behavior. Note tests that cannot be run.

## 9. Roadmap (migration first)
| Milestone/task ID | Reuse matrix IDs | Change | Prerequisites | Effort range / confidence | Acceptance test | Rollback |
|---|---|---|---|---|---|---|

- M0: baseline build/test and provenance, owner approves strategy.
- M1: minimal end-to-end vertical slice with existing instrument in desktop and web, state restoration, existing regression baseline.
- M2: ABI/declaration extensions and GFX/profile proof.
- M3: static distribution and catalog, only necessary player changes.
- M4: FM-1 reference export and documented portability proof.
Adjust order if evidence requires; identify critical path. Distinguish MVP from eventual owner-approved requirements. Estimate recurring costs (including CI/signing/OS updates, support, catalog moderation), not just implementation effort.

## 10. Owner decisions
| ID | Yes/no or alternatives | Evidence / consequence | Recommended default | Blocking? | Owner answer |
|---|---|---|---|---|---|

Only unresolved choices, no repeat of settled survey decisions. Clarify conflicts such as resource limits, trusted/native execution, HPL versus commercial reuse, and backward compatibility. Recommendations are not decisions.

## 11. Audit completion
- Original source trees unchanged: verified/not verified; details.
- Missing access and unresolved blockers:
- Assumptions and uncertainty:
- Files/revisions examined:
- Next action after approval:
- No implementation or public publication authorized by audit alone.
