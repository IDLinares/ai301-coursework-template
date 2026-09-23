# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72

**Verdict output**

[Your skill's live-mode output for this issue, pasted verbatim and ending with the
fenced JSON verdict block. A summary does not satisfy this field.]

**The verdict must record `accept` for this issue.** Choose an issue your own skill
accepts. If your skill rejects every candidate you try, that is a signal about your
rubric rather than about the issues: revise it and re-run — retries are unlimited and a
partial re-run costs about $0.20 — or run the skill on different candidates. Output
recording `reject` for the issue you chose earns no credit for this field.

```
Issue #72 — verify_password raises UnknownHashError on malformed hashes

┌───────────────────────┬─────────┬───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┐
│         Check         │  Grade  │                                                                     Evidence                                                                      │
├───────────────────────┼─────────┼───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┤
│ maintainer-alive      │ pass    │ Aburke225 committed 2026-09-16, 7 days ago; not a bot                                                                                             │
├───────────────────────┼─────────┼───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┤
│ repo-in-use           │ pass    │ archived: no; last push 2026-09-16, 7 days ago                                                                                                    │
├───────────────────────┼─────────┼───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┤
│ scope-fits-newcomer   │ pass    │ Single bug: catch UnknownHashError in core/security.py, return False, remove @pytest.mark.xfail from one test; clear end state, estimated 1–2 hrs │
├───────────────────────┼─────────┼──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┤
│ unclaimed             │ pass    │ No assignee; no linked PRs; one comment from sseid4 (NONE association = student); house rule: student claims don't block                          │
├───────────────────────┼─────────┼───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┤
│ ai-policy             │ pass    │ No policy files found; silence passes                                                                                │
├───────────────────────┼─────────┼───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┤
│ maintainer-responsive │ unclear │ No maintainer comments found across sampled issues; median undefined (preferred — no verdict impact)                                              │
└───────────────────────┴─────────┴───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┘

Verdict: ACCEPT

  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72",
    "checks": [
      {"name": "maintainer-alive", "grade": "pass", "evidence": "Aburke225 committed 2026-09-16 (7 days ago), not a bot"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "archived: no; last push 2026-09-16, 7 days ago"},
      {"name": "scope-fits-newcomer", "grade": "pass", "evidence": "Single bug: catch UnknownHashError in core/security.py, return False, remove one xfail marker; estimated 1-2 hrs"},
      {"name": "unclaimed", "grade": "pass", "evidence": "No assignee, no linked PRs; one student claim comment (sseid4, NONE association) — ignored per house rule"},
      {"name": "ai-policy", "grade": "pass", "evidence": "No CONTRIBUTING.md, AGENTS.md, or AI_POLICY.md found; silence passes"},
      {"name": "maintainer-responsive", "grade": "unclear", "evidence": "No maintainer comments found in any sampled issues; median undefined"}
    ],
    "verdict": "accept"
  }

```

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

[The agreement score of each run you did, in order. A single run is a complete answer if
only one run occurred. **The last score in your list must match the agreement line in the
`eval-run.txt` you committed** — that file is the record of your final run.]

First run: categories: claimed 4/4 clear-accept 6/8 dead-repo 3/3 policy 1/1 scope 3/4
agreement: 17/20 scored items

Second run: categories: claimed 4/4 clear-accept 8/8 dead-repo 3/3 policy 1/1 scope 3/4
agreement: 19/20 scored items (bar: 18/20: PASS)

**Issue analysis**

[One scored issue, identified by id (`issue-01` through `issue-20`; the `calib-`
issues are not scored). State your rubric's decision, the gold label, and the
reasoning that produced your rubric's result.]

item gold verdict agree note
issue-20 reject accept NO graded accept

My rubric has no check for issue quality or legitamcy, so there is no direct check to fail this issue.

**Check rationale**

[One check from the `rubric.md` uploaded to `tools/issue-select/`, quoted as it is
currently written, with the reasoning behind its current form.]

| maintainer-alive | Last 5 default-branch commits from the repo-facts block (commit dates and authors) | At least 1 non-bot commit (author username does not end in `[bot]`) dated within 90 days of the capture date (eval) or today (live)

90 days feels like a reasonable time to determine if the repo is still active. The bot check is to avoid false positives from bots that are not actively maintaining the repo.

**Trade-offs**

[What the quoted check gives up. Any one of these is a complete answer: an issue whose
result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a
stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns
the point in full when the reason follows.]

This check did not affect any verdicts on any issues as there was no need to edit this check on re-run. It does not give up anything, but does make my tool open to potentially slower maintained repos.

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

Answer all three:

1. The issue's fit to your interests and to the time available.

- The issue doesn't perfectly fit my main interest of working with frontend, but it is still a good fit for my general interests and knowledge of Python and is not too time consuming.

2. What the verdict identified correctly, and what you weighed that the rubric could
   not.

- The verdict is correct in accepting the issue showing that the repo is active with good scope for a newcomer allowing AI to help.

3. The anticipated difficulty in claiming it.

- There should be no difficulty in claiming this issue.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
