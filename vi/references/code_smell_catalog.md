# Danh mục Tham khảo Lỗi thiết kế Mã nguồn (Code Smell)

Tài liệu tham khảo này cung cấp một danh mục toàn diện về các lỗi thiết kế mã nguồn phổ biến (code smells) được sắp xếp theo danh mục, đi kèm với các heuristic phát hiện và kỹ thuật tái cấu trúc được đề xuất.

---

## 1. Bloaters — Mã nguồn phình to quá mức

| Smell (Lỗi) | Heuristic phát hiện | Kỹ thuật Tái cấu trúc |
|---|---|---|
| **Hàm quá dài (Long Method)** | Hàm > 20 dòng hoặc độ phức tạp cyclomatic > 10 | Trích xuất hàm (Extract Method), Phân rã điều kiện (Decompose Conditional) |
| **Lớp quá lớn (Large Class)** | Lớp > 200 dòng hoặc > 5 trách nhiệm | Trích xuất lớp (Extract Class), Trích xuất giao diện (Extract Interface) |
| **Danh sách tham số quá dài (Long Parameter List)** | Hàm > 3 tham số | Giới thiệu đối tượng tham số (Introduce Parameter Object), Mẫu Builder (Builder Pattern) |
| **Ám ảnh kiểu nguyên thủy (Primitive Obsession)** | Sử dụng kiểu dữ liệu nguyên thủy thay vì các đối tượng nhỏ (ví dụ: dùng chuỗi cho email) | Thay thế kiểu nguyên thủy bằng đối tượng giá trị (Replace Primitive with Value Object) |
| **Nhóm dữ liệu đi kèm (Data Clumps)** | Cùng một nhóm biến xuất hiện cùng nhau ở 3+ nơi khác nhau | Trích xuất lớp (Extract Class), Giới thiệu đối tượng tham số (Introduce Parameter Object) |

---

## 2. Lạm dụng Hướng đối tượng (Object-Orientation Abusers)

| Smell (Lỗi) | Heuristic phát hiện | Kỹ thuật Tái cấu trúc |
|---|---|---|
| **Câu lệnh rẽ nhánh (Switch Statements)** | Các câu lệnh switch/if-else lặp đi lặp lại trên cùng một bộ phân biệt kiểu | Thay thế điều kiện bằng tính đa hình (Replace Conditional with Polymorphism), Mẫu Strategy (Strategy Pattern) |
| **Từ chối thừa kế (Refused Bequest)** | Lớp con sử dụng dưới 50% giao diện của lớp cha | Thay thế thừa kế bằng ủy quyền (Replace Inheritance with Delegation) |
| **Trường tạm thời (Temporary Field)** | Các trường chỉ được thiết lập giá trị trong một số trường hợp cụ thể | Trích xuất lớp (Extract Class), Giới thiệu đối tượng Null (Introduce Null Object) |
| **Các lớp thay thế (Alternative Classes)** | Hai lớp có giao diện giống nhau nhưng tên khác nhau | Đổi tên/Hợp nhất (Rename/Merge), Trích xuất lớp siêu (Extract Superclass) |

---

## 3. Kháng cự thay đổi (Change Preventers)

| Smell (Lỗi) | Heuristic phát hiện | Kỹ thuật Tái cấu trúc |
|---|---|---|
| **Thay đổi phân kỳ (Divergent Change)** | Một lớp bị sửa đổi vì nhiều lý do không liên quan | Trích xuất lớp (Extract Class - tuân thủ SRP) |
| **Phẫu thuật tán xạ (Shotgun Surgery)** | Một thay đổi yêu cầu chỉnh sửa ở rất nhiều lớp khác nhau | Di chuyển phương thức (Move Method), Nội dòng hóa lớp (Inline Class) |
| **Phả hệ thừa kế song song (Parallel Inheritance)** | Tạo lớp con trong một hệ phân cấp bắt buộc phải tạo thêm lớp con ở một hệ phân cấp khác | Di chuyển phương thức (Move Method), Thu gọn phả hệ (Collapse Hierarchy) |

---

## 4. Thành phần thừa thãi (Dispensables — Unnecessary Code)

| Smell (Lỗi) | Heuristic phát hiện | Kỹ thuật Tái cấu trúc |
|---|---|---|
| **Mã chết (Dead Code)** | Các nhánh không bao giờ chạy tới, biến/import không dùng | Xóa bỏ mã chết (Remove Dead Code) |
| **Khái quát hóa suy đoán (Speculative Generality)** | Các lớp trừu tượng/giao diện chỉ có một triển khai duy nhất | Thu gọn phả hệ (Collapse Hierarchy), Xóa bỏ thành phần không dùng |
| **Mã trùng lặp (Duplicate Code)** | Khối mã tương tự nhau ở 2+ vị trí | Trích xuất hàm (Extract Method), Kéo phương thức lên lớp cha (Pull Up Method) |
| **Ghi chú quá mức (Comments)** | Ghi chú giải thích "cái gì" thay vì "tại sao" | Đặt tên tự ghi chú (Rename to Self-Document), Trích xuất hàm (Extract Method) |
| **Lớp lười biếng (Lazy Class)** | Lớp thực hiện quá ít công việc để duy trì sự tồn tại | Nội dòng hóa lớp (Inline Class) |

---

## 5. Kết nối quá chặt chẽ (Couplers — Excessive Dependencies)

| Smell (Lỗi) | Heuristic phát hiện | Kỹ thuật Tái cấu trúc |
|---|---|---|
| **Đố kỵ tính năng (Feature Envy)** | Phương thức sử dụng dữ liệu của lớp khác nhiều hơn dữ liệu của chính nó | Di chuyển phương thức (Move Method) |
| **Thân mật không phù hợp (Inappropriate Intimacy)** | Hai lớp truy cập trực tiếp vào các thành viên riêng tư (private) của nhau | Di chuyển phương thức (Move Method), Trích xuất lớp (Extract Class) |
| **Chuỗi thông điệp dài (Message Chains)** | Các chuỗi gọi hàm dạng `a.getB().getC().getD()` | Ẩn đại lý ủy quyền (Hide Delegate), Trích xuất hàm (Extract Method) |
| **Người trung gian (Middle Man)** | Lớp chỉ làm nhiệm vụ ủy quyền cuộc gọi cho lớp khác | Loại bỏ người trung gian (Remove Middle Man), Nội dòng hóa phương thức (Inline Method) |

---

## 6. Chống mẫu về Hiệu suất (Performance Anti-Patterns)

| Pattern (Chống mẫu) | Vấn đề | Giải pháp |
|---|---|---|
| **Truy vấn N+1 (N+1 Query)** | Vòng lặp phát sinh các truy vấn cơ sở dữ liệu riêng lẻ | Truy vấn gộp (Batch query), nạp trước dữ liệu (eager loading) |
| **Tìm kiếm trong vòng lặp lồng** | Độ phức tạp O(n²) khi có thể tối ưu thành O(n) | Sử dụng HashMap/Set để thực hiện tìm kiếm |
| **Cộng chuỗi trong vòng lặp** | Việc xây dựng chuỗi tốn O(n²) thời gian | Sử dụng StringBuilder hoặc phương thức join() |
| **Re-render không cần thiết** | Component React re-render ở mọi lần cha của nó render | Sử dụng React.memo, useMemo, useCallback |
| **I/O đồng bộ trên luồng chính** | Gọi các hàm chặn (blocking) trong luồng xử lý hiệu năng cao | Sử dụng Async/await, luồng công việc (worker threads) |
| **Rò rỉ bộ nhớ (Memory Leak)** | Trình lắng nghe sự kiện / đăng ký không được dọn dẹp | Dọn dẹp trong hàm return của useEffect / hàm hủy (destructor) |

---

## 7. Phân loại mức độ nghiêm trọng

Sử dụng phân loại này khi báo cáo các vấn đề trong Bước 1 (Chẩn đoán):

| Mức độ | Biểu tượng | Tiêu chí | Hành động |
|---|---|---|---|
| **Nghiêm trọng (Critical)** | 🔴 | Rủi ro bảo mật, hỏng dữ liệu, nguy cơ crash ứng dụng | Bắt buộc phải xử lý |
| **Lớn (Major)** | 🟠 | Suy giảm hiệu suất, thiếu xử lý lỗi, vi phạm kiến trúc | Nên xử lý |
| **Nhỏ (Minor)** | 🟡 | Vấn đề đặt tên, magic numbers, mã chết, vi phạm DRY nhẹ | Xử lý nếu thời gian cho phép |
| **Phong cách (Style)** | 🔵 | Định dạng, mẫu không tối ưu, tối ưu hóa siêu nhỏ | Đánh bóng tùy chọn |
