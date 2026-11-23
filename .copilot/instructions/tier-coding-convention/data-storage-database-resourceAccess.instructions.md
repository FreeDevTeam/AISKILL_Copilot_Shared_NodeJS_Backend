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

### đối với query database
- Không query database trực tiếp bằng library. Luôn query thông qua ResourceAccess để đảm bảo tái sử dụng, cache, và dễ maintain.
- Không tự ý thêm hàm trong resourceAccess. Chỉ Khi cần thiết cache cho việc tìm 1 record, hãy tạo hàm mới trong resourceAccess để tái sử dụng. Ví dụ: `findOneByStationCode(stationCode)` thay vì `find({ stationCode: stationCode }, 0, 1)`. Tham khảo hàm `findById` để tạo hàm mới tương tự, vì `findById` cũng chỉ lấy 1 record theo 1 field duy nhất là primary key. Nếu hàm đã tồn tại thì nên tái sử dụng.
- thay vì logic != (tìm khác biệt) thì hãy dùng logic tìm các giá trị cụ thể được chấp nhận trong constant. Vì các logic này thường áp dụng cho bộ lọc theo constant sẵn có (cố định và giới hạn số lượng giá trị). Ví dụ: thay vì `find({ feedbackStatus: { $ne: TAX_CDS_TAX_PARTNER_FEEDBACK_STATUS.COMPLETED } })` thì hãy dùng `find({ feedbackStatus: { $in: [TAX_CDS_TAX_PARTNER_FEEDBACK_STATUS.PENDING, TAX_CDS_TAX_PARTNER_FEEDBACK_STATUS.REJECTED] } })`. Logic này giúp tránh việc bỏ sót các giá trị mới được thêm vào constant trong tương lai.

## Một số best practice phải tuân thủ:
- đối với truy cập dữ liệu từ database (ResourceAccess, ví dụ StationsResourceAccess), nếu chỉ cần lấy 1 record theo 1 field duy nhất (không phải primary key) thì xem xét tạo thêm 1 hàm mới trong ResourceAccess để tối ưu sử dụng và cache. Ví dụ: findOneByStationCode(stationCode) thay vì find({ stationCode: stationCode }, 0, 1), logic tham khảo findById để thực hiện tương tự vì findById cũng chỉ lấy 1 record theo 1 field duy nhất là primary key. Lưu ý: nếu hàm đã tồn tại thì nên tái sử dụng.