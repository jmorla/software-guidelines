# Software Design Philosophy

> “Design twice. Code once.”  
> A doctrine for tactical, modular, and test-driven software engineering.

---

## 1. Introduction

This document defines the software design philosophy that governs all code produced under Jorge’s direction.  
It is not a set of rules — it is a way of thinking.  
Every module, class, and test must reflect deliberate design, tactical precision, and disciplined execution.

---

## 2. Core Principles

### 2.1 Design Twice
Design is an act of thinking, not typing.  
The first design defines **what** the system should accomplish.  
The second design defines **how** it should be built to endure.  
No architecture is final until it has been implemented once, reflected upon, and redesigned.  
Design twice — the second time is where the truth emerges.

---

### 2.2 Avoid Information Leakage
A module should expose only its contract, never its construction.  
Its data, internal rules, and decisions must remain private.  
Information flows **downward through interfaces**, not sideways through shared state.  
When a module leaks information, it loses power and integrity.  
The external world should never depend on the internal shape of a module.

---

### 2.3 Make Modules Deep
A deep module provides **substantial functionality with minimal surface area**.  
Depth means complexity is internalized and controlled.  
Shallow modules — wrappers, helpers, pass-throughs — add friction without strength.  
Strive for interfaces that are simple to use but supported by dense, thoughtful machinery beneath.  
Depth is the mark of mastery.

---

### 2.4 Pull Complexity Downwards
Complexity must live where it can be contained.  
Expose clean, declarative interfaces at the top; bury the mechanical detail below.  
Upper layers should describe *what* happens.  
Lower layers should decide *how*.  
When complexity climbs upward, it multiplies; when pushed downward, it stabilizes.

---

### 2.5 Define Error Out of Existence
Errors should be prevented by design, not patched by code.  
Eliminate invalid states through strong typing and domain constraints.  
Use constructs that make mistakes impossible — `NonEmptyList`, `ValidatedInput`, `PositiveDecimal`.  
Where failure is inevitable, isolate it, name it, and make it predictable.  
A well-designed system has few exceptional paths because most errors never exist.

---

### 2.6 Always Use Tactical Programming
Code is a tactical act — every function must have a clear, measurable objective.  
Avoid “cleverness” and focus on **clarity, locality, and intention**.  
Each piece of code should be understandable in isolation, without global knowledge.  
Abstractions exist only to make tactics reusable, not to decorate them.  
Tactical programming means deliberate, efficient motion toward a defined goal.

---

## 3. Module Doctrine

### 3.1 General-Purpose Design
Modules are not scripts; they are **tools**.  
Each should make sense on its own, applicable beyond its immediate context.  
Hard dependencies are allowed only through explicit adapters.  
A good module can be moved, reused, or tested in isolation without loss of meaning.

---

### 3.2 Information Flow
The direction of knowledge is **top → down**, never **sideways**.  
A higher layer expresses *intent*; a lower layer executes *mechanics*.  
Interactions occur only through formal contracts — interfaces, DTOs, or adapters.  
No shared mutable state. No hidden dependencies.  
Information travels in one direction, clearly and predictably.

---

### 3.3 Comments and Clarity
Code must explain its reasoning.  
Each file begins with a header comment describing *what* it is and *why* it exists.  
Functions describe *intent*, *inputs*, and *assumptions*.  
Comments do not restate the code — they illuminate design choices.  

Example:
```java
/** 
* Calculates P&L by comparing realized and unrealized gains.
* Assumes trades are chronologically ordered and validated.
**/
BigDecimal calculatePnL(List<Trade> trades)
```
