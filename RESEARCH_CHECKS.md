# Primary-source checks for the personal organization view

Checked 2026-10-03 against the local research and `ORIGINAL_GOAL.md`. Scope: a personal view for one person's life, not a commercial product. These checks validate selected premises; they do not validate the proposed interface.

## 1. Difficult resumptions are a supported target; all switching is not

Czerwinski, Horvitz, and Wilhite (2004) studied a week of self-reported activity. Eleven experienced Windows users participated; one was excluded from subsequent analyses. Returned-to tasks were rated harder to switch to, involved more documents, and lasted longer. But average reported switching difficulty was low: 1.4 on a three-point scale. Participants also described multitasking as bringing variety and enjoyment. The implication is to target costly returns to complex work, not mechanically suppress every switch. This small workplace diary study cannot establish the main bottleneck in this user's whole life or show that a particular new UI fixes it. [Author-hosted paper, pp. 2–6](https://research.microsoft.com/en-us/um/people/horvitz/taskdiary.pdf).

## 2. Suspension support is motivated, but there is a visibility tradeoff

The association concerns **open application windows**, not taskbar icons: windows under 25% visible due to obscuration took longer to return to than windows over 75% visible (PDF page 6, “Influences of visible cues on return”; email p<.005, IM p<.02).

Iqbal and Horvitz (2007) observed 27 workplace users over two weeks using application/window and communication-alert instrumentation. They examined preparation, diversion, and resumption. Greater visibility of suspended windows was associated with faster returns; interviews also identified lost context. This motivates testing cues and checkpoints. It does not causally establish that saved textual packets outperform other cues. Logged application/window activity is also not a direct measure of productive mental work. A Focus view that hides every suspended activity could remove useful reminders; test a small parked-work cue rather than assuming maximum concealment helps. Do not treat long diversion/resumption intervals as an equivalent amount of cognitively wasted time. [Author-hosted paper, pp. 2–9](https://www.microsoft.com/en-us/research/wp-content/uploads/2016/11/CHI_2007_Iqbal_Horvitz-1.pdf).

## 3. A ready-to-resume plan has intervention evidence, with a narrower outcome

Leroy and Glomb (2018) report four studies supporting a brief reflection/plan before switching. When people anticipate time pressure on returning to unfinished work, the intervention reduces attention residue and protects performance on the **interrupting task**. That is a meaningful reason to test a small manual parking ritual. It is not direct proof that a Resumption Packet speeds return to the original task, that automatic snapshots substitute for reflection, or that five saved fields are necessary. Verification here covers the publisher's abstract and metadata; the full methods and effect sizes were not independently checked. [Publisher article](https://pubsonline.informs.org/doi/10.1287/orsc.2017.1184).

## 4. Attention timing separate from deadlines is useful, but established

Things' current official documentation explicitly separates start dates from completion deadlines and controls when future work comes into view. Upcoming hides future-start work until it becomes relevant; Someday holds tentative future possibilities. Therefore, separating when something appears from when it must finish is not by itself a new organizing concept. A genuinely distinct test would separate **review/attention timing from action availability**, or test whether a spatial horizon improves this user's decisions relative to an ordinary dated list. That remains a hypothesis. [Official scheduling documentation](https://culturedcode.com/things/support/articles/2803579/).

## What remains untested

The Horizon Field geometry, one Focus Capsule, multi-factor ranking, packet schema, and complete cross-device cognitive continuity are design proposals. None of the checked sources compares that bundle against this user's present workflow. A literature-supported problem does not make its proposed solution evidence-backed.

For this personal goal, start with a narrow comparison: a brief manual checkpoint versus usual switching during substantive work. Record checkpoint-writing time as well as return friction and distractions during the intervening task. Separately compare a small attention-filtered list against the current view; hold task content constant. Do not test the entire proposed system at once if the purpose is to learn which mechanism helps.

These recommendations are inferences for experiment design, not findings from the cited studies. The personal tests should preserve genuine obligations and should not define success as task count alone.
