# Kiến trúc sư Tối ưu hóa & Tái cấu trúc Mã nguồn — Ví dụ Sử dụng

## Ví dụ 1: TypeScript — Tối ưu hóa tìm kiếm trong Mảng (Array Lookups)

### Dữ liệu đầu vào từ Người dùng
```
- Ngôn ngữ/Framework: TypeScript / React
- Mục tiêu tập trung: Tối ưu hóa hiệu suất
- Mã nguồn:
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

### Kết quả đầu ra dự kiến từ Tác nhân (Rút gọn)

**Bước 1 — Chẩn đoán:**
- 🟠 Lớn: Vòng lặp lồng nhau O(n×m) để tìm kiếm — nên sử dụng Set/Map để tối ưu thành O(n+m)
- 🟡 Nhỏ: Sử dụng kiểu `any[]` — thiếu tính an toàn kiểu
- 🟡 Nhỏ: So sánh lỏng `==` thay vì so sánh nghiêm ngặt `===`
- 🔵 Phong cách: Sử dụng vòng lặp `for` thủ công thay vì các phương thức lập trình hàm (functional array methods)

**Bước 3 — Triển khai Tái cấu trúc:**

```typescript
interface User {
  readonly id: string;
  readonly name: string;
}

// REFACTOR: Performance — Tối ưu từ O(n×m) vòng lặp lồng nhau sang O(n+m) bằng cách tìm kiếm trên Set
function findCommonUsers(listA: readonly User[], listB: readonly User[]): User[] {
  if (!listA.length || !listB.length) return [];

  const idSetB = new Set(listB.map((user) => user.id));
  return listA.filter((user) => idSetB.has(user.id));
}
```

---

## Ví dụ 2: Python — Loại bỏ mã trùng lặp (Code Duplication)

### Dữ liệu đầu vào từ Người dùng
```
- Ngôn ngữ/Framework: Python 3.11
- Mục tiêu tập trung: Clean Code / DRY
- Mã nguồn:
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

### Kết quả đầu ra dự kiến từ Tác nhân (Rút gọn)

**Bước 1 — Chẩn đoán:**
- 🟠 Lớn: Vi phạm nguyên lý DRY — hai hàm có logic giống nhau đến 90%
- 🟡 Nhỏ: Thiếu gợi ý kiểu (type hints)
- 🟡 Nhỏ: Sử dụng vòng lặp thủ công thay vì list comprehension
- 🔵 Phong cách: Sử dụng dict thay vì dataclass để chứa dữ liệu có cấu trúc

**Bước 3 — Triển khai Tái cấu trúc:**

```python
from dataclasses import dataclass
from typing import Callable, Sequence

@dataclass(frozen=True)
class UserInfo:
    name: str
    email: str
    role: str

# REFACTOR: DRY — Sử dụng một hàm lọc chung thay thế cho hai hàm gần như giống hệt nhau
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

## Ví dụ 3: React — Tái cấu trúc Component

### Dữ liệu đầu vào từ Người dùng
```
- Ngôn ngữ/Framework: TypeScript / React Native
- Mục tiêu tập trung: Clean Code chung
- Mã nguồn: [Một component lớn trộn lẫn nhiều trách nhiệm]
```

### Các mẫu cần áp dụng
1. Trích xuất custom hooks cho logic quản lý trạng thái (`useUserData`, `useFormValidation`)
2. Tách biệt component xử lý logic (container) và component hiển thị giao diện (presentational components)
3. Memoize các tính toán tốn kém bằng `useMemo`
4. Thay thế style inline bằng `StyleSheet`
5. Thêm các interface TypeScript phù hợp cho tất cả các props
