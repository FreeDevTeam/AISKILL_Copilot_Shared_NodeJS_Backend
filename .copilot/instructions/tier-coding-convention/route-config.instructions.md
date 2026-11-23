---
name: route-config
description: "Standard conventions for implementing route configurations in API modules."
applyTo: "API/*/route/*.js"
---

# Nguyên tắc chung
- URL phải có path rõ ràng theo cấu trúc: <vai trò>/<tên action cụ thể> Ví dụ: user/getUserWorldTaskList
- Có các vai trò là user, admin, robot, staff (giống admin nhưng có quyền hạn hạn chế hơn)
- Tên của function config phải rõ ràng, thường theo dạng gộp lại "<vai trò><tên action cụ thể>RouteConfig", ví dụ: userGetUserWorldTaskListRouteConfig. Để khi tìm kiếm, hạn chế bị trùng, giúp tìm kiếm code nhanh hơn
- tất cả request đều là dạng POST. Trừ 1 vài request đặc thù do developer chủ động tạo theo yêu cầu đặc biệt.
- Route không chứa business logic, chỉ dispatch về manager.
- Tham khảo SampleModuleRoute.js để biết cách triển khai route config mẫu cho thống nhất toàn bộ dự án.

# Nguyên tắc của Route Config 
- Route config phải có đầy đủ thông tin gồm: 
+ description: rõ ràng, mô tả chức năng của endpoint
+ pre: cấu hình các middleware trước khi xử lý request
+ validate: schema validate cho headers/payload
+ handler: tên function xử lý request trong module route
Ví dụ về route config
description: 'Tạo định nghĩa nhiệm vụ và các phần thưởng',
pre: [CommonMiddlewares.checkSystemApiKey],
validate: { headers: headerSchema, payload: createTaskSchema },
handler: 'insertWorldTask',

## Nguyên tắc validate cho route config
- Tất cả endpoint phải có schema validate rõ ràng cho headers/payload/query(nếu có sử dụng). Thông thường sẽ luôn có validate cho payload vì tất cả request đều là dạng POST (trừ 1 vài request đặc thù do developer chủ động tạo theo yêu cầu đặc biệt).
- Giới hạn batch (min/max) phải đặt trong Joi schema tại route.
- Auth/permission phải cấu hình trong pre method theo CommonFunctions hoặc middleware (tham khảo source hiện tại đang viết các API thế nào thì dùng thế ấy vì có sự khác nhau giữa các version source).
- Schema validate phải được viết riêng và viết trực tiếp trong route config, TUYỆT ĐỐI KHÔNG DÙNG CHUNG VỚI database (trong folder "resourceAccess") hoặc response model (trong folder "model").
- Schema nếu không cần dùng chung cho các route config khác trong cùng file thì ko cần định nghĩa constant mà hãy code chung vào route config cho gọn code. Thông thường CRUD sẽ có schema riêng cho từng action. nhưng các vai trò khác nhau thì thường lại có chung schema (chỉ khác phân quyền chứ không khác schema)
- Route không chứa business logic, chỉ dispatch về manager.

