# Rubric: is this pull request ready to submit?

<!--
THIS IS THE PART YOU WRITE (fourth week running; this is the rubric's
final form in the sandbox). Your frame in SKILL.md executes whatever
checks you define here, via your procedure.md. It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the diff read against the plan's scope, the test
     evidence read against the plan's test plan, the description read
     against the diff, the repo-facts block's template asks) or a
     location from your references/evidence-guide.md. "The PR" is not
     a source; "the diff's changed files read against the plan's
     stated boundary" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself
     (does the diff fall inside the plan plus its deviation notes? is
     the claimed evidence observable?), never the write-up's shape
     (how long the description is, how many commits there are).
     Structure-shaped checks are what make graders disagree with
     themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (submit) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. State the `unclear`
   treatment explicitly: the frame here is YOUR SKILL.md, so a rubric
   that stays silent is only covered if your frame's grading
   discipline says what happens (the contract's own default is that
   an unverifiable claim fails).

Cover what actually gets bad PRs submitted. The failure families the
lecture named ARE the harness's scoring categories, same names as the
eval README: silent drift (the diff silently does more or less than
the posted plan, or the description claims fidelity the diff
contradicts), not tested (the evidence proves nothing observable, or
the repo's own checks were never run), unreviewable (debris or
unrelated hunks bury the change), and standards wall (the repo's
stated template and disclosure asks are ignored). Your evidence
guide's four headings map onto these one to one (plan fidelity =
silent drift, test evidence = not tested, diff quality =
unreviewable, standards and comms = standards wall), and the category
floor is scored on exactly these names plus clear accept. A rubric
that ignores a category will fail the eval packages built around
that category. And remember the honest-outcome
rule, fourth week running: a PR that honestly discloses a shortfall
can be ready; a rubric that equates "less than everything" with
"hold" fails the set.
-->

## Checks

| Check          | Evidence                                                                                                                                                                                         | Pass condition                                                                                                                                                                                                                                                                                                   | Weight   |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| silent-drift   | The diff's changed files read against the plan's stated scope and any deviation notes in plan.md                                                                                                 | Passes if every file in the diff is in scope either in the plan's changes or in the deviation notes. Any changes not mentioned in the plan cannot pass.                                                                                                                                                          | Required |
| not-tested     | The draft PR's test evidence read against the plan's test plan and the repo's own checks                                                                                                         | Passes if the repro steps with the built change show the expected behavior and the evidence names the observable change. A repo check that fails is acceptable only if the PR explicitly discloses it with a reason; undisclosed failing checks fail this check. 'Test passes' alone is not sufficient evidence. | Required |
| unreviewable   | The diff's changed lines and files read against the plan's stated scope, with attention to non-functional changes (debug output, dead code, formatting-only edits on lines unrelated to the fix) | passes if every changed line serves the scope defined in the plan. No debug output, dead code, or formatting-only edits on lines unrelated to the planned change.                                                                                                                                                | Required |
| standards-wall | The repo's stated template and disclosure asks read against the draft PR's title and description                                                                                                 | Passes if the repo's PR template sections are addressed (marking N/A with a reason counts) and all required disclosures (e.g., AI use) appear in the title or description. Silent omissions — template sections left blank without explanation — fail this check.                                                | Required |

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->

Only accept if every required check passes. Preferred checks never change the verdict. Unclear counts as a fail.
