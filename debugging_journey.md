# Parabank UI Automation – Debugging Journey Documentation

This document captures every major error encountered from the start of the project (yesterday) until the moment the first test successfully passed. Each issue is listed with the cause, the fix applied, and what we learned during the process.

---

## 1. **Pytest collected 0 tests**

### **Error Message:**

No tests were collected when running `pytest`.

### **Cause:**

Pytest could not detect test files because folder names or file names did not align with Pytest's default discovery rules.

### **Solution:**

* Renamed the `tests` folder correctly.
* Ensured filenames follow the pattern `test_*.py`.
* Created a proper `pytest.ini` to explicitly define discovery rules:

  ```ini
  [pytest]
  testpaths = tests
  python_files = test_*.py
  python_classes = Test*
  python_functions = test_*
  ```

### **Outcome:**

Pytest recognized the test structure but still collected 0 tests due to missing methods.

---

## 2. **Import errors while resolving modules**

### **Error Message:**

```
ImportError: cannot import name 'LoginPage' from 'pages.login_page'
```

### **Cause:**

Python import system couldn't locate the `pages` package as a proper module.
This was because the project was missing required `__init__.py` files.

### **Solution:**

* Added `__init__.py` in:

  * `/base`
  * `/pages`
  * `/utils`
  * `/tests`
* Ensured correct import path:

  ```python
  from pages.login_page import LoginPage
  ```

### **Outcome:**

Pytest was able to import page-object modules successfully.

---

## 3. **Pytest using incompatible import mode**

### **Error Message:**

Pytest still couldn't import modules correctly, especially on Python 3.14.

### **Cause:**

Pytest’s new import system in Python 3.14 had conflicts.

### **Solution:**

Added this line inside `pytest.ini`:

```ini
addopts = --import-mode=importlib
```

### **Outcome:**

Imports finally stabilized.

---

## 4. **Fixture 'setup' not found**

### **Error Message:**

```
fixture 'setup' not found
```

### **Cause:**

The test class used:

```python
@pytest.mark.usefixtures("setup")
```

But no such fixture was defined.

### **Solution:**

Created a proper `setup` fixture inside `conftest.py`:

```python
import pytest
from selenium import webdriver

def setup(browser="chrome"):
    pass  # Initial placeholder
```

Then transformed it into a fully working Selenium fixture:

```python
@pytest.fixture
def setup():
    driver = webdriver.Chrome()
    driver.get("https://parabank.parasoft.com/")
    yield driver
    driver.quit()
```

### **Outcome:**

Tests could now request the fixture.

---

## 5. **Test discovered, but nothing ran**

### **Error Message:**

Pytest found the test class but did not execute the method.

### **Cause:**

The test file contained a class but not a valid test method initially.
Methods must start with `test_`.

### **Solution:**

Verified method name:

```python
class TestLogin:
    def test_valid_login(self, setup):
        pass
```

### **Outcome:**

Pytest recognized and executed the test.

---

## 6. **Page Object Methods Empty – Causing No Browser Interaction**

### **Issue:**

The `LoginPage` methods (`enter_username`, `enter_password`, `click_login`) were empty (only `pass`).

### **Cause:**

Initial placeholder methods had not been implemented.

### **Solution:**

Left them temporarily empty until the framework structure passed test discovery.
(This was intentional at this stage.)

### **Outcome:**

Pytest executed the test without failing because there were no Selenium operations yet.

---

## 7. **Finally: First Test Passed**

### **Message:**

```
1 passed in 17.13s
```

### **Why It Passed:**

* Folder structure fixed
* Imports resolved
* Pytest configuration corrected
* Selenium fixture working
* Test file properly discovered
* Test method implemented correctly

### **Milestone Achieved:**

**A fully working Pytest + Selenium Page Object Model setup is now alive and ready for real automation work.**

---

# Summary of What We Learned

1. **Pytest is strict about naming conventions.**
2. **Every package needs an `__init__.py` for imports to work.**
3. **Python 3.14 requires updated import rules (`--import-mode=importlib`).**
4. **Fixtures live in `conftest.py` and must be named correctly.**
5. **Your test file, class, and method must follow Pytest naming rules.**
6. **Building a framework requires step‑by‑step validation.**

---

# Current Status

✔ Framework loads
✔ Tests discovered
✔ Selenium fixture working
✔ First test passed successfully

We are now ready to move into implementing real UI automation logic.

---

