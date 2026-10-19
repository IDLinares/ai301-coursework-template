# Evidence guide: where evidence lives in a PR package

<!--
THIS IS THE PART YOU WRITE (third week running: the map stays in your
hands). Your tool uses this guide as its map: for every kind of
evidence a rubric check names, this file says WHERE to find it in a PR
package and WHAT GOOD LOOKS LIKE when you do.

The four families below are the harness's failure categories under
the names the eval README uses: plan fidelity = silent-drift, test
evidence = not-tested, diff quality = unreviewable, standards and
comms = standards-wall. A package that fails none of them is a
clear-accept. Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the plan-context block's scope pair and test
  plan, the candidate PR's diff, commits, description, or
  test-evidence section, the repo-facts block's template asks and
  stated policy). In live mode (where in your working copy and on
  GitHub: your plan.md and its deviation notes, your branch's diff,
  your draft title and description, your captured test output, the
  repo's PR template and CONTRIBUTING.md).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("every changed file falls inside the
  plan's stated boundary or a deviation note") over adjectives ("the
  diff is clean").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts three ways: your
procedure says WHEN to gather each family, this guide says WHERE, and
your SKILL.md says the tool reads both. Write the map you wish your
executor had.
-->

## Plan fidelity (harness category: silent-drift)

**Where it lives**

- Eval bundle: the plan-context block's scope/boundary section and any deviation notes appended to it; the candidate PR's diff showing every changed file and hunk; the candidate PR's description, where fidelity claims ("this PR fixes X by changing Y") are made.
- Live mode: `plan.md`, specifically the scope/boundary section and any deviation notes at the bottom of the file; the branch diff (`git diff main...HEAD`); the draft PR description's summary of what changed.

**What good looks like**

Every file touched in the diff appears in the plan's stated scope or is covered by a deviation note that names it. The PR description's claims about what changed match what the diff actually contains — no claimed changes absent from the diff, no diff changes unmentioned in the description. A diff that honestly does less than the plan (with a deviation note explaining the shortfall) still passes; a diff that silently does more does not.

**What silent drift looks like**

More direction: files changed that the plan never named, with no deviation note to account for them. Less direction: the plan promised changes to file A but the diff omits them, with no note. Description direction: the description states the fix covers behavior X but the diff only touches the code path for behavior Y.

---

## Test evidence (harness category: not-tested)

**Where it lives**

- Eval bundle: the test-evidence section of the candidate PR — before/after terminal output, screenshots, or log captures; the plan-context block's test plan section naming what evidence was expected; the repo-facts block's stated CI or check policy.
- Live mode: the captured test output attached or linked in the draft PR description (screenshots, terminal captures, CI run links); the test plan section of `plan.md`; the repo's CI status on the branch (GitHub Actions, etc.); CONTRIBUTING.md's stated test requirements.

**What good looks like**

The evidence shows two observable states: a before (the reproduction confirms the issue exists) and an after (the fix resolves it). The after state names the specific changed behavior — not just "it works" or "test passes," but the concrete output, UI change, or behavior that is now different. Any repo CI checks are shown as passing, or any failing check is explicitly disclosed with a stated reason.

**What "tests pass" alone looks like**

A claim with no before state, no named observable behavior, and no link to CI output. A screenshot of a green badge with no reproduction of the issue first. Evidence that the suite ran but no confirmation that the specific repro steps now behave correctly.

---

## Diff quality (harness category: unreviewable)

**Where it lives**

- Eval bundle: the candidate PR's diff section — the unified diff showing every changed file and hunk; the commit list showing each commit's summary.
- Live mode: the branch diff (`git diff main...HEAD`); the commit log (`git log main..HEAD`).

**What good looks like**

Every changed line traces directly to the plan's stated scope. The fix or feature is visible in isolation — a reviewer can read the diff and identify exactly what the change does without digging through unrelated edits. Commits are coherent with the scope.

**What debris looks like**

Debug print statements left in after testing; commented-out code blocks not part of the fix; whitespace or style-only edits on lines unrelated to the planned change; drive-by renames or refactors not mentioned in the plan; formatting churn that obscures the actual change in a noisy diff.

---

## Standards and comms (harness category: standards-wall)

**Where it lives**

- Eval bundle: the repo-facts block's PR template sections (the required headings and any fill-in prompts); contributing instructions and stated disclosure policy (e.g., an AI-use disclosure requirement); the candidate PR's title and description where those asks must be honored.
- Live mode: the repo's PR template (`.github/PULL_REQUEST_TEMPLATE.md` or the template pre-filled when opening a PR on GitHub); CONTRIBUTING.md's stated requirements; any explicit maintainer asks in the issue thread; the draft PR title and description.

**What compliant looks like**

Every required template section is addressed — either filled with real content relevant to the change, or marked N/A with a brief stated reason. Required disclosures appear in the title or description (e.g., "AI assistance: used Claude to draft the fix"). Any specific asks a maintainer stated in the issue thread are acknowledged.

**What non-compliant looks like**

Template sections left blank with no explanation. Placeholder text unchanged (e.g., "Describe your changes" left as the section body). A known disclosure requirement present in the repo-facts block but absent from the PR. Boilerplate that was not adapted to the actual change.
