# BÀI 3: MÃ HÓA KHÓA BÍ MẬT (SECRET-KEY / SYMMETRIC CRYPTOGRAPHY)
> **Tài liệu tham khảo chuyên sâu & Diễn giải chi tiết toàn bộ công thức, mệnh đề toán học theo slide bài giảng Môn Mã hóa - Mật mã (Khoa CNTT - ĐH Khoa học Tự nhiên).**

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
     - Định nghĩa & Công thức toán học (Diễn giải chi tiết điều kiện $\gcd(k, n) = 1$)
     - Ví dụ tính toán từng bước (Mã hóa / Giải mã "WAR")
     - Thám mã bằng Phân tích tần suất (Frequency Analysis Attack)
     - Thám mã bằng Vét cạn (Brute-Force Attack & Heuristics)
   - [Hệ mã Ma trận (Matrix / Hill Cipher mở rộng)](#32-hệ-mã-ma-trận-matrix--hill-cipher-mở-rộng)
     - Định nghĩa mã khối ma trận $C \equiv KP + B \pmod n$
     - Điều kiện ma trận khả nghịch $\gcd(\det(K), n) = 1$ & Cách tính ma trận nghịch đảo
     - Ví dụ mã hóa / giải mã "TH"
     - Thám mã biết bản rõ (Known-Plaintext Attack - KPA) giải hệ ma trận ("ATTACK" $\leftrightarrow$ "BTGTHM")
   - [Hệ mã Hoán vị khối (Block Permutation Cipher)](#33-hệ-mã-hoán-vị-khối-block-permutation-cipher)
     - Biểu diễn bằng ma trận hoán vị & tính chất $K^{-1} = K^T$
     - Đệm khối (Padding) & Ví dụ "THIS IS NIRVANA"
4. [Mật mã bí mật hiện đại](#4-mật-mã-bí-mật-hiện-đại)
   - [Mạng Hoán vị – Thay thế (Substitution-Permutation Network - SPN)](#41-mạng-hoán-vị--thay-thế-substitution-permutation-network---spn)
     - Kết hợp đa vòng (Multiple rounds)
     - Ví dụ tính toán chi tiết trong bài giảng ("SCOOBY DOO WHERE ARE YOU")
   - [Mã hóa dựa trên Tác động nhóm (Group Action Ciphers)](#42-mã-hóa-dựa-trên-tác-động-nhóm-group-action-ciphers)
   - [Mạng Feistel & Cấu trúc Hộp thay thế (S-Box)](#43-mạng-feistel--cấu-trúc-hộp-thay-thế-s-box)
     - Nguyên lý mạng Feistel: Tính đối xứng giữa mã hóa và giải mã (Hàm $f$ không cần khả nghịch)
     - Mô hình toán học của S-Box: Phép biến đổi phi tuyến và affine $S(x) = A \circ P(x)$
   - [Chuẩn mã hóa dữ liệu DES (Data Encryption Standard)](#44-chuẩn-mã-hóa-dữ-liệu-des-data-encryption-standard)
     - Lịch sử & Thông số tổng quan (Khối 64 bit, Khóa 56 bit)
     - 4 bước xử lý: Hoán vị khởi tạo $IP$, 16 vòng Feistel, Hoán vị nghịch đảo $IP^{-1}$
     - Cấu trúc hàm vòng $f(R_{i-1}, K_i)$
   - [Chuẩn 3DES (Triple DES)](#45-chuẩn-3des-triple-des)
     - Cấu trúc EDE (Encrypt - Decrypt - Encrypt)
     - 3 tùy chọn khóa (Keying Options) & Tính tương thích ngược
5. [Bảng so sánh tổng hợp & Đúc kết ôn thi](#5-bảng-so-sánh-tổng-hợp--đúc-kết-ôn-thi)
   - [So sánh Mã bí mật (Symmetric) vs Mã công khai (Asymmetric)](#51-so-sánh-mã-bí-mật-vs-mã-công-khai)
   - [So sánh DES vs 3DES vs AES](#52-so-sánh-des-vs-3des-vs-aes)
   - [Bảng tra cứu toàn bộ ký hiệu & công thức toán học](#53-bảng-tra-cứu-toàn-bộ-ký-hiệu--công-thức-toán-học)

---

## 1. TỔNG QUAN & NGUYÊN LÝ THIẾT KẾ HỆ MÃ BÍ MẬT

### 1.1 Bản chất của Mật mã đối xứng (Symmetric Cryptosystem)
- **Định nghĩa**: Hệ mã khóa bí mật (*Secret-Key Cryptosystem*), hay còn gọi là **Hệ mã đối xứng (*Symmetric Cryptosystem*)**, là hệ thống mật mã mà trong đó các đối tác tham gia trao đổi thông tin (Alice và Bob) **dùng chung một khóa bí mật $k$** cho cả quá trình mã hóa lẫn giải mã.
- **Hai tính chất cốt lõi**:
  1. **Tính đối xứng (Symmetric)**: Kiến thức về khóa mã hóa cho phép suy ra trực tiếp khóa giải mã (hoặc chúng giống hệt nhau: $k_{\text{mã hóa}} = k_{\text{giải mã}} = k$).
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
Về mặt toán học hình thức, một hệ mã bí mật được định nghĩa là một bộ 5 thành phần:
$$(\mathcal{M}, \mathcal{C}, \mathcal{K}, \mathcal{E}, \mathcal{D})$$

#### Diễn giải chi tiết từng thành phần:
1. $\mathcal{M}$ (**Plaintext / Message Space - Không gian bản rõ**): Tập hợp tất cả các thông điệp ban đầu chưa mã hóa mà người dùng có thể tạo ra.
2. $\mathcal{C}$ (**Ciphertext Space - Không gian bản mã**): Tập hợp tất cả các thông điệp đã qua xử lý xáo trộn, xuất hiện trên đường truyền.
3. $\mathcal{K}$ (**Key Space - Không gian khóa**): Tập hợp tất cả các giá trị khóa hợp lệ có thể được lựa chọn theo giải thuật.
4. $\mathcal{E} = \{E_k : k \in \mathcal{K}\}$: Tập hợp các thuật toán/hàm mã hóa ứng với từng khóa $k$. Ánh xạ $E_k: \mathcal{M} \to \mathcal{C}$.
5. $\mathcal{D} = \{D_k : k \in \mathcal{K}\}$: Tập hợp các thuật toán/hàm giải mã ứng với từng khóa $k$. Ánh xạ $D_k: \mathcal{C} \to \mathcal{M}$.

#### Mệnh đề về Tính khả nghịch (Invertibility Condition):
$$\forall m \in \mathcal{M}: \quad D_k(E_k(m)) = m$$

> **Diễn giải mệnh đề bằng lời**:
> - Ký hiệu $\forall m \in \mathcal{M}$ đọc là *"với mọi bản rõ $m$ thuộc không gian bản rõ $\mathcal{M}$"*.
> - Mệnh đề này khẳng định: **Khi ta lấy bản rõ $m$, đem mã hóa bằng khóa $k$ để thu được bản mã $c = E_k(m)$, rồi lập tức đem giải mã $c$ bằng chính khóa $k$ đó ($D_k(c)$), thì kết quả thu được bắt buộc phải trả về chính xác bản rõ $m$ ban đầu, không được sai lệch dù chỉ 1 bit**.
> - **Ý nghĩa toán học**: Hàm mã hóa $E_k$ bắt buộc phải là một **đơn ánh (Injective function)**. Không bao giờ được phép xảy ra trường hợp hai bản rõ khác nhau $m_1 \neq m_2$ lại bị mã hóa thành cùng một bản mã $c$ (tức không được có $E_k(m_1) = E_k(m_2)$). Nếu vi phạm, khi bên nhận cầm bản mã $c$ sẽ hoàn toàn không thể biết bản tin gốc là $m_1$ hay $m_2$.

---

### 1.3 Nguyên lý an toàn & Không gian tham số
Hệ mã bí mật muốn đạt được mức độ an toàn thực tiễn phải tuân thủ các nguyên lý sau:
1. **Nguyên lý Kerckhoffs (Nguyên lý cơ bản của mật mã học)**:
   > *"Độ an toàn của một hệ thống mật mã không được phụ thuộc vào sự bí mật của thuật toán, mà **chỉ phụ thuộc duy nhất vào sự bí mật của khóa**."*
   Thuật toán mã hóa $E$ và giải mã $D$ luôn được xem là công khai hoàn toàn cho kẻ tấn công biết.

2. **Yêu cầu về độ lớn không gian tham số**:
   - Không gian bản rõ $\mathcal{M}$, không gian bản mã $\mathcal{C}$, và đặc biệt là **không gian khóa $\mathcal{K}$ phải đủ lớn** để kẻ tấn công không thể sử dụng phương pháp vét cạn (*Brute-force attack*).
   - *Ví dụ*: Một khóa 56-bit có $|\mathcal{K}| = 2^{56} \approx 7.2 \times 10^{16}$ khóa (đã bị bẻ gãy dễ dàng trong vài giờ). Ngày nay, không gian khóa tối thiểu phải đạt $2^{128}$ hoặc $2^{256}$.

3. **Yêu cầu về độ phức tạp của phép biến đổi**:
   - Các phép biến đổi trong hàm $E_k$ và $D_k$ phải đủ phức tạp và mang tính phi tuyến cao để chống lại các phương pháp thám mã đại số (*Algebraic Cryptanalysis*) và thám mã thống kê (*Statistical / Frequency Analysis*).

---

### 1.4 Các mô hình tấn công thám mã cơ bản
Dựa vào lượng thông tin mà kẻ thám mã (Eve) có trong tay, các kỹ thuật tấn công được phân loại thành 4 cấp độ tăng dần:

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
   - Hai kỹ thuật COA cơ bản:
     + **Tấn công vét cạn (Brute-force attack)**: Thử lần lượt từng khóa $k \in \mathcal{K}$ để tính $m = D_k(c)$. Nếu $m$ là một văn bản có nghĩa (ngôn ngữ tự nhiên), $k$ có khả năng cao là khóa đúng.
     + **Tấn công phân tích tần suất (Frequency analysis attack)**: Khai thác quy luật phân phối xác suất không đều của các ký tự hoặc nhóm ký tự trong ngôn ngữ tự nhiên.
2. **Tấn công khi biết bản rõ (Known-Plaintext Attack - KPA)**:
   - Kẻ tấn công sở hữu một số cặp bản rõ - bản mã tương ứng $\{(m_1, c_1), (m_2, c_2), \dots, (m_t, c_t)\}$ được mã hóa bằng cùng một khóa $k$.
   - Mục tiêu: Tìm khóa bí mật $k$ để giải mã toàn bộ các bản mã khác. Kỹ thuật chung: Thiết lập hệ phương trình quan hệ từ các cặp $(m_i, c_i)$ và giải đại số.

---

## 2. HAI KỸ THUẬT BIẾN ĐỔI NỀN TẢNG

Hầu hết mọi hệ mã hóa bí mật từ cổ điển đến hiện đại đều được xây dựng dựa trên sự kết hợp khéo léo của hai phép biến đổi cơ bản:

### 2.1 Phép thay thế (Substitution / Replace)
- **Khái niệm**: Mỗi ký hiệu (ký tự, bit, byte hoặc khối bit) trong thông điệp đầu vào được thay thế bằng một ký hiệu khác theo một quy tắc xác định phụ thuộc vào khóa $k$.
- **Ví dụ kinh điển**:
  - Mã Caesar: Dịch chuyển vòng quanh bảng chữ cái $k$ vị trí.
  - Phép thế Affine: $C \equiv (a \cdot P + b) \pmod n$.
  - Hộp thay thế phi tuyến S-Box trong DES và AES.

---

### 2.2 Phép hoán vị / Chuyển vị (Permutation / Transposition)
- **Khái niệm**: Thứ tự hoặc vị trí của các ký hiệu trong thông điệp bị xáo trộn, sắp xếp lại theo một trật tự mới mà không làm thay đổi giá trị nội dung của bản thân ký hiệu đó.
- **Biểu diễn toán học hình thức**:
  Một phép hoán vị $\sigma$ trên tập chỉ số $\{0, 1, \dots, m-1\}$ là một **song ánh (Bijection)**:
  $$\sigma: \{0, 1, \dots, m-1\} \to \{0, 1, \dots, m-1\}$$
  Khối thông điệp gồm $m$ ký hiệu $M = m_0 m_1 \dots m_{m-1}$ sẽ được chuyển đổi vị trí thành:
  $$C = m_{\sigma(0)} m_{\sigma(1)} \dots m_{\sigma(m-1)}$$

> **Diễn giải mệnh đề toán học**:
> - Ký hiệu $\sigma$ (đọc là *"sigma"*) đại diện cho quy tắc hoán vị.
> - Tính chất song ánh bảo đảm: **Mỗi vị trí cũ được đưa sang đúng một vị trí mới duy nhất; không có hai ký tự nào bị gộp vào cùng một chỗ và không có vị trí nào bị bỏ trống**.
> - *Ví dụ trực quan*: Với khối 3 ký tự $\{0, 1, 2\}$, định nghĩa $\sigma(0) = 2, \sigma(1) = 0, \sigma(2) = 1$. Khi áp dụng vào từ `"CAT"` ($m_0=C, m_1=A, m_2=T$), từ mới thu được là $m_{\sigma(0)} m_{\sigma(1)} m_{\sigma(2)} = m_2 m_0 m_1 = \text{"TCA"}$.

---

### 2.3 Nguyên lý Hỗn loạn (Confusion) & Khuếch tán (Diffusion) của Claude Shannon
Năm 1949, nhà toán học lỗi lạc Claude Shannon đã đặt nền móng lý thuyết cho mật mã hiện đại với hai đặc tính thiết kế sống còn:

| Đặc tính | Bản chất & Ý nghĩa | Kỹ thuật hiện thực | Mục tiêu chống tấn công |
| :--- | :--- | :--- | :--- |
| **Hỗn loạn (Confusion)** | Làm cho mối quan hệ giữa **khóa bí mật $K$** và **bản mã $C$** trở nên cực kỳ phức tạp, mờ mịt và phi tuyến. Kẻ tấn công không thể đoán được khóa từ bản mã. | Thực hiện thông qua **Phép thay thế (Substitution / S-Box)**. | Ngăn chặn kẻ thám mã suy luận ra khóa bí mật $K$ bằng các phương pháp thống kê hoặc giải hệ đại số. |
| **Khuếch tán (Diffusion)** | Làm cho mỗi bit của **bản rõ $M$** và mỗi bit của **khóa $K$** ảnh hưởng đến **rất nhiều bit của bản mã $C$** (và ngược lại). | Thực hiện thông qua **Phép hoán vị (Permutation / P-Box / ShiftRows / MixColumns)**. | Xóa sạch dấu vết tần suất của ngôn ngữ tự nhiên; phân tán tính chất cục bộ ra toàn bộ khối mã. |

- **Hiệu ứng thác đổ (Avalanche Effect)**: Kết quả của sự kết hợp hoàn hảo giữa Confusion và Diffusion: chỉ cần thay đổi **1 bit duy nhất** của bản rõ hoặc khóa, ít nhất **50% số bit của bản mã** sẽ thay đổi ngẫu nhiên ở đầu ra.

---

## 3. CÁC HỆ MÃ BÍ MẬT CỔ ĐIỂN & KỸ THUẬT THÁM MÃ

### 3.1 Hệ mã tuyến tính (Linear / Affine Cipher)

#### 1. Định nghĩa toán học & Giải thích cặn kẽ từng đại lượng
Xét trên bảng chữ cái gồm $n$ ký tự (với tiếng Anh chuẩn, $n = 26$, gán $A = 0, B = 1, \dots, Z = 25$).
- **Không gian khóa**: Cặp số nguyên $(k, b)$ với $k, b \in \mathbb{Z}_n = \{0, 1, \dots, n-1\}$.
- **Điều kiện tiên quyết bắt buộc**:
  $$\gcd(k, n) = 1$$

---

#### 🌟 DIỄN GIẢI TOÀN DIỆN MỆNH ĐỀ $\gcd(k, n) = 1$:

1. **Ký hiệu $\gcd(k, n)$ là gì?**
   - Viết tắt của thuật ngữ tiếng Anh: **Greatest Common Divisor** (Ước số chung lớn nhất).
   - $\gcd(k, n)$ là số nguyên dương lớn nhất là ước chung của cả $k$ và $n$.

2. **Mệnh đề $\gcd(k, n) = 1$ có ý nghĩa gì?**
   - Mệnh đề này phát biểu rằng: **Ước số chung lớn nhất giữa số nhân $k$ và độ dài bảng chữ cái $n$ phải bằng 1**.
   - Nói cách khác: $k$ và $n$ là hai số **nguyên tố cùng nhau** (*coprime* hay *relatively prime*) — chúng không chia sẻ bất kỳ ước số chung nào khác ngoài số 1.

3. **TẠI SAO ĐIỀU KIỆN $\gcd(k, n) = 1$ LÀ BẮT BUỘC VÀ SỐNG CÒN?**
   - **Lý do giải mã**: Để giải mã, ta cần tìm một số $k^{-1}$ sao cho $k \cdot k^{-1} \equiv 1 \pmod n$. Theo Định lý số học Bézout, số nghịch đảo nhân modulo $k^{-1}$ **chỉ tồn tại khi và chỉ khi** $\gcd(k, n) = 1$.
   - **Lý do bảo toàn thông tin (Tính đơn ánh)**: Nếu chọn $k$ sao cho $\gcd(k, n) = d > 1$, thì hàm mã hóa sẽ **bị mất tính đơn ánh**. Khi đó, sẽ có nhiều ký tự bản rõ khác nhau bị mã hóa thành **cùng một ký tự bản mã duy nhất**! Dữ liệu bị trùng lặp, gây mất mát thông tin và **hoàn toàn không thể giải mã được**.

4. **Ví dụ chứng minh phản chứng (Nếu chọn $\gcd(k, n) \neq 1$ thì chuyện gì xảy ra?)**:
   - Giả sử với bảng chữ cái tiếng Anh $n = 26$, người dùng bất cẩn chọn khóa $k = 4, b = 0$.
   - Ta thấy $\gcd(4, 26) = 2 \neq 1$ (vi phạm điều kiện).
   - Bây giờ hãy thử mã hóa hai ký tự bản rõ hoàn toàn khác nhau:
     - Ký tự $A$ (ứng với số 0): $C_1 \equiv (4 \times 0 + 0) = 0 \equiv 0 \pmod{26} \leftrightarrow \mathbf{A}$.
     - Ký tự $N$ (ứng với số 13): $C_2 \equiv (4 \times 13 + 0) = 52 = 2 \times 26 + 0 \equiv 0 \pmod{26} \leftrightarrow \mathbf{A}$.
   - **Hậu quả**: Cả chữ $A$ và chữ $N$ đều bị biến thành chữ $A$! Khi Bob nhận được chữ $A$ trong bản mã, Bob hoàn toàn bất lực, không thể biết Alice đã gửi chữ $A$ hay chữ $N$.

---

#### 2. Công thức Mã hóa & Giải mã:
- **Công thức Mã hóa**:
  $$E_{(k, b)}(P) \equiv C \equiv (k \cdot P + b) \pmod n$$
  *(Nghĩa là: Lấy mã số của ký tự rõ $P$, nhân với hệ số $k$, cộng với độ dịch $b$, rồi chia lấy phần dư cho $n$).*
- **Công thức Giải mã**:
  $$D_{(k, b)}(C) \equiv P \equiv k^{-1} \cdot (C - b) \pmod n$$
  *(Nghĩa là: Lấy mã số của bản mã $C$, trừ đi độ dịch $b$, rồi nhân với phần tử nghịch đảo modulo $k^{-1}$, sau đó chia lấy phần dư cho $n$).*

> **Lưu ý đặc biệt về ký hiệu $k^{-1} \pmod n$**:
> Ký hiệu $k^{-1}$ trong số học modulo **KHÔNG PHẢI là phép chia phân số $\frac{1}{k}$ hay số thập phân**!
> $k^{-1}$ là một **số nguyên** $x \in \{0, 1, \dots, n-1\}$ thỏa mãn phương trình đồng dư:
> $$k \cdot x \equiv 1 \pmod n$$

---

#### 3. Ví dụ tính toán từng bước (Mã hóa / Giải mã "WAR")
*(Theo ví dụ trang 11-12 trong bài giảng)*
- **Tham số**:
  - Bảng chữ cái tiếng Anh $n = 26$.
  - Khóa: $k = 7, b = 10$.
  - Kiểm tra điều kiện: $\gcd(7, 26) = 1$ (do 7 là số nguyên tố và 26 không chia hết cho 7 $\to$ hoàn toàn hợp lệ).
  - Bản rõ cần mã hóa: $P = \text{"WAR"}$.

##### Bước 1: Mã hóa
Chuyển đổi từng chữ cái thành số theo thứ tự $A=0, B=1, \dots, Z=25$:
- $W \leftrightarrow 22$
- $A \leftrightarrow 00$
- $R \leftrightarrow 17$

Áp dụng công thức $C \equiv (7 \cdot P + 10) \pmod{26}$:
- Với chữ $W (22)$:
  $$C_1 \equiv (7 \cdot 22 + 10) = 154 + 10 = 164 = 6 \cdot 26 + 8 \equiv 8 \pmod{26} \leftrightarrow \mathbf{I}$$
- Với chữ $A (00)$:
  $$C_2 \equiv (7 \cdot 0 + 10) = 0 + 10 = 10 \equiv 10 \pmod{26} \leftrightarrow \mathbf{K}$$
- Với chữ $R (17)$:
  $$C_3 \equiv (7 \cdot 17 + 10) = 119 + 10 = 129 = 4 \cdot 26 + 25 \equiv 25 \pmod{26} \leftrightarrow \mathbf{Z}$$

$\implies$ Bản mã thu được: $C = \text{"IKZ"} \leftrightarrow (08, 10, 25)$.

##### Bước 2: Giải mã
1. **Tìm phần tử nghịch đảo nhân của $k = 7$ modulo 26 (tức tìm $7^{-1} \pmod{26}$)**:
   Ta cần tìm một số nguyên $x$ sao cho $7 \cdot x \equiv 1 \pmod{26}$.
   Sử dụng thuật toán Euclid mở rộng giải phương trình nghiệm nguyên $7x + 26y = \gcd(7, 26) = 1$:
   - Thực hiện chia Euclid liên tiếp:
     $$26 = 3 \cdot 7 + 5 \implies 5 = 26 - 3 \cdot 7$$
     $$7 = 1 \cdot 5 + 2 \implies 2 = 7 - 1 \cdot 5$$
     $$5 = 2 \cdot 2 + 1 \implies 1 = 5 - 2 \cdot 2$$
   - Đi ngược lại để biểu diễn số 1 qua 7 và 26:
     $$1 = 5 - 2 \cdot (7 - 1 \cdot 5) = 3 \cdot 5 - 2 \cdot 7$$
     $$1 = 3 \cdot (26 - 3 \cdot 7) - 2 \cdot 7 = 3 \cdot 26 - 11 \cdot 7$$
   - Lấy modulo 26 hai vế:
     $$-11 \cdot 7 \equiv 1 \pmod{26}$$
     $$\implies 7^{-1} \equiv -11 \equiv (26 - 11) = 15 \pmod{26}$$
   *(Thử lại: $7 \cdot 15 = 105 = 4 \cdot 26 + 1 \equiv 1 \pmod{26} \implies$ Chính xác tuyệt đối).*

2. **Khôi phục bản rõ**: Áp dụng công thức $P \equiv 15 \cdot (C - 10) \pmod{26}$:
   - Với chữ $I (08)$:
     $$P_1 \equiv 15 \cdot (8 - 10) = 15 \cdot (-2) = -30 = -2 \cdot 26 + 22 \equiv 22 \pmod{26} \leftrightarrow \mathbf{W}$$
   - Với chữ $K (10)$:
     $$P_2 \equiv 15 \cdot (10 - 10) = 15 \cdot 0 = 0 \equiv 0 \pmod{26} \leftrightarrow \mathbf{A}$$
   - Với chữ $Z (25)$:
     $$P_3 \equiv 15 \cdot (25 - 10) = 15 \cdot 15 = 225 = 8 \cdot 26 + 17 \equiv 17 \pmod{26} \leftrightarrow \mathbf{R}$$

$\implies$ Bản rõ được khôi phục chính xác $P = \text{"WAR"}$.

---

#### 4. Thám mã Hệ mã tuyến tính bằng Phân tích tần suất (Frequency Analysis)
*(Theo ví dụ trang 14 trong slide bài giảng)*

Trong tiếng Anh, tần suất xuất hiện tự nhiên của các chữ cái có đặc trưng bất đối xứng rõ rệt:
- Chữ cái xuất hiện nhiều nhất: **E** (mã số 04, chiếm khoảng 12.7%).
- Chữ cái xuất hiện nhiều thứ hai: **T** (mã số 19, chiếm khoảng 9.1%).

**Tình huống thám mã**:
Kẻ tấn công thu được một bản mã dài, thống kê tần suất xuất hiện các ký tự thấy:
- Ký tự xuất hiện nhiều nhất trong bản mã là **V** (mã số 21).
- Ký tự xuất hiện nhiều thứ hai trong bản mã là **E** (mã số 04).

Ta đặt giả thiết:
- Chữ cái rõ $E (04)$ đã bị mã hóa thành chữ mã $V (21)$.
- Chữ cái rõ $T (19)$ đã bị mã hóa thành chữ mã $E (04)$.

Thiết lập hệ phương trình đồng dư bậc nhất 2 ẩn $k, b$:
$$\begin{cases} 4 \cdot k + b \equiv 21 \pmod{26} \quad (1) \\ 19 \cdot k + b \equiv 4 \pmod{26} \quad (2) \end{cases}$$

**Các bước giải chi tiết**:
1. Lấy phương trình (2) trừ phương trình (1) để triệt tiêu ẩn $b$:
   $$(19k + b) - (4k + b) \equiv 4 - 21 \pmod{26}$$
   $$15k \equiv -17 \pmod{26}$$
   Vì $-17 \equiv (26 - 17) = 9 \pmod{26}$, phương trình trở thành:
   $$15k \equiv 9 \pmod{26}$$
2. Để tìm $k$, ta cần nhân cả hai vế với nghịch đảo của 15 modulo 26 ($15^{-1} \pmod{26}$):
   Ta tìm số $x$ sao cho $15x \equiv 1 \pmod{26}$.
   Nhận thấy: $15 \cdot 7 = 105 = 4 \cdot 26 + 1 \equiv 1 \pmod{26} \implies 15^{-1} \equiv 7 \pmod{26}$.
   Nhân cả hai vế với 7:
   $$k \equiv 9 \cdot 7 = 63 = 2 \cdot 26 + 11 \equiv 11 \pmod{26}$$
3. Thay giá trị $k = 11$ vào phương trình (1):
   $$4 \cdot 11 + b \equiv 21 \pmod{26}$$
   $$44 + b \equiv 21 \pmod{26}$$
   Vì $44 = 1 \cdot 26 + 18 \equiv 18 \pmod{26}$, ta có:
   $$18 + b \equiv 21 \implies b \equiv 21 - 18 = 3 \pmod{26}$$

**Kết luận**: Cặp khóa tìm được là $(k = 11, b = 3)$. Dùng khóa này giải mã thử toàn bộ văn bản để kiểm tra tính hợp lý.

---

#### 5. Thám mã bằng Vét cạn (Brute-Force Attack)
- **Tính toán không gian khóa $|\mathcal{K}|$**:
  - Giá trị dịch chuyển $b$: Có thể nhận bất kỳ giá trị nào trong tập $\{0, 1, \dots, 25\} \implies$ có **26 khả năng**.
  - Giá trị nhân $k$: Bắt buộc phải thỏa mãn $\gcd(k, 26) = 1$. Số lượng các số nhỏ hơn 26 và nguyên tố cùng nhau với 26 chính là giá trị hàm phi Euler $\varphi(26)$:
    $$\varphi(26) = \varphi(2 \times 13) = (2 - 1) \times (13 - 1) = 1 \times 12 = 12$$
    Cụ thể, tập hợp các giá trị hợp lệ của $k$ là:
    $$k \in \{1, 3, 5, 7, 9, 11, 15, 17, 19, 21, 23, 25\} \implies \text{có } 12 \text{ khả năng}$$
  - Tổng số cặp khóa $(k, b)$ khả dĩ:
    $$|\mathcal{K}| = 12 \times 26 = 312 \text{ khóa}$$
- Với kích thước không gian khóa cực nhỏ (chỉ 312 trường hợp), máy tính thông thường chỉ mất **dưới 1 phần nghìn giây** để thử toàn bộ và bẻ gãy hệ mã.

---

### 3.2 Hệ mã Ma trận (Matrix / Hill Cipher mở rộng)

#### 1. Định nghĩa toán học & Điều kiện ma trận khả nghịch
Mã ma trận là sự mở rộng đa chiều của mã Affine lên khối gồm $m$ ký hiệu (Mã khối - Block cipher):
- **Khóa**: Cặp $(K, B)$, trong đó:
  - $K$ là ma trận vuông cấp $m \times m$ với các phần tử là số nguyên thuộc $\mathbb{Z}_n$.
  - $B$ là vector cột cấp $m \times 1$ với các phần tử thuộc $\mathbb{Z}_n$.
- **Điều kiện khả nghịch bắt buộc**:
  $$\gcd(\det(K), n) = 1$$

---

#### 🌟 DIỄN GIẢI TOÀN DIỆN MỆNH ĐỀ $\gcd(\det(K), n) = 1$:

1. **Ký hiệu $\det(K)$ là gì?**
   - Viết tắt của từ tiếng Anh **Determinant** (Định thức của ma trận vuông $K$).
   - Với ma trận cấp $2 \times 2$: $K = \begin{pmatrix} a & b \\ c & d \end{pmatrix}$, định thức được tính bằng tích đường chéo chính trừ tích đường chéo phụ:
     $$\det(K) = a \cdot d - b \cdot c$$

2. **Mệnh đề $\gcd(\det(K), n) = 1$ có ý nghĩa gì?**
   - Mệnh đề này khẳng định: **Ước số chung lớn nhất giữa định thức $\det(K)$ và kích thước bảng chữ cái $n$ phải bằng 1** (tức định thức $\det(K)$ và số $n$ phải là hai số nguyên tố cùng nhau).

3. **TẠI SAO ĐIỀU KIỆN NÀY LÀ BẮT BUỘC?**
   - Trong đại số tuyến tính trên vành số nguyên modulo $n$, một ma trận $K$ tồn tại ma trận nghịch đảo $K^{-1}$ **khi và chỉ khi định thức của nó khả nghịch modulo $n$** (tức tồn tại số nghịch đảo $(\det(K))^{-1} \pmod n$).
   - Nếu $\gcd(\det(K), n) \neq 1$, ta không thể tìm được $(\det(K))^{-1}$, ma trận $K$ không thể nghịch đảo, và việc giải mã là **hoàn toàn bất khả thi**.

---

#### 2. Công thức Mã hóa & Giải mã:
- **Mã hóa khối vector $P$**:
  $$C \equiv (K \cdot P + B) \pmod n$$
- **Giải mã**:
  $$P \equiv K^{-1} \cdot (C - B) \pmod n$$

#### Công thức tính ma trận nghịch đảo $K^{-1} \pmod n$:
$$K^{-1} \equiv (\det(K))^{-1} \cdot \text{adj}(K) \pmod n$$
Trong đó:
- $(\det(K))^{-1} \pmod n$: Là nghịch đảo nhân của số nguyên $\det(K)$ theo modulo $n$.
- $\text{adj}(K)$: Là **Ma trận phụ hợp** (Adjugate Matrix / Classical Adjoint).
  Đối với ma trận cấp $2 \times 2$: $K = \begin{pmatrix} a & b \\ c & d \end{pmatrix}$, ma trận phụ hợp được tính cực kỳ đơn giản:
  $$\text{adj}(K) = \begin{pmatrix} d & -b \\ -c & a \end{pmatrix}$$
  > **Quy tắc nhớ**: **Đổi chỗ hai phần tử trên đường chéo chính ($a \leftrightarrow d$), và đổi dấu hai phần tử trên đường chéo phụ (thêm dấu âm vào $b$ và $c$)**.

---

#### 3. Ví dụ tính toán Mã hóa & Giải mã "TH"
*(Theo ví dụ trang 17 trong bài giảng)*
- Kích thước khối $m = 2$, bảng chữ cái $n = 26$.
- Khóa ma trận $K = \begin{pmatrix} 5 & 17 \\ 4 & 15 \end{pmatrix}$, vector độ dịch $B = \begin{pmatrix} 5 \\ 2 \end{pmatrix}$.
- Bản rõ cần mã hóa: $P = \text{"TH"}$. Chuyển sang vector số: $T \leftrightarrow 19, H \leftrightarrow 07 \implies P = \begin{pmatrix} 19 \\ 7 \end{pmatrix}$.

##### Giai đoạn 1: Mã hóa
$$K \cdot P = \begin{pmatrix} 5 & 17 \\ 4 & 15 \end{pmatrix} \begin{pmatrix} 19 \\ 7 \end{pmatrix} = \begin{pmatrix} 5 \cdot 19 + 17 \cdot 7 \\ 4 \cdot 19 + 15 \cdot 7 \end{pmatrix} = \begin{pmatrix} 95 + 119 \\ 76 + 105 \end{pmatrix} = \begin{pmatrix} 214 \\ 181 \end{pmatrix}$$
Cộng vector $B$:
$$K \cdot P + B = \begin{pmatrix} 214 + 5 \\ 181 + 2 \end{pmatrix} = \begin{pmatrix} 219 \\ 183 \end{pmatrix}$$
Lấy modulo 26 từng phần tử:
- Phần tử trên: $219 = 8 \cdot 26 + 11 \equiv 11 \pmod{26} \leftrightarrow \mathbf{L}$.
- Phần tử dưới: $183 = 7 \cdot 26 + 1 \equiv 1 \pmod{26} \leftrightarrow \mathbf{B}$.

$\implies$ Bản mã thu được: $C = \text{"LB"}$.

##### Giai đoạn 2: Giải mã
1. **Tìm ma trận nghịch đảo $K^{-1} \pmod{26}$**:
   - Tính định thức:
     $$\det(K) = 5 \cdot 15 - 17 \cdot 4 = 75 - 68 = 7$$
   - Kiểm tra điều kiện khả nghịch: $\gcd(7, 26) = 1$ (thỏa mãn).
   - Tìm nghịch đảo của định thức: $7^{-1} \pmod{26}$.
     Vì $7 \cdot 15 = 105 = 4 \cdot 26 + 1 \equiv 1 \pmod{26} \implies (\det(K))^{-1} \equiv 15 \pmod{26}$.
   - Tìm ma trận phụ hợp $\text{adj}(K)$:
     $$\text{adj}(K) = \begin{pmatrix} 15 & -17 \\ -4 & 5 \end{pmatrix}$$
     Đổi các số âm sang đồng dư dương modulo 26:
     $-17 \equiv 26 - 17 = 9 \pmod{26}$
     $-4 \equiv 26 - 4 = 22 \pmod{26}$
     $$\implies \text{adj}(K) \equiv \begin{pmatrix} 15 & 9 \\ 22 & 5 \end{pmatrix} \pmod{26}$$
   - Nhân với $(\det(K))^{-1} = 15$:
     $$K^{-1} \equiv 15 \cdot \begin{pmatrix} 15 & 9 \\ 22 & 5 \end{pmatrix} = \begin{pmatrix} 15 \cdot 15 & 15 \cdot 9 \\ 15 \cdot 22 & 15 \cdot 5 \end{pmatrix} = \begin{pmatrix} 225 & 135 \\ 330 & 75 \end{pmatrix} \pmod{26}$$
     Lấy modulo 26:
     - $225 = 8 \cdot 26 + 17 \equiv 17$
     - $135 = 5 \cdot 26 + 5 \equiv 5$
     - $330 = 12 \cdot 26 + 18 \equiv 18$
     - $75 = 2 \cdot 26 + 23 \equiv 23$
     $$\implies K^{-1} \equiv \begin{pmatrix} 17 & 5 \\ 18 & 23 \end{pmatrix} \pmod{26}$$

2. **Khôi phục bản rõ $P$**:
   - Trừ vector độ dịch:
     $$C - B = \begin{pmatrix} 11 \\ 1 \end{pmatrix} - \begin{pmatrix} 5 \\ 2 \end{pmatrix} = \begin{pmatrix} 11 - 5 \\ 1 - 2 \end{pmatrix} = \begin{pmatrix} 6 \\ -1 \end{pmatrix} \equiv \begin{pmatrix} 6 \\ 25 \end{pmatrix} \pmod{26}$$
   - Nhân với ma trận nghịch đảo:
     $$P \equiv K^{-1} \cdot (C - B) = \begin{pmatrix} 17 & 5 \\ 18 & 23 \end{pmatrix} \begin{pmatrix} 6 \\ 25 \end{pmatrix} = \begin{pmatrix} 17 \cdot 6 + 5 \cdot 25 \\ 18 \cdot 6 + 23 \cdot 25 \end{pmatrix} = \begin{pmatrix} 102 + 125 \\ 108 + 575 \end{pmatrix} = \begin{pmatrix} 227 \\ 683 \end{pmatrix} \pmod{26}$$
     Lấy modulo 26:
     - $227 = 8 \cdot 26 + 19 \equiv 19 \pmod{26} \leftrightarrow \mathbf{T}$
     - $683 = 26 \cdot 26 + 7 \equiv 7 \pmod{26} \leftrightarrow \mathbf{H}$

$\implies$ Bản rõ được khôi phục chính xác $P = \text{"TH"}$.

---

#### 4. Thám mã Hệ mã Ma trận: Tấn công Biết bản rõ (Known-Plaintext Attack - KPA)
*(Theo ví dụ trang 19 trong bài giảng)*

Giả sử kẻ thám mã chặn được cặp bản tin tương ứng:
- Bản rõ: **"ATTACK"**
- Bản mã: **"BTGTHM"**
Biết thuật toán sử dụng mã ma trận khối cấp $m = 2$. Đặt ma trận khóa và vector độ dịch cần tìm:
$$K = \begin{pmatrix} a & b \\ c & d \end{pmatrix}, \quad B = \begin{pmatrix} s \\ t \end{pmatrix}$$
Tổng cộng có 6 ẩn số nguyên cần giải: $a, b, c, d, s, t \in \mathbb{Z}_{26}$.

Chia các chuỗi thành từng khối 2 ký tự:
1. Cặp khối 1: $\text{"AT"} \leftrightarrow \text{"BT"}$:
   - $P_1 = \begin{pmatrix} A \\ T \end{pmatrix} = \begin{pmatrix} 0 \\ 19 \end{pmatrix}$, $C_1 = \begin{pmatrix} B \\ T \end{pmatrix} = \begin{pmatrix} 1 \\ 19 \end{pmatrix}$.
   - Thiết lập phương trình $C_1 \equiv K \cdot P_1 + B \pmod{26}$:
     $$\begin{cases} 0 \cdot a + 19 \cdot b + s \equiv 1 \pmod{26} \quad (1) \\ 0 \cdot c + 19 \cdot d + t \equiv 19 \pmod{26} \quad (2) \end{cases}$$
2. Cặp khối 2: $\text{"TA"} \leftrightarrow \text{"GT"}$:
   - $P_2 = \begin{pmatrix} T \\ A \end{pmatrix} = \begin{pmatrix} 19 \\ 0 \end{pmatrix}$, $C_2 = \begin{pmatrix} G \\ T \end{pmatrix} = \begin{pmatrix} 6 \\ 19 \end{pmatrix}$.
   - Thiết lập phương trình:
     $$\begin{cases} 19 \cdot a + 0 \cdot b + s \equiv 6 \pmod{26} \quad (3) \\ 19 \cdot c + 0 \cdot d + t \equiv 19 \pmod{26} \quad (4) \end{cases}$$
3. Cặp khối 3: $\text{"CK"} \leftrightarrow \text{"HM"}$:
   - $P_3 = \begin{pmatrix} C \\ K \end{pmatrix} = \begin{pmatrix} 2 \\ 10 \end{pmatrix}$, $C_3 = \begin{pmatrix} H \\ M \end{pmatrix} = \begin{pmatrix} 7 \\ 12 \end{pmatrix}$.
   - Thiết lập phương trình:
     $$\begin{cases} 2 \cdot a + 10 \cdot b + s \equiv 7 \pmod{26} \quad (5) \\ 2 \cdot c + 10 \cdot d + t \equiv 12 \pmod{26} \quad (6) \end{cases}$$

Giải hệ phương trình tuyến tính 6 phương trình, 6 ẩn số trên modulo 26, ta tìm được kết quả duy nhất:
$$K = \begin{pmatrix} a & b \\ c & d \end{pmatrix} \equiv \begin{pmatrix} 3 & 0 \\ 1 & 1 \end{pmatrix} \pmod{26}, \quad B = \begin{pmatrix} s \\ t \end{pmatrix} \equiv \begin{pmatrix} 1 \\ 0 \end{pmatrix} \pmod{26}$$

> **Đúc kết an ninh**: Mã ma trận hoàn toàn **không an toàn** trước phương pháp tấn công Biết bản rõ (KPA). Kẻ tấn công chỉ cần thu thập được tối thiểu $m^2 + m$ cặp ký hiệu là có thể dễ dàng lập hệ phương trình tuyến tính và giải tìm khóa trong nháy mắt.

---

### 3.3 Hệ mã Hoán vị khối (Block Permutation Cipher)

#### 1. Biểu diễn bằng Ma trận hoán vị & Tính chất $K^{-1} = K^T$
- **Mã khối hoán vị**: Chia thông điệp thành các khối có độ dài cố định $m$. Trong mỗi khối, các ký tự được tráo đổi vị trí cho nhau theo một quy tắc hoán vị xác định.
- **Biểu diễn ma trận**: Có thể xem mã hoán vị là một trường hợp đặc biệt của mã ma trận:
  $$C = K \cdot P \quad (\text{với vector độ dịch } B = O)$$
  Trong đó $K$ là một **Ma trận hoán vị (Permutation Matrix)**: Ma trận vuông chỉ chứa các số 0 và 1, sao cho trên mỗi hàng và mỗi cột có **chính xác một số 1**.
- **Tính chất đặc biệt**: Với mọi ma trận hoán vị, ma trận nghịch đảo chính là **Ma trận chuyển vị (Transpose Matrix)** của nó:
  $$K^{-1} = K^T$$

> **Diễn giải mệnh đề $K^{-1} = K^T$**:
> - Ký hiệu $K^T$ đọc là *"K chuyển vị"*, nghĩa là ma trận thu được bằng cách đổi các hàng của $K$ thành các cột tương ứng.
> - Vì mỗi hàng và mỗi cột của $K$ là một vector đơn vị trực chuẩn, nên tích $K \cdot K^T = I$ (ma trận đơn vị).
> - Điều này có nghĩa: **Để giải mã một hệ mã hoán vị, ta hoàn toàn không cần giải thuật toán đảo ma trận phức tạp, chỉ cần lật ngược các hàng thành cột là xong!**

#### 2. Kỹ thuật Đệm khối (Padding) & Ví dụ minh họa (Trang 21 trong slide)
- Cho kích thước khối $m = 5$.
- Ma trận hoán vị $K$ cấp $5 \times 5$:
  $$K = \begin{pmatrix} 0 & 0 & 1 & 0 & 0 \\ 0 & 0 & 0 & 0 & 1 \\ 0 & 0 & 0 & 1 & 0 \\ 0 & 1 & 0 & 0 & 0 \\ 1 & 0 & 0 & 0 & 0 \end{pmatrix}$$
  Quy tắc hoán vị này tương ứng ánh xạ vector chỉ số:
  $$(p_0, p_1, p_2, p_3, p_4)^T \mapsto (p_2, p_4, p_3, p_1, p_0)^T$$
- Văn bản rõ ban đầu: `"THIS IS NIRVANA"` (13 ký tự, bỏ dấu cách).
- **Kỹ thuật Đệm khối (Padding)**:
  - Chia thành các khối 5 ký tự:
    - Khối 1: `THISI` (đủ 5 ký tự).
    - Khối 2: `SNIRV` (đủ 5 ký tự).
    - Khối 3: `ANA` (chỉ có 3 ký tự, thiếu 2 ký tự).
    - **Quy tắc đệm**: Thêm 2 ký tự giả (thường dùng `XX`) vào cuối để tạo thành khối đủ 5 ký tự: `ANAXX`.
- **Thực hiện hoán vị từng khối**:
  - Khối 1 (`THISI`): $p_0=T, p_1=H, p_2=I, p_3=S, p_4=I \implies (p_2, p_4, p_3, p_1, p_0) = \mathbf{IISHT}$.
  - Khối 2 (`SNIRV`): $p_0=S, p_1=N, p_2=I, p_3=R, p_4=V \implies \mathbf{IVRNS}$.
  - Khối 3 (`ANAXX`): $p_0=A, p_1=N, p_2=A, p_3=X, p_4=X \implies \mathbf{AXXNA}$.
- Bản mã hoàn chỉnh: **`IISHT IVRNS AXXNA`**.

---

## 4. MẬT MÃ BÍ MẬT HIỆN ĐẠI

### 4.1 Mạng Hoán vị – Thay thế (Substitution-Permutation Network - SPN)
Một hệ mã thay thế đơn thuần (như mã tuyến tính, mã ma trận) dễ bị bẻ gãy bằng đại số tuyến tính; một hệ mã hoán vị đơn thuần dễ bị bẻ gãy bằng phân tích thống kê tần suất n-gram.
**Giải pháp hiện đại**: Kết hợp đan xen nhiều tầng **Thay thế (Substitution - S-Box)** và **Hoán vị (Permutation - P-Box)** qua nhiều vòng lặp liên tiếp (*Multiple Rounds*).

```
         Bản rõ P
            |
            v
   +-----------------+
   |  TẦNG THAY THẾ   | <--- Ma trận khóa K (Tạo Hỗn loạn - Confusion)
   +--------+--------+
            |
            v
   +-----------------+
   |  TẦNG HOÁN VỊ   | <--- Ma trận hoán vị T (Tạo Khuếch tán - Diffusion)
   +--------+--------+
            |
            v
   +-----------------+
   |  TẦNG THAY THẾ   | <--- Khóa vòng kế tiếp K' (Tiếp tục xáo trộn)
   +--------+--------+
            |
            v
         Bản mã C
```

#### Ví dụ minh họa trong slide (Trang 24-25)
- Bản rõ: `"SCOOBY DOO WHERE ARE YOU"` (20 ký tự).
- **Giai đoạn 1 (Gom nhóm 2 & Thay thế ma trận $K$)**:
  - Chia thành 10 cặp: `SC OO BY DO OW HE RE AR EY OU`.
  - Dùng ma trận $K = \begin{pmatrix} 5 & 17 \\ 4 & 15 \end{pmatrix}, B = \begin{pmatrix} 5 \\ 2 \end{pmatrix}$ mã hóa ra bản mã trung gian $C'$.
- **Giai đoạn 2 (Gom nhóm 5 & Hoán vị ma trận $T$)**:
  - Gom các phần tử thành các khối độ dài 5 ký tự.
  - Dùng ma trận hoán vị $T$ cấp $5 \times 5$ xáo trộn vị trí trong từng khối, thu được $C''$.
- **Giai đoạn 3 (Gom nhóm 2 & Thay thế ma trận $K$ lần 2)**:
  - Tiếp tục chia đôi và nhân với ma trận $K$ một lần nữa.
  - Kết quả cuối cùng: `CT PK ZH HG HA VK PG YV SE QU`.

*Nhận xét*: Nhờ có bước hoán vị $T$ nằm giữa, một thay đổi nhỏ ở ký tự đầu tiên sau vài vòng sẽ khuếch tán ra toàn bộ chuỗi bản mã, tạo nên hiệu ứng thác đổ mạnh mẽ!

---

### 4.2 Mã hóa dựa trên Tác động nhóm (Group Action Ciphers)
Xét một nhóm toán học $(G, *)$. Theo tiên đề cấu trúc nhóm, mọi phần tử $x \in G$ đều có phần tử nghịch đảo $x^{-1} \in G$.
- **Cơ chế mã hóa theo nhóm**:
  - Khóa bí mật là một phần tử $k \in G$.
  - Mã hóa: $c = m * k$.
  - Giải mã: $m = c * k^{-1}$.
- **Trường hợp nhóm tuần hoàn $\mathbb{Z}_p^*$ (với $p$ là số nguyên tố, $g$ là phần tử sinh)**:
  - Nhóm $\mathbb{Z}_p^* = \{1, 2, \dots, p-1\}$.
  - Khóa mã hóa $k$ được biểu diễn dưới dạng lũy thừa $g^k$.
  - Mã hóa:
    $$c \equiv (m \cdot g^k) \pmod p$$
  - Giải mã:
    $$m \equiv (c \cdot g^{-k}) \pmod p$$
  - *Ý nghĩa toán học*: Phép nhân với $g^k$ đóng vai trò là một phép hoán vị toàn diện trên tập $\mathbb{Z}_p^*$. Ký hiệu $g^{-k} \pmod p$ chính là phần tử nghịch đảo nhân của $g^k$ modulo $p$ (theo định lý Fermat nhỏ, $g^{-k} \equiv g^{p - 1 - k} \pmod p$).

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

#### Công thức toán học của vòng Feistel thứ $i$:
$$\begin{cases} L_i = R_{i-1} \\ R_i = L_{i-1} \oplus f(R_{i-1}, K_i) \end{cases}$$

---

#### 🌟 DIỄN GIẢI CHI TIẾT CÔNG THỨC FEISTEL & PHÉP TOÁN XOR $\oplus$:

1. **Ký hiệu $\oplus$ là gì?**
   - Đây là phép toán **XOR trên từng bit** (*Exclusive OR*), hay phép cộng modulo 2:
     $$0 \oplus 0 = 0, \quad 0 \oplus 1 = 1, \quad 1 \oplus 0 = 1, \quad 1 \oplus 1 = 0$$
   - **Tính chất tự hủy cực kỳ quan trọng**:
     $$A \oplus B \oplus B = A$$
     *(Một giá trị khi bị XOR 2 lần với cùng một số sẽ trở lại chính nó).*

2. **TẠI SAO MẠNG FEISTEL CÓ THỂ GIẢI MÃ ĐƯỢC DÙ HÀM $f$ KHÔNG CẦN KHẢ NGHỊCH?**
   - Đây là phát minh thiên tài của Horst Feistel!
   - Giả sử ở vòng giải mã, bên nhận có trong tay $(L_i, R_i)$.
   - Ta thấy: $R_{i-1}$ được khôi phục ngay lập tức vì $R_{i-1} = L_i$.
   - Còn để khôi phục $L_{i-1}$, bên nhận chỉ cần tính:
     $$R_i \oplus f(L_i, K_i) = \left[ L_{i-1} \oplus f(R_{i-1}, K_i) \right] \oplus f(R_{i-1}, K_i) = L_{i-1} \oplus 0 = L_{i-1}$$
   - **Kết luận**: Cho dù hàm $f$ có phức tạp, phi tuyến hay làm mất mát thông tin (nén bit) đến mức nào, cấu trúc mạng Feistel vẫn tự động giải mã được hoàn hảo.
   - Quá trình giải mã sử dụng **chính xác cùng một phần cứng/mạch logic** với quá trình mã hóa, chỉ cần đưa các khóa vòng theo thứ tự ngược lại: $K_{16}, K_{15}, \dots, K_1$.

---

#### 2. Cấu trúc Toán học của Hộp thay thế (S-Box)
Trong slide (Trang 27), mô hình toán học của S-Box hiện đại (chuẩn AES) được định nghĩa là hàm hợp:
$$S(x) = A \circ P(x)$$

---

#### 🌟 DIỄN GIẢI CHI TIẾT CÔNG THỨC S-BOX $S(x) = A \circ P(x)$:

1. **Ký hiệu $\circ$ là gì?**
   - Ký hiệu $\circ$ biểu diễn **phép hợp thành hai hàm số** (*Function Composition*):
     $$(A \circ P)(x) = A(P(x))$$
   - Nghĩa là: Giá trị đầu vào $x$ trước tiên được xử lý qua hàm $P(x)$, sau đó kết quả thu được sẽ được đưa tiếp vào làm đầu vào cho hàm $A$.

2. **Hàm $P(u)$ là gì?**
   - $P(u)$ là **phép lấy nghịch đảo nhân trong trường hữu hạn Galois** $\text{GF}(2^8)$:
     $$P(u) = \begin{cases} u^{-1} & \text{nếu } u \neq 0 \text{ (khả nghịch trong trường hữu hạn)} \\ 0 & \text{nếu } u = 0 \end{cases}$$
   - Phép nghịch đảo trong trường hữu hạn có đặc tính phi tuyến cao nhất, chống lại các đòn tấn công thám mã vi sai (*Differential Cryptanalysis*).

3. **Hàm $A(u)$ là gì?**
   - $A(u)$ là **phép biến đổi Affine** trên không gian vector 8-bit:
     $$A(u) = M \cdot u \oplus C$$
     (với $M$ là một ma trận nhị phân $8 \times 8$ cố định và $C$ là byte hằng số `0x63`).
   - Phép biến đổi này phá vỡ tính đối xứng đại số của phép nghịch đảo trường hữu hạn.

---

### 4.4 Chuẩn mã hóa dữ liệu DES (Data Encryption Standard)

#### 1. Tổng quan thông số
- **Năm ban hành**: NIST phê chuẩn năm 1977.
- **Kích thước khối dữ liệu**: 64 bit.
- **Kích thước khóa**:
  - Khóa nhập vào: 64 bit.
  - 8 bit kiểm tra tính chẵn lẻ (Parity bits ở vị trí thứ 8, 16, 24, 32, 40, 48, 56, 64).
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
        - *Cơ chế tra S-Box*: Bit 1 và bit 6 ghép lại xác định số hàng (từ 0 đến 3); 4 bit giữa xác định số cột (từ 0 đến 15).
     4. **Hoán vị $P$ (Permutation P-Box)**: 32 bit đầu ra của các S-Box được hoán vị để khuếch tán sang vòng kế tiếp.
4. **Bước 4: Hoán vị kết thúc $IP^{-1}$ (Inverse Initial Permutation)**:
   - Sau vòng 16, hai nửa được ghép ngược lại: $C' = (R_{16}, L_{16})$ (lưu ý đảo vị trí phải-trái).
   - Áp dụng hoán vị nghịch đảo:
     $$C = IP^{-1}(C')$$
   - Cho ra bản mã hoàn chỉnh 64 bit.

---

### 4.5 Chuẩn 3DES (Triple DES)

#### 1. Lý do ra đời
Với không gian khóa chỉ $2^{56} \approx 7.2 \times 10^{16}$, vào năm 1999, cỗ máy *Deep Crack* của EFF đã bẻ khóa thành công một bản mã DES trong **chưa đầy 23 giờ**.
Để tăng cường độ bảo mật mà vẫn tái sử dụng được phần cứng DES sẵn có trong hệ thống ngân hàng, người ta phát triển chuẩn **3DES**.

#### 2. Cấu trúc EDE (Encrypt - Decrypt - Encrypt)
Một chu trình 3DES thực hiện 3 lần liên tiếp thuật toán DES:
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

> **TẠI SAO BƯỚC GIỮA LẠI LÀ DECRYPT (D) MÀ KHÔNG PHẢI ENCRYPT (E)?**
> Đây là một thiết kế tương thích ngược cực kỳ tinh tế!
> Nếu ta chọn 3 khóa giống hệt nhau $K_1 = K_2 = K_3 = K$, thì:
> $$C = E(K, D(K, E(K, M))) = E(K, M)$$
> (Phép Decrypt ở giữa đã triệt tiêu hoàn toàn phép Encrypt đầu tiên!).
> Khi đó hệ thống 3DES sẽ hoạt động **chính xác như DES nguyên bản**, giúp hệ thống tương thích ngay lập tức với các thiết bị đời cũ mà không cần viết lại giải thuật.

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
| **DES** | 1977 | 64 bit | 56 bit | Mạng Feistel 16 vòng | **Đã lỗi thời, không an toàn** (khóa quá ngắn, bị vét cạn) |
| **3DES** | 1998 | 64 bit | 112 hoặc 168 bit | Mạng Feistel ($3 \times 16 = 48$ vòng) | Đang bị loại bỏ (chậm, khối 64-bit dễ bị Sweet32) |
| **AES** | 2001 | 128 bit | 128, 192, 256 bit | Mạng SPN (10, 12, 14 vòng) | **Tiêu chuẩn vàng toàn cầu, an toàn tuyệt đối** |

---

### 5.3 Bảng tra cứu toàn bộ ký hiệu & công thức toán học

| Ký hiệu / Công thức | Tên gọi chuẩn xác | Diễn giải ý nghĩa bằng lời | Ứng dụng cụ thể trong bài |
| :--- | :--- | :--- | :--- |
| **$\gcd(a, b) = 1$** | Greatest Common Divisor | Ước số chung lớn nhất của $a$ và $b$ bằng 1 (nguyên tố cùng nhau). | Điều kiện để $a$ khả nghịch modulo $b$ trong mã Affine, RSA. |
| **$\det(K)$** | Determinant | Định thức của ma trận vuông $K$. Cấp 2: $ad - bc$. | Dùng kiểm tra tính khả nghịch $\gcd(\det(K), n) = 1$ trong mã Hill. |
| **$a \equiv b \pmod n$** | Congruence modulo $n$ | $a$ đồng dư với $b$ modulo $n$ ($(a - b)$ chia hết cho $n$). | Phép toán nền tảng của mật mã học số học. |
| **$k^{-1} \pmod n$** | Modular Multiplicative Inverse | Số nguyên $x$ sao cho $k \cdot x \equiv 1 \pmod n$. | Dùng để giải mã trong mã Affine, Hill, RSA. |
| **$\text{adj}(K)$** | Adjugate Matrix | Ma trận phụ hợp (chuyển vị của ma trận phần bù đại số). | Công thức tính ma trận nghịch đảo: $K^{-1} = (\det)^{-1} \text{adj}(K)$. |
| **$K^T$** | Transpose Matrix | Ma trận chuyển vị (đổi hàng thành cột). | Nghịch đảo của ma trận hoán vị: $K^{-1} = K^T$. |
| **$A \oplus B$** | Bitwise XOR | Phép cộng modulo 2 trên từng bit ($1 \oplus 1 = 0$). | Khóa vòng Feistel trong DES, tính chất tự hủy $A \oplus B \oplus B = A$. |
| **$A \circ P(x)$** | Function Composition | Phép hợp thành hàm: thực hiện $P(x)$ trước rồi lấy kết quả đưa vào $A$. | Cấu trúc toán học của Hộp thay thế S-Box hiện đại. |
| **$\varphi(n)$** | Euler's Totient Function | Số lượng các số nguyên dương $< n$ nguyên tố cùng nhau với $n$. | Đếm không gian khóa nhân trong mã Affine: $|\mathcal{K}| = 12 \times 26$. |
