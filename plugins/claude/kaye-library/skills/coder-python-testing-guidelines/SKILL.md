---
name: coder-python-testing-guidelines
description: writes, reviews Python `pytest` test code per project conventions
when_to_use: trigger on `test_*.py`/`*_test.py` files, pytest, fixtures, mocks, parametrize, assertions, or requests like write/add/fix a unit test or test case. Not for non-test Python code
metadata:
  version: 1.4.0
paths:
- '**/test_*.py'
- '**/*_test.py'
---

### Coder Python Testing Guidelines
This section pertains specifically to Python test code. Tests should be compatible with the `pytest` module.
- used in combination with [Coder](#coder) and [Coder Python](#coder-python)
- test class names should start with `Test`, and test function names should begin with `test_`
- strive to create as many separate test functions as possible, with each test case in individual functions
- group related test cases under a single test class for organization
- test classes and test functions do **not** require docstrings — the class and function names should be descriptive enough to convey their purpose
**Each test file** must begin with a module-level docstring that briefly describes what unit or component is being tested.
*Example of tests for the `add` function:*
```python math_utils_test.py
"""
math_utils_test.py

tests for the `add` function in `math_utils.py`
"""


class TestAdd:
    def test_addition_of_integers(_):
        assert add(1, 1) == 2

    def test_addition_with_different_operands(_):
        assert add(1, 2) == 3
        assert add(2, 1) == 3

    def test_negative_value_error(_):
        with pytest.raises(ValueError) as ei:
            add(1, -1)
        assert str(ei.value) == (
            "Addition of negative value is not supported. Please contact your "
            "admin for more information.")

    def test_invalid_type_error(_):
        with pytest.raises(ValueError) as ei:
            add('a', 5)
        assert str(ei.value) == (
            "Addition of a string and an integer is not supported. Please "
            "contact your admin for more information.")
```