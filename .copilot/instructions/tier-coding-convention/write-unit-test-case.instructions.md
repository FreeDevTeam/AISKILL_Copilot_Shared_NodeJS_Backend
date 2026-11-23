---
name: write-unit-test-case.instructions
description: "Guidelines for writing unit test cases for API modules."
applyTo: "*.spec.js"
---

## Mục tiêu
- Chuẩn hoá cấu trúc viết test case

---

## 1. Core Rules (bắt buộc)

- không được dùng process.env cho TestData, phải sử dụng dữ liệu cố định trong file test.
- Sử dụng Mocha + Chai cho viết test case.
- Mỗi test case phải có mô tả rõ ràng.
- Sử dụng `describe` để nhóm các test case liên quan.
- Sử dụng `it` để định nghĩa từng test case.
- Sử dụng `before`, `beforeEach`, `after`, `afterEach` để setup và teardown.
- Sử dụng `chai.request` để gửi request đến API.
- Các điều kiện assert phải có comment rõ ràng để giải thích ý nghĩa và mục đích kiểm tra.
- Kết quả test phải được kiểm tra bằng checkResponseBody và checkResponseStatus để vừa có thể kiểm tra và in log nếu case fail 
---

## 2. Các thành phần tùy chọn
- Test API endpoints thì buộc phải gọi qua BASE_URL, không import app / server trực tiếp.
- Test ./ThirdParty modules thì cần có data test và chỉ test trực tiếp gọi method đã được wrapper, không cần test qua BASE_URL.