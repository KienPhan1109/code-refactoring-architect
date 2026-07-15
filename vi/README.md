# Kiến trúc sư Tối ưu hóa & Tái cấu trúc Mã nguồn Cao cấp

Kỹ năng tác nhân này được thiết kế để phân tích, tối ưu hóa và tái cấu trúc mã nguồn nhằm đáp ứng các tiêu chuẩn cao nhất trong ngành (Clean Code / Hiệu suất cao) trong khi bảo toàn tuyệt đối 100% logic nghiệp vụ ban đầu và hành vi đầu ra của hệ thống.

## 🚀 Các tính năng chính

- **Nguyên tắc không hồi quy (Zero Regression)**: Cải tổ mã nguồn mà không làm thay đổi hành vi chức năng hoặc các giao diện API.
- **Thực hành tốt nhất về SOLID & Clean Code**: Khuyến khích DRY, KISS, đơn nhiệm và kiến trúc lỏng (decoupled).
- **Tối ưu hóa độ phức tạp**: Cải thiện độ phức tạp thời gian và không gian (ký hiệu Big-O) thông qua các cấu trúc dữ liệu và thuật toán hiệu quả.
- **An toàn kiểu dữ liệu**: Áp dụng hệ thống kiểu nghiêm ngặt và thiết kế mô-đun hóa.
- **Lập trình phòng thủ**: Xử lý các đầu vào null/undefined, trạng thái rỗng và các trường hợp ngoại lệ tiêu chuẩn một cách khéo léo.

## 📂 Cấu trúc thư mục

```
code-refactoring-architect/
├── SKILL.md                          # Định nghĩa kỹ năng chính (Tiếng Anh)
├── README.md                         # Tài liệu hướng dẫn chính (Tiếng Anh)
├── examples/
│   ├── README.md                     # Tài liệu hướng dẫn ví dụ (Tiếng Anh)
│   └── usage_examples.md            # Các ví dụ thực tế cụ thể (Tiếng Anh)
├── references/
│   ├── README.md                     # Tài liệu hướng dẫn tham khảo (Tiếng Anh)
│   └── code_smell_catalog.md        # Danh mục tham khảo Code Smell (Tiếng Anh)
└── vi/                               # 🇻🇳 Bản dịch Tiếng Việt
    ├── SKILL.md                      # Định nghĩa kỹ năng chính (Tiếng Việt)
    ├── README.md                     # Tài liệu hướng dẫn chính này
    ├── examples/
    │   ├── README.md                 # Tài liệu hướng dẫn ví dụ (Tiếng Việt)
    │   └── usage_examples.md        # Các ví dụ sử dụng thực tế (Tiếng Việt)
    └── references/
        ├── README.md                 # Tài liệu hướng dẫn tham khảo (Tiếng Việt)
        └── code_smell_catalog.md    # Danh mục tham khảo Code Smell (Tiếng Việt)
```

## 🔄 Quy trình thực thi

Mỗi yêu cầu tái cấu trúc đều tuân thủ nghiêm ngặt **quy trình 4 bước**:

1. **Chẩn đoán — Phát hiện Code Smell**: Phân loại và chi tiết hóa các vấn đề tiềm ẩn (Nghiêm trọng 🔴, Lớn 🟠, Nhỏ 🟡, Phong cách 🔵).
2. **Bản vẽ Tái cấu trúc — Kế hoạch Cải tiến**: Ưu tiên các thay đổi về kiến trúc, tối ưu hóa hiệu suất và sửa lỗi phong cách.
3. **Triển khai Tái cấu trúc**: Viết lại mã hoàn chỉnh không dùng các ghi chú giữ chỗ, tích hợp các chú thích `REFACTOR` giải thích lý do thực hiện rõ ràng.
4. **So sánh tác động Trước/Sau**: Đối chiếu các chỉ số như độ phức tạp, an toàn kiểu, khả năng đọc và ghi chép các đánh đổi cấu trúc.

## 📖 Thư mục con

- [examples/](file:///d:/Phan%20Trung%20Ki%C3%AAn%20-%20PTIT/AI%20APPLICATION%20IN%20ACTION/skills/code-refactoring-architect/vi/examples): Xem các ví dụ đầu vào và đầu ra cụ thể bằng các ngôn ngữ như TypeScript, Python và React.
- [references/](file:///d:/Phan%20Trung%20Ki%C3%AAn%20-%20PTIT/AI%20APPLICATION%20IN%20ACTION/skills/code-refactoring-architect/vi/references): Xem các danh mục chi tiết về các lỗi thiết kế mã nguồn phổ biến (code smells) và giải pháp.

---

🇬🇧 **English Version**: Để xem tài liệu gốc bằng tiếng Anh, vui lòng truy cập [README.md](file:///d:/Phan%20Trung%20Ki%C3%AAn%20-%20PTIT/AI%20APPLICATION%20IN%20ACTION/skills/code-refactoring-architect/README.md).
