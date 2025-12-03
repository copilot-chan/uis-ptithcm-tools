# UIS PTIT Tools - MCP Server

Một Model Context Protocol (MCP) server để tích hợp các công cụ UIS PTIT, cung cấp khả năng truy cập thông báo, lịch học và các dữ liệu khác từ hệ thống UIS PTIT thông qua Claude hoặc các LLM khác.

## Tính năng chính

### 📢 Thông báo (Notifications)
- **Lấy tất cả thông báo**: Truy cập toàn bộ thông báo với hỗ trợ cache
- **Thông báo chưa đọc**: Lấy thông báo mới nhất theo thời gian thực
- Định dạng: Tiêu đề, nội dung, ngày giờ

### 📅 Lịch học (Schedule)
- **Lịch hôm nay**: Xem lịch học của ngày hiện tại
- **Lịch theo tuần**: Xem lịch học trong khoảng thời gian nhất định
- **Lịch toàn bộ**: Truy cập toàn bộ lịch học

### 🔐 Xác thực (Authentication)
- Hỗ trợ đăng nhập bằng tài khoản PTIT
- Cache credentials an toàn

## Yêu cầu hệ thống

- Python >= 3.13
- pip hoặc poetry

## Cài đặt

### 1. Clone repository
```bash
git clone <repository-url>
cd uis-ptithcm-tools
```

### 2. Tạo virtual environment
```bash
python -m venv venv
# Windows
venv\Scripts\activate
# Linux/Mac
source venv/bin/activate
```

### 3. Cài đặt dependencies
```bash
pip install -r requirements.txt
```

Hoặc sử dụng poetry:
```bash
poetry install
```

## Cấu trúc dự án

```
uis-ptithcm-tools/
├── ptit_server/
│   ├── __init__.py
│   ├── main.py              # MCP server chính
│   ├── config.py            # Cấu hình
│   ├── models.py            # Data models
│   ├── test_main.py         # Unit tests
│   ├── client/
│   │   ├── ptit_client.py   # Client UIS PTIT
│   │   └── __init__.py
│   ├── services/
│   │   ├── auth.py          # Xử lý xác thực
│   │   ├── notification.py  # Xử lý thông báo
│   │   ├── schedule.py      # Xử lý lịch học
│   │   └── __init__.py
│   └── utils/
│       ├── formatter.py     # Format dữ liệu
│       ├── helper.py        # Các hàm hỗ trợ
│       └── __init__.py
├── test/
│   └── test_ptit_server.py  # Integration tests
├── Dockerfile
├── docker-compose.yml
├── requirements.txt
├── pyproject.toml
└── README.md
```

## Sử dụng

### Chạy MCP Server

```bash
python -m ptit_server.main
```

### Sử dụng với Docker

```bash
# Build image
docker build -t uis-ptit-tools .

# Chạy container
docker-compose up
```

## API Tools

### Notifications
- `fetch_notifications(username, password)` - Lấy tất cả thông báo
- `fetch_unread_notifications(username, password)` - Lấy thông báo chưa đọc

### Schedule
- `fetch_schedule_today(username, password)` - Lịch hôm nay
- `fetch_schedule_week(username, password, date=None)` - Lịch theo tuần
- `fetch_schedule_full(username, password)` - Lịch toàn bộ

## Testing

Chạy các test:

```bash
# Unit tests
python -m pytest ptit_server/test_main.py

# Integration tests
python -m pytest test/test_ptit_server.py

# Chạy tất cả tests
pytest
```

## Cấu hình

Xem file `ptit_server/config.py` để cấu hình:
- URL API UIS PTIT
- Timeout settings
- Cache configuration
- Logging settings

## Phát triển

### Thêm tool mới

1. Tạo hàm tool trong `ptit_server/main.py`
2. Thêm decorator `@mcp.tool()` với thẻ phù hợp
3. Thêm docstring mô tả công dụng
4. Viết unit test trong `ptit_server/test_main.py`

### Thêm service mới

1. Tạo file trong `ptit_server/services/`
2. Implement logic xử lý
3. Import và sử dụng trong `main.py`

## Dependencies chính

- **fastmcp** >= 2.11.3 - FastMCP framework
- Xem `requirements.txt` để danh sách đầy đủ

## Troubleshooting

### Lỗi xác thực
- Kiểm tra tài khoản PTIT có tồn tại
- Đảm bảo password chính xác
- Kiểm tra kết nối internet

### Lỗi timeout
- Tăng timeout trong config
- Kiểm tra server UIS PTIT có hoạt động
- Kiểm tra kết nối mạng

### Lỗi cache
- Xóa cache cũ
- Kiểm tra quyền ghi trên thư mục

## Đóng góp

Mọi đóng góp đều được hoan nghênh! Vui lòng:

1. Fork repository
2. Tạo branch feature (`git checkout -b feature/AmazingFeature`)
3. Commit changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to branch (`git push origin feature/AmazingFeature`)
5. Mở Pull Request

## License

Dự án này có giấy phép MIT. Xem file LICENSE để chi tiết.

## Liên hệ

- Repository: [uis-ptithcm-tools](https://github.com/copilot-chan/uis-ptithcm-tools)
- Issues: Báo cáo vấn đề tại GitHub Issues

---

**Lưu ý**: Dự án này không liên quan chính thức đến trường PTIT. Sử dụng trên chính danh của bạn.
