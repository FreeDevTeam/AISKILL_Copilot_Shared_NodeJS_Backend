---
name: api-module-structure
description: "Standard structure for API modules in API/. Use when creating, updating or refactoring modules to enforce consistent layering, naming, and request flow."
applyTo: "API/**/*.js"
---

# Kỹ năng: API Module Structure

## Mục tiêu
- Chuẩn hoá cấu trúc module API
- Tách rõ tier chính: route - manager - functions - resourceAccess và các layer khác (nếu có).
- Đảm bảo naming và flow nhất quán theo mô hình chung của SampleModule hoặc module có sẵn khác.

---

## 1. Core structure (bắt buộc) theo đúng thứ tự này
QUY TẮC BẮT BUỘC:
- Thứ tự các thành phần trong module phải tuân thủ đúng như trên.
- Các thành phần cùng tier không được import lẫn nhau. Ví dụ: các Manager không được import lẫn nhau, các ResourceAccess cũng không được import lẫn nhau.
- Các thành phần chỉ được import từ tier dưới theo đúng thứ tự Route > Manager > Handler > Functions > Utility > ResourceAccess > Constants.

THỨ TỰ CÁC TIER:
- route/
  - index.js
  - <ModuleName>Route.js
- manager/<ModuleName>Manager.js
- handler/<ModuleName>Handler.js : Chứa code có thể dùng chung giữa các Manager.js của các module.
- <ModuleName>Functions.js
- <ModuleName>Utility.js: chứa code có thể dùng chung giữa các Functions.js của các module
- resourceAccess/<ModuleName>ResourceAccess.js
- <ModuleName>Constants.js
---

## 2. Optional components


Chỉ thêm khi cần:
- handler/
- cronjob/ : file thực hiện và lịch trình của schedule job.
- script/ : script chứa các file thực thi riêng lẻ. Chỉ gọi trên commandline khi cần thực hiện thủ công.
- data/ : lưu trữ các data cần thiết cho business logic như mẫu html, mẫu email, các init data
- test/ : chứa test case mocha + Chai-http test, chỉ để test end-to-end với BASE_URL là url deploy của backend. không test local khi không có yêu cầu. test local được thực hiện thủ công.
- resourceAccess/*View.js, *Mapping.js : chứa dữ liệu database về view và các bảng để mapping dữ liệu của các bảng gốc.
- *<ModuleName>Utility.js

---

## 3. Request flow

1. route/index: define endpoint
2. Route: validate + auth + map action manager
3. Manager: business logic
4. ResourceAccess: DB
5. Handler/Functions: reusable logic

---
