---
name: coding-convention
description: "Use for every code change in this repository: create/update/refactor/fix APIs, managers, routes, services, tests. Always load this skill first before editing code to enforce naming, structure, logging, validation, and minimal-safe changes. Trigger keywords: coding convention, convention, style, refactor, clean code, maintainability, consistency, chuẩn code, coding-convention."
---

# Quy Ước Coding

## Quy Tắc Bắt Buộc

- Luôn đọc instruction strictly-important-convention.instructions.md trước khi chỉnh sửa code trong repository.

### đối với String
- phải định nghĩa Constant trong scope cần thiết (hàm, file, hoặc module), hoặc dùng constant có sẵn. không trực tiếp đưa string vào sử dụng.
- Ngoại lệ: các string mang tính cấu hình khai báo tại chỗ và chỉ phục vụ framework/router/schema như `method`, `path`, `tags`, `description`, `handler`, Joi `.valid('asc', 'desc')`, key field trong schema, hoặc tên route config thì được phép viết trực tiếp tại nơi khai báo để dễ đọc và dễ kiểm soát luồng route. Không tách các string này vào file constants nếu việc đó làm code phải nhảy tham chiếu nhiều nơi và khó theo dõi.

### đối với Constant
- Constant phải định nghĩa trong file constants riêng theo module (ví dụ: OrderConstant.js) để tiện tái sử dụng, không hardcode trong function, manager hoặc route. Nếu chỉ sử dụng bên trong 1 file thì có thể định nghĩa constant trong file đó, nhưng vẫn phải đặt ở đầu file và nhớ kiểm tra trùng lặp.
- Tên Constant phải gồm tối thiểu 3 từ để đảm bảo rõ nghĩa, giảm trùng lặp và dễ tìm kiếm. Ví dụ: `const DEFAULT_STATION_CODE = 'stationCode';` thay vì `const STATION_CODE = 'stationCode';`.

### đối với response data của các API trong manager
- tuân thủ các field data (data có thể bất kỳ định dạng gì), total (số lượng), totalNextPage (số lượng ở trang kế tiếp)

## Checklist Trước Khi Hoàn Thành
- Không trùng lặp business logic giữa các endpoint.
- Không refactor ngoài phạm vi các file liên quan trực tiếp.

## Tài Liệu Tham Chiếu

- Tuân thủ quy ước cách code cho các tier: ./tier-coding-convention/tier-coding-convention.instructions.md
- Tuân thủ các quy ước chung về khai báo hàm: ./coding-convention/function-declaration-convention.instructions.md
- Quy ước định nghĩa mã lỗi: ./coding-convention/error-code-definition.md