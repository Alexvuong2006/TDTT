# CẨM NANG TOÀN DIỆN: HỆ ĐIỀU HÀNH - CHƯƠNG 3: QUẢN LÝ TIẾN TRÌNH & ĐIỀU PHỐI (PROCESS MANAGEMENT & CPU SCHEDULING)

> **Tài liệu học tập & Ôn thi môn Hệ Điều Hành (Operating Systems)**  
> **Khoa Công nghệ Thông tin - Trường Đại học Khoa học Tự nhiên, ĐHQG-HCM (FIT@HCMUS)**  
> Biên soạn tổng hợp kiến thức từ Slide bài giảng chương 3 và giải chi tiết chuẩn mực bài tập điều phối tiến trình.

---

## MỤC LỤC TỔNG QUAN

1. [PHẦN 1: TỔNG HỢP TOÀN BỘ KIẾN THỨC QUẢN LÝ TIẾN TRÌNH (SLIDE FIT@HCMUS)](#phần-1-tổng-hợp-toàn-bộ-kiến-thức-quản-lý-tiến-trình)
   - [1. Khái niệm cốt lõi về Tiến trình (Process)](#1-khái-niệm-cốt-lõi-về-tiến-trình-process)
   - [2. Hoạt động & Vòng đời của Tiến trình](#2-hoạt-động--vòng-đời-của-tiến-trình)
   - [3. Khối quản lý tiến trình (PCB - Process Control Block)](#3-khối-quản-lý-tiến-trình-pcb---process-control-block)
   - [4. Môi trường đa chương & Khái niệm Điều phối CPU](#4-môi-trường-đa-chương--khái-niệm-điều-phối-cpu)
   - [5. Chuyển đổi ngữ cảnh (Context Switching) & Dispatcher](#5-chuyển-đổi-ngữ-cảnh-context-switching--dispatcher)
   - [6. Các chiến lược điều phối tiến trình kinh điển](#6-các-chiến-lược-điều-phối-tiến-trình-kinh-điển)
     - [6.1. FCFS (First-Come, First-Served)](#61-fcfs-first-come-first-served)
     - [6.2. Round Robin (RR)](#62-round-robin-rr)
     - [6.3. Điều phối theo độ ưu tiên (Priority Scheduling)](#63-điều-phối-theo-độ-ưu-tiên-priority-scheduling)
     - [6.4. Shortest Job First (SJF) & SRTF](#64-shortest-job-first-sjf--srtf)
     - [6.5. Điều phối nhiều hàng đợi (Multilevel Queue & Multilevel Feedback Queue)](#65-điều-phối-nhiều-hàng-đợi-multilevel-queue--multilevel-feedback-queue)
   - [7. Tiểu trình (Thread / Lightweight Process) & Đa tiểu trình](#7-tiểu-trình-thread--lightweight-process--đa-tiểu-trình)
   - [8. Các thuật toán điều phối mở rộng (Tanenbaum)](#8-các-thuật-toán-điều-phối-mở-rộng-tanenbaum)
2. [PHẦN 2: BÀI TẬP VÀ LỜI GIẢI ĐIỀU PHỐI TIẾN TRÌNH](#phần-2-bài-tập-và-lời-giải-điều-phối-tiến-trình)
   - [ĐÁNH GIÁ TÍNH CHÍNH XÁC CỦA BÀI GIẢI CUNG CẤP](#đánh-giá-tính-chính-xác-của-bài-giải-cung-cấp)
   - [BÀI TẬP 1: ĐIỀU PHỐI CPU (SJF KHÔNG ĐỘC QUYỀN) & TÀI NGUYÊN R1 (FIFO)](#bài-tập-1-điều-phối-cpu-sjf-không-độc-quyền--tài-nguyên-r1-fifo)
     - [Phần 1.1: Trình bày lời giải chuẩn](#phần-11-trình-bày-lời-giải-chuẩn-bài-1)
     - [Phần 1.2: Giải thích chi tiết, cụ thể, chính xác lời giải](#phần-12-giải-thích-chi-tiết-cụ-thể-chính-xác-lời-giải-bài-1)
   - [BÀI TẬP 2: ĐIỀU PHỐI SJF KHÔNG ĐỘC QUYỀN (SRTF) VỚI NHIỀU CHU KỲ CPU & I/O](#bài-tập-2-điều-phối-sjf-không-độc-quyền-srtf-với-nhiều-chu-kỳ-cpu--io)
     - [Phần 2.1: Trình bày lời giải chuẩn](#phần-21-trình-bày-lời-giải-chuẩn-bài-2)
     - [Phần 2.2: Giải thích chi tiết, cụ thể, chính xác lời giải](#phần-22-giải-thích-chi-tiết-cụ-thể-chính-xác-lời-giải-bài-2)
   - [TỔNG KẾT SO SÁNH VÀ BÀI HỌC KINH NGHIỆM LÀM BÀI THI](#tổng-kết-so-sánh-và-bài-học-kinh-nghiệm-làm-bài-thi)

---

# PHẦN 1: TỔNG HỢP TOÀN BỘ KIẾN THỨC QUẢN LÝ TIẾN TRÌNH

## 1. Khái niệm cốt lõi về Tiến trình (Process)

### 1.1. Định nghĩa
- **Tiến trình (Process)**: Là một **chương trình đang được thực thi** (*a program in execution*).
- **Phân biệt Chương trình (Program) và Tiến trình (Process)**:
  - *Chương trình*: Là một thực thể **tĩnh** (*passive entity*), tập hợp các câu lệnh lưu trữ trên đĩa (tập tin thực thi như `.exe`, tệp mã nhị phân ELF).
  - *Tiến trình*: Là một thực thể **động** (*active entity*), bao gồm mã lệnh chương trình kèm theo toàn bộ trạng thái thực thi hiện hành: con trỏ lệnh (Program Counter - PC), nội dung các thanh ghi CPU, vùng ngăn xếp (Stack), vùng đống (Heap), và các tài nguyên hệ thống được cấp phát (bộ nhớ, tập tin, thiết bị I/O).

### 1.2. Các tài nguyên của một tiến trình
Một tiến trình cần phối hợp sử dụng các tài nguyên hệ thống để hoàn thành tác vụ:
1. **CPU (Bộ xử lý trung tâm)**: Dùng để thực thi các chỉ thị máy.
2. **Bộ nhớ chính (RAM)**: Chứa không gian địa chỉ của tiến trình, chia thành các phân đoạn:
   - *Text segment (Code)*: Chứa mã máy thực thi.
   - *Data segment*: Chứa các biến toàn cục (global) và biến tĩnh (static).
   - *Heap*: Vùng nhớ cấp phát động trong thời gian chạy (qua `malloc()`, `calloc()`, `new`).
   - *Stack*: Vùng nhớ ngăn xếp chứa biến cục bộ, tham số hàm, địa chỉ trả về của lời gọi hàm.
3. **Tài nguyên I/O & Tập tin**: Bảng mô tả tập tin (*File Descriptors*), kết nối mạng (*Sockets*), máy in, đĩa cứng.

### 1.3. Phân loại tiến trình theo đặc tính hoạt động
- **Tiến trình hướng tính toán (CPU-bound process)**:
  - Dành phần lớn thời gian để tính toán bằng CPU.
  - Các đợt sử dụng CPU (*CPU bursts*) rất dài, ít khi thực hiện thao tác nhập xuất I/O.
  - Ví dụ: Mã hóa video, tính toán khoa học, mô phỏng số, render đồ họa 3D.
- **Tiến trình hướng nhập xuất (I/O-bound process)**:
  - Dành phần lớn thời gian để chờ và thực hiện các thao tác I/O.
  - Các đợt sử dụng CPU (*CPU bursts*) rất ngắn, thường xuyên chuyển sang trạng thái chờ I/O.
  - Ví dụ: Trình soạn thảo văn bản, hệ quản trị cơ sở dữ liệu, trình duyệt web, máy chủ socket tương tác.

---

## 2. Hoạt động & Vòng đời của Tiến trình

### 2.1. Thao tác tạo lập tiến trình (Process Creation)
Hệ điều hành tạo tiến trình trong các tình huống:
1. **Khởi động hệ thống (System Booting)**: HĐH khởi tạo các tiến trình hệ thống nền (*daemons/services*), tiến trình `init` (Linux PID 1) hoặc `smss.exe`/`csrss.exe` (Windows).
2. **Người dùng kích hoạt chương trình**: Bấm đúp vào biểu tượng ứng dụng, hoặc nhập lệnh trong terminal (Shell/CLI).
3. **Một tiến trình đang chạy tạo tiến trình con**:
   - **Hệ điều hành Unix/Linux**:
     - Lời gọi hệ thống `fork()`: Tạo một tiến trình con là bản sao chính xác (*clone*) của tiến trình cha.
     - Lời gọi hệ thống `exec()` (họ `execl`, `execvp`): Nạp và thay thế không gian địa chỉ của tiến trình con bằng mã máy của một chương trình mới.
     - Cây tiến trình Unix: Các tiến trình có quan hệ cha - con khăng khít. Nếu cha kết thúc trước khi con kết thúc, con trở thành *Orphan process* (được `init`/`systemd` nhận nuôi). Nếu con kết thúc nhưng cha chưa đọc mã trả về (`wait()`), con trở thành *Zombie process*.
   - **Hệ điều hành Windows**:
     - Lời gọi API `CreateProcess()`: Tạo tiến trình mới và nạp luôn chương trình chỉ định trong cùng một bước.
     - Quan hệ cha - con trong Windows lỏng lẻo hơn: sau khi tạo xong, tiến trình cha và con độc lập về mặt vận hành.

### 2.2. Thao tác kết thúc tiến trình (Process Termination)
Tiến trình kết thúc qua các cơ chế:
1. **Tự nguyện kết thúc bình thường**: Xử lý xong câu lệnh cuối cùng của hàm `main()` hoặc gọi hàm thoát:
   - Unix/Linux: `exit(status)`
   - Windows: `ExitProcess(status)`
2. **Bị tiến trình khác yêu cầu kết thúc cưỡng bức**:
   - Unix/Linux: Gửi tín hiệu thông qua `kill(pid, SIGKILL)` hoặc `SIGTERM`.
   - Windows: `TerminateProcess(hProcess, exitCode)`.
   *(Tiến trình "nạn nhân" không thể từ chối nếu nhận tín hiệu dừng tuyệt đối như SIGKILL).*
3. **Kết thúc do lỗi nghiêm trọng (Fatal Errors)**:
   - Lỗi chia cho 0 (*Division by zero*).
   - Truy cập trái phép vùng nhớ (*Segmentation Fault*, *Access Violation*).
   - Tràn bộ nhớ đệm (*Stack Overflow*), thiếu bộ nhớ vật lý (*Out-of-memory - OOM Killer*).

### 2.3. Mô hình Trạng thái Tiến trình (Process States)

Mô hình kinh điển gồm 3 trạng thái cơ bản:
1. **Ready (Sẵn sàng)**: Tiến trình đã nạp vào bộ nhớ, đã có đầy đủ tài nguyên cần thiết, chỉ đang nằm trong hàng đợi sẵn sàng (*Ready Queue / Ready List - RL*) để chờ bộ điều phối cấp CPU.
2. **Running (Đang chạy)**: Các chỉ thị của tiến trình đang được CPU trực tiếp thực thi (tại một thời điểm trên một lõi CPU đơn, chỉ có tối đa 1 tiến trình ở trạng thái Running).
3. **Blocked / Waiting (Bị chặn / Chờ)**: Tiến trình tạm ngừng thực thi vì đang chờ một sự kiện bên ngoài xảy ra (chờ thao tác I/O đọc/ghi đĩa hoàn thành, chờ dữ liệu mạng, chờ mở khóa tài nguyên, chờ tín hiệu từ tiến trình khác).

```
                      +-------------------+
                      |       NEW         |
                      +-------------------+
                                | (Admitted)
                                v
               [Trả CPU - Hết Quantum / Bị Preempt]
             +--------------------------------------+
             |                                      |
             v                                      |
      +------------+       (Dispatch)        +-------------+
  --->|   READY    | ----------------------> |   RUNNING   |
      +------------+                         +-------------+
             ^                                      |
             |                                      | (Yêu cầu I/O hoặc Event)
   (I/O xong |                                      v
    Nhận Rs) |                               +-------------+
             +------------------------------ |   BLOCKED   |
                                             +-------------+
                                                    |
                                                    v (Exit)
                                             +-------------+
                                             | TERMINATED  |
                                             +-------------+
```

**Bảng tóm tắt các chuyển dịch trạng thái**:
| Chuyển dịch | Nguyên nhân | Trạng thái CPU & Tài nguyên |
| :--- | :--- | :--- |
| **Ready $\to$ Running** | Được Dispatcher cấp quyền sử dụng CPU | Có CPU, Có tài nguyên |
| **Running $\to$ Ready** | Hết định mức thời gian (Quantum) hoặc bị tiến trình có độ ưu tiên cao hơn trưng dụng (Preempt) | Mất CPU, Có tài nguyên |
| **Running $\to$ Blocked** | Tiến trình phát sinh yêu cầu I/O hoặc chờ biến cố hệ thống | Mất CPU, Thiếu tài nguyên I/O |
| **Blocked $\to$ Ready** | Sự kiện I/O hoàn tất hoặc tài nguyên mong muốn đã được giải phóng | Không có CPU, Đã đủ tài nguyên |

---

## 3. Khối quản lý tiến trình (PCB – Process Control Block)

Để quản lý mỗi tiến trình trong hệ thống, Hệ điều hành duy trì một cấu trúc dữ liệu trung tâm gọi là **PCB (Process Control Block)** (trong Linux kernel chính là cấu trúc `struct task_struct`).

Mỗi tiến trình sở hữu một PCB duy nhất chứa các thông tin:
1. **Định danh tiến trình (Process ID - PID)**: Số nguyên duy nhất gán cho tiến trình.
2. **Trạng thái tiến trình (State)**: Ready, Running, Blocked, Terminated,...
3. **Ngữ cảnh CPU (CPU Context)**:
   - *Program Counter (PC)*: Địa chỉ của chỉ thị lệnh kế tiếp cần thực hiện.
   - *Các thanh ghi CPU (CPU Registers)*: Thanh ghi tích lũy (Accumulator), thanh ghi dữ liệu, thanh ghi chỉ mục, thanh ghi cờ trạng thái.
   - *Stack Pointer (SP)*: Con trỏ trỏ đến đỉnh ngăn xếp hiện hành.
4. **Thông tin định vị bộ xử lý**: Chỉ thị CPU lõi nào được phép chạy tiến trình (Processor affinity trong hệ thống đa vi xử lý).
5. **Thông tin quản lý bộ nhớ**: Con trỏ bảng trang (*Page Table Base Register - PTBR*), thanh ghi nền và thanh ghi giới hạn (*Base & Limit registers*), kích thước các phân đoạn Text, Data, Stack.
6. **Thông tin tài nguyên sử dụng**: Bảng mô tả tập tin đang mở (*Open File Table*), danh sách các thiết bị ngoại vi đang chiếm giữ.
7. **Thông tin phả hệ & giao tiếp**: Định danh tiến trình cha (Parent PID - PPID), danh sách các tiến trình con.
8. **Thông tin điều phối (Scheduling Information)**:
   - Mức độ ưu tiên (*Priority*).
   - Lịch sử sử dụng CPU, thời gian thực thi đã tích lũy, thời gian chờ trong Ready List.

---

## 4. Môi trường đa chương & Khái niệm Điều phối CPU

### 4.1. Môi trường đa chương (Multiprogramming)
- **Vấn đề của đơn chương**: Khi tiến trình thực hiện I/O (vốn có tốc độ cơ học/truy xuất chậm hơn CPU hàng ngàn đến hàng triệu lần), CPU sẽ hoàn toàn rảnh rỗi (*CPU Idle*), gây lãng phí năng lực tính toán cực lớn.
- **Giải pháp đa chương**: Nạp đồng thời nhiều tiến trình vào bộ nhớ chính. Khi tiến trình đang chạy chuyển sang trạng thái Blocked để làm I/O, Hệ điều hành chuyển giao CPU ngay lập tức cho một tiến trình khác đang ở trạng thái Ready.

### 4.2. Mục tiêu của bộ điều phối (Scheduling Objectives)
Mỗi hệ thống hướng đến các mục tiêu điều phối chuyên biệt:
- **Mục tiêu chung**:
  - *Công bằng (Fairness)*: Mọi tiến trình đều có cơ hội nhận CPU hợp lý.
  - *Cân bằng (Balance)*: Khai thác đồng đều các thành phần của hệ thống (CPU, RAM, Kênh I/O).
  - *Tuân thủ chính sách (Policy Enforcement)*: Đảm bảo đúng quyền ưu tiên đã quy định.
- **Hệ thống theo lô (Batch Systems)**:
  - *Tối đa hóa Thông lượng (Maximize Throughput)*: Tối đa số lượng công việc hoàn tất trong một đơn vị thời gian.
  - *Giảm thiểu Thời gian lưu lại (Minimize Turnaround Time)*: $TAT = T_{finish} - T_{arrive}$.
  - *Tận dụng tối đa CPU (CPU Utilization)*: Tỷ lệ phần trăm thời gian CPU bận rộn đạt 100%.
- **Hệ thống tương tác (Interactive Systems - Desktop, Mobile)**:
  - *Giảm thiểu Thời gian chờ (Minimize Waiting Time)*: Giảm thời gian tiến trình nằm trong hàng đợi Ready Queue.
  - *Tối ưu Thời gian hồi đáp (Minimize Response Time)*: Giảm độ trễ từ lúc người dùng thao tác đến khi hệ thống bắt đầu phản hồi.
- **Hệ thống thời gian thực (Real-time Systems)**:
  - *Tuân thủ thời hạn chót (Meet Deadlines)*: Bắt buộc hoàn thành trước mốc thời gian chết, tránh gây lỗi hệ thống vật lý hoặc thảm họa.
  - *Tính khả đoán (Predictability)*: Thời gian thực thi ổn định, không dao động thất thường.

### 4.3. Phân loại chiến lược điều phối
1. **Điều phối Độc quyền (Non-preemptive Scheduling)**:
   - Một khi tiến trình đã được cấp CPU (chuyển sang Running), nó sẽ **độc quyền** nắm giữ CPU cho đến khi:
     - Tự kết thúc toàn bộ công việc, hoặc
     - Chủ động yêu cầu I/O (chuyển sang Blocked) hoặc gọi lệnh trả CPU.
   - Các tiến trình khác trong Ready Queue dù có độ ưu tiên cao đến đâu cũng không thể ngắt ngang tiến trình đang chạy.
2. **Điều phối Không độc quyền / Trưng dụng (Preemptive Scheduling)**:
   - Hệ điều hành có quyền **thu hồi CPU** từ tiến trình đang chạy ngay khi nó đang tính toán bình thường để cấp cho tiến trình khác.
   - Điểm kích hoạt trưng dụng xảy ra khi:
     - Hết định mức thời gian chạy (Time slice / Quantum expired).
     - Có tiến trình mới xuất hiện ở Ready Queue (hoặc hoàn thành I/O quay lại Ready Queue) sở hữu độ ưu tiên cao hơn hoặc thời gian thực thi còn lại ngắn hơn.

---

## 5. Chuyển đổi ngữ cảnh (Context Switching) & Dispatcher

### 5.1. Nhiệm vụ của Dispatcher (Bộ phân phối)
Bộ Dispatcher là thành phần trao quyền điều khiển CPU cho tiến trình được Scheduler lựa chọn. Công việc gồm 3 bước:
1. **Lưu ngữ cảnh (Context Save)**: Lưu trạng thái thanh ghi, PC, SP của tiến trình hiện tại vào PCB của nó.
2. **Nạp ngữ cảnh (Context Restore)**: Tải trạng thái thanh ghi, PC, SP từ PCB của tiến trình mới được chọn vào các thanh ghi vật lý của CPU.
3. **Chuyển chế độ (Switch Mode)**: Chuyển CPU từ Kernel mode sang User mode và nhảy tới địa chỉ lệnh được chỉ bởi PC mới để tiến trình thực thi.

> **Độ trễ phân phối (Dispatch Latency / Context Switch Overhead)**: Thời gian hệ điều hành dừng một tiến trình và khởi động tiến trình khác. Đây là **thời gian tiêu tốn vô ích** (*pure overhead*) vì CPU không thực hiện được bất kỳ câu lệnh hữu ích nào của người dùng.

### 5.2. Cơ chế thu hồi CPU của Hệ điều hành (Timer Interrupt)
- **Nghịch lý**: Bản thân HĐH cũng là phần mềm, chỉ chạy khi có CPU. Nếu tiến trình người dùng đang chiếm CPU chạy vòng lặp vô tận, làm sao HĐH lấy lại quyền điều khiển?
- **Giải pháp phần cứng**: Sử dụng **Ngắt đồng hồ phần cứng (Hardware Timer Interrupt)**.
  - Bộ đếm thời gian được nạp giá trị ban đầu. Cứ sau mỗi chu kỳ xung nhịp, giá trị đếm giảm đi.
  - Khi bộ đếm về 0, phần cứng phát tín hiệu ngắt (Interrupt).
  - CPU ngay lập tức tạm dừng luồng lệnh của tiến trình người dùng, lưu thanh ghi và tự động nhảy vào trình xử lý ngắt của Hệ điều hành (*Interrupt Service Routine - ISR*).
  - Tại đây, HĐH kiểm tra thời gian sử dụng CPU và thực hiện thuật toán điều phối để quyết định có thu hồi CPU hay không.

---

## 6. Các chiến lược điều phối tiến trình kinh điển

### 6.1. FCFS (First-Come, First-Served)
- **Nguyên lý**: Tiến trình nào vào hàng đợi Ready trước thì được phục vụ cấp CPU trước.
- **Tính chất**: Hoàn toàn **độc quyền (Non-preemptive)**.
- **Ưu điểm**: Thuật toán đơn giản nhất, trực quan, dễ cài đặt bằng cấu trúc hàng đợi FIFO tiêu chuẩn.
- **Nhược điểm nghiêm trọng**:
  - **Hiệu ứng đoàn tàu (Convoy Effect)**: Nếu một tiến trình dài (CPU-bound) vào trước, tất cả các tiến trình ngắn (I/O-bound) vào sau phải xếp hàng chờ đợi rất lâu.
  - Dẫn đến thời gian chờ trung bình ($AWT$) rất lớn, hiệu suất sử dụng thiết bị I/O bị kéo giảm nghiêm trọng.

### 6.2. Round Robin (RR)
- **Nguyên lý**: Được thiết kế đặc biệt cho hệ thống chia sẻ thời gian (Time-sharing).
  - Hàng đợi Ready Queue được tổ chức theo vòng tròn FIFO.
  - Mỗi tiến trình được cấp một định mức thời gian sử dụng CPU liên tục gọi là **Time Quantum** (hoặc Time Slice, ký hiệu $q$, thường từ 10 - 100 ms).
  - Nếu tiến trình thực thi xong trước khi hết $q$, nó tự giải phóng CPU.
  - Nếu hết $q$ mà tiến trình chưa hoàn thành, ngắt đồng hồ phát sinh: tiến trình bị đưa về cuối Ready Queue, CPU được giao cho tiến trình kế tiếp.
- **Tính chất**: Hoàn toàn **không độc quyền (Preemptive)** theo thời gian.
- **Đánh giá ảnh hưởng của tham số $q$**:
  - Nếu $q \to \infty$: Thuật toán suy biến thành **FCFS**. Tính tương tác bị triệt tiêu.
  - Nếu $q$ quá nhỏ (tiến tới thời gian chuyển ngữ cảnh): Số lần chuyển đổi ngữ cảnh bùng nổ, CPU mất phần lớn thời gian chỉ để lưu và nạp ngữ cảnh (*thrashing overhead*).
  - *Quy tắc kinh nghiệm*: Chọn $q$ sao cho khoảng 80% các đợt bùng nổ CPU (CPU bursts) ngắn hơn $q$.

### 6.3. Điều phối theo độ ưu tiên (Priority Scheduling)
- **Nguyên lý**: Mỗi tiến trình được gán một giá trị độ ưu tiên (thường là một số nguyên). CPU được cấp phát cho tiến trình có độ ưu tiên cao nhất.
  *(Quy ước phổ biến: Số nguyên càng nhỏ thì độ ưu tiên càng cao, ví dụ 0 là ưu tiên cao nhất).*
- **Phân loại**:
  - *Độc quyền*: Tiến trình có độ ưu tiên cao hơn vào Ready Queue phải chờ tiến trình hiện tại nhả CPU.
  - *Không độc quyền (Preemptive)*: Nếu tiến trình mới có độ ưu tiên cao hơn tiến trình đang chạy, CPU sẽ bị thu hồi ngay lập tức để giao cho tiến trình mới.
- **Phân loại cách gán**:
  - *Ưu tiên tĩnh (Static Priority)*: Không thay đổi trong suốt vòng đời tiến trình.
  - *Ưu tiên động (Dynamic Priority)*: Hệ điều hành điều chỉnh linh hoạt dựa trên hành vi (I/O-bound được tăng ưu tiên, CPU-bound dùng quá nhiều CPU bị giảm ưu tiên).
- **Vấn đề then chốt - Hiện tượng Đói tài nguyên (Starvation / Indefinite Blocking)**:
  - Một tiến trình có độ ưu tiên thấp có thể không bao giờ được cấp CPU nếu liên tục có các tiến trình độ ưu tiên cao xuất hiện trong hệ thống.
- **Giải pháp - Kỹ thuật Lão hóa (Aging)**:
  - Tăng dần độ ưu tiên của các tiến trình theo thời gian mà chúng phải nằm chờ trong Ready Queue. Sau một khoảng thời gian đủ lâu, tiến trình ưu tiên thấp nhất cũng sẽ đạt mức ưu tiên cao nhất để được chạy.

### 6.4. Shortest Job First (SJF) & SRTF
- **Nguyên lý**: Giao CPU cho tiến trình có thời gian thực thi CPU burst tiếp theo ngắn nhất. Khi có hai tiến trình có cùng thời gian burst, áp dụng FCFS để giải quyết tranh chấp.
- **Phân loại**:
  1. **SJF Độc quyền (Non-preemptive SJF)**: Khi CPU đã được cấp cho một tiến trình, nó chạy hết chu kỳ burst đó mà không bị ngắt quãng.
  2. **SJF Không độc quyền (Preemptive SJF / SRTF - Shortest Remaining Time First)**:
     - Khi một tiến trình mới xuất hiện hoặc hoàn thành I/O vào Ready Queue, hệ thống so sánh **thời gian thực thi CPU còn lại (remaining burst)** của tiến trình đang chạy với thời gian burst của tiến trình mới.
     - Nếu tiến trình mới có thời gian cần ngắn hơn thời gian còn lại của tiến trình đang chạy $\implies$ **Trưng dụng CPU ngay lập tức!**
- **Đặc tính Tối ưu**:
  - Thuật toán SJF/SRTF đã được chứng minh bằng toán học là cho **thời gian chờ trung bình (Average Waiting Time - AWT) nhỏ nhất** trong tất cả các thuật toán điều phối.
- **Khó khăn thực tế**:
  - Làm sao hệ điều hành biết trước được thời lượng bùng nổ CPU tiếp theo của một tiến trình?
- **Giải pháp dự đoán bằng quy luật trung bình giảm theo hàm mũ (Exponential Smoothing)**:
  $$\tau_{n+1} = \alpha \cdot t_n + (1 - \alpha) \cdot \tau_n$$
  Trong đó:
  - $t_n$: Thời gian sử dụng CPU thực tế ở lần chạy thứ $n$.
  - $\tau_n$: Giá trị ước lượng dự đoán cho lần chạy thứ $n$.
  - $\tau_{n+1}$: Giá trị ước lượng cho lần chạy thứ $n+1$ kế tiếp.
  - $\alpha$: Hệ số trọng số ($0 \le \alpha \le 1$).
    - Nếu $\alpha = 0$: $\tau_{n+1} = \tau_n$ (Bỏ qua lịch sử thực tế gần nhất, chỉ giữ ước lượng cũ).
    - Nếu $\alpha = 1$: $\tau_{n+1} = t_n$ (Chỉ tin vào lần chạy thực tế gần nhất, quên đi quá khứ xa hơn).
    - Khi khai triển đa thức, trọng số các lần chạy trong quá khứ giảm dần theo cấp số nhân: $\alpha(1-\alpha)^k$.

### 6.5. Điều phối nhiều hàng đợi (Multilevel Queue & Multilevel Feedback Queue)

#### A. Điều phối nhiều hàng đợi cố định (Multilevel Queue - MLQ)
- Phân chia Ready Queue thành nhiều hàng đợi riêng biệt dựa trên bản chất công việc, ví dụ:
  - *Hàng đợi 1 (Ưu tiên cao nhất)*: Các tiến trình hệ thống (System processes).
  - *Hàng đợi 2*: Các tiến trình tương tác người dùng (Interactive processes - dùng RR với $q$ nhỏ).
  - *Hàng đợi 3 (Ưu tiên thấp nhất)*: Các tiến trình xử lý theo lô (Batch processes - dùng FCFS).
- Mỗi hàng đợi có chiến lược điều phối riêng.
- Lập lịch giữa các hàng đợi: Thường theo thứ tự ưu tiên tuyệt đối có trưng dụng (Queue 1 luôn chạy trước Queue 2), hoặc chia lát thời gian (Time slice: ví dụ 80% CPU cho Queue tương tác, 20% cho Queue theo lô).

#### B. Điều phối hàng đợi đa cấp có phản hồi (Multilevel Feedback Queue - MLFQ)
- Khắc phục nhược điểm của MLQ: Cho phép tiến trình **di chuyển linh hoạt giữa các hàng đợi**.
- **Cơ chế hoạt động**:
  - Tiến trình mới vào luôn được đặt vào hàng đợi ưu tiên cao nhất ($Q_0$) với time quantum nhỏ (ví dụ 8 ms).
  - Nếu tiến trình chạy hết 8 ms mà chưa xong (tiến trình CPU-bound) $\implies$ Bị giáng cấp xuống hàng đợi $Q_1$ (time quantum 16 ms).
  - Nếu tại $Q_1$ vẫn chưa hoàn thành $\implies$ Bị giáng xuống $Q_2$ (chạy FCFS).
  - Các tiến trình I/O-bound thường nhả CPU trước khi hết quantum nên luôn được giữ ở hàng đợi ưu tiên cao, đảm bảo thời gian tương tác người dùng cực nhanh.
  - Kết hợp kỹ thuật **Aging**: Nếu tiến trình nằm ở hàng đợi thấp quá lâu mà không được chạy, nó sẽ được thăng cấp dần lên các hàng đợi cao hơn để tránh hiện tượng Starvation.

---

## 7. Tiểu trình (Thread / Lightweight Process) & Đa tiểu trình

### 7.1. Tại sao cần Tiểu trình?
- Trong các ứng dụng hiện đại, nhiều thao tác cần chạy đồng thời (vừa nhận nhập liệu người dùng, vừa tính toán ngầm, vừa tải dữ liệu mạng).
- Nếu sử dụng nhiều tiến trình độc lập:
  - Mỗi tiến trình có không gian địa chỉ riêng biệt hoàn toàn.
  - Việc liên lạc giữa các tiến trình (IPC - Inter-Process Communication như Pipes, Shared Memory, Message Queues) rất phức tạp và chi phí chuyển đổi ngữ cảnh tiến trình rất tốn kém (*heavyweight*).
- **Giải pháp**: Sử dụng **Tiểu trình (Thread)** - luồng thực thi nhẹ bên trong cùng một tiến trình (*lightweight process*).

### 7.2. Cấu trúc tài nguyên: Thành phần Riêng vs Thành phần Chung
- **Mỗi tiến trình** luôn có ít nhất một tiểu trình chính (thực thi hàm `main()`), và có thể sinh ra nhiều tiểu trình con.
- **Thành phần riêng của mỗi tiểu trình (lưu trong TCB - Thread Control Block)**:
  - Thread ID định danh riêng.
  - Tập thanh ghi CPU (Register set, Program Counter - PC lưu vị trí lệnh đang chạy).
  - Ngăn xếp riêng (**Private Stack** & Stack Pointer - SP) để lưu trữ các biến cục bộ và khung hàm của riêng luồng đó.
  - Mức độ ưu tiên và trạng thái luồng (Ready, Running, Blocked).
- **Thành phần chia sẻ chung giữa các tiểu trình trong cùng tiến trình**:
  - Toàn bộ vùng mã lệnh (**Code/Text segment**).
  - Vùng dữ liệu toàn cục (**Data segment**).
  - Vùng nhớ cấp phát động (**Heap segment**).
  - Các tài nguyên hệ thống: Bảng mô tả tập tin (*Open files*), socket mạng, tín hiệu (*signals*).

### 7.3. So sánh Tiến trình và Tiểu trình
| Tiêu chí so sánh | Tiến trình (Process) | Tiểu trình (Thread) |
| :--- | :--- | :--- |
| **Không gian địa chỉ** | Độc lập, được bảo vệ nghiêm ngặt | Chia sẻ chung không gian địa chỉ của tiến trình mẹ |
| **Chi phí tạo lập / hủy** | Cao (cần cấp phát toàn bộ PCB, bảng trang bộ nhớ, không gian địa chỉ mới) | Rất thấp (chỉ cấp phát TCB và vùng nhớ Stack nhỏ) |
| **Chuyển đổi ngữ cảnh** | Chậm, tốn kém tài nguyên (phải hoán đổi con trỏ bảng trang bộ nhớ, xóa TLB cache) | Nhanh, nhẹ nhàng (chỉ cần hoán đổi thanh ghi và SP, giữ nguyên bảng trang) |
| **Giao tiếp dữ liệu** | Phức tạp, phải dùng IPC qua lời gọi hệ thống Kernel | Rất đơn giản và trực tiếp thông qua việc đọc/ghi biến toàn cục trong RAM |
| **Tính an toàn / Độc lập** | Rất cao; 1 tiến trình crash không ảnh hưởng tiến trình khác | Thấp hơn; 1 thread lỗi bộ nhớ có thể làm sập toàn bộ tiến trình |

### 7.4. Các mô hình tổ chức tiểu trình
1. **Tiểu trình mức người dùng (User-Level Threads - ULT)**:
   - Được quản lý hoàn toàn bởi thư viện thread ở không gian người dùng (như POSIX Pthreads, Green Threads).
   - Kernel không hề biết về sự tồn tại của các tiểu trình này (đối với Kernel chỉ có 1 tiến trình).
   - *Ưu điểm*: Chuyển ngữ cảnh cực nhanh vì không cần gọi System Call vào Kernel mode.
   - *Nhược điểm*: Nếu một tiểu trình thực hiện một lời gọi hệ thống gây tắc nghẽn (blocking I/O), toàn bộ tiến trình (và tất cả tiểu trình con khác) sẽ bị Kernel dừng lại.
2. **Tiểu trình mức nhân (Kernel-Level Threads - KLT)**:
   - Kernel trực tiếp quản lý và điều phối các tiểu trình (Windows Threads, Linux Clone/NPTL).
   - *Ưu điểm*: Nếu một tiểu trình bị block, Kernel vẫn tiếp tục phân phối CPU cho các tiểu trình khác trong cùng tiến trình; hỗ trợ chạy song song thực sự trên máy tính đa lõi (Multiprocessor/Multicore).
   - *Nhược điểm*: Mỗi thao tác tạo lập, đồng bộ hay chuyển ngữ cảnh đều phải qua Kernel mode nên chi phí lớn hơn ULT.
3. **Mô hình kết hợp (Hybrid Model - M:N)**:
   - Kết hợp cả hai: Ánh xạ $M$ tiểu trình người dùng lên $N$ tiểu trình nhân ($M \ge N$), vừa đảm bảo tốc độ của thư viện vừa tận dụng được khả năng đa lõi của hệ điều hành.

---

## 8. Các thuật toán điều phối mở rộng (Tanenbaum)

Trong tài liệu tham khảo giáo trình chuẩn (*Modern Operating Systems* - Andrew S. Tanenbaum):
1. **Guaranteed Scheduling (Điều phối đảm bảo)**:
   - Cam kết phân chia tài nguyên công bằng tuyệt đối. Nếu có $n$ tiến trình đang hoạt động, hệ điều hành cam kết mỗi tiến trình sẽ nhận được đúng tỉ lệ $1/n$ năng lực tính toán của CPU. Hệ thống tính tỉ số giữa thời gian CPU thực tế nhận được và thời gian CPU lý thuyết được hưởng, tiến trình có tỉ số thấp nhất sẽ được ưu tiên chạy.
2. **Lottery Scheduling (Điều phối xổ số)**:
   - Mỗi tiến trình được cấp một số lượng "vé số" nhất định tùy theo độ quan trọng. Khi cần điều phối CPU, hệ điều hành bốc một số ngẫu nhiên. Tiến trình nắm giữ vé trúng thưởng sẽ được chạy. Giải thuật này mang tính xác suất, loại bỏ hoàn toàn nguy cơ đói tài nguyên một cách mềm dẻo.
3. **Fair-Share Scheduling (Điều phối chia sẻ công bằng)**:
   - Xem xét cả yếu tố người dùng (User) sở hữu tiến trình. Ví dụ, nếu User A chạy 1 tiến trình và User B chạy 9 tiến trình, giải thuật không chia đều CPU cho 10 tiến trình (khiến B chiếm 90%), mà chia 50% CPU cho User A và 50% CPU cho User B.

---

# PHẦN 2: BÀI TẬP VÀ LỜI GIẢI ĐIỀU PHỐI TIẾN TRÌNH

## ĐÁNH GIÁ TÍNH CHÍNH XÁC CỦA BÀI GIẢI CUNG CẤP

> ### KẾT QUẢ KIỂM ĐỊNH LỜI GIẢI: **CHÍNH XÁC 100%**
> Sau khi phân tích toán học và đối chiếu từng mốc thời gian của bài tập với file bài giải `Loi_Giai_Dieu_Phoi_Tien_Trinh_SJF_Gantt.pdf`, kết luận như sau:
> 1. **Bài tập 1**: 
>    - Mọi quyết định trưng dụng CPU theo thuật toán SJF không độc quyền (SRTF) tại các mốc thời gian $t = 2, 11, 14$ đều hoàn toàn chính xác.
>    - Việc quản lý tranh chấp tài nguyên I/O đơn thể hiện ($R1$ và $R2$) theo quy tắc FIFO được xử lý rất chặt chẽ: phát hiện chính xác điểm nghẽn tại $t = 13$ (P2 phải chờ R1 do P1 đang chiếm) và tại $t = 29$ (P3 phải chờ R2 do P4 đang chiếm).
>    - Sơ đồ Gantt và bảng thời gian chờ được phân định rõ ràng giữa hai quan điểm học thuật: thời gian chờ trên Ready List ($AWT = 2.5$) và tổng thời gian chờ cả hệ thống gồm thời gian chờ tài nguyên I/O ($AWT = 4.75$).
> 2. **Bài tập 2**:
>    - Quá trình điều phối đa chu kỳ CPU - I/O - CPU xen kẽ qua 18 mốc thời gian đều chuẩn xác từng đơn vị.
>    - Thời gian lưu lại trung bình ($ATAT = 17.75$) và thời gian chờ trung bình ($AWT = 5.75$) được tính toán bằng 2 phương pháp độc lập (phương pháp trừ bù tổng thể và phương pháp thống kê từng khoảng chờ Ready List) cho kết quả trùng khớp tuyệt đối.

Dưới đây là phần trình bày lại bài giải được chia làm 2 phần rõ rệt: **Lời giải chuẩn** (trình bày mẫu mực cho bài thi) và **Giải thích chi tiết, cụ thể, chính xác lời giải** (giải mã từng bước suy luận khoa học).

---

## BÀI TẬP 1: ĐIỀU PHỐI CPU (SJF KHÔNG ĐỘC QUYỀN) & TÀI NGUYÊN R1 (FIFO)

### Đề bài:
Xét tập các tiến trình sau:
| Tiến trình | Thời điểm vào Ready list | Thời gian CPU lần 1 | IO lần 1 (Thời gian, Thiết bị) | Thời gian CPU lần 2 | IO lần 2 (Thời gian, Thiết bị) |
| :---: | :---: | :---: | :---: | :---: | :---: |
| **P1** | 0 | 8 | 5 (R1) | 1 | 0 (Null) |
| **P2** | 2 | 1 | 8 (R2) | 2 | 5 (R1) |
| **P3** | 10 | 6 | 5 (R1) | 2 | 3 (R2) |
| **P4** | 11 | 3 | 20 (R2) | 0 | 0 (Null) |

*Yêu cầu*:
- Mỗi loại thiết bị I/O chỉ có 1 thể hiện duy nhất, mỗi chu kỳ I/O yêu cầu 1 thể hiện duy nhất của thiết bị đó.
- Vẽ sơ đồ điều phối CPU (chiến lược SJF không độc quyền / SRTF) và tài nguyên R1 (chiến lược FIFO).
- Tính thời gian chờ ($WT$) của mỗi tiến trình.

---

### PHẦN 1.1: TRÌNH BÀY LỜI GIẢI CHUẨN (BÀI 1)

#### 1. Sơ đồ Gantt Điều phối CPU và Tài nguyên R1:

**Sơ đồ Gantt CPU (SJF Không độc quyền - Preemptive SJF / SRTF):**
```
+----+----+----------+----+----+----+----+----+----+----------+----+----------+
| P1 | P2 |    P1    |IDLE| P3 | P2 | P4 | P1 | P4 |    P3    |IDLE| P3 |   IDLE   |
+----+----+----------+----+----+----+----+----+----+----------+----+----------+
0    2    3          9   10   11   13   14   15   17         22   27   29         40
```

**Sơ đồ Gantt Tài nguyên R1 (Chiến lược FIFO):**
```
+--------------------+--------------+--------------+----------+--------------+----------+
|     Rảnh (Idle)    | P1 dùng (5)  | P2 dùng (5)  |   Rảnh   | P3 dùng (5)  |   Rảnh   |
+--------------------+--------------+--------------+----------+--------------+----------+
0                    9             14             19         22             27         40
```

*(Sơ đồ Gantt Tài nguyên R2 - Minh họa bổ trợ đối chiếu tranh chấp thiết bị):*
```
+---------+--------------+----------+----------------------------------------+--------------+
|  Rảnh   | P2 dùng (8)  |   Rảnh   |              P4 dùng (20)              | P3 dùng (3)  |
+---------+--------------+----------+----------------------------------------+--------------+
0         3             11         17                                       37             40
```

---

#### 2. Bảng kết quả tính toán Thời gian lưu lại ($TAT$) và Thời gian chờ ($WT$):

*Công thức áp dụng*:
- Thời gian lưu lại hệ thống: $TAT = T_{finish} - T_{arrive}$
- Tổng thời gian phục vụ: $T_{service} = \sum CPU + \sum IO$
- Tổng thời gian chờ toàn hệ thống: $WT_{total} = TAT - T_{service} = WT_{ReadyList} + WT_{IO\_Queue}$

| Tiến trình | $T_{arrive}$ | $T_{finish}$ | $TAT$ | $\sum CPU$ | $\sum IO$ | Thời gian chờ trên Ready List ($WT_{RL}$) | Thời gian chờ thiết bị IO ($WT_{IO}$) | Tổng thời gian chờ ($WT_{total}$) |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **P1** | 0 | 15 | $15 - 0 = \mathbf{15}$ | $8 + 1 = 9$ | 5 | **1** (chờ tại $[2 - 3]$) | 0 | **1** |
| **P2** | 2 | 19 | $19 - 2 = \mathbf{17}$ | $1 + 2 = 3$ | $8 + 5 = 13$ | **0** | **1** (chờ R1 tại $[13 - 14]$) | **1** |
| **P3** | 10 | 40 | $40 - 10 = \mathbf{30}$ | $6 + 2 = 8$ | $5 + 3 = 8$ | **6** (chờ tại $[11 - 17]$) | **8** (chờ R2 tại $[29 - 37]$) | **14** |
| **P4** | 11 | 37 | $37 - 11 = \mathbf{26}$ | 3 | 20 | **3** (chờ $[11-13], [14-15]$) | 0 | **3** |
| **TRUNG BÌNH** | — | — | $\mathbf{88/4 = 22.0}$ | — | — | $\mathbf{10/4 = 2.5}$ | $\mathbf{9/4 = 2.25}$ | $\mathbf{19/4 = 4.75}$ |

**Đáp số**:
- Thời gian chờ theo hàng đợi Ready List ($WT_{RL}$):
  - $WT(P1) = 1$
  - $WT(P2) = 0$
  - $WT(P3) = 6$
  - $WT(P4) = 3$
  - **Thời gian chờ trung bình trên Ready List ($AWT_{RL}$)**: $\mathbf{2.5}$ đơn vị thời gian.
- Tổng thời gian chờ toàn hệ thống (kèm chờ thiết bị I/O - $WT_{total}$):
  - $WT(P1) = 1$
  - $WT(P2) = 1$
  - $WT(P3) = 14$
  - $WT(P4) = 3$
  - **Thời gian chờ trung bình toàn hệ thống ($AWT_{total}$)**: $\mathbf{4.75}$ đơn vị thời gian.
- **Thời gian lưu lại trung bình ($ATAT$)**: $\mathbf{22.0}$ đơn vị thời gian.

---

### PHẦN 1.2: GIẢI THÍCH CHI TIẾT, CỤ THỂ, CHÍNH XÁC LỜI GIẢI (BÀI 1)

#### A. Phân tích diễn biến điều phối theo từng mốc thời gian:

1. **Mốc $t = 0$**:
   - P1 xuất hiện tại Ready List (RL) với $CPU_1 = 8$.
   - CPU rảnh, chưa có tiến trình nào khác $\implies$ **P1 chiếm CPU** bắt đầu chạy.
2. **Mốc $t = 2$**:
   - P2 xuất hiện tại RL với $CPU_1 = 1$.
   - Kiểm tra trạng thái: P1 đã chạy được 2 đơn vị thời gian (từ 0 đến 2), do đó thời gian CPU còn lại của P1 là:
     $$Rem(P1) = 8 - 2 = 6$$
   - So sánh: $Burst(P2) = 1 < Rem(P1) = 6$.
   - **Xảy ra Trưng dụng (Preemption)!** P2 chiếm CPU thực thi trong khoảng $[2 - 3]$. P1 bị thu hồi CPU và phải lùi về Ready List với $Rem(P1) = 6$.
3. **Mốc $t = 3$**:
   - P2 chạy xong $CPU_1$ (1 đơn vị). P2 phát sinh yêu cầu I/O lần 1 trên thiết bị **R2** trong 8 đơn vị thời gian.
   - Thiết bị R2 đang hoàn toàn rảnh $\implies$ P2 chiếm R2 ngay lập tức từ $t = 3$ đến $t = 3 + 8 = 11$.
   - Trên CPU: Ready List chỉ còn lại P1 với $Rem(P1) = 6$. CPU được cấp lại cho P1 chạy tiếp từ $t = 3$ đến $t = 3 + 6 = 9$.
4. **Mốc $t = 9$**:
   - P1 chạy xong trọn vẹn $CPU_1$ (tổng cộng $2 + 6 = 8$ đơn vị). P1 phát sinh yêu cầu I/O lần 1 trên thiết bị **R1** trong 5 đơn vị thời gian.
   - Thiết bị R1 đang rảnh $\implies$ P1 chiếm R1 từ $t = 9$ đến $t = 9 + 5 = 14$.
   - Trên CPU: Ready List rỗng. Do đó CPU chuyển sang trạng thái **Nghỉ (IDLE)** trong khoảng $[9 - 10]$.
5. **Mốc $t = 10$**:
   - P3 xuất hiện tại RL với $CPU_1 = 6$.
   - CPU đang IDLE $\implies$ **P3 được cấp CPU** chạy ngay.
6. **Mốc $t = 11$ (Thời điểm đồng thời cực kỳ quan trọng)**:
   - Hai sự kiện xảy ra cùng lúc:
     - P4 xuất hiện tại RL với $CPU_1 = 3$.
     - P2 hoàn thành chu kỳ I/O trên thiết bị R2 ($3 + 8 = 11$), quay trở lại Ready List để thực hiện $CPU_2$ với thời lượng $Burst(P2) = 2$.
   - Kiểm tra tiến trình đang chạy trên CPU: P3 đã chạy được 1 đơn vị thời gian (từ 10 đến 11), thời gian còn lại là:
     $$Rem(P3) = 6 - 1 = 5$$
   - Hàng đợi Ready List hiện có 3 ứng viên với thời gian còn lại:
     - P2: 2 đơn vị
     - P4: 3 đơn vị
     - P3: 5 đơn vị
   - So sánh: $Rem(P2) = 2 < Rem(P4) = 3 < Rem(P3) = 5$.
   - **Xảy ra Trưng dụng!** P2 chiếm CPU chạy từ $t = 11$ đến $t = 11 + 2 = 13$. P3 bị đẩy về Ready List với $Rem(P3) = 5$. P4 xếp sau P2 trên Ready List.
7. **Mốc $t = 13$ (Nghẽn tài nguyên I/O)**:
   - P2 chạy xong $CPU_2$ (2 đơn vị). P2 phát sinh yêu cầu I/O lần 2 trên thiết bị **R1** với thời lượng 5 đơn vị.
   - **Kiểm tra R1**: Thiết bị R1 hiện đang bị P1 chiếm giữ (từ $t = 9$ đến $t = 14$).
   - Vì mỗi thiết bị chỉ có 1 thể hiện duy nhất và cấp phát theo FIFO $\implies$ **P2 buộc phải xếp hàng chờ trong Queue của R1** từ $t = 13$ đến $t = 14$ (chờ 1 đơn vị thời gian).
   - Trên CPU: Ready List gồm P4 ($Burst = 3$) và P3 ($Rem = 5$). Vì $3 < 5$, **P4 được cấp CPU** chạy từ $t = 13$.
8. **Mốc $t = 14$ (Giải phóng R1 & Trưng dụng CPU)**:
   - P1 hoàn thành I/O trên R1 đúng mốc $t = 14$.
     - Thiết bị R1 được giải phóng $\implies$ R1 lập tức cấp phát cho P2 đang đợi trong hàng đợi FIFO. P2 bắt đầu sử dụng R1 từ $t = 14$ đến $t = 14 + 5 = 19$.
     - P1 quay trở lại Ready List để làm $CPU_2$ với $Burst(P1) = 1$.
   - Trên CPU: P4 đã thực thi được 1 đơn vị thời gian (từ 13 đến 14), thời gian còn lại là:
     $$Rem(P4) = 3 - 1 = 2$$
   - So sánh: $Burst(P1) = 1 < Rem(P4) = 2$.
   - **Xảy ra Trưng dụng!** P1 chiếm quyền CPU ngay lập tức, chạy từ $t = 14$ đến $t = 15$. P4 bị đẩy ngược về Ready List với $Rem(P4) = 2$.
9. **Mốc $t = 15$**:
   - P1 chạy xong $CPU_2$ (1 đơn vị). P1 đã hoàn thành toàn bộ chu trình CPU và I/O $\implies$ **P1 KẾT THÚC (Terminated) tại $t = 15$**.
   - Trên CPU: Ready List còn P4 ($Rem = 2$) và P3 ($Rem = 5$).
   - Vì $2 < 5$, **P4 được cấp lại CPU** chạy tiếp từ $t = 15$ đến $t = 15 + 2 = 17$.
10. **Mốc $t = 17$**:
    - P4 chạy xong toàn bộ $CPU_1$ (tổng cộng $1 + 2 = 3$ đơn vị). P4 phát sinh yêu cầu I/O lần 1 trên thiết bị **R2** trong 20 đơn vị.
    - Kiểm tra R2: Thiết bị R2 đang rảnh (P2 đã giải phóng từ $t = 11$) $\implies$ P4 chiếm R2 từ $t = 17$ đến $t = 17 + 20 = 37$.
    - Trên CPU: Ready List chỉ còn lại P3 với $Rem(P3) = 5$. **P3 được cấp CPU** chạy từ $t = 17$ đến $t = 17 + 5 = 22$.
11. **Mốc $t = 19$**:
    - P2 hoàn thành chu kỳ I/O trên R1 ($14 + 5 = 19$).
    - P2 không còn chu kỳ nào khác $\implies$ **P2 KẾT THÚC tại $t = 19$**.
12. **Mốc $t = 22$**:
    - P3 hoàn thành $CPU_1$ (đã chạy đủ $1 + 5 = 6$ đơn vị). P3 yêu cầu I/O lần 1 trên thiết bị **R1** trong 5 đơn vị.
    - Thiết bị R1 đang rảnh (P2 đã trả từ $t = 19$) $\implies$ P3 chiếm R1 từ $t = 22$ đến $t = 22 + 5 = 27$.
    - Trên CPU: Không còn tiến trình nào trong Ready List $\implies$ CPU chuyển sang **IDLE** trong khoảng $[22 - 27]$.
13. **Mốc $t = 27$**:
    - P3 hoàn thành I/O trên R1, quay lại Ready List để thực hiện $CPU_2$ với $Burst(P3) = 2$.
    - CPU đang IDLE $\implies$ **P3 chiếm CPU** chạy từ $t = 27$ đến $t = 27 + 2 = 29$.
14. **Mốc $t = 29$ (Nghẽn tài nguyên R2)**:
    - P3 chạy xong $CPU_2$. P3 yêu cầu I/O lần 2 trên thiết bị **R2** với thời lượng 3 đơn vị.
    - **Kiểm tra R2**: Thiết bị R2 đang bị P4 độc quyền chiếm dụng (từ $t = 17$ đến $t = 37$).
    - $\implies$ **P3 phải xếp hàng chờ trong Queue của R2** từ $t = 29$ đến $t = 37$ (chờ ròng rã 8 đơn vị thời gian!).
    - Trên CPU: Không còn bất kỳ tiến trình nào $\implies$ CPU rơi vào trạng thái **IDLE** từ $t = 29$ đến $t = 37$.
15. **Mốc $t = 37$**:
    - P4 hoàn tất I/O trên R2 ($17 + 20 = 37$). P4 không có $CPU_2$ $\implies$ **P4 KẾT THÚC tại $t = 37$**.
    - Thiết bị R2 được giải phóng $\implies$ R2 cấp ngay cho P3. P3 thực thi I/O trên R2 từ $t = 37$ đến $t = 37 + 3 = 40$.
    - CPU tiếp tục **IDLE** từ $t = 37$ đến $t = 40$.
16. **Mốc $t = 40$**:
    - P3 hoàn tất I/O trên R2. P3 kết thúc toàn bộ công việc $\implies$ **P3 KẾT THÚC tại $t = 40$**.
    - Hệ thống hoàn thành 100% tất cả các tiến trình!

---

#### B. Phân tích chi tiết phương pháp tính Thời gian chờ (Waiting Time):

Trong tài liệu học thuật và các đề thi Hệ Điều Hành, thuật ngữ **Thời gian chờ (Waiting Time - WT)** có 2 cách diễn giải và tính toán:

1. **Cách 1: Thời gian chờ trên hàng đợi sẵn sàng ($WT_{RL}$ - Ready List Waiting Time)**
   - Theo định nghĩa của Silberschatz: *"Waiting time is the sum of the periods that a process spends waiting in the ready queue to get the CPU"*.
   - Theo cách này, các khoảng tiến trình nằm chờ tài nguyên I/O không được tính vào $WT$ của CPU.
   - Thống kê chi tiết:
     - **P1**: Vào RL lúc $t = 0$. Chạy $[0-2]$. Bị P2 chiếm CPU, phải chờ trong RL từ $t = 2$ đến $t = 3$ (1 đơn vị). Chạy tiếp $[3-9]$. Làm I/O $[9-14]$. Vào lại RL lúc 14, được chạy ngay $[14-15]$. $\implies WT_{RL}(P1) = 1$.
     - **P2**: Đến lúc $t = 2$, chiếm CPU ngay $[2-3]$. Làm I/O $[3-11]$. Đến RL lúc $t = 11$, chiếm CPU ngay $[11-13]$. Không có bất kỳ đơn vị thời gian nào phải chờ trên Ready List. $\implies WT_{RL}(P2) = 0$.
     - **P3**: Đến lúc $t = 10$, chiếm CPU ngay $[10-11]$. Tại $t = 11$ bị P2 chiếm CPU, P3 phải nằm chờ trong RL suốt thời gian P2 chạy $[11-13]$, P4 chạy $[13-14]$, P1 chạy $[14-15]$, và P4 chạy $[15-17]$. Tổng thời gian chờ trên RL là từ $t = 11$ đến $t = 17$ (chờ 6 đơn vị). Sau đó xong I/O lúc $t = 27$, chiếm CPU ngay $[27-29]$. $\implies WT_{RL}(P3) = 6$.
     - **P4**: Đến lúc $t = 11$. Nằm chờ P2 chạy từ $t = 11$ đến $t = 13$ (2 đơn vị). Chạy $[13-14]$. Bị P1 chiếm CPU, nằm chờ P1 chạy từ $t = 14$ đến $t = 15$ (1 đơn vị). Chạy tiếp $[15-17]$. Tổng thời gian chờ trên RL: $2 + 1 = 3$ đơn vị. $\implies WT_{RL}(P4) = 3$.
   - **Trung bình $AWT_{RL} = (1 + 0 + 6 + 3) / 4 = 10 / 4 = \mathbf{2.5}$**.

2. **Cách 2: Tổng thời gian chờ toàn hệ thống ($WT_{total}$ - Total System Waiting Time)**
   - Trong môi trường tài nguyên I/O có giới hạn thể hiện (được cấp phát qua FIFO), tiến trình không chỉ chờ CPU mà còn phải chờ đợi nhau ở hàng đợi thiết bị ngoại vi ($WT_{IO\_Queue}$).
   - Công thức bù trừ chuẩn:
     $$WT_{total} = TAT - (Tổng\ thời\ gian\ thực\ thi\ CPU + Tổng\ thời\ gian\ thực\ hiện\ I/O)$$
   - Thống kê chi tiết:
     - **P1**: $TAT = 15 - 0 = 15$. Phục vụ: $CPU(9) + IO(5) = 14$. $\implies WT_{total}(P1) = 15 - 14 = \mathbf{1}$.
     - **P2**: $TAT = 19 - 2 = 17$. Phục vụ: $CPU(3) + IO(13) = 16$. $\implies WT_{total}(P2) = 17 - 16 = \mathbf{1}$ *(chính là 1 đơn vị chờ R1 tại $[13-14]$)*.
     - **P3**: $TAT = 40 - 10 = 30$. Phục vụ: $CPU(8) + IO(8) = 16$. $\implies WT_{total}(P3) = 30 - 16 = \mathbf{14}$ *(gồm 6 đơn vị chờ RL + 8 đơn vị chờ R2 tại $[29-37]$)*.
     - **P4**: $TAT = 37 - 11 = 26$. Phục vụ: $CPU(3) + IO(20) = 23$. $\implies WT_{total}(P4) = 26 - 23 = \mathbf{3}$.
   - **Trung bình $AWT_{total} = (1 + 1 + 14 + 3) / 4 = 19 / 4 = \mathbf{4.75}$**.

*(Việc trình bày đầy đủ cả hai cách tính là chuẩn mực cao nhất, giúp giải bài thi trọn vẹn điểm số bất kể barem chấm thiên về quan điểm nào).*

---

## BÀI TẬP 2: ĐIỀU PHỐI SJF KHÔNG ĐỘC QUYỀN (SRTF) VỚI NHIỀU CHU KỲ CPU & I/O

### Đề bài:
Thực hiện điều phối theo chiến lược SJF không độc quyền (SRTF) cho các tiến trình sau:
| Tiến trình | Thời điểm vào RL | CPU lần 1 | I/O lần 1 | CPU lần 2 | I/O lần 2 | CPU lần 3 |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **P1** | 0 | 2 | 4 | 3 | — | — |
| **P2** | 3 | 6 | 3 | 2 | 3 | 2 |
| **P3** | 4 | 4 | 4 | 2 | — | — |
| **P4** | 4 | 3 | 4 | 1 | 3 | 2 |

*Yêu cầu*:
- a. Trình bày quá trình điều phối và vẽ sơ đồ điều phối (sơ đồ Gantt).
- b. Tính thời gian chờ cho các tiến trình.

*(Lưu ý: Trong Bài tập 2, đề bài không chỉ định thiết bị dùng chung có định danh, do đó các thao tác I/O được xem là độc lập và diễn ra đồng thời không bị nghẽn kênh).*

---

### PHẦN 2.1: TRÌNH BÀY LỜI GIẢI CHUẨN (BÀI 2)

#### 1. Sơ đồ Gantt Điều phối CPU (SJF Không độc quyền / Preemptive SJF - SRTF):

```
+----+----+----+----+----+----+----+----+----+----+----+----+----+----+----+----+
| P1 |IDLE| P2 | P4 | P1 | P3 | P4 | P3 | P4 | P2 | P3 | P2 |IDLE| P2 |IDLE| P2 |
+----+----+----+----+----+----+----+----+----+----+----+----+----+----+----+----+
0    2    3    4    7   10   11   12   15   17   19   21   24   27   29   32   34
```

---

#### 2. Bảng kết quả tính toán Thời gian lưu lại ($TAT$) và Thời gian chờ ($WT$):

*Công thức áp dụng*:
- $TAT = T_{finish} - T_{arrive}$
- $WT = TAT - (Tổng\ CPU + Tổng\ IO)$

| Tiến trình | $T_{arrive}$ | $T_{finish}$ | $TAT$ | Tổng thời gian CPU | Tổng thời gian I/O | Chi tiết các khoảng chờ trong Ready List | Thời gian chờ ($WT$) |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **P1** | 0 | 10 | $10 - 0 = \mathbf{10}$ | $2 + 3 = 5$ | 4 | Chờ lúc xong I/O 1: $[6 - 7]$ (khi P4 đang chạy) | **1** |
| **P2** | 3 | 34 | $34 - 3 = \mathbf{31}$ | $6 + 2 + 2 = 10$ | $3 + 3 = 6$ | • Bị chiếm CPU lúc $[4 - 17]$ (13 đv)<br>• Bị chiếm CPU lúc $[19 - 21]$ (2 đv) | **15** |
| **P3** | 4 | 21 | $21 - 4 = \mathbf{17}$ | $4 + 2 = 6$ | 4 | • Chờ từ khi đến: $[4 - 10]$ (6 đv)<br>• Bị P4 chiếm lúc: $[11 - 12]$ (1 đv) | **7** |
| **P4** | 4 | 17 | $17 - 4 = \mathbf{13}$ | $3 + 1 + 2 = 6$ | $4 + 3 = 7$ | Không phải chờ (luôn có burst ngắn nhất khi vào RL) | **0** |
| **TRUNG BÌNH** | — | — | $\mathbf{71/4 = 17.75}$ | — | — | — | $\mathbf{23/4 = 5.75}$ |

**Đáp số**:
- Thời gian chờ của từng tiến trình:
  - $WT(P1) = 1$
  - $WT(P2) = 15$
  - $WT(P3) = 7$
  - $WT(P4) = 0$
- **Thời gian chờ trung bình ($AWT$)**: $\mathbf{23/4 = 5.75}$ đơn vị thời gian.
- **Thời gian lưu lại trung bình ($ATAT$)**: $\mathbf{71/4 = 17.75}$ đơn vị thời gian.

---

### PHẦN 2.2: GIẢI THÍCH CHI TIẾT, CỤ THỂ, CHÍNH XÁC LỜI GIẢI (BÀI 2)

#### Phân tích quá trình điều phối qua từng mốc thời gian:

1. **Mốc $t = 0$**:
   - P1 vào Ready List với $CPU_1 = 2$.
   - CPU rảnh $\implies$ P1 được cấp CPU chạy $[0 - 2]$.
2. **Mốc $t = 2$**:
   - P1 hoàn thành $CPU_1$. P1 chuyển sang làm I/O lần 1 với thời lượng 4 đơn vị (từ $t = 2$ đến $t = 2 + 4 = 6$).
   - Hàng đợi Ready List rỗng $\implies$ CPU rơi vào trạng thái **IDLE** trong khoảng $[2 - 3]$.
3. **Mốc $t = 3$**:
   - P2 xuất hiện tại Ready List với $CPU_1 = 6$.
   - CPU đang IDLE $\implies$ P2 được cấp CPU chạy ngay từ $t = 3$.
4. **Mốc $t = 4$ (Hai tiến trình mới cùng xuất hiện)**:
   - Tại $t = 4$, đồng thời P3 (burst 4) và P4 (burst 3) xuất hiện tại Ready List.
   - P2 đã chạy được 1 đơn vị thời gian (từ 3 đến 4), thời gian còn lại là:
     $$Rem(P2) = 6 - 1 = 5$$
   - So sánh thời gian thực thi còn lại giữa 3 ứng viên:
     - P4: 3
     - P3: 4
     - P2: 5
   - Do $Burst(P4) = 3 < Rem(P2) = 5 \implies$ **Trưng dụng CPU (Preemption)!**
   - P4 chiếm quyền CPU chạy từ $t = 4$. P2 bị thu hồi CPU, quay về Ready List với $Rem(P2) = 5$. P3 nằm trong Ready List với $Burst(P3) = 4$.
5. **Mốc $t = 6$ (Tiến trình xong I/O quay lại nhưng không trưng dụng)**:
   - P1 hoàn tất I/O lần 1 ($2 + 4 = 6$), quay lại Ready List với $CPU_2 = 3$.
   - Đánh giá tại $t = 6$: P4 đang chạy trên CPU (đã chạy từ 4 đến 6, tức 2 đơn vị). Thời gian còn lại của P4 là:
     $$Rem(P4) = 3 - 2 = 1$$
   - So sánh: $Rem(P4) = 1 < Burst(P1) = 3$.
   - **Không xảy ra trưng dụng!** P4 tiếp tục chạy nốt 1 đơn vị còn lại đến $t = 7$.
   - P1 phải chờ trong Ready List từ $t = 6$ đến $t = 7$ (chờ 1 đơn vị thời gian).
6. **Mốc $t = 7$**:
   - P4 hoàn thành $CPU_1$ (3 đơn vị). P4 chuyển sang thực hiện I/O lần 1 trong 4 đơn vị (từ $t = 7$ đến $t = 7 + 4 = 11$).
   - Ready List hiện có:
     - P1: $Rem = 3$
     - P3: $Rem = 4$
     - P2: $Rem = 5$
   - So sánh: $Rem(P1) = 3$ là ngắn nhất $\implies$ **P1 chiếm CPU** chạy từ $t = 7$ đến $t = 7 + 3 = 10$.
7. **Mốc $t = 10$**:
   - P1 chạy xong $CPU_2$ (3 đơn vị). P1 đã hoàn thành toàn bộ chu kỳ và **KẾT THÚC tại $t = 10$**.
   - Ready List còn: P3 ($Rem = 4$) và P2 ($Rem = 5$).
   - Vì $4 < 5$, **P3 được cấp CPU** chạy từ $t = 10$.
8. **Mốc $t = 11$ (Trưng dụng CPU)**:
   - P4 hoàn thành I/O lần 1 ($7 + 4 = 11$), quay lại Ready List để thực hiện $CPU_2$ với thời lượng $Burst(P4) = 1$.
   - P3 đang chạy trên CPU (từ 10 đến 11, tức 1 đơn vị), thời gian còn lại là:
     $$Rem(P3) = 4 - 1 = 3$$
   - So sánh: $Burst(P4) = 1 < Rem(P3) = 3$.
   - **Xảy ra Trưng dụng!** P4 chiếm quyền CPU chạy $[11 - 12]$. P3 bị thu hồi CPU, quay lại Ready List với $Rem(P3) = 3$.
9. **Mốc $t = 12$**:
   - P4 chạy xong $CPU_2$ (1 đơn vị). P4 chuyển sang làm I/O lần 2 với thời lượng 3 đơn vị (từ $t = 12$ đến $t = 12 + 3 = 15$).
   - Ready List còn: P3 ($Rem = 3$) và P2 ($Rem = 5$).
   - Vì $3 < 5$, **P3 được cấp lại CPU** chạy tiếp từ $t = 12$ đến $t = 12 + 3 = 15$.
10. **Mốc $t = 15$**:
    - Hai sự kiện đồng thời:
      - P3 chạy xong $CPU_1$ (đã đủ $1 + 3 = 4$ đơn vị). P3 chuyển sang làm I/O lần 1 trong 4 đơn vị (từ $t = 15$ đến $t = 15 + 4 = 19$).
      - P4 hoàn thành I/O lần 2 ($12 + 3 = 15$), quay lại Ready List với $CPU_3 = 2$.
    - Ready List có: P4 ($Burst = 2$) và P2 ($Rem = 5$).
    - Vì $2 < 5$, **P4 được cấp CPU** chạy từ $t = 15$ đến $t = 15 + 2 = 17$.
11. **Mốc $t = 17$**:
    - P4 chạy xong $CPU_3$ (2 đơn vị). P4 đã hoàn tất toàn bộ các chu trình $\implies$ **P4 KẾT THÚC tại $t = 17$**.
    - Ready List chỉ còn duy nhất P2 với $Rem(P2) = 5$.
    - **P2 được cấp CPU** tiếp tục chạy từ $t = 17$.
12. **Mốc $t = 19$ (Trưng dụng CPU)**:
    - P3 hoàn tất I/O lần 1 ($15 + 4 = 19$), quay lại Ready List với $CPU_2 = 2$.
    - P2 đang chạy trên CPU (từ 17 đến 19, tức 2 đơn vị). Thời gian còn lại của $CPU_1$ là:
      $$Rem(P2) = 5 - 2 = 3$$
    - So sánh: $Burst(P3) = 2 < Rem(P2) = 3$.
    - **Xảy ra Trưng dụng!** P3 chiếm CPU chạy từ $t = 19$ đến $t = 19 + 2 = 21$. P2 quay lại Ready List với $Rem(P2) = 3$.
13. **Mốc $t = 21$**:
    - P3 hoàn tất $CPU_2$ (2 đơn vị). P3 hoàn thành toàn bộ chu trình $\implies$ **P3 KẾT THÚC tại $t = 21$**.
    - Ready List chỉ còn P2 ($Rem = 3$).
    - **P2 được cấp CPU** chạy tiếp từ $t = 21$ đến $t = 21 + 3 = 24$.
14. **Mốc $t = 24$**:
    - P2 hoàn tất trọn vẹn $CPU_1$ (đã chạy đủ $1 + 2 + 3 = 6$ đơn vị).
    - P2 chuyển sang thực hiện I/O lần 1 trong 3 đơn vị (từ $t = 24$ đến $t = 24 + 3 = 27$).
    - Ready List rỗng $\implies$ CPU rơi vào trạng thái **IDLE** trong khoảng $[24 - 27]$.
15. **Mốc $t = 27$**:
    - P2 hoàn thành I/O lần 1, quay lại Ready List với $CPU_2 = 2$.
    - CPU đang IDLE $\implies$ P2 được cấp CPU chạy ngay từ $t = 27$ đến $t = 27 + 2 = 29$.
16. **Mốc $t = 29$**:
    - P2 hoàn thành $CPU_2$ (2 đơn vị).
    - P2 chuyển sang làm I/O lần 2 trong 3 đơn vị (từ $t = 29$ đến $t = 29 + 3 = 32$).
    - Ready List rỗng $\implies$ CPU rơi vào trạng thái **IDLE** trong khoảng $[29 - 32]$.
17. **Mốc $t = 32$**:
    - P2 hoàn thành I/O lần 2, quay lại Ready List với $CPU_3 = 2$.
    - CPU đang IDLE $\implies$ P2 được cấp CPU chạy ngay từ $t = 32$ đến $t = 32 + 2 = 34$.
18. **Mốc $t = 34$**:
    - P2 hoàn thành $CPU_3$ (2 đơn vị). P2 kết thúc mọi tác vụ $\implies$ **P2 KẾT THÚC tại $t = 34$**.
    - Hệ thống hoàn thành xuất sắc toàn bộ 4 tiến trình!

---

#### B. Phân tích chi tiết cách tính Thời gian chờ ($WT$) của Bài tập 2:

Do Bài tập 2 không có hiện tượng tranh chấp tài nguyên I/O (không giới hạn thể hiện, không có hàng đợi thiết bị), thời gian chờ toàn hệ thống hoàn toàn trùng khớp với thời gian chờ trong Ready List ($WT_{total} = WT_{RL}$).

Ta kiểm chứng tính chính xác thông qua 2 cách tính độc lập:

- **Cách 1: Trừ bù thời gian (Turnaround Time Subtraction)**:
  - $WT = TAT - (Tổng\ CPU + Tổng\ IO)$
  - $WT(P1) = (10 - 0) - (5 + 4) = 10 - 9 = \mathbf{1}$
  - $WT(P2) = (34 - 3) - (10 + 6) = 31 - 16 = \mathbf{15}$
  - $WT(P3) = (21 - 4) - (6 + 4) = 17 - 10 = \mathbf{7}$
  - $WT(P4) = (17 - 4) - (6 + 7) = 13 - 13 = \mathbf{0}$

- **Cách 2: Thống kê từng khoảng thời gian thực tế nằm trong Ready List**:
  - **P1**: Vào RL lần 2 tại $t = 6$. Chờ P4 chạy xong từ $t = 6$ đến $t = 7$. $\implies WT(P1) = 7 - 6 = \mathbf{1}$.
  - **P2**:
    - Bị P4 chiếm CPU tại $t = 4$, phải nằm chờ trong Ready List qua các giai đoạn: P4 chạy $[4-7]$, P1 chạy $[7-10]$, P3 chạy $[10-11]$, P4 chạy $[11-12]$, P3 chạy $[12-15]$, P4 chạy $[15-17]$. Khoảng chờ thứ nhất: $17 - 4 = 13$ đơn vị.
    - Bị P3 chiếm CPU tại $t = 19$, phải nằm chờ P3 chạy $[19-21]$. Khoảng chờ thứ hai: $21 - 19 = 2$ đơn vị.
    - Tại $t = 27$ và $t = 32$, CPU đều đang IDLE nên P2 được chạy ngay (chờ 0 đơn vị).
    - $\implies WT(P2) = 13 + 2 = \mathbf{15}$.
  - **P3**:
    - Vào RL tại $t = 4$, phải chờ P4 chạy $[4-7]$ và P1 chạy $[7-10]$. Khoảng chờ thứ nhất: $10 - 4 = 6$ đơn vị.
    - Bị P4 chiếm CPU tại $t = 11$, phải chờ P4 chạy $[11-12]$. Khoảng chờ thứ hai: $12 - 11 = 1$ đơn vị.
    - Vào RL lần 2 tại $t = 19$, chiếm CPU ngay lúc $t = 19$ (chờ 0 đơn vị).
    - $\implies WT(P3) = 6 + 1 = \mathbf{7}$.
  - **P4**:
    - Đến RL lúc $t = 4$, chiếm CPU ngay $[4-7]$.
    - Vào RL lần 2 lúc $t = 11$, chiếm CPU ngay $[11-12]$.
    - Vào RL lần 3 lúc $t = 15$, chiếm CPU ngay $[15-17]$.
    - P4 luôn sở hữu burst ngắn nhất tại mọi thời điểm xuất hiện nên không bao giờ phải chờ đợi!
    - $\implies WT(P4) = \mathbf{0}$.

Kết quả của hai phương pháp hoàn toàn khớp nhau $100\%$, khẳng định bài giải chuẩn xác tuyệt đối.

---

## TỔNG KẾT SO SÁNH VÀ BÀI HỌC KINH NGHIỆM LÀM BÀI THI

| Tiêu chí so sánh | Bài tập 1 (Có tài nguyên định danh R1, R2) | Bài tập 2 (Nhiều chu kỳ CPU - I/O xen kẽ) |
| :--- | :--- | :--- |
| **Chiến lược điều phối CPU** | Preemptive SJF (SRTF) | Preemptive SJF (SRTF) |
| **Bản chất kênh I/O** | Tài nguyên dùng chung, mỗi loại 1 thể hiện duy nhất, cấp phát FIFO. | Kênh I/O độc lập / đồng thời, không bị giới hạn thể hiện. |
| **Hiện tượng nghẽn thiết bị** | **Có nghẽn**: P2 bị nghẽn R1 tại $[13-14]$; P3 bị nghẽn R2 tại $[29-37]$. | **Không nghẽn**: Mọi tiến trình đến I/O đều được phục vụ ngay. |
| **Trạng thái CPU IDLE** | Xảy ra khi tất cả tiến trình đều đang bận làm I/O hoặc đang chờ thiết bị I/O. | Xảy ra khi chỉ còn 1 tiến trình duy nhất trong hệ thống và đang làm I/O. |
| **Cách tính Waiting Time** | Cần phân định rõ giữa $WT_{ReadyList}$ và $WT_{total}$ (gồm cả thời gian chờ thiết bị). | $WT_{ReadyList}$ và $WT_{total}$ hoàn toàn trùng khớp nhau. |

> ### BÀI HỌC KINH NGHIỆM LÀM BÀI THI MÔN HỆ ĐIỀU HÀNH
> 1. **Luôn chú ý mốc thời gian diễn ra nhiều sự kiện đồng thời**: Ví dụ tại $t = 11$ (Bài 1), vừa có tiến trình mới đến, vừa có tiến trình xong I/O quay lại. Phải liệt kê đầy đủ tất cả ứng viên trong Ready List và so sánh chính xác remaining burst.
> 2. **Vẽ sơ đồ Gantt phụ cho tài nguyên I/O**: Đối với các bài toán có gán nhãn thiết bị $R1, R2$ và giới hạn số thể hiện (như Bài 1), hãy vẽ song song sơ đồ Gantt cho từng thiết bị ngoại vi. Điều này giúp không bao giờ bị bỏ sót việc một tiến trình bị nghẽn thiết bị và phải đợi trong hàng đợi FIFO.
> 3. **Kiểm tra chéo bằng 2 công thức**: Sau khi vẽ sơ đồ Gantt, luôn dùng cả 2 cách (trừ bù $TAT - CPU - IO$ và đếm trực tiếp các khoảng chờ trên Gantt) để tự tin 100% bài làm không bị sai sót số liệu.
