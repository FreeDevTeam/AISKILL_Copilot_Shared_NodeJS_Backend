Cách link với Claude
1. Tạo folder .claude cùng cấp với .github
|--.claude
|--.github
|--|--skills
|--|--instruction
2. chạy lệnh để tạo folder và link skill của github copilot và Claude
rm -rf .claude/skills && ln -s ../.github/skills .claude/skills
