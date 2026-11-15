---
name: coder-python
description: 'writes, edits, reviews Python code: scripts, modules, packages, functions, classes, inline snippets'
when_to_use: trigger for any Python task — `.py` files, code blocks, writing/fixing/refactoring/optimizing/reviewing Python, or bare code requests with no language stated in a Python context. Not for docstring-only or test-only requests, route those to the dedicated skills
metadata:
  version: 1.3.2a0
paths:
- '**/*.py'
---

## Coder Python
Adhere to the **PEP8** style guide, ensuring clarity and consistency.
- do **not** use type hints anywhere (no variable annotations, no function parameter or return type annotations).
- prefer `str.format()` for string formatting, dont use f-strings (`f""`).
- for every `try`/`except` block, bind the exception with `as e` (eg `except ValueError as e:`); if that block re-raises, the `raise` must include `from e`.
- writing code based on [Coder](#coder)
Common CBs:
- `constructor`, place before `__init__()`
- `magic methods`, eg for `__repr__()`
- `operators`, eg for `__or__()`