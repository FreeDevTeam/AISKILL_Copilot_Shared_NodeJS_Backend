# Skills

Thư mục này chứa các skill cho GitHub Copilot.

README này dành cho thành viên trong team. Copilot sẽ không tự đọc file `README.MD`; Copilot chỉ đọc `SKILL.md` trong từng thư mục skill.

## Cấu trúc thư mục (BẮT BUỘC)

Mỗi skill phải nằm trong **một thư mục con** với file `SKILL.md` bên trong:

```text
.github/skills/
  my-skill/
    SKILL.md           # BẮT BUỘC - file chính, tên phải là SKILL.md
    scripts/           # (Tùy chọn) Script thực thi
    references/        # (Tùy chọn) Tài liệu tham khảo
    assets/            # (Tùy chọn) Template, boilerplate
```

**KHÔNG** đặt file `SKILL.md` trực tiếp trong `.github/skills/` - phải có thư mục con.
