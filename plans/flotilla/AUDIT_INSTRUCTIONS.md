# Claude Code — Rokko → Flotilla reuse audit

## Task
Perform a source-grounded feasibility and migration audit on the owner's local Rokko project and related assets. Produce a practical plan that minimizes rewrites, preserves proven behaviors and makes hidden development work visible. Follow [README.md](README.md) as owner direction and [REPORT_TEMPLATE.md](REPORT_TEMPLATE.md) as deliverable structure. The existing plan is not proof of what is implemented.

## Rules
- Audit only. Inspect local repositories, including uncommitted work, without changing them. Do not reset, clean, stash, checkout over edits, install system dependencies, sign/publish, push, or migrate files. Do not create Flotilla yet.
- Discover actual repository roots and local workspaces; do not assume the public SDK is the complete project. Ask only if paths cannot be located in authorized workspace. Do not scan unrelated personal files.
- Record branch, HEAD, dirty state, relevant uncommitted changes, submodules, lockfiles, and build provenance. Never expose tokens, signing keys, credentials, or private paths beyond what the local report needs.
- Read actual implementations and tests, not README alone. Mark documented-only or inaccessible components as such. Use repo-relative file:line ranges and commit SHA; note evidence from dirty files. Distinguish observed, built, tested, inferred, and unknown.
- Where feasible run existing non-destructive tests/builds in an isolated temporary build directory/copy; do not mutate the original checkout or DAW installation. Do not download dependencies or run untrusted packages without authorization. If a test needs unavailable hardware, toolchain, permissions, or modifies tracked files, report the blocker. Do not call an untested module production-ready.
- Reuse before refactor, refactor before replace. For every rewrite proposal, prove why an adapter or surgical change is insufficient and give the cost/risk and rollback path. Avoid cosmetic renaming of internal stable interfaces unless required.
- No proprietary source excerpts, secret material, or detailed private audit results pushed to public HPL. Report stays local. Do not commit or push without separate permission.

## Investigation workflow

### 1. Inventory all relevant repositories
Identify Rokko desktop/player source (private/local if present), rokko-sdk, rokko-library, relevant existing instrument source repositories, and reusable FM-1/Felucca/Lorcha hardware/GUI assets only if locally available. Include build targets, source layout, dependencies, licenses, release and test assets, scripts, CI, branding and documentation. Record missing components explicitly.

### 2. Trace actual end-to-end behavior
Trace package loading, signature/hash validation, archive extraction, library install/cache/version selection, DSP instantiation, DAW audio/MIDI/automation, preset/state restoration, UI host/bridge, hot reload, error handling, and web trial. Identify source files, calling relationships, synchronization, memory ownership, assumptions and bugs. Trace at least one instrument, effect and MIDI module if available.

### 3. Reuse matrix
Assign each component KEEP (copy unchanged except packaging), ADAPT (bounded changes), WRAP (preserve behind new interface), REPLACE (justified incompatibility), NEW (missing capability), or DEFER (nonessential). Include dependency chain and exact import path, tested status, license, effort range, compatibility impact and a preservation test. Look at fixes in git history and regression tests; do not estimate reuse from LOC alone. List existing non-code assets and generated/build tooling separately.

Public SDK leads to verify against the local revision:
- include/rokko_abi.h, include/rokko_math.h, test/
- tools/rokko-check/src/lib.rs (Wasmtime runtime and C FFI); tools/rokko-check/src/bin/rokko_check.rs and render_ref.rs
- tools/rokko, tools/rokko-render.mjs, template/, schema/
- kit/rokko-kit.css, kit/rokko-kit.js, types/rokko.d.ts
- tools/web/web/rokko-web.js, rokko-worklet.js, tools/web/serve.py, tools/web/assets/rokko-panel.html
- docs/API_V1.md, BUNDLE_ABI.md, BUNDLE_UI.md, BUNDLE_AUTHORING.md, GUIDELINES.md
- examples/chord, tremolo, engines and library index.json/index.json.sig
These are leads, not mandatory new names or guaranteed compatible components.

### 4. Gap analysis against owner decisions
For every requirement in the brief, map existing support, missing behavior, minimal migration approach and acceptance test. Specifically:
- Audio buses/channel counts, MIDI input/output/event offsets, tempo/transport, automation and DAW constraints (VST3/AU classification, host differences, parameter identity).
- Stable ABI and versioning; declaration-driven generation with reproducibility, single source workflow, other WASM languages, SDK install/build/pack.
- State serialization, bounded GUI↔DSP exchange, sample assets/loading/recording, immutable resource identifiers, state migration, exact version/hash restoring offline.
- GUI HTML bridge and sandbox, GFX WASM independent module, input events, generated fallback, profile-specific UI, HTML+GFX composition. Investigate actual desktop player UX and reusable browser/player assets; do not mandate uniform screen geometry.
- Multi-instrument package manifest and resource sharing, catalog/sideload and registry trust keys, author-owned static deployment, paid packages without platform payments.
- Real-time safety: no blocking/allocating in callback where avoidable; timing, overload, interruption, NaN/Inf/DC/peak handling, buffer bounds, lifecycle timeouts, GUI crashes, ZIP/path traversal, permissions, browser iframe isolation/CSP and worklet runaway behavior. Existing SDK has fixed stereo assumptions and limits; investigate actual code and decide what must become configurable versus remain a safety boundary. Do not remove watchdog solely because owner rejects routine CPU budget stopping.
- Native FM-1 reference exporter: inspect actual integration, toolchain, hardware capacity, audio/MIDI/input constraints, licensing and safe install/rollback. No mandatory libretro work. Native export requires source or suitable compiled object and a separate trust model; do not promise arbitrary WASM-to-native portability.

### 5. Compare migration strategies
At least compare (A) clone/split Rokko player and SDK into Flotilla with small delta, (B) shared core/extracted runtime + new wrappers, (C) compatibility-first new ABI with adapter for Rokko V1. Consider a limited rewrite only if evidence requires it. Compare preserved functionality, code duplication, drift, dependency/maintenance cost, migration effort, security, licensing, reversibility and independent release. Recommend one and explain rejected alternatives. Distinguish reusing source from requiring Rokko bundle compatibility forever.

### 6. License audit
Record per-component ownership, license, evidence, dependency terms and target license. Check HPL restrictions versus bundled runtime/commercial compatible host/export; distinguish independently created compatible implementations from HPL-derived ones. Check permissive SDK and generated glue boundaries, static links, font/art assets, existing third-party notices, VST/AU framework terms, and any copyleft incompatibilities. Do not change a license. Flag questions for owner/legal review.

### 7. Minimal vertical slice / roadmap
Propose first milestone using existing working Rokko code and an existing simple instrument. Demonstrate one declaration → build → validation → same audio behavior in web and desktop DAW (where available) → save/restore → local install. Keep existing behavior as regression baseline. Next prove GFX + alternate profile and native FM-1. Defer catalog polish, broad device support and nonessential features until slice succeeds. Separate migration from new product features. Give ordered tasks, dependencies, acceptance criteria, rough effort ranges with confidence (not unsupported precise estimates), maintenance costs and stop/go gates.

## Output
Create a local Markdown report named `FLOTILLA_ROKKO_AUDIT.md` using the template. Optionally include `reuse-matrix.csv` with the same component IDs and `audit-evidence.md` with test command/result logs. Report actual repository revisions and test environment, including failed/not-run tests. Do not commit to HPL or publish the report. End with a compact set of owner decisions (yes/no or mutually exclusive choices), recommending defaults separately. No implementation until owner reviews the report.

Suggested invocation from a local HPL clone:
```text
Read plans/flotilla/README.md, AUDIT_INSTRUCTIONS.md and REPORT_TEMPLATE.md.
Audit my existing local Rokko project and related authorized source trees.
Maximize reuse of working code and proven behavior. Do not modify any project.
Write FLOTILLA_ROKKO_AUDIT.md locally in the agreed working directory.
If a repository cannot be located, report it and continue with available evidence.
```
