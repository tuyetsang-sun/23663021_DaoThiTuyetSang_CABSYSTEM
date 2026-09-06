
##1. Business Goals

- Xây dựng nền tảng CAB System phục vụ đặt xe trực tuyến.
- Tự động hóa quá trình tìm kiếm và phân công tài xế.
- Nâng cao trải nghiệm và khả năng theo dõi chuyến đi của khách hàng.
- Quản lý thanh toán và doanh thu tập trung.
- Nâng cao hiệu quả quản lý và vận hành doanh nghiệp.
- Đảm bảo hệ thống có khả năng mở rộng và phát triển lâu dài.
- Đảm bảo an toàn, bảo mật thông tin và dữ liệu giao dịch.
- Cho phép dễ dàng mở rộng dịch vụ, phương thức thanh toán và kênh thông báo.
# Sơ đồ quy trình nghiệp vụ CAB System

```mermaid
## 3. Module trọng tâm

Đối với dự án CAB System, các module cốt lõi cần ưu tiên trong quá trình phân tích và phát triển là:

1. **Đặt xe & Quản lý chuyến đi**
2. **Tìm kiếm & Phân công tài xế**
3. **Theo dõi vị trí & Trạng thái chuyến**
4. **Tính cước & Thanh toán**

Các module này tạo thành quy trình nghiệp vụ chính:

**Khách hàng tạo yêu cầu → Hệ thống tìm tài xế → Phân công tài xế → Theo dõi chuyến → Hoàn thành chuyến → Tính cước → Thanh toán → Đánh giá.**



flowchart TD

    A([Bắt đầu]) --> B[Khách hàng đăng nhập]
    B --> C[Nhập điểm đón và điểm đến]
    C --> D[Chọn loại xe]
    D --> E[Gửi yêu cầu đặt xe]

    E --> F[Hệ thống tiếp nhận yêu cầu]
    F --> G[Thông báo yêu cầu đã được tiếp nhận]

    G --> H[Tìm tài xế phù hợp]

    H --> I{Có tài xế phù hợp?}

    I -- Không --> J[Thông báo không tìm được tài xế]
    J --> Z([Kết thúc])

    I -- Có --> K[Ưu tiên tài xế gần và sẵn sàng]
    K --> L[Gửi thông báo chuyến xe cho tài xế]

    L --> M{Tài xế phản hồi?}

    M -- Không phản hồi --> N[Tìm tài xế khác]
    N --> H

    M -- Từ chối --> O[Tìm tài xế khác]
    O --> H

    M -- Chấp nhận --> P[Thông báo tài xế đã nhận chuyến]
    P --> Q[Hiển thị thông tin tài xế và thời gian dự kiến]

    Q --> R[Tài xế di chuyển đến điểm đón]
    R --> S[Cập nhật trạng thái: Đã đến điểm đón]
    S --> T[Thông báo cho khách hàng]

    T --> U[Tài xế đón khách]
    U --> V[Cập nhật trạng thái: Đã đón khách]

    V --> W[Tài xế bắt đầu chuyến]
    W --> X[Cập nhật trạng thái: Đang di chuyển]

    X --> Y[Tài xế hoàn thành chuyến]
    Y --> AA[Cập nhật trạng thái: Hoàn thành]

    AA --> AB[Hệ thống tính cước]
    AB --> AC[Hiển thị số tiền phải trả]

    AC --> AD{Phương thức thanh toán}

    AD -- Tiền mặt --> AE[Thanh toán tiền mặt]
    AE --> AH[Xác nhận thanh toán]

    AD -- Điện tử --> AF[Gửi yêu cầu đến nhà cung cấp thanh toán]
    AF --> AG{Thanh toán thành công?}

    AG -- Có --> AH[Xác nhận thanh toán]
    AG -- Không --> AI[Thông báo thanh toán thất bại]
    AI --> AJ[Cho phép xử lý thanh toán lại]
    AJ --> AF

    AH --> AK[Thông báo kết quả thanh toán]
    AK --> AL[Khách hàng đánh giá tài xế]
    AL --> AM[Lưu lịch sử chuyến đi]
    AM --> AN[Nhân viên vận hành theo dõi dữ liệu]

    AN --> AO([Kết thúc])
```
