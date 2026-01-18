# Debugging Journey - Selenium UI Automation Project

This document captures all the major issues, errors, and bugs faced during the development of the ParaBank Selenium UI Automation project, along with their root causes and the exact fixes applied. This serves as a practical debugging reference and a learning log.

---

## 1. `ModuleNotFoundError: No module named 'pages'`

**Where it occurred:**

* While running tests from the `tests/` directory

**Root cause:**

* Python could not resolve project-level imports because the project root was not in `sys.path`.

**Fix applied:**

* Added project root to Python path in `conftest.py`.

**Final fix snippet:**

```python
import sys, os
sys.path.append(os.path.abspath(os.path.dirname(__file__)))
```

---

## 2. `NameError: name 'LoginPage' is not defined`

**Where it occurred:**

* Inside `test_login.py`

**Root cause:**

* `LoginPage` class was used without importing it.

**Fix applied:**

* Explicitly imported the page class at the top of the test file.

**Final fix:**

```python
from pages.login_page import LoginPage
```

---

## 3. Duplicate Method Definitions Overwriting Each Other

**Where it occurred:**

* `login_page.py`

**Root cause:**

* Same method (`get_login_error_message`) was defined twice.
* Python silently overwrote the first definition.

**Fix applied:**

* Removed the duplicate method.
* Kept only the version using `WebDriverWait`.

---

## 4. `SyntaxError: 'return' outside function`

**Where it occurred:**

* `login_page.py`

**Root cause:**

* Incorrect indentation placed `return` outside method scope.

**Fix applied:**

* Fixed indentation so `return` stayed inside the function block.

---

## 5. `TimeoutException` While Waiting for Elements

**Where it occurred:**

* Login success and Accounts Overview checks

**Root cause:**

* Page was slow to load.
* Element locator was correct but appeared late.

**Fix applied:**

* Replaced direct `find_element` calls with `WebDriverWait` + Expected Conditions.

**Example fix:**

```python
WebDriverWait(driver, 10).until(
    EC.presence_of_element_located((By.XPATH, "//h1[contains(text(),'Accounts Overview')]"))
)
```

---

## 6. Assertion Failing Due to Wrong Error Message

**Where it occurred:**

* Invalid login test

**Root cause:**

* Application returned a different message:

  * `"An internal error has occurred and has been logged."`
    instead of
  * `"could not be verified"`

**Fix applied:**

* Updated assertion to match the actual UI message.

---

## 7. Tests Passing Individually but Failing Together

**Where it occurred:**

* When running full pytest suite

**Root cause:**

* Browser state was shared between tests.

**Fix applied:**

* Used pytest fixtures to create a fresh browser per test.

---

## 8. Hardcoded Locators Spread Across Methods

**Problem:**

* Locators repeated in multiple methods

**Fix applied:**

* Centralized locators as class-level constants inside Page Objects.

---

## 9. Flaky Click Actions on Login Button

**Root cause:**

* Button not clickable immediately

**Fix applied:**

* Used `element_to_be_clickable` before clicking.

---

## 10. Test Structure Becoming Too Verbose

**Problem:**

* Tests repeated login steps

**Fix applied:**

* Introduced `login_as(username, password)` method in `LoginPage`.

---

## 11. Pytest Collecting Zero Tests

**Root cause:**

* Test methods did not start with `test_`

**Fix applied:**

* Renamed methods to follow pytest naming conventions.

---

## 12. Incorrect XPath / CSS Selectors

**Root cause:**

* Dynamic DOM changes

**Fix applied:**

* Used resilient locators:

  * `contains(text())`
  * partial attribute selectors

---

## Final Outcome

By systematically debugging each failure and understanding the root cause, this project evolved into:

* A stable Page Object Model framework
* Reliable pytest execution
* Clear separation of tests and UI logic
* Strong real-world debugging experience

This document reflects real automation challenges and their solutions — exactly what recruiters look for.
