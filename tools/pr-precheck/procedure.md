# Procedure: how this tool grades a PR package

<!--
THIS IS THE PART YOU WRITE (second week running for the procedure).
Week 3 you wrote these steps for a plan package; this week the graded
object is a PR package, and the read that matters most is a
side-by-side: the diff against the plan, the evidence against the test
plan, the description against both. Your week-3 procedure is the
pattern; do not paste it unchanged, because its read order was built
for a different object.

Your rotation is the design brief again, and this week friction routes
three ways: a stall on WHAT to decide is a rubric gap, a stall on
WHERE to look is a procedure gap (this file), and a stall on what the
tool even reads or outputs is a frame gap (your SKILL.md). A complete
procedure lets someone who has never seen a PR package before grade
one exactly the way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
plan's scope pair before opening the diff, and list the files the plan
names" is a step; "understand the change" is a wish.
-->

## Read order

Read in this order before grading any check. Record the noted items as a working list; checks run against those notes, not against re-reads.

1. **Mode and scope (live only).** Read `scope.md`. Confirm the issue lives in the scoped repo. Stop and report if the Repo line is unfilled. Read `voice-guide.md` and hold it aside for the PR text check after evidence gathering.

2. **The plan.** Read `plan.md` (eval: the plan-context block). Extract and write down: (a) every file or path the plan names as in-scope, (b) every deviation note with the scope change it states, (c) the test plan's stated evidence goals — what observable outcome the test must show.

3. **The issue.** Read the issue body and any linked repro steps. Note the reported behavior (what breaks) and the expected behavior (what the fix should produce). This anchors what "the expected behavior" means when grading test evidence.

4. **The diff.** Read `git diff main...HEAD` (live) or the diff section of the eval bundle. List every changed file. For each file, note any hunks that look unrelated to the plan's scope — debug lines, formatting-only edits, drive-by changes.

5. **The PR description and title.** Read the draft description. Note every factual claim it makes about what changed and what the fix does. Hold these claims against the diff notes from step 4; flag any mismatch.

6. **The test evidence.** Read the test-evidence section (eval) or the captured output linked in the draft PR (live). Note: whether a before state is shown, whether an after state is shown, whether the after state names a specific observable change, and whether the repo's CI checks are shown as passing or explicitly disclosed as failing.

7. **The repo's template and disclosure asks.** Read the repo-facts block's PR template sections and stated policy (eval) or `.github/PULL_REQUEST_TEMPLATE.md` and CONTRIBUTING.md (live). List every required section and every required disclosure.

**Why this order:** Plan before diff, so the scope boundary is established before evaluating whether the diff respects it. Issue before description, so the grader can detect whether the description correctly frames the fix. Evidence after the diff, so claimed outcomes can be matched against actual changes. Template asks last, because they are read against the title and description already noted in step 5.

---

## Evidence gathering

After completing the read order, build one evidence record per check using the notes already taken. Do not re-read the full package; pull from the notes. Record the specific fact or quote — not a summary — that will decide each check.

**silent-drift:** Pair the list of changed files from step 4 against the scope list and deviation notes from step 2. For each changed file: is it named in the scope list? Is it covered by a deviation note? Record any file that matches neither. Record any deviation note that covers a file not in the diff (honest shortfall, noted).

**not-tested:** Pair the test evidence notes from step 6 against the test plan goals from step 2c and the issue's expected behavior from step 3. Record: does the evidence show the before state? Does it name the specific observable change in the after state? Are CI checks shown as passing, or are failing checks disclosed with a stated reason? Copy the exact phrase the evidence uses (or note its absence) for the pass-condition check.

**unreviewable:** Use the per-file hunk notes from step 4. For each flagged hunk, record whether it traces to a plan-scoped change or is extraneous (debug output, dead code, formatting-only edit, drive-by rename). Record the specific file and line description.

**standards-wall:** Pair the required template sections and disclosures from step 7 against the PR title and description from step 5. For each required section: is it present and non-empty, or marked N/A with a reason? For each required disclosure: does it appear in the title or description? Record each section and disclosure status explicitly.

---

## Check execution

Run checks in rubric order: silent-drift → not-tested → unreviewable → standards-wall.

For each check:

1. Pull the evidence record built in the gathering stage for that check.
2. Apply the rubric's pass condition exactly as written. Do not substitute your own judgment for the stated condition.
3. Assign a grade:
   - **pass**: the pass condition is satisfied by the gathered evidence.
   - **fail**: the pass condition is not satisfied by the gathered evidence.
   - **unclear**: the package does not contain enough information to determine whether the condition is satisfied. Record what specific information is absent.
4. Write the one-line evidence entry: the specific fact, quote, or absence that decided the grade. "Looks fine" is not a valid entry.

**When evidence for a check is genuinely absent** (e.g., no test-evidence section exists in the package, or the diff section is missing): grade the check `unclear` and record what is absent. Do not assume a passing state from silence.

**A check may be graded from notes alone** without re-reading the full package, as long as the notes contain the specific fact needed. If the notes are ambiguous on the deciding point, return to the original source for that one fact and update the note.

---

## Verdict assembly

1. Collect the four check grades (pass / fail / unclear).
2. Substitute fail for every unclear on a required check. (Unclear counts as fail per the rubric's verdict rule.)
3. Apply the verdict rule: accept if every required check passes; reject if any required check fails.
4. Emit the output. The JSON block lists all four checks with their grades and evidence lines. Before the JSON, write one line per check stating the grade and the evidence.
5. **Deciding check for the summary:** when more than one required check failed, the deciding check is the first failing required check in rubric order (silent-drift, then not-tested, then unreviewable, then standards-wall). Name it explicitly in the readable summary as the primary reason for rejection.
6. In live mode, append any voice-guide rule violations to the readable summary after the check lines. These do not change the verdict unless the rubric has a check that reads the voice guide.
