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

## DATE: 15-12-2025

This document captures all the errors we faced today during Day 3 of the Selenium UI Automation journey, along with the exact reason each error occurred and how we fixed it. This is intentionally written in plain language, focusing on understanding rather than theory.

---

ERROR 1: Test failed even though code ran successfully

What we saw:
The test executed, browser opened, but the assertion failed saying login was not successful.

Why it happened:
At this stage, the Page Object methods (enter_username, enter_password, click_login) still contained only `pass`. That meant Selenium was not performing any real action even though the test looked correct.

Fix:
We started implementing Page Object methods one by one instead of all at once. This helped us understand exactly which user action was missing.

Learning:
A test running does not mean a test is doing anything. Page Objects must contain real Selenium interactions for assertions to make sense.

---

ERROR 2: Assertion failed – "Accounts Overview not found"

What we saw:
AssertionError stating that Accounts Overview text was not found on the page.

Why it happened:
The login never actually completed because only username was implemented initially. Password entry and login click were still missing.

Fix:
We implemented enter_password using the correct locator and reran the test.

Learning:
Incremental implementation is the right approach. Each failure tells you which step is still incomplete.

---

ERROR 3: Login button click caused TimeoutException

What we saw:
TimeoutException while waiting for the login button to be clickable using XPath.

Why it happened:
The locator used for the login button was brittle. Selenium kept waiting because the element was either not clickable yet or slightly different in the DOM.

Fix:
We stopped relying on clicking the login button and instead submitted the form directly using:
`driver.find_element(By.NAME, "username").submit()`

Learning:
In real-world automation, form submission is often more stable than clicking buttons. Avoid fragile locators when a simpler interaction exists.

---

ERROR 4: TimeoutException when checking successful login

What we saw:
TimeoutException while waiting for either page text or URL change after login.

Why it happened:
The success condition we were waiting for was either incorrect or too strict. UI text is not always reliable and can vary.

Fix:
We refined the success check and aligned it with a stable post-login behavior (page load and successful navigation).

Learning:
Success conditions should be based on stable application behavior (URL change, page state), not cosmetic UI text.

---

ERROR 5: Duplicate method definitions inside Page Object

What we saw:
Login behavior was inconsistent even after implementing methods correctly.

Why it happened:
The same method (click_login) was defined twice in the Page Object. Python silently overrides earlier definitions, leading to confusion.

Fix:
We cleaned up the Page Object to ensure every method exists exactly once.

Learning:
Python will not warn you about duplicate method definitions. Clean, intentional code structure matters in automation frameworks.

---

FINAL RESULT

After fixing all the above issues:

* Login flow executed fully
* Form submission worked reliably
* Explicit waits behaved as expected
* Assertion passed
* Test result showed PASSED

This confirms that the framework, Page Object Model, and test design are now working correctly.

---

KEY TAKEAWAYS FROM DAY 3

1. Selenium automation is not about writing long scripts every time. It is about building reusable behavior.
2. Page Objects are written once and reused across many tests.
3. Failures are guidance, not setbacks.
4. Stable locators and stable success conditions matter more than fancy assertions.
5. Incremental development prevents hidden bugs and confusion.

---
