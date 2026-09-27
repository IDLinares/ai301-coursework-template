# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**IDLinares**

---

## Posted upstream

**[Claim comment](https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72#issuecomment-5850958712)**

Hello, I would like to work on this issue, #72, as a first contribution to the pathreview project. The issue describes an incorrect behavior of the `verify_password` function in the `core/security.py` module. Verification of a password against a malformed hash is current returning `UnknownHashError` from passlib instead of failing closed and returning `False`.

I will start by forking the repo and setting it up on my local machine, recording my OS and tool versions, following the docs/SETUP.md steps. Then, I will run the covering test, `test_verify_with_wrong_hash_format`, to make sure I can reproduce the issue on my machine and record the steps I took to do so.

**[Reproduction comment](https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72#issuecomment-5850961770)**

## Environment

**Operating system**: Windows 11 10.0.26200 (x64)

**Tool versions**: pathreview 0.1.0 | Git 2.42.0.windows.2 | Python 3.12.1 | passlib[bcrypt] 1.7.4 | bcrypt 4.3.0 | python-jose[cryptography] 3.5.0

## Reproduction Steps

From a fresh clone of a fork of this repository and setup following `docs/SETUP.md`, reproduce the following steps:

1. Run `source .venv/Scripts/activate` (Git Bash on Windows) to activate the virtual environment.
2. Run `pytest tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format -v --runxfail --disable-warnings --tb=short` from the root directory of the repository.

## Output from the test

```bash
tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format FAILED                                                                                                                                                                                                              [100%]

=============================================================================================================================================== FAILURES ===============================================================================================================================================
___________________________________________________________________________________________________________________________ TestSecurity.test_verify_with_wrong_hash_format ____________________________________________________________________________________________________________________________
tests\unit\test_security.py:227: in test_verify_with_wrong_hash_format
    result = verify_password("password", wrong_hash)
             ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
core\security.py:37: in verify_password
    return bool(pwd_context.verify(plain_password, hashed_password))
                ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
.venv\Lib\site-packages\passlib\context.py:2343: in verify
    record = self._get_or_identify_record(hash, scheme, category)
             ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
.venv\Lib\site-packages\passlib\context.py:2031: in _get_or_identify_record
    return self._identify_record(hash, category)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
.venv\Lib\site-packages\passlib\context.py:1132: in identify_record
    raise exc.UnknownHashError("hash could not be identified")
E   passlib.exc.UnknownHashError: hash could not be identified
======================================================================================================================================= short test summary info ========================================================================================================================================
FAILED tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format - passlib.exc.UnknownHashError: hash could not be identified
===================================================================================================================================== 1 failed, 1 warning in 0.38s =====================================================================================================================================
```

## Outcomes

**Expected**: `verify_password("password", wrong_hash)` should return `False`.

**Actual**: `verify_password("password", wrong_hash)` raises `passlib.exc.UnknownHashError` instead of returning `False`.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

Run 1:

"categories: clear-accept 7/8 disclosure 0/1 no-evidence 4/4 unfollowable-comms 2/3 wrong-target 3/4
agreement: 16/20 scored items (bar: 18/20: below the bar; category floor unmet: no match in disclosure)"

Run 2:

"categories: clear-accept 5/8 disclosure 0/1 no-evidence 4/4 unfollowable-comms 3/3 wrong-target 4/4
agreement: 16/20 scored items (bar: 18/20: below the bar; category floor unmet: no match in disclosure)"

Run 3:

"categories: clear-accept 8/8 disclosure 1/1 no-evidence 4/4 unfollowable-comms 3/3 wrong-target 4/4
agreement: 20/20 scored items (bar: 18/20: PASS)"

**Package analysis**

[Pick one scored package (`pkg-01` through `pkg-20` — the four `calib-` packages are never
scored). Name it by id, say what your rubric decided and what the gold label said, and
explain why your rubric read it that way.]

Specifically for Run 1, I will be analyzing `pkg-20`.

Rubric decided: PASS

Gold label: REJECT

Reasoning: My rubric did not have a specific section for AI disclosure or claim content. It only addressed following the repo's template and conventions, so it passed when it should have rejected.

**Check rationale**

Rubric check: Repo-conventions

"The report follows standard reproduction conventions (environment, steps, artifacts, outcomes). If the repo's contribution policy explicitly mandates AI disclosure on comments/issues, disclosure is present. Permissive AI policies, human-voiced comments on repos that restrict bot spam, or omitting non-essential template fields (like full package lists) pass."

Why: The repo conventions need to address not just the structure of the reproduction report (making sure it follow the standard structure), but also any specific requirements of the repo's contribution policy. My original rubric did not address AI disclosure that is often specified in repos' policies, so I needed to add a section for that.

**Trade-offs**

My rubric has actual vs expected as a preferred check, even though it is a good standard for a standard reproduction report. This shows that the contributor understands what the issue is doing and what the app is intended to do, but not all reports have this exact setup. I felt it was more important the contributor shows they were able to reproduce the failure the issue describes as opposed to explicitly stating what the intended behavior is.

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
