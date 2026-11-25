# One-page summary: HCI for a personal life-organization view

## The problem

A personal organizer needs to keep intentions available without making the person continually scan, prioritize, and remember them. The research reframes organization as **managing attention and preserving useful context**, alongside storing tasks and planning time. External cues can remind; interruptions can leave costly-to-reconstruct work states; and plans have to fit changing capacity.

## What the research supports

Personal-information-management studies describe organization as both finding and reminding, with elaborate categorization carrying its own costs ([Malone, 1983](https://doi.org/10.1145/357423.357430); [Barreau & Nardi, 1995](https://doi.org/10.1145/221296.221307)). Interruption research motivates preserving state when returning to complex work. One field study also found that more-visible suspended application windows were associated with faster returns, cautioning against hiding every inactive commitment ([Iqbal & Horvitz, 2007](https://www.microsoft.com/en-us/research/wp-content/uploads/2016/11/CHI_2007_Iqbal_Horvitz-1.pdf)). A ready-to-resume reflection plan reduced attention residue and protected performance on the interrupting task under anticipated time pressure; it does not prove that an app-generated packet speeds return to the original work ([Leroy & Glomb, 2018](https://pubsonline.informs.org/doi/10.1287/orsc.2017.1184)).

## The design proposed

The **Horizon Field** distinguishes when an intention exists, becomes actionable, deserves attention, fits best, and must be finished. It would offer a sparse Now/Today/Near/Later view, a focused next action, a small explainable shortlist, capacity estimates, flexible routines, and a **Park/Resume** checkpoint with the next step and relevant context. The underlying information could stay rich while the execution view stays simple. Local-first storage is proposed for privacy and continuity.

## The most distinctive hypotheses

- Design around **what deserves attention now**, rather than displaying the full task inventory.
- Treat work as suspendable and resumable; retain a useful checkpoint and context when it is parked.
- Let review release commitments the person no longer endorses; success need not mean completing every captured intention.
- Protect realistic capacity and user control; explain suggestions and let the person override them.

These are promising design directions, not proof that radial horizons, automatic ranking, or the full data model will work better for this person.

## The first practical test

Run a **one-week manual orientation trial** in an existing tool. After capture, label each item only enough to distinguish an actionable commitment, a waiting item, or an idea/reference; decide why and when it should return to attention; then select a few feasible next actions. Track time to choose and start, review/maintenance time, forgotten or unexpectedly resurfaced obligations, and progress on personally important outcomes. If choosing is already easy but returning to interrupted work is costly, test a brief manual Park/Resume note as a separate experiment.

## Evidence boundary

The cited literature supports relevant cognitive problems and some mechanisms. It does not validate the Horizon Field layout, its ranking formula, or the complete proposed application. The report’s one-person tests are design recommendations, not results. See the [full report index](README.md) and [primary-source checks](RESEARCH_CHECKS.md).
