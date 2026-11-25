# Chapter 07 — Implementation architecture, privacy, sync, and personalization

The implementation should mirror the cognitive model instead of grafting it onto a conventional `tasks` table.

A possible core schema is:

| Entity | Important fields | Purpose |
|---|---|---|
| `Commitment` | `id`, `kind`, `title`, `outcome`, `domain_id`, `status`, `why`, `created_at` | Durable intention |
| `Action` | `commitment_id`, `next_step`, `actionable_from`, `attention_at`, `deadline`, `deadline_kind`, `estimate`, `energy`, `contexts` | Executable projection |
| `AttentionTrigger` | time, location, device, event, dependency, person, manual-review condition | Determines when sleeping information returns |
| `Dependency` | source, target, type, state | Blocks or relates commitments |
| `Rhythm` | cue/context, preferred window, frequency range, minimum form, ideal form | Recurring behavior without requiring rigid recurrence |
| `ContextBundle` | resources, URLs/document IDs, notes, application references | Materials needed for execution |
| `ResumptionPacket` | checkpoint, next micro-step, unresolved question, context bundle, parked_at | Preserves cognitive task state |
| `Session` | action, started/ended, device, effort, interruption events | Execution history |
| `CalendarConstraint` | start/end, hard/soft, source calendar | Clock-bound availability |
| `Estimate` | likely duration, lower/upper range, confidence/source | Explicit uncertainty |
| `PreferenceModel` | learned tendencies with provenance and reset state | Adaptive ranking |
| `Event` | immutable domain mutation, timestamp, device, version | Sync/audit/history |

The event model matters because a life organizer benefits from being able to answer:

```text
Why is this here?
Why did the system suggest this?
When did the deadline change?
Why did this disappear from Today?
What did the app learn from me?
```

An append-oriented history makes those explanations substantially easier than mutating opaque state in place.

**Local-first storage** is especially appropriate here. The Ink & Switch/Kleppmann formulation describes local-first software as preserving local availability and ownership while supporting cross-device collaboration/synchronization, with privacy and long-term user control among the explicit goals.  For a one-person life organizer, “collaboration” mostly means collaboration among one person’s devices, which removes many social-conflict complexities while retaining the offline/sync benefits.

A practical architecture could look like:

```text
                 ┌──────────────────────┐
                 │ Encrypted sync relay │
                 │  opaque ciphertext   │
                 └──────────┬───────────┘
                            │
              encrypted operation/event sync
                    ┌───────┴───────┐
                    │               │
          ┌─────────▼─────┐   ┌─────▼─────────┐
          │ Desktop       │   │ Mobile        │
          │ local DB      │   │ local DB      │
          │ ranker/model  │   │ ranker/model  │
          │ search index  │   │ search index  │
          └─────────┬─────┘   └─────┬─────────┘
                    │               │
                    └──── active ───┘
                        session
                        handoff
```

The cloud relay need not understand task titles, notes, habits, or behavioral history. Server-side notification functionality may require carefully minimized metadata or encrypted scheduled envelopes, but sensitive semantics should not automatically become server-visible.

For conflict handling, a single-user/multi-device system can often avoid the full complexity of collaborative editors. Still, offline edits from phone and desktop can collide. Conflict-free replicated data type research formalized data structures designed to merge independently updated replicas toward convergence; Shapiro, Preguiça, Baquero, and Zawirski’s 2011 work is the canonical source for CRDTs.  A pragmatic implementation could use CRDT-style sets/sequences only where they actually help, with explicit domain-specific conflict rules elsewhere.

For example:

```text
Completion:
    monotonic event unless user explicitly reopens

Tags/contexts:
    observed-remove set semantics

Notes:
    CRDT text only if simultaneous multi-device editing matters

Deadline:
    field-level last-writer plus visible history

Resumption packet:
    latest active checkpoint wins, but preserve superseded packet in history

Deletion:
    tombstone/event, never silent physical deletion before sync convergence
```

The architecture should prioritize **semantic correctness over theoretical uniformity**.

**Encryption and privacy need a threat model.** At minimum, the design should consider:

| Threat | Mitigation |
|---|---|
| Sync server compromise | End-to-end encryption; server holds ciphertext and minimal routing metadata |
| Lost phone/laptop | OS-backed key protection, device revocation, local database encryption where platform supports it |
| Lock-screen leakage | Notification previews off by default for sensitive categories |
| Behavioral telemetry leakage | No mandatory analytics; local diagnostic logs; explicit opt-in export |
| ML training leakage | On-device personalization by default; no global training on personal content without explicit consent |
| Resource-history overcollection | Store explicit resource references, not indiscriminate screen/application surveillance |
| Account recovery undermining E2EE | Recovery key/passphrase or explicitly documented trusted-device recovery tradeoff |
| Long-lived intimate history | User-controlled retention, selective history deletion, export and complete purge |

The privacy standard should be stronger than “we do not sell your data.” For an app that may know medical routines, relationship commitments, finances, work projects, location cues, personal ambitions, and repeated behavioral failures, **minimization itself is a usability feature**.

**Personalization should proceed in layers.**

The first layer is deterministic:

```text
hard deadline risk
dependency readiness
available time window
current context
explicit user pins
attention horizon
```

The second layer learns simple user-specific patterns:

```text
typical duration error by action type
preferred time for cognitively heavy work
frequently chosen contexts
switching tendencies
routine success by cue/window
repeat-deferral patterns
```

Only a later layer needs a learned ranker. A contextual ranking model can predict *which eligible action the user is most likely to consider appropriate now*, but it should not learn an unconstrained proxy for “importance.” Importance is a normative judgment; observed behavior is not necessarily the user’s desired behavior.

The ranking pipeline should remain auditable:

```text
eligible commitments
      ↓
hard-constraint filter
      ↓
heuristic ranking
      ↓
optional learned adjustment
      ↓
diversity / switch-cost check
      ↓
3–5 candidate actions
      ↓
plain-language reasons
      ↓
user chooses / rejects / browses
      ↓
local feedback update
```

This is a concrete implementation of mixed initiative. Horvitz’s work argues for intelligent automation combined with direct manipulation; Amershi et al. further emphasize interaction when AI is wrong and adaptation over time. 

An LLM can still add value, but its role should be narrow and reversible. Useful functions include turning an unstructured capture into a proposed next action, drafting a resumption checkpoint from recent notes, detecting that “renew passport” probably contains multiple actions, or summarizing a weekly review. It should return **proposals**, not authoritative mutations.

For example:

```text
Captured:
"Need to deal with passport before Japan"

Suggested clarification:
Outcome: Passport renewed
Possible next action: Check expiration date
Potential hard constraint: international trip
Confidence: low — no trip date found

[Accept] [Edit] [Keep raw]
```

That interaction is superior to silently creating six tasks, estimating them, scheduling them, and notifying the user.

**Cross-device continuity should synchronize the active session with special urgency.** Ordinary archived commitments may tolerate delayed background sync. A Park/Resume handoff should propagate quickly because it carries immediate cognitive context. A lightweight active-session record might contain:

```json
{
  "action_id": "a_318",
  "state": "parked",
  "checkpoint": "Test 14 reproduces after nested ternary",
  "next_step": "Inspect parse_expr recovery branch",
  "resource_refs": [
    "repo://parser/src/parser.rs#L441",
    "repo://parser/tests/test_14.rs"
  ],
  "parked_at": "2026-10-03T14:18:00-07:00",
  "source_device": "desktop"
}
```

On mobile, those resource references need not open a desktop IDE. The phone can still show the checkpoint and defer execution. When the user returns to desktop, the complete context becomes actionable again. **Semantic continuity survives even where capability differs by device.**

Platform specialization should therefore look like:

| Desktop | Mobile |
|---|---|
| Horizon Field with broad zoom | Current Focus + Next Fits |
| Rich review and long-range planning | Capture and triage |
| Multi-resource context bundles | Lightweight resume cues |
| Scenario planning / capacity analysis | Context/location-triggered suggestions |
| Bulk clarification | Fast Park / Done / Defer |
| Model inspection and privacy settings | Secure notification controls |

The same database does not require the same interface.

