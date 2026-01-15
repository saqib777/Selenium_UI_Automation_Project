## Base Test Layer – Framework Foundation

### Purpose

The Base Test layer provides the common setup and teardown logic required by all test cases in this Selenium UI Automation project. Its responsibility is to ensure that every test starts with a ready browser session and ends with a clean shutdown.

This keeps test files focused on validation logic and avoids duplication.

---

### What the Base Layer Controls

The base layer handles:

* WebDriver initialization
* Browser configuration
* Application launch
* Test teardown and cleanup
* Shared fixtures used across all tests

All test cases depend on this layer implicitly.

---

### Why a Base Layer Is Important

Without a base layer:

* Each test would need to create and close a browser manually
* Browser configuration would be duplicated
* Maintenance would become difficult as the project grows

By centralizing this logic, the framework becomes scalable, readable, and professional.

---

### How It Works in This Project

* The base setup is implemented using Pytest fixtures
* The fixture creates a browser instance before a test starts
* The same instance is reused inside a test
* After the test finishes, the browser is closed automatically

This ensures consistency across all test executions.

---

### Key Responsibilities Explained

**Browser Initialization**

The WebDriver is created with standard settings such as browser selection and window configuration.

**Application Launch**

The ParaBank application URL is loaded before test execution begins.

**Test Isolation**

Each test starts with a fresh browser session, avoiding side effects from previous tests.

**Graceful Cleanup**

The browser is closed even if a test fails, preventing resource leaks.

---

### Files That Use the Base Layer

All test files rely on this base configuration:

* test_login.py
* test_register.py
* test_accounts.py
* test_bill_pay.py

None of these tests directly create or destroy the browser.

---

### Design Principles Followed

* Single Responsibility Principle
* DRY (Don’t Repeat Yourself)
* Clean separation between setup and test logic
* Pytest-native fixture usage

---

### Current Status

* Base setup implemented
* Integrated with all test modules
* Stable for local execution

---

### Future Enhancements

* Browser selection via configuration
* Headless execution support
* Environment-based URL handling
* Screenshot capture on test failure

---

### Summary

The Base Test layer is the backbone of the automation framework. It ensures reliability, consistency, and maintainability across the entire project.

