Register Page – Automation Documentation
Purpose

The Register Page in the ParaBank application allows a new user to create an account by entering personal, address, and login details.
This page is automated to validate that new users can successfully register and that the registration workflow behaves as expected.

Why This Page Exists in the Project

In a real banking workflow, registration is the entry point for new users.
Automating this page ensures:

New users can create accounts without errors

Mandatory fields are validated

Successful registration redirects the user correctly

The system is stable for first-time user onboarding

This page is implemented using the Page Object Model (POM) to keep tests clean and reusable.

Key Actions Covered

The automation for the Register Page focuses on the following actions:

Navigating to the registration screen

Filling personal details (name, address, phone, SSN)

Creating login credentials

Submitting the registration form

Verifying successful account creation

Each action is abstracted into methods so tests do not directly interact with Selenium locators.

Valid Registration Scenario

A valid registration test follows this flow:

User opens the ParaBank homepage

User clicks on the Register link

User fills all required fields with valid data

User submits the form

System confirms successful account creation

The test asserts that a success message or welcome text is displayed.

Negative Scenarios (Future Scope)

The following scenarios are planned for future enhancement:

Missing mandatory fields

Invalid username formats

Password mismatch

Duplicate username registration

Server-side validation errors

These cases are intentionally kept out of the first version to maintain stability and focus.

Design Decisions

Page follows Single Responsibility Principle

No assertions inside the page class

Explicit waits are used instead of hard sleeps

Locators are centralized for maintainability

This makes the page scalable as more tests are added.

Files Related to Registration

pages/register_page.py – Page Object implementation

tests/test_register.py – Registration test cases

Pages/register_pages.md – Documentation (this file)

Current Status

Basic registration flow automated

Integrated with test framework

Stable for demo and portfolio usage

Next Improvements

Data-driven registration tests

Negative validation scenarios

Screenshot capture on failure

Registration cleanup logic (optional)
