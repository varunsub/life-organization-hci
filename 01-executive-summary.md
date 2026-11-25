# Chapter 01 — Executive summary

The central HCI problem in personal organization is not “how to store more tasks” or even “how to schedule them.” It is **how to maintain a usable external model of one person’s intentions while attention, memory, available time, motivation, context, and circumstances continuously change**.

That framing follows a long line of personal-information-management research. Malone’s study of physical desks found that organization served a *reminding* function as much as a retrieval function, while Barreau and Nardi later found that computer users preferred location-based finding partly because location itself acted as a reminder, avoided elaborate filing structures, and distinguished roughly ephemeral, working, and archived information.  Task-management and interruption research then showed that the problem extends beyond remembering what exists: people must preserve task state across frequent switches and recover the mental context required to continue. 

Modern productivity applications have improved individual pieces of this problem. Things deliberately controls *when* tasks enter attention through Today, Upcoming, Anytime, and Someday; OmniFocus offers multiple “Perspectives,” defer/planned/due distinctions, contextual tags, and formal reviews; Todoist combines a date-centered Today view with priorities and time blocking; Sunsama turns tasks into a daily itinerary while retaining a less rigid “playlist” alternative; Motion automatically schedules and reschedules work around constraints; and Reclaim treats recurring routines as flexible calendar commitments rather than purely fixed events. 

The synthesis in this report is that a life-organization interface should treat **attention as the primary scarce resource and time as a constraint on attention**, rather than treating tasks as rows and time as empty calendar slots.

I propose a single-user interaction model called the **Horizon Field**. Its defining innovation is a first-class distinction among:

**when an intention exists → when it becomes actionable → when it deserves attention → when it is best executed → when it must be finished.**

Most task systems partially encode two or three of those concepts. The Horizon Field makes all five conceptually distinct while hiding most of that complexity during ordinary use. The visual center contains one **Focus Capsule**—the current action and enough context to execute it. Surrounding “attention horizons” contain only commitments that deserve consideration now, today, soon, later, or during a deliberate review. An item’s distance from the center primarily represents **next-attention time, not deadline**.

The second major innovation is a **Resumption Packet**. Whenever the user leaves substantive work, the system can preserve the actionable state—not merely the task title: “where I stopped,” the next micro-step, relevant resources, unresolved questions, and optionally application/document locations. This directly targets the resumption problem studied by Czerwinski, Horvitz, Wilhite, Iqbal, and Horvitz.  Cross-device continuity therefore means *continuity of cognitive state*, not merely synchronized records.

The third innovation is to replace a global numbered “priority” with a **small, explainable choice surface**. The app first filters for feasibility, then ranks a few candidate actions using deadline slack, outcome importance, available time, context/energy fit, continuity with the present task, routine cadence, switching cost, and uncertainty. It should display explanations such as *“deadline risk,” “fits 25 min,” “same context,”* or *“routine window closing,”* rather than an opaque score. This follows the mixed-initiative principle that automation should cooperate with direct human control, and the later human–AI guidance that intelligent behavior must remain understandable, correctable, and adaptable. 

The resulting design has a deliberate asymmetry:

| Mode | Interface philosophy | Primary question |
|---|---|---|
| **Capture** | Nearly frictionless | “What do I not want to lose?” |
| **Orient** | Selectively informative | “What deserves my attention?” |
| **Focus** | Extremely sparse | “What am I doing, and how do I continue?” |
| **Park / Resume** | Context-preserving | “How do I switch without losing state?” |
| **Review** | Feature-rich | “Does my system still match my life?” |

This resolves much of the apparent conflict between minimalism and feature richness: **richness belongs in the underlying model and review surfaces; minimalism belongs at the moment of execution.**

For habit formation, the design should emphasize stable contextual cues and flexible “rhythms” instead of brittle streaks. In Lally et al.’s field study, participants repeatedly performed a chosen behavior in a stable context over 12 weeks while automaticity was tracked, supporting the importance of repeated context–behavior coupling rather than a universal fixed “days to habit” rule.  Motivation should preserve autonomy and competence rather than turn one’s life into a compulsory points system; those needs sit at the center of Self-Determination Theory. 

For privacy and continuity, the strongest architecture for a one-person app is **local-first by default**: authoritative working data lives on the user’s devices; the app remains useful offline; encrypted synchronization connects devices; cloud computation becomes optional rather than structurally necessary. The original local-first formulation explicitly connects offline operation, multi-device collaboration, ownership, privacy, preservation, and user control. 

The overall design objective can therefore be stated succinctly:

> **Minimize the amount of life the user must keep mentally active, while maximizing confidence that the right intention will return with the right context at the right moment.**

That goal differs fundamentally from maximizing tasks completed, hours scheduled, streak length, or inbox zero.

