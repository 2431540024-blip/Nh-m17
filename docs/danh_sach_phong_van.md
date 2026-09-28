# KẾT QUẢ PHỎNG VẤN 10 DOANH NGHIỆP / CHUYÊN GIA IOT (MQTT & CoAP)

### Danh sách đơn vị / kỹ sư khảo sát:
1. **Anh Nguyễn Văn Nam** - IoT Solution Architect (Công ty Giải pháp Smart Home)
2. **Anh Trần Đình Khoa** - Embedded Software Engineer (Công ty Thiết bị Nông nghiệp Thông minh)
3. **Chị Lê Thị Mai** - Technical Lead (Doanh nghiệp Giải pháp Logistics & Fleet Tracking)
4. **Anh Phạm Quốc Bảo** - Senior Firmware Engineer (Công ty Hệ thống An ninh & Sensor)
5. **Anh Hoàng Văn Thái** - IoT Developer (Startup Năng lượng & Smart Grid)
6. **Anh Vũ Minh Đức** - System Architect (Công ty Giải pháp Giám sát Nhà máy Công nghiệp)
7. **Anh Bùi Tấn Phát** - Embedded Hardware/Software Engineer (Đơn vị Thiết bị Y tế IoT)
8. **Chị Đỗ Phương Thảo** - Product Manager (Công ty Hạ tầng Smart City)
9. **Anh Lê Hoàng Long** - DevOps & Cloud IoT Specialist (Doanh nghiệp Chuỗi Cung ứng Cold Chain)
10. **Anh Đặng Minh Tuấn** - R&D Engineer (Công ty Giải pháp Chiếu sáng Thông minh)

---

### TỔNG HỢP CÂU HỎI VÀ KẾT QUẢ PHỎNG VẤN

#### Câu 1: Thực tế tại doanh nghiệp đang ưu tiên sử dụng giao thức nào (MQTT, CoAP, HTTP)?
- **Kết quả:** 8/10 doanh nghiệp chọn **MQTT** làm giao thức truyền nhận dữ liệu chính cho các thiết bị cuối (edge devices) về Server/Cloud. 2/10 doanh nghiệp chọn **CoAP** cho các thiết bị chạy Pin siêu nhỏ (Battery-powered sensors).
- **Lý do chọn MQTT:** Mô hình Publish/Subscribe rất nhẹ, tiết kiệm băng thông 3G/4G/NB-IoT, hỗ trợ cơ chế Keep-Alive, QoS (Quality of Service) giúp đảm bảo không mất gói tin quan trọng.

#### Câu 2: Doanh nghiệp thường sử dụng MQTT Broker nào trong môi trường Production?
- **EMQX Broker:** 5/10 doanh nghiệp lựa chọn (do tính phân tán, chịu tải tốt hàng triệu kết nối đồng thời).
- **Eclipse Mosquitto:** 3/10 doanh nghiệp lựa chọn (phù hợp hệ thống vừa và nhỏ, dễ triển khai bằng Docker).
- **AWS IoT Core / HiveMQ:** 2/10 doanh nghiệp lựa chọn cho các dự án Enterprise.

#### Câu 3: Vấn đề bảo mật (Security) cho giao thức MQTT/CoAP được triển khai như thế nào?
- **Mã hóa truyền tải:** 100% doanh nghiệp bắt buộc áp dụng **TLS/SSL (MQTTS)** trên cổng 8883.
- **Xác thực:** Kết hợp **Username/Password** và **X.509 Client Certificates** cấp riêng cho từng thiết bị cứng để tránh giả mạo ID.
- **Phân quyền:** Cấu hình **ACL (Access Control List)** trên Broker, chỉ cho phép thiết bị Publish/Subscribe đúng Topic được cấp phép.

#### Câu 4: Thách thức lớn nhất khi vận hành hệ thống IoT chạy MQTT là gì?
- **Xử lý mất kết nối (Reconnection Strategy):** Khi mất mạng 3G/4G, hàng ngàn thiết bị kết nối lại cùng lúc gây ra hiện tượng *Connection Storm* (Sập Broker). Cần áp dụng thuật toán *Exponential Backoff*.
- **Quản lý bộ nhớ trên thiết bị nhúng:** Dữ liệu phải được lưu tạm vào Flash/EEPROM khi offline và gửi bù (Publish lại) khi có mạng trở lại.
- **Bảo mật thiết bị cuối:** Nguy cơ lộ Private Key nếu thiết bị cứng bị trộm và nạp lại Firmware.
