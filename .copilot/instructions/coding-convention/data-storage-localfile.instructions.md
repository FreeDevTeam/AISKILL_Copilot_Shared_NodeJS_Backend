---
name: data-storage-localfile
description: "Standard rules for implementing logic with local file data storage"
applyTo: "API/*/resourceAccess/*LocalStorage.js"
---

# Nguyên tắc chung
- data lưu dạng json, mỗi file tương ứng với 1 entity.
- trừ khi các định dạng media thì dữ liệu đều lưu dưới dạng JSON.
- lưu trữ dữ liệu theo cấu trúc thư mục rõ ràng đặt tên trong /running/<entity>, mỗi entity có 1 file riêng biệt kiểu <entity>.json.
- mỗi phần lưu và đọc file nên viết thành function riêng để dễ quản lý, tái sử dụng và kiểm soát lỗi.
- các function này nên được đặt trong cùng module với resourceAccess tương ứng, ví dụ: UserLocalStorage.js sẽ chứa các function lưu và đọc dữ liệu user.
- tất cả các function lưu và đọc file nên xử lý lỗi đầy đủ, bao gồm kiểm tra tồn tại file, quyền truy cập, và các lỗi đọc/ghi file khác.
- Model data được định nghĩa trực tiếp trong các file LocalStorage tương ứng, ví dụ: UserLocalStorage.js sẽ định nghĩa model dữ liệu user. và không dùng chung với bất kỳ nơi nào khác như /models hay /route hay /resourceAccess.
- Các field định nghĩa thì nên đặt tên rõ ràng tối thiểu có từ 2 đến 3 từ để dễ hiểu và tránh nhầm lẫn.
- Tránh sử dụng các từ viết tắt không phổ biến hoặc gây hiểu nhầm.
- Nên sử dụng kiểu dữ liệu phù hợp với từng field để đảm bảo tính toàn vẹn dữ liệu và hiệu suất truy vấn.
- Các field quan trọng nên có ràng buộc NOT NULL và các ràng buộc khác để đảm bảo dữ liệu luôn hợp lệ. dùng Joi để validate.
- Nên sử dụng các chỉ mục (index) phù hợp để tối ưu hiệu suất truy vấn, đặc biệt với các field thường xuyên được tìm kiếm hoặc lọc như các field có chữ "id","code","type","status","category","at" (timestamp),"day" (YYYYMMDD),"date" (ISO Datetime)
- Đặt tên và comment rõ ràng cho các cột. và nên có giá trị mặc định và giá trị tham khảo.
- Các cột có tên dạng type, status, category nên có CONSTANT ENUM rõ ràng và riêng biệt đặt trong *Constants.js để tái sử dụng chung cho cả project.