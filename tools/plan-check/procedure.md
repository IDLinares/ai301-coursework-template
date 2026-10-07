# Procedure: how this skill grades a plan package

<!--
THIS IS THE PART YOU WRITE, and it is a new kind of part. Weeks 1 and
2, SKILL.md carried a numbered workflow and you only wrote judgment
files. This week the workflow is gone from the frame: SKILL.md says
"execute procedure.md", and these are the operating steps you author.
The machinery is in your hands now.

Your operator swap is the design brief. When your executor stalled
because your rubric said WHAT to decide but not HOW to find the
evidence, that was a procedure gap. This file is where those gaps get
closed: a complete procedure lets someone who has never seen a plan
package before (a groupmate, or the skill itself) grade one exactly the
way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
repro evidence before the plan, and note what behavior it pins down"
is a step; "understand the context" is a wish.
-->

## Read order

<!-- What gets read, in what order, before any check is graded, and
what to note down from each part while reading. A complete procedure
decides the order (issue first? repro evidence first?) and says why
the order matters for the checks that come later. -->

1. In live mode, read `scope.md` and `voice-guide.md` and confirm the issue is inside the scoped source (the provided repo). Note any house rules. For both modes, read `rubric.md` and `reference/evidence-guide.md`. Record the following information while reading:
   - For each rubric check, write the check name and source for the evidence that the evidence guide states, along with the pass condition in one line. This allows for consulting check-by-check while grading without re-reading the rubric.
   - For the voice guide in live mode, write down each rule and the list of things to never post to compare with later against the plan and comment.
2. The complete issue context should be read next. This includes the repro evidence, the issue thread, and the repo's conventions. It is important to provide correct background for each of the rubric checks, especially for `diagnosis-grounded`, `bounded-scope`, `comment-conventions`, and `uncertainty-honest` where knowing the issue context and conventions is critial to grading the check accurately. Record the following information while reading:
   - From the repro evidence, note the exact observed behavior (error message, output, stack trace) and the exact steps to reproduce it.
   - From the issue thread, note what the maintainers/reporters are explicitly asking for in the comment.
   - From the repo's conventions, note any format or scope requirements.
3. Finally, read the candidate plan and plan comment. Record the following information while reading:
   - From the candidate plan, note the root cause and its location for `diagnosis-grounded`, the list of files mentioned for `bounded-scope`, the tests mentioned for `test-decisive`, and the implementation steps for `executable-by-a-stranger` and `comment-faithful`. Also note any speculative or vague language in the diagnosis or implementation steps for `uncertainty-honest`. If none found, also note that there are no speculative claims. Do not skip if nothing jumps out.
   - From the candidate comment, note the changes it describes and the framing it uses for `comment-faithful` and `comment-conventions`, respectively.

## Evidence gathering

<!-- For each evidence family your rubric's checks name, the concrete
gathering move: which part of the package (or, live, which page or
thread location per your evidence guide) to pull the fact from, and
what to record. A complete procedure leaves no check whose evidence an
executor would have to hunt for. -->

1. For each rubric check, read the evidence guide (in `reference/evidence-guide.md`) and evidence section of each check in `rubric.md`. In live mode, gather issue-side evidence from the locations the guide names; the drafts are the candidate side. In eval mode, quote the relevant lines from the bundle. Record the following information for each rubric check:
   - diagnosis-grounded → quote the root cause claim from the plan; quote the observed behavior line from the repro evidence
   - bounded-scope → list every file the plan says will be changed. Also note whether the plan separately lists any files that are adjacent to the changes that could be affected by the changes but should not be.
   - test-decisive → quote the test described and note whether before/after framing is stated
   - executable-by-a-stranger → read the implementation steps cold; note any steps that require outside context to interpret (quote them specifically)
   - uncertainty-honest → list every assertion in the diagnosis and implementation steps; flag any not traceable to the repro evidence.
   - comment-faithful → list the changes the comment claims; compare against the plan's implementation steps
   - comment-conventions → note the thread's explicit asks; note the repo's stated conventions from wherever the evidence guide points

2. For any rubric check where the evidence is missing, record explicitly that it is absent.

## Check execution

<!-- How one check runs against gathered evidence: in what order the
checks execute, what an executor does when evidence for a check is
genuinely absent, and when a check may be graded without re-reading
the whole package. A complete procedure makes two executors grade the
same package the same way. -->

1. For each rubric check, execute the check against the gathered evidence. All rubric checks are executed and graded in order of the checks in `rubric.md` regardless of whether they are `required` or `preferred`. The top-to-bottom order is for consistency, not a dependency; there is no short-circuiting. All checks should be run regardless of resulting grade and provide rationale for `pass` or `fail`, including if the reasoning is based on a previous check's grade.
   - Checks that require side-by-side comparisons (`diagnosis-grounded`, `comment-faithful`, `uncertainty-honest`): Hold the sources gathered in evidence gathering against each other and compare them to accurately grade the check.
   - Checks that require a single source (`bounded-scope`, `test-decisive`, `executable-by-a-stranger`, `comment-conventions`): Grade the check only against the specific gathered evidence
2. Go down the rubric checks one by one from the top. Grade each check with `pass`, `fail`, or `unclear` with a one-line evidence quote or fact and explanation for each grade. If evidence is missing for a required check, the grade is `fail`.
   - The evidence quote or fact should be stated specifically with an explanation as to why it leads to the grade provided. `pass` should quote the line or section of the source that aligns with the pass condition of the rubric check. `fail` should quote what part of the rubric check's pass condition is violated or missing from the evidence.
   - `unclear` means the evidence exists but it is ambiguous, implied, or not where the rubric says it should be. If the evidence is missing entirely, the grade is `fail`.
   - `required` checks must pass; `preferred` checks that are graded `fail` do not necessarily hold the package.

## Verdict assembly

<!-- How the per-check grades become the final accept or reject:
apply your rubric's verdict rule, state how unclear grades enter it,
and say what gets quoted in the output for the deciding check. A
complete procedure produces the same verdict from the same grades,
every time. -->

1. Apply the rubric's verdict rule ( `accept if every required check passes; preferred checks never change the verdict; unclear counts as fail.`) to produce the final verdict (`accept` - ready to post or `reject` - hold for review).
   - If the verdict is `reject`, quote the reasoning for each graded `fail` rubric check. If the verdict is `accept`, state that all required checks passed.
   - Any checks that are graded `unclear` count as `fail` in the verdict and will lead to a `reject` verdict if that check is `required`. Provide the reasoning for why the evidence was `unclear` in the rubric check.
2. In live mode, hold the drafts against the list created from the voice guide and quote any broken rules in the summary as advisory feedback for the candidate. This does not affect the verdict.
3. Follow the `SKILL.md` output instructions underneath the `verdict and output` section.
