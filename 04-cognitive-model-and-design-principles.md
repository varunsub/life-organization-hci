# Chapter 04 — First-principles cognitive model and design principles

The proposed first-principles model treats personal organization as a **closed-loop control process over intentions**:

**externalize → interpret → withhold or surface → select → execute → absorb interruption → update → review.**

A conventional to-do application strongly supports the first and final binary state: *task exists / task completed*. A life-organization interface should optimize all of the transitions in between.

The unit of organization should therefore be a **commitment**, not a task. A commitment can be an actionable task, a desired outcome, a routine, an unresolved intention, something waiting on another person, or an idea not yet worth activating. An executable action is one projection of that commitment.

A useful conceptual state model is:

`Captured → Clarified → Dormant | Waiting | Ready → Chosen → Active → Parked → Active → Done | Abandoned`

This yields a crucial distinction:

> **Priority is not an intrinsic numeric property of an action. It is a relationship among an action, the current moment, available context, competing commitments, risk, and the person’s goals.**

“Renew passport” can be low-attention for six months, high-attention when a trip becomes plausible, infeasible when documents are unavailable, and critical when processing slack collapses. Encoding it permanently as `P2` loses that dynamic structure.

The following matrix translates each requested dimension into an explicit HCI requirement.

| Dimension | Failure mode in ordinary organizers | First-principles rule | Proposed mechanism |
|---|---|---|---|
| **Cognitive load** | Large visible inventories require repeated scanning, remembering dependencies, estimating, and choosing | Make the environment carry state; minimize decisions at execution time | Hide ineligible commitments; show one current action and only a few viable next choices; reveal metadata progressively |
| **Attention management** | Due dates, overdue items, badges, and notifications compete indiscriminately | Treat visibility as a scarce resource | First-class `attention_at` and contextual attention triggers; future commitments sleep until they deserve consideration, while background risk checks remain active |
| **Memory support** | The user remembers *that* work exists but not why, where, or how to restart | Store retrieval and resumption cues together with intentions | Capture source, why, next step, associated resource, last state, waiting condition, and resume note; derive lightweight reminders from these cues. This follows the finding/reminding lineage of PIM.  |
| **Context switching** | Switching closes windows but destroys mental state | Treat suspension as an explicit transition | “Park” action generates a Resumption Packet; same-context work is favored when sensible; returning restores the checkpoint. Interruption research makes resumption support a first-class requirement.  |
| **Prioritization** | Fixed P1/P2 rankings become stale and force constant manual maintenance | Separate feasibility from ranking; explain recommendations | Hard constraints filter candidates; soft signals rank a tiny shortlist; UI displays reasons rather than a numerical “AI score” |
| **Habit formation** | Streaks measure outcomes but poorly represent cue–behavior structure | Model rhythms around contexts and acceptable windows | “After breakfast,” “after work,” or “2–4× this week between X and Y”; graceful recovery after misses. Repeated behavior in stable contexts is consistent with Lally et al.’s field design and results.  |
| **Motivation** | Points, warnings, red overdue counts, and autonomous rescheduling can feel controlling | Protect autonomy; make progress interpretable as competence | User chooses commitments; recommendations are reversible; reflection shows meaningful progress without punitive gamification, consistent with SDT’s emphasis on autonomy and competence.  |
| **Short-term planning** | Today lists become aspirational inventories | Make capacity visible before commitment | Daily capacity ribbon; “must / likely / optional” commitment bands; only selected work enters Now |
| **Long-term planning** | Goals and someday ideas either disappear or pollute daily lists | Zoom horizons rather than mix scales | Now → Today → Near → Later → Review/Dormant; long-term commitments periodically move inward as attention triggers mature |
| **Uncertainty** | Exact durations and dates create false precision | Represent uncertainty explicitly but cheaply | Optional duration ranges, hard/soft deadlines, confidence, dependencies, and buffer; planner reasons about slack rather than filling every minute |
| **Interruptions** | A new event forces the user to manually reconstruct the whole day | Re-plan minimally and preserve state | Park current work, protect checkpoint, recompute only affected candidates, and show “what changed” rather than silently rebuilding everything |
| **Privacy** | Life organizer may reveal health, finances, relationships, location, documents, habits, and behavioral history | Data minimization and user ownership are architectural requirements | Local-first authoritative data, encryption, on-device ranking by default, explicit source permissions, retention controls. Local-first research explicitly connects this model to offline use, privacy and user control.  |
| **Minimalism vs. feature richness** | Either simplistic tools lack expressive power or rich tools create continual maintenance | Keep model complexity behind state-specific surfaces | Three primary surfaces—Capture, Horizon, Focus—plus Review; advanced metadata appears only while clarifying or troubleshooting |
| **Adaptive personalization** | Static rules fail to learn; opaque AI undermines trust | Learn from behavior without silently redefining commitments | Suggest, explain, accept/override, learn; hard constraints remain user-owned; explicit reset and correction mechanisms follow mixed-initiative/Human–AI principles.  |
| **Cross-device continuity** | Sync reproduces task data but not working state | Synchronize the active cognitive session | Shared active-session object: current action, checkpoint, resources, elapsed effort, temporary notes, focus/park state |

Several principles emerge from the matrix.

**Visibility should mean relevance, not existence.** A database can contain ten thousand intentions while the execution UI shows one. Hiding is safe only if the user trusts resurfacing. That means every hidden commitment needs an explicit reason or trigger for becoming visible again. This extends the attention-control pattern already visible in Things’ scheduled lists and Someday model. 

**Separate five temporal concepts.**

| Time concept | Meaning | Example |
|---|---|---|
| `created_at` | When the intention entered the system | “Renew passport” captured in January |
| `actionable_from` | Earliest point work can meaningfully begin | Wait until new photo arrives |
| `attention_at` | Next moment it deserves conscious consideration | Review on March 1 |
| `preferred_window` | When execution would fit well | Weekday lunch break |
| `deadline` | Latest acceptable outcome | Passport application by April 15 |

The user should rarely need to fill all five. Defaults and inference keep capture light. But separating them in the model prevents abuse of the deadline field as reminder, start date, priority signal, and schedule simultaneously.

**Eligibility should precede priority.** There is little benefit in ranking an action highly if it cannot currently happen. The system should first form a feasible candidate set:

\[
E_t=\{a\mid ready(a)\land dependencies(a)\land context(a,t)\land attention(a,t)\}
\]

Then it can rank candidates approximately by:

\[
R(a,t)=
f(
\text{deadline slack},
\text{goal value},
\text{window fit},
\text{context fit},
\text{continuity},
\text{rhythm pressure},
\text{uncertainty},
-\text{switch cost}
)
\]

That expression is a design model, not a recommendation to expose numerical life scores. The UI should communicate **reasons**, not decimal utility:

`Due soon · fits 35 min · same project context`

rather than:

`Priority score: 0.843`.

**Complexity should accumulate behind the interface, not in front of the user.** This is the core answer to “minimalism versus feature richness.” A rich semantic model can power a sparse surface. During focus, tags, areas, scoring weights, dependency graphs, ML confidence, and future horizons should mostly disappear.

**Adaptation should change defaults before it changes decisions.** For example, the app may learn that the user consistently chooses writing work in the morning and administrative work late in the day. It can gradually reorder suggestions. It should not silently move a medical appointment, infer that family tasks are “low priority,” or erase work repeatedly deferred. Horvitz’s mixed-initiative framing and Amershi et al.’s guidelines both favor cooperation, correction, and intelligibility over unbounded automation.
