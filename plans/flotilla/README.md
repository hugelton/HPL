# Project Flotilla — Design brief v0.1

Status: planning / pre-implementation. 2026-11-26.
This directory is a project planning workspace, not an amendment to HPL, LICENSE, or its FAQ.

## Objective
Create a small independent platform for making, playing and sharing digital musical instruments. An idea that can be completed in one evening should not require a full native plug-in project. Humans and AI have equal access. The platform handles deterministic plumbing, not creative decisions. A work need not become a product; the creator may move the DSP into JUCE, iPlug2 or other environments later.

**Reuse-first mandate:** Rokko took substantial development time. Treat working implementation, tests, bug fixes, UX, tooling and existing instruments as valuable assets. Flotilla is a separate project, not a mandate to rewrite Rokko. Select the smallest viable architectural delta after inspecting the complete local source. Do not choose a new stack merely for stylistic reasons.

## Owner-approved directions (survey)
- A1–7: constraints that encourage creativity; small instruments first; not a professional commercial development framework; originality encouraged but lawful emulations welcomed; human/AI parity; separate project from Rokko.
- B8–15: C is a practical starting point (C99 acceptable), not the sole recommended language; any compatible language allowed. Single-command toolchain setup/build goal; deterministic generation of glue from declarations; a single C source plus minimal declaration should suffice. No official DSP algorithm collection. External libraries permitted. No official IDE.
- C16–23: independently declared audio/MIDI I/O combinations; no stereo-only standard. Transport sync; sequencers; sample loading and recording; no arbitrary universal fixed memory/CPU/parameter ceiling. Multiple selectable instruments per package. Rack/graph hosting left to third parties.
- D24–33: independent DSP/UI WASM; lightweight C GFX recommended, HTML/CSS/JS supported; GFX embedded in HTML possible. Integer 2D graphics, standard fonts/palette/widgets, custom artwork/fonts/bitmaps, generated fallback GUI. Different GUI code per profile; desktop uses normal direct manipulation, not mandatory virtual game buttons.
- E34–41: official UI/device profiles such as Desktop, Compact, Handheld; no all-target requirement, no fixed universal resource budget per profile. Common button/encoder/pointer input. FM-1 exporter as official reference; no official libretro exporter. Native compilation and migration to external frameworks welcomed.
- F42–48: do not blanket-ban OS/file/network access; do not forcibly stop ordinary budget overruns by default; protect audio output; same runtime protections for sideloaded and catalog works; local exact-version restoration. No official FFT/frequency-response analysis suite; recommend publishing validation/performance results.
- G49–55: author/authorized submitter only; no artistic merit gate; independent registries; GitHub Pages template; closed-source and paid works permitted; external payment; AI-use disclosure optional.
- H56–60: source access for official runtime (HPL preference below); third-party compatible hosts including commercial independent implementations; Hügelton stewards core compatibility; no default usage telemetry; avoid ongoing operational/development burden.
- Additional owner requirements: free basic use, negligible fixed operating cost, norns-like catalog plus sideload, creator-controlled package licensing, HPL considered for platform itself. Cloneable GitHub Pages template, no mandatory server/accounts.

## Design boundaries (proposals, verify in audit)
1. Preserve existing Kontakt-like VST/AU loader UX, library selection and user-designed panels wherever viable. A package containing multiple selectable instruments does not require a simultaneous rack.
2. Audio/MIDI/transport/parameter/action/state/asset/input/UI bridge must have shared contracts and deterministic authoring glue. Existing ABI may remain as compatibility layer; choose after audit, not by renaming all exports.
3. DSP/UI separation and profile-specific UI implementations; preserve legacy HTML path. Host capabilities choose compatible UI; missing custom UI can use generated generic controls. Do not force tiny screens onto desktop.
4. Resource claims and host limits are allowed for physical capacity, security and real-time correctness. Do not confuse absence of arbitrary creative limits with absence of safety limits.
5. Proposed permission model: explicit grants, host-mediated file/network/device access, asynchronous non-audio-thread I/O, portable fallback. No silent ambient OS access. Owner must approve exact model. Distinguish ordinary overload warning from trap, runaway execution, unsafe output and emergency interruption. Browser and native trust models differ; native export is not a sandbox.
6. Static catalog and independent author registries, local sideload and exact version/hash preservation. GitHub Actions/Pages are optional author-side deployment mechanisms subject to provider limits. No hosted AI, accounts, central commerce, or official full DSP suite.
7. Public interfaces must allow independent implementations; no AI-generated nondeterministic glue.

## Licensing direction
HPL 1.0 is source-available, not OSI open source. Owner's preference is HPL for the platform itself, but audit actual rights and dependencies first. HPL §§1.2, 3.4, 3.5 distinguish independent plugins/outputs; commercial distribution of HPL-covered platform code or hardware incorporating it can require permission. Independent compatible hosts are a separate case. Keep author-linked ABI headers, generated glue, GFX/widget SDK and template code permissively licensed (MIT proposed) so packages can use any chosen license, including proprietary. Consider a permissive specification license. Preserve existing MIT notices and third-party terms; no retroactive revocation. Do not automatically relicense files or claim compatibility. Review commercial export/runtime bundling, fonts/assets and contributor rights. Legal review is not replaced by this audit.

## Scope / non-goals
No official IDE, language, compiler, AI service, cloud build, node editor, rack, central marketplace, account/payment system, mandatory telemetry, full DSP algorithm library, full analysis suite, or universal official hardware support. Prefer existing standards/toolchains and minimal dependencies.

## Next step
Read [AUDIT_INSTRUCTIONS.md](AUDIT_INSTRUCTIONS.md) and complete [REPORT_TEMPLATE.md](REPORT_TEMPLATE.md) using the actual local Rokko source and related projects. This is a read-only investigation before implementation. No repository creation, migration, licensing edits, or product changes are authorized by this brief. Do not publish private code or findings to this public HPL repository; keep the detailed report local until the owner approves publication.
