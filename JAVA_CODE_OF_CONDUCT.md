# Java Code of Conduct

**Author:** Jorge Morla  
**Purpose:**  
This document defines the principles, constraints, and tactical rules guiding Java software development within Jorge Morla’s engineering philosophy.  
It complements the *Software Design Philosophy* and enforces disciplined, predictable, and maintainable coding practices.  

This is **not** a Java style guide.  
This is a set of **behavioral rules** that ensure correctness, robustness, and design clarity.

---

## 1. General Principles

1. Always prioritize **clarity and correctness** over cleverness.  
2. Code must **reveal intent**, not implementation details.  
3. Follow **Tactical Programming** — each decision must bring the design closer to robustness and simplicity.  
4. Write **deep modules** — encapsulate complexity and expose minimal, powerful interfaces.  
5. **Pull complexity downward** — simplify the user experience of each component.  
6. **Design twice**: think, plan, then code. Review design before implementation.  
7. Every module must be **general-purpose** unless it directly conflicts with domain constraints.  
8. **Define errors out of existence** whenever possible — avoid exposing failure paths that can be internally managed.  

---

## 2. Exception and Error Handling

1. **Never catch or throw** the base types `Exception` or `Error`.  
2. Always handle the **closest, most specific subclass** of `Throwable` required by context.  
3. System design must **avoid exposing exceptions unnecessarily**.  
   - Ask: *“Does the user of this module need to know this failed?”*  
   - If not, handle it internally.  
4. Favor **checked exceptions** only when the user can realistically recover.  
5. Use **unchecked exceptions** for unrecoverable logic errors.  
6. **Never swallow exceptions silently**. Always log or rethrow appropriately.  
7. **Never rely on exceptions for control flow.**

---

## 3. Resource Management

1. Always use **try-with-resources** when possible.  
2. Be aware of **resource leakage** — never assume GC will handle it.  
3. If automatic management isn’t available, **close the resource manually** in a `finally` block.  
4. Resources include: streams, connections, readers, writers, channels, and frameworks that manage handles or sessions.  
5. Never allow a method to return a resource that another component must close unless explicitly documented.

---

## 4. Documentation (Javadoc)

1. Every **public class, interface, and method** must include Javadoc.  
2. Javadoc must describe **what** the component does and, when necessary, **why** — but **never how**.  
3. Include examples only when absolutely required for clarity.  
4. Avoid documenting trivial code (e.g., getters and setters) unless behavior deviates from standard expectations.  
5. Keep descriptions short, direct, and aligned with intent.  
6. Example:

   ```java
   /**
    * Calculates the moving average of a list of values.
    *
    * @param values list of numeric data points
    * @return the computed moving average
    * @throws IllegalArgumentException if values is null or empty
    */
   double calculateAverage(List<Double> values);
   ```

---

## 5. Inline Comments

1. Use inline comments **only** when the logic is complex, requires context, or could confuse a reader unfamiliar with the domain.  
2. Comments must explain **intent**, not rephrase the code.  
3. When helpful, organize logic using structural sections:
   ```java
   // Given
   var user = new User("Alice");

   // When
   var result = service.register(user);

   // Then
   assertTrue(result.isSuccessful());
   ```
4. Do not over-comment — **simplicity is the winner**.  
5. Avoid decorative or redundant comments such as:
   ```java
   // Increment counter by one
   counter++;
   ```

---

## 6. Test-Driven Development (TDD)

1. Always begin by writing a **failing test** before implementing any logic.  
2. Follow the **Red → Green → Refactor** cycle strictly.  
3. Exclude **plain POJOs** (only getters/setters) from TDD unless they include validation or logic.  
4. Test names must start with `should...` and express expected behavior. Example:

   ```java
   @Test
   void shouldRegisterUserWhenEmailIsValid() {
       // Given
       var email = "test@example.com";

       // When
       var result = userService.register(email);

       // Then
       assertTrue(result.isSuccessful());
   }
   ```

5. Separate code sections with comments to increase readability:
   ```java
   // Given
   // When
   // Then / Assert
   ```
6. Prefer **unit tests first**; integration tests may follow later.  
7. Tests must cover both **expected and edge cases**.  
8. Always apply TDD — **no feature exists until a test proves it does.**

---

## 7. Architecture and Design

1. Each module must **hide internal mechanisms** and expose only what is necessary.  
2. **Avoid information leakage** — internal states or dependencies must remain private.  
3. Strive for **deep modules**: the interface should be simple, while the implementation manages the complexity.  
4. Use **composition over inheritance** unless a shared contract justifies it.  
5. Avoid using the `DTO` suffix; choose **descriptive names** that reflect purpose (e.g., `InvoiceSummary`, not `InvoiceDTO`).  
6. **Service classes** are business orchestrators — they coordinate, not execute, core logic.  
7. Before restructuring or refactoring a public interface, **inform the developer** responsible.  
8. Always **design twice** — plan, review, and validate before writing code.  
9. Adopt the **newest stable Java features** (records, sealed classes, pattern matching, etc.) when beneficial and supported.  

---

## 8. Tooling and Practices

1. Static analysis tools (e.g., Checkstyle, PMD, SonarLint) must be integrated into the workflow.  
2. Notify developers before enforcing or modifying tool rules.  
3. One-liners are acceptable **only if they remain clear and expressive**.  
4. Code formatting is **delegated to the configured formatter** — do not enforce style manually.  
5. All builds must be **warning-free**.  
6. Manual **code reviews** must validate compliance with this Code of Conduct.  
7. Documented issues should propose **constructive, actionable feedback** — never just point out failure.  

---

## 9. Developer Oath

By following this Code of Conduct, every contributor agrees to:

- Think twice before coding.  
- Pull complexity **downward**, not upward.  
- Respect module boundaries — make them **deep and simple**.  
- Never expose unnecessary details or exceptions.  
- Always start by writing a test.  
- Write code that is **intentional, readable, and maintainable**.  
- Favor **clarity and robustness** over optimization.  
- Keep interfaces clean and cohesive.  
- Treat simplicity as the ultimate sophistication.

Each line of code should serve one goal:  
> **To build software that is robust by design, self-explanatory by nature, and reliable by proof.**

---

## 10. Validation Checklist

Before committing code, verify the following:

- [ ] Did you start with a failing test?  
- [ ] Does your module expose only what’s essential?  
- [ ] Are exceptions specific and properly handled?  
- [ ] Are all resources properly closed?  
- [ ] Do public elements include accurate Javadocs?  
- [ ] Are inline comments meaningful and minimal?  
- [ ] Does your design avoid leaking internal data or errors?  
- [ ] Does your implementation make other code simpler?  
- [ ] Have you used relevant modern Java features responsibly?  
- [ ] Did you design twice — and review before coding?

---

**End of Document**
