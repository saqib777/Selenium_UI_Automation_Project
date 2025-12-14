## UI Automation Project – Notes & Development Journal

### 1. Why This File Exists

This file is intentionally created as a **single source of truth** for the UI Automation project. It combines notes, a learning journal, and technical documentation into one place. The idea is simple: instead of only showing the final working automation code, this file captures *how the project actually evolved*.

In real automation work, things rarely work on the first attempt. Errors, confusion, broken runs, and re-structuring are all part of the job. This document records those realities clearly and honestly.

This file is meant for:

* My future self, when I revisit this project
* Interviewers who want to understand my thought process
* Anyone reviewing the repository to see real learning, not just polished output

---

### 2. Project Goal and Scope

The main goal of this project is to build a **practical UI automation framework** using Python, following patterns that are actually used in industry-level SDET roles.

The scope of this project includes:

* Creating a clean and scalable project structure
* Understanding how UI tests are discovered and executed
* Handling Python-specific and automation-specific errors
* Learning how automation tools behave under the hood
* Gradually layering complexity instead of starting big

This project is intentionally built step by step rather than copying a full-fledged framework from day one.

---

### 3. Initial Setup and First Decisions

The first step was creating a fresh project folder dedicated entirely to UI automation. At this stage, the priority was **clarity**, not completeness.

Key decisions made early:

* Python chosen for automation due to its simplicity and strong ecosystem
* pytest chosen as the test runner because it is widely used and beginner-friendly
* Minimal files created initially to avoid confusion

Early structure looked something like this:

```
Ui_Automation_Project/
│
├── tests/
│   └── test_sample.py
│
├── requirements.txt
└── README.md
```

At this point, the objective was very clear: get *one test* to run successfully.

---

### 4. Understanding the Role of Empty Files

One of the first doubts was whether newly created files needed to contain code immediately.

Important realization:

* Not all files are supposed to have code right away
* Some files exist to define structure
* Automation frameworks grow over time

This helped reinforce a key automation principle:

> Structure comes first, behavior comes later.

Empty or minimal files are normal and expected in early-stage frameworks.

---

### 5. The `__pycache__` Folder Explained

After running tests, a folder named `__pycache__` appeared automatically.

Initial confusion:

* The folder was not manually created
* It appeared without any direct action
* It showed up inside project directories

Clarification gained:

* Python automatically creates `__pycache__`
* It stores compiled bytecode files
* This improves execution speed
* It should not be committed to version control

This was an important learning moment because it introduced the idea that **tools create artifacts automatically**, and not everything seen in the project folder is developer-written code.

---

### 6. Test Execution Issues and Debugging Journey

A significant portion of this project involved debugging issues before even writing real automation logic.

#### 6.1 Tests Not Getting Detected

Problem faced:

* Running pytest resulted in messages like no tests found
* Test file existed but was ignored

Root cause identified:

* pytest follows strict naming conventions
* Files must start with `test_`
* Test functions must also start with `test_`

Resolution:

* Renamed test files correctly
* Renamed test methods accordingly

Learning:

* Automation tools do not guess intent
* Naming conventions are mandatory, not optional

---

#### 6.2 Import and Path Errors

Problem faced:

* Python failed to locate modules
* Tests worked in one directory but failed in another

Root cause:

* Tests were executed from the wrong location
* Python path resolution caused confusion

Resolution:

* Always ran tests from the project root
* Avoided unnecessary imports during early stages

Learning:

* Execution context matters
* Simple structure reduces early errors

---

#### 6.3 Dependency and Environment Issues

Problem faced:

* Missing libraries caused runtime failures
* Some commands worked globally but not inside the project

Root cause:

* Dependencies were not clearly defined
* Environment setup was incomplete

Resolution:

* Installed required packages explicitly
* Tracked them using `requirements.txt`

Learning:

* Dependency management is part of automation responsibility
* Reproducibility matters

---

### 7. Achieving the First Successful Test Run

After resolving multiple issues related to naming, paths, and dependencies, the first clean test execution was achieved.

Why this mattered:

* Confirmed that the project structure was valid
* Verified that pytest was configured correctly
* Proved that tests could be discovered and executed

This moment marked a clear milestone in the project and was intentionally paused to document rather than rushing forward.

---

### 8. Repository Creation and Version Control Strategy

Once the project reached a stable point, a GitHub repository was created.

Repository name:
**Ui_Automation_Project**

Version control approach:

* Commit only essential files
* Avoid committing generated files like `__pycache__`
* Keep commits meaningful and clean

This step was important to transition the project from a local experiment into a professional artifact.

---

### 9. Why This Documentation Matters

Most repositories only show final code. This project intentionally shows the journey.

This document demonstrates:

* Problem-solving ability
* Debugging mindset
* Understanding of automation fundamentals
* Willingness to document and reflect

For interview scenarios, this file helps explain *how* and *why* decisions were made, not just *what* was built.

---

### 10. Planned Future Enhancements (Living Section)

This document will continue to evolve alongside the project.

Future topics to be documented here include:

* Browser initialization and teardown
* Page Object Model implementation
* Locator strategy decisions
* Test data management
* Reporting and screenshots
* CI/CD pipeline integration

Each addition will be recorded in this same file to maintain continuity.

---

### 11. Closing Reflection

This UI Automation project is not meant to be perfect. It is meant to be **real**.

Every failure encountered and fixed contributes directly to stronger automation skills. This journal stands as proof of that growth.

