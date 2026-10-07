# Rubric: is this plan ready to post and build from?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here (via your procedure.md). It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the plan's scope statement, the test plan read against
     the repro evidence's steps, the plan comment read against the
     thread highlights, the repo-facts block) or a location from your
     references/evidence-guide.md. "The plan" is not a source; "the
     plan's stated cause read against what the repro evidence shows"
     is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (is
     this one bounded change? could a stranger start executing it?),
     never the write-up's shape (how many sections it has, how long it
     is, whether it uses headings). Structure-shaped checks are what
     make graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad plans posted. The lecture named the
failure families: the diagnosis ignores or contradicts the reproduced
evidence, the change is unbounded (scope creep), the plan targets the
symptom while the evidence points at the cause, a stranger could not
start executing it, the test plan proves nothing observable, the
unknowns are dressed up as certainty, and the comment ignores what the
thread or the repo's stated conventions ask. A rubric that ignores a
family will fail eval packages designed around that family.
-->

## Checks

| Check                    | Evidence                                                                                 | Pass condition                                                                                                                                                                                                                                                     | Weight   |
| ------------------------ | ---------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------- |
| diagnosis-grounded       | the plan's stated root cause read against the repro evidence's steps and observed output | passes if the diagnosis shows the bug described in the issue occurring here, accurately explains why the error stated in the issue occurs here, and agrees with what the repro evidence shows                                                                      | required |
| bounded-scope            | where the planning doc says files will be changed                                        | passes if the proposed changes are limited to what is necessary to fix the issue and do not extend to unrelated behavior. Out-of-scope naming is required when the issue context makes adjacency risky, such as something that affects multiple parts of the code. | required |
| test-decisive            | the plan states a test that shows the issue has been resolved                            | passes if the test plan creates and/or runs a unit test that verifies the issue has been fixed. The test should fail before the fix is implemented and pass after.                                                                                                 | required |
| executable-by-a-stranger | the section of the planning doc with implementation or change steps                      | passes if all the files needing to be added and/or changed are named along with the approach and changes that need to be made. It must be understandable without extra context from the issue thread.                                                              | required |
| uncertainty-honest       | speculative or vague language in the diagnosis or implementation steps                   | passes if there are no claims stated with certainty about behavior that is not supported by the repro evidence, or if unverified claims are flagged as assumptions or unknowns                                                                                     | required |
| comment-faithful         | the candidate comment read against the plan's stated changes and implementation steps    | passes if the comment only describes the changes stated in the plan and all described changes are relevant to the issue being addressed                                                                                                                            | required |
| comment-conventions      | the plan comment read against the thread highlights and the repo's stated conventions    | passes if the comment addresses what the issue thread asks for and follows the repo's contribution conventions (format, scope, framing)                                                                                                                            | required |

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->

Only accept if every required check passes. Preferred checks never change the verdict. Unclear counts as a fail.
