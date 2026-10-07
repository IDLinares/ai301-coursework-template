# Plan Fix for Issue #72

## Summary

Fix the `UnknownHashError` bug in `core/security.py` by changing the `verify_password` function to return `False` instead of raising the standard Passlib CryptContext exception for an unrecognized hash.

## Diagnosis

`core/security.py` calls `pwd_context.verify` to check passwords against stored hashes. Passlib's `CryptContext` raises `UnknownHashError` when the hash is not recognized. The `verify_password` function should return `False` instead of raising the exception.

## Scope

**In Scope**

- core/security.py
- tests/unit/test_security.py

**Out of Scope**

- .venv/Lib/site-packages/passlib/context.py (Passlib's CryptContext class should not be modified)

## Approach

1. In `core/security.py`, add a try/except block in `verify_password`. The try/except block should wrap the `pwd_context.verify` call and catch `passlib.exc.UnknownHashError` and return `False` when it fires. Example implementation:

```python
try:
    return bool(pwd_context.verify(plain_password, hashed_password))
except Exception:
    return False
```

2. In `tests/unit/test_security.py`, remove the marker `@pytest.mark.xfail` from the `test_verify_with_wrong_hash_format` test. The test should now pass.

## Test Plan

1. Run `source .venv/Scripts/activate` (Git Bash on Windows) to activate the virtual environment.
2. Run `pytest tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format -v --disable-warnings --tb=short` from the root directory of the repository.

## Deviations

There were no deviations from the original plan.
