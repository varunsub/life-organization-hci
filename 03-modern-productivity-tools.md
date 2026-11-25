# Chapter 03 — Modern productivity tools: useful interaction patterns and the remaining gap

The comparison below uses current official documentation available in early October 2026. It is deliberately about **interaction patterns**, not product rankings.

| Tool | Primary interaction idea | Attention model | Temporal model | Automation | Particularly useful lesson | Gap relative to a life-optimized view |
|---|---|---|---|---|---|---|
| **Things** | Opinionated lists around when work should appear | Today, Upcoming, Anytime, Someday; future work can disappear until relevant | Start dates, deadlines, repeating rules; calendar context | Low | Visibility itself can be scheduled. Things explicitly says its date-based lists control when tasks “come to your attention.”  | Still fundamentally task/project objects; limited representation of uncertainty, resume state, energy, or interruption recovery |
| **Todoist** | Flexible task database centered around Today/Upcoming and projects | Today aggregates all dated tasks; explicit priorities can float items upward | Dates plus draggable calendar time blocks/durations | Low–medium | Easy transition from inventory → day plan; official guidance explicitly encourages rescheduling overloaded days.  | Date assignment remains central to visibility; context and cognitive continuity are secondary |
| **OmniFocus** | High-dimensional personal task model exposed through Perspectives | User-defined and standard views; contextual tags may encode people, places, state of mind or energy | Distinct due, planned and defer dates in Forecast, alongside calendars | Medium through rules/automation | Rich underlying metadata can support many personalized views; Review is first-class.  | Capability can become configuration burden; execution still resolves primarily to outlines/actions |
| **Sunsama** | Deliberate daily planning that translates tasks into time | Today/focus/planning rituals | Timeboxing creates calendar working sessions; “playlist” preserves sequence without exact clock commitments | Medium | It acknowledges that exact timeboxing and ordered-but-flexible execution suit different kinds of days.  | Daily scheduling can still overfit an uncertain day; interruption-resumption state remains external to the task representation |
| **Motion** | Scheduler as active planner | Algorithm decides where tasks belong given constraints | Availability, task duration/chunking, deadline, priority, start date and recurrence drive dynamic placement | High | A schedule can be treated as a continuously recomputed hypothesis rather than a static promise.  | High automation risks opacity and schedule churn; user values and cognitive switching costs are harder to encode |
| **Reclaim** | Flexible defense of time for tasks and routines | Priorities and flexible “smart” events compete for calendar capacity | Habits use scheduling windows, duration bounds, frequency and ideal times; conflicts can trigger rescheduling | High | A routine need not mean “Tuesday exactly at 12:00”; it can mean “find a feasible slot in this acceptable window.”  | Calendar remains the dominant representation; not every life intention benefits from occupying a time block |

Several particularly strong modern patterns deserve preservation.

**Attention gating.** Things is the clearest example: a future item can be absent from Today, Anytime, and even prominent navigation until its start date arrives; Someday explicitly keeps vague ideas out of actionable views.  This aligns unusually well with the PIM observation that *what remains visible* affects reminding. The deeper design rule is not “use start dates.” It is **permit intentional non-visibility without losing trust**.

**Multiple projections of one underlying model.** OmniFocus calls these Perspectives and lets tags represent not only categories but people, places, things, states of mind, and energy. Its Forecast projection combines work with due/planned/defer dates and calendars, while Review supports a distinct maintenance activity.  This is valuable because planning and execution genuinely require different projections. The mistake would be to expose every projection simultaneously.

**Inventory-to-time translation.** Todoist and Sunsama make the bridge from “something I intend to do” to “when I will work on it” increasingly direct. Todoist’s calendar layout lets a dated task become a duration-bearing block through drag-and-drop; Sunsama explicitly defines timeboxing as turning a list into a scheduled daily itinerary.  This reduces the fantasy that an unlimited task list can fit into finite time.

**Adaptive rescheduling.** Motion’s official scheduling documentation describes a scheduler that combines availability, duration, deadlines, priorities, start dates, recurrence, chunking rules, and changing calendar events, recalculating placements when the day changes.  Reclaim applies analogous flexibility to recurring habits and tasks, including preferred windows and durations.  This is a major improvement over brittle calendar plans.

But a common structural gap remains. This is an **inference from the interaction models above**, not a claim that the products lack every individual feature:

> Contemporary tools largely ask **“what are the tasks?”** and **“where do they fit in time?”**. A life-optimized interface should additionally ask **“what deserves consciousness now?”**, **“what state was I in when I left this?”**, and **“how confident am I that this plan survives reality?”**. 

Those are different computational objects.

A second gap concerns *planning uncertainty*. A 90-minute estimate is conventionally represented as though it were a fact. Yet users frequently do not know whether a task will take 30 minutes or three hours. Filling every free calendar region with deterministic blocks converts uncertainty into apparent precision. A life-organizer should instead distinguish **hard commitments, soft intentions, duration ranges, and reserve capacity**.

A third gap concerns *switching state*. A task title such as “Finish parser refactor” survives sync, but the mental state *“I discovered the bug is in token recovery; next inspect `parse_expr`; test 14 is the smallest reproduction”* often does not. Interruption and recovery research suggests that this lost state is precisely what an execution-oriented organizer should preserve. 

