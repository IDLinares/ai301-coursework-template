# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check                 | Evidence                                                                                                                                                                            | Pass condition                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 | Weight    |
| --------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------- |
| maintainer-alive      | Last 5 default-branch commits from the repo-facts block (commit dates and authors)                                                                                                  | At least 1 non-bot commit (author username does not end in `[bot]`) dated within 90 days of the capture date (eval) or today (live)                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | required  |
| repo-in-use           | `archived:` flag and `last push to any branch` from the repo-facts block                                                                                                            | `archived: no` AND last push within 180 days of the capture date (eval) or today (live)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | required  |
| scope-fits-newcomer   | Issue body and comment thread                                                                                                                                                       | Issue addresses one bug, feature, or docs gap with a clear end state. Fail only when: (a) the issue is explicitly a tracking/umbrella issue listing separate sub-issues meant to be split into distinct PRs; (b) it is a pure support/usage question with no actionable change requested; (c) the comment thread shows an active, unresolved design debate with no maintainer settling it; or (d) a maintainer has stated outright that the fix requires deep core-internals knowledge. A detailed or multi-bullet body alone does not fail this check — structured detail is not the same as unbounded scope. | required  |
| unclaimed             | `assignees:` and `linked PRs:` from the repo-facts block; claim comments in the comment thread with their dates and any maintainer acknowledgment; issue open date vs. capture date | No assignee AND no open linked PR AND no claim comment that received a maintainer acknowledgment within the last 30 days. Additionally fail if the issue has 2 or more closed/unmerged linked PRs, OR if the issue has been open for more than 2 years AND has evidence of at least 2 separate abandoned attempts (claim comments that were later auto-unassigned, or closed/unmerged PRs) — this pattern signals the issue is harder than it looks.                                                                                                                                                           | required  |
| ai-policy             | `contribution policy` line from the repo-facts block, including any referenced `CONTRIBUTING.md`, `AI_POLICY.md`, or `AGENTS.md` content                                            | No outright ban on AI-generated or AI-assisted contributions; conditions (disclosure, personal understanding, testing, human review) are not a ban and pass; silence passes                                                                                                                                                                                                                                                                                                                                                                                                                                    | required  |
| maintainer-responsive | `maintainer first-response sample` from the repo-facts block (days to first owner/member/collaborator comment across the 5 sampled issues)                                          | Median first-response time across issues that have a maintainer comment is <= 30 days                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | preferred |

## Verdict rule

Accept if every required check passes; preferred checks never change the verdict and are used only to rank accepted issues against each other; `unclear` on any required check counts as fail (reject).
