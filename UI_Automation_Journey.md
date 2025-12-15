<div align="center">
  
  #UI Automation Journal

</div>

### A Running Record of Learning, Errors, and Growth

---

### How to Read This Journal

This is a **living journal**, not a one-time diary entry.

New workdays will be added **at the top**, so the most recent progress is always visible first. Older entries stay below to preserve context and growth over time.

This journal is intentionally written in a reflective but professional tone. It captures:

* What was worked on each day
* What went wrong and why
* What finally worked
* How my understanding evolved

This is meant to show *process*, not perfection.

---

## Day 4 – Technical Clarity and First Real Framework Thinking

Today felt different from the previous days. The confusion was still there, but it was no longer overwhelming. Instead of reacting to errors emotionally, I started looking at them **structurally**.

This was the day I stopped treating Selenium as a magic testing tool and started seeing it for what it actually is.

Selenium does not test.
Selenium does not validate.
Selenium does not decide pass or fail.

**Selenium only drives the browser.**

That one realization changed everything.

Once this clicked, a lot of earlier frustration finally made sense. I had been subconsciously expecting Selenium to behave like Katalon, where recording, validation, execution, and reporting all feel like part of one application. Selenium is not an application. It is a library.

The real framework is something I am building *around* Selenium.

### Technical Understanding Gained Today

I clearly separated the responsibilities in my head for the first time:

* **Selenium**: interacts with the browser (click, type, navigate, wait)
* **pytest**: discovers tests, runs them, manages failures, and reports results
* **Test code**: contains assertions, logic, flow, and intent

Earlier, all of this felt like one tangled system. Today, it started to feel layered.

Another important realization was about control.

In Katalon:

* The tool decides structure
* The UI guides execution
* The framework is mostly hidden

In Selenium:

* I decide structure
* Code controls execution
* Nothing is hidden

This explains why Selenium feels harder. It is not harder because it is poorly designed. It is harder because it gives **full control**, and full control demands responsibility.

### pytest as the Backbone

Today I also gained more respect for pytest.

I realized that pytest is not "just a runner". It is the backbone that makes Selenium usable at scale. Without pytest (or a similar runner), Selenium scripts are just browser automation scripts, not tests.

Key ideas that started forming today:

* Tests must be discoverable, or they do not exist
* Assertions define success and failure, not browser actions
* Structure determines maintainability more than syntax

Even though I have not fully implemented fixtures or Page Object Model yet, I can now see **why they exist**, not just that they exist.

### Reflection for Day 4

Day 4 did not add more code, but it added depth.

This was the day Selenium stopped feeling hostile and started feeling honest.

It does not pretend to be easy.
It does not hide complexity.
It expects the engineer to think.

That expectation is intimidating, but it is also exactly what makes this worth learning.

---

## Day 3 – Stability Over Speed

Today was about slowing down and stabilizing the foundation instead of adding new automation features.

The focus shifted from “making Selenium do something” to **understanding how Selenium and pytest actually behave**. I deliberately avoided adding more files or logic and instead observed how existing pieces interacted.

Key things that became clearer today:

* Test discovery is entirely rule-based, not intelligent
* File names, function names, and execution location matter more than expected
* Python creates things like `__pycache__` automatically, and that is normal

The first consistent green test run happened today. It did not feel exciting, but it felt grounding. That green run marked the point where the project stopped feeling fragile and started feeling controlled.

This was also the day I consciously chose to **document before expanding**, knowing that early clarity is easy to lose once complexity increases.

---

## Day 2 – Friction and Self-Doubt

Day 2 was the hardest so far.

Tests existed but were not detected. Errors appeared without meaningful guidance. Fixes felt random until patterns slowly emerged. This was the day Selenium fully separated itself from Katalon in my mind.

Katalon feels like an application that guides you visually.
Selenium feels like a framework that expects discipline.

Most failures today came down to small but strict rules:

* Incorrect file naming
* Incorrect test method naming
* Running commands from the wrong directory

None of these were complex problems, but together they created frustration. This day challenged my confidence more than my technical ability.

---

## Day 1 – Familiar Confidence, Wrong Assumptions

Day 1 began with confidence built from prior experience using Katalon.

That confidence turned into incorrect assumptions. I subconsciously expected Selenium to behave like Katalon, forgetting that they solve the same problem in very different ways.

Katalon abstracts complexity.
Selenium exposes it.

What felt easy in Katalon felt manual and unforgiving in Selenium. At the time, this felt like difficulty. In hindsight, it was exposure to fundamentals.

Day 1 was less about progress and more about **unlearning expectations**.

---

## Perspective So Far

Katalon helped me understand *what* UI automation looks like.
Selenium is teaching me *how* UI automation works.

One tool made me comfortable quickly.
The other is making me precise slowly.

Both matter, but Selenium demands more responsibility.

---

## Progress Snapshot

Overall Understanding of UI Automation:

Day 1: ███░░░░░░░░ 30%
Day 2: █████░░░░░░ 50%
Day 3: ███████░░░░ 70%

---

*Next entries will be added above this line.*
