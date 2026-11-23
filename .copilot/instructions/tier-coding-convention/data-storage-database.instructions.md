---
name: data-storage-database
description: "Standard rules for implementing logic with database data storage"
applyTo: "API/*/resourceAccess/*ResourceAccess.js"
---

# Nguyên tắc chung
- data lưu trong database, mỗi bảng tương ứng với 1 entity.
- Không lưu media vào database.
- mỗi phần truy xuất dữ liệu nên viết thành function riêng trong ResourceAccess để dễ quản lý, tái sử dụng và kiểm soát lỗi. Tham khảo SampleModuleResourceAccess.js để làm tương tự cho thống nhất.
- Các query mới, đặc thù thì viết riêng nhưng vẫn luôn gọi về các function chung có sẵn cho việc khởi tạo query builder và execute query. chỉ thay thế logic ở giữa query cho phù hợp.
- Model data của database được định nghĩa trực tiếp trong các file ResourceAccess tương ứng, ví dụ: UserResourceAccess.js sẽ định nghĩa model dữ liệu user. và không dùng chung với bất kỳ nơi nào khác như /models hay /route hay LocalStorage.
- Các field định nghĩa thì nên đặt tên rõ ràng tối thiểu có từ 2 đến 3 từ để dễ hiểu và tránh nhầm lẫn.
- Tránh sử dụng các từ viết tắt không phổ biến hoặc gây hiểu nhầm.
- Nên sử dụng kiểu dữ liệu phù hợp với từng field trong database để đảm bảo tính toàn vẹn dữ liệu và hiệu suất truy vấn.
- Các field quan trọng nên có ràng buộc NOT NULL và các ràng buộc khác để đảm bảo dữ liệu luôn hợp lệ.
- Nên sử dụng các chỉ mục (index) phù hợp để tối ưu hiệu suất truy vấn, đặc biệt với các field thường xuyên được tìm kiếm hoặc lọc như các field có chữ "id","code","type","status","category","at" (timestamp),"day" (YYYYMMDD),"date" (ISO Datetime)
- Đặt tên và comment rõ ràng cho các cột. và nên có giá trị mặc định và giá trị tham khảo.
- Các cột có tên dạng type, status, category nên có CONSTANT ENUM rõ ràng và riêng biệt đặt trong *Constants.js để tái sử dụng chung cho cả project.