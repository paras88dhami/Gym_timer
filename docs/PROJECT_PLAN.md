# Gym Timer — Product and Delivery Plan

**Status:** Product plan  
**Repository:** paras88dhami/Gym_timer  
**Date:** 6 October 2026

## 1. Product vision

Gym Timer helps a person plan and complete a resistance-training session within a chosen time budget. A user can build a workout from built-in or custom exercises, choose sets, reps, rest, and effort targets, then follow a live session timer that shows what to do next and whether the workout is on schedule.

The app supports goals such as muscle growth, strength, athletic power, general fitness, and a lean-body goal. These are programming emphases, not promises about appearance or results. A timer can help someone follow a plan consistently; it cannot guarantee muscle gain, fat loss, or a particular physique.

**Product promise:** “Know what comes next, how long the session is expected to take, and how your actual workout compares with your plan.”

## 2. Who it is for

- Gym members who have a fixed amount of time, such as 45 or 60 minutes.
- People who want to create and save their own exercises and workout templates.
- Beginners who need a clear set-by-set flow without a complicated coaching system.
- Experienced lifters who want to track loads, effort, rest, and session history.
- Athletes who want a timer and workout log for a coach- or user-authored plan.

The first release is for adults using general fitness guidance. It is not a medical device, rehabilitation tool, or substitute for a qualified coach or health professional.

## 3. Research findings and product implications

The 2026 American College of Sports Medicine (ACSM) position stand reviewed 137 systematic reviews with more than 30,000 participants. It reports that resistance training improves strength, muscle size, power, endurance, and several measures of physical function. Its highlighted training emphases differ by outcome: strength is associated with heavier loads, 2–3 sets, and at least two sessions weekly; hypertrophy with higher weekly volume (at least 10 sets per week); and power with moderate loads and a fast lifting phase. The stand also notes that several popular variables do not consistently change outcomes for healthy adults. These are population-level findings, not individualized prescriptions. [ACSM 2026 position stand](https://doi.org/10.1249/MSS.0000000000003897)

The World Health Organization recommends adults accumulate 150–300 minutes of moderate aerobic activity (or equivalent) per week and do muscle-strengthening activities involving major muscle groups on at least two days per week. A gym timer can support resistance sessions, but it should not imply that one 60-minute workout covers all activity recommendations. [WHO physical activity guidance](https://www.who.int/initiatives/behealthy/physical-activity)

### Design decisions from the research

1. Treat session length as a user’s time budget, not as proof that every goal can be achieved in exactly one hour.
2. Let users edit exercises, sets, reps, rest, and effort. Any starter template must be clearly labeled as general guidance.
3. Make goal modes change the emphasis and tracking labels, not promise body transformations.
4. Do not force every set to a fixed duration. Most resistance sets end when the lifter completes the target reps; the app should time rest and estimate the session end, with optional timed sets or tempo when useful.
5. Do not silently shorten rest periods or remove planned work to fit a deadline. Warn about likely overrun and let the user decide.
6. Keep progression suggestions conservative, optional, and based on the user’s logged history. Do not auto-increase weight or volume in the MVP.

## 4. Core user journey

1. **Choose a goal and time budget.** Select a focus such as muscle growth, strength, athletic power, general fitness, or lean-body support. Set a default session length, with 60 minutes as a suggested starting value.
2. **Build a workout.** Add exercises from the library or create custom ones. For each exercise, set equipment, target sets, reps or duration, rest, and optional load and effort target.
3. **Review the estimate.** See planned work time, rest time, transitions, warm-up allowance, total estimate, and the difference from the time budget. Edit the plan before starting.
4. **Run the workout.** See the active exercise, current set, reps or duration, rest countdown, next exercise, elapsed time, remaining estimate, and scheduled finish estimate. Mark a set complete, edit the result, skip it, pause, or end the session.
5. **Review and save.** Compare planned and actual duration, record completed sets, load, reps, and perceived effort, and view simple history and personal records.

## 5. MVP feature scope

### A. Workout and exercise builder

- Create, edit, duplicate, reorder, and delete workout templates.
- Add exercises from a small starter library and create custom exercises.
- Exercise fields: name, muscle group(s), equipment, movement category, notes, and optional instructions or image.
- Workout fields: name, goal focus, planned duration, warm-up allowance, and exercises.
- Set fields: target sets, rep range or timed duration, rest after each set, optional weight, optional RPE/RIR effort target, and notes.
- Support bodyweight, free-weight, machine, band, and timed/cardio-style entries.

### B. Session planner and estimator

Estimate total duration as:

**warm-up allowance + exercise work estimates + planned between-set rests + exercise transition allowances**

For a rep-based exercise, work time can be a user-configured estimate or an optional tempo-based estimate. Label estimates as estimates; do not present a predicted set duration as an exact finish time. Show confidence as low/medium if data is sparse, then improve estimates from the user’s own completed sessions.

- Show total planned duration, time budget, and over/under budget before starting.
- Allow the user to revise the workout or start anyway.
- During the workout, update the estimated finish time from elapsed time and remaining planned work.
- Offer configurable transition allowance and warm-up block.
- Keep the plan intact when it exceeds the time budget; make the overrun visible.

### C. Live workout timer

- Large, readable current exercise and set count.
- Start, pause, resume, finish, and abandon actions.
- Rest countdown with sound/vibration options and a clear next-set cue.
- Buttons to complete a set, edit actual reps/load/effort, skip a set, or skip an exercise.
- Elapsed session time, remaining planned time, and estimated finish clock time.
- Optional timed-set countdown and tempo cue; never assume all lifting sets are timed.
- Recover correctly after screen lock, app backgrounding, or process restart. Persist timer state and derive remaining time from timestamps, rather than relying only on a running screen animation.
- Accessible controls, clear contrast, large tap targets, and optional audio cues.

### D. Workout history

- Save completed sessions and their set-by-set results.
- Show session duration, completion, exercise history, and basic personal records.
- Display simple volume summaries only when the required load and repetition data exist.
- Allow editing a workout after completion without changing the original planned-vs-actual record.
- Export or back up data in a later phase.

### E. Goal modes

Goal modes should provide a useful starting organization while leaving user control intact.

| Goal focus | Product emphasis | Important boundary |
| --- | --- | --- |
| Muscle growth / bodybuilding | Track weekly sets by muscle group, exercise, load, and reps. Support reusable split templates. | The app does not promise muscle gain or prescribe nutrition. |
| Strength | Highlight load, reps, completed sets, and progress history. | Heavy lifting guidance should be optional and should not be treated as safe for every user. |
| Athletic / power | Support coach-authored explosive or sport-specific blocks, timed drills, and rest. | Do not auto-create technical Olympic lifts or advanced sport plans for beginners. |
| General fitness | Make balanced templates and consistent logging easy. | A resistance session timer is only one part of weekly physical activity. |
| Lean-body support | Support resistance-training consistency and session history. | Fat loss depends on factors outside the timer; do not promise fat loss or prescribe a restrictive diet. |

## 6. Time and timer rules

The user controls the time budget. The app helps plan and report; it should not pressure the user to rush.

- Rest timing begins when the user marks a set complete, unless the user chooses another start rule.
- Rest may be paused, skipped, or changed by the user.
- A completed set is logged separately from its rest interval.
- The session continues if the target end time passes. Show the overrun and let the user finish, skip, or end.
- Display both “planned finish” and “current estimate” so the user can tell them apart.
- If the plan cannot fit, explain which planned blocks account for the difference rather than silently changing them.

## 7. Safety, privacy, and trust

- Show a short first-use note: use loads and movements appropriate to your ability; stop if you feel pain, dizziness, or unusual symptoms; seek qualified medical advice when needed.
- Let users skip or modify any exercise. Avoid aggressive language such as “no excuses” or “push through pain.”
- Starter plans are educational examples for generally healthy adults, not personal medical or coaching advice.
- Use effort inputs such as RPE or reps in reserve as optional self-reports; explain that they are estimates and can be difficult for beginners to judge.
- Avoid collecting health information that is not needed. Keep workout data local on the device for MVP; explain backup and deletion behavior.
- Do not include ads or social sharing in the first release.

## 8. Proposed technical direction

**Recommendation:** Build a mobile-first, offline-first app in Flutter and Dart. This fits a personal gym use case, supports Android and iOS from one codebase, and allows the core workout timer to work without an account or network connection.

### Initial architecture

- **Presentation:** screens and reusable widgets for dashboard, workout builder, live session, history, and settings.
- **Application/domain:** workout, exercise, set, session, timer, estimate, and goal-focus models; business rules kept independent from UI.
- **Data:** local database/repository for templates, custom exercises, preferences, and session records.
- **Timer service:** session state machine with timestamp-based countdown and platform notifications/audio cues.
- **Testing:** unit tests for estimate and timer rules; widget tests for key flows; integration tests for completing a workout.

Select a local persistence package after checking Flutter compatibility and maintenance. Do not add a backend until sync, accounts, coach sharing, or cross-device backup is an approved product need.

### Core data entities

- **Exercise:** id, name, muscle groups, equipment, movement type, built-in/custom flag, notes.
- **WorkoutTemplate:** id, name, goal focus, target duration, warm-up allowance, ordered exercises.
- **ExercisePlan:** exercise id, order, set plan, rep or duration target, rest seconds, optional effort target.
- **WorkoutSession:** id, template snapshot, started/ended/paused timestamps, completion status.
- **SetLog:** session id, exercise id, set number, planned target, actual reps/duration, load, effort, completed/skipped status, timestamps.
- **UserSettings:** units, default session duration, cues, transition allowance, theme, and data-export options.

Keep a snapshot of the plan in each session so future template edits do not rewrite workout history.

## 9. Screen plan

1. **Home:** Start workout, resume active session, recent sessions, templates.
2. **Goal and duration setup:** Choose a goal focus and session time budget.
3. **Workout editor:** Reorder exercises, edit sets/reps/rest, view estimated total.
4. **Exercise library:** Search, filter, view details, add custom exercises.
5. **Pre-session review:** Time estimate, overrun warning, warm-up, start button.
6. **Active session:** Current set, rest timer, progress, finish estimate, controls.
7. **Session summary:** Planned vs actual, completed work, editable notes.
8. **History and settings:** Past sessions, units, cues, data export, privacy controls.

## 10. Delivery roadmap

### Phase 0 — Product decisions and foundation

- Confirm platform (recommended Flutter), app name, target audience, age scope, and offline-first behavior.
- Add architecture, design system, and baseline navigation.
- Define timer state transitions and duration-estimation rules.

### Phase 1 — MVP workout timer

- Create and save workout templates and custom exercises.
- Configure duration, exercises, sets, reps, and rest.
- Show planned session estimate and budget mismatch.
- Run a workout with rest countdown, pause/resume, complete/skip, and persistent state.
- Save session and set history locally.
- Add accessibility and basic safety messaging.

### Phase 2 — Goal-focused history and quality

- Add goal filters and weekly set summaries.
- Improve personal estimates using the user’s own session history.
- Add optional timed sets, tempo cues, sound/vibration settings, data export/import.
- Add tests for timer accuracy, app lifecycle recovery, data integrity, and accessibility.

### Phase 3 — Optional coaching and sync

Only proceed if users validate the need:
- Cloud backup and multi-device sync.
- Coach-created plans and workout sharing.
- Carefully reviewed template library.
- Wearable or calendar integrations.

## 11. MVP acceptance criteria

- A user can create a workout with a custom exercise and save it offline.
- A user can set a session budget such as 45 or 60 minutes and see an estimate before starting.
- An over-budget plan is clearly explained and never silently shortened.
- A user can complete multiple sets, take rest periods, pause, resume, skip, and finish.
- Timer state remains accurate when the app is backgrounded or reopened.
- Actual reps, load, and optional effort can differ from the target and are saved correctly.
- A completed session appears in history with planned and actual duration.
- Core flows work without network access or account registration.
- Timer and estimate logic have unit tests; key screen flows have integration coverage.

## 12. Open decisions before implementation

These can be resolved while setting up Phase 0:

1. Android only first, or Android and iOS together?
2. Flutter as recommended here, or another stack?
3. Should users sign in in the first release? Recommendation: no; keep it offline-first.
4. Should exercise illustrations be included at launch, or added after the timer works?
5. Should the first release include built-in example workouts, or only user-created templates?

## 13. Research sources

- Currier BS, et al. **American College of Sports Medicine Position Stand: Resistance Training Prescription for Muscle Function, Hypertrophy, and Physical Performance in Healthy Adults: An Overview of Reviews.** *Medicine & Science in Sports & Exercise.* 2026;58(4):851–872. [DOI](https://doi.org/10.1249/MSS.0000000000003897)
- American College of Sports Medicine. **ACSM Releases New Position Stand on Resistance Training.** 18 March 2026. [ACSM summary](https://acsm.org/science-spotlight-acsm-releases-new-position-stand-on-resistance-training/)
- World Health Organization. **Physical activity recommendations.** [WHO guidance](https://www.who.int/initiatives/behealthy/physical-activity)

Research checked: 6 October 2026.
