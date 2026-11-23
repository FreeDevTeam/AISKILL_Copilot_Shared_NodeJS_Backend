# Cấu Trúc Manager

- Manager chỉ xử lý business logic, không tự build response HTTP thủ công.
- Mọi hàm export cho API ở Route Config trong manager đều phải có try/catch và sử dụng responseError function (hàm chung ở Common/CommonErrorFunctions) để trả về đúng mã lỗi.
- Với manager theo Promise, dùng `return resolve(...)`, `return reject(...)`, `return responseError function(...)` (hàm chung ở Common/CommonErrorFunctions) để dừng luồng thực thi rõ ràng.
- Hàm private/helper không dùng try/catch cục bộ nếu hàm public đã xử lý catch tập trung.
- Manager không trả object trạng thái như `success`, `errorCode`, `orderError`; chỉ return data khi thành công và `throw` mã lỗi để middleware xử lý.
- Với batch API trong manager, không trả output dư thừa (không trả endpoint, không tự bọc total/results nếu chưa có chuẩn chung).
- private function chỉ chứa logic dùng chung giữa các hàm của manager.
- Không trùng lặp business logic giữa các endpoint mà phải tách thành private function dùng chung.
- Không validate trùng các lỗi mà Joi middleware ở route config đã xử lý.
