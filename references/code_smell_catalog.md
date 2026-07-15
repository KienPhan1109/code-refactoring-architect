# Code Smell Reference Catalog

This reference provides a comprehensive catalog of common code smells organized by category, with detection heuristics and recommended refactoring techniques.

---

## 1. Bloaters — Code That Has Grown Too Large

| Smell | Detection Heuristic | Refactoring Technique |
|---|---|---|
| **Long Method** | Function > 20 lines or cyclomatic complexity > 10 | Extract Method, Decompose Conditional |
| **Large Class** | Class > 200 lines or > 5 responsibilities | Extract Class, Extract Interface |
| **Long Parameter List** | Function > 3 parameters | Introduce Parameter Object, Builder Pattern |
| **Primitive Obsession** | Using primitives instead of small objects (e.g., string for email) | Replace Primitive with Value Object |
| **Data Clumps** | Same group of variables appears together in 3+ places | Extract Class, Introduce Parameter Object |

---

## 2. Object-Orientation Abusers

| Smell | Detection Heuristic | Refactoring Technique |
|---|---|---|
| **Switch Statements** | Repeated switch/if-else on same type discriminator | Replace Conditional with Polymorphism, Strategy Pattern |
| **Refused Bequest** | Subclass uses < 50% of parent's interface | Replace Inheritance with Delegation |
| **Temporary Field** | Fields set only in certain circumstances | Extract Class, Introduce Null Object |
| **Alternative Classes** | Two classes with same interface but different names | Rename/Merge, Extract Superclass |

---

## 3. Change Preventers

| Smell | Detection Heuristic | Refactoring Technique |
|---|---|---|
| **Divergent Change** | One class modified for multiple unrelated reasons | Extract Class (SRP) |
| **Shotgun Surgery** | One change requires editing many classes | Move Method, Inline Class |
| **Parallel Inheritance** | Creating subclass in one hierarchy forces subclass in another | Move Method, Collapse Hierarchy |

---

## 4. Dispensables — Unnecessary Code

| Smell | Detection Heuristic | Refactoring Technique |
|---|---|---|
| **Dead Code** | Unreachable branches, unused variables/imports | Remove Dead Code |
| **Speculative Generality** | Abstract classes/interfaces with single implementation | Collapse Hierarchy, Remove Unused |
| **Duplicate Code** | Similar code blocks in 2+ locations | Extract Method, Pull Up Method |
| **Comments (Excessive)** | Comments explaining "what" instead of "why" | Rename to Self-Document, Extract Method |
| **Lazy Class** | Class that does too little to justify existence | Inline Class |

---

## 5. Couplers — Excessive Dependencies

| Smell | Detection Heuristic | Refactoring Technique |
|---|---|---|
| **Feature Envy** | Method uses another class's data more than its own | Move Method |
| **Inappropriate Intimacy** | Two classes access each other's private members | Move Method, Extract Class |
| **Message Chains** | `a.getB().getC().getD()` chains | Hide Delegate, Extract Method |
| **Middle Man** | Class that only delegates to another class | Remove Middle Man, Inline Method |

---

## 6. Performance Anti-Patterns

| Pattern | Problem | Solution |
|---|---|---|
| **N+1 Query** | Loop issues individual queries | Batch query, eager loading |
| **Nested Loop Lookup** | O(n²) when O(n) is possible | Use HashMap/Set for lookups |
| **String Concatenation in Loop** | O(n²) string building | Use StringBuilder / join() |
| **Unnecessary Re-renders** | React component re-renders on every parent render | React.memo, useMemo, useCallback |
| **Synchronous I/O in Hot Path** | Blocking call in performance-critical path | Async/await, worker threads |
| **Memory Leak** | Event listeners / subscriptions not cleaned up | Cleanup in useEffect return / destructor |

---

## 7. Severity Classification

Use this classification when reporting issues in Step 1 (Diagnosis):

| Level | Icon | Criteria | Action |
|---|---|---|---|
| **Critical** | 🔴 | Security risk, data corruption, crash potential | Must address |
| **Major** | 🟠 | Performance degradation, missing error handling, architectural violation | Should address |
| **Minor** | 🟡 | Naming issues, magic numbers, dead code, minor DRY violations | Address if time permits |
| **Style** | 🔵 | Formatting, idiomatic patterns, micro-optimizations | Optional polish |
