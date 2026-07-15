# Code Refactoring Architect — Usage Examples

## Example 1: TypeScript — Optimizing Array Lookups

### User Input
```
- Language/Framework: TypeScript / React
- Target Focus: Performance optimization
- Source Code:
```

```typescript
function findCommonUsers(listA: any[], listB: any[]) {
  const result = [];
  for (let i = 0; i < listA.length; i++) {
    for (let j = 0; j < listB.length; j++) {
      if (listA[i].id == listB[j].id) {
        result.push(listA[i]);
      }
    }
  }
  return result;
}
```

### Expected Agent Output (Abbreviated)

**Step 1 — Diagnosis:**
- 🟠 Major: O(n×m) nested loop for lookup — should use Set/Map for O(n+m)
- 🟡 Minor: `any[]` type — no type safety
- 🟡 Minor: Loose equality `==` instead of strict `===`
- 🔵 Style: Manual `for` loop instead of functional methods

**Step 3 — Refactored Code:**

```typescript
interface User {
  readonly id: string;
  readonly name: string;
}

// REFACTOR: Performance — O(n+m) via Set lookup instead of O(n×m) nested loop
function findCommonUsers(listA: readonly User[], listB: readonly User[]): User[] {
  if (!listA.length || !listB.length) return [];

  const idSetB = new Set(listB.map((user) => user.id));
  return listA.filter((user) => idSetB.has(user.id));
}
```

---

## Example 2: Python — Removing Code Duplication

### User Input
```
- Language/Framework: Python 3.11
- Target Focus: Clean Code / DRY
- Source Code:
```

```python
def get_active_users(users):
    result = []
    for user in users:
        if user['status'] == 'active':
            result.append({
                'name': user['name'],
                'email': user['email'],
                'role': user['role']
            })
    return result

def get_admin_users(users):
    result = []
    for user in users:
        if user['role'] == 'admin':
            result.append({
                'name': user['name'],
                'email': user['email'],
                'role': user['role']
            })
    return result
```

### Expected Agent Output (Abbreviated)

**Step 1 — Diagnosis:**
- 🟠 Major: DRY violation — two functions with 90% identical logic
- 🟡 Minor: No type hints
- 🟡 Minor: Manual loop instead of list comprehension
- 🔵 Style: Using dict instead of dataclass

**Step 3 — Refactored Code:**

```python
from dataclasses import dataclass
from typing import Callable, Sequence

@dataclass(frozen=True)
class UserInfo:
    name: str
    email: str
    role: str

# REFACTOR: DRY — Single generic filter function replaces two near-identical functions
def filter_users(
    users: Sequence[dict], predicate: Callable[[dict], bool]
) -> list[UserInfo]:
    return [
        UserInfo(name=u["name"], email=u["email"], role=u["role"])
        for u in users
        if predicate(u)
    ]

def get_active_users(users: Sequence[dict]) -> list[UserInfo]:
    return filter_users(users, lambda u: u.get("status") == "active")

def get_admin_users(users: Sequence[dict]) -> list[UserInfo]:
    return filter_users(users, lambda u: u.get("role") == "admin")
```

---

## Example 3: React — Component Refactoring

### User Input
```
- Language/Framework: TypeScript / React Native
- Target Focus: General Clean Code
- Source Code: [Large component with mixed concerns]
```

### Key Patterns to Apply
1. Extract custom hooks for stateful logic (`useUserData`, `useFormValidation`)
2. Separate container and presentational components
3. Memoize expensive computations with `useMemo`
4. Replace inline styles with StyleSheet
5. Add proper TypeScript interfaces for all props
