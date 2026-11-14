# Hệ điều hành: Quản lý Bộ nhớ & Bộ nhớ ảo (Memory Management & Virtual Memory)

Tài liệu này được tổng hợp dựa trên slide bài giảng **Bài 04: Quản lý Bộ nhớ - Bộ nhớ ảo** (`Bai04_Quan_ly_bo_nho.pdf` - Khoa CNTT, ĐH KHTN TP.HCM) và kèm theo phần **Giải bài tập** (`Baitap_QLBN.pdf`) gồm hai phần: **Lời giải chuẩn** và **Giải thích chi tiết**.

---

## PHẦN I: TỔNG HỢP KIẾN THỨC QUẢN LÝ BỘ NHỚ & BỘ NHỚ ẢO

### 1. Tổng quan về quản lý bộ nhớ

#### 1.1. Vấn đề bộ nhớ của tiến trình
- Khi lập trình và biên dịch:
  - Từ mã nguồn (`A.C`, `B.C`), trình biên dịch tạo ra các file đối tượng (`A.O`, `B.O`) chứa địa chỉ tương đối/cục bộ.
  - Trình liên kết (Linker) kết hợp các file đối tượng thành file thực thi (`Test.exe`) với **Không gian địa chỉ (Address Space)** gồm các **địa chỉ logic (logical / symbolic / private / virtual address)**.
  - Trình nạp (Loader) nạp chương trình vào RAM để tạo thành tiến trình nằm trong **Không gian vật lý (Physical Space)** với các **địa chỉ vật lý (physical address)**.
- CPU chỉ có thể truy xuất trực tiếp **Bộ nhớ chính (Main Memory - RAM)**.

#### 1.2. Nhu cầu bộ nhớ của một tiến trình
Một tiến trình trong bộ nhớ được tổ chức gồm các thành phần chính (từ địa chỉ thấp đến địa chỉ cao):
1. **System data segment (PCB - Process Control Block):** chứa con trỏ phân đoạn, PID, con trỏ chương trình (PC) và con trỏ ngăn xếp (SP)...
2. **Code segment:** chứa mã lệnh đọc từ file chương trình khi `exec`; thường ở chế độ chỉ đọc (read-only) và có thể chia sẻ (shared).
3. **Data segment:**
   - Biến toàn cục đã khởi tạo (initialized global variables).
   - Biến toàn cục chưa khởi tạo (uninitialized global variables).
   - **Heap:** vùng nhớ cấp phát động (ví dụ `malloc`), **tăng dần về phía địa chỉ cao**.
4. **Stack segment:** chứa biến cục bộ trong hàm, trạng thái thanh ghi được lưu (ví dụ `EIP` của hàm gọi), **tăng dần về phía địa chỉ thấp**. (Có thể có thêm các stack riêng cho các thread).

#### 1.3. Các bài toán của quản lý bộ nhớ
- **Cấp phát bộ nhớ:** Làm sao phân bổ RAM giới hạn cho $N$ tiến trình? Đảm bảo bảo vệ, chia sẻ, xử lý khi tiến trình thay đổi kích thước hoặc kích thước tiến trình lớn hơn RAM?
- **Chuyển đổi địa chỉ (Address Binding):** Thời điểm chuyển đổi, công thức chuyển đổi, sự phụ thuộc vào mô hình tổ chức RAM, hỗ trợ phần cứng, và xử lý khi tiến trình thay đổi vị trí trong RAM.

---

### 2. Chuyển đổi địa chỉ (Address Binding)

Có 3 thời điểm kết buộc địa chỉ logic thành địa chỉ vật lý:

| Thời điểm | Đặc điểm | Khả năng tái định vị |
| :--- | :--- | :--- |
| **Compile & Link-time** | Phát sinh trực tiếp địa chỉ vật lý; phải biết trước vị trí nạp chương trình. | Không. Nếu vị trí nạp thay đổi, phải **biên dịch lại**. |
| **Load-time** | Khi biên dịch chỉ phát sinh địa chỉ cục bộ. Khi nạp, biết vị trí bắt đầu (`base`) thì cộng thêm để ra địa chỉ vật lý. | Không linh hoạt sau khi nạp. Nếu dời vị trí, phải **tái nạp (reload)**. |
| **Execution-time** | Trì hoãn việc kết buộc địa chỉ tuyệt đối đến tận lúc thi hành. | **Có.** Có thể di chuyển tiến trình trong RAM khi đang chạy. Cần phần cứng **MMU (Memory Management Unit)** trong CPU hỗ trợ kiểm tra hợp lệ và ánh xạ địa chỉ. |

---

### 3. Mô hình tổ chức bộ nhớ

#### 3.1. Cấp phát liên tục (Contiguous Allocation)
- **Nguyên tắc:** Toàn bộ chương trình phải được nạp vào một vùng nhớ liên tục, đủ lớn trong RAM.
- **Không gian địa chỉ:** liên tục.

##### a) Fixed Partitioning (Phân vùng cố định)
- RAM được chia trước thành các partition (kích thước **bằng nhau** hoặc **khác nhau**). Mỗi tiến trình nạp vào 1 partition.
- **Chiến lược cấp phát cho partition kích thước khác nhau:**
  - *Nhiều hàng đợi (mỗi partition 1 hàng đợi):* cấp partition nhỏ nhất đủ chứa tiến trình. Nhược điểm: phân bố không đều, có tiến trình phải chờ dù partition lớn hơn đang trống.
  - *Một hàng đợi chung:* chọn partition tự do nhỏ nhất đủ chứa tiến trình; cần cấu trúc dữ liệu theo dõi các partition tự do.
- **Nhận xét:**
  - Bị **Phân mảnh nội (Internal Fragmentation):** phần bộ nhớ dư bên trong partition khi kích thước chương trình nhỏ hơn kích thước partition.
  - Mức độ đa chương bị giới hạn bởi số lượng partition.

##### b) Dynamic Partitioning (Phân vùng động)
- RAM không chia trước; các partition hình thành động đúng bằng kích thước tiến trình yêu cầu $\implies$ **không còn Internal Fragmentation**.
- Bị **Phân mảnh ngoại (External Fragmentation):** khi tiến trình kết thúc để lại lỗ trống (hole), tiến trình sau không lấp đầy hết hoặc tổng vùng trống đủ nhưng không liên tục.
- **Quản lý vùng nhớ:** Dùng **Bitmap** (mỗi bit ứng với 1 đơn vị cấp phát: `0` là trống, `1` là đang dùng) hoặc **Danh sách liên kết (Linked List)** các node `P` (Process) và `H` (Hole) với địa chỉ bắt đầu và độ dài.
- **Thuật toán lựa chọn vùng trống (Dynamic Allocation Problem):**
  - **First-fit:** chọn vùng trống đầu tiên đủ lớn.
  - **Best-fit:** chọn vùng trống nhỏ nhất đủ lớn.
  - **Worst-fit:** chọn vùng trống lớn nhất đủ lớn.
- **Giải pháp chống phân mảnh ngoại:** **Memory Compaction (Dồn bộ nhớ / Garbage Collection)** dồn các vùng đang dùng về một phía để gộp các lỗ trống lại, nhưng **chi phí thực hiện rất cao**.

##### c) Cơ chế chuyển đổi địa chỉ trong cấp phát liên tục
- **Linker – Loader (Load-time):** $\text{Địa chỉ vật lý} = \text{Địa chỉ logic} + \text{base}$. Không cần phần cứng, không hỗ trợ bảo vệ, không tái định vị sau nạp.
- **Base & Bound (Execution-time):** Dùng 2 thanh ghi `Base` và `Bound` (MMU hỗ trợ). Địa chỉ hợp lệ nằm trong `[Base, Bound]`, $\text{Địa chỉ vật lý} = \text{Địa chỉ logic} + \text{Base register}$. Hỗ trợ bảo vệ và tái định vị.

---

#### 3.2. Cấp phát không liên tục (Non-contiguous Allocation)
Cho phép nạp các phần của tiến trình vào nhiều vùng nhớ không liên tục trong RAM.

##### a) Segmentation (Phân đoạn)
- **Tổ chức:** Không gian địa chỉ chia theo ngữ nghĩa thành các **segment** (code, data, stack, heap...); không gian vật lý tổ chức thành các **dynamic partition**. Mỗi segment được nạp vào 1 partition liên tục, nhưng các segment của cùng 1 tiến trình có thể nằm ở các partition không kề nhau.
- **Địa chỉ logic:** $\langle s, d \rangle$ (`<segment-number, offset>`).
- **Chuyển đổi địa chỉ (MMU thực hiện lúc chạy):**
  - Tra **Segment Table** (mỗi tiến trình có 1 bảng; lưu bằng `STBR` - Segment-table base register và `STLR` - Segment-table length register, hoặc trong cache nếu nhỏ).
  - Mỗi entry gồm `base` (địa chỉ vật lý bắt đầu) và `limit` (kích thước segment).
  - Kiểm tra hợp lệ: nếu $d < \text{limit}$ thì $\text{Địa chỉ vật lý} = \text{base} + d$; ngược lại báo lỗi (`fault`).
- **Nhận xét:**
  - Tận dụng bộ nhớ tốt hơn, hỗ trợ tái định vị từng segment.
  - **Hỗ trợ bảo vệ và chia sẻ ở mức module** (do mỗi segment gắn với ngữ nghĩa cụ thể như code chỉ đọc, data đọc/ghi).
  - Vẫn chịu **External Fragmentation** vì bản chất vẫn cấp phát dynamic partition cho từng segment.

##### b) Paging (Phân trang)
- **Tổ chức:**
  - Không gian địa chỉ chia thành các **page** có kích thước bằng nhau (không quan tâm ngữ nghĩa).
  - Không gian vật lý chia thành các **frame** (fixed partition) có kích thước bằng nhau: $\text{page size} = \text{frame size} = 2^n$.
  - Tiến trình có $N$ page cần $N$ frame tự do bất kỳ (không cần liên tục).
- **Công thức kích thước & địa chỉ:**
  - Hệ thống dùng $m$ bit địa chỉ logic $\implies$ Kích thước KGĐC $= 2^m$.
  - Kích thước trang $= 2^n \implies$ Số trang trong KGĐC $= \frac{2^m}{2^n} = 2^{m-n}$ ($=$ số entry trong Page Table).
  - Địa chỉ logic gồm 2 phần: `p` ($m - n$ bit đầu: số hiệu trang) và `d` ($n$ bit cuối: offset).
- **Chuyển đổi địa chỉ:** $\langle p, d \rangle \longrightarrow \langle f, d \rangle$ thông qua **Page Table** (lưu trong RAM, trỏ bởi `PTBR`, `PTLR`).
- **Nhận xét:**
  - **Loại bỏ hoàn toàn** Dynamic Allocation và **External Fragmentation**.
  - "Trong suốt" với lập trình viên.
  - Còn **Internal Fragmentation** ở trang cuối cùng (nếu tiến trình không lấp đầy trang).
  - **Bảo vệ & chia sẻ:** áp dụng ở **mức page** (không phân biệt ngữ nghĩa bên trong page; nếu 1 page chứa cả code và data thì chia sẻ page đó sẽ chia sẻ cả hai).
  - **Vấn đề của Page Table phẳng:** Kích thước Page Table quá lớn (ví dụ địa chỉ 32-bit, page 4KB $\implies 2^{20}$ entries) và mỗi truy cập dữ liệu tốn **2 lần truy xuất RAM** (1 lần đọc Page Table, 1 lần đọc data).

##### c) Tối ưu Page Table (Tiết kiệm không gian & Tăng tốc độ)
1. **Bảng trang đa cấp (Multi-level Page Table):**
   - Phân trang cho chính Page Table; chỉ giữ thường trực bảng trang cấp 1 trong RAM, nạp bảng trang cấp 2 khi cần; loại bỏ các bảng trang của miền địa chỉ không sử dụng.
   - Ví dụ 32-bit, page 4KB (12 bit offset): 20 bit `page number` chia thành `p1` (10 bit) + `p2` (10 bit) + `d` (12 bit).
2. **Bảng trang nghịch đảo (Inverted Page Table - IPT):**
   - Chỉ dùng **1 bảng duy nhất cho toàn hệ thống**, số phần tử bằng số **frame** vật lý.
   - Mỗi entry lưu `<idp, page>` cho biết frame thứ `i` đang chứa trang `page` của tiến trình `idp`. Địa chỉ ảo có dạng `<idp, p, d>`, tìm khớp trong IPT để ra frame `i` $\implies \langle i, d \rangle$.
3. **TLB (Translation Lookaside Buffer):**
   - Vùng nhớ cache tốc độ cao trong CPU lưu tạm một phần Page Table (thường $\le 64$ phần tử), mỗi entry chứa `<p, f>`.
   - Khi chuyển đổi địa chỉ: tra **TLB trước**; nếu **TLB hit** thì lấy ngay frame `f` mà không cần đọc Page Table trong RAM; nếu **TLB miss** mới tra Page Table trong RAM (và cập nhật lại TLB).

---

#### 3.3. Đánh giá các mô hình chuyển đổi địa chỉ (TEA - Time Effective Access)
Ký hiệu:
- $t_m$: thời gian truy xuất bộ nhớ chính (RAM).
- $t_c$: thời gian truy xuất cache / thanh ghi / TLB.
- $\text{hit-ratio}$ (ký hiệu $\alpha$): tỉ lệ tìm thấy số hiệu trang `p` trong TLB.

Công thức tổng quát: $\text{TEA} = \text{Thời gian chuyển đổi địa chỉ} + \text{Thời gian truy xuất dữ liệu}$

- **Linker-Loader:** $\text{TEA} = t_m$
- **Base & Bound:** $\text{TEA} = (t_c + t_c) + t_m$
- **Segmentation (ST trong cache):** $\text{TEA} = t_c + t_m$
- **Paging (không dùng TLB, PT trong RAM):** $\text{TEA} = t_m + t_m = 2t_m$
- **Paging (có dùng TLB):**
  $$\text{TEA} = \text{hit-ratio} \times (t_c + t_m) + (1 - \text{hit-ratio}) \times (t_c + t_m + t_m)$$

---

### 4. Bộ nhớ ảo (Virtual Memory)

#### 4.1. Ý tưởng & Cơ chế
- **Vấn đề:** Tiến trình có thể lớn hơn RAM trống, và tại một thời điểm CPU chỉ thực thi một số ít chỉ thị.
- **Giải pháp Bộ nhớ ảo:**
  - Tách biệt hoàn toàn **KGĐC** ($2^m$ cho mỗi tiến trình) và **KGVL** (RAM chung).
  - Cho phép **nạp và thi hành từng phần** của tiến trình; các phần chưa cần đến được lưu trên **Bộ nhớ phụ (đĩa / backing store)** và được hoán đổi vào/ra (**swapping**) khi cần.
- **Virtual Memory với Paging:**
  - Mỗi phần tử trong Page Table có thêm **Present / Valid bit** (`1` hoặc `V`: trang đang ở trong RAM; `0` hoặc `I`: trang chưa nạp / đang ở trên đĩa).

#### 4.2. Quy trình xử lý lỗi trang (Page Fault)
Khi CPU truy xuất trang có bit `Present = 0` (`Valid = I`), phần cứng phát sinh ngắt **Page Fault** và HĐH xử lý theo **6 bước**:
1. Kiểm tra truy xuất đến bộ nhớ là hợp lệ hay bất hợp lệ (dựa vào bảng trang / vùng địa chỉ tiến trình).
2. Nếu truy xuất **bất hợp lệ**: kết thúc tiến trình. Ngược lại: sang bước 3.
3. Tìm vị trí chứa trang muốn truy xuất trên đĩa.
4. Tìm một khung trang trống trong bộ nhớ chính (RAM):
   - *a. Nếu tìm thấy:* sang bước 5.
   - *b. Nếu không còn khung trang trống:* chọn một **khung trang nạn nhân (victim)** để **swap out** ra đĩa, cập nhật bảng trang tương ứng (đặt bit `Present = 0` / `I`), rồi sang bước 5.
5. Chuyển trang muốn truy xuất từ đĩa vào khung trang trống đã chọn (hoặc vừa làm trống); cập nhật bảng trang (ghi số frame, đặt `Present = 1` / `V`) và bảng khung trang.
6. Tái kích hoạt tiến trình người sử dụng (thực thi lại lệnh vừa gây lỗi trang).

#### 4.3. Các thuật toán thay thế trang (Page Replacement)
Mục tiêu: chọn trang nạn nhân sao cho **tần suất lỗi trang thấp nhất**.

1. **FIFO (First-In, First-Out):**
   - Nạn nhân là trang "già" nhất (nạp vào RAM lâu nhất).
   - Cài đặt bằng hàng đợi FIFO. Đơn giản nhưng không xét đến tần suất sử dụng; có thể gặp **nghịch lý Belady** (cấp càng nhiều frame lại càng nhiều lỗi trang).
2. **Optimal (Tối ưu):**
   - Nạn nhân là trang **lâu được sử dụng đến nhất trong tương lai**.
   - Đảm bảo số lỗi trang thấp nhất, nhưng **không khả thi** trong thực tế vì không thể biết trước tương lai (chỉ dùng làm chuẩn đối chiếu).
3. **LRU (Least Recently Used):**
   - Nạn nhân là trang **lâu nhất chưa được sử dụng đến trong quá khứ**.
   - Xấp xỉ tốt thuật toán Optimal.
   - **Cách cài đặt:**
     - *Hỗ trợ phần cứng (Counter):* mỗi lần truy xuất tăng counter của CPU và ghi vào trường `reference time` của trang; khi thay thế chọn trang có `reference time` nhỏ nhất.
     - *Ngăn xếp (Stack):* mỗi lần truy xuất trang, đưa số hiệu trang lên đỉnh stack; đáy stack là trang LRU.
     - *Các bit lịch sử (Aging / History bits):* dùng bit `R` (Reference) được phần cứng bật `1` khi truy cập và reset `0` định kỳ; sau mỗi chu kỳ dịch phải thanh ghi `N` bit history và chép bit `R` vào bit cao nhất.
4. **Second-chance (Clock model):**
   - Kết hợp FIFO với 1 bit `R` (reference). Kiểm tra trang đầu FIFO: nếu `R = 0` thì chọn làm nạn nhân; nếu `R = 1` thì đặt `R = 0`, cập nhật thời điểm vào cuối danh sách (cho cơ hội thứ 2) và xét trang tiếp theo.
5. **NRU (Not Recently Used):**
   - Dùng 2 bit `R` (Reference) và `M` (Modify), chia thành 4 lớp ưu tiên thay thế (từ ưu tiên cao nhất đến thấp nhất):
     - Lớp `(R=0, M=0)`: không truy xuất, không sửa đổi $\to$ ưu tiên thay thế cao nhất.
     - Lớp `(R=0, M=1)`: không truy xuất gần đây, nhưng đã sửa đổi.
     - Lớp `(R=1, M=0)`: có truy xuất gần đây, không sửa đổi.
     - Lớp `(R=1, M=1)`: có truy xuất gần đây, đã sửa đổi $\to$ ưu tiên thấp nhất.
6. **Working Set (Denning, 1968) & WSClock:**
   - **Working Set (WS):** tập hợp các trang được tiến trình truy xuất trong $w$ lần truy xuất gần nhất (hoặc trong khoảng thời gian $\tau$).
   - **WSClock:** kết hợp mô hình đồng hồ (Clock) với thông tin `Time of last use` và bit `R` để tìm nhanh trang ngoài Working Set cần thay thế.

#### 4.4. Chiến lược cấp phát frame & Hiện tượng Thrashing
- **Số frame cấp cho mỗi tiến trình** ($m$ frame, $n$ tiến trình):
  - *Cấp phát công bằng (Equal allocation):* $\frac{m}{n}$ frame cho mỗi tiến trình.
  - *Cấp phát theo tỷ lệ (Proportional allocation):* $\frac{s_i}{\sum s_k} \times m$, với $s_i$ là kích thước bộ nhớ ảo của tiến trình $P_i$.
- **Phạm vi thay thế khi lỗi trang:**
  - *Cục bộ (Local):* chỉ chọn nạn nhân trong các frame thuộc tiến trình gây lỗi $\implies$ số frame của tiến trình giữ nguyên.
  - *Toàn cục (Global):* chọn nạn nhân bất kỳ (kể cả của tiến trình khác) $\implies$ số frame có thể thay đổi, dễ gây lỗi trang lan truyền.
- **Thrashing (Trì trệ hệ thống):**
  - Xảy ra khi quá nhiều tiến trình cùng chạy ($\sum \text{size of working sets} > \text{total memory size}$).
  - Hậu quả: tiến trình liên tục bị lỗi trang chỉ sau vài lệnh, I/O hoạt động 100% để swap in/out, CPU rảnh, hệ thống gần như ngừng trệ.

---

### 5. Tổ chức bộ nhớ Intel x86 (Kết hợp Segmentation & Paging)
- **Bước 1 (Segmentation):** Địa chỉ logic gồm `(Selector, Offset)`. Dùng `Selector` tra bảng mô tả (`Descriptor Table` qua `GDTR`/`LDTR`) để lấy `Segment Descriptor`, cộng `Base` với `Offset` tạo thành **Địa chỉ tuyến tính (Linear Address)** 32-bit.
- **Bước 2 (Paging 2 cấp):** Linear Address 32-bit chia thành `Directory` (10 bit) | `Table` (10 bit) | `Offset` (12 bit). Dùng thanh ghi `CR3` trỏ tới `Page Directory`, tra lần lượt qua `Page Table` để tìm `Page Frame` và ghép với `Offset` tạo thành **Địa chỉ vật lý (Physical Address)**.

---

## PHẦN II: GIẢI BÀI TẬP (`Baitap_QLBN.pdf`)

### Phần 1: Trình bày lời giải chuẩn

#### Bài tập 1

**1. Số khung trang và số lượng trang trong không gian địa chỉ:**
- Dung lượng RAM $= 512\text{ MB} = 512 \times 2^{20}\text{ byte} = 2^{29}\text{ byte}$.
- Kích thước mỗi trang (và khung trang) $= 4096\text{ byte} = 2^{12}\text{ byte}$.
- **Số khung trang của hệ thống:** $\dfrac{2^{29}}{2^{12}} = 2^{17} = 131.072$ khung trang.
- Không gian địa chỉ logic $32\text{ bit} \implies$ Kích thước KGĐC $= 2^{32}\text{ byte}$.
- **Số lượng trang trong không gian địa chỉ của một tiến trình:** $\dfrac{2^{32}}{2^{12}} = 2^{20} = 1.048.576$ trang.

**2. Diễn giải tuần tự các truy xuất bộ nhớ:**
Gọi cặp $\langle p, d \rangle$ là `(số hiệu trang, offset)` với $p = \lfloor \text{địa chỉ} / 4096 \rfloor$, $d = \text{địa chỉ} \bmod 4096$.
Các trang được HĐH neo cố định (không được swap out): `P1.p0` (`#300`), `P1.p2` (`#301`), `P2.p0` (`#300`), `P2.p2` (`#302`).
Ban đầu frame tự do là `#0`, trang không bị neo đang nằm trong RAM là `P2.p3` (`#400`).

- **a. P2 truy cập địa chỉ `13000` ($p = 3, d = 712$):**
  - Tra bảng trang của P2 tại `page 3`: `Valid = V`, `Frame = #400` $\implies$ **Page Hit**.
  - Địa chỉ vật lý: `<#400, 712>` $= 400 \times 4096 + 712 = 1.639.112$.
- **b. P1 truy cập địa chỉ `13000` ($p = 3, d = 712$):**
  - Tra bảng trang của P1 tại `page 3`: `Valid = I` $\implies$ **Page Fault**.
  - Hệ thống còn khung trang tự do `#0`. Nạp `P1.p3` từ đĩa vào frame `#0`.
  - Cập nhật bảng trang P1: `page 3 -> Frame #0, Valid = V`.
  - Địa chỉ vật lý: `<#0, 712>` $= 0 \times 4096 + 712 = 712$.
- **c. P1 truy cập địa chỉ `16383` ($p = 3, d = 4095$):**
  - Tra bảng trang của P1 tại `page 3`: `Valid = V`, `Frame = #0` $\implies$ **Page Hit**.
  - Địa chỉ vật lý: `<#0, 4095>` $= 0 \times 4096 + 4095 = 4095$.
- **d. P3 truy cập địa chỉ `4096` ($p = 1, d = 0$):**
  - Tra bảng trang của P3 tại `page 1`: `Valid = I` $\implies$ **Page Fault**.
  - Hết khung trang trống. Trong các trang không bị neo (`P2.p3` dùng lần cuối ở bước a, `P1.p3` dùng lần cuối ở bước c), theo LRU chọn **`P2.p3` (frame `#400`)** làm nạn nhân.
  - Swap out `P2.p3`, cập nhật bảng trang P2 (`page 3 -> Valid = I`).
  - Nạp `P3.p1` vào frame `#400`, cập nhật bảng trang P3 (`page 1 -> Frame #400, Valid = V`).
  - Địa chỉ vật lý: `<#400, 0>` $= 400 \times 4096 + 0 = 1.638.400$.
- **e. P3 truy cập địa chỉ `13000` ($p = 3, d = 712$):**
  - Tra bảng trang của P3 tại `page 3`: `Valid = I` $\implies$ **Page Fault**.
  - Hết khung trang trống. Trong các trang không bị neo (`P1.p3` ở bước c, `P3.p1` ở bước d), theo LRU chọn **`P1.p3` (frame `#0`)** làm nạn nhân.
  - Swap out `P1.p3`, cập nhật bảng trang P1 (`page 3 -> Valid = I`).
  - Nạp `P3.p3` vào frame `#0`, cập nhật bảng trang P3 (`page 3 -> Frame #0, Valid = V`).
  - Địa chỉ vật lý: `<#0, 712>` $= 712$.
- **f. P2 truy cập địa chỉ `16383` ($p = 3, d = 4095$):**
  - Tra bảng trang của P2 tại `page 3`: `Valid = I` $\implies$ **Page Fault**.
  - Hết khung trang trống. Trong các trang không bị neo (`P3.p1` ở bước d, `P3.p3` ở bước e), theo LRU chọn **`P3.p1` (frame `#400`)** làm nạn nhân.
  - Swap out `P3.p1`, cập nhật bảng trang P3 (`page 1 -> Valid = I`).
  - Nạp `P2.p3` vào frame `#400`, cập nhật bảng trang P2 (`page 3 -> Frame #400, Valid = V`).
  - Địa chỉ vật lý: `<#400, 4095>` $= 400 \times 4096 + 4095 = 1.642.495$.

**Bảng trạng thái bảng trang sau bước f:**

| Page | P1 (Frame / Valid) | P2 (Frame / Valid) | P3 (Frame / Valid) |
| :---: | :---: | :---: | :---: |
| **0** | `#300` / `V` | `#300` / `V` | `I` |
| **1** | `I` | `I` | `I` |
| **2** | `#301` / `V` | `#302` / `V` | `I` |
| **3** | `I` | `#400` / `V` | `#0` / `V` |

- **g. Tại sao có hai tiến trình cùng được cấp phát khung trang `#300`?**
  - Do cơ chế **chia sẻ bộ nhớ (Memory Sharing)** trong phân trang: `page 0` của P1 và `page 0` của P2 cùng ánh xạ tới một khung trang vật lý `#300` nhằm dùng chung mã lệnh (ví dụ thư viện dùng chung, code segment chỉ đọc) hoặc vùng dữ liệu chung (shared memory), giúp tiết kiệm RAM.

---

#### Bài tập 2

**1. Số khung trang (frame) của hệ thống:**
- RAM $= 4\text{ KB} = 4096\text{ byte} = 2^{12}\text{ byte}$.
- Kích thước 1 trang (và khung trang) $= 1024\text{ byte} = 2^{10}\text{ byte}$.
- **Số khung trang:** $\dfrac{4096}{1024} = 4$ khung trang (đánh số từ Frame 0 đến Frame 3).

**2. Số lượng trang ảo tối đa cho một tiến trình:**
- Địa chỉ logic $13\text{ bit} \implies$ Kích thước KGĐC $= 2^{13}\text{ byte} = 8192\text{ byte}$.
- **Số lượng trang ảo tối đa:** $\dfrac{2^{13}}{2^{10}} = 2^3 = 8$ trang ảo (đánh số từ Page 0 đến Page 7).

**3. Quá trình truy xuất bộ nhớ:**

- **a. Chuỗi truy xuất trang:**
  Với kích thước trang $1024\text{ byte}$, số hiệu trang $p = \lfloor \text{địa chỉ} / 1024 \rfloor$:
  - `P1.1024` $\to$ `P1.p1`
  - `P1.2048` $\to$ `P1.p2`
  - `P2.2050` $\to$ `P2.p2`
  - `P1.5120` $\to$ `P1.p5`
  - `P2.1000` $\to$ `P2.p0`
  - `P1.1030` $\to$ `P1.p1`
  - `P2.2050` $\to$ `P2.p2`
  - `P1.5120` $\to$ `P1.p5`
  - `P2.0` $\to$ `P2.p0`

  Chuỗi truy xuất trang: **`P1.p1, P1.p2, P2.p2, P1.p5, P2.p0, P1.p1, P2.p2, P1.p5, P2.p0`**

- **b. Diễn giải quá trình cấp phát trang theo chiến lược LRU và số lỗi trang:**

| Bước | Truy xuất | Trạng thái | Frame 0 | Frame 1 | Frame 2 | Frame 3 | Thứ tự LRU $\to$ MRU |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :--- |
| 1 | `P1.p1` | **Lỗi trang (1)** | `P1.p1` | - | - | - | `P1.p1` |
| 2 | `P1.p2` | **Lỗi trang (2)** | `P1.p1` | `P1.p2` | - | - | `P1.p1, P1.p2` |
| 3 | `P2.p2` | **Lỗi trang (3)** | `P1.p1` | `P1.p2` | `P2.p2` | - | `P1.p1, P1.p2, P2.p2` |
| 4 | `P1.p5` | **Lỗi trang (4)** | `P1.p1` | `P1.p2` | `P2.p2` | `P1.p5` | `P1.p1, P1.p2, P2.p2, P1.p5` |
| 5 | `P2.p0` | **Lỗi trang (5)** *(thay `P1.p1`)* | **`P2.p0`** | `P1.p2` | `P2.p2` | `P1.p5` | `P1.p2, P2.p2, P1.p5, P2.p0` |
| 6 | `P1.p1` | **Lỗi trang (6)** *(thay `P1.p2`)* | `P2.p0` | **`P1.p1`** | `P2.p2` | `P1.p5` | `P2.p2, P1.p5, P2.p0, P1.p1` |
| 7 | `P2.p2` | Hit | `P2.p0` | `P1.p1` | `P2.p2` | `P1.p5` | `P1.p5, P2.p0, P1.p1, P2.p2` |
| 8 | `P1.p5` | Hit | `P2.p0` | `P1.p1` | `P2.p2` | `P1.p5` | `P2.p0, P1.p1, P2.p2, P1.p5` |
| 9 | `P2.p0` | Hit | `P2.p0` | `P1.p1` | `P2.p2` | `P1.p5` | `P1.p1, P2.p2, P1.p5, P2.p0` |

- **Tổng số lỗi trang:** **6 lỗi trang**.

---

### Phần 2: Giải thích chi tiết, cụ thể, chính xác lời giải

#### Giải thích chi tiết Bài tập 1

1. **Cách quy đổi đơn vị và tính số trang / khung trang:**
   - Trong hệ thống máy tính, $1\text{ KB} = 2^{10}\text{ byte} = 1024\text{ byte}$, $1\text{ MB} = 2^{20}\text{ byte}$, $1\text{ GB} = 2^{30}\text{ byte}$.
   - RAM $= 512\text{ MB} = 2^9 \times 2^{20} = 2^{29}\text{ byte}$. Mỗi khung trang có kích thước đúng bằng kích thước trang ($4096 = 2^{12}\text{ byte}$), nên số khung trang là $2^{29} / 2^{12} = 2^{17} = 131.072$.
   - Địa chỉ logic 32 bit biểu diễn được $2^{32}$ ô nhớ (mỗi ô 1 byte), tức không gian địa chỉ tối đa của mỗi tiến trình là $4\text{ GB}$. Chia cho kích thước trang $2^{12}\text{ byte}$ được $2^{20} = 1.048.576$ trang.

2. **Cách tách địa chỉ logic thành $\langle p, d \rangle$ và tính địa chỉ vật lý:**
   - Địa chỉ logic được đánh số từ `0`. Với trang kích thước $4096\text{ byte}$:
     - Trang 0: `0` $\to$ `4095`
     - Trang 1: `4096` $\to$ `8191`
     - Trang 2: `8192` $\to$ `12287`
     - Trang 3: `12288` $\to$ `16383`
   - Do đó:
     - Địa chỉ `13000`: $13000 = 3 \times 4096 + 712 \implies p = 3, d = 712$.
     - Địa chỉ `16383`: $16383 = 3 \times 4096 + 4095 \implies p = 3, d = 4095$ (byte cuối cùng của trang 3).
     - Địa chỉ `4096`: $4096 = 1 \times 4096 + 0 \implies p = 1, d = 0$ (byte đầu tiên của trang 1).
   - Khi trang $p$ nằm tại khung trang $f$ trong RAM, địa chỉ vật lý được tính theo công thức:
     $$\text{Địa chỉ vật lý} = f \times \text{Kích thước khung trang} + d = f \times 4096 + d$$

3. **Vai trò của điều kiện "neo trang" (Pinning) khi chạy thuật toán LRU:**
   - Đề bài cho hệ thống chỉ làm việc với 5 frame `{#0, #300, #301, #302, #400}` và chỉ có `#0` là trống.
   - 4 trang bị neo (`P1.p0` ở `#300`, `P1.p2` ở `#301`, `P2.p0` ở `#300`, `P2.p2` ở `#302`) **không bao giờ được phép chọn làm nạn nhân** để swap out. Vì vậy, khi chạy thuật toán LRU để tìm trang thay thế, ta **chỉ xét các trang không bị neo** đang nằm trong RAM (cụ thể là các trang nằm trên `#0` và `#400`).
   - Tại sao điều này quan trọng? Nếu không để ý điều kiện neo, ở bước d ta có thể nhầm lẫn chọn `P1.p0` hoặc `P1.p2` vì chúng chưa được nhắc tới từ đầu. Nhờ điều kiện neo, phạm vi ứng viên thay thế chỉ còn `#0` và `#400`:
     - **Bước a ($t=1$):** `P2.p3` (`#400`) được truy xuất (Hit) $\implies$ mốc dùng gần nhất của `#400` là $t=1$.
     - **Bước b ($t=2$):** `P1.p3` lỗi trang, nạp vào frame trống `#0` $\implies$ mốc dùng gần nhất của `#0` là $t=2$.
     - **Bước c ($t=3$):** `P1.p3` (`#0`) được truy xuất lại (Hit) $\implies$ cập nhật mốc dùng gần nhất của `#0` thành $t=3$.
     - **Bước d ($t=4$):** `P3.p1` lỗi trang. So sánh `#400` ($t=1$) và `#0` ($t=3$) $\implies$ `#400` cũ hơn nên `P2.p3` bị đẩy ra đĩa (bảng trang P2 mục 3 chuyển thành `I`), `P3.p1` vào `#400` ($t=4$).
     - **Bước e ($t=5$):** `P3.p3` lỗi trang. So sánh `#0` ($t=3$) và `#400` ($t=4$) $\implies$ `#0` cũ hơn nên `P1.p3` bị đẩy ra đĩa (bảng trang P1 mục 3 chuyển thành `I`), `P3.p3` vào `#0` ($t=5$).
     - **Bước f ($t=6$):** `P2.p3` bị lỗi trang vì đã bị swap out ở bước d! So sánh `#400` ($t=4$) và `#0` ($t=5$) $\implies$ `#400` cũ hơn nên `P3.p1` bị đẩy ra đĩa (bảng trang P3 mục 1 chuyển thành `I`), `P2.p3` nạp lại vào `#400` ($t=6$).

4. **Lưu ý khi cập nhật bảng trang lúc swap out:**
   - Khi một trang bị swap out khỏi frame $f$, hệ điều hành **bắt buộc** phải sửa `Valid bit` của trang đó trong bảng trang của tiến trình sở hữu nó từ `V` thành `I` (như `P2.p3` ở bước d, `P1.p3` ở bước e, `P3.p1` ở bước f). Nếu quên bước này, ở bước f hệ thống sẽ tưởng `P2.p3` vẫn còn ở `#400` và tính sai thành Page Hit!

---

#### Giải thích chi tiết Bài tập 2

1. **Tính số frame và số trang ảo tối đa:**
   - RAM $= 4\text{ KB} = 4096\text{ byte}$. Kích thước mỗi page/frame $= 1024\text{ byte} \implies$ RAM chỉ chứa được tối đa $4096 / 1024 = 4$ frame (đánh số `0, 1, 2, 3`).
   - Địa chỉ logic $13\text{ bit}$:
     - $n = 10$ bit thấp dùng cho `offset` (vì $2^{10} = 1024\text{ byte}$).
     - $13 - 10 = 3$ bit cao dùng cho `page number` $\implies$ có tối đa $2^3 = 8$ trang ảo (`Page 0` đến `Page 7`).

2. **Chuyển đổi địa chỉ logic thành số hiệu trang (chuỗi truy xuất trang):**
   - Mỗi trang dài $1024\text{ byte}$:
     - Trang 0: `0` $\to$ `1023`
     - Trang 1: `1024` $\to$ `2047`
     - Trang 2: `2048` $\to$ `3071`
     - Trang 5: `5120` $\to$ `6143`
   - Do đó:
     - `P1.1024` $= 1 \times 1024 + 0 \to$ `P1.p1`
     - `P1.2048` $= 2 \times 1024 + 0 \to$ `P1.p2`
     - `P2.2050` $= 2 \times 1024 + 2 \to$ `P2.p2`
     - `P1.5120` $= 5 \times 1024 + 0 \to$ `P1.p5`
     - `P2.1000` $= 0 \times 1024 + 1000 \to$ `P2.p0`
     - `P1.1030` $= 1 \times 1024 + 6 \to$ `P1.p1`
     - `P2.2050` $\to$ `P2.p2`
     - `P1.5120` $\to$ `P1.p5`
     - `P2.0` $= 0 \times 1024 + 0 \to$ `P2.p0`
   - **Lưu ý quan trọng:** `P1.p2` và `P2.p2` tuy có cùng số hiệu trang là `2` nhưng thuộc **hai tiến trình khác nhau** (`P1` và `P2`), do đó đây là **2 trang hoàn toàn độc lập** và cần 2 frame riêng biệt trong RAM (không phải chia sẻ).

3. **Cơ chế hoạt động của LRU toàn cục (Global LRU) trên 4 frame:**
   - Vì đề bài cho P1 và P2 vừa được nạp vào và chưa cấp frame nào, cả 4 frame vật lý ban đầu đều trống và được cấp phát chung cho các trang của P1 và P2 theo thứ tự yêu cầu.
   - **4 truy xuất đầu tiên** (`P1.p1`, `P1.p2`, `P2.p2`, `P1.p5`) đều là những trang chưa từng có trong RAM $\implies$ phát sinh **4 lỗi trang liên tiếp**, lấp đầy 4 frame trống.
   - **Bước 5 (`P2.p0`):** RAM đã đầy. Trang lâu chưa được dùng nhất là `P1.p1` (từ bước 1) $\implies$ `P1.p1` bị thay thế bởi `P2.p0` (lỗi trang thứ 5).
   - **Bước 6 (`P1.p1`):** Ngay sau khi bị đẩy ra ở bước 5, `P1` lại truy xuất địa chỉ `1030` thuộc `P1.p1`! Vì `P1.p1` vừa bị swap out nên xảy ra **lỗi trang thứ 6**. Lúc này trang ít được dùng gần đây nhất là `P1.p2` (từ bước 2) $\implies$ `P1.p2` bị đẩy ra để nạp lại `P1.p1`.
   - **Các bước 7, 8, 9 (`P2.p2`, `P1.p5`, `P2.p0`):** Cả 3 trang này đều đang hiện diện trong RAM (tại Frame 2, Frame 3, Frame 0) $\implies$ đều là **Page Hit**, không phát sinh thêm lỗi trang nào, chỉ cập nhật lại thứ tự sử dụng gần nhất (MRU) trong danh sách LRU.
   - Tổng kết: **6 lỗi trang** trên tổng số 9 lần truy xuất.

