---
title: "Marmot Architecture Wiki"
created: 2026-04-15
updated: 2026-04-16
tags: [marmot, architecture, index]
---

# Marmot Architecture Wiki

A clear-eyed technical reference for the Marmot stack — where it is today, where it's going, and why. Written to help engineers understand the design space before making implementation decisions.

**Read order for engineers:** Start with [[nostr-role-in-marmot]], then [[target-architecture]], then whichever section is most relevant to your work.

---

## Current State

### [[index|Overview]] (this page)
The current three-repo stack and how the pieces fit together today.

### [[codebase-survey]]
Raw metrics: LOC counts, dependency graphs, module structures for whitenoise, whitenoise-rs, and mdk. Facts, not opinions.

### [[whitenoise-rs-deep-dive]]
Deep analysis of the application layer — where the complexity lives, how the session-projection refactor changes things, what the current data flow looks like.

---

## Foundations (read these first)

### [[nostr-role-in-marmot]]
The three distinct roles Nostr plays in Marmot — identity, application message format, and transport — and why they're deliberately separable. Clears up a common source of confusion about what "Marmot uses Nostr" actually means. Start here if you're new.

### [[target-architecture]]
The complete target system design in one document. Covers:
- The four components: `CgkaEngine`, `TransportPeeler`, `TransportAdapter`, application layer
- The two-layer message model (outer transport encryption + inner CGKA encryption)
- Inbound and outbound data flows with Rust trait sketches
- The `SendResult`/`PendingStateRef` outbound contract (publish-before-apply)
- Data flow from engine to UI (GroupEvent stream → DB projections → broadcast channels)
- Multi-transport simultaneous operation
- The four-step migration path

---

## Design Deep Dives

### [[cgka-engine-design]]
Detailed design for the CGKA Engine layer — the heart of the system. Covers:
- What the `CgkaEngine` trait looks like
- Which internal subsystems should be explicit state machine enums (EpochState, WelcomeState, MemberState) and which shouldn't
- The five internal subsystems: GroupLifecycle, MessageProcessor, EpochManager, CapabilityManager, KeyPackageManager
- Storage trait design — what to keep, what to fix (removing Nostr types from storage)
- The feature registry — replacing static constants with a runtime-queryable system
- Transport features as first-class citizens (NostrGroupData as one feature among many, not a special case)
- Pragmatic migration order

### [[capability-negotiation]]
How Marmot determines which features are available in a group, how groups upgrade over time, and how the UI communicates this. Covers:
- Progressive enhancement philosophy (create the best group possible, never block on ideal)
- The three capability queries: `constructable_capabilities()`, `upgradeable_capabilities()`, `feature_status()`
- Group creation: automatic RequiredCapabilities from member intersection
- Automatic upgrade via self-updates
- The admin group upgrade action
- What needs to be built in MDK
- The MIP checklist going forward

---

## Historical Context

### [[architectural-alternatives]]
The full survey of six architectural alternatives considered before landing on the target architecture. BeeKEM, causal-order CGKAs, state machine model, crate decomposition, coordinator patterns, FIPS as transport layer. Useful context for understanding *why* the target architecture looks the way it does.

### [[decision-points]]
Seven key architectural decisions with explicit recommendations. Several are now resolved (marked ✅). Read this to understand the key open questions and what's already been decided.

---

## Current State vs. Target State

| Layer | Today | Target |
|---|---|---|
| Presentation | Flutter (whitenoise) | Unchanged |
| FFI bridge | flutter_rust_bridge | **whitenoise-ffi** — transport-agnostic, outputs Dart + Swift |
| Application | whitenoise-rs singleton (`Whitenoise`) | **whitenoise-core** — thin facade, per-account sessions |
| Transport | Nostr relay control planes (embedded in whitenoise-rs) | `TransportAdapter` trait, `NostrAdapter` as first impl |
| CGKA Engine | MDK — monolithic, Nostr types in API | MDK implementing `CgkaEngine` trait, Nostr types removed from storage |
| Crypto | OpenMLS (direct) | OpenMLS behind `CgkaEngine` trait, swappable |
| Storage | `MdkStorageProvider` (good design) | Same + `CapabilityStorage` added, `Group` type de-Nostr-ified |

**The four migration steps:**
1. **Session projection** (in progress) — decompose whitenoise-rs singleton into per-account sessions
2. **Coordinator in MDK** — formalize sequencer, define `TransportMessage`/`PeeledMessage`, introduce `TransportPeeler` trait
3. **CGKA trait** — abstract OpenMLS behind `CgkaEngine` trait, clean Nostr types from MDK public API
4. **Transport adapter** — extract relay control planes into `TransportAdapter` trait; whitenoise-core becomes the wiring layer

---

## The Current Stack (detail)

```
┌──────────────────────────────────────────────┐
│  whitenoise (Flutter)                        │
│  66K LOC Dart · Riverpod + hooks             │
│  Presentation — thin, not a source of risk   │
├──────────────────────────────────────────────┤
│  whitenoise-rs (~100K LOC Rust)              │
│  Application layer — the complexity center   │
│  · Nostr relay control planes                │
│  · Account lifecycle                         │
│  · MLS/MDK integration                       │
│  · Message aggregation, chat list, search    │
│  · Push notifications, scheduled tasks       │
│  Session-projection refactor in progress     │
├──────────────────────────────────────────────┤
│  mdk (~66K LOC, 6 crates)                    │
│  Protocol/crypto layer                       │
│  · OpenMLS 0.8.1 wrapped with Nostr-aware API│
│  · Epoch snapshot + rollback system          │
│  · Storage trait abstraction                 │
│  · UniFFI bindings (Swift/Kotlin/Python)     │
└──────────────────────────────────────────────┘
```

**The core tension:** MLS requires total linear ordering of commits. Nostr relays provide unordered, unreliable pub/sub. Every piece of complexity in the relay control planes, event processor, epoch snapshot system, and scheduled tasks exists to bridge this mismatch. The target architecture resolves this by introducing the coordinator/sequencer as a first-class component in MDK.

---

## Key Decisions Already Made

- **PCS is non-negotiable.** Both FS and PCS are required. Sender Keys are off the table.
- **MLS stays.** BeeKEM and other causal-order CGKAs are interesting but too immature to adopt now. The `CgkaEngine` trait makes them swappable in future without a rewrite.
- **Transport is pluggable.** FIPS mesh and other transports are first-class future targets. The architecture is designed for this from day one.
- **whitenoise-ffi, not whitenoise-frb.** The FFI bridge is not Flutter-specific — it will output Swift bindings too.
- **Nostr has three distinct roles.** Identity (always), unsigned event structure for app messages (always), relay transport (pluggable). See [[nostr-role-in-marmot]].
- **One capability per feature.** Flat feature registry, no dependency graph. See [[capability-negotiation]].
- **Progressive enhancement, not hard breaks.** Create the best group possible, upgrade gracefully, never block communication.
