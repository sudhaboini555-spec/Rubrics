# Rubrics
{

"task": {
"title": "Fix a failing edge case in the repository and add regression coverage",
"existing_repo": true,
"repo_path_or_url": "<REPO_URL>",
"base_commit": "<FULL_40_CHAR_SHA>",
"difficulty": "hard",
"from_scratch_verification": "Searches such as 'repository bug fix', 'repository regression test', 'repository issue fix', and 'repository edge case bug' do not provide an end-to-end solution for this task. They may provide background information or related issues, but they do not identify the exact root cause at the pinned commit, the required code modifications, or the regression tests needed to verify the fix. The agent must inspect the repository, reproduce the problem, implement a fix, and validate the behavior."
},
"user_persona": {
"high_level_goals": "I need a real fix merged into this codebase, not a workaround. I want the bug reproduced, the root cause identified, and regression tests added so it does not come back.",
"familiarity_with_tools": "Comfortable with Git, Bash, unit tests, and reading application code. Can follow technical explanations but prefers concise updates.",
"opinions_on_patterns": "Prefer minimal changes that address the root cause. Avoid broad refactors, unnecessary abstractions, or disabling tests.",
"communication_style": "Short messages. Direct answers. Usually responds in one or two sentences.",
"patience_style": "Will tolerate one or two incorrect attempts before asking for a different direction. Becomes frustrated by repeated speculation.",
"hint_policy": "Provides category-level hints only. Will not reveal exact files, functions, or code changes. At most one hint per milestone."
},
"milestones": [
{
"id": "m1",
"title": "Reproduce and localize the issue",
"prompt": "There is a bug in this repository. Please reproduce it, identify the likely root cause, and tell me which files you think are involved before making changes.",
"clarification_answers": [
{
"trigger": "Agent asks whether a failing test already exists",
"reaction": "No dedicated regression test exists yet. You should determine the failure from the current code and behavior."
},
{
"trigger": "Agent asks whether the bug is limited to one module",
"reaction": "Assume the issue originates in one primary area, but verify any downstream effects."
}
],
"corrections_and_hints": [
{
"trigger": "Agent immediately starts editing code without reproducing or localizing the issue",
"reaction": "Please reproduce and explain the root cause first. I do not want blind fixes."
},
{
"trigger": "Agent proposes disabling tests or removing validation",
"reaction": "That would hide the problem rather than fix it. Please find the underlying cause."
}
],
"continuation_criteria": "Agent provides a reproducible failure scenario and identifies at least one likely implementation area responsible for the behavior."
},
{
"id": "m2",
"title": "Implement the fix",
"prompt": "Go ahead and implement the fix. Keep the change as small as possible and explain why it addresses the root cause.",
"clarification_answers": [
{
"trigger": "Agent asks whether a refactor is acceptable",
"reaction": "Only if absolutely necessary. Prefer the smallest change that fixes the issue."
}
],
"corrections_and_hints": [
{
"trigger": "Agent introduces broad architectural changes",
"reaction": "Please narrow the scope. The goal is a targeted fix."
},
{
"trigger": "Agent changes unrelated functionality",
"reaction": "Avoid touching unrelated behavior unless it is required for correctness."
}
],
"continuation_criteria": "Agent explains the code change and connects it directly to the previously identified root cause."
},
{
"id": "m3",
"title": "Add regression coverage",
"prompt": "Add tests that would have failed before the fix and now pass with the fix.",
"clarification_answers": [
{
"trigger": "Agent asks how many tests to add",
"reaction": "Add enough coverage to demonstrate the bug and prevent regressions."
}
],
"corrections_and_hints": [
{
"trigger": "Agent only updates existing assertions without covering the bug scenario",
"reaction": "Please add coverage for the actual failing behavior."
}
],
"continuation_criteria": "Agent adds or updates tests that directly exercise the bug scenario and explains expected results."
},
{
"id": "m4",
"title": "Validation and summary",
"prompt": "Run the relevant checks and summarize exactly what changed.",
"clarification_answers": [
{
"trigger": "Agent asks whether full test suite execution is required",
"reaction": "Run the most relevant validation available and report the results."
}
],
"corrections_and_hints": [
{
"trigger": "Agent claims success without reporting validation output",
"reaction": "Please include the validation steps and outcomes."
}
],
"continuation_criteria": "Agent reports executed validation steps, results, modified files, and a concise explanation of the final fix."
}
]
}
