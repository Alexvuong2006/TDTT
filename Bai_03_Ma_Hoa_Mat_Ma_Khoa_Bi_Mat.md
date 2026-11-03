# BÀI 3: MÃ HÓA KHÓA BÍ MẬT (SECRET-KEY / SYMMETRIC CRYPTOGRAPHY)
> **Tài liệu tham khảo chuyên sâu & Giải thích chi tiết toàn bộ kiến thức theo slide bài giảng Môn Mã hóa - Mật mã (Khoa CNTT - ĐH Khoa học Tự nhiên).**

---

## MỤC LỤC TỔNG QUAN

1. [Tổng quan & Nguyên lý thiết kế Hệ mã Bí mật](#1-tổng-quan--nguyên-lý-thiết-kế-hệ-mã-bí-mật)
   - [Bản chất của Mật mã đối xứng (Symmetric Cryptosystem)](#11-bản-chất-của-mật-mã-đối-xứng-symmetric-cryptosystem)
   - [Mô hình toán học của hàm mã hóa và giải mã](#12-mô-hình-toán-học-của-hàm-mã-hóa-và-giải-mã)
   - [Nguyên lý an toàn & Không gian tham số](#13-nguyên-lý-an-toàn--không-gian-tham-số)
   - [Các mô hình tấn công thám mã cơ bản (OCA, KPA, Brute-force)](#14-các-mô-hình-tấn-công-thám-mã-cơ-bản-oca-kpa-brute-force)
2. [Hai kỹ thuật biến đổi nền tảng](#2-hai-kỹ-thuật-biến-đổi-nền-tảng)
   - [Phép thay thế (Substitution / Replace)](#21-phép-thay-thế-substitution--replace)
   - [Phép hoán vị / Chuyển vị (Permutation / Transposition)](#22-phép-hoán-vị--chuyển-vị-permutation--transposition)
   - [Nguyên lý Hỗn loạn (Confusion) & Khuếch tán (Diffusion) của Claude Shannon](#23-nguyên-lý-hỗn-loạn-confusion--khuếch-tán-diffusion-của-claude-shannon)
3. [Các hệ mã bí mật cổ điển & Kỹ thuật thám mã](#3-các-hệ-mã-bí-mật-cổ-điển--kỹ-thuật-thám-mã)
   - [Hệ mã tuyến tính (Linear / Affine Cipher)](#31-hệ-mã-tuyến-tính-linear--affine-cipher)
     - Định nghĩa & Công thức toán học
     - Ví dụ tính toán từng bước (Mã hóa / Giải mã "WAR")
     - Thám mã bằng Phân tích tần suất (Frequency Analysis Attack)
     - Thám mã bằng Vét cạn (Brute-Force Attack & Heuristics)
   - [Hệ mã Ma trận (Matrix / Hill Cipher mở rộng)](#32-hệ-mã-ma-trận-matrix--hill-cipher-mở-rộng)
     - Định nghĩa mã khối ma trận $C \equiv KP + B \pmod n$
     - Điều kiện ma trận khả nghịch & Ma trận nghịch đảo modulo $n$
     - Ví dụ mã hóa / giải mã "TH"
     - Thám mã biết bản rõ (Known-Plaintext Attack - KPA) giải hệ ma trận (Ví dụ "ATTACK" $\leftrightarrow$ "BTGTHM")
   - [Hệ mã Hoán vị khối (Block Permutation Cipher)](#33-hệ-mã-hoán-vị-khối-block-permutation-cipher)
     - Biểu diễn bằng ma trận hoán vị
     - Đệm khối (Padding) & Ví dụ "THIS IS NIRVANA"
4. [Mật mã bí mật hiện đại](#4-mật-mã-bí-mật-hiện-đại)
   - [Mạng Hoán vị – Thay thế (Substitution-Permutation Network - SPN)](#41-mạng-hoán-vị--thay-thế-substitution-permutation-network---spn)
     - Kết hợp đa vòng (Multiple rounds)
     - Ví dụ tính toán chi tiết trong bài giảng ("SCOOBY DOO WHERE ARE YOU")
   - [Mã hóa dựa trên Tác động nhóm (Group Action Ciphers)](#42-mã-hóa-dựa-trên-tác-động-nhóm-group-action-ciphers)
   - [Mạng Feistel & Cấu trúc Hộp thay thế (S-Box)](#43-mạng-feistel--cấu-trúc-hộp-thay-thế-s-box)
     - Nguyên lý mạng Feistel: Tính đối xứng giữa mã hóa và giải mã
     - Mô hình toán học của S-Box: Phép biến đổi phi tuyến và affine
   - [Chuẩn mã hóa dữ liệu DES (Data Encryption Standard)](#44-chuẩn-mã-hóa-dữ-liệu-des-data-encryption-standard)
     - Lịch sử & Thông số tổng quan (Khối 64 bit, Khóa 56 bit)
     - 4 bước xử lý: Hoán vị khởi tạo $IP$, 16 vòng Feistel, Hoán vị nghịch đảo $IP^{-1}$
     - Cấu trúc hàm vòng $f(R_{i-1}, K_i)$
   - [Chuẩn 3DES (Triple DES)](#45-chuẩn-3des-triple-des)
     - Cấu trúc EDE (Encrypt - Decrypt - Encrypt)
     - 3 tùy chọn khóa (Keying Options) & Tương thích ngược
5. [Bảng so sánh tổng hợp & Đúc kết ôn thi](#5-bảng-so-sánh-tổng-hợp--đúc-kết-ôn-thi)
   - [So sánh Mã bí mật (Symmetric) vs Mã công khai (Asymmetric)](#51-so-sánh-mã-bí-mật-vs-mã-công-khai)
   - [So sánh DES vs 3DES vs AES](#52-so-sánh-des-vs-3des-vs-aes)
   - [Tóm tắt công thức then chốt cần nhớ khi đi thi](#53-tóm-tắt-công-thức-then-chốt-cần-nhớ-khi-đi-thi)

---

## 1. TỔNG QUAN & NGUYÊN LÝ THIẾT KẾ HỆ MÃ BÍ MẬT

### 1.1 Bản chất của Mật mã đối xứng (Symmetric Cryptosystem)
- **Định nghĩa**: Hệ mã khóa bí mật (*Secret-Key Cryptosystem*), hay còn gọi là **Hệ mã đối xứng (*Symmetric Cryptosystem*)**, là hệ thống mật mã mà trong đó các đối tác tham gia trao đổi thông tin (Alice và Bob) **dùng chung một khóa bí mật $k$** cho cả quá trình mã hóa lẫn giải mã.
- **Hai tính chất cốt lõi**:
  1. **Tính đối xứng (Symmetric)**: Kiến thức về khóa mã hóa cho phép suy ra trực tiếp khóa giải mã (hoặc chúng giống hệt nhau $k_{enc} = k_{dec} = k$).
  2. **Tính bí mật (Secret)**: Khóa $k$ phải được bảo vệ tuyệt mật giữa hai bên. Bất kỳ ai có được khóa $k$ đều có thể đọc toàn bộ bản tin và mạo danh người gửi.

```
                  +-----------------------------------+
                  |   KÊNH BẢO MẬT PHÂN PHỐI KHÓA     |
                  +-----------------+-----------------+
                                    |
                       Khóa bí mật k|Khóa bí mật k
                                    v
     Bản rõ m                       |                         Bản rõ m
    +--------+    +-------------+   |   +-------------+    +--------+
--->| Alice  |--->|   Mã hóa    |---|-->|   Giải mã   |--->|  Bob   |
    +--------+    |  E_k(m) = c |   |   |  D_k(c) = m |    +--------+
                  +------+------+   |   +------+------+
                         |          |          ^
                         |   Bản mã c          |
                         +---------------------+
                         (Kênh truyền công khai)
```

---

### 1.2 Mô hình toán học của hàm mã hóa và giải mã
Về mặt toán học, một hệ mã bí mật là một bộ gồm năm thành phần:
$$(\mathcal{M}, \mathcal{C}, \mathcal{K}, \mathcal{E}, \mathcal{D})$$
Trong đó:
- $\mathcal{M}$ (*Plaintext Space*): Không gian bản rõ chứa các thông điệp có thể gửi.
- $\mathcal{C}$ (*Ciphertext Space*): Không gian bản mã chứa các bản tin sau khi mã hóa.
- $\mathcal{K}$ (*Key Space*): Không gian khóa chứa các giá trị khóa hợp lệ.
- $\mathcal{E} = \{E_k : k \in \mathcal{K}\}$: Họ các hàm mã hóa.
- $\mathcal{D} = \{D_k : k \in \mathcal{K}\}$: Họ các hàm giải mã.

**Tính khả nghịch**:
Với mỗi khóa $k \in \mathcal{K}$, hàm mã hóa $E_k: \mathcal{M} \to \mathcal{C}$ phải là một **song ánh (hoặc đơn ánh)**, và tồn tại hàm giải mã tương ứng $D_k \equiv E_k^{-1}: \mathcal{C} \to \mathcal{M}$ sao cho:
$$\forall m \in \mathcal{M}: \quad D_k(E_k(m)) = m$$

---

### 1.3 Nguyên lý an toàn & Không gian tham số
Hệ mã bí mật muốn đạt được mức độ an toàn thực tiễn phải tuân thủ các nguyên lý sau:
1. **Nguyên lý Kerckhoffs (Nguyên lý cơ bản của mật mã học)**:
   > "Độ an toàn của một hệ thống mật mã không được phụ thuộc vào sự bí mật của thuật toán, mà **chỉ phụ thuộc duy nhất vào sự bí mật của khóa**."
   Thuật toán mã hóa $E$ và giải mã $D$ luôn được xem là công khai hoàn toàn cho kẻ tấn công biết.

2. **Yêu cầu về độ lớn không gian tham số**:
   - Không gian bản rõ $\mathcal{M}$, không gian bản mã $\mathcal{C}$, và đặc biệt là **không gian khóa $\mathcal{K}$ phải đủ lớn** để kẻ tấn công không thể sử dụng phương pháp vét cạn (*Brute-force attack*).
   - Ví dụ: Một khóa 56-bit có $|\mathcal{K}| = 2^{56} \approx 7.2 \times 10^{16}$ khóa (đã bị bẻ gãy dễ dàng trong vài giờ). Ngày nay, không gian khóa tối thiểu phải đạt $2^{128}$ hoặc $2^{256}$.

3. **Yêu cầu về độ phức tạp của phép biến đổi**:
   - Các phép biến đổi trong hàm $E_k$ và $D_k$ phải đủ phức tạp và mang tính phi tuyến cao để chống lại các phương pháp thám mã đại số (*Algebraic Cryptanalysis*) và thám mã thống kê (*Statistical / Frequency Analysis*).

---

### 1.4 Các mô hình tấn công thám mã cơ bản
Dựa vào lượng thông tin mà kẻ thám mã (Eve) có trong tay, các kỹ thuật tấn công được phân loại thành:

```
[Mức độ thông tin của Kẻ tấn công tăng dần]
   +-------------------------------------------------------------+
   | 1. Tấn công Chỉ cần Bản mã (Ciphertext-Only Attack - COA)   |
   +------------------------------+------------------------------+
                                  v
   +-------------------------------------------------------------+
   | 2. Tấn công Biết Bản rõ (Known-Plaintext Attack - KPA)      |
   +------------------------------+------------------------------+
                                  v
   +-------------------------------------------------------------+
   | 3. Tấn công Chọn Bản rõ (Chosen-Plaintext Attack - CPA)     |
   +------------------------------+------------------------------+
                                  v
   +-------------------------------------------------------------+
   | 4. Tấn công Chọn Bản mã (Chosen-Ciphertext Attack - CCA)     |
   +-------------------------------------------------------------+
```

1. **Tấn công chỉ cần bản mã (Ciphertext-Only Attack - COA / OCA)**:
   - Kẻ tấn công chỉ có một hoặc nhiều bản mã $c \in \mathcal{C}$ thu thập được trên đường truyền.
   - *Nguyên tắc an toàn*: **Mọi hệ mã bị phá bằng COA đều bị xem là hoàn toàn không an toàn** và bị loại bỏ ngay lập tức.
   - Hai phương pháp COA cơ bản:
     + **Tấn công vét cạn (Brute-force attack)**: Thử từng khóa $k \in \mathcal{K}$ để tính $m = D_k(c)$. Nếu $m$ là một văn bản có nghĩa (ngôn ngữ tự nhiên), $k$ có khả năng cao là khóa đúng.
     + **Tấn công phân tích tần suất (Frequency analysis attack)**: Khai thác quy luật phân phối xác suất không đều của các ký tự hoặc nhóm ký tự trong ngôn ngữ tự nhiên.
2. **Tấn công khi biết bản rõ (Known-Plaintext Attack - KPA)**:
   - Kẻ tấn công sở hữu một số cặp bản rõ - bản mã tương ứng $\{(m_1, c_1), (m_2, c_2), \dots, (m_t, c_t)\}$ được mã hóa bằng cùng một khóa $k$.
   - Mục tiêu: Tìm khóa bí mật $k$ hoặc thuật toán giải mã để đọc các bản mã khác trong tương lai.
   - Kỹ thuật chung: Thiết lập hệ phương trình quan hệ từ các cặp $(m_i, c_i)$ và giải đại số.

---

## 2. HAI KỸ THUẬT BIẾN ĐỔI NỀN TẢNG

Hầu hết mọi hệ mã hóa bí mật từ cổ điển đến hiện đại đều được xây dựng dựa trên sự kết hợp khéo léo của hai phép biến đổi cơ bản:

### 2.1 Phép thay thế (Substitution / Replace)
- **Khái niệm**: Mỗi ký hiệu (ký tự, bit, byte hoặc khối bit) trong thông điệp đầu vào được thay thế bằng một ký hiệu khác theo một quy tắc xác định phụ thuộc vào khóa $k$.
- **Ví dụ kinh điển**:
  - Mã Caesar (dịch chuyển $k$ vị trí trong bảng chữ cái).
  - Phép thế Affine ($C \equiv aP + b \pmod n$).
  - Bảng thay thế phi tuyến S-Box trong DES và AES.

### 2.2 Phép hoán vị / Chuyển vị (Permutation / Transposition)
- **Khái niệm**: Thứ tự hoặc vị trí của các ký hiệu trong thông điệp bị xáo trộn, sắp xếp lại theo một trật tự mới mà không làm thay đổi giá trị nội dung của bản thân ký hiệu đó.
- **Biểu diễn toán học**:
  Một phép hoán vị $\sigma$ trên tập chỉ số $\{0, 1, \dots, m-1\}$ là một song ánh:
  $$\sigma: \{0, 1, \dots, m-1\} \to \{0, 1, \dots, m-1\}$$
  Khối thông điệp $M = m_0 m_1 \dots m_{m-1}$ sẽ được chuyển vị thành:
  $$C = m_{\sigma(0)} m_{\sigma(1)} \dots m_{\sigma(m-1)}$$

### 2.3 Nguyên lý Hỗn loạn (Confusion) & Khuếch tán (Diffusion) của Claude Shannon
Năm 1949, nhà toán học lỗi lạc Claude Shannon đã đặt nền móng lý thuyết cho mật mã hiện đại với hai đặc tính thiết kế sống còn:

| Đặc tính | Bản chất | Kỹ thuật hiện thực | Mục tiêu chống tấn công |
| :--- | :--- | :--- | :--- |
| **Hỗn loạn (Confusion)** | Làm cho mối quan hệ giữa **khóa bí mật $K$** và **bản mã $C$** trở nên cực kỳ phức tạp, mờ mịt và phi tuyến. | Thực hiện thông qua **Phép thay thế (Substitution / S-Box)**. | Ngăn chặn kẻ thám mã suy luận ra khóa bí mật $K$ từ các số liệu thống kê bản mã. |
| **Khuếch tán (Diffusion)** | Làm cho mỗi bit của **bản rõ $M$** và mỗi bit của **khóa $K$** ảnh hưởng đến **rất nhiều bit của bản mã $C$** (và ngược lại). | Thực hiện thông qua **Phép hoán vị (Permutation / P-Box / ShiftRows / MixColumns)**. | Ngăn chặn phân tích tần suất; làm biến mất các cấu trúc thống kê lặp lại của bản rõ trong bản mã. |

- **Hiệu ứng thác đổ (Avalanche Effect)**: Kết quả của sự kết hợp hoàn hảo giữa Confusion và Diffusion: chỉ cần thay đổi **1 bit duy nhất** của bản rõ hoặc khóa, ít nhất **50% số bit của bản mã** sẽ thay đổi ngẫu nhiên.

---

## 3. CÁC HỆ MÃ BÍ MẬT CỔ ĐIỂN & KỸ THUẬT THÁM MÃ

### 3.1 Hệ mã tuyến tính (Linear / Affine Cipher)

#### 1. Định nghĩa toán học
Xét trên bảng chữ cái gồm $n$ ký tự (với tiếng Anh chuẩn, $n = 26$, gán $A = 0, B = 1, \dots, Z = 25$).
- **Khóa**: Cặp số $(k, b)$ với $k, b \in \mathbb{Z}_n$, thỏa mãn điều kiện tiên quyết:
  $$\gcd(k, n) = 1$$
  *(Điều kiện $\gcd(k, n) = 1$ bảo đảm $k$ khả nghịch trong vành $\mathbb{Z}_n$, tức tồn tại $k^{-1} \pmod n$ để giải mã duy nhất).*
- **Công thức Mã hóa**:
  $$E_{(k, b)}(P) \equiv C \equiv (k \cdot P + b) \pmod n$$
- **Công thức Giải mã**:
  $$D_{(k, b)}(C) \equiv P \equiv k^{-1} \cdot (C - b) \pmod n$$

#### 2. Ví dụ tính toán từng bước (Mã hóa / Giải mã "WAR")
*(Theo ví dụ trang 11-12 trong bài giảng)*
- **Tham số**:
  - Bảng chữ cái tiếng Anh $n = 26$.
  - Khóa: $k = 7, b = 10$.
  - Kiểm tra điều kiện: $\gcd(7, 26) = 1$ (hợp lệ).
  - Bản rõ $P = \text{"WAR"}$.

##### Bước 1: Mã hóa
Chuyển ký tự thành số:
- $W \leftrightarrow 22$
- $A \leftrightarrow 00$
- $R \leftrightarrow 17$

Áp dụng công thức $C \equiv (7 \cdot P + 10) \pmod{26}$:
- Với $W (22)$: $C_1 \equiv (7 \cdot 22 + 10) = 154 + 10 = 164 = 6 \cdot 26 + 8 \equiv 8 \pmod{26} \leftrightarrow \mathbf{I}$.
- Với $A (00)$: $C_2 \equiv (7 \cdot 0 + 10) = 10 \equiv 10 \pmod{26} \leftrightarrow \mathbf{K}$.
- Với $R (17)$: $C_3 \equiv (7 \cdot 17 + 10) = 119 + 10 = 129 = 4 \cdot 26 + 25 \equiv 25 \pmod{26} \leftrightarrow \mathbf{Z}$.

$\implies$ Bản mã thu được: $C = \text{"IKZ"} \leftrightarrow (08, 10, 25)$.

##### Bước 2: Giải mã
- **Tìm nghịch đảo của $k = 7$ modulo 26**:
  Sử dụng thuật toán Euclid mở rộng giải phương trình $7x + 26y = \gcd(7, 26) = 1$:
  $$26 = 3 \cdot 7 + 5$$
  $$7 = 1 \cdot 5 + 2$$
  $$5 = 2 \cdot 2 + 1 \implies 1 = 5 - 2 \cdot 2 = 5 - 2(7 - 5) = 3 \cdot 5 - 2 \cdot 7$$
  $$1 = 3(26 - 3 \cdot 7) - 2 \cdot 7 = 3 \cdot 26 - 11 \cdot 7$$
  Do đó: $-11 \cdot 7 \equiv 1 \pmod{26} \implies 7^{-1} \equiv -11 \equiv 15 \pmod{26}$.
  *(Kiểm tra: $7 \cdot 15 = 105 = 4 \cdot 26 + 1 \equiv 1 \pmod{26}$).*

- **Khôi phục bản rõ**: Áp dụng $P \equiv 15 \cdot (C - 10) \pmod{26}$:
  - Với $I (08)$: $P_1 \equiv 15 \cdot (8 - 10) = 15 \cdot (-2) = -30 \equiv 22 \pmod{26} \leftrightarrow \mathbf{W}$.
  - Với $K (10)$: $P_2 \equiv 15 \cdot (10 - 10) = 0 \equiv 0 \pmod{26} \leftrightarrow \mathbf{A}$.
  - Với $Z (25)$: $P_3 \equiv 15 \cdot (25 - 10) = 15 \cdot 15 = 225 = 8 \cdot 26 + 17 \equiv 17 \pmod{26} \leftrightarrow \mathbf{R}$.

$\implies$ Khôi phục chính xác $P = \text{"WAR"}$.

---

#### 3. Thám mã Hệ mã tuyến tính bằng Phân tích tần suất (Frequency Analysis)
*(Theo ví dụ trang 14 trong slide)*
Trong tiếng Anh, phân bố tần suất xuất hiện của các chữ cái có đặc trưng bất đối xứng rất mạnh:
- Ký tự xuất hiện nhiều nhất: **E** (mã số 04, chiếm khoảng 12.7%).
- Ký tự xuất hiện nhiều thứ hai: **T** (mã số 19, chiếm khoảng 9.1%).

**Kịch bản tấn công**:
Giả sử chặn được một đoạn văn bản mã hóa dài bằng mã tuyến tính, thống kê tần suất ký tự trong bản mã thấy:
- Ký tự xuất hiện nhiều nhất là **V** (21).
- Ký tự xuất hiện nhiều thứ hai là **E** (04).

Ta giả thiết:
- $E (04)$ trong bản rõ được mã hóa thành $V (21)$.
- $T (19)$ trong bản rõ được mã hóa thành $E (04)$.

Thiết lập hệ phương trình đồng dư:
$$\begin{cases} 4 \cdot k + b \equiv 21 \pmod{26} \quad (1) \\ 19 \cdot k + b \equiv 4 \pmod{26} \quad (2) \end{cases}$$

**Giải hệ phương trình**:
Lấy $(2) - (1)$:
$$(19k + b) - (4k + b) \equiv 4 - 21 \pmod{26}$$
$$15k \equiv -17 \equiv 9 \pmod{26}$$

Để tìm $k$, ta tìm nghịch đảo của 15 modulo 26:
Vì $15 \cdot 7 = 105 = 4 \cdot 26 + 1 \equiv 1 \pmod{26} \implies 15^{-1} \equiv 7 \pmod{26}$.
Nhân cả 2 vế với 7:
$$k \equiv 9 \cdot 7 = 63 = 2 \cdot 26 + 11 \equiv 11 \pmod{26}$$

Thay $k = 11$ vào phương trình (1):
$$4 \cdot 11 + b \equiv 21 \pmod{26}$$
$$44 + b \equiv 21 \implies 18 + b \equiv 21 \implies b \equiv 3 \pmod{26}$$

**Kết quả khóa tìm được**: $(k = 11, b = 3)$.
Thử giải mã toàn bộ văn bản bằng cặp khóa này. Nếu văn bản đọc hiểu được, cuộc tấn công hoàn toàn thành công!

---

#### 4. Thám mã bằng Vét cạn (Brute-Force Attack)
- **Kích thước không gian khóa**:
  - Giá trị $b \in \{0, 1, \dots, 25\} \implies$ có 26 khả năng.
  - Giá trị $k \in \{0, 1, \dots, 25\}$ thỏa $\gcd(k, 26) = 1$. Các số nguyên tố cùng nhau với 26 là: $\{1, 3, 5, 7, 9, 11, 15, 17, 19, 21, 23, 25\} \implies \varphi(26) = 12$ khả năng.
  - Tổng số khóa có thể:
    $$|\mathcal{K}| = 12 \times 26 = 312 \text{ khóa}$$
- Với chỉ 312 khóa, máy tính hiện đại chỉ mất **chưa đầy 1 mili-giây** để thử toàn bộ không gian khóa.
- **Heuristics vét cạn thực tế**: Thử tập khóa yếu trước, khóa tạo theo ngày sinh, tên người dùng hoặc quy luật dễ nhớ.

---

### 3.2 Hệ mã Ma trận (Matrix / Hill Cipher mở rộng)

#### 1. Định nghĩa toán học
Mã ma trận là sự mở rộng đa chiều của mã tuyến tính trên khối $m$ ký hiệu:
- **Khóa**: Cặp $(K, B)$, trong đó:
  - $K$ là ma trận vuông cấp $m \times m$ với các phần tử thuộc $\mathbb{Z}_n$.
  - $B$ là vector cột cấp $m \times 1$ với các phần tử thuộc $\mathbb{Z}_n$.
  - **Điều kiện khả nghịch bắt buộc**:
    $$\gcd(\det(K), n) = 1$$
- **Mã hóa**:
  $$C \equiv (K \cdot P + B) \pmod n$$
- **Giải mã**:
  $$P \equiv K^{-1} \cdot (C - B) \pmod n$$
  Trong đó ma trận nghịch đảo modulo $n$ được tính theo công thức:
  $$K^{-1} \equiv (\det(K))^{-1} \cdot \text{adj}(K) \pmod n$$
  (với $\text{adj}(K)$ là ma trận phụ hợp - transpose of cofactor matrix).

---

#### 2. Ví dụ tính toán Mã hóa & Giải mã "TH"
*(Theo ví dụ trang 17 trong bài giảng)*
- Cho $n = 26$, khối $m = 2$:
  $$K = \begin{pmatrix} 5 & 17 \\ 4 & 15 \end{pmatrix}, \quad B = \begin{pmatrix} 5 \\ 2 \end{pmatrix}$$
- Bản rõ: $P = \text{"TH"} \leftrightarrow \begin{pmatrix} 19 \\ 07 \end{pmatrix}$.

##### Mã hóa:
$$K \cdot P = \begin{pmatrix} 5 & 17 \\ 4 & 15 \end{pmatrix} \begin{pmatrix} 19 \\ 7 \end{pmatrix} = \begin{pmatrix} 5 \cdot 19 + 17 \cdot 7 \\ 4 \cdot 19 + 15 \cdot 7 \end{pmatrix} = \begin{pmatrix} 95 + 119 \\ 76 + 105 \end{pmatrix} = \begin{pmatrix} 214 \\ 181 \end{pmatrix}$$
$$C \equiv K \cdot P + B = \begin{pmatrix} 214 + 5 \\ 181 + 2 \end{pmatrix} = \begin{pmatrix} 219 \\ 183 \end{pmatrix} \pmod{26}$$
Ta có:
- $219 = 8 \cdot 26 + 11 \equiv 11 \pmod{26} \leftrightarrow \mathbf{L}$.
- $183 = 7 \cdot 26 + 1 \equiv 1 \pmod{26} \leftrightarrow \mathbf{B}$.

$\implies$ Bản mã: $C = \text{"LB"}$.

##### Giải mã:
1. **Tính ma trận nghịch đảo $K^{-1} \pmod{26}$**:
   - Định thức: $\det(K) = 5 \cdot 15 - 17 \cdot 4 = 75 - 68 = 7$.
   - Vì $\gcd(7, 26) = 1$, tồn tại nghịch đảo.
   - Tìm $7^{-1} \pmod{26}$: Ta có $7 \cdot 15 = 105 \equiv 1 \pmod{26} \implies (\det(K))^{-1} \equiv 15 \pmod{26}$.
   - Ma trận phụ hợp của ma trận $2 \times 2$:
     $$\text{adj}(K) = \begin{pmatrix} 15 & -17 \\ -4 & 5 \end{pmatrix} \equiv \begin{pmatrix} 15 & 9 \\ 22 & 5 \end{pmatrix} \pmod{26}$$
   - Nhân với nghịch đảo định thức:
     $$K^{-1} \equiv 15 \cdot \begin{pmatrix} 15 & 9 \\ 22 & 5 \end{pmatrix} = \begin{pmatrix} 225 & 135 \\ 330 & 75 \end{pmatrix} \equiv \begin{pmatrix} 17 & 5 \\ 18 & 23 \end{pmatrix} \pmod{26}$$
2. **Khôi phục bản rõ**:
   $$C - B = \begin{pmatrix} 11 - 5 \\ 1 - 2 \end{pmatrix} = \begin{pmatrix} 6 \\ -1 \end{pmatrix} \equiv \begin{pmatrix} 6 \\ 25 \end{pmatrix} \pmod{26}$$
   $$P \equiv K^{-1}(C - B) = \begin{pmatrix} 17 & 5 \\ 18 & 23 \end{pmatrix} \begin{pmatrix} 6 \\ 25 \end{pmatrix} = \begin{pmatrix} 17 \cdot 6 + 5 \cdot 25 \\ 18 \cdot 6 + 23 \cdot 25 \end{pmatrix} = \begin{pmatrix} 102 + 125 \\ 108 + 575 \end{pmatrix} = \begin{pmatrix} 227 \\ 683 \end{pmatrix} \pmod{26}$$
   - $227 = 8 \cdot 26 + 19 \equiv 19 \pmod{26} \leftrightarrow \mathbf{T}$.
   - $683 = 26 \cdot 26 + 7 \equiv 7 \pmod{26} \leftrightarrow \mathbf{H}$.

$\implies$ Khôi phục chính xác $P = \text{"TH"}$.

---

#### 3. Thám mã Hệ mã Ma trận: Tấn công Biết bản rõ (Known-Plaintext Attack - KPA)
*(Theo ví dụ trang 19 trong bài giảng)*

Giả sử kẻ thám mã biết văn bản rõ **"ATTACK"** được mã hóa thành bản mã **"BTGTHM"**.
Kích thước khối $m = 2$. Đặt:
$$K = \begin{pmatrix} a & b \\ c & d \end{pmatrix}, \quad B = \begin{pmatrix} s \\ t \end{pmatrix}$$
Ta có 6 ẩn số cần tìm: $a, b, c, d, s, t \pmod{26}$.

Phân tích các cặp khối bản rõ $\leftrightarrow$ bản mã:
1. $\text{"AT"} \leftrightarrow \text{"BT"}$:
   - $P_1 = \begin{pmatrix} A \\ T \end{pmatrix} = \begin{pmatrix} 0 \\ 19 \end{pmatrix}$, $C_1 = \begin{pmatrix} B \\ T \end{pmatrix} = \begin{pmatrix} 1 \\ 19 \end{pmatrix}$.
   - Phương trình:
     $$\begin{cases} 0 \cdot a + 19 \cdot b + s \equiv 1 \pmod{26} \quad (1) \\ 0 \cdot c + 19 \cdot d + t \equiv 19 \pmod{26} \quad (2) \end{cases}$$
2. $\text{"TA"} \leftrightarrow \text{"GT"}$:
   - $P_2 = \begin{pmatrix} 19 \\ 0 \end{pmatrix}$, $C_2 = \begin{pmatrix} 6 \\ 19 \end{pmatrix}$.
   - Phương trình:
     $$\begin{cases} 19 \cdot a + 0 \cdot b + s \equiv 6 \pmod{26} \quad (3) \\ 19 \cdot c + 0 \cdot d + t \equiv 19 \pmod{26} \quad (4) \end{cases}$$
3. $\text{"CK"} \leftrightarrow \text{"HM"}$:
   - $P_3 = \begin{pmatrix} 2 \\ 10 \end{pmatrix}$, $C_3 = \begin{pmatrix} 7 \\ 12 \end{pmatrix}$.
   - Phương trình:
     $$\begin{cases} 2 \cdot a + 10 \cdot b + s \equiv 7 \pmod{26} \quad (5) \\ 2 \cdot c + 10 \cdot d + t \equiv 12 \pmod{26} \quad (6) \end{cases}$$

Giải hệ phương trình tuyến tính 6 phương trình, 6 ẩn số trên modulo 26, ta tìm được duy nhất nghiệm:
$$K = \begin{pmatrix} a & b \\ c & d \end{pmatrix} \equiv \begin{pmatrix} 3 & 0 \\ 1 & 1 \end{pmatrix} \pmod{26}, \quad B = \begin{pmatrix} s \\ t \end{pmatrix} \equiv \begin{pmatrix} 1 \\ 0 \end{pmatrix} \pmod{26}$$

> **Nhận xét quan trọng**: Hệ mã ma trận hoàn toàn bất lực trước tấn công Biết bản rõ (KPA). Chỉ cần có $m^2 + m$ cặp ký tự, kẻ tấn công dễ dàng giải hệ phương trình tuyến tính để bẻ gãy toàn bộ khóa!

---

### 3.3 Hệ mã Hoán vị khối (Block Permutation Cipher)

#### 1. Nguyên lý và Biểu diễn bằng Ma trận hoán vị
- **Mã khối hoán vị**: Chia thông điệp thành các khối có độ dài cố định $m$. Trong mỗi khối, các ký tự được tráo đổi vị trí cho nhau theo một quy tắc hoán vị xác định.
- **Biểu diễn ma trận**: Có thể xem mã hoán vị là một trường hợp đặc biệt của mã ma trận:
  $$C = K \cdot P \quad (\text{với } B = O)$$
  Trong đó $K$ là một **Ma trận hoán vị (Permutation Matrix)**: Ma trận vuông chỉ chứa các số 0 và 1, sao cho trên mỗi hàng và mỗi cột có **chính xác một số 1**.
- **Tính chất đặc biệt**: Với ma trận hoán vị, ma trận nghịch đảo chính là ma trận chuyển vị của nó:
  $$K^{-1} = K^T$$

#### 2. Ví dụ minh họa (Trang 21 trong bài giảng)
- Kích thước khối $m = 5$.
- Cho ma trận hoán vị $K$ cấp $5 \times 5$:
  $$K = \begin{pmatrix} 0 & 0 & 1 & 0 & 0 \\ 0 & 0 & 0 & 0 & 1 \\ 0 & 0 & 0 & 1 & 0 \\ 0 & 1 & 0 & 0 & 0 \\ 1 & 0 & 0 & 0 & 0 \end{pmatrix}$$
  Quy tắc hoán vị này tương ứng ánh xạ vector vị trí đầu vào:
  $$(p_0, p_1, p_2, p_3, p_4)^T \mapsto (p_2, p_4, p_3, p_1, p_0)^T$$
- Văn bản rõ: `"THIS IS NIRVANA"` (13 ký tự, bỏ dấu cách).
- **Kỹ thuật Đệm khối (Padding)**:
  - Chia khối độ dài 5:
    - Khối 1: `THISI` (5 ký tự).
    - Khối 2: `SNIRV` (5 ký tự).
    - Khối 3: `ANA` (thiếu 2 ký tự $\implies$ đệm thêm `XX` thành `ANAXX`).
- **Mã hóa từng khối**:
  - `THISI`: $p_0=T, p_1=H, p_2=I, p_3=S, p_4=I \implies (p_2, p_4, p_3, p_1, p_0) = \mathbf{IISHT}$.
  - `SNIRV`: $p_0=S, p_1=N, p_2=I, p_3=R, p_4=V \implies \mathbf{IVRNS}$.
  - `ANAXX`: $p_0=A, p_1=N, p_2=A, p_3=X, p_4=X \implies \mathbf{AXXNA}$.
- Bản mã hoàn chỉnh: **`IISHT IVRNS AXXNA`**.

---

## 4. MẬT MÃ BÍ MẬT HIỆN ĐẠI

### 4.1 Mạng Hoán vị – Thay thế (Substitution-Permutation Network - SPN)
Một hệ mã thay thế đơn thuần (như mã tuyến tính, mã ma trận) dễ bị phá bằng đại số tuyến tính; một hệ mã hoán vị đơn thuần dễ bị phá bằng phân tích thống kê tần suất n-gram.
**Giải pháp hiện đại**: Kết hợp đan xen nhiều tầng **Thay thế (Substitution)** và **Hoán vị (Permutation)** qua nhiều vòng lặp liên tiếp (*Multiple Rounds*).

```
         Bản rõ P
            |
            v
   +-----------------+
   |  TẦNG THAY THẾ   | <--- Ma trận khóa K (Confusion)
   +--------+--------+
            |
            v
   +-----------------+
   |  TẦNG HOÁN VỊ   | <--- Ma trận hoán vị T (Diffusion)
   +--------+--------+
            |
            v
   +-----------------+
   |  TẦNG THAY THẾ   | <--- Khóa vòng kế tiếp K'
   +--------+--------+
            |
            v
         Bản mã C
```

#### Ví dụ minh họa trong slide (Trang 24-25)
- Bản rõ: `"SCOOBY DOO WHERE ARE YOU"` (20 ký tự).
- **Giai đoạn 1 (Gom nhóm 2 & Thay thế ma trận $K$)**:
  - Gom thành 10 cặp: `SC OO BY DO OW HE RE AR EY OU`.
  - Dùng ma trận $K = \begin{pmatrix} 5 & 17 \\ 4 & 15 \end{pmatrix}, B = \begin{pmatrix} 5 \\ 2 \end{pmatrix}$ mã hóa ra bản mã trung gian $C'$.
- **Giai đoạn 2 (Gom nhóm 5 & Hoán vị ma trận $T$)**:
  - Gom các phần tử thành các khối độ dài 5.
  - Dùng ma trận hoán vị $T$ cấp $5 \times 5$ xáo trộn vị trí trong từng khối, thu được $C''$.
- **Giai đoạn 3 (Gom nhóm 2 & Thay thế ma trận $K$ lần 2)**:
  - Tiếp tục chia đôi và nhân với ma trận $K$ một lần nữa.
  - Kết quả cuối cùng: `CT PK ZH HG HA VK PG YV SE QU`.

*Nhận xét*: Nhờ có bước hoán vị $T$ nằm giữa, một thay đổi nhỏ ở ký tự đầu tiên sau vài vòng sẽ khuếch tán ra toàn bộ chuỗi bản mã!

---

### 4.2 Mã hóa dựa trên Tác động nhóm (Group Action Ciphers)
Xét một nhóm toán học $(G, *)$. Theo tiên đề nhóm, mọi phần tử $x \in G$ đều có phần tử nghịch đảo $x^{-1} \in G$.
- **Cơ chế mã hóa theo nhóm**:
  - Chọn khóa là một phần tử $k \in G$.
  - Mã hóa: $c = m * k$.
  - Giải mã: $m = c * k^{-1}$.
- **Trường hợp nhóm tuần hoàn $\mathbb{Z}_p^*$ (với $p$ nguyên tố, $g$ là phần tử sinh)**:
  - Nhóm $G = \langle g \rangle = \{g^0, g^1, \dots, g^{p-2}\}$.
  - Khóa mã hóa $k$ tương ứng với lũy thừa $g^k$.
  - Mã hóa: $c \equiv m \cdot g^k \pmod p$.
  - Giải mã: $m \equiv c \cdot g^{-k} \pmod p$.
  - Phép nhân với $g^k$ đóng vai trò là một phép hoán vị toàn diện trên tập $\mathbb{Z}_p^*$.

---

### 4.3 Mạng Feistel & Cấu trúc Hộp thay thế (S-Box)

#### 1. Nguyên lý Mạng Feistel (Feistel Network)
Phát minh bởi Horst Feistel (IBM) vào những năm 1970, đây là kiến trúc nền tảng của hàng loạt thuật toán mã khối kinh điển (DES, Blowfish, RC5, Twofish).

```
                Khối đầu vào 2w bit
                 +-------+-------+
                 | L_{i-1}| R_{i-1}|
                 +-------+-------+
                     |       |
                     |       +----------------+
                     |       |                |
                     |       v                |
                     |   +-------+            |
                     |   | Hàm f |<-- Khóa K_i|
                     |   +-------+            |
                     |       |                |
                     v       v                |
                    (+) <----+                |
                     |                        |
                     |                        |
                 +---+------------------------+
                 |   |
                 v   v
             +-------+-------+
             |  L_i  |  R_i  |
             +-------+-------+
```

- **Mô hình hoạt động của một vòng Feistel thứ $i$**:
  Khối dữ liệu được chia làm 2 nửa bằng nhau: Nửa trái $L_{i-1}$ và Nửa phải $R_{i-1}$.
  $$\begin{cases} L_i = R_{i-1} \\ R_i = L_{i-1} \oplus f(R_{i-1}, K_i) \end{cases}$$
  *(Trong đó $\oplus$ là phép toán XOR bit, $f$ là hàm làm tròn bất kỳ, $K_i$ là khóa vòng).*
- **Ưu điểm thiên tài của Mạng Feistel**:
  - **Hàm $f$ không cần phải khả nghịch!** Cho dù hàm $f$ có phức tạp, phi tuyến hay làm mất mát thông tin đến mức nào, cấu trúc mạng Feistel vẫn tự động giải mã được hoàn hảo.
  - Quá trình giải mã sử dụng **chính xác cùng một phần cứng/mạch logic** với quá trình mã hóa, chỉ cần đảo ngược thứ tự các khóa vòng: $K_{16}, K_{15}, \dots, K_1$.

#### 2. Cấu trúc Toán học của Hộp thay thế (S-Box)
S-Box là thành phần **phi tuyến duy nhất** trong mạng SPN và Feistel, chịu trách nhiệm tạo nên tính Hỗn loạn (Confusion).
Trong slide (Trang 27), mô hình toán học hiện đại của S-Box (áp dụng trong AES) được định nghĩa là hàm hợp:
$$S(x) = A \circ P(x)$$
Trong đó:
1. $P(u)$ là phép nghịch đảo trong trường hữu hạn Galois Field $\text{GF}(2^8)$:
   $$P(u) = \begin{cases} u^{-1} & \text{nếu } u \text{ khả nghịch (khác 0)} \\ 0 & \text{nếu } u = 0 \end{cases}$$
2. $A(u)$ là phép biến đổi Affine trên không gian vector bit: $A(u) = M \cdot u \oplus C$.
Phép nghịch đảo trường hữu hạn mang tính phi tuyến tối đa, giúp chống lại phương pháp Thám mã vi sai (*Differential Cryptanalysis*) và Thám mã tuyến tính (*Linear Cryptanalysis*).

---

### 4.4 Chuẩn mã hóa dữ liệu DES (Data Encryption Standard)

#### 1. Tổng quan thông số
- **Năm ban hành**: NIST phê chuẩn năm 1977.
- **Kích thước khối dữ liệu**: 64 bit.
- **Kích thước bản mã**: 64 bit.
- **Kích thước khóa**:
  - Khóa nhập vào: 64 bit.
  - 8 bit kiểm tra tính chẵn lẻ (Parity bits ở vị trí 8, 16, 24, 32, 40, 48, 56, 64).
  - **Khóa thực tế hiệu dụng chỉ có 56 bit**.

#### 2. Quy trình 4 bước xử lý chi tiết trong DES
1. **Bước 1: Hoán vị khởi tạo $IP$ (Initial Permutation)**:
   - Khối 64-bit $M$ được xáo trộn các vị trí bit theo bảng cố định $IP$:
     $$M' = IP(M)$$
2. **Bước 2: Phân chia khối**:
   - Chia $M'$ thành 2 nửa bằng nhau:
     - Nửa trái: $L_0$ (32 bit).
     - Nửa phải: $R_0$ (32 bit).
3. **Bước 3: Thực hiện 16 vòng lặp Feistel**:
   - Với $i = 1, 2, \dots, 16$:
     $$L_i = R_{i-1}$$
     $$R_i = L_{i-1} \oplus f(R_{i-1}, K_i)$$
   - *Khóa vòng $K_i$*: Mỗi khóa vòng $K_i$ có độ dài 48 bit, được sinh ra từ khóa chính 56 bit thông qua bộ lập lịch khóa (*Key Schedule*: gồm các phép dịch bit và hoán vị nén PC-1, PC-2).
   - *Hàm vòng $f(R_{i-1}, K_i)$*:
     1. **Hộp mở rộng $E$ (Expansion)**: Mở rộng 32 bit của $R_{i-1}$ thành 48 bit bằng cách nhân bản một số bit.
     2. **Phép XOR**: $E(R_{i-1}) \oplus K_i$ (48 bit).
     3. **8 Hộp thay thế S-Box ($S_1 \to S_8$)**: 48 bit được chia thành 8 nhóm 6-bit. Mỗi nhóm đi qua một S-Box riêng biệt để cho ra kết quả 4-bit ($8 \times 4 = 32$ bit).
        - *Cơ chế tra S-Box*: Bit 1 và bit 6 xác định số hàng (0-3); 4 bit giữa xác định số cột (0-15).
     4. **Hoán vị $P$ (Permutation P-Box)**: 32 bit đầu ra của các S-Box được hoán vị để khuếch tán sang vòng kế tiếp.
4. **Bước 4: Hoán vị kết thúc $IP^{-1}$ (Inverse Initial Permutation)**:
   - Sau vòng 16, hai nửa được ghép ngược lại: $C' = (R_{16}, L_{16})$ (lưu ý hoán đổi vị trí phải-trái).
   - Áp dụng hoán vị nghịch đảo:
     $$C = IP^{-1}(C')$$
   - Cho ra bản mã hoàn chỉnh 64 bit.

---

### 4.5 Chuẩn 3DES (Triple DES)

#### 1. Lý do ra đời
Với không gian khóa chỉ $2^{56} \approx 7.2 \times 10^{16}$, vào năm 1999, tổ chức EFF (*Electronic Frontier Foundation*) đã chế tạo cỗ máy *Deep Crack* bẻ khóa thành công một bản mã DES trong **chưa đầy 23 giờ**.
Để tận dụng phần cứng DES sẵn có trong hệ thống ngân hàng và tài chính mà vẫn tăng cường độ an toàn, người ta phát triển **3DES**.

#### 2. Cấu trúc EDE (Encrypt - Decrypt - Encrypt)
Một chu trình 3DES thực hiện 3 lần thuật toán DES liên tiếp:
- **Quá trình Mã hóa**:
  $$C = E(K_3, D(K_2, E(K_1, M)))$$
- **Quá trình Giải mã**:
  $$M = D(K_1, E(K_2, D(K_3, C)))$$

```
        Bản rõ M
           |
           v
    +--------------+
    | DES ENCRYPT  |<--- Khóa K_1
    +------+-------+
           |
           v
    +--------------+
    | DES DECRYPT  |<--- Khóa K_2
    +------+-------+
           |
           v
    +--------------+
    | DES ENCRYPT  |<--- Khóa K_3
    +------+-------+
           |
           v
        Bản mã C
```

> **Tại sao bước giữa lại là DECRYPT (D) mà không phải ENCRYPT (E)?**
> Đây là thiết kế tương thích ngược cực kỳ thông minh! Nếu ta chọn $K_1 = K_2 = K_3 = K$, thì:
> $$C = E(K, D(K, E(K, M))) = E(K, M)$$
> Hệ thống 3DES sẽ lập tức biến thành DES tiêu chuẩn, tương thích với các máy đời cũ mà không cần thay đổi thuật toán.

#### 3. Ba tùy chọn khóa (Keying Options) trong 3DES

| Tùy chọn | Quan hệ giữa các khóa | Độ dài khóa thực tế | Mức độ an toàn chống tấn công | Ghi chú |
| :--- | :--- | :--- | :--- | :--- |
| **Option 1** | $K_1 \neq K_2 \neq K_3$ | $3 \times 56 = 168$ bit | 112 bit (do bị tấn công Meet-in-the-Middle) | An toàn nhất trong 3DES |
| **Option 2** | $K_1 \neq K_2$ và $K_3 = K_1$ | $2 \times 56 = 112$ bit | 80 bit | **Phổ biến nhất trong thực tế** |
| **Option 3** | $K_1 = K_2 = K_3$ | 56 bit | 56 bit | Hoàn toàn tương thích ngược với DES gốc |

---

## 5. BẢNG SO SÁNH TỔNG HỢP & ĐÚC KẾT ÔN THI

### 5.1 So sánh Mã bí mật (Symmetric) vs Mã công khai (Asymmetric)

| Đặc trưng so sánh | Mã hóa Khóa bí mật (Symmetric) | Mã hóa Khóa công khai (Asymmetric) |
| :--- | :--- | :--- |
| **Số lượng khóa** | **1 khóa duy nhất** (dùng chung cho cả $E$ và $D$) | **1 cặp khóa riêng biệt** (Public Key và Private Key) |
| **Tốc độ thực thi** | **Rất nhanh** (hàng trăm MB/s đến GB/s, tối ưu trên phần cứng) | **Rất chậm** (chậm hơn từ 100 đến 1.000 lần do phép toán số lớn) |
| **Quản lý khóa trong mạng $N$ người** | $\frac{N(N-1)}{2} = \mathcal{O}(N^2)$ khóa $\to$ Khó mở rộng | $2N = \mathcal{O}(N)$ khóa $\to$ Quản lý rất dễ dàng |
| **Phân phối khóa** | Cần kênh bảo mật cao cấp hoặc giao thức trao đổi khóa (như Diffie-Hellman) | Công bố tự do trên Internet (cần PKI / CA để xác thực) |
| **Ứng dụng tiêu biểu** | Mã hóa dữ liệu khối lớn, đường truyền VPN, HTTPS payload (AES, DES, ChaCha20) | Trao đổi khóa phiên, Chữ ký số, Xác thực danh tính (RSA, ECC, ElGamal) |

---

### 5.2 So sánh DES vs 3DES vs AES

| Thuật toán | Năm ra đời | Kích thước khối | Kích thước khóa | Cấu trúc giải thuật | Trạng thái an toàn hiện nay |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **DES** | 1977 | 64 bit | 56 bit | Mạng Feistel 16 vòng | **Đã lỗi thời, không an toàn** (khóa quá ngắn) |
| **3DES** | 1998 | 64 bit | 112 hoặc 168 bit | Mạng Feistel ($3 \times 16 = 48$ vòng) | Đang bị loại bỏ (chậm, khối 64-bit dễ bị Sweet32) |
| **AES** | 2001 | 128 bit | 128, 192, 256 bit | Mạng SPN (10, 12, 14 vòng) | **Tiêu chuẩn vàng toàn cầu, an toàn tuyệt đối** |

---

### 5.3 Tóm tắt công thức then chốt cần nhớ khi đi thi

1. **Mã tuyến tính (Affine Cipher)**:
   - Điều kiện: $\gcd(k, n) = 1$.
   - Mã hóa: $C \equiv (kP + b) \pmod n$.
   - Giải mã: $P \equiv k^{-1}(C - b) \pmod n$.
   - Tìm nghịch đảo: Dùng thuật toán Euclid mở rộng tìm $k^{-1} \pmod n$.
2. **Mã Ma trận (Hill Cipher mở rộng)**:
   - Điều kiện: $\gcd(\det(K), n) = 1$.
   - Mã hóa: $C \equiv (KP + B) \pmod n$.
   - Giải mã: $P \equiv K^{-1}(C - B) \pmod n$.
   - Ma trận nghịch đảo cấp 2:
     $$\begin{pmatrix} a & b \\ c & d \end{pmatrix}^{-1} \equiv (\det)^{-1} \begin{pmatrix} d & -b \\ -c & a \end{pmatrix} \pmod n$$
3. **Mã Hoán vị**:
   - $C = K \cdot P$ với $K$ là ma trận hoán vị.
   - Giải mã: $K^{-1} = K^T$.
4. **Mạng Feistel & DES**:
   - Vòng thứ $i$: $L_i = R_{i-1}$, $R_i = L_{i-1} \oplus f(R_{i-1}, K_i)$.
   - Khối DES: 64 bit, Khóa thực tế: 56 bit (8 bit kiểm tra chẵn lẻ).
5. **3DES**:
   - $C = E(K_3, D(K_2, E(K_1, M)))$.
   - $M = D(K_1, E(K_2, D(K_3, C)))$.
