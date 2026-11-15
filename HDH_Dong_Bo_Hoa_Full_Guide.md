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
