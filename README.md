# Task: Build a web-based behavioral experiment program

Please build a browser-based experimental program for two human-AI interaction studies. Use jsPsych or another lightweight JavaScript-based framework. The program must run locally in a browser and export trial-level data as CSV or JSON.

The project includes two experiments. Please prioritize Experiment 2 first.

## General requirements

1. The experiment should run in a browser.
2. Each participant should receive a randomly generated participant_id.
3. The program should support between-subject random assignment to conditions.
4. Trial-level data must be recorded.
5. Data should be downloadable as CSV at the end of the experiment.
6. The code should be modular, readable, and documented.
7. Do not hard-code all materials inside one file. Use external CSV or JSON files for trial materials when possible.
8. Include a simple README explaining how to run the experiment locally.

---

# Experiment 2: Social choice information and insufficient judgment updating after feedback

## Theoretical model

Independent variable:
- social_choice_source_type
- 0 = authoritative human group
- 1 = professional AI Agent group

Moderator:
- social_choice_consensus
- 0 = low consensus, e.g., 58% vs. 42%
- 1 = high consensus, e.g., 82% vs. 18%

Mediators measured by scales after the task:
- perceived cognitive authority
- consensus cue reliance
- responsibility displacement perception

Dependent variable:
- insufficient judgment updating after feedback

This dependent variable is measured behaviorally rather than by self-report.

## Trial structure

Each trial should follow this sequence:

1. Present a business forecasting case.
2. Ask participant for initial binary choice:
   - growth
   - decline
3. Ask participant for initial probability judgment P0:
   - “What is the probability that the company will grow next quarter?”
   - 0–100 slider
   - The slider should not have a visible default value.
4. Present social choice information according to assigned condition:
   - Source type: authoritative human group or professional AI Agent group.
   - Consensus level: low consensus or high consensus.
   - Example high consensus: 82% choose growth, 18% choose decline.
   - Example low consensus: 58% choose growth, 42% choose decline.
5. Ask participant for probability judgment after social choice information, P1.
6. Present a low-salience market information update section:
   - Do not explicitly say “the environment has changed.”
   - Use neutral wording: “The system has updated several market information modules. You may view them before making your final judgment.”
7. Show several clickable information modules:
   - sales performance
   - cost change
   - industry trend
   - competitive dynamics
   - market sentiment
8. Each module should be collapsed initially.
9. Record:
   - which modules were clicked
   - click order
   - viewing time for each module
   - whether diagnostic modules were clicked
10. Ask participant for final binary choice:
   - growth
   - decline
11. Ask participant for final probability judgment P2.
12. Proceed to the next trial.

## Diagnostic feedback and P_star

Each trial material should include a hidden normative probability P_star. This should not be shown to participants.

P_star is the normative probability after fully integrating diagnostic feedback.

For conflict trials:
- social choice information supports one direction
- diagnostic feedback supports the opposite direction
- these trials are used to compute the main dependent variable

## Main dependent variable

For each valid conflict trial:

actual_adjustment = (P2 - P1) * sign(P_star - P1)

optimal_adjustment = abs(P_star - P1)

feedback_updating_weight = actual_adjustment / optimal_adjustment

insufficient_judgment_updating = 1 - feedback_updating_weight

Rules:
- If optimal_adjustment is smaller than 10 percentage points, flag the trial as invalid for the main analysis.
- If actual_adjustment is negative, flag it as reverse adjustment.
- Keep both raw and cleaned values in the exported data.
- Also compute final_error = abs(P2 - P_star).

## Data to record for Experiment 2

At the participant level:
- participant_id
- condition_source_type
- condition_consensus
- age
- gender
- AI familiarity
- trust in AI
- business forecasting experience
- cognitive reflection or need for cognition if included

At the trial level:
- participant_id
- trial_id
- case_id
- source_type
- consensus_level
- social_choice_direction
- social_choice_ratio_majority
- social_choice_ratio_minority
- initial_choice
- P0
- P1
- P2
- P_star
- final_choice
- conflict_trial
- actual_adjustment
- optimal_adjustment
- feedback_updating_weight
- insufficient_judgment_updating
- final_error
- clicked_modules
- click_order
- viewing_time_by_module
- diagnostic_module_clicked
- total_viewing_time
- response_time_P0
- response_time_P1
- response_time_P2

## Scale items after Experiment 2

Use 7-point Likert scales.

Perceived cognitive authority:
- The group has professional ability to make this business forecast.
- The group’s judgment is likely to be accurate.
- The group is qualified to evaluate this forecasting task.
- The group’s choice is an important basis for my judgment.

Consensus cue reliance:
- When most members choose one option, I tend to regard that option as more likely to be correct.
- A highly concentrated choice ratio makes me more willing to trust the majority choice.
- The majority choice provides a useful shortcut for making this judgment.
- The more consistent the group choice is, the more persuasive I find it.

Responsibility displacement perception:
- After seeing the group choice, I felt the decision outcome was not entirely my personal responsibility.
- If I followed the group choice and the judgment turned out to be wrong, I would not feel it was entirely my own fault.
- Following the group choice made my judgment feel more justifiable.
- The group choice reduced my sense of personal responsibility for the outcome.

Manipulation checks:
- The choice information came from: human group / AI Agent group.
- The group’s choices were highly consistent.
- I noticed the approximate choice ratio.
- The later market information conflicted with the previous group choice.
- The task was uncertain and difficult.

---

# Experiment 1: Social comparison and defensive decision inertia

Please implement Experiment 1 after Experiment 2.

## Theoretical model

Independent variable:
- comparison_target_type
- 0 = human individual
- 1 = AI Agent individual

Moderator:
- social_comparison_direction
- 0 = upward comparison
- 1 = downward comparison

Upstream mediator:
- ability-evaluative threat

Second-stage mediators:
- state cognitive closure reaction
- strategy switching resistance
- defensive information selection bias

Dependent variable:
- defensive decision inertia

## Trial structure

Experiment 1 is a two-option investment decision task.

1. Present task instructions.
2. Participants make repeated A/B investment decisions.
3. The program should create a baseline preference for one option.
4. Participants then see social comparison information:
   - human individual or AI Agent individual
   - upward or downward comparison
   - comparison gap shown as a percentage
5. The comparison gap should vary slightly across rounds rather than remain fixed.
6. After comparison information, measure ability-evaluative threat and second-stage mediators.
7. Present a subtle market update suggesting that the original option may no longer be optimal.
8. Participants continue making key-round A/B investment decisions.
9. Defensive decision inertia is calculated as the proportion of key rounds in which the participant stays with the original preferred option.

## Data to record for Experiment 1

- participant_id
- condition_target_type
- condition_comparison_direction
- trial_id
- phase
- chosen_option
- original_preferred_option
- stayed_with_original
- own_return
- target_return
- comparison_gap
- response_time
- confidence
- clicked_information_type
- information_viewing_time
- ability_evaluative_threat_score
- state_cognitive_closure_reaction_score
- strategy_switching_resistance_score
- defensive_information_selection_bias_score
- defensive_decision_inertia

## Scale items for Experiment 1

Use 7-point Likert scales and phrase all items as state/task-specific.

Ability-evaluative threat:
- After seeing the comparison result, I felt that my investment judgment ability was challenged.
- The comparison result made me feel that my performance position was threatened.
- Compared with the target, I felt disadvantaged in ability evaluation.
- The comparison result made me question the value of my original decision approach.

State cognitive closure reaction:
- After seeing the comparison result, I wanted to settle on a decision quickly.
- In the current task, I did not want to keep comparing different options.
- I wanted to reduce uncertainty and reach a clear judgment as soon as possible.
- I preferred to stop repeatedly reconsidering my decision.

Strategy switching resistance:
- In the current task, changing my original investment strategy felt difficult.
- Even after new information appeared, I did not want to easily abandon my original strategy.
- Switching away from my original strategy involved psychological cost.
- Changing my strategy would feel like admitting that my earlier judgment was wrong.

Defensive information selection bias:
- I preferred to view information that supported my original investment choice.
- I was less willing to view information that contradicted my original investment choice.
- I tended to look for information that justified my previous choice.
- I paid more attention to information favorable to my original strategy.

Manipulation checks:
- I recognized the comparison target as human / AI Agent.
- The target performed better / worse than me.
- The comparison gap was noticeable.
- The comparison gap felt attainable.
- I noticed that the investment environment had changed.

---

# Deliverables

Please produce:
1. A working local experiment program.
2. A clear folder structure.
3. Trial materials in editable CSV or JSON files.
4. Data export function.
5. README instructions for running locally.
6. Comments in code explaining key sections.
7. A small demo dataset generated from test runs.
8. If possible, include a simple Python or R script to compute the main dependent variables from exported data.
