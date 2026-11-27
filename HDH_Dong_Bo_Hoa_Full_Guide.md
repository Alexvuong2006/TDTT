# Tổng Hợp Kiến Thức & Giải Bài Tập: Đồng Bộ Hóa (Synchronization)

> **Môn học:** Hệ điều hành (FIT@HCMUS)  
> **Nguồn tài liệu:** `Bai05_Dong_bo_hoa.pdf` & `Baitap_DBH.pdf`

---

## Mục lục
- [Phần I: Tổng hợp kiến thức về Đồng bộ hóa](#phần-i-tổng-hợp-kiến-thức-về-đồng-bộ-hóa)
  - [1. Liên lạc giữa các tiến trình (IPC – Inter-process Communication)](#1-liên-lạc-giữa-các-tiến-trình-ipc--inter-process-communication)
  - [2. Các vấn đề xử lý đồng hành](#2-các-vấn-đề-xử-lý-đồng-hành)
  - [3. Yêu cầu đối với một giải pháp đồng bộ hóa](#3-yêu-cầu-đối-với-một-giải-pháp-đồng-bộ-hóa)
  - [4. Các giải pháp đồng bộ hóa](#4-các-giải-pháp-đồng-bộ-hóa)
  - [5. Các bài toán đồng bộ hóa kinh điển](#5-các-bài-toán-đồng-bộ-hóa-kinh-điển)
- [Phần II: Giải bài tập Đồng bộ hóa](#phần-ii-giải-bài-tập-đồng-bộ-hóa)
  - [Bài tập 1: Bài toán Tạo phân tử $H_2O$](#bài-tập-1-bài-toán-tạo-phân-tử-h_2o)
  - [Bài tập 2: Bài toán Hãng sản xuất xe ôtô](#bài-tập-2-bài-toán-hãng-sản-xuất-xe-ôtô)
  - [Bài tập 3: Quy trình thu mua mía của nhà máy mía đường](#bài-tập-3-quy-trình-thu-mua-mía-của-nhà-máy-mía-đường)
  - [Bài tập 4: Bài toán Qua sông (Nhân viên Microsoft & Linux Hacker)](#bài-tập-4-bài-toán-qua-sông-nhân-viên-microsoft--linux-hacker)

---

# Phần I: Tổng hợp kiến thức về Đồng bộ hóa

## 1. Liên lạc giữa các tiến trình (IPC – Inter-process Communication)

Các tiến trình hoạt động đồng hành thường cần trao đổi dữ liệu hoặc phối hợp với nhau. Có 2 nhóm cơ chế trao đổi dữ liệu chính:

### 1.1. Chia sẻ tài nguyên dùng chung
Các tiến trình chia sẻ chung bộ nhớ (Memory), không gian hệ thống tập tin (File System Space), hoặc các phương tiện/giao thức liên lạc thông qua OS Kernel:
- **Signal:**
  - Gồm *Meaning* (ý nghĩa tín hiệu) và *Handler* (hàm xử lý). Phải được định nghĩa trước khi liên lạc (`SIGINT`, `SIGSTOP`, `SIGUSR1`, `SIGUSR2`,...).
  - Hỗ trợ liên lạc **không đồng bộ** giữa Kernel với user process (lỗi tiến trình, timer, tiến trình con kết thúc,...) hoặc giữa các user process với nhau (kết thúc tiến trình, tạm dừng/tiếp tục,...).
  - **Không cho phép trao đổi dữ liệu.**
  - *Một số signal thường gặp:* `SIGHUP` (1), `SIGINT` (2 - Ctrl+C), `SIGQUIT` (3 - Ctrl+\), `SIGFPE` (8 - chia cho 0), `SIGKILL` (9 - kill process), `SIGUSR1` (10), `SIGSEGV` (11 - truy cập bộ nhớ trái phép), `SIGUSR2` (12), `SIGALRM` (14 - hết giờ `alarm()`), `SIGTERM` (15), `SIGCHLD` (17), `SIGCONT` (18), `SIGSTOP` (19), `SIGTSTP` (20 - Ctrl+Z), `SIGWINCH` (28).
- **Pipes:**
  - Là một kernel buffer (dạng file) có kích thước giới hạn (4KB, 8KB). HĐH cung cấp `WritePipe()` & `ReadPipe()`. Cần đồng bộ khi ghi lúc Pipe đầy hoặc đọc lúc Pipe rỗng.
  - *UNIX original Pipe:* Liên lạc giữa 2 tiến trình Cha – Con, **một chiều**, không cấu trúc (byte transfer).
  - *Named Pipe (Unix, Windows NT,...):* Truyền dữ liệu **có cấu trúc**, liên lạc **2 chiều**.
- **Shared Memory:**
  - Một vùng nhớ không thuộc sở hữu riêng của tiến trình nào, do HĐH tạo ra.
  - Các tiến trình ánh xạ địa chỉ vào vùng nhớ này (`shmget()`, `shmat()`, `shmctl()`,...) để truy xuất như bộ nhớ nội bộ.
  - Không giới hạn số tiến trình, chiều trao đổi và thứ tự truy cập $\rightarrow$ dễ gây **mâu thuẫn truy xuất** $\rightarrow$ **cần đồng bộ hóa**.

### 1.2. Trao đổi thông điệp
Không sử dụng bộ nhớ chung, cần đường kết nối giữa các máy tính:
- **Message Passing:**
  - Dữ liệu có cấu trúc, được thỏa thuận trước giữa 2 tiến trình.
  - HĐH cung cấp 2 primitive: `send(destination, message)` và `receive(source, message)`.
  - Các vấn đề quan tâm: Định địa chỉ trực tiếp/gián tiếp (Direct/Indirect addressing), Blocking/Non-blocking, Tin cậy/Không tin cậy (Reliable/Unreliable), Có buffer/Không buffer.
  - Là cơ chế IPC tổng quát (dùng được cả trên cùng máy và hệ thống phân tán, cần chú ý khi liên lạc giữa các hệ thống không đồng nhất như UNIX – Windows).
- **Socket:** Được tìm hiểu sâu trong môn Mạng máy tính.

---

## 2. Các vấn đề xử lý đồng hành

Khi nhiều tiến trình chạy song song (concurrent), có 2 vấn đề cốt lõi phát sinh:

### 2.1. Tranh chấp điều khiển (Race Condition) & Độc quyền truy xuất (Mutual Exclusion)
- **Định nghĩa:** Xảy ra khi nhiều tiến trình truy xuất đồng thời một tài nguyên mang bản chất **không chia sẻ được**. Kết quả phụ thuộc vào thứ tự điều phối (scheduling) của CPU (*bad interleavings*) $\rightarrow$ cùng input nhưng output có thể khác nhau, khó phát hiện và khó debug.
- **Ví dụ:**
  - *Ví dụ 1:* Hai tiến trình $P_1, P_2$ cùng thực hiện `read hits; hits = hits + 1;` trên biến chung `hits = 0`. Nếu bị xen ngang sau khi đọc, kết quả cuối có thể là `1` thay vì `2`.
  - *Ví dụ 2:* Thread A (`while(i < 10) i = i + 1;`) và Thread B (`while(i > -10) i = i - 1;`) cùng thao tác trên `i = 0`.
- **Hướng giải quyết:**
  - Bảo đảm tính **atomicity** (không thể phân chia) khi truy xuất tài nguyên chung.
  - Xác định **Miền găng (Critical Section / Critical Region - CS)**: đoạn chương trình có khả năng gây ra race condition.
  - Áp dụng **Độc quyền truy xuất (Mutual Exclusion)** cho CS theo mô hình:
    1. Kiểm tra và giành quyền vào CS.
    2. Thực thi `CS;`.
    3. Từ bỏ quyền sử dụng CS.

### 2.2. Phối hợp xử lý (Rendez-vous)
- **Vấn đề:** Các tiến trình chạy độc lập không biết tiến độ của nhau nên thứ tự thực hiện công việc có thể bị đảo lộn, không ăn khớp (ví dụ: $P_1$ gửi `"em"`, $P_2$ gửi `"yêu"`, $P_3$ gửi `"anh"`, $P_4$ gửi `"không"` nhưng có thể bị in thành `"anh không yêu em"`).
- **Hướng giải quyết:** Hỗ trợ **Rendez-vous** ("hẹn hò") để bảo đảm trình tự xử lý định trước:
  - $P_1$: Thực hiện `Job1;` $\rightarrow$ **Báo hiệu**.
  - $P_2$: **Chờ** báo hiệu $\rightarrow$ Thực hiện `Job2;`.

---

## 3. Yêu cầu đối với một giải pháp đồng bộ hóa

Một giải pháp đồng bộ hóa tốt cho bài toán miền găng cần thỏa mãn **3 điều kiện**:
1. **Mutual Exclusion (Độc quyền truy xuất):** Tại một thời điểm, không có hai tiến trình nào cùng ở trong miền găng.
2. **Progress (Tiến triển):** Một tiến trình đang tạm dừng bên ngoài miền găng không được ngăn cản các tiến trình khác vào miền găng.
3. **Bounded Waiting (Chờ đợi hữu hạn):** Không có tiến trình nào phải chờ đợi vô hạn để được vào miền găng (tránh *starvation*).

> **Lưu ý:** Không được đặt giả thiết về tốc độ tương đối giữa các tiến trình cũng như số lượng bộ xử lý trong hệ thống.

---

## 4. Các giải pháp đồng bộ hóa

### 4.1. Nhóm giải pháp Busy Waiting
Tiến trình tiếp tục **tiêu thụ CPU** trong vòng lặp (`while (chưa có quyền) do_nothing();`) khi chờ vào CS; không cần sự trợ giúp của HĐH.

#### a) Giải pháp phần mềm
| Giải pháp | Cơ chế | Đánh giá |
| :--- | :--- | :--- |
| **Biến cờ hiệu** (`int lock = 0`) | Kiểm tra `while (lock == 1);` rồi gán `lock = 1;` trước CS; ra khỏi CS gán `lock = 0;`. | Mở rộng được cho $N$ tiến trình, nhưng **KHÔNG bảo đảm Mutual Exclusion** vì bản thân đoạn kiểm tra và gán `lock` cũng là CS (có thể bị ngắt giữa chừng). |
| **Kiểm tra luân phiên** (`int turn = 1`) | $T_0$ chờ `while (turn != 0);` và gán `turn = 1;` khi xong; $T_1$ ngược lại. | Chỉ dùng cho 2 tiến trình. Bảo đảm Mutual Exclusion, nhưng **KHÔNG bảo đảm Progress** ("mở cửa" cho người = "đóng cửa" chính mình; nếu $T_1$ dừng ở NonCS thì $T_0$ không vào được CS lần 2). |
| **Giải pháp Peterson** | Kết hợp `turn` và mảng `interest[2]` (`interest[i] = TRUE; turn = j; while (turn == j && interest[j] == TRUE);`). | Đáp ứng **đủ cả 3 điều kiện** (Mutual Exclusion, Progress, Bounded Waiting) cho 2 tiến trình, nhưng **không thể mở rộng cho $N$ tiến trình**. |

#### b) Giải pháp phần cứng
- **Cấm ngắt (`Disable Interrupt` / `Enable Interrupt`):**
  - Cấm mọi ngắt (kể cả ngắt đồng hồ) trước khi vào CS và bật lại khi ra.
  - *Nhược điểm:* Quá nguy hiểm (nếu tiến trình bị khóa trong CS $\rightarrow$ System Halt; trao lệnh đặc quyền cho user process) và **không bảo đảm Mutual Exclusion trên máy nhiều CPU / multi-core**.
- **Chỉ thị TSL (Test and Set Lock):**
  - CPU cung cấp lệnh atomic `TSL(boolean &target)`: trả về giá trị hiện tại của `target` và đặt `target = TRUE`.
  - Sử dụng: `while (TSL(lock));` $\rightarrow$ `CS;` $\rightarrow$ `lock = 0;`.
  - Dễ mở rộng cho $N$ tiến trình nhưng vẫn lãng phí CPU do busy-waiting.

> **Nhận xét chung nhóm Busy Waiting:** Sử dụng CPU không hiệu quả. Để khắc phục, cần **khóa (block)** các tiến trình chưa đủ điều kiện vào CS để nhường CPU cho tiến trình khác (nhờ Scheduler của HĐH).

---

### 4.2. Nhóm giải pháp Sleep & Wakeup
Cần sự hỗ trợ của HĐH để thay đổi trạng thái tiến trình:
- `Sleep()`: Chuyển tiến trình gọi sang trạng thái *Blocked*.
- `WakeUp(P)`: Chuyển tiến trình $P$ sang trạng thái *Ready*.

#### a) Áp dụng `Sleep()` & `WakeUp()` thô sơ và vấn đề
Dùng biến `busy` và `blocked` kết hợp `if (busy) { blocked++; Sleep(); } else busy = 1;`.  
**Vấn đề:** Do việc kiểm tra điều kiện và gọi `Sleep()` không phải thao tác nguyên tử (atomic) nên có thể bị ngắt quãng giữa chừng $\rightarrow$ dẫn đến **WakeUp bị "lạc" (Lost Wakeup)**, làm tiến trình bị *Blocked vĩnh viễn*.

#### b) Semaphore (Dijkstra, 1965)
- Là cơ chế do HĐH cung cấp, gồm một giá trị nguyên `value` và hàng đợi `L` chứa các tiến trình đang bị block:
  ```c
  typedef struct {
      int value;
      struct process* L;
  } Semaphore;
  ```
- Chỉ thao tác qua 2 primitive **không thể phân chia (atomic / cấm ngắt)**:
  ```c
  Down(S) {
      S.value--;
      if (S.value < 0) {
          Add(P, S.L);
          Sleep();
      }
  }

  Up(S) {
      S.value++;
      if (S.value <= 0) {
          Remove(P, S.L);
          Wakeup(P);
      }
  }
  ```
- **2 mô hình sử dụng chuẩn:**
  1. **Độc quyền truy xuất (Mutual Exclusion):** Khởi tạo `Semaphore s = 1;`
     ```c
     Down(s);
     CS;
     Up(s);
     ```
  2. **Phối hợp xử lý (Rendez-vous):** Khởi tạo `Semaphore s = 0;`
     - Tiến trình $P_1$: `Job1; Up(s);`
     - Tiến trình $P_2$: `Down(s); Job2;`
- *Nhận xét:* Rất tốt và dễ dùng cho $N$ tiến trình, nhưng ý nghĩa sử dụng (Mutex hay Rendez-vous) chỉ phân biệt qua mô hình nên dễ gây nhầm lẫn khi lập trình.

#### c) Mutex (trong `pthread`)
- Là phiên bản đơn giản hóa của Semaphore (chỉ có 2 trạng thái: *locked - 0* và *unlocked - 1*), phù hợp cho tiểu trình (thread) ở không gian người dùng.
- **Độc quyền truy xuất:** `pthread_mutex_lock(&the_mutex); CS; pthread_mutex_unlock(&the_mutex);`
- **Phối hợp xử lý:** Kết hợp với biến điều kiện `pthread_cond_t cond` qua `pthread_cond_wait(&cond, &the_mutex)` và `pthread_cond_signal(&cond)`.

#### d) Monitor (Hoare 1974 & Brinch 1975)
- Là cơ chế do **ngôn ngữ lập trình** cung cấp dưới dạng một module đóng gói (encapsulation) các dữ liệu dùng chung và các phương thức thao tác trên dữ liệu đó.
- **Tự động bảo đảm Mutual Exclusion:** Tại một thời điểm chỉ có duy nhất 1 tiến trình được thực thi phương thức bên trong Monitor; các tiến trình khác phải chờ ở `Entry queue`.
- Hỗ trợ Synchronization thông qua **Condition Variables** (`Wait(c)`, `Signal(c)`, `C.queue`).

#### e) Message
- Hỗ trợ bởi HĐH cho môi trường phân tán với 2 primitive `Send` & `Receive` ở chế độ **blocking**.

---

## 5. Các bài toán đồng bộ hóa kinh điển

### 5.1. Producer – Consumer (Bounded Buffer)
- **Yêu cầu:**
  - Producer ($P$) không được ghi vào Buffer khi Buffer đầy (Rendez-vous).
  - Consumer ($C$) không được đọc từ Buffer khi Buffer rỗng (Rendez-vous).
  - $P$ và $C$ không được thao tác trên Buffer cùng lúc (Mutual Exclusion).
- **Giải pháp Semaphore:**
  - Khai báo: `mutex = 1`, `empty = BufferSize`, `full = 0`.
  - **Producer:** `produce_item` $\rightarrow$ `down(&empty)` $\rightarrow$ `down(&mutex)` $\rightarrow$ `enter_item` $\rightarrow$ `up(&mutex)` $\rightarrow$ `up(&full)`.
  - **Consumer:** `down(&full)` $\rightarrow$ `down(&mutex)` $\rightarrow$ `remove_item` $\rightarrow$ `up(&mutex)` $\rightarrow$ `up(&empty)` $\rightarrow$ `consume_item`.
  - **Cảnh báo Deadlock (Slide 55):** Nếu đảo thứ tự gọi `down(&mutex)` lên trước `down(&empty)` / `down(&full)`, khi Buffer đầy (hoặc rỗng), tiến trình giữ `mutex` sẽ bị block ở `down(&empty)` (hoặc `down(&full)`), khiến tiến trình kia không thể vào lấy/thêm item để giải phóng $\rightarrow$ **Deadlock**.
- *Ngoài ra còn có giải pháp bằng Mutex + Condition Variable, Monitor (`ProducerConsumer`), và Message (cần gửi sẵn $N$ Request ban đầu để tránh Deadlock).*

### 5.2. Readers – Writers
- **Yêu cầu:**
  - Nhiều Reader ($R$) có thể đọc CSDL đồng thời.
  - Writer ($W$) không được ghi khi có ít nhất 1 $R$ đang đọc; $R$ không được đọc khi $W$ đang ghi; tại 1 thời điểm chỉ có tối đa 1 $W$ được ghi.
- **Giải pháp Semaphore (ưu tiên Reader):**
  - Khai báo: `semaphore db = 1;` (bảo vệ CSDL), `semaphore mutex = 1;` (bảo vệ biến đếm `rc`), `int rc = 0;` (số Reader đang đọc).
  - **Reader:**
    ```c
    down(&mutex);
    if (rc == 0) down(&db);
    rc = rc + 1;
    up(&mutex);
    read_db(Database);
    down(&mutex);
    rc = rc - 1;
    if (rc == 0) up(&db);
    up(&mutex);
    ```
  - **Writer:** `down(&db); write_db(Database); up(&db);`
  - *Lưu ý:* Giải pháp này có thể làm Writer bị chờ đói (*starvation*) nếu các Reader đến liên tục. Có thể khắc phục bằng giải pháp ưu tiên Writer (Courtois) hoặc dùng Monitor (`ReaderWriter`).

### 5.3. Dining Philosophers
- **Mô tả:** 5 triết gia ngồi quanh bàn, giữa 5 đĩa có 5 chiếc nĩa; mỗi người cần 2 chiếc nĩa (trái và phải) để ăn spaghetti.
- **Yêu cầu:** Không xảy ra **Deadlock** và **Starvation**.
- **Giải pháp Semaphore ngây thơ (bị Deadlock):** Nếu mỗi triết gia đều gọi `down(fork[i]);` rồi `down(fork[(i+1) % 5]);`, khi cả 5 người cùng cầm nĩa bên trái lên cùng lúc thì tất cả sẽ chờ nĩa bên phải mãi mãi $\rightarrow$ **Deadlock**.

---

# Phần II: Giải bài tập Đồng bộ hóa

## Bài tập 1: Bài toán Tạo phân tử $H_2O$

### Đề bài
Sử dụng semaphore để đồng bộ hoạt động của một phòng thí nghiệm sử dụng nhiều tiến trình đồng hành sau để tạo các phân tử $H_2O$:
- `MakeH()`: Mỗi tiến trình `MakeH` tạo 1 nguyên tử H (`Make-Hydro();`).
- `MakeO()`: Mỗi tiến trình `MakeO` tạo 1 nguyên tử O (`Make-Oxy();`).
- `MakeWater()`: Tiến trình `MakeWater` hoạt động đồng hành với các tiến trình `MakeH`, `MakeO`, chờ có đủ 2 H và 1 O để tạo $H_2O$:
  ```c
  while (T)
      Make-Water(); // Tạo 1 phân tử H2O
  ```

---

### 1. Lời giải chuẩn

```c
// Khai báo và khởi tạo các Semaphore dùng chung
Semaphore H = 0;      // Đếm số nguyên tử H đã tạo sẵn sàng
Semaphore O = 0;      // Đếm số nguyên tử O đã tạo sẵn sàng
Semaphore mutex = 1;  // Đảm bảo độc quyền khi gom đủ 2H + 1O (an toàn nếu có nhiều tiến trình MakeWater)

MakeH() // Mỗi tiến trình MakeH tạo 1 nguyên tử H
{
    Make-Hydro();
    Up(H);
}

MakeO() // Mỗi tiến trình MakeO tạo 1 nguyên tử O
{
    Make-Oxy();
    Up(O);
}

MakeWater() /* Chờ có đủ 2 H và 1 O để tạo H2O */
{
    while (T)
    {
        Down(mutex);
        Down(H);
        Down(H);
        Down(O);
        Up(mutex);

        Make-Water(); // Tạo 1 phân tử H2O
    }
}
```

---

### 2. Giải thích chi tiết

1. **Bản chất bài toán:**
   - Đây là bài toán **Phối hợp xử lý (Rendez-vous)** kết hợp mô hình **Producer – Consumer** không giới hạn bộ đệm:
     - Các tiến trình `MakeH()` và `MakeO()` đóng vai trò **Producer**, tạo ra nguyên liệu (nguyên tử H và O).
     - Tiến trình `MakeWater()` đóng vai trò **Consumer**, chỉ được phép thực hiện `Make-Water()` khi đã có đủ **2 nguyên tử H** và **1 nguyên tử O**.

2. **Ý nghĩa và giá trị khởi tạo của các Semaphore:**
   - `Semaphore H = 0;`: Đếm số lượng nguyên tử Hydro đã được tạo xong và đang chờ kết hợp. Ban đầu chưa có nguyên tử H nào nên khởi tạo bằng `0`.
   - `Semaphore O = 0;`: Đếm số lượng nguyên tử Oxy đã được tạo xong và đang chờ kết hợp. Ban đầu chưa có nguyên tử O nào nên khởi tạo bằng `0`.
   - `Semaphore mutex = 1;`: Dùng để bảo vệ cụm thao tác lấy nguyên liệu (`Down(H); Down(H); Down(O);`).
     - Nếu hệ thống chỉ có **1 tiến trình `MakeWater()`** duy nhất, có thể lược bỏ `mutex`.
     - Tuy nhiên, nếu có **nhiều tiến trình `MakeWater()`** chạy song song, `mutex` đóng vai trò **cực kỳ quan trọng** để tránh Deadlock (xem giải thích ở mục 4).

3. **Luồng hoạt động từng bước:**
   - Khi một tiến trình `MakeH()` chạy, nó thực hiện `Make-Hydro()` để tạo ra 1 nguyên tử H, sau đó gọi `Up(H)` để tăng giá trị semaphore `H` lên 1 (báo hiệu có thêm 1 H sẵn sàng).
   - Tương tự, khi một tiến trình `MakeO()` chạy, nó thực hiện `Make-Oxy()` rồi gọi `Up(O)` để tăng giá trị semaphore `O` lên 1.
   - Ở phía `MakeWater()`, trong mỗi vòng lặp để tạo 1 phân tử $H_2O$:
     - Gọi `Down(H)` **2 lần** liên tiếp: đảm bảo tiêu thụ đủ **2 nguyên tử H**. Nếu chưa đủ 2 H, tiến trình sẽ bị block (ngủ) tại lệnh `Down(H)` cho đến khi có đủ `Up(H)` từ các tiến trình `MakeH()`.
     - Gọi `Down(O)` **1 lần**: đảm bảo tiêu thụ đủ **1 nguyên tử O**. Nếu chưa có O, tiến trình sẽ bị block tại `Down(O)` cho đến khi một tiến trình `MakeO()` gọi `Up(O)`.
     - Chỉ khi đã vượt qua cả 3 lệnh `Down` (tức đã có chắc chắn 2 H và 1 O), tiến trình mới gọi `Make-Water()`.

4. **Tại sao nên có `mutex` quanh 3 lệnh `Down`?**
   - Giả sử có 2 tiến trình `MakeWater` ($MW_1$ và $MW_2$) cùng chạy, và hiện tại chỉ có đúng 2 H và 1 O (`H = 2, O = 1`).
   - Nếu **không có `mutex`**: $MW_1$ có thể chạy `Down(H)` (còn `H = 1`), rồi bị CPU ngắt chuyển sang $MW_2$ chạy `Down(H)` (còn `H = 0`). Lúc này cả $MW_1$ và $MW_2$ đều chỉ lấy được 1 H và cùng bị block ở lệnh `Down(H)` thứ hai, dù lượng nguyên tử ban đầu đủ để tạo 1 phân tử $H_2O$.
   - Khi bọc `Down(mutex)` ... `Up(mutex)` quanh 3 lệnh `Down`, tại một thời điểm chỉ có 1 tiến trình `MakeWater` được phép lấy nguyên liệu, đảm bảo lấy trọn bộ `2H + 1O` rồi mới nhường quyền cho tiến trình `MakeWater` tiếp theo. Đồng thời, `Up(mutex)` được gọi **trước** `Make-Water()` để các tiến trình `MakeWater` khác vẫn có thể chuẩn bị tạo phân tử tiếp theo song song trong lúc phân tử hiện tại đang được `Make-Water()`.

---

## Bài tập 2: Bài toán Hãng sản xuất xe ôtô

### Đề bài
Một hãng sản xuất xe ôtô có các bộ phận hoạt động song song:
- Bộ phận sản xuất khung xe: `MakeChassis()` gọi `Produce_chassis();`
- Bộ phận sản xuất bánh xe: `MakeTire()` gọi `Produce_tire();`
- Bộ phận lắp ráp: `Assemble()` gọi `Put_4_tires_to_chassis();` sau khi có 1 khung xe và 4 bánh xe.

**Nguyên tắc đồng bộ:**  
*Tại mỗi thời điểm chỉ cho phép sản xuất ra 1 khung xe. Cần chờ có đủ 4 bánh xe để gắn vào khung xe hiện tại này trước khi sản xuất ra một khung xe mới.*

---

### 1. Lời giải chuẩn

```c
// Khai báo và khởi tạo các Semaphore dùng chung
Semaphore empty_chassis = 1; // Cho phép sản xuất tối đa 1 khung xe tại một thời điểm
Semaphore chassis = 0;       // Số khung xe đã sản xuất xong và đang chờ lắp ráp
Semaphore tire = 0;          // Số bánh xe đã sản xuất xong và đang chờ lắp ráp

MakeChassis() // Sản xuất ra một khung xe
{
    Down(empty_chassis);
    Produce_chassis();
    Up(chassis);
}

MakeTire() // Sản xuất ra một bánh xe
{
    Produce_tire();
    Up(tire);
}

Assemble() // Gắn 4 bánh xe vào khung xe
{
    Down(chassis);
    Down(tire);
    Down(tire);
    Down(tire);
    Down(tire);

    Put_4_tires_to_chassis();

    Up(empty_chassis);
}
```

---

### 2. Giải thích chi tiết

1. **Ý nghĩa và giá trị khởi tạo của các Semaphore:**
   - `Semaphore empty_chassis = 1;`: Kiểm soát số lượng khung xe được phép tồn tại/sản xuất cùng lúc. Khởi tạo bằng `1` vì ban đầu chưa có khung xe nào, cho phép bộ phận `MakeChassis()` sản xuất ngay **1 khung xe đầu tiên**.
   - `Semaphore chassis = 0;`: Báo hiệu đã có khung xe hoàn chỉnh sẵn sàng cho việc lắp ráp. Ban đầu bằng `0` vì chưa có khung xe nào được tạo.
   - `Semaphore tire = 0;`: Đếm số lượng bánh xe đã được sản xuất và sẵn sàng để lắp ráp. Ban đầu bằng `0` vì chưa có bánh xe nào được tạo.

2. **Kiểm chứng từng nguyên tắc của đề bài:**
   - **Nguyên tắc 1: *"Tại mỗi thời điểm chỉ cho phép sản xuất ra 1 khung xe."***
     - Trước khi gọi `Produce_chassis()`, tiến trình `MakeChassis()` bắt buộc phải thực hiện `Down(empty_chassis)`.
     - Vì `empty_chassis` khởi tạo bằng `1`, tiến trình đầu tiên đi qua sẽ giảm `empty_chassis` từ `1` xuống `0`.
     - Nếu có một tiến trình `MakeChassis()` thứ hai chạy song song trước khi khung xe hiện tại được lắp ráp xong, nó sẽ gặp `empty_chassis == 0` và bị block tại `Down(empty_chassis)` (`0 -> -1`). Do đó, không bao giờ có 2 khung xe được sản xuất cùng lúc hoặc chồng lên nhau.
   - **Nguyên tắc 2: *"Cần chờ có đủ 4 bánh xe để gắn vào khung xe hiện tại này trước khi sản xuất ra một khung xe mới."***
     - Trong `Assemble()`:
       - `Down(chassis);` chờ đến khi `MakeChassis()` hoàn tất `Produce_chassis()` và gọi `Up(chassis)`.
       - 4 lệnh `Down(tire);` liên tiếp (có thể viết gọn thành vòng lặp `for (int i = 0; i < 4; i++) Down(tire);`) đảm bảo phải nhận đủ **4 bánh xe** từ các lệnh `Up(tire)` của `MakeTire()`.
       - Tiếp theo, thực hiện `Put_4_tires_to_chassis();` để gắn 4 bánh xe vào khung xe hiện tại.
       - **Quan trọng:** Lệnh `Up(empty_chassis);` được đặt **sau** `Put_4_tires_to_chassis();`. Điều này bảo đảm quá trình gắn 4 bánh xe vào khung xe hiện tại phải **hoàn tất hoàn toàn** thì `empty_chassis` mới được trả lại giá trị `1` để cho phép sản xuất khung xe tiếp theo. Nếu đặt `Up(empty_chassis)` trước `Put_4_tires_to_chassis()`, khung xe mới sẽ bị sản xuất trước khi khung xe cũ kịp gắn xong bánh xe (vi phạm đề bài).

3. **Tại sao phải đặt `Down(chassis)` trước 4 lệnh `Down(tire)`?**
   - Giả sử có nhiều tiến trình `Assemble()` chạy đồng thời:
     - Vì `empty_chassis = 1`, tại mọi thời điểm chỉ có tối đa 1 khung xe được tạo ra $\rightarrow$ chỉ có tối đa **1 tiến trình `Assemble()`** vượt qua được `Down(chassis)` tại một thời điểm; các tiến trình `Assemble()` khác đều bị block tại `Down(chassis)`.
     - Do đó, `Down(chassis)` gián tiếp đóng vai trò như một **khóa độc quyền (mutex)** cho công đoạn lắp ráp: chỉ 1 `Assemble()` được phép gom đủ 4 bánh xe rồi gọi `Put_4_tires_to_chassis()` và `Up(empty_chassis)`.
   - Ngược lại, nếu đặt `Down(tire)` lên trước `Down(chassis)`, khi có 2 tiến trình `Assemble()` cùng chạy và có 4 bánh xe, mỗi tiến trình có thể lấy 2 bánh rồi cùng bị kẹt khi chờ thêm bánh xe và khung xe (gây **Deadlock**).

4. **Về bộ phận sản xuất bánh xe (`MakeTire()`):**
   - Đề bài chỉ giới hạn việc sản xuất khung xe (mỗi thời điểm 1 khung), không giới hạn số lượng bánh xe sản xuất trước. Vì vậy, `MakeTire()` có thể hoạt động song song tự do: mỗi lần tạo xong 1 bánh xe (`Produce_tire()`) thì tăng `Up(tire)`. Nếu bánh xe được sản xuất nhiều hơn 4 chiếc, các bánh dư sẽ được lưu lại qua giá trị dương của semaphore `tire` để dùng cho các khung xe kế tiếp.

5. **Minh họa một kịch bản chạy mẫu:**
   1. Khởi tạo: `empty_chassis = 1`, `chassis = 0`, `tire = 0`.
   2. `MakeChassis()` lần 1 chạy `Down(empty_chassis)` (`1 -> 0`), gọi `Produce_chassis()`, xong gọi `Up(chassis)` (`0 -> 1`).
   3. `MakeChassis()` lần 2 (nếu chạy lúc này) gọi `Down(empty_chassis)` (`0 -> -1`) $\rightarrow$ **bị block**.
   4. `Assemble()` chạy `Down(chassis)` (`1 -> 0`), sau đó chờ đủ 4 lần `Up(tire)` từ `MakeTire()`.
   5. Khi đã qua đủ 4 lệnh `Down(tire)`, `Assemble()` thực thi `Put_4_tires_to_chassis()`.
   6. Cuối cùng `Assemble()` gọi `Up(empty_chassis)` (`-1 -> 0`), đánh thức `MakeChassis()` lần 2 để bắt đầu sản xuất khung xe mới.

---

## Bài tập 3: Quy trình thu mua mía của nhà máy mía đường

### Đề bài
Quy trình thu mua mía của 1 nhà máy mía đường diễn ra theo thứ tự:
1. Xe tải chở mía đến **Trạm cân vào** để đo trọng lượng cả mía lẫn xe.
2. Xe di chuyển đến **Trạm Labo** để lấy mẫu thử đo độ đường.
3. Xe đổ mía xuống tại **Trạm sơ chế** (chỉ xử lý một lượt cho lượng mía của 5 xe mía cùng lúc).
4. Xe di chuyển đến **Trạm cân ra** để đo trọng lượng xe không (từ đó tính trọng lượng mía).
5. Xe ra khỏi nhà máy, cung cấp cho **Phòng thu mua** phiếu cân vào, phiếu cân ra và phiếu đo độ đường để tính tiền mía phải trả cho nông dân.

Quy trình được mô hình hóa bằng 5 function: `Trạm_cân_vào()`, `Trạm_Labo()`, `Trạm_sơ_chế()`, `Trạm_cân_ra()`, `Phòng_thu_mua()`.

**Yêu cầu:** Chỉ sử dụng **semaphore** (không sử dụng thêm gì khác), sửa lại 5 function trên sao cho:
- Bất chấp kết quả điều phối, việc thực thi các function phải thỏa mãn quy trình hoạt động của nhà máy và trật tự xử lý của từng bộ phận.
- Trạm sơ chế chỉ xử lý một lượt cho lượng mía của 5 xe mía cùng 1 lúc.
- Tính từ thời điểm cân vào đến thời điểm cân ra, chỉ cho phép có **tối đa 10 xe tải** được phép ở bên trong khu vực nhà máy.

---

### 1. Lời giải chuẩn

```c
// Khai báo và khởi tạo các Semaphore dùng chung
Semaphore cho_trong = 10;      // Số chỗ trống tối đa bên trong khu vực nhà máy (tối đa 10 xe)
Semaphore da_can_vao = 0;      // Số xe đã hoàn tất cân vào, chờ vào Trạm Labo
Semaphore da_do_duong = 0;     // Số xe đã đo độ đường xong, chờ vào Trạm sơ chế
Semaphore da_so_che = 0;       // Số xe đã đổ mía sơ chế xong, chờ ra Trạm cân ra
Semaphore da_can_ra = 0;       // Số xe đã cân ra xong (đủ 3 phiếu), chờ Phòng thu mua tính tiền

Semaphore mutex_can_vao = 1;   // Đảm bảo Trạm cân vào xử lý lần lượt từng xe
Semaphore mutex_labo = 1;      // Đảm bảo Trạm Labo xử lý lần lượt từng xe
Semaphore mutex_so_che = 1;    // Đảm bảo Trạm sơ chế gom đủ 5 xe mỗi lượt, tránh tranh chấp
Semaphore mutex_can_ra = 1;    // Đảm bảo Trạm cân ra xử lý lần lượt từng xe
Semaphore mutex_thu_mua = 1;   // Đảm bảo Phòng thu mua xử lý lần lượt từng xe

Trạm_cân_vào() // Xử lý cho lần lượt từng xe chở mía vào
{
    Down(cho_trong);
    Down(mutex_can_vao);
    Đo_trọng_lượng_xe_và_mía();
    Up(mutex_can_vao);
    Up(da_can_vao);
}

Trạm_Labo() // Đo độ đường trong mẫu mía của từng xe
{
    Down(da_can_vao);
    Down(mutex_labo);
    Lấy_mẫu_mía_để_đo_độ_đường();
    Up(mutex_labo);
    Up(da_do_duong);
}

Trạm_sơ_chế() // Sơ chế khi có đủ 5 xe mía
{
    Down(mutex_so_che);
    Down(da_do_duong);
    Down(da_do_duong);
    Down(da_do_duong);
    Down(da_do_duong);
    Down(da_do_duong);

    Chuyển_mía_đi_sơ_chế();

    Up(da_so_che);
    Up(da_so_che);
    Up(da_so_che);
    Up(da_so_che);
    Up(da_so_che);
    Up(mutex_so_che);
}

Trạm_cân_ra() // Xử lý cho lần lượt từng xe ra
{
    Down(da_so_che);
    Down(mutex_can_ra);
    Đo_trọng_lượng_xe();
    Up(mutex_can_ra);
    Up(cho_trong);
    Up(da_can_ra);
}

Phòng_thu_mua()
{
    Down(da_can_ra);
    Down(mutex_thu_mua);
    Tính_tiền_mía_phải_trả();
    Up(mutex_thu_mua);
}
```

---

### 2. Giải thích chi tiết

1. **Ý nghĩa các Semaphore sử dụng:**
   - **Nhóm semaphore phối hợp theo dây chuyền (Rendez-vous):**
     - `da_can_vao = 0`, `da_do_duong = 0`, `da_so_che = 0`, `da_can_ra = 0`: Đóng vai trò "tín hiệu chuyển trạm" theo đúng thứ tự:
       $$\text{Trạm cân vào} \xrightarrow{\text{da\_can\_vao}} \text{Trạm Labo} \xrightarrow{\text{da\_do\_duong}} \text{Trạm sơ chế} \xrightarrow{\text{da\_so\_che}} \text{Trạm cân ra} \xrightarrow{\text{da\_can\_ra}} \text{Phòng thu mua}$$
     - Ban đầu chưa có xe nào đi qua các trạm nên tất cả đều khởi tạo bằng `0`.
   - **Semaphore giới hạn sức chứa nhà máy:**
     - `cho_trong = 10`: Theo đề bài, tính từ thời điểm cân vào đến thời điểm cân ra, bên trong khu vực nhà máy chỉ được chứa tối đa **10 xe**.
     - Trước khi xe thực hiện `Đo_trọng_lượng_xe_và_mía()`, phải gọi `Down(cho_trong)` để chiếm 1 chỗ.
     - Chỉ sau khi xe hoàn tất `Đo_trọng_lượng_xe()` tại `Trạm_cân_ra()` (tức chuẩn bị rời khỏi khu vực nhà máy), mới gọi `Up(cho_trong)` để nhường chỗ cho xe mới vào.
   - **Nhóm semaphore độc quyền truy xuất (Mutual Exclusion):**
     - `mutex_can_vao = 1`, `mutex_can_ra = 1`: Đảm bảo đúng mô tả *"xử lý cho lần lượt từng xe"* tại trạm cân vào và trạm cân ra (không có 2 xe cân cùng lúc).
     - `mutex_labo = 1`, `mutex_thu_mua = 1`: Đảm bảo tính tuần tự khi có nhiều tiến trình cùng gọi `Trạm_Labo()` hoặc `Phòng_thu_mua()`.
     - `mutex_so_che = 1`: Đảm bảo tại một thời điểm chỉ có 1 tiến trình `Trạm_sơ_chế()` gom đủ 5 xe, tránh tình trạng nhiều tiến trình `Trạm_sơ_chế()` tranh nhau lấy lẻ (ví dụ tiến trình A lấy 3 xe, tiến trình B lấy 2 xe rồi cả hai cùng bị block gây **Deadlock**).

2. **Giải thích cơ chế gom 5 xe tại `Trạm_sơ_chế()`:**
   - Đề bài yêu cầu *chỉ sử dụng semaphore (không sử dụng thêm biến đếm hay cấu trúc khác)* và *xử lý một lượt cho lượng mía của 5 xe mía cùng 1 lúc*.
   - Vì vậy, `Trạm_sơ_chế()` thực hiện gọi `Down(da_do_duong)` **5 lần liên tiếp**. Tiến trình sẽ phải chờ cho đến khi có đủ 5 xe hoàn thành ở `Trạm_Labo()` (tức 5 lần `Up(da_do_duong)`).
   - Khi đã gom đủ 5 xe, trạm mới thực thi `Chuyển_mía_đi_sơ_chế();`.
   - Sau khi đổ mía và sơ chế xong cho mẻ 5 xe đó, trạm gọi `Up(da_so_che)` **5 lần liên tiếp** để giải phóng cả 5 xe di chuyển sang `Trạm_cân_ra()`.

3. **Kiểm chứng không xảy ra Deadlock:**
   - **Sức chứa nhà máy ($10$) và kích thước mẻ sơ chế ($5$):** Vì sức chứa tối đa của nhà máy là $10 \ge 5$, ngay cả khi 10 xe vào đầy nhà máy (`cho_trong = 0`), toàn bộ 10 xe này đều đi qua được `Trạm_Labo()` để tạo ra `da_do_duong = 10`. Lượng xe này đủ để `Trạm_sơ_chế()` xử lý thành công (thậm chí đủ 2 mẻ 5 xe) và đẩy sang `Trạm_cân_ra()`, từ đó gọi `Up(cho_trong)` giải phóng chỗ trong nhà máy. Do đó không bao giờ xảy ra bế tắc do thiếu xe vào mẻ.
   - **Thứ tự `Down` trong `Trạm_cân_vào()`:** `Down(cho_trong)` được đặt **trước** `Down(mutex_can_vao)`. Nếu đặt ngược lại, khi nhà máy đã đủ 10 xe (`cho_trong == 0`), xe thứ 11 sẽ giữ `mutex_can_vao` trong khi chờ `cho_trong`; tuy không khóa `Trạm_cân_ra()` nhưng làm trạm cân vào bị giữ khóa không cần thiết. Đặt `Down(cho_trong)` ở ngoài là đúng chuẩn *Producer – Consumer*.
   - **Điều kiện tính tiền ở `Phòng_thu_mua()`:** `Up(da_can_ra)` chỉ được gọi sau khi xe đã đi qua tuần tự `Trạm_cân_vào()` (có phiếu cân vào) $\rightarrow$ `Trạm_Labo()` (có phiếu đo độ đường) $\rightarrow$ `Trạm_sơ_chế()` $\rightarrow$ `Trạm_cân_ra()` (có phiếu cân ra). Do đó, khi `Phòng_thu_mua()` vượt qua `Down(da_can_ra)`, chắc chắn xe đã có đầy đủ 3 loại phiếu hợp lệ để `Tính_tiền_mía_phải_trả()`.

---

## Bài tập 4: Bài toán Qua sông (Nhân viên Microsoft & Linux Hacker)

### Đề bài
Các nhân viên Microsoft (`Employee`) và Linux hacker (`Hacker`) cùng sử dụng một bến sông với các thuyền chở **đúng 4 người** mới được khởi hành. Để đảm bảo an toàn, cần tuân thủ các quy tắc:
- Không chấp nhận **3 Employee + 1 Hacker** trên cùng một thuyền.
- Không chấp nhận **3 Hacker + 1 Employee** trên cùng một thuyền.
- Các trường hợp kết hợp hợp lệ: **4 Hacker**, **4 Employee**, hoặc **2 Hacker + 2 Employee**.
- Thuyền chỉ khởi hành khi đã có đủ 4 hành khách; người đã lên thuyền khi chưa đầy phải chờ đến khi người thứ 4 xuống thuyền mới cùng qua sông. *(Xem như luôn có sẵn thuyền cho các nhóm hợp lệ).*

Hoạt động của mỗi tiến trình:
```c
Hacker() {
    RuntoRiver();    // Đi đến bờ sông
    HackerArrives(); // Kiểm tra điều kiện xuống thuyền
    CrossRiver();    // Khởi hành qua sông
}

Employee() {
    RuntoRiver();      // Đi đến bờ sông
    EmployeeArrives(); // Kiểm tra điều kiện xuống thuyền
    CrossRiver();      // Khởi hành qua sông
}
```
**Yêu cầu:** Xây dựng 2 thủ tục `HackerArrives()` và `EmployeeArrives()`.

---

### 1. Lời giải chuẩn

```c
// Khai báo các biến đếm và Semaphore dùng chung
int hackers = 0;               // Số Linux hacker đang chờ tại bến sông
int employees = 0;             // Số nhân viên Microsoft đang chờ tại bến sông

Semaphore mutex = 1;           // Đảm bảo độc quyền truy xuất biến hackers, employees
Semaphore hackerQueue = 0;     // Hàng đợi các Hacker đang chờ đủ nhóm 4 hợp lệ
Semaphore employeeQueue = 0;   // Hàng đợi các Employee đang chờ đủ nhóm 4 hợp lệ

HackerArrives()
{
    Down(mutex);
    hackers++;

    if (hackers == 4)
    {
        // Đủ bộ 4 Hacker -> đánh thức 3 Hacker đang chờ, cùng bản thân qua sông
        Up(hackerQueue);
        Up(hackerQueue);
        Up(hackerQueue);
        hackers -= 4;
        Up(mutex);
    }
    else if (hackers == 2 && employees >= 2)
    {
        // Đủ bộ 2 Hacker + 2 Employee -> đánh thức 1 Hacker & 2 Employee đang chờ
        Up(hackerQueue);
        Up(employeeQueue);
        Up(employeeQueue);
        hackers -= 2;
        employees -= 2;
        Up(mutex);
    }
    else
    {
        // Chưa tạo được nhóm 4 hợp lệ -> trả mutex và chờ
        Up(mutex);
        Down(hackerQueue);
    }
}

EmployeeArrives()
{
    Down(mutex);
    employees++;

    if (employees == 4)
    {
        // Đủ bộ 4 Employee -> đánh thức 3 Employee đang chờ, cùng bản thân qua sông
        Up(employeeQueue);
        Up(employeeQueue);
        Up(employeeQueue);
        employees -= 4;
        Up(mutex);
    }
    else if (employees == 2 && hackers >= 2)
    {
        // Đủ bộ 2 Employee + 2 Hacker -> đánh thức 1 Employee & 2 Hacker đang chờ
        Up(employeeQueue);
        Up(hackerQueue);
        Up(hackerQueue);
        employees -= 2;
        hackers -= 2;
        Up(mutex);
    }
    else
    {
        // Chưa tạo được nhóm 4 hợp lệ -> trả mutex và chờ
        Up(mutex);
        Down(employeeQueue);
    }
}
```

---

### 2. Giải thích chi tiết

1. **Ý nghĩa các biến và Semaphore:**
   - `hackers = 0`, `employees = 0`: Lưu số lượng Hacker và Employee hiện đang chờ tại bến sông chưa được ghép thành nhóm 4 hợp lệ.
   - `Semaphore mutex = 1`: Bảo vệ miền găng (truy cập và cập nhật 2 biến đếm `hackers`, `employees` cũng như kiểm tra điều kiện ghép nhóm), tránh *Race Condition* khi nhiều người đến bến cùng lúc.
   - `Semaphore hackerQueue = 0`, `Semaphore employeeQueue = 0`: Hàng đợi riêng cho từng nhóm đối tượng. Người đến trước khi chưa đủ bộ 4 hợp lệ sẽ gọi `Down(...)` để ngủ trên hàng đợi tương ứng, chờ người thứ 4 của nhóm đánh thức.

2. **Cơ chế ghép nhóm 4 người hợp lệ (người thứ 4 làm "trưởng nhóm"):**
   - Mỗi khi một **Hacker** đến (`HackerArrives()`), tăng `hackers++` và chỉ có đúng **2 trường hợp** giúp người này hoàn thành ngay một nhóm 4 hợp lệ:
     - **Trường hợp 1 (`hackers == 4`):** Đã có 3 Hacker đang chờ trên `hackerQueue` cộng thêm bản thân là đủ **4 Hacker**. Tiến trình này gọi `Up(hackerQueue)` **3 lần** để đánh thức 3 Hacker kia, giảm `hackers -= 4`, trả `mutex` và thoát khỏi `HackerArrives()` để cả 4 người cùng chạy `CrossRiver()`.
     - **Trường hợp 2 (`hackers == 2 && employees >= 2`):** Đã có 1 Hacker đang chờ và ít nhất 2 Employee đang chờ, cộng thêm bản thân là đủ **2 Hacker + 2 Employee**. Tiến trình này gọi `Up(hackerQueue)` **1 lần** và `Up(employeeQueue)` **2 lần**, giảm `hackers -= 2`, `employees -= 2`, trả `mutex` và cùng 3 người kia qua sông.
     - **Các trường hợp còn lại (`else`):** Chưa thể ghép bộ 4 hợp lệ (ví dụ: 1H+0E, 2H+1E, 3H+1E,...). Tiến trình bắt buộc phải gọi `Up(mutex)` **trước** rồi mới gọi `Down(hackerQueue)` để ngủ chờ (nếu không trả `mutex` trước khi ngủ sẽ gây **Deadlock** vì không ai khác vào kiểm tra điều kiện được nữa).
   - Thủ tục `EmployeeArrives()` hoạt động hoàn toàn đối xứng.

3. **Tại sao phải kiểm tra `employees >= 2` (và `hackers >= 2`) thay vì `== 2`?**
   - Xét tình huống tại bến sông đang có **3 Hacker và 1 Employee** (`hackers = 3, employees = 1`). Nhóm 4 người này **không hợp lệ** (vi phạm luật cấm 3–1) nên cả 4 đều đang chờ.
   - Lúc này, một **Employee thứ 2** đến: `employees` tăng từ `1` lên `2`, còn `hackers` đang bằng **`3`** (chứ không phải `2`!).
   - Nhờ điều kiện `employees == 2 && hackers >= 2`, Employee thứ 2 lập tức ghép thành công bộ **2 Employee + 2 Hacker**, đánh thức 1 Employee và 2 Hacker, sau đó cập nhật `employees -= 2` (về `0`) và `hackers -= 2` (còn `1` Hacker tiếp tục chờ cho chuyến sau).
   - Nếu viết nhầm thành `hackers == 2`, tình huống `(3H, 2E)` sẽ bị bỏ sót không ghép được nhóm!

4. **Kiểm chứng tính đúng đắn & không Deadlock:**
   - **Bất biến (Invariant):** Sau mỗi lần `Up(mutex)`, số người chờ luôn thỏa $0 \le \text{hackers} \le 3$, $0 \le \text{employees} \le 3$, và không bao giờ đồng thời có $\text{hackers} \ge 2$ lẫn $\text{employees} \ge 2$.
   - Do đó, tổng số người tối đa có thể bị kẹt chờ ở bến sông là $3 + 1 = 4$ người (trường hợp 3H+1E hoặc 1H+3E). Ngay khi có người thứ 5 bất kỳ đến (dù là Hacker hay Employee), chắc chắn sẽ thỏa một trong hai nhánh `== 4` hoặc `2 + 2` để lập tức cho 4 người qua sông $\rightarrow$ **không bao giờ xảy ra Deadlock**, và **không bao giờ có thuyền 3–1** hay thuyền thiếu 4 người khởi hành.



