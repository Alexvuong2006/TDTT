# CẨM NANG CHUẨN BỊ VẤN ĐÁP ĐỒ ÁN 1: SỐ NGUYÊN TỐ & TRAO ĐỔI KHÓA DIFFIE-HELLMAN

> **Môn học:** Nhập môn mã hóa - mật mã (FIT - HCMUS)  
> **Giảng viên hướng dẫn:** Thầy Trần Hải Anh Điền  
> **Nhóm 18:** Vương Hữu Khang (`24120070`) — Tạ Quang Mạnh (`24120089`) — Lâm Duy Minh (`24120091`)  
> **Bài nộp trên Moodle:** `24120070-24120089-24120091.zip` (gồm 6 file `.cpp` trong `project_01_source/` và `report.pdf` trong `project_01_report/`)

---

## MỤC LỤC NHANH

- [PHẦN 1: CHUẨN BỊ VỀ MẶT HẠ TẦNG (VẬT LÝ, MÔI TRƯỜNG, FILE & VIDEO DEMO)](#phần-1-chuẩn-bị-về-mặt-hạ-tầng-vật-lý-môi-trường-file--video-demo)
  - [1.1. Chuẩn bị môi trường & Source code bài nộp từ Moodle (Lưu ý 1)](#11-chuẩn-bị-môi-trường--source-code-bài-nộp-từ-moodle-lưu-ý-1)
  - [1.2. Kịch bản quay Video Demo 1–2 phút chi tiết từng giây (Lưu ý 2)](#12-kịch-bản-quay-video-demo-12-phút-chi-tiết-từng-giây-lưu-ý-2)
  - [1.3. Bộ lệnh Demo "Bất bại" & Phương án dự phòng (Plan B)](#13-bộ-lệnh-demo-bất-bại--phương-án-dự-phòng-plan-b)
- [PHẦN 2: CHUẨN BỊ VỀ MẶT KIẾN THỨC (GIẢI THÍCH CODE TỪNG DÒNG & LUYỆN PHẢN BIỆN)](#phần-2-chuẩn-bị-về-mặt-kiến-thức-giải-thích-code-từng-dòng--luyện-phản-biện)
  - [2.1. Tổng quan Kiến trúc Hệ thống & Mô hình Unity Build](#21-tổng-quan-kiến-trúc-hệ-thống--mô-hình-unity-build)
  - [2.2. Module `bigint.cpp` — Hệ thống Số lớn & Phép chia Knuth Algorithm D](#22-module-bigintcpp--hệ-thống-số-lớn--phép-chia-knuth-algorithm-d)
  - [2.3. Module `dh.cpp` — Số học Mô-đun & Giao thức Diffie-Hellman](#23-module-dhcpp--số-học-mô-đun--giao-thức-diffie-hellman)
  - [2.4. Module `fips202.cpp` & `prng.cpp` — CSPRNG, Entropy OS & Keccak Sponge](#24-module-fips202cpp--prngcpp--csprng-entropy-os--keccak-sponge)
  - [2.5. Module `prime.cpp` — Rejection Sampling, Miller-Rabin & Sinh Safe Prime 4 tầng](#25-module-primecpp--rejection-sampling-miller-rabin--sinh-safe-prime-4-tầng)
  - [2.6. Module `main.cpp` — Điều phối Chương trình & Giao diện CLI](#26-module-maincpp--điều-phối-chương-trình--giao-diện-cli)
  - [2.7. Tình huống Live-Coding & Hỏi xoáy tổng hợp tại chỗ](#27-tình-huống-live-coding--hỏi-xoáy-tổng-hợp-tại-chỗ)
- [PHẦN 3: GIẢI THÍCH TỪNG DÒNG CODE CHI TIẾT CỦA TOÀN BỘ 6 FILE MÃ NGUỒN](#phần-3-giải-thích-từng-dòng-code-chi-tiết-của-toàn-bộ-6-file-mã-nguồn)
  - [3.1. File `fips202.cpp` (850 dòng) — Lõi Keccak / SHA-3 / SHAKE128](#31-file-fips202cpp-850-dòng--lõi-keccak--sha-3--shake128)
  - [3.2. File `prng.cpp` (129 dòng) — CSPRNG & Nguồn Entropy OS](#32-file-prngcpp-129-dòng--csprng--nguồn-entropy-os)
  - [3.3. File `bigint.cpp` (509 dòng) — Hệ thống Số lớn & Chia Knuth Algorithm D](#33-file-bigintcpp-509-dòng--hệ-thống-số-lớn--chia-knuth-algorithm-d)
  - [3.4. File `dh.cpp` (170 dòng) — Số học Mô-đun & Trao đổi khóa Diffie-Hellman](#34-file-dhcpp-170-dòng--số-học-mô-đun--trao-đổi-khóa-diffie-hellman)
  - [3.5. File `prime.cpp` (484 dòng) — Rejection Sampling, Miller-Rabin & Sinh Safe Prime](#35-file-primecpp-484-dòng--rejection-sampling-miller-rabin--sinh-safe-prime)
  - [3.6. File `main.cpp` (201 dòng) — Chương trình chính & Giao diện CLI](#36-file-maincpp-201-dòng--chương-trình-chính--giao-diện-cli)

---

# PHẦN 1: CHUẨN BỊ VỀ MẶT HẠ TẦNG (VẬT LÝ, MÔI TRƯỜNG, FILE & VIDEO DEMO)

Mục tiêu của Phần 1 là đảm bảo **tuyệt đối không xảy ra sự cố kỹ thuật** (lỗi đường dẫn, lỗi trình biên dịch, lúng túng mở file, quay video bị lỗi hoặc quá giờ) trong lúc quay video và trong buổi vấn đáp trực tiếp.

---

## 1.1. Chuẩn bị môi trường & Source code bài nộp từ Moodle (Lưu ý 1)

### A. Kiểm tra hiện trạng máy tính (Checklist trước buổi vấn đáp 1 ngày)

1. **Trình biên dịch C++ (`g++`):**
   - Máy đã cài sẵn `g++ 15.2.0` (MSYS2 UCRT64) trong `PATH`.
   - Mở PowerShell kiểm tra lại bằng lệnh:
     ```powershell
     g++ --version
     ```
     Phải in ra `g++.exe (Rev8, Built by MSYS2 project) 15.2.0` (không báo lỗi `not recognized`).
2. **Kiểm tra file bài nộp trên Moodle:**
   - Tên file chính xác: `24120070-24120089-24120091.zip` (kích thước `659,912 bytes`, SHA-256: `54c00f6864cecbdee50cd0984d2b6d55eb9f7cdcdb1c028ac576a697fb31ac9f`).
   - Cấu trúc bên trong phải đúng 7 file:
     ```text
     24120070-24120089-24120091.zip
     ├── project_01_source/
     │   ├── bigint.cpp
     │   ├── dh.cpp
     │   ├── fips202.cpp
     │   ├── main.cpp
     │   ├── prime.cpp
     │   └── prng.cpp
     └── project_01_report/
         └── report.pdf
     ```

### B. Cạm bẫy chết người trên Windows — BẮT BUỘC TRÁNH

> ⚠️ **CẢNH BÁO ĐỎ:** Khi biên dịch với MinGW `g++` trên Windows, nếu đường dẫn đầu ra có **chữ tiếng Việt có dấu** (ví dụ `D:\Nhập môn Crypto\...`), trình liên kết `ld.exe` có thể báo lỗi `cannot open output file ...: Invalid argument`.
>
> **Cách phòng tránh 100%:**
> 1. Tải file `.zip` từ Moodle về thư mục **KHÔNG DẤU, KHÔNG KHOẢNG TRẮNG** như `C:\Users\Khang\Downloads` hoặc tạo sẵn thư mục `C:\demo_dh`.
> 2. Luôn `cd` vào thẳng bên trong thư mục `project_01_source` rồi mới gõ lệnh `g++ -o dh.exe main.cpp` (dùng tên file tương đối `dh.exe`, không truyền đường dẫn tuyệt đối có dấu).

### C. Bố trí màn hình & Công cụ trước giờ vấn đáp 15 phút

1. **Đăng nhập sẵn Moodle** trên trình duyệt (mở sẵn đúng tab trang nộp Đồ án 1 để nếu thầy yêu cầu tải lại trước mặt thầy thì bấm tải ngay, không mất công nhập mật khẩu/2FA).
2. **Giải nén sẵn 1 bản đã tải trực tiếp từ Moodle** tại `C:\demo_dh\24120070-24120089-24120091\`.
3. **Mở sẵn VS Code** tại thư mục `C:\demo_dh\24120070-24120089-24120091\project_01_source`:
   - Mở sẵn 6 tab theo đúng thứ tự phụ thuộc: `main.cpp` | `bigint.cpp` | `dh.cpp` | `prime.cpp` | `prng.cpp` | `fips202.cpp`.
   - Tăng cỡ chữ editor (`Ctrl + =`) lên khoảng `15–16px` để khi chiếu màn hình thầy đọc rõ.
4. **Mở sẵn 1 cửa sổ Windows Terminal / PowerShell** đứng sẵn tại `project_01_source`:
   - Tăng cỡ chữ Terminal (`Ctrl + cuộn chuột` hoặc Settings → Font size `16–18pt`).
   - Xóa sạch lịch sử màn hình (`cls`) cho gọn gàng.
5. **Mở sẵn `report.pdf`** ở 1 tab trình duyệt hoặc PDF reader để khi thầy hỏi bảng benchmark, số liệu đo đạc, hoặc công thức trong báo cáo thì lật ngay tới trang đó.
6. **Tắt toàn bộ thông báo** (bật chế độ *Do Not Disturb* trên Windows, tắt Messenger/Zalo/Discord popup), dọn dẹp Desktop, sạc đầy pin laptop + cắm sẵn sạc.

---

## 1.2. Kịch bản quay Video Demo 1–2 phút chi tiết từng giây (Lưu ý 2)

### A. Chuẩn bị kỹ thuật quay video

- **Phần mềm quay khuyến nghị:**
  - **Cách 1 (Nhanh nhất, có sẵn trên Windows 11):** Nhấn `Win + Shift + R` (Snipping Tool Record) → chọn quay toàn màn hình (Full Screen).
  - **Cách 2 (Chất lượng sắc nét nhất):** Dùng **OBS Studio** (Display Capture, 1920×1080, 30 fps, định dạng `.mp4`).
- **Yêu cầu cốt lõi của thầy:**
  - Thời lượng: **1 đến 2 phút** (đẹp nhất là **1 phút 25 giây – 1 phút 45 giây**, tuyệt đối không dài dòng vượt 2 phút).
  - Bắt buộc bắt đầu **từ bước tải source code trực tiếp từ Moodle** (nhìn thấy giao diện Moodle, click vào file zip nộp bài, thấy file tải xuống).
- **Mẹo quay 1 phát ăn ngay:**
  - Đăng nhập sẵn Moodle trước khi bấm Record.
  - Dọn trống thư mục `C:\Users\Khang\Downloads` (hoặc tạo một thư mục tải về riêng trống trơn) để khi tải file zip xuống nhìn thấy rõ ràng, không bị rối lẫn file cũ.
  - Mở sẵn Notepad ở màn hình phụ (hoặc nhớ sẵn) các câu lệnh để gõ nhanh, mượt, không gõ sai chính tả.

### B. Kịch bản chi tiết từng mốc thời gian (Tổng ~1 phút 35 giây)

| Mốc thời gian | Thao tác thực hiện trên màn hình | Lưu ý để video "ăn điểm" |
| :--- | :--- | :--- |
| **0:00 – 0:15** | Đang ở trang nộp bài trên **Moodle**. Rê chuột vào file `24120070-24120089-24120091.zip` và click tải xuống. Chờ trình duyệt báo tải xong. | Giữ chuột 1–2 giây trên tên file để thầy nhìn rõ đúng bài nộp trên Moodle. |
| **0:15 – 0:30** | Mở thư mục `Downloads` → chuột phải vào `24120070-24120089-24120091.zip` → **Extract All...** (Giải nén). Mở thư mục vừa giải nén cho thấy đúng 2 thư mục `project_01_source` và `project_01_report`. Click vào `project_01_source` để lộ đúng 6 file `.cpp`. | Cho thầy thấy trực quan không có file rác, không có `.h` hay `.exe` sẵn trong bài nộp. |
| **0:30 – 0:45** | Trong thư mục `project_01_source`, chuột phải chọn **Open in Terminal** (hoặc gõ `cmd` / `powershell` trên thanh địa chỉ). Gõ lệnh biên dịch:<br>`g++ -std=c++14 -O2 -Wall -Wextra -Wpedantic -o dh.exe main.cpp` | Nhấn Enter. Dừng 2 giây cho thầy thấy terminal không in ra bất kỳ lỗi hay cảnh báo nào (biên dịch sạch 100% chuẩn C++14). |
| **0:45 – 1:05** | Chạy chương trình với cấu hình mặc định (512-bit):<br>`.\dh.exe` | Chương trình chạy trong ~0.3–0.5s. Cuộn nhẹ hoặc dừng 4–5 giây để thầy nhìn rõ đủ 5 bước: `p` (đúng 512 bit), `g = 4`, `a, b`, `A, B` hợp lệ, `s_A == s_B` và dòng `[XAC MINH THANH CONG]`. |
| **1:05 – 1:25** | Chạy lệnh xem trợ giúp & chạy thử 1024-bit:<br>`.\dh.exe --help`<br>`.\dh.exe --bits 1024 --rounds 40` | Thể hiện khả năng tùy biến tham số dòng lệnh linh hoạt (sinh safe prime 1024-bit mất khoảng 2–5 giây, rất nhanh và ấn tượng). |
| **1:25 – 1:40** | *(Tùy chọn, nếu vẫn dưới 1:45)* Chạy với `--seed` cố định:<br>`.\dh.exe --bits 512 --seed 0123456789abcdef0123456789abcdef0123456789abcdef0123456789abcdef` | Chứng minh chế độ tái lập kết quả để debug/kiểm thử hoạt động trơn tru. Sau đó dừng quay. |

### C. Checklist kiểm duyệt video trước khi lưu

- [ ] Video dài trong khoảng `1:10` – `1:55` (tuyệt đối không quá 2:00).
- [ ] Mở đầu có cảnh tải trực tiếp từ Moodle rõ ràng.
- [ ] Chữ trong Terminal đọc rõ nét, không bị mờ/nhỏ.
- [ ] Thấy rõ lệnh biên dịch có cờ `-std=c++14` và không có lỗi/warning.
- [ ] Thấy rõ kết quả `[XAC MINH THANH CONG] Bi mat chung hai ben hoan toan TRUNG KHOP!`.
- [ ] Xem lại từ đầu đến cuối ít nhất 1 lần bằng media player để chắc chắn file video không bị corrupt/mất hình.

---

## 1.3. Bộ lệnh Demo "Bất bại" & Phương án dự phòng (Plan B)

### Bộ lệnh copy-paste sẵn cho buổi vấn đáp trực tiếp

```powershell
# 1. Kiểm tra file trong thư mục source (chỉ có 6 file .cpp)
ls

# 2. Biên dịch chuẩn C++14 với mức cảnh báo tối đa
g++ -std=c++14 -O2 -Wall -Wextra -Wpedantic -o dh.exe main.cpp

# 3. Xem hướng dẫn tham số CLI
.\dh.exe --help

# 4. Chạy mặc định (512 bit, 40 vòng Miller-Rabin, entropy từ OS)
.\dh.exe

# 5. Chạy 768 bit hoặc 1024 bit
.\dh.exe --bits 768
.\dh.exe --bits 1024 --rounds 40

# 6. Chạy với seed cố định (64 ký tự hex = 32 byte) -> chạy 2 lần ra kết quả giống hệt nhau
.\dh.exe --bits 512 --seed 0123456789abcdef0123456789abcdef0123456789abcdef0123456789abcdef

# 7. Demo bắt lỗi đầu vào (Validation)
.\dh.exe --bits 2048      # Báo vượt MAX_PRIME_BITS (1024) và chỉ rõ chỗ sửa trong bigint.cpp
.\dh.exe --seed 1234      # Báo lỗi phải đủ 64 ký tự hex
.\dh.exe --rounds 5000    # Báo lỗi vượt khoảng [1, 1000]
```

### Phương án dự phòng (Plan B) nếu có sự cố

- **Moodle bị chậm/không truy cập được lúc vấn đáp:** Dùng ngay file `24120070-24120089-24120091.zip` đã tải sẵn từ trước đó (để trong `Downloads`), đồng thời có sẵn video quay bước tải từ Moodle làm bằng chứng.
- **Lỡ chạy `--bits 1024` đúng lượt gặp ứng viên lâu (> 10s):** Bình tĩnh giải thích cho thầy: *"Vì sinh số nguyên tố là quá trình ngẫu nhiên (phân bố hình học), thời gian mỗi lần dao động từ 0.4s đến ~12s, trung bình ~4.5s theo benchmark của nhóm"*. Nếu cần nhanh ngay lập tức, có thể bấm `Ctrl + C` và chạy lại hoặc chạy với `--seed` đã test sẵn ra nhanh!
- **Thầy muốn kiểm tra thêm unit test / benchmark (nếu có hỏi):** Bộ test đầy đủ nằm ở repo gốc `D:\Nhập môn Crypto\GitHub\tests\` (`test_bigint.cpp`, `test_prng_prime.cpp`, `test_dh.cpp`, `bench_safe_prime.cpp`, `crosscheck_div_stress.py`, `crosscheck_modexp.py`). Nhớ nhấn mạnh với thầy: *các file test này không nộp vào `.zip` để tuân thủ đúng quy định `project_01_source/*.cpp`.*

---

# PHẦN 2: CHUẨN BỊ VỀ MẶT KIẾN THỨC (GIẢI THÍCH CODE TỪNG DÒNG & LUYỆN PHẢN BIỆN)

Phần này hệ thống lại **toàn bộ kiến trúc, cơ sở toán học, và giải thích cặn kẽ từng khối/từng dòng code** trong cả 6 file `.cpp` của bài nộp, kèm **hệ thống câu hỏi phản biện từ cơ bản đến hỏi xoáy**.

---

## 2.1. Tổng quan Kiến trúc Hệ thống & Mô hình Unity Build

### Kiến thức cốt lõi

1. **Quy định bài nộp (`Lab01.pdf`):**
   - Ngôn ngữ: C/C++ chuẩn **C++14 trở xuống** (`-std=c++14`), chỉ dùng C++ Standard Library + mã nguồn PRNG tham khảo.
   - Cấu trúc: `project_01_source/*.cpp` — **chỉ chứa file `.cpp`**, không `.h`, không `.c`, không `Makefile`.
2. **Giải pháp kiến trúc — Unity Build (Single Translation Unit):**
   - Thay vì tách `.h`/`.cpp` và link nhiều file `.o`, mỗi module được gói gọn trong 1 file `.cpp` duy nhất và được bảo vệ bằng **include guard** (`#ifndef <NAME>_CPP ... #define <NAME>_CPP ... #endif`).
   - File `main.cpp` đóng vai trò "file gốc" `#include` các module theo đúng thứ tự phụ thuộc (DAG — Directed Acyclic Graph):
     ```text
     fips202.cpp  (Keccak / SHAKE128 - không phụ thuộc module nội bộ nào)
          │
          ▼
     prng.cpp     (CSPRNG dùng SHAKE128 + randombytes OS)
          │
          ▼
     bigint.cpp   (Số nguyên lớn uint_t<N>, big_t, Knuth D)
          │
          ▼
     dh.cpp       (AddMod/MultMod/ExpMod, modular_exponentiation, choose_generator, is_valid_public_value)
          │
          ▼
     prime.cpp    (random_bits, random_range, Miller-Rabin, sàng đồng thời, generate_safe_prime, generate_private_key)
          │
          ▼
     main.cpp     (CLI + điều phối toàn bộ 5 bước Diffie-Hellman)
     ```
3. **Phân công công việc thực tế (33.3% mỗi người, KHÔNG nói chức danh trưởng nhóm):**
   - **Vương Hữu Khang (`24120070`):** Kiến trúc tổng thể, `bigint.cpp` (biểu diễn, I/O hex/dec, so sánh, `+`, `-`, `*`, `<<`, `>>`, `mod_small`), `AddMod`/`MultMod`/`ExpMod` theo pseudocode, `main.cpp` (CLI & luồng chính), bộ test `test_bigint` & `crosscheck_bigint`, Báo cáo Mục 1 (chính), Mục 5, tổng hợp Mục 6 & xuất PDF.
   - **Tạ Quang Mạnh (`24120089`):** Phép chia số lớn Knuth Algorithm D (`divmod`, `/`, `%`) trong `bigint.cpp`, `dh.cpp` (`modular_exponentiation`, `choose_generator`, `is_valid_public_value`), validation trong `main.cpp`, stress test phép chia & lũy thừa, Báo cáo Mục 1.5, 1.6 và Mục 4.
   - **Lâm Duy Minh (`24120091`):** Port `prng.cpp` sang Windows (`rand_s`) + sửa bug `outlen` và UB dịch bit, toàn bộ `prime.cpp` (`random_bits`, `random_range` Rejection Sampling, Miller-Rabin `uint64_t` & `big_t`, sàng đồng thời 302 số nguyên tố nhỏ, `generate_safe_prime` 4 tầng, `generate_private_key`), `bench_safe_prime`, Báo cáo Mục 2, Mục 3 (điểm cộng) và Mục 6.1.

### Câu hỏi luyện phản biện — Phần 2.1

> **Q1.1: Tại sao lại `#include` file `.cpp` vào nhau? Trong C++ bình thường người ta khuyên không nên làm vậy mà?**
> - **Đáp:** Bình thường tách `.h`/`.cpp` để giảm thời gian biên dịch lại ở dự án hàng trăm file. Tuy nhiên đề bài yêu cầu thư mục `project_01_source/` **chỉ chứa file `*.cpp`** (không có `.h` hay `Makefile`). Với dự án nhỏ gồm 6 file, mô hình **Unity Build** giúp: (1) giảng viên biên dịch chỉ bằng đúng 1 lệnh `g++ main.cpp` mà không cần tự tìm danh sách file để link; (2) tránh lỗi định nghĩa trùng lặp (ODR violation) nhờ include guard `#ifndef ..._CPP`; (3) trình biên dịch nhìn thấy toàn bộ mã nguồn trong một đơn vị biên dịch nên thực hiện inlining và tối ưu hóa toàn cục (`-O2`) tốt hơn.
>
> **Q1.2: Nếu tôi biên dịch bằng lệnh `g++ -std=c++14 *.cpp` thay vì `g++ -std=c++14 main.cpp` thì sao?**
> - **Đáp:** Nếu biên dịch tất cả `*.cpp` cùng lúc, trình liên kết sẽ báo lỗi `multiple definition` vì `main.cpp` đã `#include` các file kia (mỗi file `.cpp` được biên dịch thành 1 `.o` riêng đều chứa bản sao của hàm không phải `inline`/`template`). Do đó trong báo cáo Mục 5 và comment đầu `main.cpp`, nhóm đã ghi rất rõ lệnh biên dịch chuẩn là `g++ -std=c++14 -O2 -Wall -Wextra -o dh main.cpp`.
>
> **Q1.3: Chương trình có dùng tính năng nào của C++17 trở lên không?**
> - **Đáp:** Tuyệt đối không. Nhóm luôn biên dịch kiểm tra bằng cờ `-std=c++14 -Wall -Wextra -Wpedantic` (đạt 0 lỗi, 0 cảnh báo). Không dùng `std::optional`, `std::string_view`, structured bindings, `if constexpr`, v.v.
>
> **Q1.4: Trong `bigint.cpp` dùng `unsigned __int128` và `__builtin_clzll`, vậy đó có phải là thư viện ngoài không?**
> - **Đáp:** Không phải thư viện ngoài, đây là phần mở rộng nội tại (compiler extension / intrinsic) của trình biên dịch `g++`/Clang trên kiến trúc 64-bit, được chính file gợi ý `u512_sample.h` của môn học gợi ý sử dụng. Với `__builtin_clzll` và `__builtin_ctzll`, nhóm còn viết sẵn nhánh `#else` thuần C++ dự phòng nếu biên dịch trên trình biên dịch khác.

---

## 2.2. Module `bigint.cpp` — Hệ thống Số lớn & Phép chia Knuth Algorithm D

*(File dài 509 dòng — Đây là phần TRỌNG TÂM của Khang ở các dòng 1–348 và của Mạnh ở phần chia Knuth D dòng 350–506)*

### A. Giải thích chi tiết từng khối / từng dòng code

#### 1. Kiểu 128-bit & Cấu trúc `uint_t<N>` (Dòng 21–33 & 177–185)

```cpp
21: __extension__ typedef unsigned __int128 uint128_t;
23: template <size_t N> // N limb 64-bit
24: struct uint_t {
26:     uint64_t digits[N];
29:     uint_t() {
31:         for (size_t i = 0; i < N; i++) digits[i] = 0;
32:     }
...
183: const size_t MAX_PRIME_BITS = 1024;
184: const size_t BIG_LIMBS = 2 * MAX_PRIME_BITS / 64; // = 32 limbs = 2048 bit
185: typedef uint_t<BIG_LIMBS> big_t;
```

- **Dòng 21 (`__extension__`):** Khi bật cờ `-Wpedantic`, GCC sẽ cảnh báo ISO C++ không có kiểu `__int128`. Từ khóa `__extension__` bảo trình biên dịch đây là chủ ý để biên dịch sạch 0 warning.
- **Dòng 23–26 (`template <size_t N>`):** Dùng mảng tĩnh `uint64_t digits[N]` biểu diễn số nguyên không âm theo **Little-Endian theo cấp limb**:

$$
A = \sum_{i=0}^{N-1} d_i \cdot 2^{64i}
$$

- Trong đó `d_i` chính là `digits[i]`: `digits[0]` chứa 64 bit thấp nhất (từ $2^0$ đến $2^{63}$), `digits[N-1]` chứa 64 bit cao nhất.
- **Lợi ích cấp phát tĩnh trên Stack:** Không có `new`/`malloc` hay `std::vector`, triệt tiêu overhead cấp phát động trên Heap trong hàng nghìn vòng lặp Miller-Rabin và tận dụng tối đa CPU L1/L2 Cache.
- **Dòng 29–33 (Constructor mặc định):** Luôn khởi tạo toàn bộ `N` limb về `0` để không bao giờ chứa giá trị rác từ stack.
- **Dòng 183–185 (Quy tắc gấp đôi độ rộng):** Khi tính `(a * b) % p` với $a, b \lt p$ và $p \le 2^{B}$ (với `B = MAX_PRIME_BITS`), tích trung gian $a \times b$ có độ dài tối đa là `2B` bit. Với `MAX_PRIME_BITS = 1024`, ta cần `BIG_LIMBS = 2048 / 64 = 32` limbs (`big_t` rộng 2048 bit), đảm bảo tích `a * b` **không bao giờ bị tràn**.

#### 2. Khởi tạo & Chuyển đổi chuỗi I/O (Dòng 36–128)

- **`from_u64(uint64_t v)` (Dòng 36–41):** Tạo `uint_t r` (đã zero-init), gán `r.digits[0] = v`, trả về `r`.
- **`from_hex(const std::string &s)` (Dòng 44–80):**
  - Dòng 48–50: Tự động bỏ qua tiền tố `"0x"` hoặc `"0X"` nếu có.
  - Dòng 52–59: Lọc ra chuỗi `clean` chỉ giữ các ký tự hex hợp lệ (`0-9`, `a-f`, `A-F`) — chịu lỗi tốt nếu chuỗi có khoảng trắng hay dấu gạch dưới.
  - Dòng 63–78: Vì **1 ký tự hex = 4 bit**, nên **16 ký tự hex = 64 bit = đúng 1 limb `uint64_t`**. Duyệt từ **phải sang trái** (`chunk_start = len - chunk_len`), mỗi lần cắt tối đa 16 ký tự, dịch trái `val <<= 4` rồi OR giá trị nibble vào, ghi lần lượt vào `r.digits[0]`, `r.digits[1]`,... cho đến khi hết chuỗi hoặc đầy `N` limb.
- **`to_hex()` (Dòng 82–99):**
  - Dòng 84–88: Tìm limb cao nhất khác 0 (`top`). Nếu `top < 0` (số 0) trả về `"0"`.
  - Dòng 91: Limb cao nhất `digits[top]` in bằng `"%llx"` (không đệm số 0 thừa ở đầu).
  - Dòng 94–97: Các limb thấp hơn `top - 1` xuống `0` **bắt buộc** in bằng `"%016llx"` (đệm đủ 16 chữ số hex, nếu thiếu số 0 ở giữa sẽ sai giá trị hoàn toàn!).
- **`to_dec()` (Dòng 101–128):**
  - **Kỹ thuật tối ưu rất thông minh:** Thay vì chia số lớn cho `10` từng chữ số một (rất chậm), nhóm chia lặp cho `BASE10 = 10^18` (lũy thừa lớn nhất của 10 nhỏ hơn $2^{64} \approx 1.84 \times 10^{19}$).
  - Dòng 110–115: Chia `tmp` cho `BASE10` từ limb cao xuống thấp bằng `uint128_t`: `cur = (rem << 64) | tmp.digits[i]`, thương mới `cur / BASE10`, dư mới `cur % BASE10`.
  - Dòng 119–125: Mỗi lần chia lấy ra **đúng 18 chữ số thập phân** (`%018llu` cho các khối ở sau, `%llu` cho khối cao nhất khi `tmp.is_zero()`), nối vào đầu chuỗi `s`. Giảm số vòng chia tới **18 lần**!

#### 3. Các hàm tiện ích & Thao tác bit (Dòng 130–174)

- **`is_zero()` (Dòng 130–136):** Duyệt `0..N-1`, hễ gặp limb ≠ 0 trả về `false`. Độ phức tạp `O(N)`.
- **`is_odd()` (Dòng 138):** `(digits[0] & 1) != 0`. Chỉ kiểm tra bit 0 của limb thấp nhất, `O(1)`.
- **`bit_length()` (Dòng 141–158):**
  - Tìm `top` là limb cao nhất khác 0. Nếu `top < 0` trả về `0`.
  - Dùng `__builtin_clzll(digits[top])` (Count Leading Zeros — dịch ra 1 lệnh CPU `BSR`/`LZCNT` trên x86_64):

$$
L = \text{top} \times 64 + \bigl(64 - \text{clzll}(d_{\text{top}})\bigr)
$$

  - Lưu ý quan trọng: `__builtin_clzll(0)` là Undefined Behavior, nhưng ở dòng 147 ta đã chắc chắn `digits[top] != 0` trước khi gọi!
- **`test_bit(i)` & `set_bit(i)` (Dòng 160–174):**
  - Vị trí limb: `limb = i / 64`; vị trí bit trong limb: `bit = i % 64`.
  - Kiểm tra `limb < N` để tránh truy cập ngoài mảng. Dùng hằng `1ULL` (unsigned 64-bit) chứ **tuyệt đối không dùng `1`** (vì `1 << 31` trở lên trên `int` 32-bit là Undefined Behavior!).

#### 4. Toán tử so sánh (Dòng 188–217)

- `operator==`: So từng limb từ `0` đến `N-1`.
- `operator<`: **Phải duyệt từ limb cao nhất `N-1` xuống `0`** (trọng số lớn quyết định trước!). Gặp cặp `a[i] != b[i]` đầu tiên là quyết định ngay `true`/`false`. Nếu hết vòng lặp đều bằng nhau thì trả về `false`.
- `!=`, `>`, `<=`, `>=`: Suy diễn 1 dòng từ `==` và `<` để đảm bảo tính nhất quán tuyệt đối (không thể xảy ra bug mâu thuẫn giữa `<` và `>=`).

#### 5. Phép cộng & Phép trừ (Dòng 221–252)

- **`operator+` (Dòng 222–232) — Ripple-carry Addition:**
  ```cpp
  uint128_t carry = 0;
  for (size_t i = 0; i < N; i++) {
      uint128_t sum = static_cast<uint128_t>(a.digits[i]) + b.digits[i] + carry;
      res.digits[i] = static_cast<uint64_t>(sum);
      carry = sum >> 64;
  }
  ```
  - Ép `a.digits[i]` sang `uint128_t` giúp toàn bộ tổng nằm trong 128 bit (giá trị tối đa $(2^{64}-1) + (2^{64}-1) + 1 = 2^{65} - 1$, chiếm 65 bit).
  - 64 bit thấp ghi vào `res.digits[i]`, bit thứ 64 (`sum >> 64`, chỉ nhận 0 hoặc 1) thành `carry` cho limb kế tiếp.
- **`operator-` (Dòng 236–252) — Trừ có mượn (giả định `a >= b`):**
  ```cpp
  uint128_t sub = static_cast<uint128_t>(b.digits[i]) + borrow;
  uint128_t ai = a.digits[i];
  if (ai >= sub) {
      res.digits[i] = static_cast<uint64_t>(ai - sub);
      borrow = 0;
  } else {
      res.digits[i] = static_cast<uint64_t>((static_cast<uint128_t>(1) << 64) + ai - sub);
      borrow = 1;
  }
  ```
  - **Chi tiết đắt giá:** Tại sao phải tính `sub` bằng `uint128_t` thay vì `uint64_t`? Vì nếu `b.digits[i] == 0xFFFFFFFFFFFFFFFFULL` ($2^{64}-1$) và `borrow == 1`, phép cộng `uint64_t` sẽ bị **tràn vòng về 0**, làm sai hoàn toàn nhánh `if (ai >= sub)`! Dùng `uint128_t` triệt tiêu hoàn toàn bug kinh điển này.

#### 6. Phép nhân Schoolbook tối ưu (Dòng 256–284)

```cpp
260: int len_a = static_cast<int>(N);
261: while (len_a > 0 && a.digits[len_a - 1] == 0) len_a--;
262: int len_b = static_cast<int>(N);
263: while (len_b > 0 && b.digits[len_b - 1] == 0) len_b--;
265: if (len_a == 0 || len_b == 0) return res;
267: for (int i = 0; i < len_a; i++) {
268:     if (a.digits[i] == 0) continue;
269:     uint128_t carry = 0;
270:     uint128_t ai = a.digits[i];
271:     for (int j = 0; j < len_b; j++) {
272:         if (static_cast<size_t>(i + j) >= N) break;
273:         uint128_t prod = ai * b.digits[j] + res.digits[i + j] + carry;
274:         res.digits[i + j] = static_cast<uint64_t>(prod);
275:         carry = prod >> 64;
276:     }
277:     for (size_t k = i + len_b; carry > 0 && k < N; k++) {
278:         uint128_t sum = static_cast<uint128_t>(res.digits[k]) + carry;
279:         res.digits[k] = static_cast<uint64_t>(sum);
280:         carry = sum >> 64;
281:     }
282: }
```

- **Tại sao `prod` không bao giờ tràn `uint128_t`?**

$$
\max(\text{prod}) = (2^{64}-1)(2^{64}-1) + (2^{64}-1) + (2^{64}-1) = 2^{128} - 1
$$

- Khớp vừa khít giá trị cực đại của `uint128_t`! Đây là bất đẳng thức kinh điển trong số học đa độ chính xác (TAOCP Vol 2).
- **Tối ưu thực tế:** Với số 512-bit nằm trong `big_t` 2048-bit (`N = 32`), nhờ cắt `len_a = 8`, `len_b = 8`, số vòng lặp chỉ là `8 × 8 = 64` thay vì `32 × 32 = 1024` (nhanh hơn **16 lần**!).
- **Dòng 277–281:** Lan truyền nốt phần nhớ `carry` lên các limb cao hơn `i + len_b` cho đến khi `carry == 0` hoặc chạm biên `N`.

#### 7. Phép dịch bit `<<` và `>>` (Dòng 286–332)

- Tách độ dịch thành 2 phần: `limb_shift = shift / 64` (dịch nguyên từ nhớ) và `bit_shift = shift % 64` (dịch bit trong từ nhớ).
- **Tại sao phải tách 2 nhánh `if (bit_shift == 0)` và `else`?**
  - Trong nhánh `else`, ta viết `a.digits[...] >> (64 - bit_shift)` (với `<<`) hoặc `<< (64 - bit_shift)` (với `>>`).
  - Nếu `bit_shift == 0`, biểu thức `64 - bit_shift` bằng **`64`**. Trong C++, dịch một số `uint64_t` đi ≥ 64 bit là **Undefined Behavior** (trên CPU x86_64 lệnh `SHL`/`SHR` chỉ lấy `count mod 64 = 0` nên sẽ cho kết quả sai bét!). Tách nhánh `bit_shift == 0` loại bỏ hoàn toàn UB này.

#### 8. Lấy dư với số nhỏ `mod_small` (Dòng 335–348)

```cpp
uint128_t rem = 0;
for (int i = top; i >= 0; i--) {
    rem = ((rem << 64) | a.digits[i]) % m;
}
return static_cast<uint32_t>(rem);
```

- **Nguyên lý (Sơ đồ Horner trong cơ số $2^{64}$):**

$$
A \equiv \Bigl(\bigl(\dots(d_{\text{top}} \cdot 2^{64} + d_{\text{top}-1}) \cdot 2^{64} + \dots\bigr) \cdot 2^{64} + d_0\Bigr) \pmod m
$$

- **Chứng minh không tràn `uint128_t`:** Vì `m` kiểu `uint32_t` ($m \lt 2^{32}$), sau mỗi bước `rem < m < 2^32`. Do đó `(rem << 64) | a.digits[i] < 2^96 < 2^128`.
- **Vai trò:** Dùng cho tầng sàng 302 số nguyên tố nhỏ trong `prime.cpp`, độ phức tạp chỉ `O(top) = O(n)` (chỉ ~8 phép chia phần cứng cho số 512-bit!).

#### 9. Phép chia số lớn `divmod` — Knuth Algorithm D (Dòng 367–506)

Đây là phần quan trọng nhất quyết định tốc độ toàn bộ chương trình (tăng tốc **~160 lần** so với chia nhị phân: `mulmod` 512-bit từ `72 µs` xuống `0.44 µs`, `modexp` 512-bit từ `~55 ms` xuống `0.24 ms`).

- **Xử lý đầu vào & Aliasing (Dòng 370–389):**
  - Tính vào biến cục bộ `quo, rem` rồi cuối hàm (dòng 488–489) mới gán `q = quo; r = rem;` ⇒ an toàn ngay cả khi người gọi truyền `divmod(a, b, a, r)`.
  - `n == 0` (chia cho 0): trả `q = r = 0` an toàn, không crash.
  - `a < b`: trả ngay `q = 0, r = a` trong `O(N)`.
- **Đường tắt chia 1 limb (`n == 1`, Dòng 390–399 — Short Division):**
  - Chia trực tiếp từ limb cao xuống thấp bằng `uint128_t`: `cur = (cur_rem << 64) | a.digits[i]`.
- **Knuth Algorithm D (`n >= 2`, Dòng 400–486):** Chia dài giống tiểu học nhưng trong cơ số $B = 2^{64}$:
  - **Bước D1 — Chuẩn hóa (Dòng 403–420):**
    - Tính `s = __builtin_clzll(b.digits[n - 1])`.
    - Dịch trái cả `b` thành `v[0..n-1]` và `a` thành `u[0..m_len]` đi `s` bit.
    - **Mục đích:** Đảm bảo bit cao nhất của `v[n-1]` bằng 1, tức $v_{n-1} \ge \lfloor B/2 \rfloor = 2^{63}$. Theo định lý Knuth (TAOCP Vol 2, Theorem B), điều kiện này bảo đảm ước lượng thương $\hat{q}$ ở bước D3 **không bao giờ nhỏ hơn thương thật** và **chỉ lớn hơn thương thật tối đa 2 đơn vị** ($q \le \hat{q} \le q + 2$).
    - **Tại sao mảng `u` có kích thước `N + 1`?** Vì khi dịch trái `a` đi `s` bit, các bit cao bị đẩy tràn sang limb thứ `m_len` (`u[m_len] = a.digits[m_len - 1] >> (64 - s)`).
    - **Lưu ý tính đúng toán học:** $\lfloor (a \cdot 2^s) / (b \cdot 2^s) \rfloor = \lfloor a / b \rfloor$ (thương không đổi), còn số dư bị nhân thêm $2^s$ nên bước D8 chỉ cần dịch phải lại `s` bit.
  - **Bước D2..D7 — Vòng lặp tính từng limb thương `j = m_len - n` xuống `0` (Dòng 427–476):**
    - **D3 — Ước lượng & Hiệu chỉnh $\hat{q}$ (Dòng 430–440):**
      - Lấy 2 limb cao nhất của phần bị chia hiện tại: `num = u[j+n] * B + u[j+n-1]`.
      - Tính $\hat{q} = \lfloor \text{num} / v_{n-1} \rfloor$ và $\hat{r} = \text{num} \bmod v_{n-1}$.
      - Kiểm tra thêm bằng limb thứ hai `v[n-2]` và `u[j+n-2]`:
        ```cpp
        while (q_hat >= BASE || q_hat * v_lo > ((r_hat << 64) | u[j + n - 2])) {
            q_hat--;
            r_hat += v_hi;
            if (r_hat >= BASE) break;
        }
        ```
      - *Ý nghĩa:* Nếu bất đẳng thức sau xảy ra:

$$
\hat{q} \cdot (v_{n-1} B + v_{n-2}) \gt u_{j+n} B^2 + u_{j+n-1} B + u_{j+n-2} \iff \hat{q} \cdot v_{n-2} \gt \hat{r} \cdot B + u_{j+n-2}
$$

      - thì $\hat{q}$ chắc chắn quá lớn ít nhất 1 đơn vị ⇒ giảm $\hat{q}$ đi 1, tăng $\hat{r}$ thêm `v[n-1]`. Nếu `r_hat >= BASE` thì vế phải $\ge B^2 \gt \hat{q} \cdot v_{n-2}$ chắc chắn thỏa nên `break` luôn (cũng tránh tràn `r_hat << 64` trong `uint128_t`!). Vòng `while` này chạy **tối đa 2 lần** và loại trừ hầu hết ước lượng sai (chỉ còn sai lệch 1 đơn vị với xác suất $\approx 2 / 2^{64}$).
    - **D4 — Nhân và Trừ `u[j..j+n] -= qh * v` (Dòng 442–462):**
      - Nhân `qh * v[i] + mul_carry` ra `p` (128-bit): tách `p_lo` (64 bit thấp) và `mul_carry` (64 bit cao).
      - Trừ có mượn 2 bước: `t = x - p_lo` (mượn `b1`), `t2 = t - borrow` (mượn `b2`), gộp `borrow = b1 | b2` (tránh tràn `p_lo + borrow` trong 64 bit!).
    - **D5/D6 — Cộng bù Add-back (Dòng 464–474):**
      - Nếu `(b1_top | b2_top) != 0`, nghĩa là kết quả bị âm (trường hợp cực hiếm ≈ $2/2^{64}$ khi $\hat{q}$ vẫn lớn hơn thương thật đúng 1 đơn vị).
      - Giảm `qh--` và cộng trả lại `v[0..n-1]` vào `u[j..j+n-1]`, phần nhớ tràn ra ở `u[j+n]` triệt tiêu đúng dấu âm (mod $2^{64}$).
    - Dòng 475: Ghi limb thương `quo.digits[j] = qh`.
  - **Bước D8 — Khử chuẩn hóa phần dư (Dòng 478–485):**
    - Dịch phải `u[0..n-1]` đi `s` bit để khôi phục phần dư thật `rem`.
- **Độ phức tạp Knuth D:** `O(n * (m_len - n + 1))`. Trong `modular_exponentiation`, tích có `2n` limb chia cho `p` có `n` limb ⇒ `O(n^2)`, tương đương đúng 1 phép nhân!

### B. Bộ câu hỏi phản biện & vấn đáp — Phần 2.2

> **Q2.1: Tại sao `uint_t<N>` không hỗ trợ số âm? Lỡ trong phép trừ `a - b` mà `a < b` thì sao?**
> - **Đáp:** Mọi đại lượng trong Diffie-Hellman (`p, q, g, a, b, A, B, s`) đều nằm trong `[0, p - 1]`, không bao giờ âm. Việc bỏ bit dấu giúp cấu trúc đơn giản, nhanh hơn và tránh nhánh xử lý bù 2. Trong toàn bộ code, mọi chỗ gọi `a - b` đều có tiền điều kiện đảm bảo `a >= b` (ví dụ `p - 1`, `p - 2`, `hi - lo` sau khi check `if (hi <= lo)`, hay `p - y` sau `y = y % p`). Nếu gọi `a - b` khi `a < b`, kết quả sẽ tràn vòng theo modulo $2^{64N}$ giống `uint64_t` trong C++.
>
> **Q2.2: Tại sao chọn `N` cố định bằng `template <size_t N>` thay vì dùng `std::vector<uint64_t>` cho linh hoạt kích thước?**
> - **Đáp:** Trong Miller-Rabin và `modular_exponentiation`, một lần sinh safe prime phải thực hiện hàng trăm nghìn phép `+`, `-`, `*`, `%`. Nếu dùng `std::vector`, mỗi biến trung gian phải gọi `new`/`delete` trên Heap, gây overhead rất lớn và phân mảnh cache. Dùng mảng tĩnh trên Stack nhanh hơn gấp nhiều lần, mà vẫn dễ mở rộng kích thước chỉ bằng cách sửa 1 hằng số `MAX_PRIME_BITS` duy nhất ở dòng 183 `bigint.cpp`.
>
> **Q2.3: Nếu thầy muốn sinh số nguyên tố an toàn 2048-bit ngay bây giờ thì sửa đúng những dòng nào?**
> - **Đáp:** Chỉ cần sửa **duy nhất 1 dòng** — dòng 183 trong `project_01_source/bigint.cpp`: đổi `const size_t MAX_PRIME_BITS = 1024;` thành `2048;`! Khi đó `BIG_LIMBS` tự động tính thành `2 * 2048 / 64 = 64` limbs (4096 bit), tất cả các hàm trong `bigint.cpp`, `dh.cpp`, `prime.cpp`, `main.cpp` đều tự động tương thích mà không cần sửa thêm dòng nào.
>
> **Q2.4: Tại sao trong `operator*`, phép tính `ai * b.digits[j] + res.digits[i + j] + carry` chắc chắn không bị tràn `uint128_t`?**
> - **Đáp:** Vì mỗi hạng tử `ai`, `b.digits[j]`, `res.digits[i+j]`, `carry` đều $\le 2^{64} - 1$. Nên giá trị cực đại là $(2^{64}-1)^2 + 2(2^{64}-1) = 2^{128} - 2 \cdot 2^{64} + 1 + 2 \cdot 2^{64} - 2 = 2^{128} - 1$, đúng bằng `UINT128_MAX`, không thể tràn được!
>
> **Q2.5: Tại sao trong `operator<<` và `operator>>` phải viết riêng trường hợp `if (bit_shift == 0)`?**
> - **Đáp:** Vì trong nhánh `else` có phép dịch `>> (64 - bit_shift)`. Khi `bit_shift == 0`, ta sẽ dịch `uint64_t` đi 64 bit — đây là **Undefined Behavior** trong chuẩn C++ (trên x86_64 chỉ lấy `64 % 64 = 0`, làm phép dịch bị vô hiệu và hỏng kết quả).
>
> **Q2.6: Nhánh cộng bù (D5/D6) trong Knuth D có xác suất xảy ra chỉ $\approx 2 / 2^{64}$ (gần như bằng 0 với test ngẫu nhiên). Làm sao nhóm chắc chắn nhánh đó không có bug?**
> - **Đáp:** Mạnh đã viết riêng bộ test `tests/crosscheck_div_stress.py` chuyên sinh các số "hiểm" (nhiều limb toàn `0`, `0x8000000000000000`, `0xFFFFFFFFFFFFFFFF`...) gồm **50.016 phép chia**. Khi gắn bộ đếm tạm vào code, bộ test này đã kích hoạt nhánh cộng bù đúng **3.242 lần** và nhánh hiệu chỉnh $\hat{q}$ **53.062 lần**, đối chiếu với Python cho **0 sai lệch**.
>
> **Q2.7: Trong `divmod` dòng 438, tại sao có dòng `if (r_hat >= BASE) break;`?**
> - **Đáp:** Hai lý do: (1) Về toán học, nếu $\hat{r} \ge B = 2^{64}$ thì vế phải $\hat{r} \cdot B + u_{j+n-2} \ge B^2$, trong khi vế trái $\hat{q} \cdot v_{n-2} \le (B-1)^2 \lt B^2$, nên điều kiện vòng lặp chắc chắn sai; (2) Về lập trình, nếu không `break`, phép dịch `r_hat << 64` ở lần kiểm tra tiếp theo sẽ **tràn `uint128_t`** và so sánh sai!
>
> **Q2.8: Tại sao trong `to_dec()` lại chia cho $10^{18}$ mà không chia cho `10` hay $10^{19}$?**
> - **Đáp:** Chia cho `10` phải lặp ~155 lần cho số 512-bit, còn chia cho $10^{18}$ chỉ lặp ~9 lần (nhanh gấp 18 lần). Không chọn $10^{19}$ vì dù $10^{19} \lt 2^{64} \approx 1.844 \times 10^{19}$, chọn $10^{18}$ an toàn và chẵn chữ số, mỗi lần lấy ra đúng 18 chữ số thập phân dễ format bằng `"%018llu"`.

---

## 2.3. Module `dh.cpp` — Số học Mô-đun & Giao thức Diffie-Hellman

*(File dài 170 dòng — Phụ trách chính: Mạnh + bộ hàm pseudocode Khang bổ sung)*

### A. Giải thích chi tiết từng khối / từng dòng code

#### 1. Bộ 3 hàm theo `pseudocode-modular-operation.pdf` (Dòng 22–68)

- **`AddMod(x, y, p)` (Dòng 23–32):**
  ```cpp
  x = x % p;
  y = y % p;
  uint_t<N> p_minus_y = p - y;
  if (x >= p_minus_y) return x - p_minus_y;
  return x + y;
  ```
  - **Ý tưởng:** Nếu viết `(x + y) % p` trong thanh ghi đúng `n` bit (khi `p` sát $2^n$), tổng `x + y` có thể vượt $2^n$ gây tràn trước khi `% p`. Thay vào đó, vì $0 \le x, y \lt p$, ta kiểm tra tương đương $x + y \ge p \iff x \ge p - y$ (phép `p - y` không bao giờ âm hay tràn!). Nếu đúng thì trả `x - (p - y) = x + y - p`, ngược lại $x + y \lt p \lt 2^n$ nên cộng trực tiếp không tràn!
- **`MultMod(x, y, p)` (Dòng 37–49):**
  - Kỹ thuật **Double-and-Add** nhị phân: viết $y = \sum_{i=0}^{n-1} y_i 2^i$, suy ra:

$$
x \cdot y \equiv \sum_{y_i = 1} (x \cdot 2^i) \pmod p
$$

  - Mỗi bước: nếu bit `i` của `y` bằng 1 thì `ret = AddMod(ret, x, p)`, sau đó nhân đôi `x = AddMod(x, x, p)`.
  - Mọi giá trị trung gian luôn `< p`, không cần bộ đệm `2n` bit. Nhược điểm: cần `n` vòng lặp `AddMod` (tốn `O(n * N)`), chậm hơn nhân khối + Knuth D khoảng 3 lần.
- **`ExpMod(x, y, p)` (Dòng 53–68):**
  - Lũy thừa mô-đun dạng **Right-to-Left Square-and-Multiply** gọi `MultMod`.

#### 2. `modular_exponentiation(base, exp, mod)` — Hàm chính của nhóm (Dòng 91–111)

```cpp
95:  if (mod.is_zero() || mod == one) return big_t();
98:  assert(mod.bit_length() <= MAX_PRIME_BITS);
100: big_t b = base % mod;
101: big_t result = one;
103: size_t nbits = exp.bit_length();
104: for (size_t i = nbits; i-- > 0;) {
105:     result = (result * result) % mod;
106:     if (exp.test_bit(i)) {
107:         result = (result * b) % mod;
108:     }
109: }
110: return result;
```

- **Dòng 95:** Trường hợp biên: `mod == 0` (tránh chia 0) hoặc `mod == 1` (mọi số mod 1 đều bằng 0) trả về `0`. Nếu `exp == 0`, `nbits == 0`, vòng `for` không chạy, trả về `result = 1` (đúng quy ước $b^0 \bmod m = 1$ với `m > 1`).
- **Dòng 98:** `assert` bảo vệ tiền điều kiện: `mod` không quá `MAX_PRIME_BITS` để tích `result * result` không vượt 2048 bit.
- **Dòng 104 (`for (size_t i = nbits; i-- > 0;)`):** Cú pháp duyệt ngược chuẩn mực cho biến không dấu `size_t` (nếu viết `for (size_t i = nbits - 1; i >= 0; i--)` sẽ **lặp vô hạn** vì `size_t` không bao giờ âm!).
- **Thuật toán Left-to-Right Square-and-Multiply:**
  - Duyệt từ bit cao nhất xuống bit 0. Mỗi bước luôn bình phương `result = (result * result) % mod`; nếu bit thứ `i` của `exp` là `1` thì nhân thêm `b`.
  - **Ví dụ nháp nhanh trên bảng (khi thầy kêu chạy tay):** Tính $3^{13} \bmod 7$. Ta có $13 = (1101)_2$, khởi tạo `result = 1`:
    - Bit 3 (`1`): $1^2 \cdot 3 \equiv 3 \pmod 7$
    - Bit 2 (`1`): $3^2 \cdot 3 = 27 \equiv 6 \pmod 7$
    - Bit 1 (`0`): $6^2 = 36 \equiv 1 \pmod 7$
    - Bit 0 (`1`): $1^2 \cdot 3 \equiv 3 \pmod 7$ ⇒ Kết quả là `3`.
  - **Số phép toán:** Với số mũ `k` bit, cần đúng `k` phép bình phương và trung bình `k/2` phép nhân ⇒ `≈ 1.5k` phép nhân mô-đun (~768 phép cho 512-bit, thay vì $2^{512}$ phép nhân ngây thơ!). Thời gian thực tế: **~0.24 ms** (512-bit), **~1.17 ms** (1024-bit).

#### 3. `choose_generator(p)` — Chọn phần tử sinh nhóm con bậc `q` (Dòng 133–155)

```cpp
141: big_t p_minus_1 = p - one;
142: big_t q = p_minus_1 >> 1; // q = (p - 1) / 2
144: for (uint64_t h = 2; h < 1000000; h++) {
145:     big_t hb = big_t::from_u64(h);
146:     if (hb >= p_minus_1) break;
148:     big_t g = (hb * hb) % p; // thặng dư bậc hai
149:     if (g == one) continue;
150:     if (modular_exponentiation(g, q, p) == one) {
151:         return g;
152:     }
153: }
```

- **Cơ sở toán học (CỰC KỲ HAY BỊ HỎI):**
  - Với Safe Prime $p = 2q + 1$ (`q` nguyên tố), nhóm nhân $\mathbb{Z}_p^{\ast}$ là nhóm cyclic bậc $p - 1 = 2q$.
  - Theo **Định lý Lagrange**, bậc (order) của mọi phần tử $x \in \mathbb{Z}_p^{\ast}$ phải là ước của `2q`, tức chỉ có thể thuộc tập `{1, 2, q, 2q}`:
    - Bậc `1`: duy nhất `x = 1`.
    - Bậc `2`: duy nhất $x = p - 1 \equiv -1 \pmod p$.
    - Bậc `q`: tất cả các **thặng dư bậc hai** (quadratic residues) khác 1 — có đúng `q - 1` phần tử.
    - Bậc `2q`: các phi-thặng dư bậc hai khác `p - 1` (phần tử sinh của toàn bộ $\mathbb{Z}_p^{\ast}$) — có đúng `q - 1` phần tử.
  - Khi ta lấy $g = h^2 \bmod p$ (với `h = 2` ⇒ `g = 4` cho mọi `p > 5`), `g` chắc chắn là thặng dư bậc hai nên theo tiêu chuẩn Euler:

$$
g^q = (h^2)^{(p-1)/2} = h^{p-1} \equiv 1 \pmod p
$$

  - Vì `g ≠ 1` và `q` là số nguyên tố, bậc của `g` là ước `> 1` của `q` ⇒ **bậc của `g` chắc chắn bằng đúng `q`!**
- **Tại sao nhóm chọn `g` bậc `q` (cụ thể `g = 4`) thay vì `g` bậc `2q` (căn nguyên thủy của cả $\mathbb{Z}_p^{\ast}$)?**
  1. **Tránh rò rỉ 1 bit của khóa bí mật `a`:** Nếu `g` có bậc `2q`, thì $A = g^a \bmod p$ là thặng dư bậc hai khi và chỉ khi **`a` chẵn**! Kẻ nghe lén chỉ cần tính ký hiệu Legendre $\left(\frac{A}{p}\right) \equiv A^q \pmod p$ là biết ngay bit cuối cùng (tính chẵn/lẻ) của khóa riêng `a`! Ngược lại, khi `g` sinh nhóm con thặng dư bậc hai bậc `q`, mọi $g^a$ đều là thặng dư bậc hai nên ký hiệu Legendre luôn bằng `+1`, **không rò rỉ bất kỳ thông tin nào về `a`**.
  2. **Đúng cho mọi safe prime `p > 5`:** Trong RFC 7919 dùng `g = 2` vì họ chọn riêng các safe prime thỏa $p \equiv 7 \pmod 8$ (khi đó 2 là thặng dư bậc hai). Chương trình sinh `p` ngẫu nhiên nên `p` có thể $\equiv 3 \pmod 8$ hoặc $7 \pmod 8$; chọn $g = 2^2 = 4$ đảm bảo luôn sinh đúng nhóm con bậc `q` cho **mọi** safe prime `p > 5`.

#### 4. `is_valid_public_value(v, p)` — Xác thực khóa công khai (Dòng 160–168)

```cpp
164: if (p < big_t::from_u64(7)) return false;
165: if (v < two || v > p - two) return false;
166: big_t q = (p - one) >> 1;
167: return modular_exponentiation(v, q, p) == one;
```

- **Kiểm tra 1 (`2 <= v <= p - 2`):** Loại bỏ `v = 0`, `v = 1` (bậc 1 ⇒ $s = 1^a = 1$), và `v = p - 1` (bậc 2 ⇒ $s = (-1)^a \in \{1, p-1\}$, kẻ tấn công đoán ngay bí mật chung và biết tính chẵn/lẻ của `a`).
- **Kiểm tra 2 ($v^q \equiv 1 \pmod p$):** Xác nhận `v` thực sự nằm trong nhóm con bậc nguyên tố `q` (không thuộc nhóm con nhỏ hay coset bậc `2q`), ngăn chặn hoàn toàn **Small-Subgroup Confinement Attack** (Lim & Lee, 1997).

### B. Bộ câu hỏi phản biện & vấn đáp — Phần 2.3

> **Q3.1: Tại sao trong `dh.cpp` lại cài cả 2 hàm `ExpMod` và `modular_exponentiation`? Khác nhau ở chỗ nào?**
> - **Đáp:** `AddMod`/`MultMod`/`ExpMod` được cài đặt để đối chiếu theo tài liệu `pseudocode-modular-operation.pdf` của thầy (giữ mọi biến trung gian trong `n` bit bằng Double-and-Add, không cần bộ nhớ gấp đôi nhưng chậm hơn ~3 lần). Còn `modular_exponentiation` tận dụng bộ đệm `2n` bit của `big_t` kết hợp nhân Schoolbook 128-bit và chia Knuth D, chạy nhanh hơn rất nhiều (0.24 ms cho 512-bit) nên được dùng trong luồng chính. Nhóm đã test chéo hai hàm cho kết quả trùng khớp 100%.
>
> **Q3.2: Nếu trong `choose_generator` tôi đặt cứng `g = 2` như chương trình mẫu của đề bài thì có vấn đề gì không?**
> - **Đáp:** Nếu $p \equiv 7 \pmod 8$ thì `2` là thặng dư bậc hai (bậc `q`, tốt). Nhưng nếu $p \equiv 3 \pmod 8$ (xác suất 50%) thì `2` là phi-thặng dư bậc hai (bậc `2q`), khi đó khóa công khai $A = 2^a \bmod p$ sẽ làm rò rỉ tính chẵn/lẻ của khóa riêng `a` qua ký hiệu Legendre $A^q \bmod p \in \{+1, -1\}$. Chọn $g = h^2 \bmod p$ (`g = 4`) khắc phục hoàn toàn điểm này cho mọi safe prime `p > 5`.
>
> **Q3.3: Nếu Alice không gọi `is_valid_public_value(B, p)` trước khi tính $s = B^a \bmod p$, kẻ tấn công làm gì được?**
> - **Đáp:** Kẻ tấn công tích cực có thể thay `B` bằng `B' = 1` (ép bí mật chung `s = 1`, biết trước 100%!) hoặc `B' = p - 1` (ép $s = (-1)^a \bmod p$, chỉ có 2 giá trị khả dĩ là `1` nếu `a` chẵn và `p - 1` nếu `a` lẻ, vừa đoán được khóa phiên vừa làm lộ 1 bit khóa riêng `a`).
>
> **Q3.4: Giao thức Diffie-Hellman cài trong đồ án có chống được tấn công Man-in-the-Middle (MitM) không? Thực tế TLS 1.3 giải quyết ra sao?**
> - **Đáp:** **Không.** Diffie-Hellman thuần túy không có cơ chế xác thực danh tính: Mallory có thể đứng giữa thỏa thuận khóa $s_1$ với Alice và $s_2$ với Bob, giải mã rồi mã hóa lại mọi tin nhắn. Trong thực tế (như **TLS 1.3 / HTTPS**), DH ephemeral (`(EC)DHE`) luôn đi kèm **chứng chỉ số (Certificate)** do CA ký và **chữ ký số trên toàn bộ bản ghi bắt tay (`CertificateVerify`)** để xác thực server. Ngoài ra, khóa `s` không dùng trực tiếp làm khóa AES mà đi qua hàm dẫn xuất khóa **HKDF**.
>
> **Q3.5: Forward Secrecy (PFS) là gì? Tại sao TLS 1.3 bắt buộc dùng `(EC)DHE` và loại bỏ RSA Key Exchange?**
> - **Đáp:** Với RSA Key Exchange cũ, nếu kẻ tấn công ghi lại lưu lượng mã hóa hôm nay và 5 năm sau đánh cắp được khóa riêng của server, hắn giải mã được toàn bộ dữ liệu trong quá khứ. Với `(EC)DHE` (ephemeral), khóa riêng `a, b` chỉ sinh tạm cho **duy nhất 1 phiên** rồi xóa ngay khỏi RAM; kể cả sau này khóa ký dài hạn của server bị lộ, kẻ tấn công vẫn không thể khôi phục bí mật chung $s = g^{ab} \bmod p$ của các phiên cũ.
>
> **Q3.6: Tấn công Logjam (2015) là gì? Liên quan gì đến đồ án 512-bit của mình?**
> - **Đáp:** Logjam (CVE-2015-4000) gồm 2 đòn: (1) kẻ tấn công MitM ép hạ cấp xuống `DHE_EXPORT` 512-bit; (2) bước tiền tính của thuật toán Sàng trường số (NFS) chỉ phụ thuộc vào `p` chứ không phụ thuộc `a, b`, nên với các số nguyên tố 512-bit dùng chung phổ biến, chỉ cần tiền tính 1 lần (vài ngày trên cụm máy tính) là sau đó giải từng logarit rời rạc chỉ mất vài phút! Bài học: 512-bit chỉ phù hợp mục đích học tập/minh họa như Lab01; thực tế TLS 1.3 yêu cầu tối thiểu `ffdhe2048` (2048-bit) hoặc dùng **ECDHE** (X25519 / P-256).
>
> **Q3.7: Thuật toán `modular_exponentiation` của nhóm có điểm yếu bảo mật nào về mặt thực thi không?**
> - **Đáp:** Có — nó nhạy cảm với tấn công **kênh kề thời gian / năng lượng (Timing Attack / Simple Power Analysis - SPA)**. Vì nhánh `if (exp.test_bit(i))` chỉ chạy phép nhân khi bit khóa riêng là `1`, thời gian và năng lượng tiêu thụ sẽ khác nhau giữa bit `0` và bit `1`. Hướng khắc phục là cài **Montgomery Ladder** (thời gian hằng — constant-time: mỗi bit dù 0 hay 1 đều thực hiện đúng 1 phép bình phương và 1 phép nhân).

---

## 2.4. Module `fips202.cpp` & `prng.cpp` — CSPRNG, Entropy OS & Keccak Sponge

*(File `fips202.cpp` 850 dòng gộp nguyên văn từ mẫu giảng viên; `prng.cpp` 129 dòng do Minh port và sửa lỗi)*

### A. Giải thích chi tiết từng khối / từng dòng code

#### 1. `fips202.cpp` — Cấu trúc Keccak Sponge & SHAKE128

- **Trạng thái nội bộ (`keccak_state`, dòng 28–32):**
  ```cpp
  typedef struct {
      uint64_t s[25];   // Ma trận 5x5 lane 64-bit = 1600 bit (200 byte)
      unsigned int pos; // Vị trí byte hiện tại đang absorb hoặc squeeze
  } keccak_state;
  ```
- **Thông số SHAKE128 (Chuẩn NIST FIPS 202):**
  - Tổng kích thước trạng thái: `b = 1600` bit (200 byte).
  - **Rate (tốc độ hấp thụ/xuất):** `r = SHAKE128_RATE = 168` byte (1344 bit).
  - **Capacity (dung lượng ẩn bảo mật):** `c = b - r = 256` bit (32 byte) ⇒ đảm bảo độ an toàn mật mã 128-bit (đạt `c/2 = 128` bit chống đụng độ và 128-bit bảo mật cho XOF).
  - **Hoán vị cốt lõi:** `KeccakF1600_StatePermute(s)` gồm **24 vòng** (`NROUNDS = 24`), mỗi vòng có 5 bước phi tuyến và khuếch tán ($\theta, \rho, \pi, \chi, \iota$).
  - **Domain separation byte:** `0x1F` (dòng 626) theo chuẩn padding `1111 || 10*1` của SHAKE (phân biệt với SHA-3 dùng `0x06`).
- **Quy trình 3 pha Sponge trong `prng_seed` và `prng_next_*`:**
  1. `shake128_init`: Xóa toàn bộ `s[0..24] = 0`, `pos = 0`.
  2. `shake128_absorb`: XOR từng byte của `seed` (32 byte) vào phần `rate` của trạng thái `s`.
  3. `shake128_finalize`: Đệm domain byte `0x1F` và bit cuối của block `1ULL << 63`, đặt `pos = SHAKE128_RATE` để lần squeeze đầu tiên lập tức gọi `KeccakF1600_StatePermute(s)`.
  4. `shake128_squeeze`: Đọc từng byte ra từ phần `rate` (168 byte đầu của `s`); mỗi khi đọc hết 168 byte (`pos == r`), lại gọi `KeccakF1600_StatePermute(s)` để tạo 168 byte ngẫu nhiên mới không giới hạn độ dài (**XOF — Extendable-Output Function**).

#### 2. `prng.cpp` — Port đa nền tảng & Sửa lỗi từ code mẫu

- **Dòng 17–27 (Xử lý biên dịch `rand_s` trên Windows MinGW-w64):**
  ```cpp
  #ifdef _WIN32
  #ifndef _CRT_RAND_S
  #define _CRT_RAND_S
  #endif
  #include <stdlib.h>
  #if defined(_CRTIMP)
  extern "C" _CRTIMP int __cdecl rand_s(unsigned int*);
  #else
  extern "C" int __cdecl rand_s(unsigned int*);
  #endif
  #endif
  ```
  - **Tại sao cần đoạn khai báo `extern "C"` này?** Trên MinGW-w64, nếu một file khác (như `main.cpp` hoặc unit test) `#include <iostream>` trước `prng.cpp`, `<stdlib.h>` đã được nạp ngầm mà chưa có `_CRT_RAND_S`, dẫn đến `rand_s` không được khai báo. Thêm khai báo khớp thuộc tính `_CRTIMP` (khớp `dllimport`) giúp biên dịch sạch không lỗi, không warning trên mọi thứ tự `#include`.
- **Dòng 58–90 (`randombytes(uint8_t *out, size_t outlen)`):**
  - **Sửa lỗi 1 từ code mẫu:** Đổi `uint8_t outlen` (giới hạn 255 byte) sang `size_t outlen`.
  - **Nhánh Windows (`#ifdef _WIN32`):** Gọi lặp `rand_s(&r)` (bên dưới gọi `RtlGenRandom` / `BCryptGenRandom` của nhân Windows, lấy entropy phần cứng của OS — **khác hoàn toàn với `rand()`**!). Nếu `rand_s(&r) != 0`, in lỗi và `abort()` ngay (fail-closed, tuyệt đối không tiếp tục với dữ liệu rác!). Tách 4 byte của `r` theo little-endian ghi vào `out`.
  - **Nhánh Linux/macOS (`#else`):** Gọi syscall `getrandom(out, outlen, 0)` (CSPRNG ChaCha20 của nhân Linux). Nếu bị gián đoạn bởi tín hiệu (`errno == EINTR`) thì thử lại; nếu lỗi khác thì `abort()`.
- **Dòng 99–127 (`prng_next_u16`, `prng_next_u32`, `prng_next_u64`):**
  - **Sửa lỗi 2 từ code mẫu (Undefined Behavior):** Trong code mẫu viết `buf[3] << 24`. Vì `buf[3]` là `uint8_t`, trong C++ nó bị *integer promotion* thành **`int` có dấu 32-bit**; nếu `buf[3] >= 0x80` thì dịch trái 24 bit sẽ **tràn vào bit dấu của `int` — Undefined Behavior trong C++14!** Nhóm đã sửa thành `static_cast<uint32_t>(buf[3]) << 24` (tương tự với `u16` và `u64`).

### B. Bộ câu hỏi phản biện & vấn đáp — Phần 2.4

> **Q4.1: Phân biệt TRNG, PRNG và CSPRNG? Chương trình của nhóm dùng loại nào?**
> - **Đáp:**
>   - **TRNG (True RNG):** Lấy từ nhiễu vật lý (nhiệt, jitter xung nhịp, ngắt phần cứng); không tất định nhưng chậm.
>   - **PRNG (Pseudorandom NG):** Tất định từ seed, nhanh, phân phối thống kê tốt nhưng **dễ dự đoán** (VD: `rand()`, `mt19937`).
>   - **CSPRNG (Cryptographically Secure PRNG):** Tất định từ seed có entropy cao nhưng thỏa mãn 2 tính chất: (1) *Không thể dự đoán bit kế tiếp* (Next-bit unpredictability) và (2) *Chống truy ngược trạng thái* (Backtracking resistance).
>   - Chương trình của nhóm dùng **kiến trúc CSPRNG 2 tầng**: lấy 256-bit entropy từ CSPRNG hạt nhân OS (`rand_s`/`getrandom`, tích hợp TRNG phần cứng) làm seed, rồi mở rộng vô hạn bằng **SHAKE128**.
>
> **Q4.2: Tại sao tuyệt đối không được dùng `std::rand()` hay `std::mt19937` để sinh khóa riêng `a, b`?**
> - **Đáp:**
>   - `rand()` dùng LCG ($X_{n+1} = (a X_n + c) \bmod m$), trạng thái rất nhỏ (`RAND_MAX` trên Windows chỉ là `32767`), chỉ cần 2–3 đầu ra là đoán hết; nếu dùng `srand(time(NULL))` thì 1 ngày chỉ có 86.400 seed, vét cạn trong `< 1 ms`!
>   - `std::mt19937` (Mersenne Twister) dù chu kỳ $2^{19937}-1$ nhưng phép biến đổi trạng thái (tempering) là **tuyến tính khả nghịch trên** $\mathbb{F}_2$. Chỉ cần quan sát đúng **624 số đầu ra 32-bit liên tiếp** là kẻ tấn công khôi phục 100% mảng trạng thái và dự đoán chính xác mọi khóa sinh ra sau đó!
>
> **Q4.3: SHAKE128 là hàm băm (XOF), tại sao lại dùng làm CSPRNG được?**
> - **Đáp:** Nhờ cấu trúc **Keccak Sponge** có phần ẩn `capacity` `c = 256` bit không bao giờ bị lộ ra trực tiếp ở đầu ra (chỉ đọc từ phần `rate` 168 byte), và mỗi block đều đi qua 24 vòng hoán vị phi tuyến `Keccak-f[1600]`. Vì phép hoán vị này có tính chất giả ngẫu nhiên và không thể đảo ngược khi không biết 256 bit `capacity`, đầu ra squeeze không thể phân biệt với chuỗi ngẫu nhiên thật trong thời gian đa thức.
>
> **Q4.4: Tại sao `rand_s()` lại an toàn còn `rand()` thì không, nghe tên giống nhau vậy?**
> - **Đáp:** Tuy cùng nằm trong `<stdlib.h>` của CRT Windows, nhưng `rand()` là thuật toán LCG yếu cài trong thư viện C, còn `rand_s()` là hàm bảo mật gọi trực tiếp xuống nhân hệ điều hành Windows (`RtlGenRandom` / `BCryptGenRandom`) để lấy byte ngẫu nhiên chuẩn mật mã từ bể entropy của OS.
>
> **Q4.5: Kể tên 1 sự cố thực tế nổi tiếng do sinh số ngẫu nhiên yếu?**
> - **Đáp:** **Debian OpenSSL CVE-2008-0166 (2008):** Một lập trình viên vô tình comment bỏ dòng trộn dữ liệu chưa khởi tạo vào entropy pool để tắt cảnh báo Valgrind, khiến nguồn entropy chỉ còn lại mỗi PID tiến trình (chỉ có 32.768 giá trị!). Toàn bộ khóa SSH và chứng chỉ SSL tạo trên Debian/Ubuntu trong suốt 2 năm đều bị vét cạn trong vài giây. Ngoài ra còn vụ **Dual_EC_DRBG** (nghi ngờ cài backdoor của NSA) và nghiên cứu **Mining Your Ps and Qs (2012)** phát hiện hàng nghìn khóa RSA trùng ước chung do thiết bị nhúng thiếu entropy lúc khởi động.

---

## 2.5. Module `prime.cpp` — Rejection Sampling, Miller-Rabin & Sinh Safe Prime 4 tầng

*(File dài 484 dòng — Phụ trách: Minh)*

### A. Giải thích chi tiết từng khối / từng dòng code

#### 1. Sinh số lớn ngẫu nhiên & Rejection Sampling (Dòng 28–97)

- **`random_upto_bits(ctx, bits)` (Dòng 28–55):**
  - Sinh số ngẫu nhiên đồng đều trong $[0, 2^{b} - 1]$ với `b = bits` (không ép bật bit cao nhất).
  - Tính `num_limbs = (bits + 63) / 64`, đổ `prng_next_u64(ctx)` vào các limb.
  - Nếu `rem_bits = bits % 64 != 0`, dùng mặt nạ `mask = (1ULL << rem_bits) - 1ULL` để xóa sạch các bit thừa ở limb cuối.
- **`random_bits(ctx, bits)` (Dòng 59–75):**
  - Gọi `random_upto_bits(ctx, bits)` rồi bật bit cao nhất `res.set_bit(bits - 1)` ⇒ đảm bảo kết quả nằm trong $[2^{b-1}, 2^{b} - 1]$, có **chính xác `bits` bit**.
- **`random_range(ctx, lo, hi)` (Dòng 79–97) — Rejection Sampling:**
  ```cpp
  if (hi <= lo) return lo;
  big_t range = hi - lo;
  size_t k = range.bit_length(); // 2^(k - 1) <= range <= 2^k - 1
  while (true) {
      big_t r = random_upto_bits(ctx, k);
      if (r <= range) return lo + r;
  }
  ```
  - **Loại bỏ hoàn toàn Modulo Bias:** Thay vì lấy `r % (range + 1)` (làm các số nhỏ xuất hiện nhiều hơn các số lớn), ta chọn `k` nhỏ nhất sao cho $2^k - 1 \ge R$ (với `R = range`), sinh đều $r \in [0, 2^k - 1]$, nếu `r > range` thì **vứt bỏ sinh lại**.
  - **Chứng minh hiệu quả:** Vì `k = range.bit_length()`, ta có $R \ge 2^{k-1}$, nên xác suất chấp nhận mỗi vòng là:

$$
P(\text{accept}) = \frac{R + 1}{2^k} \gt \frac{2^{k-1}}{2^k} = \frac{1}{2}
$$

  - Do đó, theo phân bố hình học, số lần lặp trung bình luôn **nhỏ hơn 2 lần**!

#### 2. Kiểm tra nguyên tố Miller-Rabin (Dòng 103–294)

- Nhóm cài 2 phiên bản: `is_probable_prime_u64` (trên 64-bit, dùng để test nhanh các số Carmichael) và `is_probable_prime` (trên `big_t`).
- **Phân tích từng dòng của `is_probable_prime(ctx, n, rounds = 40)` (Dòng 227–294):**
  - Dòng 234–245: Xử lý biên: `n < 2` ⇒ `false`; `n ∈ {2, 3}` ⇒ `true`; `n` chẵn ⇒ `false`.
  - Dòng 248–251: Phân tích $n - 1 = 2^s \cdot d$ với `d` lẻ:
    - `s = count_trailing_zeros(n_minus_1)` (dùng `__builtin_ctzll` trên limb thấp nhất khác 0).
    - `d = n_minus_1 >> s`.
  - Dòng 259–291: Lặp `rounds` (mặc định 40) vòng độc lập:
    1. Chọn cơ sở `a = random_range(ctx, 2, n - 2)` (phân phối đều 100%).
    2. Tính $x = a^d \bmod n$. Nếu `x == 1` hoặc `x == n - 1` ⇒ vòng này đạt (`continue`).
    3. Lặp `r = 1 .. s - 1`:
       - Bình phương: `x = (x * x) % n`.
       - Nếu `x == n - 1`: vòng này đạt (`passed_round = true; break;`).
       - Nếu `x == 1`: **trả về `false` ngay lập tức!** (Vì trước khi bình phương $x \not\equiv \pm 1 \pmod n$ mà $x^2 \equiv 1 \pmod n$ ⇒ tìm thấy căn bậc hai không tầm thường của `1`, chắc chắn `n` là hợp số!).
    4. Nếu hết vòng `for` mà `!passed_round` ⇒ $a^{n-1} \not\equiv 1 \pmod n$ (vi phạm định lý Fermat nhỏ) ⇒ trả về `false`.
  - Dòng 293: Qua hết `rounds` vòng ⇒ trả về `true` (Probable Prime).
- **Cơ sở xác suất (Định lý Monier–Rabin, 1980):** Với **mọi hợp số lẻ `n > 9`** (kể cả mọi số Carmichael!), số lượng "nhân chứng giả mạnh" (strong liars) không vượt quá $(n - 1)/4$. Do đó sau `k` vòng chọn `a` độc lập, xác suất một hợp số lọt lưới là:

$$
P(\text{error}) \le 4^{-k} = 2^{-2k}
$$

- Với `k = 40`: xác suất sai $\le 4^{-40} = 2^{-80} \approx 8.27 \times 10^{-25}$ (nhỏ hơn cả xác suất tia vũ trụ làm lật bit RAM!).

#### 3. Sàng đồng thời & Pipeline sinh Safe Prime 4 tầng (Dòng 301–470)

- **Bảng `SMALL_PRIMES[]` (Dòng 301–329):** 302 số nguyên tố lẻ từ `3` đến `1999`.
- **Hàm `passes_safe_prime_sieve(q, bitsize)` (Dòng 336–352):**
  ```cpp
  for (size_t i = 0; i < NUM_SMALL_PRIMES; i++) {
      uint32_t r = SMALL_PRIMES[i];
      if (bitsize <= 12 && r >= (1U << (bitsize - 2))) break;
      uint64_t rem = mod_small(q, r);
      if (rem == 0 || rem == static_cast<uint64_t>((r - 1) / 2)) {
          return false;
      }
  }
  return true;
  ```
  - **Đẳng thức sàng đồng thời (CỰC HAY ĐƯỢC KHEN):**
    - Nếu $q \bmod r = 0$ ⇒ `r | q` ⇒ `q` là hợp số.
    - Xét điều kiện `r | p` với $p = 2q + 1$:

$$
2q + 1 \equiv 0 \pmod r \iff 2q \equiv r - 1 \pmod r \iff q \equiv \frac{r - 1}{2} \pmod r
$$

    - Phép chia cho 2 hợp lệ vì `r` lẻ nên $\gcd(2, r) = 1$. Chỉ cần gọi **1 lần** `mod_small(q, r)` là sàng đồng thời cả `q` và `p`, loại bỏ ngay **~98.56%** ứng viên hợp số!
  - **Dòng 341 (`if (bitsize <= 12 && r >= (1U << (bitsize - 2))) break;`):** Bảo vệ khi test `bitsize` nhỏ (ví dụ `q` chỉ khoảng 500) để không loại nhầm khi chính `q == r` (khi đó `q % r == 0` nhưng `q` lại là số nguyên tố!).
- **Hàm `miller_rabin_base2(n)` (Dòng 355–391):** Chạy nhanh đúng 1 vòng Miller-Rabin với cơ sở cố định `a = 2`, loại `> 99.99%` hợp số còn sót sau sàng.
- **Hàm `generate_safe_prime(ctx, bitsize, rounds)` (Dòng 411–470) — Kiến trúc lọc 4 tầng:**
  1. **Khởi tạo ứng viên (Dòng 432–433):**
     ```cpp
     big_t q = random_bits(ctx, bitsize - 1);
     q.set_bit(0);
     ```
     - Gọi `b = bitsize`. Vì `q` có đúng `b - 1` bit và lẻ, ta có $2^{b-2} + 1 \le q \le 2^{b-1} - 1$.
     - Do đó $p = 2q + 1$ thỏa mãn $2^{b-1} + 3 \le p \le 2^{b} - 1$ ⇒ `p` **luôn lẻ** và **luôn có chính xác `bitsize` bit** (không bao giờ bị 511 hay 513 bit!).
  2. **Tầng 1 (Dòng 436):** `passes_safe_prime_sieve(q, bitsize)` — loại ~98.56% ứng viên.
  3. **Tầng 2 (Dòng 443):** `miller_rabin_base2(q)` — kiểm tra nhanh 1 vòng cho `q` (chưa cần tính `p`).
  4. **Tầng 3 (Dòng 450–451):** Tính `p = (q << 1) + one`, chạy `miller_rabin_base2(p)`.
  5. **Tầng 4 (Dòng 458–465):** Chỉ khi **cả `q` và `p` đều qua hết 3 tầng trên**, mới chạy đủ `rounds` (40) vòng Miller-Rabin ngẫu nhiên cho cả `q` và `p` ⇒ giảm số lần chạy 40 vòng từ hàng chục lần xuống đúng **1 lần duy nhất** cho mỗi safe prime tìm được!
- **Hàm `generate_private_key(ctx, p)` (Dòng 473–482):** Gọi `random_range(ctx, 2, p - 2)`.
- **Số liệu Benchmark thực tế (đã ghi trong báo cáo):**
  - 512-bit: trung bình **~0.26–0.85 s** (~58.000 ứng viên thử, sàng loại **98.56%**).
  - 768-bit: trung bình **~1.32–4.14 s** (sàng loại **98.58%**).
  - 1024-bit: trung bình **~1.58–4.52 s** (sàng loại **98.55%**).

### B. Bộ câu hỏi phản biện & vấn đáp — Phần 2.5

> **Q5.1: Cho một ví dụ số nhỏ minh họa Modulo Bias nếu không dùng Rejection Sampling!**
> - **Đáp:** Giả sử ta có bộ sinh đều 3 bit (trả về `0..7`, gồm 8 giá trị) và muốn sinh số ngẫu nhiên trong `[0, 4]` (gồm 5 giá trị). Nếu dùng phép dư `r % 5`:
>   - `0` nhận từ `{0, 5}` (xác suất `2/8 = 25%`)
>   - `1` nhận từ `{1, 6}` (xác suất `2/8 = 25%`)
>   - `2` nhận từ `{2, 7}` (xác suất `2/8 = 25%`)
>   - `3` chỉ nhận từ `{3}` (xác suất `1/8 = 12.5%`)
>   - `4` chỉ nhận từ `{4}` (xác suất `1/8 = 12.5%`)
>   Các số `0, 1, 2` xuất hiện **gấp đôi** `3, 4`! Với Rejection Sampling, nếu sinh ra `{5, 6, 7}` ta bỏ sinh lại ⇒ mỗi giá trị `0..4` có xác suất bằng nhau chính xác `1/5 = 20%`.
>
> **Q5.2: Trong `random_range`, vòng lặp `while (true)` có bao giờ chạy quá lâu hoặc lặp vô hạn không?**
> - **Đáp:** Về lý thuyết xác suất dừng bằng 1, còn trong thực tế vì `k = range.bit_length()` nên `range + 1 > 2^(k-1)`, xác suất chấp nhận ở mỗi lượt luôn `> 50%`. Xác suất phải thử quá 100 lần liên tiếp nhỏ hơn $2^{-100} \approx 7.8 \times 10^{-31}$ (bất khả thi), và số lần lặp kỳ vọng luôn `< 2`.
>
> **Q5.3: Số Carmichael là gì? Tại sao Fermat thất bại trên 561 mà Miller-Rabin lại bắt được?**
> - **Đáp:** Số Carmichael là hợp số lẻ `n` thỏa $a^{n-1} \equiv 1 \pmod n$ với mọi $\gcd(a, n) = 1$ (nhỏ nhất là `561 = 3 × 11 × 17`). Kiểm tra Fermat chỉ kiểm tra lũy thừa cuối $a^{560} \bmod 561$ nên gần như luôn trả nhầm "nguyên tố". Miller-Rabin phân tích $560 = 2^4 \cdot 35$ (`s = 4, d = 35`). Thử với `a = 2`:
>   - $2^{35} \bmod 561 = 263$ (`≠ 1`, `≠ 560`)
>   - $263^2 \bmod 561 = 166$
>   - $166^2 \bmod 561 = 67$
>   - $67^2 \bmod 561 = 1$ ⇒ gặp `1` mà số trước đó là `67` ($67 \not\equiv \pm 1 \pmod{561}$)! Đây là căn bậc hai không tầm thường của `1`, khẳng định chắc chắn `561` là hợp số!
>
> **Q5.4: Tại sao không dùng thuật toán tất định AKS (2002) cho đúng 100%, mà lại dùng thuật toán xác suất Miller-Rabin?**
> - **Đáp:** Dù AKS chứng minh bài toán `PRIMES` thuộc lớp **P** với độ phức tạp $\tilde{O}(\log^6 n)$, nhưng hằng số ẩn cực lớn (phải nhân đa thức bậc hàng triệu trên hệ số lớn), chậm hơn Miller-Rabin (`O(k * log^3 n)`) hàng triệu lần ở kích thước 512–1024 bit. Trong khi đó Miller-Rabin với `k = 40` có xác suất sai $\le 4^{-40} = 2^{-80}$ (thực tế cho số ngẫu nhiên 512-bit còn nhỏ hơn $2^{-160}$ theo định lý Damgård–Landrock–Pomerance), an toàn tuyệt đối trong thực tế mật mã.
>
> **Q5.5: Tại sao trong `generate_safe_prime` lại đặt kiểm tra `miller_rabin_base2(q)` trước rồi mới tính `p = 2q + 1` và kiểm tra `p`?**
> - **Đáp:** Hai lý do: (1) Nếu `q` đã là hợp số (xác suất `> 95%` các số lọt qua sàng nhỏ vẫn là hợp số!) thì ta loại ngay mà không cần tốn phép tính tạo `p` và không cần chạy lũy thừa mô-đun trên `p`; (2) `q` ít hơn `p` 1 bit nên tính toán nhanh hơn một chút. Thực tế trên benchmark 512-bit: ~840 ứng viên qua sàng → qua `base2(q)` chỉ còn ~34 số → qua `base2(p)` chỉ còn đúng **1 số**!
>
> **Q5.6: Có mẹo nào để `generate_safe_prime` sinh nhanh hơn nữa không (khi mở rộng lên 2048-bit)?**
> - **Đáp:** Có 3 hướng (nhóm đã phân tích trong Mục 6 báo cáo):
>   1. **Incremental Sieve (Bảng dư bước nhảy `O(1)`):** Thay vì gọi lại `mod_small` cho mọi ứng viên mới, tính bảng dư `rem[i] = q0 % SMALL_PRIMES[i]` một lần rồi tăng `q = q + 2`, cập nhật `rem[i] = (rem[i] + 2) % r` chỉ tốn phép cộng!
>   2. **Song song hóa đa luồng (`std::thread`):** Cho mỗi nhân CPU chạy 1 luồng với seed phân tách miền (domain-separated), luồng nào tìm thấy safe prime trước thì báo các luồng khác dừng.
>   3. **Phép nhân Montgomery:** Thay phép chia Knuth D trong `modular_exponentiation` bằng rút gọn Montgomery (chỉ dùng phép nhân và dịch bit).
>
> **Q5.7: Đẳng thức sàng đồng thời $q \equiv (r - 1)/2 \pmod r$ có dùng được cho `r = 2` không?**
> - **Đáp:** Không cần và không dùng cho `r = 2`, vì ta đã chủ động ép `q` lẻ (`q.set_bit(0)`) nên `q` luôn không chia hết cho 2, và `p = 2q + 1` đương nhiên luôn lẻ. Bảng `SMALL_PRIMES` của nhóm bắt đầu từ `3`, mọi `r` đều lẻ nên `(r - 1)/2` luôn là số nguyên chính xác!
>
> **Q5.8: Nếu chỉ biết $q \equiv 2 \pmod 3$, thì `p = 2q + 1` có chia hết cho 3 không? Áp dụng vào công thức sàng thế nào?**
> - **Đáp:** Với `r = 3`, `(r - 1)/2 = 1`. Khi $q \equiv 1 \pmod 3$ thì $2q + 1 \equiv 3 \equiv 0 \pmod 3$ ⇒ `3 | p`, bị loại! Khi $q \equiv 0 \pmod 3$ ⇒ `3 | q`, cũng bị loại! Vậy mọi cặp `(q, p)` với `q > 3` **bắt buộc phải thỏa** $q \equiv 2 \pmod 3$ (suy ra $p = 2q + 1 \equiv 2 \pmod 3$, và kết hợp `q` lẻ ⇒ $q \equiv 5 \pmod 6$, $p \equiv 11 \pmod{12}$!). Công thức tổng quát của nhóm đã tự động bao hàm quy luật này cho cả 302 số nguyên tố lẻ `< 2000`!

---

## 2.6. Module `main.cpp` — Điều phối Chương trình & Giao diện CLI

*(File dài 201 dòng — Phụ trách: Khang & Mạnh)*

### A. Giải thích chi tiết từng khối / từng dòng code

- **Dòng 14 (`#define _CRT_RAND_S`):** Đặt ở **dòng đầu tiên của toàn bộ chương trình**, trước cả `<iostream>` và `<cstdlib>`, để đảm bảo trên Windows MSVC/MinGW macro này có hiệu lực ngay khi `<stdlib.h>` được nạp lần đầu.
- **Dòng 25–29:** Thứ tự `#include` 5 module còn lại của Unity Build (`fips202.cpp` → `prng.cpp` → `bigint.cpp` → `dh.cpp` → `prime.cpp`).
- **Dòng 43–85 (Xử lý tham số dòng lệnh an toàn):**
  - Mặc định: `bit_size = 512`, `rounds = 40`, `use_fixed_seed = false`.
  - Dùng `std::strtoul` / `std::strtol` với con trỏ `char *end` kiểm tra `end == argv[i] || *end != '\0'` — tốt hơn `std::atoi` vì bắt được cả chuỗi rác như `"512abc"` hay chuỗi rỗng `""`.
  - Kiểm tra `--rounds` trong `[1, 1000]`.
  - Kiểm tra `--seed` dài đúng 64 ký tự hex (tương ứng 32 byte = 256 bit), dùng `std::isxdigit(static_cast<unsigned char>(...))` — ép kiểu `unsigned char` tránh Undefined Behavior khi `char` có dấu nhận giá trị âm (ký tự ngoài ASCII).
- **Dòng 87–94:** Nếu `bit_size < 512` thì in **cảnh báo** (nhưng vẫn cho chạy để tiện debug/test 64-bit, 128-bit); nếu `bit_size > MAX_PRIME_BITS` thì **chặn và báo lỗi** rõ ràng kèm hướng dẫn tăng `MAX_PRIME_BITS` trong `bigint.cpp` (tránh tràn bộ đệm 2048-bit).
- **Dòng 105–122 (Khởi tạo CSPRNG):**
  - Nếu có `--seed`: parse từng cặp 2 ký tự hex bằng `strtoul(..., 16)` vào mảng `uint8_t seed[32]`.
  - Nếu không có `--seed`: gọi `randombytes(seed, 32)` lấy 256 bit entropy thật từ hệ điều hành.
  - Gọi `prng_seed(&ctx, seed, sizeof(seed))` nạp seed vào SHAKE128.
- **Dòng 126–198 (5 bước trao đổi khóa + 4 chốt kiểm tra phòng thủ):**
  - **Bước `[1]` (Dòng 126–138):** Sinh `p = generate_safe_prime(&ctx, bit_size, rounds)`, đo thời gian bằng `std::chrono::high_resolution_clock`. **Chốt kiểm tra 1:** `p.bit_length() == bit_size && p.is_odd()`.
  - **Bước `[2]` (Dòng 140–150):** Chọn `g = choose_generator(p)`, tính `q = (p - 1) >> 1`. **Chốt kiểm tra 2:** `g != 1 && g^q mod p == 1`.
  - **Bước `[3]` (Dòng 153–157):** Sinh khóa bí mật `a, b = generate_private_key(&ctx, p)` trong `[2, p - 2]`.
  - **Bước `[4]` (Dòng 160–176):** Tính `A = g^a mod p`, `B = g^b mod p`, đo thời gian. **Chốt kiểm tra 3:** `is_valid_public_value(A, p) && is_valid_public_value(B, p)`.
  - **Bước `[5]` (Dòng 179–198):** Tính `s_alice = B^a mod p`, `s_bob = A^b mod p`, đo thời gian. **Chốt kiểm tra 4:** `matched = (s_alice == s_bob) && (s_alice > 1)`.

### B. Bộ câu hỏi phản biện & vấn đáp — Phần 2.6

> **Q6.1: Tại sao ở dòng 192 lại kiểm tra `(s_alice == s_bob) && (s_alice > big_t::from_u64(1))` mà không chỉ kiểm tra `s_alice == s_bob`?**
> - **Đáp:** Để phòng trường hợp hàm `modular_exponentiation` hoặc `generate_safe_prime` chưa cài đặt (trả về `0` hoặc `1`) dẫn đến `0 == 0` hoặc `1 == 1` mà vẫn báo thành công giả (false positive), đồng thời loại trừ trường hợp bí mật chung bị suy biến về phần tử đơn vị `1`.
>
> **Q6.2: Chạy chương trình với `--seed` cố định hai lần có ra cùng `p, a, b, s` không? Khi nào nên và không nên dùng `--seed`?**
> - **Đáp:** Ra kết quả **giống hệt nhau từng bit**, vì SHAKE128 là hàm tất định (cùng seed ⇒ cùng dòng byte đầu ra). Chế độ `--seed` chỉ dùng để **gỡ lỗi, kiểm thử chéo và tái hiện kết quả** (đề bài cho phép); trong môi trường thực tế tuyệt đối không được dùng seed cố định mà phải lấy từ `randombytes()` của hệ điều hành.
>
> **Q6.3: Tại sao phải truyền `static_cast<unsigned char>(fixed_seed_hex[k])` vào `std::isxdigit` ở dòng 75?**
> - **Đáp:** Theo chuẩn C/C++, hàm `<cctype>` như `std::isxdigit(int ch)` yêu cầu giá trị `ch` phải biểu diễn được bởi `unsigned char` hoặc bằng `EOF`. Nếu người dùng gõ ký tự có dấu tiếng Việt vào `--seed`, kiểu `char` có dấu trên Windows sẽ mang giá trị âm, truyền thẳng vào `isxdigit` sẽ gây **Undefined Behavior** (thậm chí crash trên MSVC debug).

---

## 2.7. Tình huống Live-Coding & Hỏi xoáy tổng hợp tại chỗ

Đây là 6 yêu cầu thực tế mà giảng viên rất hay yêu cầu sinh viên làm trực tiếp trên máy trong buổi vấn đáp:

| # | Yêu cầu đột xuất của thầy | Cách xử lý nhanh, chuẩn xác ngay tại chỗ |
| :--- | :--- | :--- |
| **1** | *"Em chạy thử sinh số nguyên tố 1024-bit cho thầy xem."* | Chạy ngay: `.\dh.exe --bits 1024 --rounds 40` (không cần sửa code, chạy trong ~2–5 giây). |
| **2** | *"Em sửa code để sinh được số 2048-bit xem nào?"* | Mở `bigint.cpp` dòng 183, đổi `MAX_PRIME_BITS = 1024` → `2048`, biên dịch lại bằng `g++ -std=c++14 -O2 -o dh.exe main.cpp`, rồi chạy `.\dh.exe --bits 2048`. *(Lưu ý nói trước với thầy: 2048-bit trên 1 luồng sẽ mất khoảng vài chục giây đến ~1–2 phút vì mật độ safe prime giảm theo tỉ lệ nghịch bình phương logarit).* |
| **3** | *"Em in thêm số nguyên tố Sophie Germain `q` và chứng minh `p = 2q + 1` có thật sự là số nguyên tố không?"* | Trong `main.cpp` ngay sau dòng 142 (`big_t q = (p - big_t::from_u64(1)) >> 1;`), thêm:<br>`std::cout << "    q = " << q.to_hex() << " (" << q.bit_length() << " bit)\n";`<br>`std::cout << "    MR(q)=" << is_probable_prime(&ctx, q, 40) << ", MR(p)=" << is_probable_prime(&ctx, p, 40) << "\n";` |
| **4** | *"Nếu thầy sửa `B` thành `p - 1` ngay trước bước kiểm tra thì chương trình em phản ứng sao?"* | Trong `main.cpp` dòng 169, tạm gán `B = p - big_t::from_u64(1);` rồi chạy lại → `is_valid_public_value(B, p)` lập tức phát hiện `SAI` và dừng chương trình với mã lỗi `1`, ngăn tính bí mật chung không an toàn! *(Xong nhớ Ctrl+Z trả lại như cũ).* |
| **5** | *"Chứng minh Miller-Rabin của em bắt được số Carmichael 561 xem nào?"* | Nếu thầy cho mở repo test, chạy `tests/test_prng_prime.exe` (đã test sẵn 561, 1105, 1729, 2465, 2821, 6601, 41041 và số Mersenne nguyên tố $2^{127}-1$). Hoặc thêm 1 dòng nhanh trong `main.cpp`: `std::cout << is_probable_prime(&ctx, big_t::from_u64(561), 40);` → in `0` (`false`). |
| **6** | *"Nếu thầy muốn chuyển sang in kết quả hệ thập phân thay vì hệ hex?"* | Đổi `.to_hex()` thành `.to_dec()` (hàm `to_dec()` nhóm đã cài sẵn tối ưu chia cho $10^{18}$ trong `bigint.cpp` dòng 101–128!). |

---

### Lời khuyên tâm lý cho buổi vấn đáp

1. **Bình tĩnh, trả lời thẳng vào trọng tâm (3 câu ngắn: Cái gì → Tại sao → Ở đâu trong code)** trước khi mở rộng thêm chi tiết.
2. **Đừng ngại mở code chỉ trực tiếp:** Khi thầy hỏi một cơ chế (như Knuth D, Rejection Sampling, sàng đồng thời), hãy vừa nói vừa bấm sang đúng file/dòng trong VS Code để chỉ — thầy đánh giá rất cao sinh viên thuộc vị trí code của mình.
3. **Nắm chắc số liệu thực nghiệm trong báo cáo** (512-bit ~0.26–0.85s, sàng loại 98.56%, Knuth D nhanh hơn chia nhị phân ~160 lần: 0.44 µs vs 72 µs, `modexp` 512-bit ~0.24 ms, crosscheck 30.000 + 50.016 phép chia + 4.452 lũy thừa với Python 0 sai lệch) để dẫn chứng thuyết phục.
4. **Nếu gặp câu hỏi mở rộng chưa cài** (như Montgomery Multiplication, Montgomery Ladder, đa luồng `std::thread`, Baillie–PSW), trả lời thẳng thắn: *"Hiện tại chương trình chưa cài phần này và nhóm đã tự phân tích rõ trong Mục 6 — Hạn chế và Hướng cải thiện của báo cáo, cụ thể hướng làm sẽ là..."* — cách trả lời này thể hiện tư duy kỹ thuật chín chắn và trung thực.

**Chúc bạn và Nhóm 18 vấn đáp thật tự tin và đạt điểm tối đa!**

---

# PHẦN 3: GIẢI THÍCH TỪNG DÒNG CODE CHI TIẾT CỦA TOÀN BỘ 6 FILE MÃ NGUỒN

Phần này đi qua **từng dòng / từng câu lệnh theo đúng thứ tự từ dòng 1 đến dòng cuối** của toàn bộ 6 file trong `project_01_source/`. Khi vấn đáp, thầy chỉ bất kỳ dòng nào trong bất kỳ file nào, bạn chỉ cần tra đúng số dòng dưới đây là giải thích trôi chảy ngay lập tức.

---

## 3.1. File `fips202.cpp` (850 dòng) — Lõi Keccak / SHA-3 / SHAKE128

*(Gộp nguyên văn từ `fips202.h` + `fips202.c` trong bộ mã nguồn mẫu Kyber/PQ-Crystals giảng viên cung cấp — KHÔNG chỉnh sửa thuật toán, chỉ gộp để đáp ứng quy định chỉ nộp `.cpp`.)*

### Phần Header gộp (Dòng 1–74)
- **`Dòng 7–8` (`#ifndef FIPS202_CPP` / `#define FIPS202_CPP`):** Include guard cho mô hình Unity Build, đảm bảo nếu nhiều file `.cpp` cùng `#include "fips202.cpp"` thì nội dung chỉ được nạp đúng 1 lần.
- **`Dòng 11–12` (`#ifndef FIPS202_H` / `#define FIPS202_H`):** Include guard gốc của file header `fips202.h`.
- **`Dòng 14–15` (`#include <stddef.h>`, `#include <stdint.h>`):** Nạp các kiểu chuẩn `size_t`, `uint8_t`, `uint64_t`.
- **`Dòng 17–19` và `69–71` (`#ifdef __cplusplus extern "C" { ... }`):** Bảo trình biên dịch C++ giữ quy ước đặt tên hàm (linkage) kiểu C (không name-mangling) cho các hàm FIPS 202.
- **`Dòng 21–24` (Các hằng số `RATE` tính bằng byte):**
  - `SHAKE128_RATE = 168` byte (`1344` bit) ⇒ `capacity = 1600 - 1344 = 256` bit (bảo mật 128-bit).
  - `SHAKE256_RATE = 136` byte (`1088` bit) ⇒ `capacity = 512` bit (bảo mật 256-bit).
  - `SHA3_256_RATE = 136` byte; `SHA3_512_RATE = 72` byte (`576` bit, `capacity = 1024` bit).
- **`Dòng 26` (`#define FIPS202_NAMESPACE(s) pqcrystals_kyber_fips202_ref_##s`):** Macro gắn tiền tố namespace vào tên hàm để tránh đụng độ tên với các thư viện khác.
- **`Dòng 28–32` (`typedef struct { uint64_t s[25]; unsigned int pos; } keccak_state;`):**
  - `s[25]`: Ma trận trạng thái 3 chiều `5 × 5 × 64 = 1600` bit (200 byte) của Keccak.
  - `pos`: Con trỏ byte hiện tại trong vùng `rate` (`0 .. r`), cho biết đã hấp thụ (absorb) hoặc vắt (squeeze) tới byte nào của block hiện hành.
- **`Dòng 34–67`:** Khai báo nguyên mẫu hàm (prototype) cho nhóm API tăng dần (`init`, `absorb`, `finalize`, `squeeze`, `absorb_once`, `squeezeblocks`) của `shake128`, `shake256`, và API một lần của `shake128`, `shake256`, `sha3_256`, `sha3_512`.

### Tiện ích nạp/xuất 64-bit & Hằng số vòng (Dòng 81–147)
- **`Dòng 84` (`#define NROUNDS 24`):** Keccak-f[1600] chạy cố định **24 vòng** hoán vị.
- **`Dòng 85` (`#define ROL(a, offset) ((a << offset) ^ (a >> (64-offset)))`):** Phép **xoay vòng trái bit** (Rotate Left) trên thanh ghi `uint64_t`. Dịch trái `offset` bit rồi XOR (tương đương OR vì 2 phần bit không chồng nhau) với `offset` bit cao bị đẩy vòng sang phải.
- **`Dòng 96–104` (`load64(const uint8_t x[8])`):** Ghép 8 byte liên tiếp thành 1 số `uint64_t` theo thứ tự **Little-Endian**: `r |= (uint64_t)x[i] << 8*i`.
- **`Dòng 114–119` (`store64(uint8_t x[8], uint64_t u)`):** Tách 1 số `uint64_t` thành 8 byte Little-Endian: `x[i] = u >> 8*i` (phép gán vào `uint8_t` tự cắt lấy 8 bit thấp nhất).
- **`Dòng 122–147` (`KeccakF_RoundConstants[24]`):** 24 hằng số vòng 64-bit sinh từ thanh ghi dịch phản hồi tuyến tính LFSR theo chuẩn NIST FIPS 202, dùng trong bước $\iota$ (Iota) để phá vỡ tính đối xứng giữa các vòng và các lane.

### Hoán vị lõi `KeccakF1600_StatePermute(uint64_t state[25])` (Dòng 156–418)
- **`Dòng 160–171`:** Khai báo 25 biến cục bộ `Aba..Asu` (biểu diễn ma trận 5×5 hiện tại), 25 biến `Eba..Esu` (ma trận 5×5 sau 1 vòng), 5 biến `BCa..BCu` (tổng XOR cột / giá trị trung gian), và 5 biến `Da..Du` (hiệu ứng cột $\theta$). Để tất cả trong biến cục bộ giúp trình biên dịch giữ chúng trên thanh ghi CPU thay vì truy cập RAM liên tục.
- **`Dòng 174–198` (`copyFromState`):** Nạp 25 phần tử `state[0..24]` vào 25 biến thanh ghi `Aba..Asu`.
- **`Dòng 200–390` (Vòng lặp `for (round = 0; round < NROUNDS; round += 2)` — Kỹ thuật Loop Unrolling 2 vòng/lượt):**
  - Chạy **2 vòng liền nhau trong mỗi lượt** (vòng chẵn `round` biến đổi `A -> E`, vòng lẻ `round + 1` biến đổi `E -> A`), giúp loại bỏ hoàn toàn bước copy ngược `E -> A` sau mỗi vòng!
  - **Trong mỗi vòng (VD dòng 202–294 cho vòng `round`, và dòng 297–389 cho vòng `round + 1`):** thực hiện gộp 5 bước chuẩn Keccak ($\theta, \rho, \pi, \chi, \iota$):
    1. **Bước $\theta$ (Theta — Dòng 202–213):** Tính parity (XOR) của từng cột (`BCa..BCu`), sau đó tính `Da = BCu ^ ROL(BCe, 1)` (tương tự `De..Du`) rồi XOR vào từng lane (VD `Aba ^= Da`). Tác dụng: khuếch tán tuyến tính giữa các cột.
    2. **Bước $\rho$ (Rho) & $\pi$ (Pi — Dòng 215–224, 232–241, ...):** Xoay vòng bit từng lane theo các hằng số góc chuẩn (`44, 43, 21, 14, 28, 20, ...`) bằng `ROL(...)` đồng thời hoán vị vị trí lane sang hàng/cột mới (gộp trực tiếp khi gán vào `BCa..BCu`). Tác dụng: khuếch tán mạnh giữa các bit và các lane.
    3. **Bước $\chi$ (Chi — Dòng 225, 227–230, ...):** Phép biến đổi **phi tuyến duy nhất** của Keccak: `Eba = BCa ^ ((~BCe) & BCi)` (tương đương lật bit nếu 2 bit lân cận là `0` và `1`). Tác dụng: tạo tính phi tuyến chống thám mã tuyến tính và vi sai.
    4. **Bước $\iota$ (Iota — Dòng 226 và dòng 321):** XOR `KeccakF_RoundConstants[round]` vào lane đầu tiên `(0, 0)` (`Eba` ở vòng chẵn, `Aba` ở vòng lẻ) để phá vỡ tính đối xứng vòng.
- **`Dòng 393–417` (`copyToState`):** Ghi 25 thanh ghi `Aba..Asu` trở lại mảng `state[0..24]`.

### Cơ chế Sponge: Init, Absorb, Finalize, Squeeze (Dòng 427–588)
- **`Dòng 427–432` (`keccak_init`):** Khởi tạo `s[0..24] = 0`.
- **`Dòng 447–467` (`keccak_absorb` — hấp thụ tăng dần):**
  - `Dòng 455–461`: Khi dữ liệu còn lại `pos + inlen >= r` (đủ lấp đầy 1 block `r` byte), XOR từng byte vào `s[i/8]` ở vị trí byte `8 * (i % 8)`, giảm `inlen -= r - pos`, gọi `KeccakF1600_StatePermute(s)` để trộn toàn trạng thái, rồi đặt lại `pos = 0`.
  - `Dòng 463–466`: Phần dữ liệu lẻ chưa đủ 1 block được XOR tiếp từ `pos` đến `pos + inlen`, trả về vị trí `pos` mới.
- **`Dòng 479–483` (`keccak_finalize` — đệm pad10*1):**
  - `Dòng 481`: XOR byte phân tách miền `p` (`0x1F` cho SHAKE, `0x06` cho SHA-3) vào ngay sau byte dữ liệu cuối tại `pos`.
  - `Dòng 482`: XOR bit cao nhất của byte cuối vùng rate (`s[r/8 - 1] ^= 1ULL << 63`) để đóng khung padding `10*1`.
- **`Dòng 500–520` (`keccak_squeeze` — vắt byte ngẫu nhiên tăng dần):**
  - `Dòng 508`: Lặp khi vẫn còn byte cần xuất (`while (outlen)`).
  - `Dòng 509–512`: Nếu `pos == r` (đã vắt hết `r` byte của block hiện tại, hoặc mới `finalize` xong), gọi `KeccakF1600_StatePermute(s)` tạo block 168 byte mới và reset `pos = 0`.
  - `Dòng 513–516`: Đọc từng byte `s[i/8] >> 8*(i%8)` ghi vào `*out++` cho đến khi hết block `r` hoặc đủ `outlen`; cập nhật `outlen` và `pos`.
- **`Dòng 535–588` (`keccak_absorb_once`, `keccak_squeezeblocks`):** Phiên bản không tăng dần (hấp thụ toàn bộ input 1 lần và vắt theo từng khối `r` byte hoàn chỉnh).

### Các hàm bao ngoài (Wrapper API) (Dòng 597–850)
- **`Dòng 597–643` (`shake128_init`, `shake128_absorb`, `shake128_finalize`, `shake128_squeeze`):** Các hàm **được `prng.cpp` gọi trực tiếp**:
  - `shake128_init` (597–601): gọi `keccak_init(state->s)` và `state->pos = 0`.
  - `shake128_absorb` (612–615): gọi `keccak_absorb` với `SHAKE128_RATE = 168`.
  - `shake128_finalize` (624–628): gọi `keccak_finalize(..., 0x1F)` và đặt `state->pos = SHAKE128_RATE` để lần `squeeze` đầu tiên lập tức hoán vị `KeccakF1600`.
  - `shake128_squeeze` (640–643): gọi `keccak_squeeze` với `SHAKE128_RATE = 168`.
- **`Dòng 654–848`:** Các wrapper tương ứng cho `shake128_absorb_once`, `shake128_squeezeblocks`, họ `shake256_*` (`rate = 136`, domain `0x1F`), `sha3_256` (`rate = 136`, domain `0x06`, xuất 32 byte), `sha3_512` (`rate = 72`, domain `0x06`, xuất 64 byte). Giữ nguyên đầy đủ từ thư viện chuẩn của giảng viên.
- **`Dòng 850` (`#endif // FIPS202_CPP`):** Đóng include guard.

---

## 3.2. File `prng.cpp` (129 dòng) — CSPRNG & Nguồn Entropy OS

*(Gộp từ `prng.h` + `prng.cpp` mẫu, được Minh port sang Windows và vá 2 lỗi quan trọng.)*

### Include Guard, Khai báo Windows `rand_s` & Thư viện (Dòng 14–40)
- **`Dòng 14–15` (`#ifndef PRNG_CPP` / `#define PRNG_CPP`):** Include guard Unity Build.
- **`Dòng 17–27` (Khối `#ifdef _WIN32`):**
  - `Dòng 18–20`: Nếu chưa định nghĩa `_CRT_RAND_S` thì định nghĩa để kích hoạt `rand_s` trong CRT Windows.
  - `Dòng 21`: Nạp `<stdlib.h>`.
  - `Dòng 22–26`: Khai báo tường minh `extern "C" _CRTIMP int __cdecl rand_s(unsigned int*);` (nếu `_CRTIMP` có định nghĩa, khớp với `dllimport` của MinGW-w64 UCRT, tránh cảnh báo `redeclared without dllimport attribute`; nhánh `#else` khai báo không có `_CRTIMP`). Đoạn này đảm bảo dù file gọi có `#include <iostream>` trước `prng.cpp`, trình biên dịch vẫn luôn thấy `rand_s`.
- **`Dòng 29–33`:** Nạp các header C chuẩn: `<stdint.h>`, `<stddef.h>`, `<stdlib.h>`, `<stdio.h>` (cho `fprintf`), `<errno.h>` (cho `EINTR` trên Linux).
- **`Dòng 35–37` (`#ifndef _WIN32 #include <sys/random.h> #endif`):** Trên Linux/macOS, nạp `<sys/random.h>` để dùng syscall `getrandom()`.
- **`Dòng 39` (`#include "fips202.cpp"`):** Nạp lõi Keccak/SHAKE128.

### Cấu trúc dữ liệu & Khai báo hàm (Dòng 42–51)
- **`Dòng 42–45` (`typedef struct { keccak_state sponge; } prng_ctx;`):** Ngữ cảnh bộ sinh số ngẫu nhiên — bọc trọn 1 trạng thái `keccak_state` (200 byte + `pos`). Dùng struct giúp hỗ trợ nhiều luồng/ngữ cảnh PRNG độc lập nếu mở rộng đa luồng.
- **`Dòng 47–51`:** Prototype 5 hàm công khai: `randombytes`, `prng_seed`, `prng_next_u16`, `prng_next_u32`, `prng_next_u64`.

### Hàm `randombytes(uint8_t *out, size_t outlen)` (Dòng 58–90)
- **`Dòng 58`:** Nhận con trỏ buffer đầu ra `out` và độ dài `outlen` (đã sửa từ `uint8_t` của mẫu sang `size_t` để không bị trần 255 byte).
- **Nhánh Windows (`#ifdef _WIN32`, Dòng 60–76):**
  - `Dòng 61`: Lặp cho đến khi ghi đủ `outlen` byte (`while (outlen > 0)`).
  - `Dòng 63–68`: Khởi tạo `unsigned int r = 0;`, gọi `rand_s(&r)` (bên dưới gọi `RtlGenRandom` của nhân Windows). Nếu trả về khác `0` (lỗi lấy entropy OS), in thông báo ra `stderr` và gọi `abort()` ngay lập tức (nguyên tắc **fail-closed**: thà dừng chương trình còn hơn sinh khóa từ entropy rỗng!).
  - `Dòng 69`: Tính số byte cần chép trong lượt này: `chunk = (outlen < sizeof(r)) ? outlen : sizeof(r)` (tối đa 4 byte, xử lý gọn trường hợp `outlen` không chia hết cho 4).
  - `Dòng 70–73`: Tách từng byte của `r` theo Little-Endian `(r >> (8 * i)) & 0xFFU` ghi vào `out[i]`.
  - `Dòng 74–75`: Dịch con trỏ `out += chunk` và giảm `outlen -= chunk`.
- **Nhánh Linux/macOS (`#else`, Dòng 77–89):**
  - `Dòng 78–81`: Lặp `while (outlen > 0)`, gọi `ret = getrandom(out, outlen, 0)` (cờ `0` dùng `/dev/urandom` CSPRNG của nhân, tự chờ nếu bể entropy chưa khởi tạo xong lúc boot).
  - `Dòng 82–83`: Nếu bị tín hiệu hệ thống ngắt (`ret == -1 && errno == EINTR`), quay lại gọi tiếp `continue`.
  - `Dòng 84–85`: Nếu lỗi nghiêm trọng khác (`ret < 0`), gọi `abort()`.
  - `Dòng 86–87`: Tịnh tiến `out += ret` và giảm `outlen -= ret` (vì `getrandom` có thể trả về ít hơn `outlen` byte trong 1 lần gọi).

### Các hàm khởi tạo & sinh số nguyên ngẫu nhiên (Dòng 92–129)
- **`Dòng 92–97` (`prng_seed`):**
  - `Dòng 94`: `shake128_init(&ctx->sponge)` — xóa trắng trạng thái 1600 bit.
  - `Dòng 95`: `shake128_absorb(&ctx->sponge, seed, seedlen)` — hấp thụ toàn bộ `seed` (32 byte = 256 bit).
  - `Dòng 96`: `shake128_finalize(&ctx->sponge)` — đóng pha hấp thụ, sẵn sàng vắt byte ngẫu nhiên.
- **`Dòng 99–105` (`prng_next_u16`):**
  - `Dòng 101–102`: Vắt 2 byte vào `uint8_t buf[2]` bằng `shake128_squeeze`.
  - `Dòng 103–104`: Ép kiểu từng byte sang `uint16_t` rồi ghép Little-Endian `buf[0] | (buf[1] << 8)`.
- **`Dòng 107–115` (`prng_next_u32`):**
  - `Dòng 109–110`: Vắt 4 byte vào `buf[4]`.
  - `Dòng 111–114`: **Quan trọng** — ép tường minh `static_cast<uint32_t>(buf[i])` **trước** khi dịch trái `8, 16, 24` bit để loại bỏ Undefined Behavior tràn bit dấu `int` 32-bit ở code mẫu gốc.
- **`Dòng 117–127` (`prng_next_u64`):**
  - `Dòng 119–120`: Vắt 8 byte vào `buf[8]`.
  - `Dòng 121–126`: Khởi tạo `uint64_t ret = 0`, lặp `i = 0..7` ghép `ret |= static_cast<uint64_t>(buf[i]) << (8 * i)` và trả về `ret`. Đây là hàm được `prime.cpp` gọi trực tiếp để đổ dữ liệu vào từng limb 64-bit của `big_t`.
- **`Dòng 129` (`#endif // PRNG_CPP`):** Đóng include guard.

---

## 3.3. File `bigint.cpp` (509 dòng) — Hệ thống Số lớn & Chia Knuth Algorithm D

*(Khang phụ trách dòng 1–348; Mạnh phụ trách phần chia Knuth D dòng 350–506.)*

### Phần 1: Định nghĩa kiểu & Constructor (Dòng 13–33)
- **`Dòng 13–14`:** Include guard `BIGINT_CPP`.
- **`Dòng 16–19`:** Nạp `<stdint.h>`, `<stddef.h>`, `<stdio.h>` (cho `std::snprintf`), `<string>` (cho `std::string`).
- **`Dòng 21` (`__extension__ typedef unsigned __int128 uint128_t;`):** Định nghĩa kiểu 128-bit không dấu nội tại của GCC/Clang; `__extension__` triệt tiêu cảnh báo `-Wpedantic`.
- **`Dòng 23–26` (`template <size_t N> struct uint_t { uint64_t digits[N]; ... };`):** Struct template cấp phát tĩnh `N` limb 64-bit trên Stack theo thứ tự Little-Endian (`digits[0]` thấp nhất).
- **`Dòng 29–33` (`uint_t()`):** Constructor mặc định gán toàn bộ `digits[0..N-1] = 0` để tránh rác bộ nhớ.

### Phần 2: Khởi tạo & Chuyển đổi I/O (Dòng 36–128)
- **`Dòng 36–41` (`from_u64(uint64_t v)`):** Tạo `uint_t r` (mọi limb bằng 0), gán `r.digits[0] = v`, trả về `r`.
- **`Dòng 44–80` (`from_hex(const std::string &s)`):**
  - `Dòng 46–50`: Khởi tạo `r = 0`; nếu chuỗi bắt đầu bằng `"0x"` hoặc `"0X"` thì đặt `start = 2`.
  - `Dòng 52–60`: Tạo chuỗi `clean` (`reserve` trước để tối ưu cấp phát), chỉ chép các ký tự hex `0-9`, `a-f`, `A-F`. Nếu `clean.empty()` thì trả về `0`.
  - `Dòng 63–65`: Khởi tạo `len = clean.length()`, `limb_idx = 0`. Lặp khi còn ký tự (`len > 0`) và chưa đầy mảng (`limb_idx < N`).
  - `Dòng 66–68`: Tính độ dài cụm tối đa 16 ký tự hex từ cuối chuỗi (`chunk_len = (len >= 16) ? 16 : len`, `chunk_start = len - chunk_len`) và trích `chunk`.
  - `Dòng 69–75`: Khởi tạo `val = 0`; với mỗi ký tự `c` trong `chunk`, dịch trái `val <<= 4` rồi OR giá trị `0..15` tương ứng vào 4 bit thấp.
  - `Dòng 76–77`: Ghi `val` vào `r.digits[limb_idx++]`, lùi `len = chunk_start` để đọc cụm 16 ký tự kế tiếp sang trái.
- **`Dòng 82–99` (`to_hex()`):**
  - `Dòng 84–88`: Duyệt ngược `top` từ `N - 1` xuống `0` tìm limb cao nhất khác `0`. Nếu `top < 0` trả về `"0"`.
  - `Dòng 90–92`: In limb cao nhất bằng `"%llx"` (không số 0 thừa ở đầu) vào `s`.
  - `Dòng 94–97`: Duyệt các limb thấp hơn `top - 1` xuống `0`, in mỗi limb bằng `"%016llx"` (bắt buộc đệm đủ 16 ký tự hex) nối vào `s`.
- **`Dòng 101–128` (`to_dec()`):**
  - `Dòng 103`: Nếu bằng `0` trả về `"0"`.
  - `Dòng 105–107`: Đặt cơ số `BASE10 = 1000000000000000000ULL` ($10^{18}$), sao chép bản thân sang `tmp`, chuỗi kết quả `s`.
  - `Dòng 109–115`: Lặp khi `!tmp.is_zero()`: chia `tmp` cho `BASE10` từ limb `N - 1` xuống `0` bằng `uint128_t`: `cur = (rem << 64) | tmp.digits[i]`, cập nhật `tmp.digits[i] = cur / BASE10`, `rem = cur % BASE10`.
  - `Dòng 117–125`: Lấy phần dư `chunk` (18 chữ số thập phân). Nếu `tmp.is_zero()` (đây là khối cao nhất) thì format `"%llu"` (không đệm 0 đầu); ngược lại format `"%018llu"` (đệm đủ 18 chữ số) rồi ghép vào **trước** chuỗi `s` (`s = std::string(buf) + s`).

### Phần 3: Tiện ích Bit & Định nghĩa `big_t` (Dòng 130–185)
- **`Dòng 130–136` (`is_zero()`):** Lặp `0..N-1`; nếu bất kỳ `digits[i] != 0` trả về `false`; hết vòng trả `true`.
- **`Dòng 138` (`is_odd()`):** Trả về `(digits[0] & 1) != 0` (`O(1)`).
- **`Dòng 141–158` (`bit_length()`):**
  - `Dòng 143–147`: Tìm `top` là limb cao nhất khác 0; nếu `top < 0` trả về `0`.
  - `Dòng 149–151` (GCC/Clang): Gọi `__builtin_clzll(digits[top])` đếm số bit 0 đầu của limb cao nhất (an toàn vì `digits[top] != 0`), trả về `top * 64 + (64 - lz)`.
  - `Dòng 152–157` (Fallback trình biên dịch khác): Đếm bằng vòng lặp `while (v > 0) { bits++; v >>= 1; }`.
- **`Dòng 160–166` (`test_bit(size_t i)`):** Tính `limb = i / 64`; nếu `limb >= N` trả `false`; tính `bit = i % 64`, trả `((digits[limb] >> bit) & 1ULL) != 0`.
- **`Dòng 168–174` (`set_bit(size_t i)`):** Tính `limb = i / 64`; nếu `limb < N` thì bật bit bằng `digits[limb] |= (1ULL << (i % 64))`.
- **`Dòng 177–185`:** Định nghĩa các bí danh tiện dụng (`uint512_t`, `uint1024_t`, `uint2048_t`) và hằng cấu hình `MAX_PRIME_BITS = 1024`, `BIG_LIMBS = 2 * MAX_PRIME_BITS / 64 = 32`, `typedef uint_t<BIG_LIMBS> big_t`.

### Phần 4: Các toán tử So sánh (Dòng 188–217)
- **`Dòng 188–195` (`operator==`):** Duyệt `i = 0..N-1`, gặp `a.digits[i] != b.digits[i]` trả `false`, hết vòng trả `true`.
- **`Dòng 197–198` (`operator!=`):** Trả `!(a == b)`.
- **`Dòng 200–208` (`operator<`):** Duyệt ngược `i = N - 1` xuống `0`: nếu `a.digits[i] < b.digits[i]` trả `true`; nếu `a.digits[i] > b.digits[i]` trả `false`. Hết vòng (bằng nhau) trả `false`.
- **`Dòng 210–217` (`>`, `<=`, `>=`):** Suy diễn trực tiếp từ `<`: `b < a`, `!(b < a)`, `!(a < b)`.

### Phần 5: Cộng, Trừ, Nhân, Dịch bit & `mod_small` (Dòng 221–348)
- **`Dòng 221–232` (`operator+`):**
  - `Dòng 224–225`: Khởi tạo `res = 0`, `uint128_t carry = 0`.
  - `Dòng 226–230`: Với từng limb `i = 0..N-1`: tính tổng 128-bit `sum = (uint128_t)a.digits[i] + b.digits[i] + carry`, lưu 64 bit thấp vào `res.digits[i]`, cập nhật `carry = sum >> 64`.
- **`Dòng 235–252` (`operator-`, giả định `a >= b`):**
  - `Dòng 238–239`: Khởi tạo `res = 0`, `uint128_t borrow = 0`.
  - `Dòng 240–242`: Tính `sub = (uint128_t)b.digits[i] + borrow` (dùng 128-bit để không tràn khi `b[i] = 2^64 - 1` và `borrow = 1`), ép `ai = a.digits[i]`.
  - `Dòng 243–245`: Nếu `ai >= sub`: trừ trực tiếp `ai - sub`, `borrow = 0`.
  - `Dòng 246–249`: Ngược lại: mượn $2^{64}$ (`(1 << 64) + ai - sub`), đặt `borrow = 1`.
- **`Dòng 256–284` (`operator*` — Schoolbook tối ưu):**
  - `Dòng 260–265`: Tìm độ dài limb thực `len_a`, `len_b` (bỏ limb 0 ở đầu); nếu một trong hai bằng 0 trả ngay `0`.
  - `Dòng 267–270`: Vòng ngoài `i = 0..len_a - 1`; nếu `a.digits[i] == 0` thì `continue` (tiết kiệm cả vòng trong!); khởi tạo `carry = 0`, `ai = a.digits[i]`.
  - `Dòng 271–276`: Vòng trong `j = 0..len_b - 1`; nếu `i + j >= N` thì `break` (chống ghi ngoài mảng); tính `prod = ai * b.digits[j] + res.digits[i + j] + carry` (tối đa $2^{128}-1$, không tràn), ghi 64 bit thấp vào `res.digits[i + j]`, giữ 64 bit cao làm `carry`.
  - `Dòng 277–281`: Lan truyền phần `carry` dư sang các limb `k = i + len_b` trở lên khi `carry > 0 && k < N`.
- **`Dòng 286–308` (`operator<<`):**
  - `Dòng 289–290`: `shift == 0` trả `a`; `shift >= N * 64` trả `0`.
  - `Dòng 292–294`: Tách `limb_shift = shift / 64`, `bit_shift = shift % 64`.
  - `Dòng 296–299`: Nhánh `bit_shift == 0` (tránh UB dịch 64 bit): chép `res.digits[i] = a.digits[i - limb_shift]`.
  - `Dòng 300–306`: Nhánh `bit_shift != 0`: phần thấp `low = a.digits[i - limb_shift] << bit_shift`, phần cao lấy các bit tràn từ limb dưới `high = (i > limb_shift) ? (a.digits[i - limb_shift - 1] >> (64 - bit_shift)) : 0`, ghép `res.digits[i] = low | high`.
- **`Dòng 310–332` (`operator>>`):** Đối xứng hoàn toàn với `<<`:
  - `Dòng 320–323`: Nhánh `bit_shift == 0`: `res.digits[i] = a.digits[i + limb_shift]`.
  - `Dòng 324–330`: Nhánh `bit_shift != 0`: `low = a.digits[i + limb_shift] >> bit_shift`, `high = (i + limb_shift + 1 < N) ? (a.digits[i + limb_shift + 1] << (64 - bit_shift)) : 0`, ghép `low | high`.
- **`Dòng 335–348` (`mod_small(const uint_t<N> &a, uint32_t m)`):**
  - `Dòng 338–341`: Nếu `m == 0` hoặc `a == 0` trả về `0`; tìm `top` là limb cao nhất khác 0.
  - `Dòng 343–347`: Sơ đồ Horner duyệt ngược `i = top..0`: `rem = ((rem << 64) | a.digits[i]) % m`, trả `static_cast<uint32_t>(rem)`.

### Phần 6: Phép chia số lớn `divmod`, `/`, `%` — Knuth Algorithm D (Dòng 367–509)
- **`Dòng 370–389` (Chuẩn bị & biên):**
  - `Dòng 370`: Khai báo `quo, rem` tạm (để hỗ trợ aliasing nếu `q` hoặc `r` trùng biến với `a` hoặc `b`).
  - `Dòng 373–379`: Đếm độ dài thực `n` của `b`; nếu `n == 0` (chia 0) gán `q = quo; r = rem; return;`.
  - `Dòng 381–385`: Nếu `a < b` trả ngay `q = 0`, `r = a`.
  - `Dòng 387–388`: Đếm độ dài thực `m_len` của `a` (chắc chắn `m_len >= n >= 1`).
- **`Dòng 390–399` (Đường tắt chia 1 limb `n == 1` — Short Division):**
  - `Dòng 392–393`: Lấy `d = b.digits[0]`, khởi tạo `uint128_t cur_rem = 0`.
  - `Dòng 394–398`: Duyệt ngược `i` từ `m_len - 1` xuống `0`: ghép `cur = (cur_rem << 64) | a.digits[i]`, ghi thương `quo.digits[i] = cur / d`, cập nhật dư `cur_rem = cur % d`.
  - `Dòng 399`: Lưu phần dư vào `rem.digits[0]`.
- **`Dòng 400–420` (Knuth D — Bước D1 Chuẩn hóa):**
  - `Dòng 403`: Tính `s = __builtin_clzll(b.digits[n - 1])` (số bit cần dịch trái để bit 63 của `v[n-1]` bằng 1).
  - `Dòng 404–405`: Khai báo mảng stack `v[N]` (chứa `b << s`) và `u[N + 1]` (chứa `a << s`, thêm 1 limb `u[m_len]` cho các bit tràn sang trái).
  - `Dòng 407–410`: Nếu `s == 0` (đã chuẩn hóa sẵn): chép thẳng `v`, `u` và đặt `u[m_len] = 0`.
  - `Dòng 411–420`: Nếu `s > 0`: dịch trái `b` sang `v` và `a` sang `u` đi `s` bit (lưu phần tràn cao nhất của `a` vào `u[m_len] = a.digits[m_len - 1] >> (64 - s)`).
- **`Dòng 422–428` (Chuẩn bị vòng lặp chính D2):**
  - `Dòng 422–424`: Định nghĩa `BASE = 1 << 64` (128-bit), lưu 2 limb cao nhất của số chia `v_hi = v[n - 1]`, `v_lo = v[n - 2]`.
  - `Dòng 427–428`: Duyệt ngược `j` từ `m_len - n` xuống `0` (mỗi lượt tính chính xác 1 limb 64-bit của thương `quo.digits[j]`).
- **`Dòng 430–440` (Bước D3 — Ước lượng và hiệu chỉnh thương thử $\hat{q}$):**
  - `Dòng 431–433`: Ghép 2 limb cao nhất `num = (u[j+n] << 64) | u[j+n-1]`, tính `q_hat = num / v_hi` và `r_hat = num % v_hi`.
  - `Dòng 434–439`: Vòng hiệu chỉnh (chạy tối đa 2 lần): trong khi `q_hat >= BASE` (thương thử tràn 64 bit) hoặc `q_hat * v_lo > ((r_hat << 64) | u[j+n-2])` (ước lượng quá lớn khi xét thêm limb thứ 2), giảm `q_hat--` và cộng bù `r_hat += v_hi`. Nếu `r_hat >= BASE` thì `break` (vừa biết chắc đã đạt, vừa tránh tràn `r_hat << 64`).
  - `Dòng 440`: Ép `q_hat` (lúc này chắc chắn `< 2^64`) về `uint64_t qh`.
- **`Dòng 442–462` (Bước D4 — Nhân và trừ `u[j..j+n] -= qh * v`):**
  - `Dòng 443`: Khởi tạo `mul_carry = 0` (nhớ phép nhân) và `borrow = 0` (mượn phép trừ).
  - `Dòng 444–456`: Vòng lặp `i = 0..n - 1`:
    - `Dòng 445–447`: Tính tích 128-bit `p = qh * v[i] + mul_carry`, tách `p_lo` (64 bit thấp) và `mul_carry` (64 bit cao).
    - `Dòng 449–455`: Trừ 2 nhịp trên `uint64_t` để không bị tràn `p_lo + borrow`: `t = x - p_lo` (mượn `b1 = (x < p_lo)`), `t2 = t - borrow` (mượn `b2 = (t < borrow)`), ghi `u[i+j] = t2`, gộp `borrow = b1 | b2`.
  - `Dòng 457–462`: Xử lý limb cao nhất `u[j + n]` trừ đi `mul_carry` và `borrow`, lưu hai cờ mượn `b1_top`, `b2_top`.
- **`Dòng 464–475` (Bước D5/D6 — Kiểm tra âm & Cộng bù Add-back):**
  - `Dòng 465`: Nếu `(b1_top | b2_top) != 0` nghĩa là phép trừ bị âm (`qh` lớn hơn thương thật đúng 1 đơn vị).
  - `Dòng 466–473`: Giảm `qh--`, rồi cộng trả lại `v[0..n-1]` vào `u[j..j+n-1]` với `add_carry`, cộng nốt `add_carry` vào `u[j + n]` (bit tràn mod $2^{64}$ triệt tiêu dấu âm).
  - `Dòng 475`: Ghi limb thương chuẩn xác `quo.digits[j] = qh`.
- **`Dòng 478–490` (Bước D8 — Khử chuẩn hóa phần dư & Trả kết quả):**
  - `Dòng 479–485`: Nếu `s == 0`, chép `u[0..n-1]` sang `rem.digits`. Nếu `s > 0`, dịch phải `u[0..n-1]` đi `s` bit: `rem.digits[i] = (u[i] >> s) | (u[i + 1] << (64 - s))` và `rem.digits[n - 1] = u[n - 1] >> s`.
  - `Dòng 488–489`: Gán kết quả cuối cùng `q = quo; r = rem;`.
- **`Dòng 492–506` (`operator/` và `operator%`):** Gọi `divmod(a, b, q, r)` rồi trả về `q` (cho `/`) hoặc `r` (cho `%`).
- **`Dòng 508` (`#endif // BIGINT_CPP`):** Đóng include guard.

---

## 3.4. File `dh.cpp` (170 dòng) — Số học Mô-đun & Trao đổi khóa Diffie-Hellman

*(Phụ trách: Mạnh + bộ 3 hàm đối chiếu pseudocode Khang bổ sung.)*

### Include Guard & Thư viện (Dòng 10–14)
- **`Dòng 10–11` (`#ifndef DH_CPP` / `#define DH_CPP`):** Include guard Unity Build.
- **`Dòng 13` (`#include <assert.h>`):** Nạp macro `assert` dùng để kiểm tra tiền điều kiện trong `modular_exponentiation`.
- **`Dòng 14` (`#include "bigint.cpp"`):** Nạp kiểu số lớn `uint_t<N>` và `big_t`.

### Phần 1: Các thuật toán theo `pseudocode-modular-operation.pdf` (Dòng 21–68)
- **`Dòng 22–32` (`AddMod(uint_t<N> x, uint_t<N> y, const uint_t<N> &p)`):**
  - `Dòng 25–26`: Rút gọn đầu vào `x = x % p; y = y % p;` đảm bảo `0 <= x, y < p`.
  - `Dòng 27`: Tính `p_minus_y = p - y` (chắc chắn dương vì `y < p`).
  - `Dòng 28–30`: Nếu `x >= p_minus_y` (tương đương `x + y >= p`), trả về `x - p_minus_y` (tương đương `x + y - p`) mà **không cần cộng `x + y` nên không bao giờ tràn n-bit**.
  - `Dòng 31`: Ngược lại `x + y < p`, cộng trực tiếp `return x + y;`.
- **`Dòng 36–49` (`MultMod(uint_t<N> x, const uint_t<N> &y, const uint_t<N> &p)`):**
  - `Dòng 39–41`: Khởi tạo `ret = 0`, rút gọn `x = x % p`, lấy số bit `n = y.bit_length()`.
  - `Dòng 42–47`: Duyệt từng bit `i` từ `0` đến `n - 1` của `y` (Double-and-Add):
    - `Dòng 43–45`: Nếu bit `i` của `y` là `1`, cộng dồn `ret = AddMod(ret, x, p)`.
    - `Dòng 46`: Nhân đôi `x = AddMod(x, x, p)` (tương đương tính $x \cdot 2^{i+1} \bmod p$).
  - `Dòng 48`: Trả về `ret = (x * y) % p`.
- **`Dòng 52–68` (`ExpMod(const uint_t<N> &x, const uint_t<N> &y, const uint_t<N> &p)`):**
  - `Dòng 55–57`: Nếu `p == 1` trả về `0`.
  - `Dòng 58–60`: Khởi tạo `ret = 1`, `base = x % p`, `n = y.bit_length()`.
  - `Dòng 61–66`: Duyệt từng bit `i = 0..n - 1` (Right-to-Left Square-and-Multiply): nếu bit `i` là `1` thì `ret = MultMod(ret, base, p)`; sau đó luôn bình phương `base = MultMod(base, base, p)`.
  - `Dòng 67`: Trả về `ret`.

### Phần 2: `modular_exponentiation` — Lũy thừa Mô-đun chính (Dòng 91–111)
- **`Dòng 91–93`:** Khai báo `modular_exponentiation(const big_t &base, const big_t &exp, const big_t &mod)` và tạo hằng `one = big_t::from_u64(1)`.
- **`Dòng 95–97`:** Nếu `mod == 0` (tránh chia 0) hoặc `mod == 1` (mọi số mod 1 bằng 0), trả về `big_t()` (`0`).
- **`Dòng 98` (`assert(mod.bit_length() <= MAX_PRIME_BITS);`):** Khẳng định `mod` nằm trong nửa dưới của `big_t` để tích `result * result` hoặc `result * b` (tối đa `2 * MAX_PRIME_BITS` bit) không bao giờ bị tràn.
- **`Dòng 100–101`:** Rút gọn `b = base % mod` (đưa về `[0, mod - 1]`), khởi tạo `result = 1`.
- **`Dòng 103–109` (Vòng lặp Left-to-Right Square-and-Multiply):**
  - `Dòng 103`: Lấy `nbits = exp.bit_length()` (nếu `exp == 0` thì `nbits = 0`, không vào vòng lặp, trả `1`).
  - `Dòng 104`: `for (size_t i = nbits; i-- > 0;)` — duyệt ngược từ `nbits - 1` xuống `0` an toàn với kiểu không dấu `size_t`.
  - `Dòng 105`: Luôn bình phương và lấy dư ngay: `result = (result * result) % mod` (dùng Schoolbook 128-bit + Knuth D).
  - `Dòng 106–108`: Nếu bit thứ `i` của `exp` là `1`, nhân thêm `b` và lấy dư ngay: `result = (result * b) % mod`.
- **`Dòng 110`:** Trả về `result`.

### Phần 3: `choose_generator` & `is_valid_public_value` (Dòng 133–170)
- **`Dòng 133–155` (`choose_generator(const big_t &p)`):**
  - `Dòng 135–140`: Tạo hằng `one`, `two`; nếu `p < 7` (safe prime tối thiểu hữu dụng là `7 = 2*3 + 1`) trả fallback `2`.
  - `Dòng 141–142`: Tính `p_minus_1 = p - 1` và `q = p_minus_1 >> 1` (chính là `(p - 1) / 2`).
  - `Dòng 144–153`: Thử lần lượt `h = 2, 3, ... < 1000000`:
    - `Dòng 145–146`: Chuyển `h` thành `hb`; nếu `hb >= p - 1` thì `break`.
    - `Dòng 148`: Tính bình phương `g = (hb * hb) % p` (thặng dư bậc hai; với `h = 2` và mọi `p > 5` thì `g = 4`).
    - `Dòng 149`: Nếu `g == 1` thì bỏ qua (`continue`).
    - `Dòng 150–152`: Kiểm tra `modular_exponentiation(g, q, p) == one`. Vì `q` nguyên tố và `g != 1`, đẳng thức này khẳng định bậc của `g` đúng bằng `q` ⇒ trả về `g` ngay ở lượt đầu tiên (`h = 2`, `g = 4`)!
  - `Dòng 154`: Fallback trả `2` nếu `p` không phải safe prime.
- **`Dòng 160–168` (`is_valid_public_value(const big_t &v, const big_t &p)`):**
  - `Dòng 162–164`: Nếu `p < 7` trả `false`.
  - `Dòng 165`: Kiểm tra `if (v < two || v > p - two) return false;` — loại `v = 0, 1, p - 1` và các giá trị `>= p`.
  - `Dòng 166–167`: Tính `q = (p - 1) >> 1` và trả về `modular_exponentiation(v, q, p) == one` — khẳng định `v` thuộc đúng nhóm con cấp nguyên tố `q` (chống tấn công nhóm con nhỏ).
- **`Dòng 170` (`#endif // DH_CPP`):** Đóng include guard.

---

## 3.5. File `prime.cpp` (484 dòng) — Rejection Sampling, Miller-Rabin & Sinh Safe Prime

*(Phụ trách: Lâm Duy Minh.)*

### Include Guard & Phụ thuộc (Dòng 15–20)
- **`Dòng 15–16` (`#ifndef PRIME_CPP` / `#define PRIME_CPP`):** Include guard Unity Build.
- **`Dòng 18–20`:** Nạp `"prng.cpp"`, `"bigint.cpp"`, `"dh.cpp"` (tất cả đều có include guard nên không bị nạp trùng).

### Phần 1: Sinh số ngẫu nhiên lớn & Rejection Sampling (Dòng 28–97)
- **`Dòng 28–55` (`static big_t random_upto_bits(prng_ctx *ctx, size_t bits)`):**
  - `Dòng 30–34`: Khởi tạo `res = 0`; nếu `bits == 0` trả về `0`.
  - `Dòng 36–40`: Chặn trên `bits <= BIG_LIMBS * 64` để không ghi vượt mảng `digits`.
  - `Dòng 42–46`: Tính số limb cần sinh `num_limbs = (bits + 63) / 64` (làm tròn lên); vòng `for` đổ `prng_next_u64(ctx)` vào từng `res.digits[i]`.
  - `Dòng 48–53`: Tính số bit lẻ ở limb cao nhất `rem_bits = bits % 64`; nếu `rem_bits != 0`, tạo mặt nạ `mask = (1ULL << rem_bits) - 1ULL` và AND `res.digits[num_limbs - 1] &= mask` để xóa các bit thừa cao hơn `bits - 1`. Trả về `res` phân phối đều tuyệt đối trên `[0, 2^bits - 1]`.
- **`Dòng 59–75` (`big_t random_bits(prng_ctx *ctx, size_t bits)`):**
  - `Dòng 61–70`: Xử lý `bits == 0` và chặn trên `max_bits`.
  - `Dòng 72–74`: Gọi `res = random_upto_bits(ctx, bits)` rồi ép bật bit cao nhất `res.set_bit(bits - 1)` ⇒ luôn nằm trong `[2^(bits-1), 2^bits - 1]`, có **đúng `bits` bit**.
- **`Dòng 79–97` (`big_t random_range(prng_ctx *ctx, const big_t &lo, const big_t &hi)`):**
  - `Dòng 81–84`: Nếu `hi <= lo` trả ngay `lo`.
  - `Dòng 86–87`: Tính độ rộng `range = hi - lo` và số bit nhỏ nhất `k = range.bit_length()` sao cho $2^{k-1} \le R \le 2^k - 1$.
  - `Dòng 89–96`: Vòng lặp Rejection Sampling: sinh `r = random_upto_bits(ctx, k)`; nếu `r <= range` thì chấp nhận và trả về `lo + r`; nếu `r > range` thì vứt bỏ và lặp lại (loại 100% modulo bias, trung bình `< 2` lượt).

### Phần 2: Miller-Rabin trên `uint64_t` (Dòng 103–195)
- **`Dòng 103–119` (`static uint64_t powmod_u64(base, exp, mod)`):**
  - `Dòng 105–108`: `mod == 1` trả `0`; khởi tạo `res = 1`, `b = base % mod`.
  - `Dòng 109–118`: Right-to-Left binary exponentiation, dùng `static_cast<uint128_t>(...)` khi nhân 2 số `uint64_t` để không tràn 64-bit trước khi `% mod`.
- **`Dòng 121–141` (`static bool miller_rabin_witness_u64(a, d, s, n)`):**
  - `Dòng 123–127`: Tính `x = powmod_u64(a, d, n)`; nếu `x == 1 || x == n - 1` trả `true` (đạt).
  - `Dòng 128–139`: Lặp `r = 1..s - 1`: bình phương `x = (x * x) % n` qua `uint128_t`; gặp `n - 1` trả `true`; gặp `1` trả `false` ngay (căn bậc hai không tầm thường của `1`).
  - `Dòng 140`: Không gặp `n - 1` ⇒ trả `false` (hợp số).
- **`Dòng 144–195` (`bool is_probable_prime_u64(ctx, n, rounds = 40)`):**
  - `Dòng 146–151`: Xử lý `n < 2` (`false`), `n == 2 || n == 3` (`true`), `n` chẵn (`false`).
  - `Dòng 153–159`: Phân tích `n - 1 = 2^s * d` bằng vòng `while ((d & 1ULL) == 0) { d >>= 1; s++; }`.
  - `Dòng 161–176`: Chuẩn bị `rounds` (mặc định 40) và mặt nạ `mask` cho Rejection Sampling trên `range = n - 3` (để chọn `a = 2 + r` trong `[2, n - 2]`).
  - `Dòng 178–194`: Lặp `rounds` lần: sinh `r` bằng Rejection Sampling (`do { r = prng_next_u64(ctx) & mask; } while (r > range);`), đặt `a = 2 + r`, gọi `miller_rabin_witness_u64(a, d, s, n)`; hễ sai 1 vòng trả `false` ngay, qua hết trả `true`.

### Phần 3: Miller-Rabin trên `big_t` (Dòng 202–294)
- **`Dòng 202–223` (`static size_t count_trailing_zeros(const big_t &x)`):**
  - `Dòng 204–221`: Duyệt từ limb thấp nhất `i = 0` lên `BIG_LIMBS - 1`, tìm limb đầu tiên khác `0`.
  - `Dòng 208–209` (GCC/Clang): Trả `i * 64 + __builtin_ctzll(x.digits[i])` (Count Trailing Zeros).
  - `Dòng 211–218` (Fallback): Đếm bằng vòng lặp `while ((v & 1ULL) == 0)`.
- **`Dòng 227–294` (`bool is_probable_prime(prng_ctx *ctx, const big_t &n, int rounds = 40)`):**
  - `Dòng 229–245`: Khởi tạo `one, two, three`; xử lý `n < 2` (`false`), `n == 2 || n == 3` (`true`), `!n.is_odd()` (`false`).
  - `Dòng 248–251`: Tính `n_minus_1 = n - 1`, `n_minus_2 = n - 2`, `s = count_trailing_zeros(n_minus_1)`, `d = n_minus_1 >> s` (phân tích $n - 1 = 2^s \cdot d$).
  - `Dòng 253–256`: Nếu `rounds <= 0` thì ép về mặc định `40`.
  - `Dòng 259–291`: Lặp `rounds` vòng độc lập:
    - `Dòng 262`: Chọn cơ sở ngẫu nhiên đều `a = random_range(ctx, two, n_minus_2)`.
    - `Dòng 265–269`: Tính `x = modular_exponentiation(a, d, n)`; nếu `x == one || x == n_minus_1` thì `continue` sang vòng tiếp theo.
    - `Dòng 271–285`: Đặt `passed_round = false`; lặp `r = 1..s - 1`: tính `x = (x * x) % n`; gặp `x == n_minus_1` thì `passed_round = true; break;`; gặp `x == one` thì `return false;` ngay (căn bậc hai không tầm thường của `1`).
    - `Dòng 287–290`: Nếu `!passed_round`, `a` là nhân chứng hợp số ⇒ `return false;`.
  - `Dòng 293`: Qua hết `rounds` vòng ⇒ `return true;`.

### Phần 4: Sàng đồng thời & Pipeline sinh Safe Prime 4 tầng (Dòng 301–484)
- **`Dòng 301–329` (`SMALL_PRIMES[]` & `NUM_SMALL_PRIMES`):** Mảng hằng gồm **302 số nguyên tố lẻ nhỏ hơn 2000** (từ `3` đến `1999`).
- **`Dòng 336–352` (`static bool passes_safe_prime_sieve(const big_t &q, size_t bitsize)`):**
  - `Dòng 338–350`: Duyệt từng `r = SMALL_PRIMES[i]`:
    - `Dòng 341–344`: Nếu `bitsize <= 12 && r >= (1U << (bitsize - 2))` thì `break` (tránh loại nhầm khi chính `q == r` ở kích thước bit rất nhỏ).
    - `Dòng 345`: Tính 1 lần duy nhất `rem = mod_small(q, r)`.
    - `Dòng 346–349`: Nếu `rem == 0` (`r | q`) hoặc `rem == (r - 1) / 2` (`r | (2q + 1)` tức `r | p`) thì trả `false` ngay.
  - `Dòng 351`: Qua hết 302 số nguyên tố nhỏ ⇒ trả `true`.
- **`Dòng 355–391` (`static bool miller_rabin_base2(const big_t &n)`):**
  - Tương tự 1 vòng của `is_probable_prime`, nhưng cố định cơ sở `a = 2` (`two`) — không cần gọi `random_range`, chạy cực nhanh để lọc sơ bộ `> 99.99%` hợp số còn sót sau sàng.
- **`Dòng 394–402` (`struct SafePrimeStats` & `g_last_safe_prime_stats`):** Lưu 4 chỉ số thống kê của lần sinh gần nhất (`total_candidates`, `passed_sieve`, `passed_q_base2`, `passed_p_base2`) phục vụ đo benchmark.
- **`Dòng 411–470` (`big_t generate_safe_prime(prng_ctx *ctx, size_t bitsize = 512, int rounds = 40)`):**
  - `Dòng 413–420`: Trường hợp biên rất nhỏ: `bitsize < 3` trả `5`; `bitsize == 3` trả `7`.
  - `Dòng 422–423`: Khởi tạo `one = 1` và bộ đếm `stats = {0, 0, 0, 0}`.
  - `Dòng 425–469` (Vòng lặp `while (true)` tìm cặp `(q, p)`):
    - `Dòng 427`: Tăng `stats.total_candidates++`.
    - `Dòng 432–433`: Sinh `q = random_bits(ctx, bitsize - 1)` (đúng `bitsize - 1` bit, bit cao nhất = 1) và `q.set_bit(0)` (ép `q` lẻ) ⇒ đảm bảo `p = 2q + 1` có **chính xác `bitsize` bit** và luôn lẻ.
    - `Dòng 436–440` (**Tầng 1 — Sàng đồng thời**): Gọi `passes_safe_prime_sieve(q, bitsize)`; không đạt thì `continue` (loại ~98.56%); đạt thì `stats.passed_sieve++`.
    - `Dòng 443–447` (**Tầng 2 — MR cơ sở 2 trên `q`**): Gọi `miller_rabin_base2(q)`; không đạt thì `continue`; đạt thì `stats.passed_q_base2++`.
    - `Dòng 450–455` (**Tầng 3 — MR cơ sở 2 trên `p`**): Tính `p = (q << 1) + one` (dịch trái 1 bit cộng 1 = `2q + 1`); gọi `miller_rabin_base2(p)`; không đạt thì `continue`; đạt thì `stats.passed_p_base2++`.
    - `Dòng 458–465` (**Tầng 4 — Xác nhận đầy đủ `rounds` vòng**): Gọi `is_probable_prime(ctx, q, rounds)` rồi `is_probable_prime(ctx, p, rounds)`; cả hai đều đạt thì lưu `g_last_safe_prime_stats = stats` và `return p;`.
- **`Dòng 473–482` (`big_t generate_private_key(prng_ctx *ctx, const big_t &p)`):**
  - `Dòng 475–479`: Nếu `p <= 4` trả fallback `2`.
  - `Dòng 480–481`: Tính `p_minus_two = p - 2` và trả về `random_range(ctx, two, p_minus_two)` — khóa riêng phân phối đều tuyệt đối trên `[2, p - 2]`.
- **`Dòng 484` (`#endif // PRIME_CPP`):** Đóng include guard.

---

## 3.6. File `main.cpp` (201 dòng) — Chương trình chính & Giao diện CLI

*(Tích hợp & hoàn thiện: Vương Hữu Khang & Tạ Quang Mạnh.)*

### Macro đầu file, Thư viện chuẩn & Unity Build (Dòng 14–39)
- **`Dòng 14` (`#define _CRT_RAND_S`):** Đặt ở dòng code đầu tiên trước mọi `#include` để đảm bảo `<cstdlib>` trên Windows mở khóa hàm `rand_s`.
- **`Dòng 16–22`:** Nạp các header chuẩn C++14: `<iostream>` (in/nhập), `<iomanip>`, `<chrono>` (đo thời gian chính xác cao), `<string>`, `<cstring>` (`std::memset`), `<cstdlib>` (`strtoul`, `strtol`), `<cctype>` (`isxdigit`).
- **`Dòng 25–29`:** `#include` 5 module theo đúng thứ tự phụ thuộc: `fips202.cpp` → `prng.cpp` → `bigint.cpp` → `dh.cpp` → `prime.cpp`.
- **`Dòng 31–39` (`print_usage`):** In hướng dẫn sử dụng các cờ `--bits`, `--rounds`, `--seed`, `-h`/`--help`.

### Bước 1: Parse & Validate tham số dòng lệnh (Dòng 41–102)
- **`Dòng 43–46`:** Khởi tạo cấu hình mặc định: `bit_size = 512`, `rounds = 40`, `fixed_seed_hex = ""`, `use_fixed_seed = false`.
- **`Dòng 49–85` (Vòng lặp `for (int i = 1; i < argc; i++)`):**
  - `Dòng 51–53` (`-h` hoặc `--help`): Gọi `print_usage(argv[0])` và `return 0;`.
  - `Dòng 54–61` (`--bits <N>`): Dùng `std::strtoul(argv[++i], &end, 10)` parse số nguyên dương; kiểm tra `end == argv[i]` (rỗng/không phải số), `*end != '\0'` (dính chữ thừa như `"512abc"`), hoặc `v == 0` ⇒ báo lỗi và `return 1;`.
  - `Dòng 62–69` (`--rounds <K>`): Dùng `std::strtol(argv[++i], &end, 10)` parse và kiểm tra nằm trong `[1, 1000]`; sai thì báo lỗi và `return 1;`.
  - `Dòng 70–79` (`--seed <HEX>`): Kiểm tra đúng 64 ký tự (`fixed_seed_hex.length() == 64`) và mọi ký tự thỏa `std::isxdigit(static_cast<unsigned char>(...)) != 0` (ép `unsigned char` tránh UB khi `char` âm); sai thì báo lỗi và `return 1;`.
  - `Dòng 80–84`: Bắt mọi tham số lạ hoặc thiếu giá trị, in lỗi + hướng dẫn và `return 1;`.
- **`Dòng 87–94` (Kiểm tra biên `bit_size`):**
  - `Dòng 87–89`: Nếu `bit_size < 512`, in cảnh báo (nhưng vẫn cho chạy để test nhanh 64/128 bit).
  - `Dòng 90–94`: Nếu `bit_size > MAX_PRIME_BITS` (1024), báo lỗi rõ ràng kèm chỉ dẫn sửa `MAX_PRIME_BITS` trong `bigint.cpp` và `return 1;` (ngăn tràn bộ đệm 2048-bit).
- **`Dòng 96–102`:** In banner tiêu đề Đồ án 1 Nhóm 18 và cấu hình hiện tại (`bit_size`, `rounds`).

### Bước 2: Khởi tạo CSPRNG (Dòng 105–123)
- **`Dòng 105–106`:** Khai báo ngữ cảnh `prng_ctx ctx;` và mảng `uint8_t seed[32];` (256 bit).
- **`Dòng 108–115` (Nhánh `if (use_fixed_seed)`):** Xóa trắng `seed` bằng `std::memset`, duyệt `i = 0..31` cắt từng cặp 2 ký tự hex `fixed_seed_hex.substr(i * 2, 2)` đổi sang 1 byte bằng `std::strtoul(..., nullptr, 16)`.
- **`Dòng 116–120` (Nhánh `else` — mặc định an toàn):** Gọi `randombytes(seed, sizeof(seed))` lấy 32 byte entropy thật từ OS (`rand_s` / `getrandom`).
- **`Dòng 122` (`prng_seed(&ctx, seed, sizeof(seed));`):** Hấp thụ seed vào trạng thái Sponge SHAKE128.

### Bước 3: Sinh Safe Prime `p` & Chọn phần tử sinh `g` (Dòng 126–150)
- **`Dòng 126–132`:** Ghi mốc `t0`, gọi `p = generate_safe_prime(&ctx, bit_size, rounds)`, ghi mốc `t1`, tính thời gian `time_prime` (giây) bằng `std::chrono::duration<double>(t1 - t0).count()`, in thời gian và giá trị `p.to_hex()`.
- **`Dòng 133–138` (Chốt kiểm tra 1):** Kiểm tra `p.bit_length() != bit_size || !p.is_odd()`; nếu sai thì báo lỗi và `return 1;`.
- **`Dòng 140–146`:** Gọi `g = choose_generator(p)`, tính `q = (p - 1) >> 1`, kiểm tra độc lập `g_ok = (g != 1) && (modular_exponentiation(g, q, p) == 1)`, in `g` và kết quả kiểm tra `DUNG`/`SAI`.
- **`Dòng 147–150` (Chốt kiểm tra 2):** Nếu `!g_ok`, báo lỗi `p` có thể không phải safe prime và `return 1;`.

### Bước 4–7: Trao đổi khóa Alice–Bob & Xác minh kết quả (Dòng 153–201)
- **`Dòng 153–157` (Bước `[3]` — Sinh khóa riêng):** Gọi `a = generate_private_key(&ctx, p)` cho Alice và `b = generate_private_key(&ctx, p)` cho Bob (đều nằm đều trong `[2, p - 2]`), in dạng hex.
- **`Dòng 160–168` (Bước `[4]` — Tính giá trị công khai):** Đo thời gian `t_pub0..t_pub1`, tính `A = modular_exponentiation(g, a, p)` và `B = modular_exponentiation(g, b, p)`, in `A`, `B` và thời gian tính.
- **`Dòng 170–176` (Chốt kiểm tra 3 — Xác thực giá trị công khai):** Gọi `pub_ok = is_valid_public_value(A, p) && is_valid_public_value(B, p)` (kiểm tra `[2, p - 2]` và $A^q \equiv B^q \equiv 1 \pmod p$); nếu `!pub_ok`, báo lỗi và `return 1;`.
- **`Dòng 179–188` (Bước `[5]` — Tính bí mật chung):** Đo thời gian `t_dh0..t_dh1`, Alice tính `s_alice = modular_exponentiation(B, a, p)`, Bob tính `s_bob = modular_exponentiation(A, b, p)`, in `s_A`, `s_B` và thời gian tính `time_dh`.
- **`Dòng 191–198` (Chốt kiểm tra 4 — Xác minh cuối cùng):** Kiểm tra `matched = (s_alice == s_bob) && (s_alice > big_t::from_u64(1))` (loại cả trường hợp suy biến `0` và `1`). Nếu `matched` đúng, in `[XAC MINH THANH CONG] Bi mat chung hai ben hoan toan TRUNG KHOP!`, ngược lại in thông báo thất bại.
- **`Dòng 200` (`return 0;`):** Kết thúc chương trình thành công.
