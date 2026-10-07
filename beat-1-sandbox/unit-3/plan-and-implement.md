# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**IDLinares**

---

**[Plan comment](https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72#issuecomment-6044442394)t**

I traced the bug to the `verify_password` function in `core/security.py`. The function calls `pwd_context.verify` to check passwords against stored hashes. This traces back to Passlib's `CrypyContext` class, which raises `UnknownHashError` from the `idenfify_record` method when the hash is not recognized. I wrapped the `pwd_context.verify` call in a try/except block to catch the exception and return `False` gracefully, instead of raising the exception. The `test_verify_with_wrong_hash_format` test passes now.

## Your branch

**fix/72-verify-password-error**

**Evidence**

Before:

From a fresh clone of a fork of this repository and setup following `docs/SETUP.md`, reproduce the following steps:

1. Run `source .venv/Scripts/activate` (Git Bash on Windows) to activate the virtual environment.
2. Run `pytest tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format -v --runxfail --disable-warnings --tb=short` from the root directory of the repository.

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

---

After:

From a fresh clone of a fork of this repository and setup following `docs/SETUP.md`, reproduce the following steps:

1. Run `source .venv/Scripts/activate` (Git Bash on Windows) to activate the virtual environment.
2. Run `pytest tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format -v --disable-warnings --tb=short` from the root directory of the repository.

```bash
 pytest tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format -v --disable-warnings --tb=short
================================================================================================================================== test session starts ==================================================================================================================================
platform win32 -- Python 3.12.1, pytest-9.1.1, pluggy-1.6.0 -- C:\Users\isaia\Github\pathreview-ai301-fa26-s3\.venv\Scripts\python.exe
cachedir: .pytest_cache
hypothesis profile 'default'
benchmark: 5.3.0 (defaults: timer=time.perf_counter disable_gc=False min_rounds=5 min_time=0.000005 max_time=1.0 calibration_precision=10 warmup=False warmup_iterations=100000)
rootdir: C:\Users\isaia\Github\pathreview-ai301-fa26-s3
configfile: pyproject.toml
plugins: anyio-4.15.1, hypothesis-6.168.1, platformdirs-4.12.0, asyncio-1.4.0, benchmark-5.3.0, cov-7.1.0, pytest_httpserver-1.1.5
asyncio: mode=Mode.STRICT, debug=False, asyncio_default_fixture_loop_scope=None, asyncio_default_test_loop_scope=function
collected 1 item

tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format PASSED                                                                                                                                                                                               [100%]

============================================================================================================================= 1 passed, 1 warning in 0.30s ==============================================================================================================================
```

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

Only run:

categories: clear-accept 6/7 scope-creep 4/4 thread-convention 2/2 unbuildable 3/3 wrong-cause 4/4
agreement: 19/20 scored items (bar: 18/20: PASS)

**Package analysis**

`pkg-06`

Rubric decided: REJECT

Gold label: REJECT

Reasoning: My rubric failed the package on the `bounded-scope` check since it can only pass if the proposed changes are limited only to what is necessary to fix the issue. This packages proposes changes to refactor the whole pipeline for saving images when the issue is specifically just with exporting the images. The suggested pipeline refactoring should be proposed as a separate issue and PR.

**Check rationale**

Rubric check: `uncertainty-honest`

"passes if there are no claims stated with certainty about behavior that is not supported by the repro evidence, or if unverified claims are flagged as assumptions or unknowns"

Why: This check ensures the plan's diagnosis and implementation are supported by evidence from the repro so that the fix is accurate. Initially, I only had the first part about not having unsupported claims, but I added the second part about unverified claims being flagged as assumptions or unknowns since every claim cannot be entirely verified, but the fix can still be correct. In that case, the check should still pass as long as the plan states any assumptions or unknowns explicitly.

**Trade-offs**

My rubric's `executubable-by-a-stranger` check is a bit strict in that it only passes if there is a list of steps in order that can be followed to resolve the issue without any additional information. For simpler fixes, this check could cause the plan to fix as they require less context and effort to implement. Some might only be one step but if there isn't an explicit list, the rubric could fail the package.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.
