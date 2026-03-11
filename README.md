# Opencode + GitNexus Configuration

Hướng dẫn cài đặt và sử dụng Opencode với GitNexus trong project này.

## Yêu cầu

- **Node.js** >= 18
- **Git**
- **npm** hoặc **yarn**

## 1. Cài đặt Opencode

### Cài đặt toàn cục (khuyến nghị)

```bash
npm install -g @opencode-ai/cli
```

### Hoặc cài đặt cục bộ trong project

```bash
npm install @opencode-ai/cli
```

### Kiểm tra cài đặt

```bash
opencode --version
```

## 2. Cài đặt GitNexus

GitNexus là công cụ phân tích code knowledge graph, giúp Opencode hiểu rõ cấu trúc codebase.

### Cài đặt toàn cục

```bash
npm install -g gitnexus
```

### Hoặc cài đặt cục bộ

```bash
npm install gitnexus
```

### Kiểm tra cài đặt

```bash
gitnexus --version
```

## 3. Khởi tạo GitNexus cho Repository

Sau khi cài đặt, bạn cần phân tích codebase để GitNexus xây dựng knowledge graph:

```bash
# Trong thư mục gốc của repository
gitnexus analyze
```

Lệnh này sẽ:
- Phân tích toàn bộ cấu trúc code
- Xây dựng knowledge graph với các nodes (functions, classes, files)
- Phát hiện các execution flows và processes
- Tạo các communities (nhóm chức năng liên quan)

> **Lưu ý**: Chạy lại `gitnexus analyze` khi codebase có thay đổi lớn.

## 4. Cấu trúc Configuration

```
.opencode/
├── opencode.json          # Cấu hình chính
├── settings.json          # Cài đặt bổ sung
├── package.json           # Dependencies
└── skills/               # Các skill tích hợp
    ├── gitnexus/         # Skills cho GitNexus
    │   ├── exploring/
    │   ├── debugging/
    │   ├── refactoring/
    │   └── impact-analysis/
    └── superpowers/      # Skills nâng cao
        ├── brainstorming/
        ├── writing-plans/
        └── executing-plans/
```

## 5. Sử dụng Opencode

### Khởi động

```bash
# Từ thư mục gốc của project
opencode
```

### Các lệnh cơ bản

| Lệnh | Mô tả |
|------|-------|
| `/help` | Hiển thị trợ giúp |
| `/skills` | Liệt kê các skill có sẵn |
| `/agents` | Liệt kê các agents |
| `/clear` | Xóa lịch sử chat |
| `/exit` | Thoát |

## 6. Sử dụng GitNexus

### Kiểm tra trạng thái index

```bash
# Liệt kê các repository đã được index
gitnexus list repos

# Hoặc dùng trong Opencode
READ gitnexus://repos
```

### Truy vấn codebase

```bash
# Tìm execution flows liên quan đến một concept
gitnexus query "authentication flow"

# Xem context 360 độ của một symbol
gitnexus context UserService

# Phân tích impact trước khi refactor
gitnexus impact UserService --direction upstream
```

### Các Skills GitNexus có sẵn

| Skill | Mục đích |
|-------|----------|
| `gitnexus-exploring` | Khám phá codebase mới |
| `gitnexus-debugging` | Tracing bugs qua call chains |
| `gitnexus-refactoring` | Lập kế hoạch refactor an toàn |
| `gitnexus-impact-analysis` | Phân tích blast radius |

## 7. Agents Configuration

Config này định nghĩa nhiều agents chuyên biệt:

### Agents chính

- **orchestrator**: Điều phối chính, phân công tasks
- **solution-architector**: Thiết kế kiến trúc giải pháp
- **reviewer**: Review code kiểu Senior Architect
- **checker**: QA Inspector (chạy ruff/mypy/pytest)
- **explore**: Codebase Navigator
- **librarian**: Task & Knowledge Manager

### Coder Workers

- **coder1**: Python implementation (naga/qwen3-coder-plus)
- **coder2**: Python implementation (naga/grok-4.1)
- **coder3**: Python implementation (naga/minimax-m2.5)
- **coder4**: Python implementation (naga/deepseek-v3.2)
- **coder5**: Python implementation (naga/deepseek-v3.2)

## 8. Tích hợp MCP

Config này tích hợp 2 MCP servers:

### Ripgrep MCP
- Tìm kiếm nội dung file nhanh chóng
- Command: `npx -y mcp-ripgrep@latest`

### GitNexus MCP
- Truy vấn knowledge graph
- Command: `gitnexus mcp`

## 9. Cập nhật Index

Khi codebase thay đổi, cập nhật GitNexus index:

```bash
# Phân tích lại toàn bộ
gitnexus analyze

# Hoặc phân tích thay đổi gần đây
gitnexus analyze --incremental
```

## 10. Troubleshooting

### GitNexus không khởi động được

1. Kiểm tra Node.js version: `node --version` (cần >= 18)
2. Kiểm tra cài đặt: `gitnexus --version`
3. Xóa cache và thử lại: `rm -rf .git/gk && gitnexus analyze`

### Opencode không nhận diện GitNexus

1. Kiểm tra `opencode.json` có cấu hình `mcp.gitnexus`
2. Đảm bảo `gitnexus` có trong PATH
3. Thử chạy `gitnexus mcp` trực tiếp để test

### Index bị stale (cũ)

Khi thấy cảnh báo "Index is stale":
```bash
gitnexus analyze
```

## 11. Tài liệu tham khảo

- [Opencode Documentation](https://opencode.ai)
- [GitNexus Repository](https://github.com/anomalyco/gitnexus)
- [MCP Protocol](https://modelcontextprotocol.io)

## 12. Đóng góp

Để thêm skill mới hoặc điều chỉnh config:

1. Thêm file SKILL.md vào `.opencode/skills/`
2. Cập nhật `opencode.json` nếu cần
3. Test thay đổi với `opencode --dry-run`

---

**Lưu ý**: Đảm bảo chạy `gitnexus analyze` ít nhất một lần trước khi sử dụng các tính năng GitNexus trong Opencode.
