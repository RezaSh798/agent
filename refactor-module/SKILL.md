---
name: refactor-module
description: Pragmatic, safe, and maintainable refactoring for Node.js modules without introducing breaking changes or over-engineering.
publish: true
metadata:
  author: kilo-assistant
  version: "1.0.0"
---

# Pragmatic Node.js Module Refactoring Skill

This skill guides the AI coding agent to perform safe, maintainable, and pragmatic refactoring of Node.js modules (JavaScript or TypeScript) without introducing breaking changes or over-engineering.

---

## 1. Trigger & Target

- **Trigger:** The user invokes this skill and supplies a relative or absolute file path to a Node.js module (`.js`, `.cjs`, `.mjs`, or `.ts`).
- **Target Analysis:**
  1. Resolve the target file path to its full absolute path.
  2. Read the target file thoroughly to understand its context, exported symbols, public contract, and internal mechanisms.
  3. Identify callers or dependents if necessary to verify exported interfaces.
  4. Formulate a pragmatic refactoring plan before modifying the file.

---

## 2. Core Refactoring Directives (Pragmatic & High-ROI)

1. **JSDoc Annotation:**
   - Add concise, meaningful JSDoc blocks for all exported methods/classes, major internal helper methods, parameters (with explicit types), and return types.
   - Example:
     ```javascript
     /**
      * Fetches configuration by key with fallback to defaults.
      * @param {string} configKey - Unique configuration identifier.
      * @param {object} [options={}] - Optional fetch parameters.
      * @returns {Promise<object>} Resolved configuration entity.
      */
     ```

2. **Extract Method & SRP (Single Responsibility Principle):**
   - Break down monolithic or overly long functions (> 25-30 lines) into focused, single-purpose helper functions.
   - Keep internal helper functions focused on a single sub-task (e.g., validation, payload transformation, query construction).

3. **Descriptive & Precise Naming:**
   - Rename cryptic, single-letter (e.g., `x`, `d`, `tmp`), or misleading variables and functions to convey clear business/domain intent.
   - Use clear verb-noun patterns for functions (e.g., `validatePayload` instead of `check`).

4. **Guard Clauses & Early Returns:**
   - Eliminate deeply nested `if/else` ladders by returning or throwing early on edge/invalid cases.
   - Keep the primary "happy path" flat and prominent.

5. **No Magic Values:**
   - Extract magic strings and magic numbers into module-level `const` declarations.
   - Use `SCREAMING_SNAKE_CASE` or freeze configuration objects with `Object.freeze()`.
   - Place constants near the top of the file after imports.

6. **Async/Await & Error Hygiene:**
   - Replace awkward `.then().catch()` chains with clean `async/await`.
   - Avoid empty catch blocks or silent swallows.
   - Wrap contextual information around thrown errors:
     ```javascript
     throw new Error(`Failed to [action]: ${err.message}`);
     ```

7. **Parameter Object Pattern:**
   - If a function accepts 3 or more arguments, refactor it to accept a destructured options object with sensible defaults where applicable.
   - *Crucial:* For public/exported functions, preserve backward compatibility with existing positional argument callers (e.g., inspect `typeof` or arguments length) or apply this pattern to internal functions.

8. **Modern Idiomatic JavaScript:**
   - Use Optional Chaining (`?.`) and Nullish Coalescing (`??`) to simplify null/undefined checks.
   - Use declarative array methods (`map`, `filter`, `reduce`, `some`, `every`) where appropriate over imperative loops.
   - Eliminate `var` completely in favor of `const` (preferred) and `let`.

9. **Avoid Unnecessary Mutations:**
   - Prefer non-mutating transformations (e.g., object spread `{ ...obj }`, array spread `[...arr]`) over direct in-place mutation of input arguments.

---

## 3. Strict Guardrails (Golden Rules)

- **Zero Breaking Changes:**
  - Never break public interfaces, exported functions, method signatures intended for external callers, or expected return structures.
  - Ensure compatibility with existing test suites and consumers.
- **No Over-Engineering:**
  - Do not introduce heavy design patterns, unnecessary abstractions, external libraries, or full architectural rewrites.
  - Focus solely on clean, readable, robust code within the target file.
- **Preserve Existing Logic:**
  - Do not invert logic, drop edge-case validations, or alter business rules.
  - Preserve intended side effects.

---

## 4. Execution Workflow & Output Format

1. **Read & Understand:** Read the entire file content using the file reading tool. Determine module system (`CommonJS` vs. `ESM`) and public exports.
2. **Plan Refactoring:** Identify candidates for method extraction, magic values, nested conditionals, error handling hygiene, and JSDoc additions.
3. **Apply Changes:** Apply the refactored code cleanly to the file (or show the refactored code cleanly if dry-run mode is requested).
4. **Report Summary:** Provide a brief, bulleted Changelog:
   - **Methods Extracted:** List new helper functions created and their responsibilities.
   - **Structural & Readability Improvements:** Detail guard clauses, constants extracted, async/await upgrades, and naming improvements.
   - **Warnings & Observations:** Highlight any potential pre-existing bugs, edge cases, or follow-up recommendations observed during refactoring.
