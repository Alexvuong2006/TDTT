# CẨM NANG ÔN THI GIỮA KỲ TOÀN DIỆN: MẠNG MÁY TÍNH NÂNG CAO (CSC11004)
**Trường Đại học Khoa học Tự nhiên - ĐHQG TP.HCM (FIT - HCMUS)**  
**Giảng viên lý thuyết:** TS. Lê Ngọc Sơn (`lnson@fit.hcmus.edu.vn`)  
**Giảng viên thực hành & Trợ giảng:** ThS. Nguyễn Thanh Quân (`ntquan@fit.hcmus.edu.vn`)  
**Hình thức thi:** Trắc nghiệm khách quan (Multiple Choice Questions) - Chiếm 15% tổng điểm học phần  
**Phạm vi ôn tập trọng tâm:** 6 chuyên đề cốt lõi:
1. **TCP Congestion Control** (Điều khiển tắc nghẽn TCP cổ điển & hiện đại)
2. **Queue Management & AQM** (Quản lý hàng đợi và bộ đệm Router)
3. **Quality of Service (QoS)** (Chất lượng dịch vụ, Điều hòa lưu lượng, IntServ & DiffServ)
4. **Internet Routing** (Định tuyến tĩnh, RIP, OSPF, BGP, Phòng chống Routing Loops & Thuật toán chọn đường BGP)
5. **IPv6** (Header, Đánh địa chỉ RFC 5952, Modified EUI-64, SLAAC, DHCPv6, ICMPv6/NDP, Chuyển đổi Dual-Stack/Tunneling/NAT64)
6. **Software-Defined Networking (SDN)** (Kiến trúc phân tách Control/Data Plane, OpenFlow, Flow Table, Controller)

---

## MỤC LỤC TỔNG QUAN

1. [PHẦN 1: THÔNG TIN KỲ THI & CHIẾN LƯỢC ÔN TẬP ĐẠT ĐIỂM TỐI ĐA](#phần-1-thông-tin-kỳ-thi--chiến-lược-ôn-tập-đạt-điểm-tối-đa)
   - 1.1. Cấu trúc học phần và tỷ trọng điểm số
   - 1.2. Ma trận phân bổ câu hỏi đề thi giữa kỳ
   - 1.3. Các bẫy trắc nghiệm kinh điển và chiến thuật làm bài
2. [PHẦN 2: CHUYÊN ĐỀ 1 - ĐIỀU KHIỂN TẮC NGHẼN TCP (TCP CONGESTION CONTROL)](#phần-2-chuyên-đề-1---điều-khiển-tắc-nghẽn-tcp-tcp-congestion-control)
   - 2.1. Phân biệt bản chất: Flow Control vs. Congestion Control
   - 2.2. Cơ chế ước lượng RTT và Retransmission Timeout (RTO)
   - 2.3. Nguyên lý hội tụ và tính công bằng: Vector AIMD (Chiu & Jain)
   - 2.4. TCP Tahoe (1988): Slow Start, Congestion Avoidance, Fast Retransmit
   - 2.5. TCP Reno (1990) & Thuật toán Fast Recovery từng bước
   - 2.6. TCP NewReno & TCP SACK (Selective Acknowledgement)
   - 2.7. Băng thông BDP cao & Hạn chế của Loss-based TCP trên mạng LFN
   - 2.8. TCP Vegas (Delay-based Congestion Control)
   - 2.9. TCP CUBIC (RFC 9438): Hàm bậc ba, Concave/Convex, RTT-fairness
   - 2.10. Vấn nạn Bufferbloat & Thuật toán TCP BBR (Google Model-based)
   - 2.11. Báo hiệu tắc nghẽn chủ động: Explicit Congestion Notification (ECN, L4S, Accurate ECN RFC 9768)
   - 2.12. Bảng so sánh tổng hợp các biến thể TCP Congestion Control
3. [PHẦN 3: CHUYÊN ĐỀ 2 - QUẢN LÝ HÀNG ĐỢI & AQM (QUEUE MANAGEMENT)](#phần-3-chuyên-đề-2---quản-lý-hàng-đợi--aqm-queue-management)
   - 3.1. Kiến trúc Router và bài toán kích thước bộ đệm (Buffer Sizing: Rule of Thumb vs. Stanford Model)
   - 3.2. Cơ chế Drop Tail truyền thống và 3 nhược điểm chí mạng (Lock-out, Global Synchronization, Full Buffer Delay)
   - 3.3. Quản lý hàng đợi tích cực (AQM) & Thuật toán RED (Random Early Detection)
   - 3.4. Công thức toán học tính độ dài hàng đợi trung bình (EWMA) và xác suất drop ($p_b, p_a$)
   - 3.5. Đánh giá ưu nhược điểm của RED và các biến thể nâng cao (WRED, FRED, BLUE, CoDel/FQ-CoDel)
4. [PHẦN 4: CHUYÊN ĐỀ 3 - CHẤT LƯỢNG DỊCH VỤ (QUALITY OF SERVICE - QOS)](#phần-4-chuyên-đề-3---chất-lượng-dịch-vụ-quality-of-service---qos)
   - 4.1. Bốn tham số cốt lõi đo lường QoS (Bandwidth, Delay, Jitter, Packet Loss)
   - 4.2. Kỹ thuật điều hòa lưu lượng (Traffic Conditioning): So sánh Policing vs. Shaping
   - 4.3. Thuật toán Leaky Bucket (Thùng rò rỉ)
   - 4.4. Thuật toán Token Bucket (Thùng thẻ bài): Công thức tính thời gian burst và dung lượng truyền tối đa
   - 4.5. Cơ chế đánh dấu màu srTCM (RFC 2697) và trTCM (RFC 2698)
   - 4.6. Các cơ chế lập lịch gói tin (Packet Scheduling Disciplines): FIFO, PQ, FQ, WFQ, DRR, CBWFQ, LLQ
   - 4.7. Mô hình dịch vụ tích hợp IntServ (RFC 1633) & Giao thức RSVP (RFC 2205)
   - 4.8. Mô hình dịch vụ phân biệt DiffServ (RFC 2474, 2475) & Trường DSCP
   - 4.9. Các nhóm hành vi chuyển tiếp từng chặng (Per-Hop Behaviors - PHB): DF, EF, AF1x-AF4x, CS0-CS7
   - 4.10. Bảng đối chiếu toàn diện: IntServ vs. DiffServ
5. [PHẦN 5: CHUYÊN ĐỀ 4 - ĐỊNH TUYẾN INTERNET (INTERNET ROUTING)](#phần-5-chuyên-đề-4---định-tuyến-internet-internet-routing)
   - 5.1. Khái niệm Routing vs. Forwarding, Cấu trúc bảng định tuyến (RIB vs. FIB)
   - 5.2. Nguyên lý khớp tiền tố dài nhất (Longest Prefix Match - LPM)
   - 5.3. Administrative Distance (AD) & Bảng tra chuẩn Cisco
   - 5.4. Định tuyến tĩnh (Static Routing): Standard, Default, Floating Static Route
   - 5.5. Phân loại giao thức định tuyến động: IGP vs. EGP, Distance Vector vs. Link-State vs. Path Vector
   - 5.6. Giao thức Distance Vector & Hiện tượng Đếm đến vô cùng (Count-to-Infinity)
   - 5.7. Năm cơ chế phòng chống Routing Loops trong Distance Vector (Max Metric, Split Horizon, Poison Reverse, Hold-down Timers, Triggered Updates)
   - 5.8. Giao thức RIP (RIPv1 vs. RIPv2) & Các thông số cấu hình chuẩn
   - 5.9. Giao thức Link-State OSPF (Dijkstra SPF, LSDB, LSA types, Router ID, DR/BDR, Area 0, OSPF Cost)
   - 5.10. Giao thức BGP (BGPv4, Autonomous Systems, AS-Path, eBGP vs. iBGP, Quan hệ kinh tế Customer-Provider / Peering)
   - 5.11. Bốn nhóm thuộc tính BGP (BGP Attributes)
   - 5.12. Thuật toán lựa chọn đường đi tối ưu BGP (BGP Best Path Selection - 12 bước bất biến)
   - 5.13. An ninh định tuyến Internet: BGP Route Hijacking & Giải pháp RPKI / ROA
6. [PHẦN 6: CHUYÊN ĐỀ 5 - GIAO THỨC IPV6 (INTERNET PROTOCOL VERSION 6)](#phần-6-chuyên-đề-5---giao-thức-ipv6-internet-protocol-version-6)
   - 6.1. Động lực chuyển dịch & Khuyết điểm của giải pháp NAT kéo dài
   - 6.2. Cấu trúc Header IPv6 cố định (40 bytes) và phân tích từng trường
   - 6.3. Chuỗi tiêu đề mở rộng (Extension Headers chain) & Quy trình Path MTU Discovery
   - 6.4. Định dạng và Không gian địa chỉ IPv6 (128 bits)
   - 6.5. Quy tắc rút gọn địa chỉ IPv6 chuẩn RFC 5952
   - 6.6. Phân loại địa chỉ: Unicast (GUA, LLA fe80::/10, ULA fc00::/7), Multicast (ff00::/8), Anycast (Không có Broadcast!)
   - 6.7. Quy tắc chuyển đổi MAC 48-bit sang Interface ID 64-bit theo Modified EUI-64
   - 6.8. Giao thức ICMPv6 & Neighbor Discovery Protocol (NDP): 5 bản tin (RS, RA, NS, NA, Redirect)
   - 6.9. Cơ chế phân giải địa chỉ (Address Resolution) qua Solicited-Node Multicast & Kiểm tra trùng lặp địa chỉ (DAD)
   - 6.10. Ba phương thức cấu hình địa chỉ động: SLAAC thuần túy, SLAAC + Stateless DHCPv6, Stateful DHCPv6 (Cờ A, M, O)
   - 6.11. Chiến lược chuyển đổi công nghệ: Dual-Stack (Happy Eyeballs), Tunneling (6in4, GRE), Translation (NAT64 + DNS64)
7. [PHẦN 7: CHUYÊN ĐỀ 6 - MẠNG ĐIỀU KHIỂN BẰNG PHẦN MỀM (SDN)](#phần-7-chuyên-đề-6---mạng-điều-khiển-bằng-phần-mềm-sdn)
   - 7.1. Bối cảnh ra đời: Hạn chế của mạng truyền thống phân tán (Distributed Control)
   - 7.2. Nguyên lý kiến trúc SDN: Phân tách Data Plane, Control Plane, Management Plane
   - 7.3. Các giao diện lập trình: Southbound API, Northbound API, East/Westbound API
   - 7.4. Giao thức OpenFlow: Cấu trúc Switch OpenFlow, Flow Table, Flow Entry (Match, Priority, Counters, Instructions, Timeouts, Cookie)
   - 7.5. Cơ chế xử lý gói tin: Phân biệt Reactive Mode (Packet-In / Flow-Mod) vs. Proactive Mode
   - 7.6. Hệ điều hành mạng (Network OS / Controller) & Ứng dụng SDN trong Trung tâm dữ liệu (Data Center Virtualization)
8. [PHẦN 8: BẢNG TRA CỨU NHANH CÔNG THỨC, THAM SỐ & LỆNH CẤU HÌNH THỰC HÀNH](#phần-8-bảng-tra-cứu-nhanh-công-thức-tham-số--lệnh-cấu-hình-thực-hành)
9. [PHẦN 9: NGÂN HÀNG CÂU HỎI TRẮC NGHIỆM VÀ BÀI TẬP TÍNH TOÁN ÔN THI TRỌNG TÂM CÓ LỜI GIẢI CHI TIẾT](#phần-9-ngân-hàng-câu-hỏi-trắc-nghiệm-và-bài-tập-tính-toán-ôn-thi-trọng-tâm-có-lời-giải-chi-tiết)
   - 9.1. Dạng bài tính toán cửa sổ tắc nghẽn TCP (Trace bảng cwnd qua từng RTT)
   - 9.2. Dạng bài tính toán Buffer Size (Stanford vs. Rule of Thumb)
   - 9.3. Dạng bài tính toán xác suất loại bỏ gói RED ($p_b, p_a$)
   - 9.4. Dạng bài tính toán Token Bucket (Thời gian burst & Dung lượng burst)
   - 9.5. Dạng bài lập lịch hàng đợi Weighted Fair Queuing (WFQ Finish Time)
   - 9.6. Dạng bài nén/giải nén IPv6 và tạo Interface ID Modified EUI-64
   - 9.7. Dạng bài phân tích cờ RA (A, M, O) xác định phương thức gán IP
   - 9.8. Dạng bài phân tích thuật toán chọn đường BGP Best Path Selection
   - 9.9. Ngân hàng 50 câu trắc nghiệm lý thuyết sâu sắc (kèm đáp án và giải thích chi tiết)

---

## PHẦN 1: THÔNG TIN KỲ THI & CHIẾN LƯỢC ÔN TẬP ĐẠT ĐIỂM TỐI ĐA

### 1.1. Cấu trúc học phần và tỷ trọng điểm số
Môn học **CSC11004 - Mạng máy tính nâng cao** tại Khoa CNTT - ĐHKHTN TP.HCM có cơ cấu điểm như sau:
- **Bài tập tại lớp + Bài tập về nhà:** 10% (5% + 5%)
- **Đồ án môn học:** 35%
  - Đồ án 1 (10%): Định tuyến Internet (Multi-AS topology, OSPF, BGP, Routing Policy trên GNS3)
  - Đồ án 2 (10%): Lập trình SDN (Mininet + Ryu Controller: Load Balancing, Firewall, Traffic Engineering)
  - Đồ án 3 (15%): Tự động hóa mạng (Python/Netmiko + Ansible + NETCONF/YANG / RESTCONF)
- **Thi giữa kỳ lý thuyết:** **15%** (Hình thức: Trắc nghiệm khách quan)
- **Thi cuối kỳ lý thuyết:** **40%** (Hình thức: Trắc nghiệm khách quan)

### 1.2. Ma trận phân bổ câu hỏi đề thi giữa kỳ
Dựa trên đề cương chính thức và hệ thống slide của bộ môn, đề thi trắc nghiệm giữa kỳ phân bổ đồng đều vào 6 khối kiến thức:
1. **TCP Congestion Control (khoảng 20%):** Cơ chế AIMD, Tahoe vs. Reno vs. NewReno, CUBIC, BBR, ECN, tính toán giá trị `cwnd` và `ssthresh` qua từng vòng RTT.
2. **Queue Management & AQM (khoảng 15%):** Vấn đề Drop Tail, Global Synchronization, thuật toán RED, tính toán xác suất loại bỏ gói $p_b, p_a$, so sánh RED với WRED, CoDel.
3. **Quality of Service - QoS (khoảng 15%):** Leaky Bucket vs. Token Bucket, tính toán burst size, các cơ chế lập lịch PQ, WFQ, so sánh kiến trúc IntServ (RSVP) vs. DiffServ (DSCP, PHB EF, AF, DF).
4. **Internet Routing (khoảng 25%):** Administrative Distance, hiện tượng Routing Loops và 5 giải pháp trong Distance Vector, so sánh RIPv1 vs. RIPv2, OSPF (SPF Dijkstra, LSA, DR/BDR, Area 0, Cost), BGP (eBGP vs. iBGP, quan hệ Peering vs. Transit, các loại thuộc tính, thứ tự 12 bước chọn Best Path).
5. **IPv6 (khoảng 15%):** Header 40 bytes cố định, Path MTU Discovery, quy tắc rút gọn RFC 5952, Modified EUI-64, Solicited-Node Multicast, DAD, ý nghĩa cờ `A, M, O` trong RA, các kỹ thuật chuyển đổi (Dual-Stack, Tunneling, NAT64/DNS64).
6. **Software-Defined Networking - SDN (khoảng 10%):** Tách biệt Control Plane và Data Plane, kiến trúc Southbound/Northbound, giao thức OpenFlow, cấu trúc Flow Table và Flow Entry, chế độ Reactive vs. Proactive.

### 1.3. Các "bẫy" trắc nghiệm kinh điển và chiến thuật làm bài
- **Bẫy 1 (TCP):** Nhầm lẫn giữa Timeout và 3 Duplicate ACKs ở TCP Reno. Khi Timeout, Reno **LUÔN QUAY VỀ $cwnd = 1\text{ MSS}$** giống hệt Tahoe! Chỉ khi nhận 3 Dup ACKs, Reno mới vào Fast Recovery và đặt $cwnd = ssthresh + 3\text{ MSS}$.
- **Bẫy 2 (Queue Management):** RED tính xác suất drop dựa trên độ dài hàng đợi **TRUNG BÌNH ($avg$)**, KHÔNG BAO GIỜ dựa trên độ dài hàng đợi tức thời ($q$).
- **Bẫy 3 (QoS Token Bucket):** Token Bucket không làm phẳng tốc độ như Leaky Bucket mà cho phép truyền bùng nổ (burst) với tốc độ đường truyền tối đa $M$ trong khoảng thời gian hữu hạn $T = b / (M - r)$.
- **Bẫy 4 (Routing Loops):** Split Horizon là "không quảng bá ngược lại route ra cổng đã học", còn Poison Reverse là "quảng bá ngược lại nhưng với metric bằng vô cùng (16)".
- **Bẫy 5 (BGP Selection):** Thuộc tính `WEIGHT` là thuộc tính độc quyền của Cisco (cục bộ trên router, không gửi đi đâu), trong khi `LOCAL_PREF` gửi trong nội bộ AS. `WEIGHT` đứng bước 1, `LOCAL_PREF` đứng bước 2. Giá trị CÀNG LỚN CÀNG TỐT. Ngược lại, `MED` giá trị CÀNG NHỎ CÀNG TỐT.
- **Bẫy 6 (IPv6):** Router trung gian **KHÔNG BAO GIỜ** phân mảnh gói IPv6. Nếu gói lớn hơn MTU của chặng kế tiếp, router lập tức DROP gói và gửi bản tin ICMPv6 Type 2 "Packet Too Big" về cho host nguồn.
- **Bẫy 7 (IPv6 Address):** Dấu hai chấm kép `::` chỉ được xuất hiện **DUY NHẤT MỘT LẦN** trong địa chỉ IPv6 để tránh việc giải nén bị mơ hồ (ambiguous).

---

## PHẦN 2: CHUYÊN ĐỀ 1 - ĐIỀU KHIỂN TẮC NGHẼN TCP (TCP CONGESTION CONTROL)

### 2.1. Phân biệt bản chất: Flow Control vs. Congestion Control
Trong kiến trúc tầng Giao vận (Transport Layer), việc điều tiết tốc độ truyền dữ liệu của TCP bị chi phối bởi hai cơ chế độc lập nhưng phối hợp chặt chẽ:

| Đặc trưng | Điều khiển luồng (Flow Control) | Điều khiển tắc nghẽn (Congestion Control) |
| :--- | :--- | :--- |
| **Bảo vệ đối tượng nào?** | Phía nhận (Receiver) | Mạng truyền thông & các liên kết nghẽn (Bottleneck Links) |
| **Mục đích** | Không để phía gửi làm tràn bộ đệm nhận (Receive Buffer) | Không để các nguồn gửi bơm dữ liệu vượt quá năng lực xử lý/chuyển tiếp của router |
| **Cơ chế phản hồi** | Tường minh qua trường `Receive Window (rwnd)` trong TCP Header | Nội suy ngầm qua mất gói/trễ (Loss/Delay) hoặc qua tín hiệu ECN từ mạng |
| **Biến kiểm soát** | `rwnd` (Receiver Window - do Receiver thông báo) | `cwnd` (Congestion Window - do Sender tự tính toán và duy trì) |
| **Quy tắc phát dữ liệu** | Phía gửi chỉ được phép duy trì lượng dữ liệu đang bay: $W = \min(cwnd, rwnd)$ |

> **Quy tắc Vàng thi trắc nghiệm:** Kích thước cửa sổ phát thực tế luôn bị chặn bởi giá trị nhỏ hơn giữa `cwnd` và `rwnd`. Nếu $rwnd < cwnd$, liên kết bị giới hạn bởi bộ đệm máy nhận (flow-limited). Nếu $cwnd < rwnd$, liên kết bị giới hạn bởi mạng (congestion-limited).

---

### 2.2. Cơ chế ước lượng RTT và Retransmission Timeout (RTO)
TCP là giao thức truyền tin cậy dựa trên bộ đếm thời gian truyền lại (Retransmission Timer). Để đặt giá trị timeout $RTO$ hợp lý:
- Nếu $RTO$ quá ngắn $\to$ Phát sinh truyền lại giả tạo (premature/spurious retransmissions), gây lãng phí băng thông.
- Nếu $RTO$ quá dài $\to$ Phản ứng chậm chạp khi mất gói thật sự, đường truyền bị bỏ đói (idle link).

#### Thuật toán Jacobson/Karels (RFC 6298)
TCP đo thời gian $SampleRTT$ cho mỗi phân đoạn dữ liệu được xác nhận (ACK). Sau đó tính toán giá trị trung bình trượt có trọng số (EWMA):
1. **Ước lượng RTT làm mượt (Smoothed RTT):**  
   $EstimatedRTT = (1 - \alpha) \cdot EstimatedRTT + \alpha \cdot SampleRTT \quad (\alpha = 0.125 = 1/8)$
2. **Ước lượng độ lệch RTT (RTT Variation):**  
   $DevRTT = (1 - \beta) \cdot DevRTT + \beta \cdot |SampleRTT - EstimatedRTT| \quad (\beta = 0.25 = 1/4)$
3. **Tính toán khoảng thời gian Timeout:**  
   $RTO = EstimatedRTT + 4 \cdot DevRTT$

   *(Trong thực tế, thông số khuyến nghị RFC 6298 đặt $RTO = \max(RTO, 1.0\text{s})$ khi khởi tạo).*

#### Thuật toán Karn-Partridge (Karn's Algorithm)
- **Quy tắc 1 (Mập mờ ACK):** Không lấy mẫu $SampleRTT$ cho bất kỳ phân đoạn nào đã từng được truyền lại (vì khi nhận được ACK, phía gửi không thể biết ACK này trả lời cho lần gửi đầu tiên hay lần truyền lại).
- **Quy tắc 2 (Exponential Backoff):** Mỗi khi xảy ra Timeout cho một gói tin, giá trị $RTO$ được nhân đôi ngay lập tức: $RTO_{new} = 2 \cdot RTO_{old}$. Cơ chế này giúp TCP giảm tải áp lực lên router đang bị nghẽn nghiêm trọng.

---

### 2.3. Nguyên lý hội tụ và tính công bằng: Vector AIMD (Chiu & Jain)
Một thuật toán điều khiển tắc nghẽn phân tán lý tưởng cần thỏa mãn hai tiêu chí:
1. **Hiệu quả (Efficiency):** Khai thác tối đa băng thông liên kết ($x_1 + x_2 = C$).
2. **Công bằng (Fairness):** Các luồng chia sẻ băng thông ngang nhau ($x_1 = x_2$).

#### Phân tích không gian trạng thái Chiu & Jain
Giả sử hai luồng gửi $x_1$ và $x_2$ cùng chia sẻ một bottleneck link có dung lượng $C$:
- **AIAD (Additive Increase, Additive Decrease):** Dao động song song với đường công bằng, không bao giờ hội tụ về điểm giao nhau tối ưu.
- **MIMD (Multiplicative Increase, Multiplicative Decrease):** Dao động hướng về gốc tọa độ hoặc ra xa, không có xu hướng hội tụ về đường công bằng.
- **AIMD (Additive Increase, Multiplicative Decrease):**
  - **Additive Increase (+1 MSS mỗi RTT):** Di chuyển theo đường xiên góc 45° so với các trục tọa độ ($x_1(t+1) = x_1(t) + \alpha; x_2(t+1) = x_2(t) + \alpha$).
  - **Multiplicative Decrease (/2 khi mất gói):** Kéo vector trạng thái thẳng về gốc tọa độ $(0,0)$ theo phương xuyên tâm ($x_1(t+1) = x_1(t) \cdot \beta; x_2(t+1) = x_2(t) \cdot \beta$ với $\beta = 0.5$).
  - **Kết quả:** Sau mỗi chu kỳ tăng tuyến tính và giảm nhân, điểm vận hành từng bước tiến sát về giao điểm giữa **Đường hiệu quả (Efficiency line)** và **Đường công bằng (Fairness line)**. Đây là lý do AIMD được chọn làm nền tảng cốt lõi của Internet suốt nhiều thập kỷ.

---

### 2.4. TCP Tahoe (1988): Khởi nguyên điều khiển tắc nghẽn
Được phát triển bởi Van Jacobson sau sự cố "sụp đổ vì tắc nghẽn" (Congestion Collapse) của mạng ARPANET năm 1986.

#### Ba pha vận hành của TCP Tahoe
1. **Khởi động chậm (Slow Start - SS):**
   - Bắt đầu với $cwnd = 1\text{ MSS}$.
   - Với mỗi gói ACK mới nhận về: $cwnd = cwnd + 1\text{ MSS}$

   - Sau mỗi vòng thời gian trễ $1\text{ RTT}$, giá trị $cwnd$ tăng **gấp đôi** (tăng trưởng hàm mũ: $1 \to 2 \to 4 \to 8 \to 16 \dots$).
   - Kết thúc Slow Start khi: $cwnd \ge ssthresh$ (Slow Start Threshold) hoặc khi xảy ra mất gói.
2. **Tránh tắc nghẽn (Congestion Avoidance - CA):**
   - Kích hoạt khi $cwnd \ge ssthresh$.
   - Mục đích: Dò tìm băng thông thận trọng hơn. Với mỗi ACK nhận được: $cwnd = cwnd + \frac{1}{cwnd}\text{ MSS}$

   - Sau mỗi $1\text{ RTT}$, giá trị $cwnd$ chỉ tăng đúng **+1 MSS** (tăng trưởng tuyến tính theo thời gian).
3. **Phát lại nhanh (Fast Retransmit):**
   - Khi nhận liên tiếp **3 Duplicate ACKs** (tổng cộng 4 ACK giống nhau cho cùng một số thứ tự sequence number):
   - Phía gửi kết luận gói tin tiếp theo chắc chắn bị rơi trên đường truyền (chứ không phải bị trễ hay đổi thứ tự gói).
   - Truyền lại ngay lập tức phân đoạn bị mất mà **không cần chờ bộ đếm RTO đếm hết**.

#### Phản ứng khi mất gói của TCP Tahoe (ĐIỂM YẾU LỚN NHẤT)
Bất kể mất gói do **3 Duplicate ACKs** hay do **RTO Timeout**:
- Cập nhật ngưỡng: $ssthresh = \max\left(\frac{cwnd}{2}, 2\text{ MSS}\right)$
- Ép cửa sổ về gốc: $cwnd = 1\text{ MSS}$

- Trạng thái kế tiếp: Quay về **Slow Start**.
- **Hậu quả:** Làm rỗng đường ống (empty pipeline), lãng phí tài nguyên mạng, thông lượng bị sụt giảm nghiêm trọng hình răng cưa sâu hoắm.

---

### 2.5. TCP Reno (1990) & Thuật toán Fast Recovery
TCP Reno ra đời nhằm khắc phục nhược điểm của Tahoe bằng cách bổ sung trạng thái **Phục hồi nhanh (Fast Recovery)** khi mất gói nhẹ (nhận 3 Dup ACKs).

#### Cơ chế Fast Recovery từng bước chi tiết (Chuẩn RFC 5681)
Khi phía gửi nhận được đúng **3 Duplicate ACKs**:
- **Bước 1 (Thiết lập ngưỡng):** $ssthresh = \max\left(\frac{cwnd}{2}, 2\text{ MSS}\right)$
- **Bước 2 (Fast Retransmit):** Truyền lại ngay phân đoạn bị thiếu.
- **Bước 3 (Thổi phồng cửa sổ - Window Inflation):** $cwnd = ssthresh + 3\text{ MSS}$

  *(Lý do cộng 3: 3 Duplicate ACKs là bằng chứng cho thấy có đúng 3 phân đoạn gửi sau đã đến được máy nhận thành công và đang nằm trong bộ đệm của máy nhận, nghĩa là 3 phân đoạn đó đã rời khỏi mạng!)*
- **Bước 4 (Trong trạng thái Fast Recovery):**
  - Mỗi khi nhận thêm một Duplicate ACK tiếp theo: $cwnd = cwnd + 1\text{ MSS}$

    (Vì thêm một gói nữa đã rời mạng). Nếu giá trị $cwnd$ mới cho phép, phía gửi có thể phát thêm các gói tin mới chưa gửi.
- **Bước 5 (Thoát Fast Recovery khi nhận New ACK):**
  - Khi nhận được một ACK xác nhận dữ liệu mới (New ACK - xác nhận gói bị mất đã được máy nhận tiếp nhận):
  - **Thu hẹp cửa sổ (Window Deflation):** $cwnd = ssthresh$

  - Chuyển trạng thái sang **Congestion Avoidance** (tiếp tục tăng tuyến tính +1 MSS / RTT).

> [!WARNING]
> **Quy tắc trắc nghiệm cốt tử của TCP Reno:**
> - Nếu mất gói được phát hiện bằng **3 Duplicate ACKs** $\to$ Kích hoạt Fast Retransmit + Fast Recovery: $ssthresh = cwnd / 2$, sau đó $cwnd = ssthresh$ (vào Congestion Avoidance).
> - Nếu mất gói do **Timeout (RTO)** $\to$ **RENO HÀNH ĐỘNG HỆT NHƯ TAHOE**: $ssthresh = cwnd / 2$, **$cwnd = 1\text{ MSS}$**, và rơi thẳng về **Slow Start**!

---

### 2.6. TCP NewReno & TCP SACK (Selective Acknowledgement)

#### TCP NewReno (RFC 6582)
- **Vấn đề của Reno:** Trong một cửa sổ dữ liệu lớn, nếu có từ 2 gói tin trở lên bị mất cùng lúc, TCP Reno sau khi nhận Partial ACK (chỉ ACK gói mất đầu tiên) sẽ lập tức thoát Fast Recovery, làm sụt $cwnd$ lần thứ hai và thường xuyên bị Timeout.
- **Giải pháp của NewReno:** Phân biệt rõ hai loại ACK trong Fast Recovery:
  - **Partial ACK:** Chỉ xác nhận một phần dữ liệu đã gửi trước khi vào Fast Recovery $\to$ Kết luận vẫn còn gói khác bị mất! NewReno **không thoát Fast Recovery**, lập tức truyền lại gói tiếp theo và giữ cửa sổ để duy trì luồng dữ liệu.
  - **Full ACK:** Xác nhận toàn bộ dữ liệu gửi trước khi mất gói $\to$ Lúc này mới chính thức hoàn thành Fast Recovery và chuyển sang Congestion Avoidance.

#### TCP SACK (RFC 2018)
- Sử dụng trường TCP Options để máy nhận gửi kèm thông tin các khối dữ liệu không liên tục (out-of-order blocks) mà nó đã nhận được.
- Phía gửi duy trì một "bảng điểm" (Scoreboard) và chỉ truyền lại chính xác những lỗ hổng (missing gaps), giải quyết triệt để vấn đề mất nhiều gói trong cùng một RTT.

---

### 2.7. Băng thông BDP cao & Hạn chế của Loss-based TCP trên mạng LFN
- Khái niệm **LFN (Long Fat Networks - RFC 7323):** Mạng có tích số Băng thông - Độ trễ rất lớn (High Bandwidth-Delay Product: $BDP = \text{Bandwidth} \times RTT$).  
  *Ví dụ:* Đường truyền $10\text{ Gbps}$ với $RTT = 100\text{ ms} \implies BDP = 10^9\text{ bits} \approx 125\text{ MB}$. Với $MSS = 1500\text{ bytes}$, cần cửa sổ $cwnd \approx 83,333\text{ packets}$.
**Công thức Throughput Mathis:** $\text{Throughput} \le \frac{MSS}{RTT} \sqrt{\frac{3}{2p}} \approx \frac{1.22 \cdot MSS}{RTT \cdot \sqrt{p}}$ *(với $p$ là xác suất mất gói).*
- **Nghịch lý của Reno trên mạng LFN:**
  - Nếu mất gói một lần, Reno giảm cửa sổ đi 50% ($83,333 / 2 \approx 41,666\text{ packets}$).
  - Với tốc độ tăng tuyến tính $+1\text{ MSS}$ mỗi RTT ($100\text{ ms}$), Reno cần $41,666\text{ RTT} \approx 4,166\text{ s} \approx 70\text{ min}$ chỉ để phục hồi lại mức thông lượng ban đầu!
  - Để duy trì đường truyền $10\text{ Gbps}$, tỷ lệ mất gói yêu cầu phải nhỏ hơn $10^{-10}$ (điều không tưởng trên thực tế).

---

### 2.8. TCP Vegas (Delay-based Congestion Control)
Được đề xuất bởi **Lawrence Brakmo và Larry Peterson (1994)** tại Đại học Arizona. Đây là thuật toán tiên phong đại diện cho trường phái **Dựa trên độ trễ (Delay-based Congestion Control)**, chủ động phát hiện dấu hiệu nghẽn mạng từ sự gia tăng RTT trước khi xảy ra hiện tượng tràn bộ đệm và rớt gói (Packet Loss).

#### 1. Nguyên lý đo lường thông lượng & hàng đợi
- **Đo lường RTT cơ sở ($BaseRTT$):** Là giá trị RTT nhỏ nhất đo được trong suốt phiên truyền, đại diện cho độ trễ truyền lan hai chiều thuần túy khi mạng rảnh rỗi (bộ đệm router hoàn toàn rỗng: $\text{Queue Delay} = 0$).
- **Đo lường RTT thực tế ($ActualRTT$):** Là RTT trung bình đo được của các gói tin trong vòng RTT hiện tại (khi hàng đợi bắt đầu có gói tin tích tụ, $ActualRTT > BaseRTT$).
- **Thông lượng kỳ vọng (Expected Throughput):** $\text{Expected} = \frac{cwnd}{BaseRTT}$ *(Tốc độ mà kết nối lẽ ra đạt được nếu đường truyền hoàn toàn không có độ trễ hàng đợi).*
- **Thông lượng thực tế (Actual Throughput):** $\text{Actual} = \frac{cwnd}{ActualRTT}$ *(Tốc độ truyền tải thực tế đo được trên mạng).*

#### 2. Bản chất và công thức tính lượng dữ liệu ứ đọng trong hàng đợi (Queue Backlog - $\text{Diff}$ hay $\Delta$)
Độ chênh lệch giữa thông lượng kỳ vọng và thông lượng thực tế biểu thị tốc độ dữ liệu bị kẹt lại trong bộ đệm router. Khi nhân độ chênh lệch này với $BaseRTT$, ta thu được **chính xác số lượng gói tin (packets) đang tích tụ trong hàng đợi**:
$\Delta = \text{Diff} = (\text{Expected} - \text{Actual}) \times BaseRTT$  
Biến đổi đại số từng bước chi tiết:  
$\Delta = \left(\frac{cwnd}{BaseRTT} - \frac{cwnd}{ActualRTT}\right) \times BaseRTT = cwnd \cdot \left(\frac{BaseRTT}{BaseRTT} - \frac{BaseRTT}{ActualRTT}\right) = cwnd \cdot \left(1 - \frac{BaseRTT}{ActualRTT}\right)$
- **Ý nghĩa vật lý của $\Delta$:** Đại diện cho số lượng gói tin (packets) đang nằm chờ trong bộ đệm của bottleneck router.

#### 3. Quy tắc điều chỉnh cửa sổ $cwnd$ theo ngưỡng $(\alpha, \beta)$
TCP Vegas so sánh số gói tin ứ đọng $\Delta$ với hai ngưỡng cấu hình trước $(\alpha, \beta)$ (thông số chuẩn khuyến nghị: $\alpha = 1\text{ gói}, \beta = 3\text{ gói}$):
- **Nếu $\Delta < \alpha$ (Hàng đợi quá rỗng):** Đường truyền còn dư thừa năng lực $\implies$ Tăng tuyến tính cửa sổ: $cwnd = cwnd + 1\text{ MSS}$ mỗi RTT.
- **Nếu $\Delta > \beta$ (Hàng đợi tích tụ quá nhiều gói):** Nguy cơ tắc nghẽn cao $\implies$ Giảm tuyến tính cửa sổ: $cwnd = cwnd - 1\text{ MSS}$ mỗi RTT để giải tỏa bộ đệm.
- **Nếu $\alpha \le \Delta \le \beta$ (Vùng ổn định lý tưởng):** Hàng đợi router duy trì ở mức tối ưu $\implies$ Giữ nguyên kích thước $cwnd$.

#### 4. Nhược điểm chí mạng của TCP Vegas
- **Bị TCP Loss-based lấn át (Unfairness with Reno/CUBIC):** Khi chia sẻ chung đường truyền cổ chai với các luồng TCP Loss-based (như Reno, CUBIC), khi hàng đợi bắt đầu đầy, Vegas phát hiện RTT tăng nên lập tức chủ động giảm $cwnd$ để bảo vệ hàng đợi. Trong khi đó, Reno tiếp tục tăng $cwnd$ cho đến khi tràn buffer. Kết quả là Vegas liên tục nhường băng thông và bị các luồng Reno bóp nghẹt thông lượng (Starvation).
- **Nhạy cảm với sự thay đổi định tuyến:** Nếu định tuyến thay đổi khiến đường truyền dài hơn, $BaseRTT$ bị tăng lên mà Vegas không biết, dẫn đến ước tính sai số gói trong hàng đợi.

---

### 2.9. TCP CUBIC (RFC 9438 - Thuật toán mặc định trên Linux)
CUBIC (Ha, Rhee, Xu - 2008) được thiết kế đặc thù cho mạng tốc độ cao (LFN), thay thế BIC-TCP và trở thành chuẩn mặc định của Linux kernel từ phiên bản 2.6.19 đến nay.

#### Hàm tăng trưởng cửa sổ bậc ba
Quy mô cửa sổ của CUBIC là một hàm bậc ba theo thời gian thực $t$ (tính bằng giây) kể từ lần giảm cửa sổ gần nhất: $W_{cubic}(t) = C \cdot (t - K)^3 + W_{max}$

Trong đó:
- $W_{max}$: Kích thước cửa sổ ngay trước khi xảy ra sự kiện mất gói gần nhất.
- $\beta$: Hệ số giảm nhân khi mất gói (CUBIC chọn $\beta = 0.7$, tức chỉ giảm 30%, giữ lại 70% cửa sổ, nhẹ nhàng hơn Reno giảm 50%).
- $C$: Hằng số tỷ lệ co dãn (mặc định $C = 0.4$).
- $K$: Khoảng thời gian cần thiết để cửa sổ tăng từ $W_{\max} \cdot \beta$ trở lại $W_{\max}$ khi không có mất gói: $K = \sqrt[3]{\frac{W_{\max} \cdot (1 - \beta)}{C}} = \sqrt[3]{\frac{W_{\max} \cdot 0.3}{0.4}}$

#### Hai giai đoạn tăng trưởng của CUBIC
1. **Pha Lõm (Concave Region - khi $t < K$):**
   - Cửa sổ tăng rất nhanh ở giai đoạn đầu để tận dụng băng thông trống.
   - Khi tiệm cận mức $W_{max}$, tốc độ tăng chậm dần lại và trở nên rất phẳng gần điểm bão hòa, giúp hệ thống hoạt động ổn định và hạn chế rớt gói lặp lại.
2. **Pha Lồi (Convex Region - khi $t > K$):**
   - Nếu sau khoảng thời gian $K$ mà mạng vẫn không xảy ra mất gói, CUBIC nhận định dung lượng liên kết đã tăng lên.
   - CUBIC bắt đầu tăng tốc độ dò tìm băng thông: ban đầu tăng chậm, sau đó tăng vọt theo hàm mũ bậc ba để nhanh chóng lấp đầy liên kết mới.

#### Tính chất vượt trội của CUBIC
- **Độc lập với RTT (RTT-Fairness):** Hàm tăng trưởng $W_{cubic}(t)$ phụ thuộc vào đồng hồ thời gian thực $t$ chứ không phụ thuộc vào số vòng lặp RTT. Các luồng có RTT ngắn và RTT dài có tốc độ tăng cửa sổ ngang nhau.
- **Chế độ thân thiện với Reno (TCP-Friendly Mode):** Trên các đường truyền băng thông nhỏ và RTT ngắn nơi Reno chiếm ưu thế, CUBIC tự động tính toán cửa sổ theo mô hình Reno $W_{\text{reno}}(t)$ và luôn chọn: $cwnd = \max(W_{\text{cubic}}(t), W_{\text{reno}}(t))$.

---

### 2.10. Vấn nạn Bufferbloat & Thuật toán TCP BBR (Google)

#### Hiện tượng Bufferbloat
- **Nguyên nhân:** Nhà sản xuất thiết bị mạng trang bị bộ đệm RAM quá lớn và rẻ tiền vào router, kết hợp với chính sách quản lý Drop Tail.
- **Hệ quả:** Các thuật toán loss-based (Reno, CUBIC) liên tục bơm dữ liệu cho đến khi đầy bộ đệm mới giảm tốc độ. Hàng đợi router luôn trong trạng thái đầy ắp, khiến độ trễ RTT tăng vọt từ vài mili-giây lên hàng giây mà không hề có gói tin bị drop. Người dùng bị lag, giật cuộc gọi thoại/video dù băng thông hiển thị rất cao.

#### TCP BBR (Bottleneck Bandwidth and RTT)
BBR (Cardwell, Cheng, Gunn, Yuchung Cheng, Van Jacobson - Google 2016) là thuật toán dựa trên mô hình (Model-based), không xem packet loss là tín hiệu tắc nghẽn.

#### Điểm vận hành tối ưu Kleinrock
Theo lý thuyết hàng đợi Kleinrock:
- Tốc độ phát tối ưu đúng bằng băng thông nút thắt: $\text{Rate} = BtlBw$ (Bottleneck Bandwidth).
- Lượng dữ liệu in-flight tối ưu đúng bằng: $\text{BDP} = BtlBw \times RTprop$

  *(với $RTprop$ là Round-Trip Propagation Time khi hàng đợi rỗng).*
- Tại điểm này: Thông lượng đạt cực đại (Full Throughput) trong khi độ trễ đạt cực tiểu (Minimum Delay) và hàng đợi rỗng hoàn toàn!

#### Bốn trạng thái hoạt động của BBR
1. **Startup:** Tăng tốc độ phát theo hàm mũ (nhân đôi mỗi RTT với hệ số gain $2/\ln 2 \approx 2.89$) để phát hiện nhanh giá trị $BtlBw$.
2. **Drain:** Khi phát hiện $BtlBw$ chững lại, giảm tốc độ phát (với gain $1/2.89$) để xả sạch toàn bộ hàng đợi phát sinh trong pha Startup.
3. **ProbeBW:** Pha vận hành ổn định. Chu kỳ 8 RTT với các hệ số điều chỉnh tốc độ (Pacing Gain): $[1.25, \; 0.75, \; 1.0, \; 1.0, \; 1.0, \; 1.0, \; 1.0, \; 1.0]$.

   (1 vòng thăm dò băng thông cao hơn, 1 vòng xả hàng đợi, 6 vòng duy trì ổn định).
4. **ProbeRTT:** Cứ mỗi 10 giây một lần, BBR hạ cửa sổ phát xuống còn đúng **4 gói tin (4 MSS)** trong vòng 200 ms để làm rỗng hàng đợi hoàn toàn, từ đó đo đạc lại giá trị $RTprop$ thực sự của liên kết.

---

### 2.11. Báo hiệu tắc nghẽn chủ động: ECN, L4S & Accurate ECN

#### Explicit Congestion Notification (ECN - RFC 3168)
Thay vì chờ router drop gói để nhận biết nghẽn, ECN cho phép router chủ động đánh dấu vào gói tin IP khi hàng đợi bắt đầu chớm nghẽn:
- **Trường ECN trong IPv4 ToS / IPv6 Traffic Class (2 bits):**
  - `00`: Non-ECT (Không hỗ trợ ECN).
  - `01` hoặc `10`: ECT(1) hoặc ECT(0) (Endpoint hỗ trợ ECN).
  - `11`: **CE (Congestion Experienced)** - Do Router ghi đè vào khi phát hiện nguy cơ tắc nghẽn!
- **Các cờ trong TCP Header:**
  - Khi máy nhận nhận gói tin có `CE = 11`, nó bật cờ **ECE (ECN-Echo)** trong gói ACK gửi ngược về cho máy gửi.
  - Phía gửi nhận được cờ ECE sẽ giảm $cwnd$ hệt như khi bị rớt gói (nhưng không phải truyền lại), đồng thời bật cờ **CWR (Congestion Window Reduced)** trong gói dữ liệu kế tiếp để thông báo cho máy nhận tắt cờ ECE.

#### L4S & Accurate ECN (RFC 9330-9332, RFC 9768 - Cập nhật 2026)
- **L4S (Low Latency, Low Loss, Scalable Throughput):** Kiến trúc kết hợp thuật toán điều khiển tắc nghẽn Prague và hàng đợi kép (DualQ Coupled AQM) giúp đưa độ trễ hàng đợi trên Internet xuống dưới 1 mili-giây.
- **Accurate ECN (RFC 9768):** Tái cấu trúc các cờ TCP (ECE, CWR, NS) thành bộ đếm phản hồi liên tục số lượng gói tin bị đánh dấu CE, giúp phía gửi phản hồi tỷ lệ chính xác thay vì phản ứng bật/tắt thô bạo.

---

### 2.12. Bảng so sánh tổng hợp các biến thể TCP Congestion Control

| Thuật toán | Loại cơ chế | Tín hiệu nhận diện nghẽn | Phản ứng khi có tín hiệu nghẽn | Khả năng thích ứng LFN / BDP cao | Thân thiện Reno |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **TCP Tahoe (1988)** | Loss-based | 3 Dup ACKs hoặc Timeout | Luôn đặt $cwnd = 1$, $ssthresh = cwnd/2$, vào Slow Start | Rất kém | Chuẩn gốc |
| **TCP Reno (1990)** | Loss-based | 3 Dup ACKs / Timeout | 3 Dup ACKs: Fast Recovery ($cwnd = ssthresh$). Timeout: $cwnd = 1$ | Kém | Chuẩn gốc |
| **TCP NewReno (1999)**| Loss-based | Partial / Full ACKs | Xử lý mất nhiều gói trong 1 RTT không bị Timeout | Kém | Tương thích |
| **TCP Vegas (1994)** | Delay-based | RTT tăng ($\Delta = Expected - Actual$) | Điều chỉnh mịn $cwnd \pm 1$ dựa trên ngưỡng $\alpha, \beta$ | Trung bình | Kém (bị Reno đè) |
| **TCP CUBIC (2008)** | Hybrid Loss | Hàm bậc ba thời gian thực $W(t)$ | Giảm 30% ($\beta = 0.7$), tăng tốc bậc ba concave/convex | **Xuất sắc** | Tốt (có Reno mode) |
| **TCP BBR (2016)** | Model-based | Đo lường $BtlBw$ và $RTprop$ | Duy trì in-flight $= BDP$, điều chỉnh pacing rate | **Xuất sắc** | Chiếm ưu thế lớn |
| **DCTCP (2010)** | ECN-based | Tỷ lệ gói tin CE trong Data Center | Giảm cửa sổ tỷ lệ theo phần trăm gói CE | Rất cao (Data Center)| Cần hạ tầng riêng |

---

## PHẦN 3: CHUYÊN ĐỀ 2 - QUẢN LÝ HÀNG ĐỢI & AQM (QUEUE MANAGEMENT)

### 3.1. Kiến trúc Router và bài toán kích thước bộ đệm (Buffer Sizing)

#### Kiến trúc tổng quát của Router hiện đại
Router bao gồm 3 thành phần phần cứng cốt lõi:
1. **Cổng vào (Input Ports):** Tiếp nhận tín hiệu vật lý, giải mã khung Layer 2, tra cứu bảng chuyển tiếp FIB (Forwarding Information Base) bằng bộ nhớ TCAM để xác định cổng ra.
2. **Khung chuyển mạch (Switching Fabric):** Đưa gói tin từ cổng vào sang cổng ra (dạng Shared Memory, Bus, hoặc Crossbar đa tầng tốc độ cao).
3. **Cổng ra (Output Ports):** **Nơi xảy ra hiện tượng thắt cổ chai (Bottleneck) và tắc nghẽn chính!** Khi nhiều cổng vào cùng chuyển tiếp gói tin tới một cổng ra với tổng tốc độ vượt quá băng thông đường truyền ra, các gói tin buộc phải xếp hàng chờ trong bộ đệm (Buffer Memory).

```
[Input Port 1] ---\                                 /--> [Output Port 1 (Buffer & Queue)]
[Input Port 2] ----> === [ Switching Fabric ] === ----> [Output Port 2 (Buffer & Queue)]
[Input Port 3] ---/                                 \--> [Output Port 3 (Buffer & Queue)]
```

#### Bài toán kích thước bộ đệm Router (Buffer Sizing)
- **Quy tắc kinh điển (Rule of Thumb - Villamizar & Song 1994):** $B = RTT \times C$

  *(với $C$ là băng thông liên kết, $RTT$ là thời gian trễ khứ hồi trung bình, thường lấy chuẩn 250 ms).*
  - *Ý nghĩa:* Xuất phát từ cơ chế AIMD của TCP Reno. Khi xảy ra mất gói, Reno giảm cửa sổ đi 50%. Để đường truyền luôn bận 100% (không bị rỗng trong thời gian đợi ACK quay về), bộ đệm router cần chứa đủ lượng dữ liệu bị thiếu hụt này, tức đúng bằng dung lượng $RTT \times C$.
- **Mô hình Stanford (Appenzeller, Keshav, McKeown - SIGCOMM 2004):**
  Khi có số lượng lớn $N$ luồng TCP độc lập chạy đồng thời qua một bottleneck router lõi: $B = \frac{RTT \times C}{\sqrt{N}}$

  - *Bản chất toán học:* Các luồng TCP độc lập không bị mất gói cùng một lúc (không đồng bộ). Dựa trên Định lý Giới hạn Trung tâm (Central Limit Theorem), độ biến thiên tổng thể của lượng dữ liệu đến giảm theo tỷ lệ $1/\sqrt{N}$.
  - *Ý nghĩa thực tiễn:* Với một liên kết 40 Gbps gồm 10,000 luồng TCP, bộ đệm yêu cầu giảm từ 1 GB (theo Rule of Thumb) xuống chỉ còn 10 MB (theo Stanford), giúp tiết kiệm hàng triệu USD chi phí phần cứng và giảm trễ hàng đợi đáng kể.

---

### 3.2. Cơ chế Drop Tail truyền thống và 3 nhược điểm chí mạng
Drop Tail (Loại bỏ ở đuôi) là cơ chế quản lý hàng đợi thụ động (Passive Queue Management) mặc định:
- Hoạt động theo nguyên tắc FIFO: Gói tin đến khi bộ đệm chưa đầy sẽ được xếp vào cuối hàng.
- Khi bộ đệm đầy 100% dung lượng ($q = B$), mọi gói tin mới đến tiếp theo đều bị loại bỏ (drop) không thương tiếc.

#### Ba khuyết điểm chí mạng của Drop Tail
1. **Khóa nghẽn luồng (Lock-out / Starvation):**
   Một luồng gửi bùng nổ (bursty flow) hoặc luồng UDP phát tốc độ cao có thể chiếm trọn toàn bộ không gian hàng đợi, khiến các luồng gửi nhỏ, nhạy cảm với độ trễ (như DNS, Telnet, VoIP) không thể chen chân vào bộ đệm và bị loại bỏ liên tục.
2. **Đồng bộ hóa toàn cục (Global Synchronization):**
   - Khi bộ đệm router đầy ắp, hàng loạt gói tin thuộc về nhiều luồng TCP khác nhau bị rớt đồng thời trong cùng một thời điểm.
   - Hậu quả: Tất cả các luồng TCP đồng loạt phát hiện mất gói $\to$ tất cả cùng kích hoạt giảm nhân cửa sổ $cwnd$ chia đôi $\to$ lưu lượng tổng trên liên kết tụt dốc thảm hại, đường truyền bị lãng phí. Sau đó, tất cả lại cùng nhau tăng cửa sổ trở lại $\to$ bộ đệm lại đầy $\to$ lặp lại chu kỳ sụt giảm liên tục.
3. **Độ trễ hàng đợi tối đa (Full Buffer Delay - Bufferbloat):**
   Trong điều kiện tải cao, hàng đợi luôn bị giữ ở trạng thái gần đầy 100%. Mọi gói tin đi qua router đều phải chịu thời gian trễ hàng đợi cực đại $Delay_{queue} = B / C$, làm tê liệt các ứng dụng thời gian thực.

---

### 3.3. Quản lý hàng đợi tích cực (AQM) & Thuật toán RED
Active Queue Management (AQM) ra đời nhằm chủ động phát hiện dấu hiệu tắc nghẽn và gửi tín hiệu cảnh báo (bằng cách drop hoặc đánh dấu ECN) **trước khi bộ đệm router thực sự đầy**.

#### Thuật toán RED (Random Early Detection - Sally Floyd & Van Jacobson 1993)
RED là thuật toán AQM kinh điển và quan trọng nhất, vận hành dựa trên 3 nguyên tắc:
1. Giám sát độ dài hàng đợi **trung bình** ($avg$) thay vì độ dài tức thời ($q$).
2. Loại bỏ gói tin theo **xác suất ngẫu nhiên** tăng dần khi hàng đợi trung bình vượt ngưỡng tối thiểu.
3. Phân tán các sự kiện mất gói đều đặn theo thời gian để triệt tiêu hiện tượng đồng bộ toàn cục.

---

### 3.4. Công thức toán học tính độ dài hàng đợi trung bình và xác suất drop

#### 1. Tính toán độ dài hàng đợi trung bình ($avg$)
Sử dụng bộ lọc trung bình trượt có trọng số theo hàm mũ (EWMA): $avg \leftarrow (1 - w_q) \cdot avg + w_q \cdot q$

- $q$: Độ dài hàng đợi thực tế tức thời tại thời điểm gói tin đến.
- $w_q$: Trọng số hàng đợi (thường chọn $w_q = 0.002$). Trọng số nhỏ giúp lọc bỏ các đợt bùng nổ lưu lượng tạm thời (transient bursts), ngăn không cho hệ thống phản ứng thái quá.

*Trường hợp hàng đợi rỗng (Queue is Idle):* Nếu router phát hiện hàng đợi bị rỗng trong một khoảng thời gian $idle\_time$, $avg$ được suy giảm nhân theo số lượng gói tin giả định $m$: $avg \leftarrow avg \cdot (1 - w_q)^m \quad (\text{với } m = \frac{\text{idle\_time}}{\text{transmission\_time}})$.

#### 2. Tính toán xác suất loại bỏ gói tin ($p_b$ và $p_a$)
RED thiết lập hai ngưỡng cấu hình:
- $min_{th}$: Ngưỡng tối thiểu (Minimum Threshold).
- $max_{th}$: Ngưỡng tối đa (Maximum Threshold, thường khuyến nghị $max_{th} \ge 2 \cdot min_{th}$ hoặc $3 \cdot min_{th}$).
- $max_p$: Xác suất loại bỏ tối đa tại ngưỡng $max_{th}$ (thường chọn $0.02 - 0.1$).

```
Xác suất Drop (P)
   1.0 |                                      /---------- (Drop 100%)
       |                                     /
 max_p |                           /--------/
       |                          / (Xác suất tuyến tính pb)
     0 +-------------------------+----------+-------------->
       0                      min_th      max_th           Dung lượng Buffer
```

**Quy tắc phân vùng trạng thái:**
1. **Vùng an toàn ($avg < min_{th}$):**
   - Không có nguy cơ nghẽn.
   - Xác suất loại bỏ: $P = 0$ (Chấp nhận 100% gói tin).
2. **Vùng cảnh báo ($min_{th} \le avg < max_{th}$):**
   - Nguy cơ tắc nghẽn chớm xuất hiện.
   - Tính xác suất nền tảng $p_b$ (tăng tuyến tính từ $0$ đến $max_p$): $p_b = max_p \cdot \frac{avg - min_{th}}{max_{th} - min_{th}}$

   - Điều chỉnh xác suất thực tế $p_a$ theo biến đếm gói $count$: $p_a = \frac{p_b}{1 - count \cdot p_b}$

     *(Biến $count$ đếm số gói tin liên tiếp được chấp nhận kể từ gói bị drop gần nhất. Khi $count$ tăng, $p_a$ tăng dần, đảm bảo khoảng cách giữa hai gói bị drop phân bố đều đặn, triệt tiêu hoàn toàn hiện tượng rớt gói chùm - bursty drops).*
3. **Vùng nghẽn nghiêm trọng ($avg \ge max_{th}$):**
   - Hàng đợi vượt ngưỡng an toàn.
   - Xác suất loại bỏ: $P = 1.0$ (Drop toàn bộ gói tin mới đến).

---

### 3.5. Đánh giá ưu nhược điểm của RED và các biến thể nâng cao

#### Ưu điểm vượt trội của RED
- **Xóa bỏ đồng bộ toàn cục:** Do drop gói ngẫu nhiên, chỉ một hoặc vài luồng TCP bị phạt tại một thời điểm, các luồng khác vẫn truyền bình thường.
- **Dung nạp lưu lượng bùng nổ (Burst Tolerance):** Nhờ cơ chế EWMA làm mượt, những đợt tăng gói tức thời không làm $avg$ tăng vọt ngay, giúp tránh drop gói oan uổng.
- **Duy trì độ trễ hàng đợi thấp:** Giữ kích thước hàng đợi trung bình lơ lửng quanh vùng $[min_{th}, max_{th}]$, giải quyết tận gốc hiện tượng full buffer delay.
- **Công bằng tương đối:** Xác suất một luồng bị drop gói tỷ lệ thuận với số lượng gói luồng đó bơm vào hàng đợi (luồng nào chiếm nhiều băng thông nhất sẽ bị drop nhiều nhất).

#### Nhược điểm của RED
- **Cực kỳ nhạy cảm với việc tinh chỉnh tham số:** Nếu chọn sai $(w_q, min_{th}, max_{th}, max_p)$, RED sẽ thoái hóa thành Drop Tail (nếu ngưỡng quá cao) hoặc gây lãng phí băng thông nghiêm trọng (nếu ngưỡng quá thấp).
- **Bất lực trước các luồng UDP bất hợp tác (Unresponsive Flows):** Gói UDP không giảm tốc độ khi bị drop, tiếp tục tràn ngập và chèn ép các luồng TCP tuân thủ luật chơi.

#### Các biến thể nâng cao của AQM
- **WRED (Weighted RED):** Dành cho mạng phân tầng chất lượng dịch vụ. Router duy trì các đường cong $(min_{th}, max_{th}, max_p)$ riêng biệt cho từng lớp lưu lượng (IP Precedence hoặc DSCP). Gói tin ưu tiên thấp sẽ có ngưỡng $min_{th}$ thấp hơn, bị drop sớm hơn gói ưu tiên cao.
- **FRED (Flow-based RED):** Theo dõi số lượng gói tin của từng luồng đang nằm trong buffer. Nếu một luồng gửi vượt quá hạn mức công bằng, FRED sẽ tăng mạnh xác suất drop của riêng luồng đó.
- **BLUE:** Thay vì đo độ dài hàng đợi, BLUE cập nhật xác suất drop $P_{drop}$ dựa trên hai sự kiện phần cứng trực tiếp:
  - Khi bộ đệm bị tràn (packet loss event) $\to P_{drop} = P_{drop} + \delta_1$.
  - Khi đường truyền bị rỗng hoàn toàn (link idle event) $\to P_{drop} = P_{drop} - \delta_2$.
- **CoDel (Controlled Delay - RFC 8289):**
  - Không đo số lượng gói tin mà đo trực tiếp **thời gian lưu lại trong hàng đợi (Sojourn Time)** của từng gói tin.
  - Nếu thời gian sojourn time tối thiểu trong một cửa sổ thời gian trượt `interval` (mặc định 100 ms) liên tục vượt quá ngưỡng `target` (mặc định 5 ms) $\to$ CoDel kích hoạt trạng thái drop gói với tần suất tăng dần theo tỷ lệ $1/\sqrt{n}$.
  - **FQ-CoDel (Fair Queuing CoDel - RFC 8290):** Kết hợp lập lịch công bằng luồng (Deficit Round Robin) với cơ chế quản lý trễ CoDel trên từng hàng đợi con. Hiện là tiêu chuẩn AQM tiên tiến nhất chống Bufferbloat trên Linux và macOS.

---

## PHẦN 4: CHUYÊN ĐỀ 3 - CHẤT LƯỢNG DỊCH VỤ (QUALITY OF SERVICE - QOS)

### 4.1. Bốn tham số cốt lõi đo lường QoS
Chất lượng dịch vụ (QoS) là tập hợp các công nghệ nhằm phân bổ tài nguyên mạng (băng thông, bộ đệm, thời gian xử lý) có kiểm soát cho các loại lưu lượng ứng dụng khác nhau.

Bốn tham số định lượng cơ bản của mạng IP:
1. **Băng thông (Bandwidth / Throughput):** Tốc độ truyền tải dữ liệu hữu ích tối đa qua đường truyền, đo bằng bps (bit per second).
2. **Độ trễ toàn trình (One-Way End-to-End Delay / Latency):**
Tổng thời gian một gói tin đi từ nguồn tới đích: $\text{Delay}_{\text{total}} = \text{Delay}_{\text{prop}} + \text{Delay}_{\text{trans}} + \text{Delay}_{\text{proc}} + \text{Delay}_{\text{queue}}$

   - $\text{Delay}_{\text{prop}} = \frac{d}{s}$: Trễ truyền lan vật lý ($d$ là cự ly cáp, $s \approx 2 \times 10^8\text{ m/s}$ trong sợi quang). Cố định, không thể tối ưu bằng phần mềm.
   - $\text{Delay}_{\text{trans}} = \frac{L}{R}$: Trễ phát tín hiệu ($L$ là kích thước gói, $R$ là tốc độ cổng).
   - $\text{Delay}_{\text{proc}}$: Trễ xử lý bên trong router (tra bảng FIB, kiểm tra checksum, cập nhật TTL). Rất nhỏ (vài micro-giây với phần cứng ASIC).
   - $\text{Delay}_{\text{queue}}$: **Trễ hàng đợi trong bộ đệm router.** Biến động mạnh nhất và là đối tượng can thiệp chính của các cơ chế QoS!
3. **Độ biến thiên trễ (Jitter / Delay Variation):**
   Sự chênh lệch về thời gian đến đích giữa các gói tin liên tiếp trong cùng một luồng. Cực kỳ nguy hại đối với cuộc gọi thoại thời gian thực (VoIP) và hội nghị truyền hình.
4. **Tỷ lệ mất gói (Packet Loss Rate):**
   Phần trăm gói tin bị rơi trên đường truyền do nghẽn bộ đệm router hoặc lỗi đường truyền vật lý.

---

### 4.2. Kỹ thuật điều hòa lưu lượng: Policing vs. Shaping
Một bộ điều hòa lưu lượng (Traffic Conditioner) đặt tại biên mạng gồm 4 khối chức năng:
- **Meter (Đo đạc):** Theo dõi tốc độ đến của luồng gói tin so với hồ sơ thỏa thuận dịch vụ (SLA).
- **Marker (Đánh dấu):** Thiết lập lại giá trị DSCP hoặc IP Precedence trên tiêu đề gói tin.
- **Shaper (Làm mượt):** Đệm các gói tin vượt ngưỡng và phát ra từ từ theo tốc độ quy định.
- **Dropper (Loại bỏ):** Tiêu hủy các gói tin vượt ngưỡng.

#### So sánh bản chất giữa Traffic Policing và Traffic Shaping

| Tiêu chí | Giám sát lưu lượng (Traffic Policing) | Định hình lưu lượng (Traffic Shaping) |
| :--- | :--- | :--- |
| **Hành vi với gói vượt ngưỡng** | Loại bỏ ngay lập tức (**Drop**) hoặc hạ bậc ưu tiên (**Remark**) | Giữ lại trong bộ đệm (**Buffer**) và phát ra đều đặn |
| **Độ trễ & Biến thiên trễ (Jitter)**| Không tạo thêm trễ (gói được đi ngay hoặc bị vứt bỏ) | Làm **tăng độ trễ** và tăng Jitter do thời gian xếp hàng trong bộ đệm |
| **Yêu cầu bộ nhớ đệm** | Không cần bộ đệm (No buffer required) | Yêu cầu bộ nhớ đệm lớn (Memory-intensive) |
| **Đặc tính lưu lượng đầu ra** | Vẫn có thể bùng nổ (giới hạn đỉnh gắt gao hình răng cưa)| Lưu lượng ra cực kỳ mượt mà, phẳng đều |
| **Tác động lên TCP** | Làm rớt gói $\to$ TCP kích hoạt retransmission & sụt giảm $cwnd$ | Giảm rớt gói $\to$ TCP duy trì tốc độ truyền ổn định |
| **Vị trí triển khai khuyến nghị**| Thường đặt tại **Cổng vào biên (Ingress Edge)** của ISP | Thường đặt tại **Cổng ra (Egress Interface)** của Doanh nghiệp |

---

### 4.3. Thuật toán Leaky Bucket (Thùng rò rỉ)
- **Hình tượng:** Một chiếc thùng có đáy bị đục một lỗ nhỏ với tốc độ rò rỉ cố định $r$. Dữ liệu đến có thể bùng nổ đổ ào ạt vào thùng.
- **Nguyên lý:**
  - Bộ đệm đóng vai trò thân thùng với dung lượng tối đa $B$.
  - Bất kể tốc độ gói tin đổ vào thùng thất thường thế nào, gói tin chỉ được phép rời khỏi đáy thùng với **tốc độ không đổi $r$ (constant rate)**.
  - Nếu dữ liệu đổ vào quá nhanh làm nước tràn qua miệng thùng ($q > B$), mọi gói tin mới đến tiếp theo đều bị loại bỏ ngay lập tức.
- **Đặc trưng:** Triệt tiêu hoàn toàn tính bùng nổ của lưu lượng; đầu ra là luồng dữ liệu đều đặn tuyệt đối (thích hợp cho các kênh truyền ATM hoặc mạng thoại TDM).

---

### 4.4. Thuật toán Token Bucket (Thùng thẻ bài)

#### Nguyên lý vận hành
- Một "thùng thẻ bài" có sức chứa tối đa $b$ thẻ (tokens).
- Các thẻ bài được tự động sinh ra và nạp vào thùng với tốc độ không đổi $r$ (tokens/giây). Nếu thùng đã đầy $b$ thẻ, thẻ mới sinh ra sẽ bị tràn và bỏ đi.
- Khi một gói tin có kích thước $L$ bytes đến:
  - Nếu trong thùng đang có $\ge L$ thẻ: Gói tin lập tức lấy đi $L$ thẻ và được phép truyền đi ngay qua giao diện với **tốc độ đường truyền tối đa $M$ (Maximum Transmission Rate / Peak Rate)**.
  - Nếu trong thùng không đủ thẻ: Gói tin bị coi là không tuân thủ (non-conforming). Tùy thuộc vào chính sách: gói sẽ bị drop / remark (Policing) hoặc phải nằm chờ trong hàng đợi cho đến khi có đủ thẻ mới được đi (Shaping).

```
Thẻ bài sinh ra (r tokens/sec)
        |
        v
    [=======]
    |       |   Thùng chứa tối đa b tokens
    |  ***  |
    [=======]
        |
        v (Cần L tokens)
Gói tin đến ---> [ Kiểm tra Thẻ ] ---> Gói tin đi (Tốc độ đỉnh M)
```

#### Công thức toán học quan trọng thi trắc nghiệm & tự luận
Giả sử thùng đang đầy ắp $b$ tokens, một đợt bùng nổ lưu lượng dữ liệu khổng lồ ập đến và được phát đi với tốc độ tối đa của đường truyền $M$ ($M > r$).

1. **Thời gian bùng nổ tối đa (Maximum Burst Duration - $T$):**
   Trong khoảng thời gian $T$, tổng số token tiêu thụ bằng tổng số token có sẵn ban đầu ($b$) cộng với số token mới sinh ra trong thời gian đó ($r \cdot T$): $b + r \cdot T = M \cdot T \implies T = \frac{b}{M - r}$

2. **Tổng lượng dữ liệu tối đa truyền được trong đợt bùng nổ ($S$):** $S = M \cdot T = \frac{b \cdot M}{M - r}$

> **So sánh then chốt:** Leaky Bucket ép tốc độ ra luôn bằng hằng số $r$ (không cho phép burst). Token Bucket cho phép lưu lượng **truyền bùng nổ ở tốc độ cực đại $M$** trong thời gian ngắn $T$, nhưng kiểm soát tốc độ truyền trung bình trong dài hạn không vượt quá $r$.

---

### 4.5. Cơ chế đánh dấu màu srTCM và trTCM

#### 1. srTCM (Single Rate Three Color Marker - RFC 2697)
- Cấu hình 1 tốc độ và 2 kích thước thùng:
  - $CIR$ (Committed Information Rate): Tốc độ cam kết.
  - $CBS$ (Committed Burst Size): Thùng thẻ $C$ (tối đa $CBS$).
  - $EBS$ (Excess Burst Size): Thùng thẻ $E$ (tối đa $EBS$).
- Thẻ sinh ra với tốc độ $CIR$. Nạp đầy thùng $C$ trước, thẻ thừa nạp tiếp vào thùng $E$.
- **Quy tắc phân màu gói tin:**
  - **Màu Xanh (Green):** Đủ thẻ trong thùng $C$ (trừ thẻ ở thùng $C$). Gói tuân thủ hoàn toàn SLA.
  - **Màu Vàng (Yellow):** Thiếu thẻ ở thùng $C$ nhưng đủ thẻ ở thùng $E$ (trừ thẻ ở thùng $E$). Gói vượt cam kết nhưng còn trong giới hạn dư thừa cho phép.
  - **Màu Đỏ (Red):** Cả hai thùng đều không đủ thẻ. Gói vi phạm nghiêm trọng, bị drop đầu tiên khi nghẽn mạng.

#### 2. trTCM (Two Rate Three Color Marker - RFC 2698)
- Cấu hình 2 tốc độ độc lập và 2 kích thước thùng:
  - $PIR$ (Peak Information Rate) & $PBS$ (Peak Burst Size) cho thùng $P$.
  - $CIR$ (Committed Information Rate) & $CBS$ (Committed Burst Size) cho thùng $C$ ($PIR \ge CIR$).
- Thùng $P$ nhận thẻ ở tốc độ $PIR$; thùng $C$ nhận thẻ ở tốc độ $CIR$.
- **Quy tắc phân màu:**
  - Nếu gói tin vượt quá $PIR/PBS \to$ **Màu Đỏ**.
  - Nếu gói không vượt $PIR$ nhưng vượt quá $CIR/CBS \to$ **Màu Vàng**.
  - Nếu gói nằm trong cả $CIR$ và $PIR \to$ **Màu Xanh**.

---

### 4.6. Các cơ chế lập lịch gói tin (Packet Scheduling Disciplines)
Khi hàng đợi chứa nhiều gói tin từ các luồng khác nhau, bộ lập lịch (Scheduler) quyết định **gói tin nào được phát đi tiếp theo**.

1. **FIFO (First-In First-Out):**
   - Đơn giản nhất, không có khái niệm ưu tiên hay phân loại. Luồng gửi nhanh sẽ chiếm dụng toàn bộ đường truyền.
2. **Priority Queuing (PQ):**
   - Phân chia thành nhiều hàng đợi có mức ưu tiên cố định (High, Medium, Normal, Low).
   - Bộ lập lịch luôn vét cạn gói trong hàng đợi High trước; chỉ khi High rỗng mới chuyển sang phục vụ Medium; tương tự với Normal và Low.
   - **Nhược điểm chí mạng:** Gây đói tài nguyên vĩnh viễn (**Starvation**) cho các hàng đợi ưu tiên thấp nếu hàng đợi ưu tiên cao liên tục có gói đến.
3. **Fair Queuing (FQ):**
   - Giả lập cơ chế Generalized Processor Sharing (GPS) - phân chia băng thông công bằng bit-by-bit giữa các luồng hoạt động.
4. **Weighted Fair Queuing (WFQ):**
   - Gán cho mỗi luồng $i$ một trọng số $w_i$ (trong thiết bị Cisco, trọng số tự động gán theo giá trị IP Precedence: $w_i = \text{IP\_Precedence} + 1$).
   - Tính toán **Thời gian hoàn thành ảo (Virtual Finish Time - $F_i^k$)** cho gói tin thứ $k$ của luồng $i$: $F_i^k = \max(F_i^{k-1}, V(a_i^k)) + \frac{L_i^k}{w_i}$

     *(với $a_i^k$ là thời điểm gói đến, $L_i^k$ là độ dài gói, $V(t)$ là thời gian ảo của hệ thống).*
   - **Nguyên tắc phát:** Gói tin nào có giá trị $F$ nhỏ nhất trong tất cả các hàng đợi sẽ được phát ra trước. Đảm bảo luồng có trọng số lớn hơn hoặc gói tin ngắn hơn sẽ được ưu tiên chuyển tiếp nhanh hơn.
5. **Deficit Round Robin (DRR - Shreedhar & Varghese 1996):**
   - Giải thuật lập lịch công bằng với độ phức tạp tính toán siêu nhẹ $O(1)$ cho gói tin có chiều dài biến động.
   - Mỗi hàng đợi được cấp một lượng hạn mức `Quantum` mỗi vòng. Sử dụng biến đếm thâm hụt `DeficitCounter`:
     - Khi đến lượt hàng đợi: $\text{DeficitCounter} = \text{DeficitCounter} + \text{Quantum}$.
     - Nếu $\text{DeficitCounter} \ge \text{PacketLength}$: Gói tin được phát và $\text{DeficitCounter} = \text{DeficitCounter} - \text{PacketLength}$. Quá trình lặp lại cho gói tiếp theo nếu hạn mức vẫn còn đủ.
     - Nếu không đủ: Giữ nguyên số dư `DeficitCounter` cho vòng lặp tiếp theo và chuyển sang hàng đợi kế bên.
6. **Low Latency Queuing (LLQ):**
   - Kết hợp hoàn hảo giữa **Strict Priority (PQ)** và **Class-Based Weighted Fair Queuing (CBWFQ)**.
   - Lưu lượng thoại VoIP nhạy cảm với trễ được đưa vào hàng đợi Priority (được phục vụ trước tiên nhưng bị kiểm soát trần bằng Policing để chống tràn); các loại lưu lượng dữ liệu khác được phân vào các lớp CBWFQ với tỷ lệ phần trăm băng thông được bảo đảm.

---

### 4.7. Mô hình dịch vụ tích hợp IntServ & Giao thức RSVP
- **Tiêu chuẩn:** IETF RFC 1633.
- **Triết lý:** Bảo đảm chất lượng dịch vụ nghiêm ngặt theo **từng luồng đơn lẻ (Per-flow QoS)**. Mỗi luồng muốn truyền phải thực hiện "Báo hiệu đặt chỗ trước tài nguyên" dọc theo toàn bộ tuyến đường từ nguồn đến đích trước khi gửi dữ liệu thật.

#### Giao thức RSVP (Resource Reservation Protocol - RFC 2205)
1. Máy nguồn gửi bản tin **RSVP PATH** xuôi dòng (downstream) đến máy đích. Bản tin PATH mang theo thông số **TSpec (Traffic Specification)** mô tả đặc trưng luồng dữ liệu cần phát:
   - $r$: Tốc độ sinh token (token rate).
   - $b$: Dung lượng thùng token (bucket depth).
   - $p$: Tốc độ đỉnh (peak rate).
   - $m$: Kích thước gói tối thiểu (minimum policed unit).
   - $M$: Kích thước gói tối đa (maximum packet size).
2. Máy đích nhận được PATH, tính toán tài nguyên cần thiết và gửi ngược bản tin **RSVP RESV** ngược dòng (upstream) theo đúng tuyến đường mà PATH đã đi qua. Bản tin RESV mang theo thông số **RSpec (Reservation Specification)**:
   - $R$: Băng thông yêu cầu dành riêng.
   - $S$: Giới hạn độ trễ (slack term).
3. Mỗi router dọc đường nhận được RESV sẽ thực hiện **Kiểm tra chấp nhận (Admission Control)**:
   - Nếu đủ tài nguyên: Khóa tài nguyên lại cho luồng đó và chuyển tiếp RESV về phía nguồn.
   - Nếu không đủ tài nguyên: Từ chối kết nối, hủy đặt chỗ và gửi báo lỗi về.

#### Ba kiểu đặt chỗ của RSVP (Reservation Styles)
1. **Wildcard-Filter (WF):** Đặt chỗ chung cho tất cả các nguồn phát gửi tới đích (thường dùng trong truyền hình trực tiếp, broadcast).
2. **Fixed-Filter (FF):** Đặt chỗ cố định riêng biệt cho đúng một nguồn phát xác định cụ thể (Point-to-Point).
3. **Shared-Explicit (SE):** Cho phép một nhóm các nguồn phát đã chỉ định cụ thể cùng chia sẻ một hạn mức tài nguyên đặt chỗ chung.

#### Hai lớp dịch vụ của IntServ
- **Guaranteed Service (RFC 2212):** Cam kết cứng tuyệt đối: Đảm bảo băng thông, chặn cận trên độ trễ chắc chắn, **tỷ lệ mất gói bằng 0** (không có packet loss do nghẽn).
- **Controlled-Load Service (RFC 2211):** Cung cấp chất lượng truyền tải tương đương với một mạng IP hoàn toàn không bị tải (gần như không trễ hàng đợi và mất gói rất thấp), thích hợp cho các ứng dụng đa phương tiện thích ứng được.

#### Tại sao IntServ thất bại trên Internet công cộng?
- **Khả năng mở rộng cực kém (Scalability Nightmare):** Mọi router lõi (Core Router) đều phải lưu trữ và duy trì thông tin trạng thái đặt chỗ (Per-flow state) của hàng triệu luồng kết nối đồng thời $\to$ bùng nổ bảng trạng thái, làm quá tải bộ nhớ và CPU.
- **Cơ chế Soft-State tốn kém:** Các bên phải liên tục gửi lại bản tin PATH và RESV định kỳ (mỗi 30s) để làm mới trạng thái (Refresh State); nếu mất kết nối thì timeout tự hủy $\to$ lãng phí băng thông báo hiệu.

---

### 4.8. Mô hình dịch vụ phân biệt DiffServ & Trường DSCP
- **Tiêu chuẩn:** IETF RFC 2474, RFC 2475.
- **Triết lý:** Thay thế việc theo dõi từng luồng phức tạp của IntServ bằng phương pháp **Gom nhóm theo lớp hành vi (Behavior Aggregation)**:
  - **Tại biên mạng (Edge Routers):** Thực hiện các tác vụ nặng nhọc: phân loại luồng (Classification), đo đạc (Metering), đánh dấu mã lớp (Marking vào IP Header), và điều hòa lưu lượng (Policing/Shaping).
  - **Tại lõi mạng (Core Routers):** Hoàn toàn **không lưu trữ trạng thái luồng (Stateless)**! Router lõi chỉ nhìn vào nhãn mã hóa trong tiêu đề gói tin và thực thi ngay hành vi chuyển tiếp từng chặng tương ứng (**Per-Hop Behavior - PHB**). Cực kỳ nhẹ tải và mở rộng không giới hạn!

#### Cấu trúc trường DS (Differentiated Services Field)
Trường ToS (Type of Service) trong IPv4 Header hoặc Traffic Class trong IPv6 Header (8 bits) được IETF định nghĩa lại thành **DS Field**:

```
+---+---+---+---+---+---+---+---+
|           DSCP        |  ECN  |
+---+---+---+---+---+---+---+---+
  0   1   2   3   4   5   6   7
```
- **DSCP (Differentiated Services Code Point - 6 bits đầu):** Cung cấp $2^6 = 64$ giá trị mã dịch vụ khác nhau.
- **ECN (Explicit Congestion Notification - 2 bits cuối):** Dùng để báo hiệu tắc nghẽn chủ động.

#### Khả năng tương thích ngược: IP Precedence & Class Selector (CS)
- Thời kỳ cũ, IPv4 sử dụng 3 bit đầu của ToS làm **IP Precedence** (từ 0 đến 7):
  - 0: Routine (Bình thường)
  - 1: Priority
  - 2: Immediate
  - 3: Flash
  - 4: Flash Override
  - 5: Critical (Thoại)
  - 6: Internetwork Control
  - 7: Network Control
- **Class Selector (CS0 đến CS7):** Để tương thích ngược với các thiết bị cũ chỉ đọc 3-bit IP Precedence, DiffServ định nghĩa các giá trị DSCP dạng `xxx000`:
  - $CS0 = 000000_2 = 0$ (tương đương IP Prec 0)
  - $CS1 = 001000_2 = 8$ (tương đương IP Prec 1)
  - $CS2 = 010000_2 = 16$ (tương đương IP Prec 2)
  - $CS3 = 011000_2 = 24$ (tương đương IP Prec 3)
  - $CS4 = 100000_2 = 32$ (tương đương IP Prec 4)
  - $CS5 = 101000_2 = 40$ (tương đương IP Prec 5)
  - $CS6 = 110000_2 = 48$ (tương đương IP Prec 6)
  - $CS7 = 111000_2 = 56$ (tương đương IP Prec 7)

---

### 4.9. Các nhóm hành vi chuyển tiếp từng chặng (PHB)

#### 1. Default Forwarding (DF PHB)
- Giá trị DSCP: `000000` (Thập phân: **0**).
- Cung cấp dịch vụ **Best-Effort** truyền thống: Xếp hàng FIFO, khi nghẽn thì Drop Tail hoặc RED cơ bản.

#### 2. Expedited Forwarding (EF PHB - RFC 3246)
- Giá trị DSCP: `101110` (Thập phân: **46**).
- Mục đích: Cung cấp dịch vụ tương đương đường dây thuê riêng (Leased Line): Băng thông bảo đảm tối đa, độ trễ cực thấp, jitter cực thấp, tỷ lệ mất gói gần như bằng 0.
- Được chỉ định bắt buộc cho **Lưu lượng thoại VoIP (Voice Payload)**.
- Triển khai: Đưa vào hàng đợi ưu tiên nghiêm ngặt (Strict Priority Queue trong LLQ) kết hợp với Traffic Policing để ngăn luồng EF chiếm dụng đường truyền của các lớp khác.

#### 3. Assured Forwarding (AF PHB - RFC 2597)
Cung cấp dịch vụ chuyển tiếp có bảo đảm với 4 lớp dịch vụ độc lập (**Class 1 đến Class 4**). Trong mỗi lớp lại phân chia thành 3 mức độ ưu tiên loại bỏ gói (**Drop Precedence 1, 2, 3**: Thấp, Trung bình, Cao).

**Cấu trúc nhị phân của DSCP nhóm AF:** $[a_1 a_2 a_3] \; [d_1 d_2] \; [0]$

- 3 bit đầu $[a_1 a_2 a_3]$ xác định **Lớp dịch vụ (Class 1-4)**:
  - Class 1: `001`
  - Class 2: `010`
  - Class 3: `011`
  - Class 4: `100` (Class 4 được cấp nhiều tài nguyên băng thông nhất).
- 2 bit tiếp theo $[d_1 d_2]$ xác định **Xác suất loại bỏ gói khi nghẽn (Drop Precedence)**:
  - Drop Precedence 1 (Thấp - Khó bị rớt nhất): `01`
  - Drop Precedence 2 (Trung bình): `10`
  - Drop Precedence 3 (Cao - Bị drop đầu tiên khi nghẽn): `11`
- Bit cuối cùng luôn luôn là `0`.

#### Bảng tra cứu toàn diện 12 giá trị DSCP nhóm AF

| Lớp dịch vụ | Drop Precedence 1 (Thấp) | Drop Precedence 2 (Trung bình) | Drop Precedence 3 (Cao) |
| :--- | :--- | :--- | :--- |
| **Class 1** | **AF11** = `001 01 0` = **10** | **AF12** = `001 10 0` = **12** | **AF13** = `001 11 0` = **14** |
| **Class 2** | **AF21** = `010 01 0` = **18** | **AF22** = `010 10 0` = **20** | **AF23** = `010 11 0` = **22** |
| **Class 3** | **AF31** = `011 01 0` = **26** | **AF32** = `011 10 0` = **28** | **AF33** = `011 11 0` = **30** |
| **Class 4** | **AF41** = `100 01 0` = **34** | **AF42** = `100 10 0` = **36** | **AF43** = `100 11 0` = **38** |

> **Cách phối hợp WRED và AF PHB:** Khi bộ đệm xảy ra nguy cơ nghẽn, cơ chế WRED sẽ bắt đầu drop các gói tin có mức Drop Precedence cao nhất trước (ví dụ AF13 bị drop trước AF12, và AF11 được bảo vệ an toàn đến cuối cùng).

---

### 4.10. Bảng đối chiếu toàn diện: IntServ vs. DiffServ

| Đặc tính | IntServ (Integrated Services) | DiffServ (Differentiated Services) |
| :--- | :--- | :--- |
| **Tiêu chuẩn IETF** | RFC 1633, RFC 2205 | RFC 2474, RFC 2475 |
| **Mức độ kiểm soát** | Từng luồng đơn lẻ (Per-flow granularity) | Nhóm tập hợp theo lớp (Per-class aggregation) |
| **Giao thức báo hiệu**| Bắt buộc dùng **RSVP** báo hiệu đặt chỗ trước | **Không dùng giao thức báo hiệu** (No signaling) |
| **Bảo đảm chất lượng**| Cam kết tuyệt đối về băng thông và cận trễ (Hard QoS)| Bảo đảm tương đối theo mức độ ưu tiên (Soft QoS) |
| **Trạng thái router lõi**| Duy trì trạng thái của mọi luồng (**Stateful**) | Hoàn toàn không lưu trạng thái luồng (**Stateless**) |
| **Khả năng mở rộng** | **Rất kém** ($O(N)$ luồng $\to$ nghẽn router lõi) | **Vô cùng xuất sắc** (Chỉ phụ thuộc số lớp PHB) |
| **Phân loại gói tin** | Mọi router trên đường truyền đều phải kiểm tra | Chỉ thực hiện phân loại và đánh dấu tại Router biên |
| **Phạm vi ứng dụng** | Mạng quy mô nhỏ, phòng thu phát video chuyên dụng| **Toàn bộ hạ tầng mạng Internet và ISP toàn cầu** |

---

## PHẦN 5: CHUYÊN ĐỀ 4 - ĐIỀU KHIỂN ĐỊNH TUYẾN INTERNET (INTERNET ROUTING)

### 5.1. Khái niệm Routing vs. Forwarding & Cấu trúc Bảng định tuyến

| Khái niệm | Định tuyến (Routing - Control Plane) | Chuyển tiếp (Forwarding - Data Plane) |
| :--- | :--- | :--- |
| **Bản chất** | Quá trình tính toán, trao đổi thông tin để tìm ra đường đi toàn cục từ nguồn đến đích | Quá trình đẩy một gói tin cụ thể từ cổng vào sang cổng ra thích hợp trên router |
| **Phạm vi** | Toàn mạng (Network-wide logic) | Cục bộ trên từng router (Per-router local action) |
| **Bảng dữ liệu** | **Bảng định tuyến (RIB - Routing Information Base):** Chứa tất cả các tuyến đường học được từ mọi giao thức | **Bảng chuyển tiếp (FIB - Forwarding Information Base):** Bảng tinh gọn nạp vào phần cứng TCAM tốc độ cao |
| **Thời gian xử lý**| Chạy ở chế độ nền (giây hoặc mili-giây) | Xử lý theo thời gian thực ở tốc độ đường truyền (nano-giây / micro-giây) |

---

### 5.2. Nguyên lý khớp tiền tố dài nhất (Longest Prefix Match - LPM)
Khi một gói tin IP đến router, router sẽ so sánh địa chỉ IP đích với các mục trong bảng định tuyến:
- Nếu địa chỉ IP đích khớp với nhiều mạng con khác nhau, router **BẮT BUỘC** phải chọn tuyến đường có **Subnet Mask dài nhất (nhiều bit 1 nhất - tiền tố cụ thể nhất)** để chuyển tiếp gói tin!
- *Ví dụ kinh điển:*
  - Tuyến 1: `192.168.1.0/24`
  - Tuyến 2: `192.168.1.128/25`
  - Tuyến 3: `0.0.0.0/0` (Default route)
  - Gói tin có IP đích `192.168.1.130` sẽ khớp với cả 3 tuyến trên, nhưng router **bắt buộc chọn Tuyến 2 (`/25`)** vì nó có tiền tố dài nhất (25 bits so với 24 bits và 0 bit).

---

### 5.3. Administrative Distance (AD) & Bảng tra chuẩn Cisco
Khi router học được cùng một mạng đích từ **nhiều nguồn định tuyến khác nhau**, router sẽ căn cứ vào **Độ tin cậy của nguồn (Administrative Distance - AD)** để chọn duy nhất tuyến đường tốt nhất cài vào bảng định tuyến:
- **Nguyên tắc:** **Giá trị AD càng nhỏ càng được ưu tiên!** (AD = 0 là tin cậy tuyệt đối; AD = 255 là không bao giờ tin cậy).

#### Bảng tra cứu Administrative Distance chuẩn Cisco (Bắt buộc học thuộc)

| Nguồn định tuyến (Routing Source) | Giá trị Administrative Distance (AD) |
| :--- | :--- |
| **Connected Interface (Liên kết trực tiếp)** | **0** |
| **Static Route (Tuyến tĩnh)** | **1** |
| **eBGP (BGP đối ngoại)** | **20** |
| **EIGRP (Internal - Nội miền)** | **90** |
| **OSPF** | **110** |
| **IS-IS** | **115** |
| **RIP (RIPv1 & RIPv2)** | **120** |
| **EIGRP (External - Ngoại miền)** | **170** |
| **iBGP (BGP đối nội)** | **200** |
| **Unreachable / Unknown** | **255** (Không bao giờ cài vào bảng định tuyến) |

> **Phân biệt AD và Metric:**
> - **AD:** Dùng để so sánh giữa **CÁC GIAO THỨC KHÁC NHAU** (Ví dụ: Tuyến học qua OSPF (AD=110) sẽ luôn thắng tuyến học qua RIP (AD=120) bất kể metric là bao nhiêu).
> - **Metric:** Dùng để so sánh giữa các đường đi trong **CÙNG MỘT GIAO THỨC** (Ví dụ: Trong RIP so sánh số hop; trong OSPF so sánh tổng Cost).

---

### 5.4. Định tuyến tĩnh (Static Routing)
- **Ưu điểm:** Tiết kiệm băng thông (không gửi gói tin cập nhật định kỳ), bảo mật cao (người ngoài không thể can thiệp bảng định tuyến), nhẹ CPU router.
- **Nhược điểm:** Phải cấu hình thủ công từng thiết bị; không tự động thích ứng khi mạng có sự cố đứt cáp.
- **Cú pháp Cisco:**
  `Router(config)# ip route <network-address> <subnet-mask> {next-hop-ip | exit-interface} [distance]`

#### Ba dạng tuyến tĩnh quan trọng
1. **Standard Static Route:** Chỉ định đường đi tới một mạng cụ thể.
2. **Default Static Route (Tuyến mặc định):**
   `Router(config)# ip route 0.0.0.0 0.0.0.0 {next-hop-ip | exit-interface}`
   Khớp với mọi địa chỉ đích khi không có mục nào khác trong bảng định tuyến khớp (Gateway of Last Resort).
3. **Floating Static Route (Tuyến tĩnh dự phòng):**
   Cấu hình tuyến tĩnh với giá trị AD lớn hơn AD của giao thức định tuyến động đang chạy (Ví dụ: `ip route 10.0.0.0 255.0.0.0 192.168.1.2 130` để dự phòng cho OSPF có AD=110). Khi đường OSPF bình thường, tuyến tĩnh này bị ẩn; khi đường OSPF chết, tuyến tĩnh lập tức nổi lên thay thế.

---

### 5.5. Phân loại Giao thức Định tuyến Động

```
                             [ Giao thức Định tuyến ]
                                        |
         +------------------------------+------------------------------+
         |                                                             |
   [ IGP - Nội miền ]                                            [ EGP - Liên miền ]
   (Trong cùng 1 AS)                                            (Giữa các AS khác nhau)
         |                                                             |
   +-----+--------------------+                                        |
   |                          |                                        |
[ Distance Vector ]     [ Link-State ]                           [ Path Vector ]
- RIPv1, RIPv2          - OSPF                                   - BGPv4
- EIGRP (Advanced DV)   - IS-IS
```

---

### 5.6. Giao thức Distance Vector & Hiện tượng Routing Loops

#### Bản chất Distance Vector (Thuật toán Bellman-Ford)
- "Định tuyến theo tin đồn (Routing by rumor)": Router chỉ biết mạng thông qua thông tin láng giềng kể lại, hoàn toàn không có sơ đồ tổng thể toàn mạng.
- Định kỳ gửi toàn bộ bảng định tuyến cho các router láng giềng trực tiếp.

#### Hiện tượng Đếm đến vô cùng (Count-to-Infinity Problem)
Giả sử có topology dạng chuỗi: `Network 1 --- [Router A] --- [Router B] --- [Router C] --- [Router D]`
1. Ban đầu: Router A cách Network 1 là 1 hop, B cách 2 hops, C cách 3 hops, D cách 4 hops.
2. **Sự cố đứt liên kết:** Liên kết giữa Router A và Network 1 bị đứt. Router A nhận biết Network 1 bị hỏng.
3. Tuy nhiên, trước khi A kịp gửi thông báo cập nhật, Router C gửi bản tin định kỳ cho B: *"Tôi có đường tới Network 1 với chi phí 3 hops"*.
4. Router B nhận tin, nghĩ rằng: *"À, đi qua C tới được Network 1 mất 3 hops, vậy mình đi qua C sẽ mất 3 + 1 = 4 hops!"*. B cập nhật bảng định tuyến: Network 1 đi qua C (4 hops).
5. Tiếp theo, B quảng bá đường đi 4 hops này cho A. Router A thấy đường trực tiếp hỏng, liền cập nhật: Network 1 đi qua B (5 hops).
6. A lại quảng bá cho B $\to$ B tăng lên 6 hops $\to$ C cập nhật lên 7 hops $\to$ D cập nhật lên 8 hops...
7. Giá trị metric cứ thế tăng dần qua từng chu kỳ cho đến vô tận!
8. **Hậu quả:** Gói tin gửi tới Network 1 bị luân chuyển vòng tròn vô tận giữa các router (Routing Loop), làm nghẽn băng thông, tràn CPU và router bị sập.

---

### 5.7. Năm cơ chế phòng chống Routing Loops trong Distance Vector

1. **Định nghĩa bước nhảy tối đa (Defining Maximum Hop Count / Maximum Metric):**
   - Đặt một cận trên giới hạn giá trị vô cùng. Đối với RIP, **Infinity = 16 hops**.
   - Khi metric của một tuyến đường tăng chạm ngưỡng 16, mạng đó lập tức bị đánh dấu là **Unreachable (Không thể tiếp cận)** và bị loại bỏ khỏi bảng định tuyến, ngăn chặn vòng lặp tăng vô tận.
2. **Luật Split Horizon (Đường chân trời chia đôi):**
   - **Quy tắc vàng:** *"Không bao giờ quảng bá ngược lại thông tin về một tuyến đường ra chính cổng giao tiếp mà router đã học được tuyến đường đó!"*
   - *Tác dụng:* Router B học được đường tới Network 1 từ cổng nối với A $\to$ B sẽ không bao giờ phát ngược lại đường tới Network 1 cho A.
3. **Poison Reverse (Split Horizon with Poison Reverse):**
   - Thay vì im lặng không gửi như Split Horizon thuần túy, router vẫn gửi lại thông tin về tuyến đường đó ra cổng đã học, nhưng gán thẳng giá trị metric bằng **Vô cùng (16 đối với RIP)**.
   - *Tác dụng:* Xác nhận dứt khoát và tức thời rằng router này không thể là đường đi dự phòng ngược lại cho láng giềng.
4. **Bộ đếm Hold-down Timers:**
   - Khi một router nhận được thông tin rằng một mạng đang bị sự cố (Unreachable), router sẽ đưa mạng đó vào trạng thái "tạm khóa" (Hold-down state) trong một khoảng thời gian quy định (RIP mặc định là **180 giây**).
   - Trong suốt thời gian này, router **phớt lờ mọi thông tin cập nhật mới** về mạng đó nếu thông tin mới có metric bằng hoặc xấu hơn metric cũ. Chỉ chấp nhận thông tin nếu có router báo một đường đi tốt hơn rõ rệt.
   - *Tác dụng:* Cho phép toàn bộ mạng có đủ thời gian để nhận thông tin hỏng và hội tụ ổn định, tránh bị lừa bởi các gói tin định tuyến cũ lạc hậu trôi nổi trên mạng.
5. **Cập nhật kích hoạt ngay lập tức (Triggered Updates):**
   - Thông thường RIP gửi cập nhật định kỳ mỗi 30 giây.
   - Khi có sự cố đứt mạng xảy ra, router phát hiện sự cố sẽ **lập tức gửi ngay một bản tin cập nhật đột xuất** (không đợi hết đồng hồ 30s) lan truyền ra toàn mạng.
   - *Tác dụng:* Tăng tốc độ hội tụ mạng lên gấp nhiều lần, dập tắt nguy cơ hình thành vòng lặp trước khi các bản tin định kỳ kịp gây rối.

---

### 5.8. Giao thức RIP (Routing Information Protocol)

#### So sánh chi tiết RIPv1 vs. RIPv2

| Đặc tính | RIPv1 (RFC 1058) | RIPv2 (RFC 2453) |
| :--- | :--- | :--- |
| **Loại định tuyến** | **Classful** (Có lớp: A, B, C) | **Classless** (Không phân lớp) |
| **Gửi Subnet Mask** | **KHÔNG** gửi kèm subnet mask trong bản tin | **CÓ** gửi kèm subnet mask đầy đủ |
| **Hỗ trợ VLSM / CIDR**| **KHÔNG hỗ trợ** | **HỖ TRỢ ĐẦY ĐỦ** VLSM và CIDR |
| **Phương thức truyền** | **Broadcast** (`255.255.255.255`) | **Multicast** (`224.0.0.9`) |
| **Xác thực (Authentication)**| Không hỗ trợ xác thực | Hỗ trợ xác thực mật khẩu Plain-text & **MD5** |
| **Tự động gom cụm** | Bắt buộc gom cụm về ranh giới lớp mạng | Cho phép tắt bằng lệnh `no auto-summary` |
| **Metric tối đa** | 15 hops (16 = Unreachable) | 15 hops (16 = Unreachable) |

#### Bốn bộ đếm thời gian (Timers) của RIP
- **Update Timer (30 giây):** Chu kỳ phát bản tin cập nhật bảng định tuyến ra các cổng.
- **Invalid Timer (180 giây):** Nếu sau 180s không nhận được tin cập nhật về một tuyến đường, tuyến đó bị đánh dấu là hỏng (metric = 16).
- **Holddown Timer (180 giây):** Thời gian tạm khóa phớt lờ các thông tin cập nhật kém hơn.
- **Flush Timer (240 giây):** Thời gian xóa sổ hoàn toàn tuyến đường hỏng ra khỏi bảng định tuyến.

#### Các lệnh cấu hình thực hành RIPv2 chuẩn trên Cisco IOS
```cisco
Router(config)# router rip
Router(config-router)# version 2
Router(config-router)# no auto-summary
Router(config-router)# network 192.168.1.0
Router(config-router)# network 10.0.0.0
Router(config-router)# passive-interface FastEthernet0/0   ! Không gửi update ra mạng LAN có người dùng
Router(config-router)# default-information originate      ! Quảng bá default route cho toàn mạng RIP
```

---

### 5.9. Giao thức Link-State OSPF (Open Shortest Path First)

#### Nguyên lý vận hành cốt lõi (Thuật toán Dijkstra)
Khác hoàn toàn với Distance Vector, trong Link-State:
1. Mỗi router khám phá các láng giềng trực tiếp và trạng thái liên kết (Link-State).
2. Phát tán thông tin trạng thái liên kết (**LSA - Link-State Advertisement**) cho toàn bộ các router khác trong vùng bằng giải thuật Flooding tin cậy.
3. Mọi router trong cùng một Area đều sở hữu một **Cơ sở dữ liệu trạng thái liên kết (LSDB - Link-State Database) HOÀN TOÀN GIỐNG HỆT NHAU**.
4. Mỗi router độc lập lấy chính mình làm gốc, áp dụng **Thuật toán Dijkstra (Shortest Path First - SPF)** lên LSDB để tính toán cây đường đi ngắn nhất không vòng lặp (Loop-free Shortest Path Tree).

#### Năm loại gói tin OSPF (OSPF Packet Types)
1. **Type 1 - Hello:** Thiết lập và duy trì mối quan hệ láng giềng (Neighbor Adjacency).
2. **Type 2 - DBD (Database Description):** Tóm tắt nội dung của LSDB để đồng bộ hóa.
3. **Type 3 - LSR (Link-State Request):** Yêu cầu láng giềng gửi chi tiết các LSA còn thiếu.
4. **Type 4 - LSU (Link-State Update):** Gói tin mang theo các LSA thực tế (trả lời cho LSR).
5. **Type 5 - LSAck (Link-State Acknowledgement):** Xác nhận đã nhận LSU an toàn.

#### Bảy trạng thái láng giềng OSPF (Neighbor States)
`Down` $\to$ `Init` $\to$ `2-Way` (Bầu chọn DR/BDR) $\to$ `ExStart` $\to$ `Exchange` $\to$ `Loading` $\to$ `Full` (Đồng bộ LSDB hoàn tất).

#### Bầu chọn DR (Designated Router) & BDR (Backup Designated Router)
- **Mục đích:** Trên các mạng Broadcast đa truy cập (như Ethernet LAN kết nối nhiều router), nếu $N$ router cùng thiết lập quan hệ láng giềng với nhau sẽ sinh ra $\frac{N(N-1)}{2}$ mối quan hệ, gây bão gói tin LSA. OSPF giải quyết bằng cách chỉ định 1 DR và 1 BDR. Tất cả các router khác (DROther) chỉ thiết lập quan hệ `Full` với DR và BDR.
- **Địa chỉ Multicast OSPF:**
  - `224.0.0.5` (**AllSPFRouters**): Tất cả các router OSPF đều lắng nghe.
  - `224.0.0.6` (**AllDRouters**): Chỉ có DR và BDR lắng nghe (DROther gửi LSU tới địa chỉ này).
- **Quy tắc bầu chọn DR/BDR:**
  1. Router có **OSPF Priority cao nhất** thắng (Mặc định Priority = 1; nếu Priority = 0 thì không bao giờ tham gia bầu chọn).
  2. Nếu Priority bằng nhau: Router có **Router ID (RID) lớn nhất** sẽ thắng!
- **Thứ tự xác định Router ID (RID):**
  1. Lệnh cấu hình thủ công: `Router(config-router)# router-id X.X.X.X` (Ưu tiên số 1).
  2. Địa chỉ IPv4 cao nhất trong số các cổng ảo **Loopback** đang active.
  3. Địa chỉ IPv4 cao nhất trong số các cổng **vật lý (Physical)** đang active.

#### Khái niệm Phân vùng (OSPF Areas) & Cách tính Cost
- **Area 0 (Backbone Area):** Vùng xương sống bắt buộc. Mọi vùng non-backbone (Area 1, Area 2...) đều phải có kết nối vật lý hoặc logic (Virtual Link) trực tiếp vào Area 0.
- **Router biên vùng (ABR - Area Border Router):** Router có cổng nằm ở ít nhất hai vùng khác nhau (kết nối Area non-backbone vào Area 0).
- **Router biên AS (ASBR - Autonomous System Boundary Router):** Router kết nối mạng OSPF với một hệ thống định tuyến khác (chạy BGP, RIP, hoặc Static).
**Công thức tính OSPF Cost chuẩn:** $\text{Cost} = \frac{\text{Reference Bandwidth}}{\text{Interface Bandwidth}} = \frac{10^8 \text{ bps}}{\text{Interface Bandwidth (bps)}} = \frac{100 \text{ Mbps}}{\text{Interface Bandwidth (Mbps)}}$

  *(Lưu ý: Mặc định cổng 100 Mbps có Cost = 1, cổng 1 Gbps cũng có Cost = 1. Để phân biệt tốc độ cao, cần cấu hình lệnh: `auto-cost reference-bandwidth 1000` hoặc cao hơn).*

---

### 5.10. Giao thức BGP (Border Gateway Protocol - BGPv4)

#### Bản chất và Đặc điểm cốt lõi của BGP
- BGP là giao thức định tuyến **Path Vector** liên miền (Inter-domain) duy nhất vận hành toàn bộ mạng Internet toàn cầu (RFC 4271).
- Chạy trên nền tảng kết nối tin cậy **TCP cổng 179**.
- Trao đổi thông tin giữa các **Hệ thống tự trị (Autonomous System - AS)**. Mỗi AS được định danh bởi một số hiệu ASN (Autonomous System Number: 16-bit cũ từ 1 - 65535, dải private: 64512 - 65535; hoặc 32-bit mới).

#### Phân biệt eBGP vs. iBGP

| Tiêu chí | eBGP (External BGP) | iBGP (Internal BGP) |
| :--- | :--- | :--- |
| **Phạm vi kết nối** | Giữa hai router thuộc **hai AS khác nhau** | Giữa các router thuộc **cùng một AS** |
| **Administrative Distance**| **20** (Cực kỳ tin cậy) | **200** |
| **Thuộc tính AS_PATH** | Tự động chèn thêm ASN của mình vào đầu chuỗi | **KHÔNG** được sửa đổi AS_PATH |
| **Quy tắc lặp (Loop Prevention)**| Bỏ qua route nếu thấy ASN của chính mình trong AS_PATH | **Quy tắc iBGP Split Horizon:** Không quảng bá route học từ một iBGP peer cho một iBGP peer khác |
| **Yêu cầu Topology** | Thường nối trực tiếp (TTL = 1 mặc định) | Bắt buộc kết nối **Full-Mesh logic** giữa các iBGP router (hoặc dùng Route Reflector / Confederation) |

#### Quan hệ kinh tế giữa các AS & Quy tắc định tuyến Valley-Free (Gao-Rexford)
1. **Customer-Provider (Transit):** Khách hàng trả tiền cho nhà cung cấp để mua quyền truy cập toàn bộ Internet.
2. **Peer-to-Peer (Peering):** Hai AS thỏa thuận kết nối ngang hàng để trao đổi lưu lượng miễn phí (settlement-free) cho các khách hàng của nhau.
3. **Quy tắc Valley-Free:**
   - Tuyến đường học được từ **Customer** $\to$ Được phép quảng bá cho tất cả mọi người (Provider, Peer, Customer khác).
   - Tuyến đường học được từ **Provider** hoặc **Peer** $\to$ **CHỈ ĐƯỢC PHÉP quảng bá cho Customer của mình**, TUYỆT ĐỐI KHÔNG quảng bá cho Provider hoặc Peer khác (để tránh việc trở thành đường trung chuyển không công cho thiên hạ).

---

### 5.11. Bốn nhóm thuộc tính BGP (BGP Path Attributes)

1. **Well-known Mandatory (Bắt buộc phải nhận biết & bắt buộc có trong mọi update):**
   - **ORIGIN:** Nguồn gốc của route ($IGP = 0$, $EGP = 1$, $INCOMPLETE = 2$).
   - **AS_PATH:** Danh sách chuỗi các số hiệu AS mà gói tin đã đi qua (dùng để chống loop và đo khoảng cách liên miền).
   - **NEXT_HOP:** Địa chỉ IP của router bước kế tiếp để đi tới mạng đích.
2. **Well-known Discretionary (Bắt buộc phải nhận biết nhưng tùy chọn có trong update):**
   - **LOCAL_PREF:** Mức độ ưu tiên cục bộ để chọn cổng ra khỏi AS.
   - **ATOMIC_AGGREGATE:** Đánh dấu tuyến đường đã bị gom cụm làm mất thông tin chi tiết.
3. **Optional Transitive (Tùy chọn, router không hiểu vẫn phải giữ lại và chuyển tiếp):**
   - **COMMUNITY:** Thẻ gắn nhãn nhóm các route để áp dụng chính sách.
   - **AGGREGATOR:** Thông tin về router và AS đã thực hiện gom cụm route.
4. **Optional Non-transitive (Tùy chọn, router không hiểu thì vứt bỏ, không chuyển tiếp sang AS khác):**
   - **MED (Multi-Exit Discriminator):** Thuộc tính dùng để gợi ý cho AS lân cận chọn lối vào nào khi có nhiều đường nối.

---

### 5.12. Thuật toán lựa chọn đường đi tối ưu BGP (12 Bước Bất Biến)
Khi một router BGP nhận được nhiều đường đi khác nhau tới cùng một mạng đích, router sẽ thực hiện so sánh tuần tự theo đúng 12 bước sau đây cho đến khi tìm được một đường đi duy nhất chiến thắng:

```
[1. WEIGHT cao nhất] (Cisco proprietary)
       |
[2. LOCAL_PREF cao nhất] (Toàn bộ AS)
       |
[3. Tuyến do chính router Originate] (network/redistribute > aggregate)
       |
[4. Chiều dài AS_PATH ngắn nhất]
       |
[5. Mã ORIGIN thấp nhất] (IGP < EGP < Incomplete)
       |
[6. Giá trị MED thấp nhất] (Giữa các route cùng AS láng giềng)
       |
[7. Ưu tiên eBGP hơn iBGP]
       |
[8. Metric IGP tới NEXT_HOP thấp nhất]
       |
[9. Cân bằng tải Multipath (nếu bật)]
       |
[10. Tuyến eBGP học lâu nhất / ổn định nhất]
       |
[11. BGP Router ID (RID) thấp nhất]
       |
[12. Địa chỉ IP của Neighbor thấp nhất]
```

> **Ghi nhớ sâu sắc để làm bài trắc nghiệm:**
> - Hai thuộc tính đầu tiên: **WEIGHT** (Bước 1) và **LOCAL_PREF** (Bước 2) $\to$ **CÀNG CAO CÀNG TỐT (Highest wins)**.
> - Các thuộc tính kỹ thuật sau: **AS_PATH length** (Bước 4), **ORIGIN** (Bước 5), **MED** (Bước 6), **IGP Metric** (Bước 8), **Router ID** (Bước 11), **Neighbor IP** (Bước 12) $\to$ **CÀNG NHỎ CÀNG TỐT (Lowest wins)**.

---

### 5.13. An ninh định tuyến Internet & BGP Hijacking
- **Bản chất lỗ hổng:** BGP nguyên thủy được thiết kế trên mô hình tin tưởng lẫn nhau (implicit trust). Bất kỳ router nào cũng có thể gửi bản tin BGP quảng bá quyền sở hữu một dải IP prefix bất kỳ mà không có cơ chế mật mã nào kiểm tra tính xác thực.
- **Kịch bản BGP Route Hijacking (Cướp quyền định tuyến):**
  - Kẻ tấn công cấu hình router BGP của mình phát quảng bá một dải IP thuộc về nạn nhân (Ví dụ dải DNS `8.8.8.0/24` của Google).
  - Tinh vi hơn: Kẻ tấn công quảng bá một dải IP cụ thể hơn (**More Specific Prefix**, ví dụ `8.8.8.0/25`). Do nguyên tắc Longest Prefix Match (LPM) luôn ưu tiên tiền tố dài hơn, toàn bộ lưu lượng của người dùng trên toàn thế giới sẽ bị hút sạch về máy chủ của kẻ tấn công (Blackhole hoặc Man-in-the-Middle).
- **Giải pháp phòng thủ hiện đại:**
  - **RPKI (Resource Public Key Infrastructure):** Hệ thống chứng chỉ khóa công khai phân cấp gán liền quyền sở hữu dải IP với số hiệu ASN thông qua đối tượng **ROA (Route Origin Authorization)**.
  - **BGP Origin Validation:** Router BGP kiểm tra chữ ký số mật mã của bản tin BGP nhận được; nếu trạng thái là `Invalid` (AS quảng bá không trùng khớp với ASN ghi trong ROA) $\to$ router lập tức drop tuyến đường đó, ngăn chặn triệt để BGP Hijacking.

---

## PHẦN 6: CHUYÊN ĐỀ 5 - GIAO THỨC IPV6 (INTERNET PROTOCOL VERSION 6)

### 6.1. Động lực chuyển dịch & Khuyết điểm của giải pháp NAT kéo dài
- **Khủng hoảng cạn kiệt địa chỉ IPv4:** Không gian 32-bit của IPv4 chỉ cung cấp tối đa $2^{32} \approx 4.29$ tỷ địa chỉ. IANA đã chính thức cạn kiệt kho địa chỉ IPv4 tự do từ năm 2011.
- **Tại sao NAT (Network Address Translation) không thể là giải pháp lâu dài?**
  - **Phá vỡ tính toàn vẹn đầu-cuối (End-to-End Principle):** Các máy trong mạng nội bộ không thể trực tiếp nhận kết nối từ bên ngoài nếu không cấu hình Port Forwarding hoặc STUN/TURN phức tạp.
  - **Gây trở ngại lớn cho các ứng dụng P2P:** Cuộc gọi thoại VoIP (SIP/RTP), hội nghị truyền hình, game online nhiều người chơi liên tục gặp lỗi thiết lập phiên.
  - **Tốn kém tài nguyên và dễ nghẽn cổ chai:** Router NAT phải duy trì bảng trạng thái phiên (State Table) khổng lồ, ngốn CPU và RAM.
  - **Bất lực trước làn sóng IoT (Internet of Things):** Hàng chục tỷ thiết bị thông minh, cảm biến và xe tự hành đòi hỏi kết nối mạng độc lập và địa chỉ IP công cộng thực sự.

---

### 6.2. Cấu trúc Header IPv6 cố định (40 bytes) và phân tích từng trường
Tiêu đề cơ sở của IPv6 được thiết kế tinh giản tối đa với **kích thước cố định đúng 40 bytes** (so với tiêu đề IPv4 có độ dài biến thiên từ 20 đến 60 bytes).

```
 0                   1                   2                   3
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|Version| Traffic Class |           Flow Label                  |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|         Payload Length        |  Next Header  |   Hop Limit   |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                                                               |
+                                                               +
|                                                               |
+                         Source Address                        +
|                           (128 bits)                          |
+                                                               +
|                                                               |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                                                               |
+                                                               +
|                                                               |
+                      Destination Address                      +
|                           (128 bits)                          |
+                                                               +
|                                                               |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```

#### Phân tích chi tiết 8 trường trong IPv6 Header
1. **Version (4 bits):** Luôn mang giá trị nhị phân `0110` (số 6 thập phân).
2. **Traffic Class (8 bits):** Tương đương trường ToS (Type of Service) trong IPv4. Gồm 6 bits DSCP (phân lớp QoS DiffServ) và 2 bits ECN (báo hiệu nghẽn chủ động).
3. **Flow Label (20 bits):** Trường hoàn toàn mới trong IPv6. Dùng để dán nhãn nhận diện các gói tin thuộc về cùng một luồng dữ liệu thời gian thực (như video streaming). Router có thể chuyển tiếp gói tin theo đường đi nhanh (Fast Path) mà không cần bóc tách kiểm tra các tiêu đề tầng giao vận (TCP/UDP) bên trong.
4. **Payload Length (16 bits):** Độ dài của toàn bộ dữ liệu đi sau tiêu đề cơ sở 40 bytes (tính bằng bytes), **bao gồm cả các tiêu đề mở rộng (Extension Headers)**. Giá trị tối đa $65,535\text{ bytes}$ (nếu lớn hơn cần dùng tùy chọn Jumbo Payload).
5. **Next Header (8 bits):** Thay thế trường Protocol của IPv4. Xác định loại tiêu đề mở rộng kế tiếp hoặc giao thức tầng giao vận (TCP = 6, UDP = 17, ICMPv6 = 58).
6. **Hop Limit (8 bits):** Thay thế trường TTL (Time to Live) của IPv4. Giảm đi 1 qua mỗi chặng router. Khi giảm về 0, gói tin bị loại bỏ và router gửi bản tin ICMPv6 Type 3 "Time Exceeded" về nguồn.
7. **Source Address (128 bits = 16 bytes):** Địa chỉ IPv6 của máy gửi.
8. **Destination Address (128 bits = 16 bytes):** Địa chỉ IPv6 của máy nhận.

#### Các trường bị loại bỏ so với IPv4 và lý do cải tiến
- **Bỏ trường `IHL (Header Length)`:** Vì tiêu đề cơ sở của IPv6 luôn cố định 40 bytes.
- **Bỏ trường `Header Checksum`:** Tăng tốc độ chuyển tiếp gói tin của router lên gấp nhiều lần. Việc kiểm tra lỗi đã được tầng 2 (Ethernet CRC) và tầng 4 (TCP/UDP Checksum) đảm nhận.
- **Bỏ các trường `Identification`, `Flags`, `Fragment Offset` khỏi header cơ sở:**
  > **NGUYÊN TẮC VÀNG THI TRẮC NGHIỆM:** **Router trung gian trên đường truyền KHÔNG BAO GIỜ phân mảnh gói tin IPv6!** Nếu gói tin vượt quá MTU của cổng ra, router lập tức hủy gói và gửi bản tin ICMPv6 Type 2 "Packet Too Big" về cho máy nguồn. Việc phân mảnh chỉ do chính máy nguồn thực hiện thông qua tiêu đề mở rộng Fragment Extension Header.

---

### 6.3. Chuỗi tiêu đề mở rộng (Extension Headers Chain) & Path MTU Discovery
IPv6 xử lý các tùy chọn bổ sung thông qua kiến trúc **Chuỗi tiêu đề mở rộng (Daisy Chain of Next Headers)**:

```
[IPv6 Header] Next Header = Hop-by-Hop (0)
     |
     v
[Hop-by-Hop Header] Next Header = Routing (43)
     |
     v
[Routing Header] Next Header = TCP (6)
     |
     v
[TCP Header + Payload]
```

#### Thứ tự khuyến nghị chuẩn IETF của các Extension Headers
1. **Hop-by-Hop Options:** Phải được xử lý bởi mọi router trên đường đi (thường dùng cho Router Alert hoặc Jumbo Payload).
2. **Destination Options:** Xử lý bởi các router trung gian được chỉ định trong Routing header.
3. **Routing Header:** Định tuyến nguồn (Source Routing).
4. **Fragment Header:** Chứa thông tin phân mảnh gói tin (chỉ do nguồn tạo ra).
5. **Authentication Header (AH):** Xác thực nguồn gốc và toàn vẹn gói tin (IPsec).
6. **Encapsulating Security Payload (ESP):** Mã hóa bảo mật dữ liệu (IPsec).
7. **Destination Options:** Xử lý bởi thiết bị đích cuối cùng.
8. **Upper-Layer Header:** TCP, UDP, hoặc ICMPv6.

#### Quy trình Path MTU Discovery (PMTUD - RFC 8201)
- IPv6 quy định kích thước MTU liên kết tối thiểu bắt buộc là **1280 bytes**.
- Máy nguồn ban đầu giả định MTU của toàn tuyến đường bằng MTU của cổng mạng cục bộ (ví dụ 1500 bytes với Ethernet).
- Khi gói tin đi qua một liên kết có MTU nhỏ hơn (ví dụ đường hầm tunnel có MTU = 1400 bytes), router tại đó sẽ hủy gói và gửi bản tin ICMPv6 Type 2 "Packet Too Big" kèm theo giá trị MTU của liên kết nghẽn (1400 bytes).
- Máy nguồn nhận được bản tin ICMPv6 này sẽ giảm kích thước gói tin gửi đi xuống 1400 bytes và lưu vào bộ nhớ cache PMTU.

---

### 6.4. Định dạng và Không gian địa chỉ IPv6
- **Quy mô không gian:** Chiều dài 128 bits, cung cấp $2^{128} \approx 3.4 \times 10^{38}$ địa chỉ.

  (Đủ để cấp hàng nghìn tỷ địa chỉ cho mỗi milimet vuông bề mặt Trái Đất).
- **Quy cách biểu diễn:** 128 bits được chia thành **8 nhóm (hextets)**, mỗi nhóm gồm 16 bits biểu diễn bằng 4 chữ số thập lục phân (hex), phân cách nhau bằng dấu hai chấm `:`.  
  *Ví dụ:* `2001:0db8:0000:0000:0000:ff00:0042:8329`

---

### 6.5. Quy tắc rút gọn địa chỉ IPv6 chuẩn RFC 5952
Để biểu diễn địa chỉ IPv6 đồng nhất và chuẩn hóa, RFC 5952 quy định 4 bước bắt buộc:

1. **Bỏ các số 0 ở đầu (Omit Leading Zeros):** Trong mỗi nhóm 16-bit, lược bỏ các chữ số `0` đứng đầu:
   - `:0db8:` $\to$ `:db8:`
   - `:0042:` $\to$ `:42:`
   - `:0000:` $\to$ `:0:` (Phải giữ lại ít nhất một chữ số 0 nếu nhóm toàn số 0).
2. **Dùng dấu hai chấm kép `::` nén dãy số 0 liên tiếp dài nhất:**
   - Thay thế một chuỗi gồm hai hoặc nhiều nhóm `:0:0:...:` liên tiếp bằng một dấu hai chấm kép `::`.
3. **Quy tắc giải quyết hòa (Tie-breaking):**
   - Nếu có hai hoặc nhiều dãy số 0 liên tiếp có độ dài bằng nhau, **bắt buộc phải rút gọn dãy đầu tiên xuất hiện bên trái!**
4. **Quy tắc bất biến duy nhất:**
   > **LƯU Ý CỐT TỬ:** Dấu `::` **CHỈ ĐƯỢC PHÉP XUẤT HIỆN DUY NHẤT 1 LẦN** trong toàn bộ địa chỉ IPv6! Nếu xuất hiện 2 lần, việc giải nén sẽ bị mơ hồ (ambiguous) và không xác định được số lượng bit 0 ở mỗi vị trí.

*Ví dụ minh họa rút gọn:*
- Địa chỉ gốc: `2001:0db8:0000:0000:0000:0000:1428:57ab`
  - Bước 1 (bỏ số 0 đầu): `2001:db8:0:0:0:0:1428:57ab`
  - Bước 2 (dùng `::`): `2001:db8::1428:57ab`
- Địa chỉ gốc: `fe80:0000:0000:0000:0202:b3ff:fe1e:8329`
  - Rút gọn chuẩn: `fe80::202:b3ff:fe1e:8329`
- Địa chỉ Loopback: `0000:0000:0000:0000:0000:0000:0000:0001` $\to$ `::1`
- Địa chỉ Unspecified: `0000:0000:0000:0000:0000:0000:0000:0000` $\to$ `::`

---

### 6.6. Phân loại địa chỉ IPv6 (KHÔNG CÒN BROADCAST!)
IPv6 chính thức **xóa sổ hoàn toàn địa chỉ Broadcast** để loại bỏ hiện tượng bão broadcast (Broadcast Storm) gây quá tải CPU của các máy trong cùng mạng LAN. Thay vào đó, IPv6 chia thành 3 loại:

```
                          [ Các loại Địa chỉ IPv6 ]
                                      |
         +----------------------------+----------------------------+
         |                                                         |
    [ Unicast ]                                              [ Multicast ]
(1 giao diện duy nhất)                                  (ff00::/8 - Nhóm giao diện)
         |
   +-----+-------------------------+
   |                               |
[ GUA: 2000::/3 ]          [ LLA: fe80::/10 ]              [ Anycast ]
(Công cộng toàn cầu)       (Cục bộ trên link)          (1 địa chỉ - Giao diện gần nhất)
         |
   [ ULA: fc00::/7 ]
   (Nội bộ riêng tư)
```

#### 1. Global Unicast Address (GUA - Địa chỉ toàn cầu)
- **Dải tiền tố:** `2000::/3` (Bắt đầu bằng 3 bit nhị phân `001...`, tương đương dải từ `2000::` đến `3fff::`).
- Tương đương địa chỉ Public IP của IPv4, có thể định tuyến tự do trên toàn bộ Internet.
- **Cấu trúc phân cấp 3 phần:**
  - **Global Routing Prefix (48 bits):** Do cơ quan quản lý (RIR) và nhà cung cấp dịch vụ ISP cấp cho tổ chức.
  - **Subnet ID (16 bits):** Do người quản trị mạng tổ chức tự chia mạng con (cung cấp $2^{16} = 65,536$ mạng con khác nhau!).
  - **Interface ID (64 bits):** Định danh duy nhất của giao diện mạng của máy trạm.

#### 2. Link-Local Address (LLA - Địa chỉ cục bộ liên kết)
- **Dải tiền tố:** `fe80::/10` (Trong thực tế luôn đi kèm prefix 64-bit là `fe80::/64`).
- **Bắt buộc phải có:** Mọi giao diện mạng bật IPv6 đều tự động sinh ra một địa chỉ Link-Local.
- **Phạm vi hiệu lực:** **CHỈ CÓ GIÁ TRỊ TRONG NỘI BỘ MỘT LIÊN KẾT VẬT LÝ (Local Link)**. Router tuyệt đối **KHÔNG BAO GIỜ** định tuyến gói tin có địa chỉ nguồn hoặc đích Link-Local ra khỏi liên kết đó!
- **Ứng dụng thực tế:** Dùng làm địa chỉ Default Gateway cho các máy trạm, dùng làm địa chỉ láng giềng Next-Hop cho các giao thức định tuyến động nội miền (OSPFv3, RIPng).

#### 3. Unique Local Address (ULA - Địa chỉ cục bộ duy nhất)
- **Dải tiền tố:** `fc00::/7` (Trong thực tế hầu như luôn sử dụng `fd00::/8` với bit L=1).
- Tương đương dải địa chỉ Private IP của IPv4 (RFC 1918 như `10.0.0.0/8`, `192.168.0.0/16`). Chỉ dùng trong mạng nội bộ công ty/tòa nhà, không định tuyến trên Internet công cộng.

#### 4. Multicast Address (Địa chỉ đa hướng)
- **Dải tiền tố:** `ff00::/8` (Bắt đầu bằng `1111 1111_2`).
- Gói tin gửi tới địa chỉ Multicast sẽ được chuyển tới tất cả các thiết bị đăng ký lắng nghe nhóm đó.
- **Các địa chỉ Multicast quen thuộc bắt buộc ghi nhớ:**
  - `ff02::1`: **All-Nodes Multicast** (Mọi thiết bị IPv6 trên liên kết - thay thế Broadcast).
  - `ff02::2`: **All-Routers Multicast** (Tất cả các router IPv6 trên liên kết).
  - `ff02::5`: All OSPFv3 Routers.
  - `ff02::6`: All OSPFv3 DR/BDR Routers.

#### 5. Anycast Address (Địa chỉ bất kỳ hướng)
- Không có dải tiền tố riêng; có cấu trúc hoàn toàn giống địa chỉ Unicast.
- Được gán đồng thời cho **nhiều giao diện mạng thuộc nhiều máy chủ khác nhau** (thường đặt ở nhiều châu lục). Gói tin gửi tới địa chỉ Anycast sẽ được hạ tầng định tuyến Internet tự động chuyển tiếp tới **giao diện máy chủ "gần nhất"** theo chi phí metric của bảng định tuyến (thường ứng dụng cho DNS Root Servers và CDN).

---

### 6.7. Quy tắc chuyển đổi MAC 48-bit sang Interface ID theo Modified EUI-64
Khi sử dụng cơ chế cấu hình tự động, thiết bị có thể tự tạo phần Interface ID 64-bit từ địa chỉ MAC vật lý 48-bit của card mạng theo chuẩn **Modified EUI-64**.

#### Quy trình 3 bước chuyển đổi chuẩn xác
- **Bước 1:** Chia đôi địa chỉ MAC 48-bit (6 bytes) thành hai nửa bằng nhau (mỗi nửa 3 bytes): Nửa đầu đại diện cho nhà sản xuất (OUI), nửa sau là số hiệu thiết bị (NIC).
- **Bước 2:** Chèn chuỗi 16-bit cố định có giá trị `ff:fe` (hoặc `FF-FE`) vào chính giữa hai nửa.
- **Bước 3 (BƯỚC QUAN TRỌNG NHẤT):** Đảo ngược giá trị của **bit thứ 7** (bit Universal/Local - tính từ trái sang phải, với bit cực trái là bit 0) của byte đầu tiên:
  - Nếu bit thứ 7 đang là `0` $\to$ Đổi thành `1`.
  - Nếu bit thứ 7 đang là `1` $\to$ Đổi thành `0`.
  *(Trong thực tế, do địa chỉ MAC card mạng thương mại có bit thứ 7 mặc định là 0, sau khi đảo nó sẽ thành 1, tương đương với việc **cộng thêm 2 vào chữ số Hex thứ hai** của byte đầu tiên!).*

#### Bài tập mẫu thực chiến EUI-64
- **Đề bài:** Cho địa chỉ MAC của card mạng là `00:1A:2B:3C:4D:5E`. Hãy tạo Interface ID 64-bit theo chuẩn Modified EUI-64.
- **Lời giải từng bước:**
  - *Bước 1:* Chia đôi thành `00:1A:2B` và `3C:4D:5E`.
  - *Bước 2:* Chèn `FF:FE` vào giữa $\to$ `00:1A:2B:FF:FE:3C:4D:5E`.
  - *Bước 3:* Xét byte đầu tiên là `00` (Hex):
    - Đổi sang nhị phân: `0000 0000_2`
    - Bit thứ 7 (bit gạch chân): `0000 00[0]0_2`
    - Đảo bit thành: `0000 00[1]0_2` $\to$ Đổi ngược lại Hex thành `02`.
  - *Kết quả cuối cùng:* Interface ID là `021a:2bff:fe3c:4d5e`.

---

### 6.8. Giao thức ICMPv6 & Neighbor Discovery Protocol (NDP)
Trong IPv6, giao thức **ICMPv6 (Next Header = 58)** đóng vai trò trung tâm sống còn, tích hợp toàn bộ chức năng của ICMPv4, giao thức phân giải địa chỉ ARP, và giao thức quản lý nhóm IGMP.

#### Giao thức khám phá láng giềng NDP (RFC 4861) với 5 bản tin cốt lõi
1. **Router Solicitation (RS - ICMPv6 Type 133):** Do host phát ra khi vừa cắm mạng để truy tìm router trên link (Gửi tới địa chỉ Multicast `ff02::2` - All Routers).
2. **Router Advertisement (RA - ICMPv6 Type 134):** Do router định kỳ phát ra (hoặc trả lời RS) để thông báo cho host biết: Prefix mạng, MTU, Default Gateway và các cờ cấu hình địa chỉ IP (Gửi tới `ff02::1` - All Nodes).
3. **Neighbor Solicitation (NS - ICMPv6 Type 135):** **Thay thế hoàn toàn bản tin ARP Request** của IPv4 để hỏi địa chỉ MAC của một IP láng giềng; đồng thời dùng để kiểm tra trùng lặp địa chỉ (DAD).
4. **Neighbor Advertisement (NA - ICMPv6 Type 136):** **Thay thế bản tin ARP Reply** của IPv4 để phản hồi địa chỉ MAC của mình.
5. **Redirect (ICMPv6 Type 137):** Do router phát ra để hướng dẫn máy trạm gửi gói tin trực tiếp sang một router khác trên cùng liên kết có đường đi tối ưu hơn.

---

### 6.9. Phân giải địa chỉ qua Solicited-Node Multicast & DAD

#### Địa chỉ Solicited-Node Multicast (Cơ chế chống bão Broadcast)
- Trong IPv4, khi muốn tìm MAC của IP đích, máy gửi phải phát bản tin ARP Request dạng Broadcast `FF:FF:FF:FF:FF:FF` $\to$ Mọi máy tính trong mạng LAN đều bị ngắt phần cứng để kiểm tra gói tin.
- Trong IPv6, bản tin NS được gửi tới **Địa chỉ Solicited-Node Multicast** đặc biệt:  
  **Định dạng:** `ff02::1:ffxx:xxxx`  
  Được tạo bằng cách ghép tiền tố cố định `ff02::1:ff00:0/104` với **24 bits cuối cùng** của địa chỉ IPv6 cần tìm kiếm.
- *Lợi ích:* Ở tầng liên kết dữ liệu Layer 2, card mạng Ethernet sẽ chuyển địa chỉ này thành địa chỉ MAC Multicast tương ứng dạng `33-33-FF-xx-xx-xx`. Chỉ có đúng thiết bị nào sở hữu 24 bits cuối trùng khớp mới tiếp nhận và xử lý bản tin NS, các máy khác hoàn toàn bỏ qua ở cấp chip mạng, triệt tiêu 100% lãng phí CPU.

#### Quy trình Kiểm tra trùng lặp địa chỉ (DAD - Duplicate Address Detection)
Trước khi bất kỳ một địa chỉ IPv6 nào (kể cả Link-Local hay GUA) được phép hoạt động chính thức trên giao diện mạng:
1. Địa chỉ đó được đặt ở trạng thái tạm thời (**Tentative Address**).
2. Host gửi một bản tin **Neighbor Solicitation (NS)** với:
   - Địa chỉ IP nguồn: `::` (Unspecified Address - vì địa chỉ của host chưa được xác thực).
   - Địa chỉ IP đích: Địa chỉ **Solicited-Node Multicast** của chính địa chỉ đang thăm dò.
3. Host lắng nghe trên mạng:
   - Nếu trong một khoảng thời gian chờ mà nhận được bản tin **Neighbor Advertisement (NA)** trả lời $\to$ Chứng tỏ địa chỉ đã bị máy khác chiếm dụng $\to$ Quá trình DAD thất bại, giao diện báo lỗi trùng IP và bị vô hiệu hóa.
   - Nếu hết thời gian mà không có ai trả lời $\to$ Địa chỉ được xác nhận là duy nhất trên liên kết và chuyển sang trạng thái hợp lệ để sử dụng.

---

### 6.10. Ba phương thức cấu hình địa chỉ động (SLAAC & DHCPv6)
Khi nhận được bản tin Router Advertisement (RA) từ router, máy trạm sẽ đọc giá trị của **3 cờ điều khiển (Flags)** nằm trong tiêu đề RA để quyết định phương thức lấy địa chỉ IP:
- **Cờ A (Autonomous Address Configuration):** Nếu bật (=1), cho phép host tự tạo GUA bằng tiền tố trong RA.
- **Cờ M (Managed Address Configuration):** Nếu bật (=1), bắt buộc host phải xin địa chỉ IP từ máy chủ **Stateful DHCPv6**.
- **Cờ O (Other Configuration):** Nếu bật (=1), cho phép host xin các thông số phụ khác (như DNS Server IP, Domain name) từ máy chủ **Stateless DHCPv6**.

#### Bảng ma trận 3 phương thức cấu hình địa chỉ IPv6 chuẩn

| Phương thức cấu hình | Trạng thái cờ (Flags) | Nguồn cấp địa chỉ IPv6 GUA | Nguồn cấp DNS / Domain | Server lưu State? |
| :--- | :--- | :--- | :--- | :--- |
| **1. SLAAC thuần túy (Stateless Only)** | `A = 1, M = 0, O = 0` | Host tự ghép Prefix từ RA với Interface ID (EUI-64/Random)| Lấy qua tùy chọn RDNSS trong RA (RFC 8106) | **KHÔNG** (Hoàn toàn Stateless) |
| **2. SLAAC + Stateless DHCPv6** | `A = 1, M = 0, O = 1` | Host tự tạo bằng SLAAC qua Prefix của RA | **Stateless DHCPv6 Server** cấp phát | **KHÔNG** (DHCPv6 không lưu IP lease) |
| **3. Stateful DHCPv6** | `M = 1` *(A=0, O=0 hoặc 1)* | **Stateful DHCPv6 Server** cấp phát toàn bộ | **Stateful DHCPv6 Server** cấp phát | **CÓ** (DHCPv6 server quản lý bảng IP lease hệt như IPv4) |

---

### 6.11. Chiến lược chuyển đổi công nghệ: Dual-Stack, Tunneling, Translation

```
                   [ Các giải pháp chuyển dịch sang IPv6 ]
                                     |
         +---------------------------+---------------------------+
         |                                                       |
   [ Dual-Stack ]                                          [ Translation ]
(Chạy song song 2 giao thức)                            (NAT64 + DNS64 biên dịch)
         |
   [ Tunneling ]
(Đóng gói IPv6 trong IPv4)
- 6in4, GRE, 6to4, Teredo
```

1. **Dual-Stack (Ngăn xếp kép):**
   - Giải pháp tự nhiên và tối ưu nhất: Mọi router, switch, máy chủ và máy trạm đều được cài đặt và cấu hình đồng thời cả hai ngăn xếp giao thức IPv4 và IPv6 trên cùng giao diện vật lý.
   - **Cơ chế Happy Eyeballs (RFC 8305):** Khi người dùng truy cập một website, ứng dụng gửi đồng thời cả hai truy vấn DNS `A` (IPv4) và `AAAA` (IPv6). Sau đó tiến hành bắt tay TCP song song với cả hai địa chỉ. Kết nối nào phản hồi trước sẽ được ưu tiên sử dụng, mang lại trải nghiệm duyệt web mượt mà tuyệt đối không bị gián đoạn.
2. **Tunneling (Kỹ thuật đường hầm):**
   - Áp dụng khi hai ốc đảo mạng IPv6 cần liên lạc với nhau nhưng hạ tầng kết nối trung gian chỉ hỗ trợ IPv4.
   - Router biên đóng gói toàn bộ gói tin IPv6 vào bên trong phần tải dữ liệu của một gói tin IPv4 (với trường `IPv4 Protocol = 41` cho kết nối 6in4) để chuyển tải an toàn qua đám mây IPv4.
3. **Translation (Biên dịch giao thức - NAT64 + DNS64):**
   - Cho phép các máy trạm chỉ chạy thuần IPv6 (IPv6-only clients) có thể kết nối và truy cập các máy chủ đời cũ chỉ có IPv4 (IPv4-only servers) trên Internet.
   - **DNS64:** Khi client IPv6 hỏi bản ghi `AAAA` của một server chỉ có bản ghi `A` (ví dụ `192.0.2.1`), máy chủ DNS64 tự động tổng hợp một địa chỉ IPv6 ảo bằng cách ghép tiền tố Well-Known Prefix **`64:ff9b::/96`** với địa chỉ IPv4 32-bit của server $\to$ trả về địa chỉ ảo `64:ff9b::192.0.2.1`.
   - **NAT64:** Router NAT64 nằm giữa nhận gói tin từ client gửi tới địa chỉ `64:ff9b::...`, tiến hành bóc bỏ tiêu đề IPv6, chuyển đổi thành tiêu đề IPv4 tương ứng và chuyển tiếp tới server IPv4.

---

## PHẦN 7: CHUYÊN ĐỀ 6 - MẠNG ĐIỀU KHIỂN BẰNG PHẦN MỀM (SDN)

### 7.1. Bối cảnh ra đời & Hạn chế của Mạng truyền thống

#### Kiến trúc "Hộp đóng" tích hợp dọc của Mạng truyền thống
Trong suốt hơn 40 năm phát triển của Internet, các thiết bị chuyển mạch (Switches) và bộ định tuyến (Routers) được thiết kế theo mô hình **tích hợp dọc nguyên khối (Vertically Integrated Monolith)**:
- Mỗi thiết bị là một chiếc "Hộp đen (Black Box)" độc quyền của nhà sản xuất phần cứng (Cisco, Juniper, Huawei...).
- Cả hai mặt phẳng: **Mặt phẳng điều khiển (Control Plane)** và **Mặt phẳng dữ liệu (Data Plane)** đều bị đóng chặt bên trong cùng một khung máy vật lý.
- Các giao thức định tuyến (OSPF, BGP, RIP) chạy theo mô hình **Điều khiển phân tán (Distributed Control)**: Mỗi router tự chạy thuật toán, tự tính toán bảng định tuyến và tự cấu hình cho chính mình dựa trên các thông điệp trao đổi cục bộ.

#### Các hạn chế chí mạng của mạng truyền thống
1. **Quản trị thủ công phân tán (Per-box Configuration):** Người quản trị phải đăng nhập qua giao diện dòng lệnh (CLI) độc quyền vào từng router riêng lẻ để cấu hình. Dễ xảy ra lỗi do con người (Human Error), cấu hình sai chính sách bảo mật hoặc tạo ra các liên kết tắt (short-cut links) vi phạm quy tắc phân vùng mạng.
2. **Thiếu cái nhìn toàn cục (Lack of Global View):** Các thuật toán định tuyến phân tán mất nhiều thời gian để hội tụ khi có sự cố mạng. Khó tối ưu hóa lưu lượng toàn cục (Traffic Engineering) vì mỗi router chỉ có cái nhìn cục bộ.
3. **Chu kỳ đổi mới công nghệ cực kỳ chậm chạp:** Muốn bổ sung một tính năng hoặc giao thức định tuyến mới, người ta phải mất từ 5 đến 10 năm để chuẩn hóa tại IETF, chờ các hãng thiết kế chip ASIC phần cứng mới, và thay thế toàn bộ thiết bị trên mạng.
4. **Phụ thuộc độc quyền vào nhà cung cấp (Vendor Lock-in):** Chi phí thiết bị mạng đắt đỏ, không thể tùy biến hay lập trình hóa theo nhu cầu của doanh nghiệp.

---

### 7.2. Nguyên lý kiến trúc SDN: Tách rời Control Plane & Data Plane
Software-Defined Networking (SDN) là một cuộc cách mạng thay đổi hoàn toàn tư duy thiết kế mạng:
> **ĐỊNH NGHĨA CỐT LÕI:** SDN là kiến trúc mạng trong đó **Mặt phẳng điều khiển (Control Plane) được tách rời hoàn toàn khỏi Mặt phẳng dữ liệu (Data Plane)**, và được tập trung hóa về mặt logic vào một thực thể phần mềm gọi là **Bộ điều khiển mạng (SDN Controller)**.

```
       [ Ứng dụng Mạng: Firewall, Load Balancer, Routing, QoS ]
                                  |
               ======================================= (Northbound API / RESTful)
                                  |
              [ MẶT PHẲNG ĐIỀU KHIỂN (CONTROL PLANE) ]
                     SDN Controller (Network OS)
                 (Toàn quyền quan sát toàn bộ mạng)
                                  |
               ======================================= (Southbound API / OpenFlow)
                                  |
               [ MẶT PHẲNG DỮ LIỆU (DATA PLANE) ]
          +-----------------------+-----------------------+
          |                       |                       |
    [ OpenFlow Switch 1 ]   [ OpenFlow Switch 2 ]   [ OpenFlow Switch 3 ]
    (Phần cứng đơn giản: Tra bảng Flow Table và chuyển tiếp ở tốc độ cáp)
```

#### So sánh chức năng ba Mặt phẳng (Planes) trong SDN

| Mặt phẳng | Vị trí thực thi | Chức năng nhiệm vụ cốt lõi | Thang đo thời gian (Timescale) |
| :--- | :--- | :--- | :--- |
| **Mặt phẳng Dữ liệu (Data Plane / Forwarding Plane)** | Nằm trên chip phần cứng của các Switch (White-box switches) | Tiếp nhận gói tin, so khớp với bảng luật (**Flow Table**) và chuyển tiếp ra cổng tương ứng ở tốc độ đường truyền (Wire-speed streaming) | Cực nhanh: **Nano-giây / Micro-giây** (trên từng gói tin) |
| **Mặt phẳng Điều khiển (Control Plane)** | Nằm tập trung trên phần mềm máy chủ (**SDN Controller**) | Thu thập sơ đồ topo toàn mạng, tính toán đường đi tối ưu, quyết định chính sách bảo mật, và nạp các luật chuyển tiếp xuống switch | Trung bình: **Mili-giây / Giây** (trên từng luồng gói tin) |
| **Mặt phẳng Quản trị (Management Plane)** | Hệ thống quản trị tập trung (Orchestrator, GUI, Dashboard) | Cấu hình tham số thiết bị, giám sát hiệu năng, theo dõi SLA, cấp phát tài nguyên cho người dùng | Chậm: **Phút / Giờ / Ngày** (do con người hoặc kịch bản điều khiển) |

---

### 7.3. Các giao diện lập trình trong kiến trúc SDN (APIs)

1. **Giao diện Hướng Nam (Southbound API):**
   - Nằm giữa **SDN Controller** và các **Thiết bị mạng Data Plane (Switches)**.
   - Cho phép Controller lập trình hóa phần cứng, ra lệnh nạp, sửa đổi, xóa các luật chuyển tiếp trong Flow Table của switch; đồng thời cho phép switch gửi cảnh báo hoặc gửi gói tin chưa biết lên Controller.
   - **Giao thức chuẩn phổ biến nhất:** **OpenFlow** (do Open Networking Foundation - ONF chuẩn hóa). Ngoài ra còn có: P4Runtime, NETCONF/YANG, OVSDB, BGP-LS.
2. **Giao diện Hướng Bắc (Northbound API):**
   - Nằm giữa **SDN Controller** và các **Ứng dụng mạng (Network Applications)**.
   - Cung cấp các giao diện lập trình cấp cao (thường là **RESTful APIs** với định dạng dữ liệu **JSON** hoặc Python SDK) giúp lập trình viên viết các ứng dụng điều khiển mạng (như tự động cân bằng tải, định tuyến theo chất lượng đường truyền, thiết lập tường lửa động) một cách trực quan mà không cần hiểu biết chi tiết về phần cứng bên dưới.
3. **Giao diện Đông - Tây (East-Westbound API):**
   - Dùng để trao đổi dữ liệu và đồng bộ hóa trạng thái giữa **nhiều bộ điều khiển SDN Controller khác nhau** trong một kiến trúc phân tán đa vùng, nhằm đảm bảo khả năng mở rộng (Scalability) và dự phòng chịu lỗi (Fault Tolerance).

---

### 7.4. Giao thức OpenFlow: Cấu trúc Switch & Flow Entry
OpenFlow là giao thức Southbound mở đầu tiên và chuẩn mực nhất của SDN (khởi xướng từ Đại học Stanford bởi Nick McKeown năm 2008).

#### Cấu trúc một Flow Entry trong Flow Table
Một thiết bị chuyển mạch OpenFlow duy trì một chuỗi các **Bảng luồng (Flow Tables)**. Mỗi mục luật (**Flow Entry**) trong Flow Table bao gồm 6 thành phần bắt buộc:

```
+--------------+----------+----------+-----------------------+----------+--------+
| Match Fields | Priority | Counters | Instructions / Actions| Timeouts | Cookie |
+--------------+----------+----------+-----------------------+----------+--------+
```

1. **Trường So Khớp (Match Fields):**
   Tập hợp các trường tiêu đề từ Tầng 1 đến Tầng 4 để nhận diện luồng gói tin:
   - *Tầng 1 (Physical):* Cổng mạng vào (Ingress Port).
   - *Tầng 2 (Data Link):* Địa chỉ MAC nguồn (Ethernet SA), MAC đích (Ethernet DA), Mã loại giao thức (EtherType), Nhãn mạng ảo (VLAN ID & VLAN Priority).
   - *Tầng 3 (Network):* Địa chỉ IPv4/IPv6 nguồn, IPv4/IPv6 đích, Giao thức IP (IP Protocol), Trường ToS / Traffic Class (DSCP/ECN).
   - *Tầng 4 (Transport):* Cổng dịch vụ nguồn (TCP/UDP Source Port), Cổng dịch vụ đích (TCP/UDP Destination Port), Loại bản tin ICMP.
   *(Cho phép sử dụng ký tự đại diện `*` (Wildcard) để so khớp một dải luồng).*
2. **Độ ưu tiên (Priority):**
   Số nguyên biểu thị mức độ ưu tiên của luật. Khi một gói tin khớp với nhiều Flow Entry khác nhau, **luật có giá trị Priority LỚN HƠN sẽ được áp dụng!**
3. **Bộ đếm thống kê (Counters):**
   Tự động ghi nhận số lượng gói tin (Packet Counter) và số lượng bytes (Byte Counter) đã khớp với luật này, dùng cho mục đích giám sát lưu lượng và thanh toán cước viễn thông.
4. **Tập hành động / Chỉ thị (Instructions / Actions):**
   Hành động switch phải thực thi ngay khi gói tin khớp luật:
   - **Forward:** Chuyển tiếp gói tin ra một cổng vật lý cụ thể, hoặc gửi tới các cổng ảo đặc biệt:
     - `CONTROLLER`: Đóng gói và gửi gói tin lên Controller qua bản tin `Packet-In`.
     - `ALL`: Gửi gói tin ra tất cả các cổng (trừ cổng đã nhận gói).
     - `IN_PORT`: Gửi ngược lại ra chính cổng đã nhận gói.
     - `LOCAL`: Gửi lên ngăn xếp mạng nội bộ của chính switch.
     - `TABLE`: Đưa gói tin sang Flow Table kế tiếp trong đường ống (Pipeline Processing).
   - **Drop:** Hủy bỏ gói tin (tương đương tường lửa Firewall).
   - **Modify-Field:** Viết lại tiêu đề gói tin (sửa đổi địa chỉ MAC, IP, thay đổi cổng TCP/UDP, hoặc giảm giá trị TTL/Hop Limit - tính năng của Router và NAT).
   - **Push/Pop Tag:** Thêm hoặc bóc tách nhãn VLAN tag hoặc MPLS label.
   - **Meter:** Giới hạn tốc độ luồng dữ liệu (Rate-limiting QoS).
5. **Thời gian sống của Luật (Timeouts):**
   - **Idle_timeout:** Nếu trong vòng $X$ giây liên tiếp mà không có bất kỳ gói tin nào khớp với luật này $\to$ Switch tự động xóa luật để giải phóng bộ nhớ TCAM.
   - **Hard_timeout:** Sau đúng $Y$ giây kể từ thời điểm nạp luật, switch bắt buộc phải xóa luật, **bất kể luật đó có đang được sử dụng hay không**.
6. **Cookie:**
   Giá trị số nguyên 64-bit do Controller gán vào để phân loại hoặc quản lý các nhóm luật do ứng dụng cụ thể tạo ra.

---

### 7.5. Cơ chế xử lý luồng: Reactive Mode vs. Proactive Mode

```
[ Gói tin đến Switch ]
          |
          v
  Khớp Flow Entry?  --- CÓ ---> [ Thực thi Action (Forward / Drop) ] (Tốc độ cáp)
          |
         KHÔNG (Table-Miss)
          |
          +---> Chế độ PROACTIVE: Drop ngay lập tức hoặc gửi theo Default rule.
          |
          +---> Chế độ REACTIVE:
                    1. Đóng gói gửi [ Packet-In ] lên Controller.
                    2. Controller tính toán đường đi.
                    3. Controller gửi [ Flow-Mod ] nạp luật xuống Switch.
                    4. Controller gửi [ Packet-Out ] để Switch phát gói tin đi.
```

#### 1. Chế độ Phản ứng (Reactive Mode)
- **Kịch bản:** Khi một gói tin đầu tiên của luồng mới ập đến switch mà chưa có luật nào trong Flow Table khớp (gọi là sự kiện **Table-Miss**):
  1. Switch tạm giữ gói tin trong bộ đệm và gửi bản tin **`Packet-In`** lên Controller.
  2. Controller nhận `Packet-In`, phân tích tiêu đề gói tin, tra cứu sơ đồ mạng và tính toán đường đi tối ưu.
  3. Controller gửi bản tin **`Flow-Mod`** xuống switch để cài đặt một Flow Entry mới vào Flow Table.
  4. Controller gửi bản tin **`Packet-Out`** ra lệnh cho switch chuyển tiếp gói tin đang bị giữ ra cổng đích thích hợp.
  5. Các gói tin tiếp theo của cùng luồng đó khi đến switch sẽ khớp ngay với luật vừa cài đặt và được chuyển tiếp ở tốc độ phần cứng cực nhanh mà không cần hỏi Controller nữa.
- **Ưu điểm:** Cực kỳ linh hoạt, tối ưu hóa bộ nhớ phần cứng (chỉ cài luật cho các luồng đang thực sự hoạt động).
- **Nhược điểm:** Gói tin đầu tiên bị trễ (First-packet latency); Controller dễ bị nghẽn nếu có hàng triệu luồng mới xuất hiện đồng thời.

#### 2. Chế độ Chủ động (Proactive Mode)
- **Kịch bản:** Controller tính toán trước toàn bộ các đường đi khả dĩ và chủ động gửi bản tin `Flow-Mod` nạp sẵn toàn bộ các luật chuyển tiếp xuống Flow Table của switch ngay từ đầu (trước khi lưu lượng thực tế xuất hiện).
- **Ưu điểm:** Không có độ trễ gói tin đầu tiên (Zero first-packet latency); switch hoạt động độc lập ngay cả khi mất kết nối tạm thời với Controller.
- **Nhược điểm:** Tốn kém dung lượng bộ nhớ phần cứng TCAM quý giá; kém linh hoạt khi có sự cố mạng bất ngờ.

---

### 7.6. Hệ điều hành mạng (Network OS / Controller) & Ứng dụng SDN

#### Các bộ điều khiển SDN phổ biến hiện nay
- **Ryu:** Bộ điều khiển viết hoàn toàn bằng **Python**, mã nguồn mở do NTT phát triển. Cực kỳ gọn nhẹ, trực quan, hỗ trợ OpenFlow 1.0 đến 1.5, là công cụ giảng dạy và thực hành chính trong môn học CSC11004 (kết hợp với trình giả lập mạng Mininet).
- **ONOS (Open Network Operating System):** Viết bằng Java, thiết kế riêng cho các nhà mạng viễn thông (Telco) và trung tâm dữ liệu khổng lồ, hỗ trợ kiến trúc phân tán và khả năng chịu lỗi cao.
- **OpenDaylight (ODL):** Dự án mã nguồn mở quy mô lớn dưới sự bảo trợ của Linux Foundation.

#### Ứng dụng sát thủ (Killer Apps) của SDN
1. **Ảo hóa mạng trong Trung tâm dữ liệu Đám mây (Data Center Network Virtualization):**
   Trong môi trường Cloud Multi-tenant (như AWS, Google Cloud, OpenStack), hàng nghìn máy ảo của các khách hàng khác nhau cùng chạy trên một hạ tầng phần cứng. SDN cho phép tạo ra các mạng riêng ảo (Overlay Virtual Networks) cách ly hoàn toàn về mặt logic thông qua các đường hầm VXLAN / Geneve được lập trình tự động.
2. **Kỹ thuật điều khiển lưu lượng WAN (Traffic Engineering - WAN TE):**
   Mạng WAN liên lục địa của Google (**Google B4**) sử dụng SDN tập trung để giám sát tải của các tuyến cáp quang biển. Nhờ Controller tính toán đường đi tập trung, Google đã nâng hiệu suất khai thác băng thông đường truyền từ mức trung bình 30% - 40% của mạng truyền thống lên **gần 100% dung lượng liên kết**, tiết kiệm hàng tỷ USD chi phí đầu tư cáp mới.

---

## PHẦN 8: BẢNG TRA CỨU NHANH CÔNG THỨC, THAM SỐ & LỆNH CẤU HÌNH THỰC HÀNH

### 8.1. Bảng tổng hợp các công thức toán học trọng tâm

| Đại lượng / Khái niệm | Công thức toán học chuẩn | Ý nghĩa & Ứng dụng thi trắc nghiệm |
| :--- | :--- | :--- |
| **Ước lượng RTT (EWMA)** | $EstimatedRTT = (1-\alpha) EstimatedRTT + \alpha \cdot SampleRTT$ | $\alpha = 0.125 = 1/8$ (Hệ số làm mượt RTT của TCP) |
| **Độ lệch RTT (DevRTT)** | $DevRTT = (1-\beta) DevRTT + \beta \cdot \lvert SampleRTT - EstimatedRTT \rvert$ | $\beta = 0.25 = 1/4$ (Độ biến thiên trễ khứ hồi) |
| **Khoảng Timeout RTO** | $RTO = EstimatedRTT + 4 \cdot DevRTT$ | Bộ đếm thời gian truyền lại của TCP (Karn-Partridge: nhân đôi khi timeout) |
| **Throughput Mathis (TCP)** | $\text{Throughput} \le \frac{MSS}{RTT} \sqrt{\frac{3}{2p}} \approx \frac{1.22 \cdot MSS}{RTT \cdot \sqrt{p}}$ | Giới hạn thông lượng tối đa của TCP Reno qua tỷ lệ mất gói $p$ |
| **Cửa sổ CUBIC** | $W_{cubic}(t) = C(t - K)^3 + W_{max} , \; K = \sqrt[3]{\frac{W_{max} \cdot 0.3}{C}}$ | $C = 0.4, \beta = 0.7$ (Giảm 30% khi mất gói, độc lập RTT) |
| **Điểm tối ưu Kleinrock** | $\text{Rate} = BtlBw; \quad \text{Inflight} = BDP = BtlBw \times RTprop$ | Trạng thái vận hành tối ưu của TCP BBR (Full Throughput, Min Delay) |
| **Buffer Sizing (Rule of Thumb)** | $B = RTT \times C$ | Kích thước bộ đệm router kinh điển cho 1 luồng TCP Reno |
| **Buffer Sizing (Stanford)** | $B = \frac{RTT \times C}{\sqrt{N}}$ | Kích thước bộ đệm cho $N$ luồng TCP độc lập qua core router |
| **Hàng đợi RED (EWMA)** | $avg \leftarrow (1 - w_q) \cdot avg + w_q \cdot q$ | $w_q = 0.002$ (Trọng số tính độ dài hàng đợi trung bình) |
| **Xác suất drop RED ($p_b$)** | $p_b = max_p \cdot \frac{avg - min_{th}}{max_{th} - min_{th}}$ | Xác suất nền tảng khi $min_{th} \le avg < max_{th}$ |
| **Xác suất drop thực tế ($p_a$)**| $p_a = \frac{p_b}{1 - count \cdot p_b}$ | $count$ là số gói đã chấp nhận; giúp phân bố gói drop đều đặn |
| **Thời gian burst Token Bucket**| $T = \frac{b}{M - r}$ | $b$: Dung lượng thùng token, $r$: Tốc độ sinh token, $M$: Tốc độ đỉnh phát |
| **Lượng dữ liệu burst tối đa** | $S = M \cdot T = \frac{b \cdot M}{M - r}$ | Tổng số bytes truyền được ở tốc độ tối đa $M$ trong khoảng thời gian $T$ |
| **WFQ Finish Time** | $F_i^k = \max(F_i^{k-1}, V(a_i^k)) + \frac{L_i^k}{w_i}$ | $w_i = \text{IP\_Precedence} + 1$; gói có $F$ nhỏ nhất được phát trước |
| **Chi phí OSPF (Cost)** | $\text{Cost} = \frac{\text{Reference Bandwidth}}{\text{Interface Bandwidth}} = \frac{10^8 \text{ bps}}{\text{BW}}$ | Mặc định cổng 100 Mbps và 1 Gbps đều có Cost = 1 |

---

### 8.2. Bảng đối chiếu các thông số & Cổng dịch vụ chuẩn

| Giao thức / Thành phần | Tầng (Layer) | Giao thức tầng dưới & Cổng (Port) | Địa chỉ Multicast chuẩn | Administrative Distance |
| :--- | :--- | :--- | :--- | :--- |
| **RIPv1** | Application | UDP Cổng **520** | `255.255.255.255` (Broadcast) | **120** |
| **RIPv2** | Application | UDP Cổng **520** | `224.0.0.9` (All RIP Routers) | **120** |
| **RIPng (IPv6)** | Application | UDP Cổng **521** | `ff02::9` (All RIPng Routers) | **120** |
| **OSPFv2** | Network | Trực tiếp trên IP (Protocol **89**) | `224.0.0.5` (All), `224.0.0.6` (DR/BDR)| **110** |
| **OSPFv3 (IPv6)** | Network | Trực tiếp trên IPv6 (Next Header **89**) | `ff02::5` (All), `ff02::6` (DR/BDR) | **110** |
| **BGPv4** | Application | TCP Cổng **179** | Unicast láng giềng (Peering) | **eBGP: 20, iBGP: 200** |
| **ICMPv6 / NDP** | Network | Trực tiếp trên IPv6 (Next Header **58**) | `ff02::1` (Nodes), `ff02::2` (Routers) | N/A |
| **OpenFlow** | Control Plane | TCP / TLS Cổng **6653** (cũ 6633) | Unicast kết nối Controller | N/A |

---

### 8.3. Bảng tổng hợp các tập lệnh cấu hình CLI thực hành (Cisco IOS & GNS3)

```cisco
! ====================================================================
! 1. ĐỊNH TUYẾN TĨNH (STATIC ROUTING)
! ====================================================================
! Cấu hình route tĩnh chỉ định Next-Hop IP
Router(config)# ip route 192.168.2.0 255.255.255.0 10.0.0.2

! Cấu hình Default Route (Tuyến mặc định)
Router(config)# ip route 0.0.0.0 0.0.0.0 10.0.0.2

! Cấu hình Floating Static Route (Dự phòng cho OSPF với AD = 130)
Router(config)# ip route 192.168.2.0 255.255.255.0 10.0.0.2 130

! ====================================================================
! 2. GIAO THỨC RIPv2
! ====================================================================
Router(config)# router rip
Router(config-router)# version 2
Router(config-router)# no auto-summary
Router(config-router)# network 192.168.1.0
Router(config-router)# network 10.0.0.0
Router(config-router)# passive-interface FastEthernet0/0
Router(config-router)# default-information originate

! ====================================================================
! 3. GIAO THỨC OSPFv2
! ====================================================================
Router(config)# router ospf 1
Router(config-router)# router-id 1.1.1.1
Router(config-router)# auto-cost reference-bandwidth 1000
Router(config-router)# network 192.168.1.0 0.0.0.255 area 0
Router(config-router)# network 10.0.0.0 0.0.0.3 area 0
Router(config-router)# passive-interface FastEthernet0/0
Router(config-router)# redistribute rip subnets   ! Tái phân phối route từ RIP sang OSPF

! Thiết lập Priority bầu chọn DR/BDR trên cổng giao tiếp
Router(config)# interface FastEthernet0/0
Router(config-if)# ip ospf priority 200            ! Priority cao nhất sẽ thắng cử DR

! ====================================================================
! 4. GIAO THỨC BGPv4
! ====================================================================
Router(config)# router bgp 65001
Router(config-router)# neighbor 10.0.0.2 remote-as 65002        ! Cấu hình eBGP Peer
Router(config-router)# neighbor 192.168.1.2 remote-as 65001     ! Cấu hình iBGP Peer
Router(config-router)# neighbor 192.168.1.2 update-source Loopback0
Router(config-router)# neighbor 192.168.1.2 next-hop-self
Router(config-router)# network 172.16.0.0 mask 255.255.0.0

! Gán thuộc tính BGP bằng Route-Map
Router(config-route-map)# set weight 500
Router(config-route-map)# set local-preference 200
Router(config-route-map)# set metric 50                         ! MED

! ====================================================================
! 5. CẤU HÌNH IPV6 CƠ BẢN & OSPFv3
! ====================================================================
Router(config)# ipv6 unicast-routing                            ! BẮT BUỘC: Bật chuyển tiếp IPv6 trên router
Router(config)# interface FastEthernet0/0
Router(config-if)# ipv6 address 2001:db8:1::1/64
Router(config-if)# ipv6 address fe80::1 link-local              ! Gán địa chỉ Link-Local thủ công
Router(config-if)# ipv6 nd other-config-flag                    ! Bật cờ O=1 (Stateless DHCPv6)
Router(config-if)# ipv6 nd managed-config-flag                  ! Bật cờ M=1 (Stateful DHCPv6)
Router(config-if)# ipv6 ospf 1 area 0                           ! Bật OSPFv3 trực tiếp trên interface
Router(config)# ipv6 router ospf 1
Router(config-rtr)# router-id 1.1.1.1                           ! OSPFv3 bắt buộc phải có RID 32-bit dạng IPv4
```

---

## PHẦN 9: NGÂN HÀNG CÂU HỎI TRẮC NGHIỆM VÀ BÀI TẬP TÍNH TOÁN ÔN THI TRỌNG TÂM CÓ LỜI GIẢI CHI TIẾT

### 9.1. Dạng bài 1: Trace bảng cửa sổ tắc nghẽn TCP (Tahoe vs. Reno)

#### Đề bài mẫu
Một kết nối TCP bắt đầu truyền với $cwnd = 1\text{ MSS}$, ngưỡng khởi động chậm ban đầu $ssthresh = 16\text{ MSS}$. Giả sử kích thước bộ đệm nhận $rwnd$ rất lớn và không ảnh hưởng đến quá trình truyền.
- Tại vòng **RTT thứ 6**, xảy ra sự kiện **Timeout (RTO)**.
- Kết nối tiếp tục phục hồi và truyền dữ liệu. Đến vòng **RTT thứ 13**, xảy ra sự kiện nhận được **3 Duplicate ACKs**.
**Yêu cầu:** Hãy lập bảng theo dõi sự biến thiên của giá trị $cwnd$ và $ssthresh$ từ RTT 1 đến RTT 17 cho cả hai biến thể: **TCP Tahoe** và **TCP Reno**.

#### Lời giải chi tiết từng bước

```
+-----+-----------------------+-----------------------+------------------------------------------+
|     |       TCP TAHOE       |       TCP RENO        |                                          |
| RTT | cwnd (MSS) | ssthresh | cwnd (MSS) | ssthresh | Diễn giải sự kiện & Chế độ hoạt động     |
+-----+------------+----------+------------+----------+------------------------------------------+
|  1  |     1      |    16    |     1      |    16    | Slow Start (Tăng gấp đôi mỗi RTT)        |
|  2  |     2      |    16    |     2      |    16    | Slow Start                               |
|  3  |     4      |    16    |     4      |    16    | Slow Start                               |
|  4  |     8      |    16    |     8      |    16    | Slow Start                               |
|  5  |    16      |    16    |    16      |    16    | Chạm ngưỡng ssthresh -> Congestion Avoid |
|  6  |    17      |    16    |    17      |    16    | [SỰ KIỆN 1]: TIMEOUT XẢY RA!             |
+-----+------------+----------+------------+----------+------------------------------------------+
|  7  |     1      |     8    |     1      |     8    | Cả Tahoe và Reno: ssthresh = 17/2 = 8,   |
|     |            |          |            |          | cwnd = 1 MSS -> Rơi về Slow Start!       |
|  8  |     2      |     8    |     2      |     8    | Slow Start                               |
|  9  |     4      |     8    |     4      |     8    | Slow Start                               |
| 10  |     8      |     8    |     8      |     8    | Chạm ngưỡng ssthresh -> Congestion Avoid |
| 11  |     9      |     8    |     9      |     8    | Congestion Avoidance (+1 MSS / RTT)      |
| 12  |    10      |     8    |    10      |     8    | Congestion Avoidance                     |
| 13  |    11      |     8    |    11      |     8    | [SỰ KIỆN 2]: 3 DUPLICATE ACKS XẢY RA!    |
+-----+------------+----------+------------+----------+------------------------------------------+
| 14  |     1      |     5    |     5      |     5    | Tahoe: ssthresh=11/2=5, cwnd=1 (SS)      |
|     |            |          |            |          | Reno: ssthresh=11/2=5, cwnd=ssthresh=5   |
|     |            |          |            |          | (Thoát Fast Recovery -> Congestion Avoid)|
| 15  |     2      |     5    |     6      |     5    | Tahoe: Slow Start (1 -> 2)               |
|     |            |          |            |          | Reno: Congestion Avoidance (5 -> 6)      |
| 16  |     4      |     5    |     7      |     5    | Tahoe: Slow Start (2 -> 4)               |
|     |            |          |            |          | Reno: Congestion Avoidance (6 -> 7)      |
| 17  |     5      |     5    |     8      |     5    | Tahoe: Chạm ssthresh=5 -> CA             |
|     |            |          |            |          | Reno: Congestion Avoidance (7 -> 8)      |
+-----+------------+----------+------------+----------+------------------------------------------+
```

> **Bài học rút ra:** Tại RTT 14, khi gặp 3 Duplicate ACKs:
> - Tahoe phạt nặng: đẩy $cwnd$ về $1\text{ MSS}$ (Slow Start).
> - Reno giữ đường ống: đẩy $cwnd$ về $ssthresh = 5\text{ MSS}$ và chuyển sang Congestion Avoidance (tăng $+1$ mỗi RTT).

---

### 9.2. Dạng bài 2: Tính toán Kích thước Bộ đệm Router (Buffer Sizing)

#### Đề bài mẫu
Một router lõi kết nối đường truyền cáp quang có băng thông $C = 10\text{ Gbps}$. Độ trễ khứ hồi trung bình qua liên kết là $RTT = 200\text{ ms}$.
1. Tính kích thước bộ đệm router cần thiết theo Quy tắc kinh điển (Rule of Thumb).
2. Tính kích thước bộ đệm router theo Mô hình Stanford nếu qua router có đồng thời $N = 400$ luồng TCP độc lập hoạt động.
3. Kích thước bộ đệm theo mô hình Stanford giảm bao nhiêu lần so với Rule of Thumb?

#### Lời giải chi tiết
1. **Theo Quy tắc kinh điển (Rule of Thumb):**  
   $B_{\text{classic}} = RTT \times C = (200 \times 10^{-3}\text{ s}) \times (10 \times 10^9\text{ bps}) = 2 \times 10^9\text{ bits}$  
   Đổi sang Megabytes: $B_{\text{classic}} = \frac{2 \times 10^9\text{ bits}}{8 \times 10^6\text{ bits/MB}} = 250\text{ MB}$

2. **Theo Mô hình Stanford:**  
   $B_{\text{stanford}} = \frac{RTT \times C}{\sqrt{N}} = \frac{250\text{ MB}}{\sqrt{400}} = \frac{250\text{ MB}}{20} = 12.5\text{ MB}$

3. **Mức độ suy giảm:**  
   $\text{Reduction Ratio} = \frac{B_{\text{classic}}}{B_{\text{stanford}}} = \sqrt{N} = \sqrt{400} = 20 $

---

### 9.3. Dạng bài 3: Tính toán Xác suất Loại bỏ gói của RED

#### Đề bài mẫu
Một bộ định tuyến kích hoạt thuật toán RED với các thông số cấu hình: $min_{th} = 20\text{ packets}$, $max_{th} = 80\text{ packets}$, và xác suất drop tối đa $max_p = 0.1$.
1. Tại thời điểm xét, độ dài hàng đợi trung bình tính được là $avg = 50\text{ packets}$. Tính xác suất nền tảng $p_b$.
2. Giả sử đã có liên tiếp $count = 15$ gói tin được chấp nhận vào hàng đợi kể từ lần drop gói gần nhất. Hãy tính xác suất loại bỏ thực tế $p_a$ áp dụng cho gói tin hiện tại.
3. Nếu độ dài hàng đợi trung bình tăng vọt lên $avg = 85\text{ packets}$, xác suất drop sẽ là bao nhiêu?

#### Lời giải chi tiết
1. **Tính xác suất nền tảng $p_b$:**  
   Vì $min_{th} \le avg < max_{th}$ ($20 \le 50 < 80$):  
   $p_b = max_p \cdot \frac{avg - min_{th}}{max_{th} - min_{th}} = 0.1 \cdot \frac{50 - 20}{80 - 20} = 0.1 \cdot \frac{30}{60} = 0.05 \quad (5\%)$

2. **Tính xác suất thực tế $p_a$ theo biến đếm $count$:**  
   $p_a = \frac{p_b}{1 - count \cdot p_b} = \frac{0.05}{1 - 15 \cdot 0.05} = \frac{0.05}{1 - 0.75} = \frac{0.05}{0.25} = 0.20 \quad (20\%)$

3. **Khi $avg = 85\text{ packets}$:**  
   Vì $avg \ge max_{th}$ ($85 \ge 80$), hàng đợi rơi vào vùng nghẽn nghiêm trọng: $P = 1.0 \quad (100\%)$. 

---

### 9.4. Dạng bài 4: Tính toán Lưu lượng Bùng nổ Token Bucket

#### Đề bài mẫu
Một cơ chế điều hòa lưu lượng Token Bucket có dung lượng thùng $b = 2\text{ Megabytes} = 16\text{ Megabits}$. Tốc độ nạp token vào thùng là $r = 10\text{ Mbps}$. Giao diện mạng đầu ra có tốc độ truyền tối đa đường truyền là $M = 50\text{ Mbps}$.
1. Giả sử thùng token đang đầy 100%. Hãy tính thời gian tối đa $T$ mà máy chủ có thể phát dữ liệu bùng nổ liên tục ở tốc độ cực đại $M = 50\text{ Mbps}$.
2. Tính tổng lượng dữ liệu $S$ (tính bằng Megabytes) truyền được trong đợt bùng nổ đó.

#### Lời giải chi tiết
1. **Thời gian bùng nổ cực đại $T$:**  
   Áp dụng công thức cân bằng token tiêu thụ và token sinh ra: $b + r \cdot T = M \cdot T \implies T = \frac{b}{M - r}$  
   Thay số: $T = \frac{16\text{ Mbits}}{50\text{ Mbps} - 10\text{ Mbps}} = \frac{16}{40} = 0.4\text{ s} $

2. **Tổng lượng dữ liệu truyền được trong đợt burst ($S$):**  
   $S = M \cdot T = 50\text{ Mbps} \times 0.4\text{ s} = 20\text{ Megabits} = 2.5\text{ Megabytes}$

   *(Kiểm chứng: $2\text{ MB}$ có sẵn trong thùng $+ (10\text{ Mbps} \times 0.4\text{ s} = 4\text{ Mbits} = 0.5\text{ MB})$ mới sinh $= 2.5\text{ MB}$).*

---

### 9.5. Dạng bài 5: Lập lịch hàng đợi Weighted Fair Queuing (WFQ)

#### Đề bài mẫu
Xét một router chạy giải thuật lập lịch WFQ. Có hai luồng dữ liệu đến:
- Luồng 1 có IP Precedence = 0 $\to$ Trọng số $w_1 = \text{IP\_Prec} + 1 = 1$.
- Luồng 2 có IP Precedence = 3 $\to$ Trọng số $w_2 = \text{IP\_Prec} + 1 = 4$.
Tại thời điểm ban đầu thời gian ảo $V(0) = 0$, cả hai luồng đều rỗng. Sau đó:
- Gói tin $P_{1,1}$ thuộc Luồng 1 đến tại thời điểm $a = 0$, kích thước $L = 100\text{ bytes}$.
- Gói tin $P_{2,1}$ thuộc Luồng 2 đến tại thời điểm $a = 0$, kích thước $L = 200\text{ bytes}$.
- Gói tin $P_{1,2}$ thuộc Luồng 1 đến ngay sau đó, kích thước $L = 100\text{ bytes}$.
**Yêu cầu:** Tính thời gian hoàn thành ảo $F$ của từng gói tin và chỉ ra thứ tự các gói tin được router phát đi.

#### Lời giải chi tiết
Công thức tính thời gian ảo hoàn thành: $F_i^k = \max(F_i^{k-1}, V(a_i^k)) + \frac{L_i^k}{w_i}$

1. **Gói $P_{1,1}$ (Luồng 1):** $F_{1,1} = \max(0, 0) + \frac{100}{1} = 100$
2. **Gói $P_{2,1}$ (Luồng 2):** $F_{2,1} = \max(0, 0) + \frac{200}{4} = 50$
3. **Gói $P_{1,2}$ (Luồng 1):** $F_{1,2} = \max(F_{1,1}, 0) + \frac{100}{1} = 100 + \frac{100}{1} = 200$

**Thứ tự phát gói (Ưu tiên gói có $F$ nhỏ nhất trước):**
1. Gói $P_{2,1}$ phát đầu tiên (vì $F = 50$).
2. Gói $P_{1,1}$ phát thứ hai (vì $F = 100$).
3. Gói $P_{1,2}$ phát cuối cùng (vì $F = 200$).

---

### 9.6. Dạng bài 6: Nén và Giải nén Địa chỉ IPv6 theo RFC 5952

#### Bài tập 1: Nén địa chỉ
Hãy nén các địa chỉ sau đây về dạng chuẩn ngắn gọn nhất theo đúng RFC 5952:
1. `2001:0db8:0000:0000:0000:0000:0000:0001`
   - Bỏ số 0 đầu: `2001:db8:0:0:0:0:0:1`
   - Dùng `::` nén dãy 0 dài nhất: **`2001:db8::1`**
2. `fe80:0000:0000:0000:020c:29ff:fe53:45a1`
   - Nén chuẩn: **`fe80::20c:29ff:fe53:45a1`**
3. `2001:0000:0000:abcd:0000:0000:0000:1234`
   - Có 2 dãy số 0: dãy 1 gồm 2 nhóm, dãy 2 gồm 3 nhóm.
   - Bắt buộc nén dãy dài hơn (dãy 3 nhóm): **`2001:0:0:abcd::1234`**
4. `2001:0db8:0000:0000:1234:0000:0000:5678`
   - Có 2 dãy số 0 cùng có độ dài bằng nhau (2 nhóm).
   - Quy tắc giải quyết hòa: Nén dãy đầu tiên xuất hiện bên trái: **`2001:db8::1234:0:0:5678`**

#### Bài tập 2: Giải nén địa chỉ
Hãy bung đầy đủ 128-bit (8 hextets, mỗi hextet 4 chữ số hex) cho địa chỉ: **`2001:db8:1::ab`**
- Đếm số hextet đã hiển thị: `2001` (1), `db8` (2), `1` (3), `ab` (4) $\to$ Đã có 4 hextets.
- Số hextets bị ẩn bên trong dấu `::` là: $8 - 4 = 4$ hextets toàn số 0.
- Kết quả bung đầy đủ:
  **`2001:0db8:0001:0000:0000:0000:0000:00ab`**

---

### 9.7. Dạng bài 7: Chuyển đổi MAC sang Interface ID Modified EUI-64

#### Đề bài mẫu
Cho địa chỉ MAC của card mạng Ethernet: `34-56-FE-89-AB-CD`.
Hãy tạo Interface ID 64-bit theo chuẩn Modified EUI-64 và viết địa chỉ Link-Local hoàn chỉnh của giao diện này.

#### Lời giải chi tiết
1. **Chia đôi địa chỉ MAC:**
   `34:56:FE` và `89:AB:CD`
2. **Chèn `FF:FE` vào giữa:**
   `34:56:FE:FF:FE:89:AB:CD`
3. **Đảo bit thứ 7 của byte đầu tiên (`34` Hex):**
   - Đổi `34` sang nhị phân 8 bits: `0011 0100_2`
   - Bit thứ 7 (tính từ trái sang: bit 0, 1, 2, 3, 4, 5, 6, [7]):
     `0 0 1 1   0 1 [0] 0`
   - Đảo bit `0` thành `1`:
     `0 0 1 1   0 1 [1] 0` $\to$ Đổi lại Hex: `36`
4. **Ghép thành Interface ID 64-bit (4 hextets):**
   **`3656:feff:fe89:abcd`**
5. **Địa chỉ Link-Local hoàn chỉnh:**
   Ghép với tiền tố `fe80::/64`:
   **`fe80::3656:feff:fe89:abcd`**

---

### 9.8. Dạng bài 8: Phân tích Thuật toán chọn đường BGP Best Path Selection

#### Đề bài mẫu
Router R1 (thuộc AS 100) nhận được 4 thông báo đường đi BGP khác nhau để đi tới mạng đích `172.16.0.0/16` như bảng sau:

| Tuyến (Path) | Weight | Local_Pref | Next_Hop | AS_PATH | Origin | MED | Loại phiên | Metric IGP đến Next_Hop |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **Path A** | 0 | 100 | 10.1.1.2 | `200 300 400` | IGP | 50 | eBGP | 20 |
| **Path B** | 300 | 100 | 10.2.2.2 | `200 500` | IGP | 100 | iBGP | 10 |
| **Path C** | 0 | 200 | 10.3.3.2 | `200 500` | IGP | 0 | eBGP | 30 |
| **Path D** | 0 | 200 | 10.4.4.2 | `200 500 600` | EGP | 0 | eBGP | 15 |

**Yêu cầu:** Áp dụng thuật toán BGP Best Path Selection, hãy phân tích từng bước và kết luận tuyến đường nào sẽ được R1 chọn làm Best Path?

#### Lời giải chi tiết
- **Bước 1 (So sánh WEIGHT - Cao nhất thắng):**
  - Path A: `Weight = 0`
  - Path B: `Weight = 300`
  - Path C: `Weight = 0`
  - Path D: `Weight = 0`
  - **KẾT LUẬN NGAY:** Path B có `Weight = 300` cao nhất trong tất cả các tuyến!
  - Vì bước 1 là bước đầu tiên và Path B có giá trị Weight vượt trội (300 so với 0), thuật toán **LẬP TỨC DỪNG LẠI VÀ CHỌN PATH B LÀ BEST PATH**!
  *(Mặc dù Path B là iBGP và Local_Pref thấp hơn Path C/D, nhưng thuộc tính WEIGHT của Cisco có trọng số ưu tiên cao nhất tuyệt đối).*

*Mở rộng giả định:* Nếu Path B có `Weight = 0` (hòa ở Bước 1):
- **Bước 2 (So sánh LOCAL_PREF - Cao nhất thắng):**
  - Path A có `Local_Pref = 100` (bị loại).
  - Path C và Path D cùng có `Local_Pref = 200` (Path C và D tiếp tục vào vòng trong).
- **Bước 3 (Locally Originated):** Cả C và D đều học từ ngoài (hòa).
- **Bước 4 (AS_PATH ngắn nhất):**
  - Path C có độ dài AS_PATH = 2 (`200 500`).
  - Path D có độ dài AS_PATH = 3 (`200 500 600`).
  - $\to$ **Path C sẽ chiến thắng** nhờ có chiều dài AS_PATH ngắn hơn!

---

### 9.9. Ngân hàng 50 Câu hỏi Trắc nghiệm Lý thuyết Ôn thi Trọng tâm

#### Chuyên đề 1: Điều khiển tắc nghẽn TCP (10 Câu)

**Câu 1:** Trong giao thức TCP, cơ chế nào bảo vệ bộ đệm của máy nhận và cơ chế nào bảo vệ các router trên mạng?  
A. Cả hai đều do Congestion Control đảm nhiệm.  
B. Flow Control bảo vệ máy nhận; Congestion Control bảo vệ router mạng.  
C. Congestion Control bảo vệ máy nhận; Flow Control bảo vệ router mạng.  
D. Cả hai đều do Flow Control đảm nhiệm.  
*Đáp án:* **B**. (Flow control dựa trên `rwnd` của receiver; Congestion control dựa trên `cwnd` của sender).

**Câu 2:** Biến thể TCP Tahoe phản ứng như thế nào khi nhận được 3 Duplicate ACKs?  
A. $ssthresh = cwnd/2$, $cwnd = ssthresh + 3\text{ MSS}$, vào Fast Recovery.  
B. $ssthresh = cwnd/2$, $cwnd = ssthresh$, vào Congestion Avoidance.  
C. $ssthresh = cwnd/2$, $cwnd = 1\text{ MSS}$, vào Slow Start.  
D. Giữ nguyên $cwnd$, chỉ truyền lại gói bị thiếu.  
*Đáp án:* **C**. (Tahoe không có Fast Recovery; mọi sự cố rớt gói đều đưa $cwnd$ về $1\text{ MSS}$).

**Câu 3:** Tại sao thuật toán AIMD được chọn cho TCP thay vì MIMD hay AIAD?  
A. Vì AIMD giúp tăng tốc độ truyền nhanh nhất.  
B. Vì AIMD trong phân tích vector không gian Chiu & Jain là cơ chế duy nhất hội tụ về cả đường Hiệu quả và đường Công bằng.  
C. Vì AIMD không cần phía nhận phải gửi bản tin ACK.  
D. Vì AIMD giúp loại bỏ hoàn toàn hiện tượng mất gói trên mạng.  
*Đáp án:* **B**.

**Câu 4:** Điểm khác biệt mấu chốt giữa TCP Reno và TCP Tahoe là gì?  
A. Reno bổ sung cơ chế Fast Recovery khi nhận 3 Dup ACKs, không đưa $cwnd$ về $1\text{ MSS}$.  
B. Reno không sử dụng ngưỡng $ssthresh$.  
C. Reno không bị sụt giảm cửa sổ khi bị Timeout.  
D. Reno sử dụng độ trễ RTT để phát hiện tắc nghẽn thay vì mất gói.  
*Đáp án:* **A**.

**Câu 5:** Trong TCP Reno, khi đang truyền ở pha Congestion Avoidance với $cwnd = 20\text{ MSS}$, nếu xảy ra sự kiện **RTO Timeout**, giá trị $cwnd$ và $ssthresh$ tiếp theo là:  
A. $cwnd = 10\text{ MSS}, ssthresh = 10\text{ MSS}$.  
B. $cwnd = 1\text{ MSS}, ssthresh = 10\text{ MSS}$.  
C. $cwnd = 13\text{ MSS}, ssthresh = 10\text{ MSS}$.  
D. $cwnd = 1\text{ MSS}, ssthresh = 20\text{ MSS}$.  
*Đáp án:* **B**. (Khi TIMEOUT, Reno hành động giống hệt Tahoe: $ssthresh = 20/2 = 10\text{ MSS}$, $cwnd = 1\text{ MSS}$ và vào Slow Start!).

**Câu 6:** Thuật toán TCP CUBIC thay thế sự phụ thuộc vào RTT bằng đại lượng nào trong hàm tăng trưởng cửa sổ?  
A. Tỷ lệ mất gói $p$.  
B. Thời gian thực $t$ kể từ lần giảm cửa sổ gần nhất.  
C. Số lượng gói tin ECN nhận được.  
D. Dung lượng bộ đệm của router.  
*Đáp án:* **B**. ($W(t) = C(t-K)^3 + W_{max}$, hoàn toàn độc lập với RTT, đảm bảo tính công bằng giữa các luồng có RTT khác nhau).

**Câu 7:** Hệ số giảm cửa sổ nhân $\beta$ của TCP CUBIC khi phát hiện mất gói là bao nhiêu?  
A. $\beta = 0.5$ (giảm 50%).  
B. $\beta = 0.7$ (giảm 30%, giữ lại 70%).  
C. $\beta = 0.8$ (giảm 20%).  
D. $\beta = 0.1$ (giảm 90%).  
*Đáp án:* **B**.

**Câu 8:** Điểm vận hành tối ưu của thuật toán TCP BBR theo mô hình Kleinrock đạt được khi:  
A. Bộ đệm router đầy 100% để tối đa hóa băng thông.  
B. Tốc độ phát bằng $BtlBw$ và lượng dữ liệu in-flight đúng bằng $BDP = BtlBw \times RTprop$.  
C. Tỷ lệ mất gói đạt mức 10%.  
D. Cửa sổ $cwnd$ đạt giá trị vô cùng.  
*Đáp án:* **B**.

**Câu 9:** Để router báo hiệu tắc nghẽn cho máy gửi thông qua cơ chế ECN mà không cần drop gói, router ghi đè giá trị nào vào 2 bit ECN trong tiêu đề IP?  
A. `00` (Non-ECT).  
B. `01` (ECT(1)).  
C. `10` (ECT(0)).  
D. `11` (CE - Congestion Experienced).  
*Đáp án:* **D**.

**Câu 10:** Khi máy nhận nhận được gói tin có cờ `CE = 11`, nó thông báo cho máy gửi bằng cách bật cờ nào trong TCP Header của gói ACK?  
A. Cờ CWR.  
B. Cờ ECE (ECN-Echo).  
C. Cờ URG.  
D. Cờ RST.  
*Đáp án:* **B**.

---

#### Chuyên đề 2: Quản lý hàng đợi & AQM (8 Câu)

**Câu 11:** Trong kiến trúc phần cứng của Router, thành phần nào là nơi thường xuyên phát sinh hiện tượng thắt cổ chai và tích lũy hàng đợi nhất?  
A. Cổng vào (Input Port).  
B. Khung chuyển mạch (Switching Fabric).  
C. Cổng ra (Output Port).  
D. Bộ xử lý định tuyến (Routing Processor).  
*Đáp án:* **C**.

**Câu 12:** Hiện tượng "Đồng bộ toàn cục (Global Synchronization)" trong hàng đợi Drop Tail xảy ra do nguyên nhân nào?  
A. Do các router trao đổi bản tin định tuyến cùng một thời điểm.  
B. Do khi bộ đệm đầy, hàng loạt gói tin của nhiều luồng TCP cùng bị drop đồng thời, khiến tất cả các luồng cùng lùi bước giảm cửa sổ một lúc.  
C. Do đồng hồ phần cứng của các switch bị lệch pha.  
D. Do giao thức NTP bị lỗi.  
*Đáp án:* **B**.

**Câu 13:** Theo mô hình Stanford, nếu có $N$ luồng TCP độc lập cùng đi qua một bottleneck link, kích thước bộ đệm router $B$ cần thiết là:  
A. $B = RTT \times C \times N$.  
B. $B = \frac{RTT \times C}{N}$.  
C. $B = \frac{RTT \times C}{\sqrt{N}}$.  
D. $B = RTT \times C \times \sqrt{N}$.  
*Đáp án:* **C**.

**Câu 14:** Thuật toán RED tính toán xác suất loại bỏ gói tin dựa trên thông số nào sau đây?  
A. Độ dài hàng đợi tức thời $q$ tại thời điểm gói đến.  
B. Độ dài hàng đợi trung bình $avg$ được tính qua hàm trượt EWMA.  
C. Số lượng kết nối TCP đang mở.  
D. Tốc độ quạt tản nhiệt của router.  
*Đáp án:* **B**.

**Câu 15:** Trong thuật toán RED, nếu độ dài hàng đợi trung bình thỏa mãn $min_{th} \le avg < max_{th}$, gói tin đến sẽ bị xử lý như thế nào?  
A. Chấp nhận 100% không loại bỏ gói nào.  
B. Drop 100% tất cả các gói tin.  
C. Bị loại bỏ ngẫu nhiên với xác suất $p_a$ tăng dần theo $avg$ và số gói $count$.  
D. Gửi trả lại cho máy gửi.  
*Đáp án:* **C**.

**Câu 16:** Nhược điểm lớn nhất của thuật toán RED là gì?  
A. Không hỗ trợ giao thức IPv4.  
B. Rất nhạy cảm với việc chọn bộ tham số cấu hình và không trừng phạt được các luồng UDP bất hợp tác.  
C. Tiêu tốn nhiều băng thông đường truyền.  
D. Làm tăng hiện tượng đồng bộ toàn cục.  
*Đáp án:* **B**.

**Câu 17:** Biến thể nào của RED áp dụng các ngưỡng drop $(min_{th}, max_{th})$ khác nhau cho từng mức ưu tiên IP Precedence hoặc DSCP?  
A. FRED.  
B. WRED (Weighted RED).  
C. BLUE.  
D. CoDel.  
*Đáp án:* **B**.

**Câu 18:** Thuật toán CoDel (Controlled Delay) sử dụng thước đo nào để quyết định drop gói tin nhằm chống lại Bufferbloat?  
A. Kích thước gói tin tính bằng bytes.  
B. Số lượng cổng đang active trên switch.  
C. Thời gian lưu lại trong hàng đợi (Sojourn Time) của gói tin.  
D. Số lượng địa chỉ MAC học được.  
*Đáp án:* **C**.

---

#### Chuyên đề 3: Chất lượng dịch vụ - QoS (8 Câu)

**Câu 19:** Kỹ thuật điều hòa lưu lượng nào sau đây làm tăng độ trễ và jitter của gói tin do sử dụng bộ nhớ đệm để làm phẳng lưu lượng?  
A. Traffic Policing.  
B. Traffic Shaping.  
C. Packet Marking.  
D. Packet Filtering.  
*Đáp án:* **B**.

**Câu 20:** Điểm khác biệt căn bản giữa thuật toán Leaky Bucket và Token Bucket là gì?  
A. Leaky Bucket cho phép truyền bùng nổ (burst), còn Token Bucket thì không.  
B. Leaky Bucket ép tốc độ đầu ra luôn là hằng số cố định, trong khi Token Bucket cho phép truyền bùng nổ ở tốc độ đỉnh $M$ trong thời gian ngắn.  
C. Token Bucket không bao giờ làm mất gói tin.  
D. Leaky Bucket chỉ áp dụng cho mạng không dây.  
*Đáp án:* **B**.

**Câu 21:** Cơ chế lập lịch hàng đợi nào sau đây có nguy cơ gây "đói tài nguyên (starvation)" vĩnh viễn cho các hàng đợi mức thấp?  
A. Fair Queuing (FQ).  
B. Weighted Fair Queuing (WFQ).  
C. Strict Priority Queuing (PQ).  
D. Deficit Round Robin (DRR).  
*Đáp án:* **C**.

**Câu 22:** Giao thức báo hiệu đặt trước tài nguyên trong mô hình IntServ là gì?  
A. OSPF.  
B. RSVP (Resource Reservation Protocol).  
C. BGP.  
D. LDP.  
*Đáp án:* **B**.

**Câu 23:** Trong giao thức RSVP, phía nhận gửi bản tin nào ngược dòng (upstream) về phía nguồn để yêu cầu cấp phát băng thông và độ trễ?  
A. Bản tin PATH.  
B. Bản tin RESV.  
C. Bản tin SYN.  
D. Bản tin ACK.  
*Đáp án:* **B**.

**Câu 24:** Tại sao mô hình IntServ không thể triển khai trên quy mô toàn mạng Internet công cộng?  
A. Vì không tương thích với giao thức TCP.  
B. Vì các router lõi phải lưu trữ và duy trì trạng thái của hàng triệu luồng kết nối riêng lẻ (per-flow state), làm quá tải bộ nhớ và CPU.  
C. Vì IntServ chỉ hỗ trợ mạng cáp đồng.  
D. Vì không có cơ chế bảo mật.  
*Đáp án:* **B**.

**Câu 25:** Nhóm Per-Hop Behavior nào trong DiffServ được gán mã DSCP `101110` (thập phân 46), cung cấp dịch vụ trễ thấp, jitter thấp dành riêng cho VoIP?  
A. Default Forwarding (DF).  
B. Assured Forwarding (AF11).  
C. Expedited Forwarding (EF).  
D. Class Selector 1 (CS1).  
*Đáp án:* **C**.

**Câu 26:** Trong nhóm Assured Forwarding (AF), giá trị DSCP nào sau đây có nguy cơ bị router loại bỏ (drop) sớm nhất khi xảy ra tắc nghẽn mạng?  
A. AF11.  
B. AF12.  
C. AF13.  
D. AF41.  
*Đáp án:* **C**. (Trong cùng Class 1, số thứ hai biểu thị Drop Precedence: 1 là thấp nhất, 3 là cao nhất $\to$ AF13 bị drop trước tiên).

---

#### Chuyên đề 4: Định tuyến Internet (12 Câu)

**Câu 27:** Giả sử bảng định tuyến của router có các tuyến sau: `10.0.0.0/8`, `10.1.0.0/16`, và `10.1.1.0/24`. Gói tin có IP đích `10.1.1.50` sẽ được chuyển tiếp theo tuyến nào?  
A. `10.0.0.0/8`.  
B. `10.1.0.0/16`.  
C. `10.1.1.0/24`.  
D. Bị loại bỏ vì trùng lặp.  
*Đáp án:* **C**. (Theo nguyên lý Longest Prefix Match, `/24` là tiền tố dài nhất và cụ thể nhất).

**Câu 28:** Router học được đường tới cùng mạng đích qua cả OSPF và RIP. Tuyến đường nào sẽ được chọn cài vào bảng định tuyến RIB?  
A. RIP vì số bước nhảy (hop) ít hơn.  
B. OSPF vì có Administrative Distance nhỏ hơn (AD = 110 so với RIP có AD = 120).  
C. Router thực hiện cân bằng tải qua cả hai đường.  
D. Phụ thuộc vào tốc độ băng thông của card mạng.  
*Đáp án:* **B**.

**Câu 29:** Giá trị Administrative Distance (AD) mặc định của eBGP và iBGP lần lượt là bao nhiêu?  
A. eBGP = 110, iBGP = 120.  
B. eBGP = 20, iBGP = 200.  
C. eBGP = 90, iBGP = 170.  
D. eBGP = 1, iBGP = 255.  
*Đáp án:* **B**.

**Câu 30:** Cơ chế phòng chống vòng lặp định tuyến nào trong Distance Vector quy định "không quảng bá ngược lại tuyến đường ra chính cổng đã học được"?  
A. Route Poisoning.  
B. Split Horizon.  
C. Hold-down Timer.  
D. Poison Reverse.  
*Đáp án:* **B**.

**Câu 31:** Giá trị metric tối đa đại diện cho "Vô cùng (Unreachable)" trong giao thức RIP là bao nhiêu?  
A. 15 hops.  
B. 16 hops.  
C. 255 hops.  
D. 100 hops.  
*Đáp án:* **B**. (15 hops là đường đi hợp lệ tối đa; 16 hops là vô cùng/không thể tới).

**Câu 32:** Địa chỉ Multicast nào được giao thức RIPv2 sử dụng để gửi các bản tin cập nhật định tuyến?  
A. `224.0.0.5`.  
B. `224.0.0.6`.  
C. `224.0.0.9`.  
D. `255.255.255.255`.  
*Đáp án:* **C**.

**Câu 33:** Giao thức OSPF chạy trực tiếp trên nền IP sử dụng số hiệu giao thức (IP Protocol Number) là bao nhiêu?  
A. 6 (TCP).  
B. 17 (UDP).  
C. 89.  
D. 520.  
*Đáp án:* **C**.

**Câu 34:** Trên một liên kết mạng đa truy cập (Broadcast Multi-access), router nào trong OSPF sẽ lắng nghe trên địa chỉ Multicast `224.0.0.6`?  
A. Tất cả các router OSPF.  
B. Chỉ có DR (Designated Router) và BDR (Backup Designated Router).  
C. Các router biên vùng ABR.  
D. Chỉ có router có Router ID nhỏ nhất.  
*Đáp án:* **B**. (`224.0.0.5` dành cho All OSPF Routers; `224.0.0.6` dành cho All DR/BDR).

**Câu 35:** Thứ tự ưu tiên cao nhất khi một router OSPF tự động xác định Router ID (RID) nếu không có cấu hình thủ công là gì?  
A. Địa chỉ IP cao nhất trên các cổng vật lý đang active.  
B. Địa chỉ IP cao nhất trên các giao diện ảo Loopback đang active.  
C. Địa chỉ IP thấp nhất trên cổng Loopback.  
D. Địa chỉ MAC lớn nhất.  
*Đáp án:* **B**.

**Câu 36:** Giao thức BGPv4 thiết lập các phiên quan hệ láng giềng (Peering Session) dựa trên giao thức tầng giao vận nào?  
A. UDP cổng 520.  
B. TCP cổng 179.  
C. Trực tiếp trên IP protocol 89.  
D. ICMPv6.  
*Đáp án:* **B**.

**Câu 37:** Trong thuật toán lựa chọn đường đi BGP Best Path Selection, hai thuộc tính nào được xét ở 2 bước đầu tiên và theo quy tắc "Càng cao càng tốt"?  
A. AS_PATH và MED.  
B. WEIGHT và LOCAL_PREF.  
C. ORIGIN và NEXT_HOP.  
D. Router ID và Neighbor IP.  
*Đáp án:* **B**. (Bước 1: WEIGHT cao nhất; Bước 2: LOCAL_PREF cao nhất).

**Câu 38:** Kỹ thuật BGP Route Hijacking nguy hiểm nhất thường được kẻ tấn công thực hiện bằng cách nào để hút trọn lưu lượng của nạn nhân?  
A. Giảm giá trị MTU của gói tin.  
B. Quảng bá dải địa chỉ IP có tiền tố cụ thể hơn (More Specific Prefix / Longest Prefix Match).  
C. Tắt cổng mạng của nạn nhân.  
D. Gửi bản tin ICMP Redirect liên tục.  
*Đáp án:* **B**.

---

#### Chuyên đề 5: Giao thức IPv6 (8 Câu)

**Câu 39:** Kích thước tiêu đề cơ sở cố định (Base Header) của gói tin IPv6 là bao nhiêu bytes?  
A. 20 bytes.  
B. 32 bytes.  
C. 40 bytes.  
D. 64 bytes.  
*Đáp án:* **C**.

**Câu 40:** Trường nào trong IPv4 Header đã bị loại bỏ hoàn toàn trong tiêu đề cơ sở của IPv6 nhằm tăng tốc độ xử lý chuyển tiếp của router?  
A. Version.  
B. Header Checksum.  
C. Hop Limit.  
D. Destination Address.  
*Đáp án:* **B**.

**Câu 41:** Khi một router trung gian nhận được gói tin IPv6 có kích thước lớn hơn MTU của cổng xuất, hành vi chuẩn của router là gì?  
A. Phân mảnh gói tin IPv6 thành các mảnh nhỏ hơn rồi chuyển tiếp tiếp.  
B. Hủy bỏ gói tin và gửi bản tin ICMPv6 Type 2 "Packet Too Big" về cho máy nguồn.  
C. Lưu gói tin vào bộ đệm và đợi tăng băng thông.  
D. Tự động nén phần tải dữ liệu.  
*Đáp án:* **B**. (Router IPv6 không bao giờ phân mảnh!).

**Câu 42:** Dạng rút gọn chuẩn RFC 5952 của địa chỉ `fe80:0000:0000:0000:0000:0000:0000:0001` là gì?  
A. `fe80::1`.  
B. `fe80:0:0:0:0:0:0:1`.  
C. `fe80::0::1`.  
D. `fe80:1`.  
*Đáp án:* **A**.

**Câu 43:** Dải địa chỉ nào sau đây đại diện cho địa chỉ Link-Local trong IPv6?  
A. `2000::/3`.  
B. `fc00::/7`.  
C. `fe80::/10`.  
D. `ff00::/8`.  
*Đáp án:* **C**.

**Câu 44:** Trong quy tắc Modified EUI-64 chuyển đổi địa chỉ MAC 48-bit thành Interface ID 64-bit, chuỗi 16-bit nào được chèn vào chính giữa và bit nào bị đảo ngược?  
A. Chèn `00:00`, đảo bit thứ 1.  
B. Chèn `FF:FE`, đảo bit thứ 7 (Universal/Local bit) của byte đầu tiên.  
C. Chèn `FF:FF`, đảo bit thứ 8.  
D. Chèn `FE:80`, không đảo bit nào.  
*Đáp án:* **B**.

**Câu 45:** Bản tin nào trong giao thức Neighbor Discovery Protocol (NDP) đóng vai trò thay thế cho ARP Request trong việc phân giải địa chỉ IP sang MAC?  
A. Router Solicitation (RS).  
B. Neighbor Solicitation (NS).  
C. Router Advertisement (RA).  
D. Neighbor Advertisement (NA).  
*Đáp án:* **B**.

**Câu 46:** Khi bản tin Router Advertisement (RA) có các cờ được thiết lập là `M = 0` và `O = 1`, máy trạm sẽ cấu hình địa chỉ IP và DNS theo phương thức nào?  
A. Stateful DHCPv6 cho cả IP và DNS.  
B. SLAAC để tự tạo địa chỉ IP; Stateless DHCPv6 để lấy thông tin DNS.  
C. SLAAC thuần túy không dùng DHCP.  
D. Cấu hình hoàn toàn bằng tay (Static).  
*Đáp án:* **B**.

---

#### Chuyên đề 6: Mạng điều khiển bằng phần mềm - SDN (4 Câu)

**Câu 47:** Bản chất kiến trúc mang tính cách mạng của SDN là gì?  
A. Thay thế toàn bộ cáp đồng bằng cáp quang.  
B. Tách rời hoàn toàn Mặt phẳng Điều khiển (Control Plane) khỏi Mặt phẳng Dữ liệu (Data Plane).  
C. Xóa bỏ hoàn toàn địa chỉ IP.  
D. Chỉ sử dụng mạng không dây Wi-Fi.  
*Đáp án:* **B**.

**Câu 48:** Giao diện lập trình (API) nào trong SDN nằm giữa Bộ điều khiển (SDN Controller) và các Ứng dụng mạng cấp cao (như Firewall, Cân bằng tải)?  
A. Southbound API.  
B. Northbound API.  
C. Eastbound API.  
D. Data Plane API.  
*Đáp án:* **B**.

**Câu 49:** Một mục luật (Flow Entry) trong Flow Table của switch OpenFlow KHÔNG chứa thành phần nào sau đây?  
A. Match Fields (Trường so khớp).  
B. Instructions / Actions (Tập hành động).  
C. Bảng định tuyến BGP toàn cầu của ISP khác.  
D. Priority & Counters.  
*Đáp án:* **C**.

**Câu 50:** Trong chế độ xử lý luồng Reactive Mode của OpenFlow, khi một gói tin đến switch mà không khớp với bất kỳ luật nào trong Flow Table (Table-miss), switch sẽ làm gì?  
A. Tự động tắt cổng mạng.  
B. Đóng gói gói tin vào bản tin `Packet-In` và gửi lên SDN Controller để xin chỉ thị.  
C. Tự động tính toán giải thuật Dijkstra.  
D. Chuyển đổi gói tin sang giao thức RIP.  
*Đáp án:* **B**.

---
