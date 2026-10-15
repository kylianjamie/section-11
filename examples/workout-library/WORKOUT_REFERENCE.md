# Section 11 — Running Workout Reference Library

This library defines the canonical running workout templates available to the AI coaching and planning system.

The AI coach MUST select, personalize, schedule, and adapt workouts using these templates. It MUST generate concrete, executable sessions with exact durations, pace targets, Garmin heart-rate zone targets, recovery periods, and progression rules.

All cycling templates have been removed.

---

## SECTION 11.1 — GLOBAL COACHING RULES

### A. Athlete Data and Personalization

Before prescribing a workout, retrieve the most recent available running data from Intervals.icu and the athlete's configured Garmin heart-rate zones.

Use the following data where available:

- Garmin running heart-rate zones Z1–Z5, including their actual BPM boundaries.
- Current running threshold pace.
- Current lactate threshold heart rate (LTHR), if available.
- Current maximum heart rate (HRmax), if available.
- Configured running pace zones in Intervals.icu, if available.
- Recent running activities, including duration, distance, pace, average/max HR, interval performance, and training load.
- Recent weekly running volume and longest recent run.
- Recent hard sessions, recovery status, and training-load trends.
- Current event goals and target race distance, if known.
- Recent lower-body strength training and other relevant training load.

Use the most recent credible data. Do not treat missing, stale, estimated, or conflicting values as confirmed measurements.

If a required threshold or zone definition is missing, explicitly identify the missing data and use the best-supported alternative available. Never invent an individual threshold, pace, or heart-rate boundary.

### B. Garmin Heart-Rate Zones Are Authoritative

The athlete uses Garmin's configured five-zone heart-rate system and follows these zones when executing workouts on the Garmin watch.

**Garmin's configured Z1–Z5 boundaries are the authoritative source for every heart-rate zone prescription.**

- Never recalculate, replace, normalize, or override Garmin's configured HR zones using a generic percentage-of-HRmax formula.
- Never assume that a particular physiological threshold corresponds to a specific Garmin zone.
- Retrieve the actual Garmin zone boundaries in BPM whenever available.
- If Garmin's zones are unavailable to the coach, use the athlete's recorded zone settings if explicitly provided. Otherwise, request the missing values rather than inventing boundaries.
- Intervals.icu's LTHR and threshold pace may be used as additional physiological and pace information, but they MUST NOT override Garmin's HR-zone boundaries.
- If Intervals.icu and Garmin display different HR zones, use Garmin for HR-zone targets and explicitly explain any relevant discrepancy.

Use these descriptions as general guidance only; the athlete's actual Garmin settings define the zone boundaries:

- **Z1:** Very easy / recovery.
- **Z2:** Easy aerobic running.
- **Z3:** Moderate / steady running.
- **Z4:** Hard running, often used for threshold-oriented work depending on the athlete's configured zones.
- **Z5:** Very hard running.

Do not automatically equate Garmin Z3 with lactate threshold. The relationship between physiological thresholds and Garmin's five zones depends on the athlete's settings and zone calculation method.

### C. Concrete Target Generation

Every prescribed workout MUST include explicit targets for every segment.

For each segment, specify:

- Duration or distance.
- Target pace in min/km, as a range where appropriate.
- Target Garmin HR zone, using the actual configured Garmin zones.
- BPM range when the actual zone boundaries are available and useful.
- RPE target on a 1–10 scale.
- Recovery duration and recovery intensity.
- Purpose of the segment.

Target selection rules:

1. **Easy running:** use a pace consistent with the athlete's current aerobic fitness and an easy effort. Garmin Z2 is the default HR target, provided it is consistent with the athlete's aerobic threshold and comfortable conversational effort.
2. **Threshold work:** derive pace from the athlete's current threshold pace, recent performances, and available pace zones. Prescribe the relevant Garmin HR zone as a secondary target based on the athlete's configured zones and observed response.
3. **VO2max intervals:** derive pace from recent interval performance, current threshold pace, and available pace zones. Use Garmin HR zones as secondary monitoring targets; do not require immediate HR-zone attainment during short repetitions.
4. **Strides:** prescribe duration and relaxed acceleration rather than an exact HR target.
5. **Race-specific sessions:** derive pace from a realistic current performance estimate and event goal, not solely from an aspirational goal time.

If a suitable configured pace zone is available, use its boundaries. Otherwise, derive a conservative pace range from individual threshold pace and recent performances.

When converting between speed and pace, calculate correctly: a percentage change in running speed is not the same percentage change in min/km.

For every session, display concrete targets in a Garmin-friendly format, for example:

`8 min — 5:15–5:25/km — Garmin Z3–Z4 (actual BPM boundaries) — RPE 7/10`

The values above are illustrative only, not prescribed targets for a specific athlete.

Do not display contradictory targets. If pace and HR disagree, explain which metric takes priority for that segment and why.

### D. Heart Rate During Running

- For easy running, Garmin HR zones and conversational effort are primary intensity controls.
- For threshold and longer intervals, use pace and effort alongside Garmin HR zones.
- HR responds with a delay during short intervals. Do not require the athlete to reach Z4 or Z5 immediately after starting a 30-second or 1-minute repetition.
- For VO2max work, use pace and RPE as the primary controls during short repetitions; Garmin HR is a secondary check.
- Allow for heat, hills, wind, fatigue, dehydration, and sensor error.
- Do not prescribe walking solely because of a brief HR excursion into a higher zone.
- If HR remains unusually high at an easy pace, reduce intensity and assess recovery rather than forcing the planned pace.
- Do not ask the athlete to change Garmin's configured zones merely to make a workout template fit.

### E. Weekly Structure: Three Running Sessions

For a typical recreational runner training three times per week:

1. One easy aerobic run, optionally including strides.
2. One quality session selected from the threshold, VO2max, hill, or race-specific templates.
3. One longer easy aerobic run.

The AI coach MUST NOT prescribe every quality template within the same week by default.

Select ONE primary hard running session per week initially. A second demanding session may be considered only when training history, current volume, recovery, goals, and concurrent gym training support it.

For runners with limited training history or inconsistent running volume, prioritize consistency and gradual progression over adding more intensity.

### F. Concurrent Strength Training

Account for the athlete's gym sessions, particularly demanding lower-body training.

- Avoid scheduling demanding running intervals immediately after a fatiguing lower-body session.
- Prefer approximately 24–48 hours between demanding lower-body strength training and a hard running workout when practical.
- Treat this interval as a planning guideline, not a universal physiological rule.
- Easy running may be appropriate sooner if the athlete is recovered and symptom-free.
- Consider total lower-body load from squats, lunges, plyometrics, hills, and running intervals.
- When scheduling conflicts arise, reduce workout volume, substitute an easy session, or reschedule rather than automatically stacking hard sessions.

### G. Recovery and Load Management

Use training-load indicators such as TSB and ACWR as contextual signals, not as standalone eligibility rules.

- Do not automatically prohibit a workout solely because TSB is below -15.
- Do not automatically prohibit a workout solely because ACWR exceeds 1.3.
- Consider recent load changes, fatigue, soreness, sleep, perceived recovery, performance trends, pain, and the combined running/gym schedule.
- When several indicators suggest poor recovery, substitute easy running or rest.
- Never use an apparently acceptable TSB or ACWR to override meaningful pain or other warning signs.
- If the athlete reports pain that changes running mechanics, recommend stopping the session and assessing the issue rather than prescribing harder training.

### H. Progression and Adaptation

- Change only one major loading variable at a time where practical: total duration, interval count, interval duration, pace, or intensity.
- Progress based on successful completion, stable mechanics, and adequate recovery.
- Do not apply a mandatory percentage-based weekly mileage increase.
- Use a lighter week when fatigue, soreness, or accumulated load warrants it.
- Reassess threshold pace and training paces when credible new performance data becomes available.
- Never increase both the quality-session workload and the long-run duration aggressively in the same week.
- Do not automatically progress every week; repeat a workout when it remains productive and recovery is incomplete.

---

## SECTION 11.2 — WORKOUT TEMPLATES

### 1. RUN_Z2_EASY

domain: run  
is_hard_session: false  
quality_work_minutes: 0  
est_total_minutes: 45  
duration_range_minutes: 30–50

#### Objective

Develop aerobic endurance with low fatigue cost. Support recovery and maintain consistent weekly running volume.

#### Structure

- 5–10 min easy warm-up, included in the total duration.
- Continue at easy aerobic intensity until the planned total duration is reached.
- No mandatory strides or fast finish.

#### Intensity

- Pace: individualized easy-running pace based on current fitness and recent performance.
- Garmin HR target: primarily Z2, using the actual configured Garmin BPM boundaries, provided this is consistent with comfortable aerobic effort.
- RPE: 2–4/10.
- Conversational pace throughout.

#### Coaching Rules

- Select duration according to recent training history.
- Use Garmin HR and conversational effort alongside pace.
- Slow down if effort or HR remains above the intended aerobic intensity.
- Brief walk breaks are allowed when necessary.
- Do not require walking for every brief HR excursion into a higher zone.
- `is_hard_session: false`.

---

### 2. RUN_Z2_LONG

domain: run  
is_hard_session: false  
quality_work_minutes: 0  
est_total_minutes: 75  
duration_range_minutes: 45–120

#### Objective

Build aerobic endurance, fatigue resistance, and the ability to sustain longer distances.

#### Structure

- 5–10 min easy settling-in period.
- Continue easy running until the planned total duration is reached.
- Optional brief walk breaks if necessary.
- No mandatory fast finish.

#### Intensity

- Pace: individualized easy pace.
- Garmin HR target: predominantly Z2, using the athlete's actual configured Garmin zones.
- RPE: 3–4/10.
- Full-sentence conversation should remain possible.

#### Coaching Rules

- The default 75 minutes is a reference, not a mandatory duration.
- Select duration based on recent longest run, weekly volume, and recovery.
- Increase duration gradually; do not prescribe 90 minutes to an athlete whose current training cannot support it.
- Avoid placing this session immediately before a hard running workout or demanding lower-body gym session.
- Fuel longer sessions appropriately when duration and individual needs warrant it.
- `is_hard_session: false`.

---

### 3. RUN_TEMPO_CRUISE

domain: run  
is_hard_session: true  
quality_work_minutes: 24  
est_total_minutes: 48  
duration_range_minutes: 40–60

#### Objective

Improve threshold speed and the ability to sustain a demanding pace for 5K–10K performance.

#### Structure

- 10 min easy warm-up, Garmin Z1–Z2 as appropriate.
- 3 × 8 min controlled threshold-oriented running.
- 2 min easy jog between repetitions.
- 10 min easy cool-down, Garmin Z1–Z2 as appropriate.

#### Intensity

- Work intervals: individualized threshold training pace.
- Pace: derive from current threshold pace and configured running pace zones.
- Garmin HR target: individualized according to the actual Garmin zones and observed HR response. The coach must not assume threshold equals Garmin Z3 or Z4.
- RPE: approximately 7–8/10.
- Recovery: easy jog, normally Garmin Z1–Z2.

#### Coaching Rules

- Start with 2 × 8 min or 3 × 6 min when the full session is too demanding.
- The final repetition should remain controlled and repeatable.
- Use individualized threshold pace as the primary pace reference, with Garmin HR as a secondary control.
- If HR rises unusually early or substantially above the intended zone, reduce effort and reassess conditions.
- `is_hard_session: true`.

---

### 4. RUN_TEMPO_SUSTAINED

domain: run  
is_hard_session: true  
quality_work_minutes: 20  
est_total_minutes: 42  
duration_range_minutes: 35–55

#### Objective

Improve sustained threshold-oriented running, pace control, and tolerance of continuous demanding effort.

#### Structure

- 12 min easy warm-up, Garmin Z1–Z2 as appropriate.
- 20 min continuous threshold-oriented tempo.
- 10 min easy cool-down, Garmin Z1–Z2 as appropriate.

#### Intensity

- Work segment: individualized threshold training pace, adjusted to the athlete's current ability.
- Garmin HR target: use actual Garmin zone boundaries and the athlete's known HR response to threshold effort.
- RPE: approximately 7/10, rising to 8/10 only if appropriate.
- Finish feeling that the effort was hard but controlled.

#### Coaching Rules

- Use as an alternative to RUN_TEMPO_CRUISE, not as an additional mandatory weekly workout.
- Prefer cruise intervals for athletes who struggle to maintain consistent pacing.
- Prefer continuous tempo when the athlete can already sustain controlled threshold work.
- Reduce duration if the athlete cannot maintain the prescribed effort without substantial deterioration.
- `is_hard_session: true`.

---

### 5. RUN_VO2_SHORT

domain: run  
is_hard_session: true  
quality_work_minutes: 10  
est_total_minutes: 45  
duration_range_minutes: 35–50

#### Objective

Improve aerobic power and the ability to repeat high-intensity efforts.

#### Structure

- 12 min easy warm-up, Garmin Z1–Z2.
- Optional 2–3 min of dynamic running drills.
- 2 sets of 10 ×:
  - 30 sec hard running.
  - 30 sec easy jog.
- 3 min easy recovery between sets.
- 10 min easy cool-down, Garmin Z1–Z2.

#### Intensity

- Hard repetitions: individualized high-intensity pace, normally corresponding to high-intensity pace zones appropriate to the athlete's fitness.
- Garmin HR: may rise toward Z4–Z5 over repeated efforts, depending on the athlete's actual Garmin settings; do not require immediate HR-zone attainment.
- RPE: 8–9/10 during the hardest repetitions.
- Recovery: easy jog, normally Garmin Z1–Z2.

#### Coaching Rules

- The default contains 10 minutes of hard work, not 15.
- Start with 1 set or 2 × 6–8 repetitions for less experienced runners.
- The athlete should run fast but not sprint maximally.
- Stop increasing intensity if mechanics deteriorate or pace becomes inconsistent.
- Use this session instead of another hard running session, not in addition to it by default.
- `is_hard_session: true`.

---

### 6. RUN_VO2_CLASSIC

domain: run  
is_hard_session: true  
quality_work_minutes: athlete_dependent  
est_total_minutes: athlete_dependent  
duration_range_minutes: 35–60

#### Objective

Improve aerobic power, high-intensity running capacity, and performance at shorter race distances.

#### Structure

Default session for athletes with sufficient training history:

- 12–15 min easy warm-up, Garmin Z1–Z2.
- 4 × 3 min hard running.
- 2–3 min easy jog between repetitions.
- 10 min easy cool-down, Garmin Z1–Z2.

Advanced alternative:

- 4 × 1,000 m at an individually appropriate high-aerobic-intensity pace.
- 2.5–3 min easy jog or walk recovery.
- Use only when the athlete's current performance and training history support the workload.

#### Intensity

- Work intervals: controlled high aerobic intensity based on individual pace and recent interval performance.
- Garmin HR: may approach Z4–Z5 late in repetitions, depending on actual Garmin zones; HR is secondary during the early part of each repetition.
- RPE: approximately 8–9/10.
- Recovery: easy jog or walk, normally Garmin Z1–Z2 effort.

#### Coaching Rules

- Select interval duration or distance according to training level.
- Do not automatically prescribe 4 × 1,000 m to a less experienced runner.
- Pace should be repeatable across all repetitions; avoid an excessively fast first repetition.
- Progress repetitions or duration only after successful completion and adequate recovery.
- `is_hard_session: true`.

---

### 7. RUN_Z2_STRIDES

domain: run  
is_hard_session: false  
quality_work_minutes: 0  
est_total_minutes: 48  
duration_range_minutes: 35–55

#### Objective

Maintain aerobic conditioning while improving relaxed acceleration, coordination, and running economy.

#### Structure

- 35 min easy aerobic running.
- 5 × 20 sec relaxed strides.
- 60–100 sec walking or very easy jogging recovery after each stride.
- 5 min easy cool-down.

#### Intensity

- Easy running: individualized easy pace; Garmin Z2 as the default HR target when appropriate.
- Strides: progressive acceleration to fast, relaxed running; no maximal sprinting.
- Garmin HR: no target for individual strides.
- RPE: 2–4/10 for the easy run; strides should feel fast but technically relaxed.

#### Coaching Rules

- Adjust easy-running duration so the total session fits the planned duration.
- Full recovery between strides is mandatory.
- Do not prescribe strides if pain, acute fatigue, or poor running mechanics make acceleration inappropriate.
- Count this as an easy session, provided the strides remain short and relaxed.
- `is_hard_session: false`.

---

### 8. RUN_EASY_PROGRESSIVE

domain: run  
is_hard_session: false  
quality_work_minutes: 0  
est_total_minutes: 40  
duration_range_minutes: 25–50

#### Objective

Progressively develop easy-running volume for athletes who are not yet ready for longer continuous sessions.

#### Structure

- 5–10 min very easy running or run/walk.
- 20–35 min easy aerobic running, adjusted to current ability.
- Optional short walking breaks.
- No fast finish or mandatory strides.

#### Intensity

- Pace: individualized easy pace.
- Garmin HR: predominantly Z1–Z2, with Z2 as the default target when appropriate.
- RPE: 2–4/10.

#### Coaching Rules

- Select this template when the athlete needs gradual volume development.
- Increase duration only after the current session is comfortably tolerated.
- Prefer a modest duration increase over simultaneously adding intervals.
- When the athlete is ready for longer easy sessions, transition toward RUN_Z2_EASY or RUN_Z2_LONG.
- `is_hard_session: false`.

---

### 9. RUN_HILL_REPEATS

domain: run  
is_hard_session: true  
quality_work_minutes: 4–8  
est_total_minutes: 40–50  
duration_range_minutes: 35–55

#### Objective

Develop uphill running strength, coordination, and the ability to produce high running effort without relying exclusively on flat-road speed.

#### Structure

- 12–15 min easy warm-up, Garmin Z1–Z2.
- 6 × 30–45 sec uphill at controlled hard effort.
- Walk or jog downhill for full recovery, typically 90–150 sec.
- 10 min easy cool-down.

#### Intensity

- Uphill repetitions: RPE 7–8/10, strong but controlled.
- Garmin HR: may rise into Z4; do not use HR as the primary target for short uphill repetitions.
- Recovery: easy effort, normally Garmin Z1–Z2.
- Pace: effort-based rather than a fixed min/km target because gradient changes pace substantially.

#### Coaching Rules

- Introduce only after a consistent easy-running base has been established.
- Use a moderate, even gradient and stable footing.
- Do not combine with another hard running workout in the same week by default.
- Account for additional calf, Achilles, and lower-leg loading.
- Replace rather than add to an existing quality session.
- `is_hard_session: true`.

---

### 10. RUN_RACE_SPECIFIC

domain: run  
is_hard_session: true  
quality_work_minutes: athlete_dependent  
est_total_minutes: athlete_dependent  
duration_range_minutes: 35–65

#### Objective

Improve the ability to sustain the pace and effort required for a specific target event.

#### Structure

Select one workout appropriate to the athlete's event, current fitness, and training phase.

Example A — 5K:

- 12–15 min easy warm-up.
- 4–6 × 3 min at current 5K-specific effort.
- 2 min easy jog recovery.
- 10 min easy cool-down.

Example B — 10K:

- 12–15 min easy warm-up.
- 3 × 8 min at controlled current 10K-specific effort.
- 2 min easy jog recovery.
- 10 min easy cool-down.

Example C — Half marathon:

- 12–15 min easy warm-up.
- 2 × 15 min at individually appropriate half-marathon effort.
- 3 min easy jog recovery.
- 10 min easy cool-down.

These are starting templates, not mandatory workloads. Select only the version that fits the athlete's current ability.

#### Intensity

- Use a realistic current performance estimate and individualized race-pace targets.
- Prescribe concrete pace ranges in min/km.
- Use Garmin HR zones as monitoring targets based on the actual configured zones and the intended race effort.
- RPE depends on event distance and interval duration; effort must remain controlled enough to complete all repetitions.

#### Coaching Rules

- Do not derive race pace solely from an aspirational goal time.
- Use recent race results, credible time trials, threshold pace, and recent workouts.
- Distinguish current achievable pace from target race pace.
- Introduce event-specific work as the event approaches.
- Do not prescribe this as an additional hard session on top of the weekly quality session.
- `is_hard_session: true`.

---

## SECTION 11.3 — WORKOUT METADATA AND DURATION RULES

The coach and planner MUST distinguish total session duration from quality-work duration.

Use these fields consistently:

- `quality_work_minutes`: minutes spent at the intended quality intensity; zero for purely easy workouts.
- `easy_running_minutes`: planned easy-running minutes, where known.
- `recovery_minutes`: total planned recovery time between repetitions, where known.
- `est_total_minutes`: estimated complete session duration, including warm-up, work intervals, recoveries, drills, and cool-down.
- `duration_range_minutes`: acceptable total session duration range.
- `is_hard_session`: whether the workout contains a meaningful demanding running stimulus.

Rules:

1. Do not label total session duration as quality-work duration.
2. Compute total duration from the actual structure.
3. When distance-based intervals are prescribed, calculate estimated work duration using the athlete's individualized pace.
4. When exact duration depends on pace or recovery, calculate it dynamically and report the estimate.
5. Do not count recovery intervals as hard work.
6. Strides remain an easy-session accessory when brief, relaxed, and fully recovered.
7. A workout is not automatically easy merely because its quality-work duration is short.

---

## SECTION 11.4 — WEEKLY SELECTION AND PROGRESSION ALGORITHM

### Default Weekly Selection

For an athlete training three times per week:

- Session A: RUN_Z2_EASY, RUN_Z2_STRIDES, or RUN_EASY_PROGRESSIVE.
- Session B: exactly one primary quality workout selected from RUN_TEMPO_CRUISE, RUN_TEMPO_SUSTAINED, RUN_VO2_SHORT, RUN_VO2_CLASSIC, RUN_HILL_REPEATS, or RUN_RACE_SPECIFIC.
- Session C: RUN_Z2_LONG, with duration based on current training capacity.

This is the default structure, not a rigid rule. The coach may prescribe two easy runs and no quality session during recovery weeks, after illness, during return from injury, or when overall fatigue is high.

### Quality Session Selection

Prioritize threshold work when:
- The primary goal is improving sustainable 5K–10K pace.
- The athlete tolerates sustained controlled efforts well.
- Current training suggests threshold development is appropriate.

Prioritize VO2max intervals when:
- The athlete has an adequate aerobic base.
- A high-intensity aerobic stimulus is appropriate.
- Recovery and concurrent strength training permit the additional intensity.

Prioritize race-specific work when:
- An event goal and date are known.
- The athlete is sufficiently prepared for event-specific training.
- The planned workout supports the event rather than unnecessarily duplicating another quality stimulus.

Prioritize easy running when:
- Recent training load has increased sharply.
- Recovery is poor.
- The athlete has persistent soreness or pain.
- Recent workouts show declining pace, rising effort, or inability to complete prescribed work.

### Progression

The coach MUST use recent completed workouts to decide whether to progress.

- If a session is completed comfortably with consistent pace and good recovery, consider a small increase in work duration or repetition count.
- If the session is completed but feels unusually difficult, repeat or reduce the workload.
- If repetitions deteriorate significantly, do not progress intensity or volume.
- If the athlete misses sessions, do not automatically compensate by stacking workouts.
- During recovery weeks, reduce total duration or quality-work volume as appropriate.
- Reassess training paces when new reliable performance data becomes available.

---

## SECTION 11.5 — REQUIRED AI COACH OUTPUT

Every prescribed workout MUST be returned as a complete, executable training plan.

For each session, include:

1. Workout ID and objective.
2. Total estimated duration.
3. Every segment in execution order.
4. Exact duration or distance for each segment.
5. Individualized target pace in min/km, where appropriate.
6. Garmin HR zone and actual BPM range, where available.
7. RPE target.
8. Recovery duration and recovery intensity.
9. Warm-up and cool-down instructions.
10. Brief guidance for adjusting the session if HR, pace, or perceived effort deviates substantially from the plan.

The coach MUST use the athlete's actual Intervals.icu and Garmin values when available and MUST NOT present illustrative example values as personal prescriptions.

If the athlete asks for a weekly plan, include the three running sessions, their order, spacing from lower-body gym sessions, and the rationale for the selected quality workout.

The final plan must be specific enough that the athlete can execute it on a Garmin watch without independently deciding what pace, HR zone, interval duration, or recovery period to use.

### Garmin Workout Compatibility

When preparing workouts for Garmin execution:

- Prefer structured steps that Garmin supports: warm-up, run intervals, recovery intervals, repetitions, and cool-down.
- Specify HR-zone targets using the athlete's actual Garmin zone definitions.
- Specify pace targets as explicit ranges when appropriate.
- Do not prescribe simultaneous pace and HR targets that are impossible or contradictory under expected conditions.
- For short intervals, prioritize pace or effort rather than an immediate HR target.
- If the coach cannot access the exact Garmin BPM boundaries, label the HR target by Garmin zone only and do not invent BPM values.
- Preserve Garmin's configured HR zones; do not instruct the athlete to change them to match a generated workout.
