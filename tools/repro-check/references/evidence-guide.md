# Evidence guide: where proof lives in a reproduction package

## Environment

**Where it lives**

The environment line or section at the top of the reproduction report. In an eval package, look in the "Candidate repro report" section. Compare it with the issue's own environment line and with what the repo's bug-report template asks for (found in the "Repo facts" block under "bug reports").

**What good looks like**

Both the OS (name + version) and the relevant tool version are named explicitly. If the reporter's version differs from the one the issue was filed against, the difference is called out rather than silently substituted. Testing on a different version fails if it isn't called out or if the issue specifies reproducing on the latest release.

## Steps

**Where it lives**

The numbered or sequentially described steps in the reproduction report, following the environment line. Compare them against the steps given in the original issue.

**What good looks like**

Steps are present, ordered, and self-contained: a stranger could follow them from a clean starting state to the trigger without needing to ask the author for clarification. There are no implied prerequisites (files, configs, prior state) that aren't created or explained within the steps themselves. Specifying that the issue's reproduction script or code snippet is run as part of the steps is self-contained and acceptable as long as it is in order with the reproduction steps.

## Artifacts

**Where it lives**

Pasted terminal output, error messages, logs, screenshots, or video embedded in or attached to the reproduction report. In an eval package, these appear inside code fences or as described attachments within the "Candidate repro report" section.

**What good looks like**

At least one concrete artifact is present — a command plus its actual output, a screenshot, or a log excerpt — that a reader can inspect to independently verify that the reporter ran the steps and observed a result.

## Claim-intent

**Where it lives**

The candidate claim comment.

**What good looks like**

The claim is specific to the issue and free of generic boilerplate, self-assignment demands, or guaranteed fix timelines.

## Issue-match

**Where it lives**

The artifact(s) in the reproduction report, read against the behavior described in the issue. The issue's "Actual behavior" or error output is the reference. In an eval package, compare the artifact in "Candidate repro report" with the terminal output or description in the "Issue" section.

**What good looks like**

The artifact captures the same failure mode the issue describes. A different error message, exit code, or symptom — even a superficially related one — does not satisfy this check. For example, a report that triggers a validation error when the issue describes a process crash has not matched the issue's behavior.

**Cannot-reproduce exception**

If the outcome claim is "cannot reproduce" (or equivalent: "did not trigger," "could not confirm"), apply this check as follows: grade Issue-match **pass** automatically, provided Honest-outcome passes. A valid cannot-reproduce report has no failure artifact to match — the artifact correctly shows the behavior was _not_ observed — so demanding the issue's failure mode appear in the artifact would misread what the report is claiming. All ordinary proof requirements (attempt evidence, environment, steps) are still evaluated by their own checks.

## Honest-outcome

**Where it lives**

The outcome claim in the reproduction report (phrases like "reproduced," "confirmed," "cannot reproduce," or "expected / actual" sections) matched against the artifact evidence present in the same report.

**What good looks like**

The claim matches what the artifacts actually show. If the report says "reproduced," the artifacts must demonstrate the described failure. If the report says "cannot reproduce," evidence of the attempt (the commands run, the output received) must be present. A report that asserts reproduction while showing a different or absent failure fails this check.

## Actual-vs-expected

**Where it lives**

The written prose of the reproduction report, independent of any artifact. Look for an explicit "Expected:" and "Actual:" block, or equivalent labeled prose, anywhere in the report text.

**What good looks like**

The report states in plain text what the reporter expected to happen and what they observed instead, as two separate written claims. Restating the artifact output verbatim without a written expected-behavior statement does not satisfy this check.

## Repo-conventions

**Where it lives**

The structure and wording of the entire submission — the claim comment and the reproduction report — compared against the repo's stated template or contribution policy. In an eval package, the template requirements appear in the "Repo facts" block under "bug reports" and "contribution policy," including any AI-use disclosure requirements.

**What good looks like**

The report's structure should follow the standard structure (e.g., version, steps, artifacts, and outcomes/expected vs actual). It does not need to duplicate new-issue intake requirements like issue titles, duplicate search confirmations, or extraneous package dumps unless relevant to the bug. If the repo states an AI-use policy (such as a disclosure requirement in CONTRIBUTING.md or AI_POLICY.md), the submission must comply. Only explicit mandatory disclosure on the report requires AI-use to be stated in the report. Permissive or PR-only policies do not require an AI use statement in the comment or report. In an eval package, all candidate submissions are treated as AI-assisted.
