# Chapter 06 — Interaction flows, feature set, usability evaluation, and tradeoffs

A coherent feature set follows from the model; it should not begin as a checklist of conventional productivity features.

| Feature | Interaction | Cognitive purpose |
|---|---|---|
| **Frictionless Capture** | One text/voice/share-sheet gesture; optional source backlink | Prevent prospective-memory rehearsal |
| **Clarify Later** | Captured item need not receive project, priority, due date, tags, or estimate immediately | Avoid making organization a prerequisite for remembering |
| **Attention Horizon** | Now / Today / Near / Later / Dormant placement | Control what enters awareness |
| **Focus Capsule** | One executable action plus immediate context | Reduce scanning and selection load |
| **Next Fits** | Tiny shortlist of feasible next actions with explanation chips | Support prioritization without opaque “AI priority” |
| **Resumption Packet** | Park with checkpoint, next move, resources, unresolved issue | Make interruption recovery explicit |
| **Capacity Ribbon** | Approximate commitment pressure across days/weeks | Connect intentions to finite capacity without overscheduling |
| **Flexible Rhythms** | Context/window/frequency/minimum form | Support habit repetition without streak fragility |
| **Waiting Conditions** | “Waiting for Alex,” “after package arrives,” “when at pharmacy” | Prevent blocked work from polluting actionable views |
| **Scenario Peek** | “What happens if I defer this?” | Make downstream deadline/capacity effects visible before commitment |
| **Zoomed Review** | Inspect dormant, repeatedly deferred, risky, or directionless commitments | Keep hidden information trustworthy |
| **Why This?** | Explanation for every adaptive suggestion | Preserve intelligibility and correction |
| **Active Session Handoff** | Resume current state from another device | Make cross-device continuity cognitive, not merely database-level |
| **Local Privacy Controls** | Per-source capture permissions, history retention, private fields, ML controls | Bound the surveillance potential of an intimate organizer |

Several concrete interaction flows illustrate how these pieces fit together.

**Morning orientation.** The app should not begin by asking the user to manually rank an entire list. It opens with the capacity ribbon, fixed commitments imported from calendars, rhythms whose windows matter today, and perhaps two or three commitments whose attention conditions have matured. The user accepts, removes, or promotes a small set into Today. Exact scheduling remains optional.

This differs subtly from Todoist’s Today view, which aggregates every task carrying today’s date, and from Sunsama’s more deliberate calendar-oriented daily planning.  The Horizon Field treats “today deserves awareness” and “today has a scheduled time” as separate decisions.

**Beginning work.** Selecting a candidate opens the Focus Capsule, not the full project database. Previous resume context appears automatically if one exists. Notifications unrelated to hard safety/communication rules can be delayed until a user-defined breakpoint or the focus session ends. The user can always expose the broader Horizon Field manually.

**Receiving an interruption.** Suppose a call requires immediate attention. Pressing Park produces a one-line checkpoint:

> “Stopped before changing recovery branch; run test 14 after edit.”

If application integration is enabled, the packet also stores document/resource references. The current commitment moves to `Parked`, not back into an undifferentiated open-task list.

**Unexpected free time.** The user has 25 minutes before leaving home. Rather than scanning 80 tasks, the Next Fits query uses current location/device, available duration, readiness, attention status, and switching continuity. It might offer:

```text
Review insurance renewal      15–25m · home document available
Call pharmacy                  ~10m · closes in 50m
Continue parser checkpoint     20m+ · context ready on laptop
```

This is where context-aware organization becomes materially different from sorting a list by due date.

**Weekly zoom-out.** The interface expands from attention management into commitment management. It highlights items that repeatedly surfaced and were rejected, outcomes with no viable next action, overloaded horizons, dormant commitments approaching deadlines, stale waiting conditions, and rhythms losing their intended context. The user decides whether to reactivate, redefine, defer, or abandon. Nothing should be silently “cleaned up” by AI.

**Long-term planning.** A quarter-scale zoom does not show every individual action. It shows outcomes, recurring capacity claims, known hard events, and directional imbalance—for example, health commitments repeatedly losing all discretionary capacity to work. This allows “life planning” without turning every life domain into a corporate project-management dashboard.

**Motivational feedback.** The review surface should privilege evidence of capability:

```text
You underestimated coding sessions by ~35% this month.
Three administrative tasks were completed successfully in 20-minute gaps.
Your walking rhythm is most reliable immediately after lunch.
You repeatedly deferred "research guitar lessons"; keep, redefine, or release it?
```

This feedback is intended to strengthen realistic self-knowledge and competence, rather than maximize app engagement. That posture is more compatible with autonomy-supportive motivation than compulsory scoring. 

The design also has substantial tradeoffs.

| Design choice | Benefit | Risk | Mitigation |
|---|---|---|---|
| Hide future/ineligible commitments | Dramatically cleaner execution view | “Out of sight, out of mind” if resurfacing fails | Explicit attention triggers, risk scanner, scheduled review, searchable full inventory |
| Dynamic Next Fits ranking | Less manual prioritization | User may become dependent on opaque recommendations | Reason chips, manual browse, pins, deterministic rules first, full override |
| Attention date separate from due date | Better control of consciousness | Adds another temporal concept | Infer defaults; expose field mainly during planning/review |
| Resumption packets | Faster and more reliable recovery | Capture friction; sensitive working-state data | One-tap templates, automatic draft + manual edit, local storage, retention limits |
| Duration ranges | More honest plans | More data entry than one estimate | Permit `~`, learn ranges automatically, make field optional |
| Flexible rhythms | Handles real life better than fixed recurrences | Too much flexibility can weaken cues | Preserve preferred context and show stability rather than endlessly moving routines |
| Rich semantic data model | Enables powerful personalized views | Configuration temptation | Progressive disclosure and strong defaults |
| Aggressive local-first privacy | Ownership, offline operation, low cloud exposure | Harder sync, recovery, search and ML infrastructure | Encrypted sync relay, explicit backup/recovery, selective cloud features |
| Cross-device active session | Low-friction continuity | Could encourage excessive switching | Handoff preserves state but does not prompt switching; Focus remains primary |
| Single-user optimization | Can encode idiosyncratic routines without team compromises | Poor collaboration model | Keep collaborative items as external references rather than redesigning the whole system around teams |
| ML personalization | Adaptation to actual behavior | Bias, surveillance, loss of agency | On-device first, bounded actions, explainability, confidence thresholds, reset/delete learning history |

The most dangerous failure mode is **premature intelligence**. A prototype should not begin with an LLM deciding what the user “should” do. It should begin with a transparent rules engine and an excellent underlying information model. Only after enough behavior exists should personalization reorder candidates or suggest patterns. This ordering is consistent with mixed-initiative design and human–AI guidance emphasizing correction, understandable capabilities, and appropriate adaptation. 

A serious usability evaluation should measure **cognitive and interaction outcomes**, not just “tasks completed.”

For a system explicitly optimized for one person, the most informative evaluation would combine a within-person longitudinal study with targeted interaction tests:

| Evaluation question | Useful measure |
|---|---|
| Does capture reduce memory burden without creating a dirty inbox? | Capture latency; unclarified-item age; self-reported confidence that intentions are safe |
| Does the Horizon Field reduce choice effort? | Time from opening app to choosing work; number of items inspected before selection |
| Does Focus reduce unnecessary switching? | Voluntary switch frequency; number of concurrently active commitments |
| Do Resumption Packets work? | Time from return to productive action; need to reopen/search unrelated resources; subjective “where was I?” rating |
| Is planning more realistic? | Estimated versus actual effort distribution; daily plan churn; number of forced deferrals |
| Does hiding remain trustworthy? | Forgotten commitment incidents; frequency of searching for items assumed lost |
| Does personalization help? | Suggestion acceptance, override patterns, ranking regret after reflection |
| Does the system preserve autonomy? | User-reported control; rate of manual overrides without penalty; qualitative interviews |
| Is the rich model becoming maintenance work? | Metadata-editing time versus execution time |
| Does cross-device handoff preserve context? | Resume latency after moving mobile ↔ desktop |

A practical single-user field protocol could use an **ABAB-style comparison**: conventional list/calendar baseline → Horizon Field → baseline → Horizon Field, each for enough days to encounter recurring work and interruptions. Exact duration should depend on the user’s routine cadence rather than an arbitrary universal number. A longer final deployment is needed to study habit/rhythm effects because habit formation unfolds through repeated context exposure, not a one-session usability test. 

Qualitative “critical incident” logging would be especially valuable. Whenever the system makes a bad recommendation, hides something the user expected, interrupts at the wrong time, or successfully restores a difficult task after interruption, capture the incident. Those cases reveal model failures that aggregate completion counts hide.

Success should therefore mean something closer to:

> **less planning overhead, fewer forgotten commitments, lower resumption friction, fewer unwanted switches, more realistic capacity commitments, and greater subjective control**

rather than simply “more checkmarks.”

