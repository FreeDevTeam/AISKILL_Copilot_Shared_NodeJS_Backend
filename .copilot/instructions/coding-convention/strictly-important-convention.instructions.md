---
name: strictly-important-convention
description: "Important conventions"
applyTo: "API/**/*.js"
---

# Kỹ năng: important convention

## Mục tiêu
- Hạn chế những code smell, code duplicate, code khó maintain.

---

## 1.bắt buộc

- Mọi thứ phải đặt tên rõ ràng từ 3-5 từ để đảm bảo dễ hiểu và tránh trùng lặp.
- ưu tiên if rõ ràng thay vì normalize trung gian.
- Format code theo chuẩn Prettier đã được lưu sẵn trong .prettierrc của dự án.
- Dùng function declaration, không arrow cho named function.
- Không được dùng assert trong code, trừ khi đó là đang viết test case trong file *.spec.js.
- Việc gọi hàm phải được gọi rõ ràng, tuyệt đối không được gọi hàm gián tiếp thông qua biến, object, array, hoặc bất kỳ cách nào khác. Ví dụ: `const func = myFunction; func();` là không được phép.
- Đặt tên theo đúng pattern của module hiện tại để đảm bảo nhất quán.
- Chỉ thêm comment khi logic khó hiểu, không thêm comment mô tả điều hiển nhiên.
- Suy nghĩ và giữ code đơn giản để dễ bảo trì.
- đối với các loại dữ liệu JSON như object, array, khi sử dụng phải đầy đủ field và value. Ví dụ: { stationCode: stationCode } thay vì { stationCode }.
- export và define và import tuân thủ theo thứ tự alphabet để tránh bị conflict khi merge code. Lưu ý: ưu tiên từ trên xuống, không điều chỉnh thứ tự của code cũ, để tránh việc phải review lại toàn bộ không cần thiết.
- Các hàm tiện ích (utility functions) phải thuần JavaScript, không chứa logic đặc thù module, không gọi database, không gọi API ngoài, không gọi chức năng đối tác (folder ThirdParty) và không phụ thuộc module khác. Các hàm này được đặt theo đúng file chuyên biệt theo mục đích sử dụng bao gồm:
+ `utils/UtilsFunctionsString.js`: contain all helper functions for string manipulation and formatting.
+ `utils/UtilsFunctionsArrayString.js`: contain all helper functions for array of strings manipulation.
+ `utils/UtilsFunctionsArrayObject.js`: contain all helper functions for array of objects manipulation.
+ `utils/UtilsFunctionsNumber.js`: contain all helper functions for number manipulation and formatting.
+ `utils/UtilsFunctionsObject.js`: contain all helper functions for object manipulation and formatting.
+ `utils/UtilsFunctionsDate.js`: contain all helper functions for date and time manipulation and formatting.
+ `utils/UtilsFunctionsValidation.js`: contain all helper functions for form validation and regex checks (email, phone, patterns).

## 2. Tối ưu:
- Nếu thấy đoạn code trong hàm hiện tại liên quan đến công việc hiện tại nhưng không đúng convention thì cũng sửa lại để đảm bảo nhất quán và dễ bảo trì.
- Chỉ sửa trong phạm vi yêu cầu, thay đổi tối thiểu và an toàn.