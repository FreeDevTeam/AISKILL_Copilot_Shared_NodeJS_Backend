---
name: resourceaccess-query-basics
description: "Use for general ResourceAccess query conventions: filter, paging, sorting, count, and safe defaults."
---

# ResourceAccess Query Basics

## Rule cốt lõi
- Query qua ResourceAccess, không query DB trực tiếp ở manager.
- Tận dụng `_makeQueryBuilderByFilter` + `Common.filterHandler`.
- Tránh `DB.raw` nếu query builder làm được.
- nên xem trong CommonResourceAccess để tận dụng các hàm sẵn có

## searchText
- Không tự ý thêm `like` cho các field. Chỉ `like` những field đã có sẵn hoặc được yêu cầu rõ (thường là field tên / tiêu đề như `title`).
- Không `like` các field mã (code, shortCode), URL, id: các field này đã lọc chính xác được qua `filter`, mà `like '%...%'` thì không dùng được index.

## Data mapping
- Dùng một field id nhất quán trong toàn flow.
- `||` chỉ để default (`0`, `''`, `[]`).
- Không fallback nhiều biến cho cùng ý nghĩa id.