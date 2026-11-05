# BÀI 4: MÃ HÓA ỨNG DỤNG (APPLIED CRYPTOGRAPHY)
> **Tài liệu tham khảo chuyên sâu & Diễn giải chi tiết toàn bộ kiến thức theo slide bài giảng Môn Mã hóa - Mật mã (Khoa CNTT - ĐH Khoa học Tự nhiên).**

---

## MỤC LỤC TỔNG QUAN

1. [Chữ ký số (Digital Signatures) & Thuật giải DSA/DSS](#1-chữ-ký-số-digital-signatures--thuật-giải-dsadss)
   - [Bản chất & Nguyên tắc hoạt động của Chữ ký số](#11-bản-chất--nguyên-tắc-hoạt-động-của-chữ-ký-số)
   - [Mô hình chữ ký số RSA cơ bản](#12-mô-hình-chữ-ký-số-rsa-cơ-bản)
   - [Chuẩn chữ ký số DSA (Digital Signature Algorithm / Standard)](#13-chuẩn-chữ-ký-số-dsa-digital-signature-algorithm--standard)
     - Các tham số hệ thống
     - Quy trình ký (Signing Process)
     - Quy trình xác minh (Verification Process)
     - Chứng minh tính đúng đắn toán học của DSA
2. [Bảo mật Cơ sở Dữ liệu bằng Định lý Thặng dư Trung Hoa (CRT)](#2-bảo-mật-cơ-sở-dữ-liệu-bằng-định-lý-thặng-dư-trung-hoa-crt)
   - [Đặt bài toán & Ý tưởng phân quyền đọc/ghi](#21-đặt-bài-toán--ý-tưởng-phân-quyền-đọcghi)
   - [Thuật toán mã hóa CSDL tổng quát](#22-thuật-toán-mã-hóa-csdl-tổng-quát)
   - [Thuật toán giải mã & Cơ chế phân quyền](#23-thuật-toán-giải-mã--cơ-chế-phân-quyền)
   - [Ví dụ tính toán từng bước chi tiết (D = {2, 2, 5})](#24-ví-dụ-tính-toán-từng-bước-chi-tiết-d--2-2-5)
3. [Hệ thống Nhiều thành viên: Sơ đồ Chia sẻ Bí mật Ngưỡng (k, n) của Shamir](#3-hệ-thống-nhiều-thành-viên-sơ-đồ-chia-sẻ-bí-mật-ngưỡng-k-n-của-shamir)
   - [Bài toán n nhà khoa học & Khái niệm Ngưỡng (k, n)](#31-bài-toán-n-nhà-khoa-học--khái-niệm-ngưỡng-k-n)
   - [Cơ sở toán học: Đa thức & Nội suy Lagrange](#32-cơ-sở-toán-học-đa-thức--nội-suy-lagrange)
   - [Giao thức thiết lập bí mật riêng phần (Key Distribution)](#33-giao-thức-thiết-lập-bí-mật-riêng-phần-key-distribution)
   - [Giao thức phục hồi bí mật chung (Secret Reconstruction)](#34-giao-thức-phục-hồi-bí-mật-chung-secret-reconstruction)
   - [Các ví dụ minh họa step-by-step theo slide (S = 5, k = 3, n = 5)](#35-các-ví-dụ-minh-họa-step-by-step-theo-slide-s--5-k--3-n--5)
     - Trường hợp 1: Có đúng 3 người (Khôi phục thành công)
     - Trường hợp 2: Chỉ có 2 người (Thất bại - Không đủ ngưỡng)
     - Trường hợp 3: Có 4 người (Khôi phục thành công)
4. [Phụ lục: Công thức & Chứng minh Nội suy Lagrange tổng quát](#4-phụ-lục-công-thức--chứng-minh-nội-suy-lagrange-tổng-quát)
5. [Bảng so sánh tổng hợp & Đúc kết ôn thi](#5-bảng-so-sánh-tổng-hợp--đúc-kết-ôn-thi)

---

## 1. CHỮ KÝ SỐ (DIGITAL SIGNATURES) & THUẬT GIẢI DSA/DSS

### 1.1 Bản chất & Nguyên tắc hoạt động của Chữ ký số
- **Khái niệm**: Chữ ký số (*Digital Signature*) là một chuỗi bit được tạo ra bằng phương pháp mật mã học, gắn liền với một thông điệp số nhằm cung cấp 3 dịch vụ an toàn thông tin cốt lõi:
  1. **Tính xác thực (Authenticity)**: Chứng minh người ký thực sự là chủ sở hữu của khóa cá nhân tương ứng (không thể mạo danh).
  2. **Tính toàn vẹn (Integrity)**: Đảm bảo thông điệp không bị thay đổi, chỉnh sửa dù chỉ 1 bit trên đường truyền.
  3. **Tính chống chối bỏ (Non-repudiation)**: Người gửi một khi đã ký thì không thể phủ nhận việc mình đã gửi tài liệu đó.

```
       Người gửi (Alice)                                 Người nhận (Bob)
 -----------------------------                     -----------------------------
 Thông điệp M                                      Thông điệp M nhận được
   |                                                 |
   v                                                 |
 [Hàm băm H(M)] -> Tiêu bản h                        |
   |                                                 v
   v                                               [Hàm băm H(M)] -> Tiêu bản h'
 [Ký bằng Khóa riêng d]                              |
   |                                                 v
 Chữ ký S                                          [Xác minh bằng Khóa công khai e]
   |                                                 |
   +======> Gửi kèm (M, S) =========================>+ So sánh: Tiêu bản h' == Kết quả giải?
                                                       - ĐÚNG: Chữ ký hợp lệ!
                                                       - SAI: Dữ liệu đã bị sửa đổi!
```

- **Nguyên lý thiết kế**:
  - Trái ngược với mã hóa dữ liệu (người gửi dùng khóa công khai của người nhận để mã hóa, người nhận dùng khóa bí mật của mình để giải mã), **quá trình ký số sử dụng khóa bí mật của người gửi để ký**, và **tất cả mọi người dùng khóa công khai của người gửi để xác minh**.

---

### 1.2 Mô hình chữ ký số RSA cơ bản
Trên nguyên tắc lý thuyết, mọi hệ mã công khai đều có thể được sử dụng để làm chữ ký số:
- **Ký (Signing)**: Alice dùng khóa bí mật d của mình tính:
  ```
  S = RSA(M, d, n) = M^d (mod n)
  ```
- **Xác minh (Verification)**: Bob (hoặc bất kỳ ai) dùng khóa công khai (e, n) của Alice tính:
  ```
  M' = RSA(S, e, n) = S^e (mod n)
  ```
  Sau đó kiểm tra điều kiện:
  ```
  Nếu M' == M: Xác nhận chữ ký hợp lệ và văn bản toàn vẹn.
  Nếu M' ≠ M: Chữ ký giả mạo hoặc văn bản đã bị sửa đổi.
  ```

> **Hạn chế của RSA ký trực tiếp trên thông điệp M**:
> 1. Tốc độ rất chậm nếu thông điệp M có dung lượng lớn (phải chia khối và tính lũy thừa số lớn nhiều lần).
> 2. Kích thước chữ ký quá lớn (bằng đúng kích thước của văn bản).
> 3. Dễ bị tấn công nhân tính đại số (Multiplicative property): Nếu kẻ tấn công có chữ ký của M1 và M2, chúng có thể tạo ra chữ ký hợp lệ của M1 * M2 mà không cần biết khóa bí mật d.
> **Giải pháp chuẩn hóa**: Ký trên **Trị băm (Hash digest / H(M))** thay vì ký trực tiếp trên thông điệp gốc.

---

### 1.3 Chuẩn chữ ký số DSA (Digital Signature Algorithm / Standard)
DSA (Digital Signature Algorithm) được Viện Tiêu chuẩn và Công nghệ Quốc gia Hoa Kỳ (NIST) đề xuất vào năm 1991 và chuẩn hóa trong FIPS 186 (DSS - Digital Signature Standard). Khác với RSA, DSA **chỉ dùng để ký số**, không dùng để mã hóa bí mật dữ liệu.

#### 1. Các tham số hệ thống của DSA
- **p**: Số nguyên tố rất lớn (độ dài từ 512 bit đến 1024-3072 bit trong chuẩn nâng cao).
- **q**: Số nguyên tố 160 bit (là ước số nguyên tố của p - 1, tức (p - 1) chia hết cho q).
- **n**: Đặt n = p * q (theo bài giảng).
- **g**: Phần tử sinh thuộc Z_p^* có bậc là q, tức là:
  ```
  o(g) = q   <=>   g^q ≡ 1 (mod p)
  ```
  *(Cách tạo g: Chọn số h bất kỳ sao cho g = h^((p - 1)/q) mod p > 1).*
- **H**: Hàm băm mật mã chuẩn (ví dụ SHA-1, SHA-256), ánh xạ dữ liệu độ dài tùy ý thành chuỗi nhị phân 160 bit:
  ```
  H: {0, 1}* -> {0, 1}^160
  ```
- **Khóa ký bí mật (Private Key)**:
  ```
  d thuộc Z_q   (với 0 < d < q)
  ```
- **Khóa kiểm tra công khai (Public Key)**:
  ```
  e ≡ g^d (mod p)
  ```

---

#### 2. Quy trình Tạo chữ ký DSA (Signing Process)
Để ký lên thông điệp M bằng khóa riêng d, người ký thực hiện các bước sau:
1. **Bước 1**: Chọn một số nguyên ngẫu nhiên bí mật k sử dụng đúng 1 lần duy nhất (*Ephemeral Key*):
   ```
   0 < k < q
   ```
2. **Bước 2**: Tính thành phần chữ ký thứ nhất r:
   ```
   r ≡ (g^k mod p) (mod q)
   ```
   *(Nếu r = 0, quay lại chọn k khác).*
3. **Bước 3**: Tính thành phần chữ ký thứ hai s:
   ```
   s ≡ k^(-1) * (H(M) + d * r) (mod q)
   ```
   *(Trong đó k^(-1) là nghịch đảo nhân của k modulo q. Nếu s = 0, quay lại chọn k khác).*
4. **Đầu ra**: Cặp số **(r, s)** chính là chữ ký số của Alice trên thông điệp M.

---

#### 3. Quy trình Xác minh chữ ký DSA (Verification Process)
Người nhận nhận được thông điệp M, chữ ký (r, s), và khóa công khai (p, q, g, e) của người gửi:
1. **Bước 1**: Kiểm tra tính hợp lệ cơ bản: 0 < r < q và 0 < s < q.
2. **Bước 2**: Tính nghịch đảo nhân của s theo modulo q:
   ```
   t ≡ s^(-1) (mod q)
   ```
3. **Bước 3**: Kiểm tra điều kiện xác minh:
   ```
   v ≡ ( (g^(H(M) * t) * e^(r * t)) mod p ) (mod q)
   ```
   - **Nếu v == r**: Xác nhận chữ ký **HỢP LỆ** (văn bản nguyên vẹn, đúng do Alice ký).
   - **Nếu v ≠ r**: Chữ ký **KHÔNG HỢP LỆ** (bị từ chối).

---

#### 4. Chứng minh tính đúng đắn toán học của DSA
*(Chứng minh tại sao khi chữ ký hợp lệ thì v luôn luôn bằng r)*

Ta xuất phát từ công thức tính s ở bước ký:
```
s ≡ k^(-1) * (H(M) + d * r) (mod q)
```
Nhân cả hai vế với k:
```
k * s ≡ H(M) + d * r (mod q)
```
Nhân cả hai vế với t = s^(-1) (mod q):
```
k ≡ (H(M) + d * r) * s^(-1) (mod q)
k ≡ (H(M) + d * r) * t (mod q)
k ≡ H(M) * t + d * r * t (mod q)
```
Vì g có bậc q modulo p (tức g^q ≡ 1 mod p), số mũ của g có thể rút gọn theo modulo q:
```
g^k ≡ g^(H(M) * t + d * r * t) (mod p)
    ≡ g^(H(M) * t) * g^(d * r * t) (mod p)
    ≡ g^(H(M) * t) * (g^d)^(r * t) (mod p)
```
Thay khóa công khai e ≡ g^d (mod p) vào:
```
g^k ≡ g^(H(M) * t) * e^(r * t) (mod p)
```
Lấy modulo q cả hai vế:
```
(g^k mod p) (mod q) ≡ ( (g^(H(M) * t) * e^(r * t)) mod p ) (mod q)
```
Theo định nghĩa ở bước ký: r ≡ (g^k mod p) (mod q). Do đó:
```
r ≡ v (mod q)
```
=> **Chứng minh hoàn tất!** ■ (Q.E.D)

---

## 2. BẢO MẬT CƠ SỞ DỮ LIỆU BẰNG ĐỊNH LÝ THẶNG DƯ TRUNG HOA (CRT)

### 2.1 Đặt bài toán & Ý tưởng phân quyền đọc/ghi
- **Bối cảnh thực tế**: Một bản ghi cơ sở dữ liệu (CSDL) gồm nhiều trường thông tin nhạy cảm khác nhau:
  ```
  D = <F1, F2, ..., Fn>
  ```
  *(Ví dụ: F1 = Mã nhân viên, F2 = Họ tên, F3 = Tiền lương, F4 = Bệnh án y tế).*
- **Mục tiêu bảo mật**:
  1. Mã hóa toàn bộ bản ghi D thành **một số nguyên duy nhất C**.
  2. **Phân quyền truy cập chính xác**: Mỗi nhóm người dùng chỉ được phép đọc một hoặc một số trường nhất định.
     - Kế toán chỉ được đọc trường F3 (Tiền lương), không được đọc F4.
     - Bác sĩ chỉ được đọc trường F4 (Bệnh án), không được đọc F3.
  3. Người quản trị có khóa ghi để mã hóa, người dùng được cấp khóa đọc riêng biệt.

---

### 2.2 Thuật toán mã hóa CSDL tổng quát
Sử dụng **Định lý Thặng dư Trung Hoa (Chinese Remainder Theorem - CRT)**:

#### Các bước thực hiện của Người quản trị:
1. **Bước 1**: Chọn n số nguyên tố phân biệt m1, m2, ..., mn sao cho mỗi số nguyên tố lớn hơn giá trị của trường tương ứng:
   ```
   mi > Fi    với mọi i = 1, 2, ..., n
   ```
2. **Bước 2**: Tính tích toàn bộ các số nguyên tố:
   ```
   M = m1 * m2 * ... * mn
   ```
3. **Bước 3**: Với mỗi trường i = 1, 2, ..., n, tính:
   - Modulo thành phần: M_i = M / m_i (là tích của tất cả các số nguyên tố ngoại trừ m_i).
   - Nghịch đảo nhân modulo: (M_i)^(-1) (mod m_i).
   - Hệ số ghi e_i:
     ```
     e_i = M_i * ( (M_i)^(-1) mod m_i )
     ```
4. **Bước 4**: Bản mã C của toàn bộ CSDL là tổ hợp:
   ```
   C ≡ (e1 * F1 + e2 * F2 + ... + en * Fn) (mod M)
   ```
5. **Bước 5**: Phân phối khóa đọc: Cấp khóa m_i cho người dùng có quyền đọc trường F_i.

---

### 2.3 Thuật toán giải mã & Cơ chế phân quyền
- **Cách đọc dữ liệu**: Người dùng sở hữu khóa đọc m_i chỉ cần thực hiện một phép chia lấy dư đơn giản:
  ```
  F_i = C mod m_i
  ```
- **Tại sao công thức này hoạt động?**
  Theo cách xây dựng hệ số ghi:
  - Với j ≠ i: e_j chứa thừa số M_j = M / m_j. Vì M_j chứa m_i nên:
    ```
    e_j ≡ 0 (mod m_i)   (với mọi j ≠ i)
    ```
  - Với j = i: e_i = M_i * (M_i)^(-1) ≡ 1 (mod m_i).
  Do đó khi lấy C modulo m_i:
  ```
  C mod m_i ≡ (0 + ... + 1 * F_i + ... + 0) mod m_i = F_i mod m_i = F_i
  ```
  *(vì m_i > F_i nên F_i mod m_i chính là F_i).*
- **Tính an toàn**: Người nắm khóa m_i hoàn toàn không thể đọc được trường F_j (với j ≠ i) nếu không biết khóa m_j!

---

### 2.4 Ví dụ tính toán từng bước chi tiết (D = {2, 2, 5})
*(Theo đúng ví dụ trang 15 trong slide bài giảng)*

- **Dữ liệu CSDL**: Gồm 3 trường D = {F1, F2, F3} = {2, 2, 5}.

#### Bước 1: Chọn các khóa đọc m_i nguyên tố
- Chọn m1 = 3 (thỏa mãn m1 = 3 > F1 = 2).
- Chọn m2 = 5 (thỏa mãn m2 = 5 > F2 = 2).
- Chọn m3 = 7 (thỏa mãn m3 = 7 > F3 = 5).
*(Cả 3 số 3, 5, 7 đều là các số nguyên tố phân biệt).*

#### Bước 2: Tính M và các M_i
- Modulo chung:
  ```
  M = 3 * 5 * 7 = 105
  ```
- Các modulo thành phần:
  - M1 = M / m1 = 105 / 3 = 35.
  - M2 = M / m2 = 105 / 5 = 21.
  - M3 = M / m3 = 105 / 7 = 15.

#### Bước 3: Tính các nghịch đảo và hệ số ghi e_i
1. **Tính e1**:
   - 35 mod 3 = 2.
   - Tìm nghịch đảo của 2 modulo 3: Vì 2 * 2 = 4 ≡ 1 (mod 3) => 35^(-1) ≡ 2 (mod 3).
   - e1 = M1 * (M1)^(-1) = 35 * 2 = 70.
2. **Tính e2**:
   - 21 mod 5 = 1.
   - Nghịch đảo của 1 modulo 5 là 1 => 21^(-1) ≡ 1 (mod 5).
   - e2 = M2 * (M2)^(-1) = 21 * 1 = 21.
3. **Tính e3**:
   - 15 mod 7 = 1.
   - Nghịch đảo của 1 modulo 7 là 1 => 15^(-1) ≡ 1 (mod 7).
   - e3 = M3 * (M3)^(-1) = 15 * 1 = 15.

#### Bước 4: Mã hóa toàn bộ CSDL ra bản mã C
```
C ≡ (e1 * F1 + e2 * F2 + e3 * F3) (mod M)
C ≡ (70 * 2 + 21 * 2 + 15 * 5) (mod 105)
C ≡ (140 + 42 + 75) (mod 105)
C ≡ 257 (mod 105)
```
Vì 257 = 2 * 105 + 47:
```
=> C = 47
```
Bản mã lưu trữ trong CSDL là số **47**.

#### Bước 5: Giải mã thử nghiệm
- Người có quyền đọc F1 dùng khóa m1 = 3:
  ```
  F1 = 47 mod 3 = 2   (Chính xác!)
  ```
- Người có quyền đọc F2 dùng khóa m2 = 5:
  ```
  F2 = 47 mod 5 = 2   (Chính xác!)
  ```
- Người có quyền đọc F3 dùng khóa m3 = 7:
  ```
  F3 = 47 mod 7 = 5   (Chính xác!)
  ```

---

## 3. HỆ THỐNG NHIỀU THÀNH VIÊN: SƠ ĐỒ CHIA SẺ BÍ MẬT NGƯỠNG (K, N) CỦA SHAMIR

### 3.1 Bài toán n nhà khoa học & Khái niệm Ngưỡng (k, n)
- **Bài toán thực tế**: Một dự án nghiên cứu tối mật có n nhà khoa học. Mật mã phóng tên lửa hoặc mở két sắt bí mật S cần được phân tán sao cho:
  - Nếu có **ít nhất k thành viên** (k <= n) cùng có mặt và hợp tác, họ có thể giải mã và phục hồi lại bí mật S.
  - Nếu có **ít hơn k thành viên** (chỉ có k - 1 người hoặc ít hơn), họ **hoàn toàn không thu được bất kỳ thông tin nào** về bí mật S.
- Sơ đồ này được nhà mật mã học nổi tiếng Adi Shamir phát minh năm 1979, gọi là **Shamir's (k, n) Threshold Scheme**.

```
                           Bí mật S
                              |
              +---------------+---------------+
              |   Tạo đa thức ngẫu nhiên bậc k-1   |
              |   f(x) = S + a1*x + ... + a_(k-1)*x^(k-1)
              +---------------+---------------+
                              |
    +-----------+-----------+---+-----------+-----------+
    |           |           |               |           |
    v           v           v               v           v
  Khóa 1      Khóa 2      Khóa 3          Khóa 4      Khóa 5
 (x1, y1)    (x2, y2)    (x3, y3)        (x4, y4)    (x5, y5)
    |           |           |
    +-----------+-----------+
                |
                v  (Chỉ cần gom đủ >= k = 3 người)
       [Nội suy Lagrange] -> Phục hồi f(0) = S
```

---

### 3.2 Cơ sở toán học: Đa thức & Nội suy Lagrange
- **Định lý cơ bản**:
  > Qua k điểm phân biệt trên mặt phẳng (x1, y1), (x2, y2), ..., (xk, yk) (với các xi đôi một khác nhau), **tồn tại duy nhất một đa thức bậc tối đa k - 1** đi qua tất cả các điểm đó.
- *Ví dụ*:
  - Qua 2 điểm xác định duy nhất 1 đường thẳng (đa thức bậc 1).
  - Qua 3 điểm xác định duy nhất 1 đường parabol (đa thức bậc 2).
  - Do đó, nếu ta giấu bí mật vào hệ số tự do của đa thức bậc k - 1:
    - Biết k điểm: Khôi phục chính xác 100% đa thức và tìm được bí mật.
    - Biết k - 1 điểm: Có vô số đa thức bậc k - 1 đi qua k - 1 điểm đó, mỗi đa thức cho một giá trị bí mật khác nhau => An toàn thông tin tuyệt đối (*Information-theoretically secure*).

---

### 3.3 Giao thức thiết lập bí mật riêng phần (Key Distribution)
Để chia sẻ bí mật S (dưới dạng một số nguyên):
1. **Bước 1**: Chọn một số nguyên tố lớn p sao cho p > S và p > n. Mọi phép tính sau đó được thực hiện trên trường hữu hạn Z_p.
2. **Bước 2**: Chọn ngẫu nhiên k - 1 số nguyên a1, a2, ..., a_(k-1) thuộc Z_p.
3. **Bước 3**: Xây dựng đa thức bậc k - 1:
   ```
   f(x) ≡ S + a1 * x + a2 * x^2 + ... + a_(k-1) * x^(k-1) (mod p)
   ```
   *(Lưu ý: Giá trị tại x = 0 chính là bí mật: f(0) = S).*
4. **Bước 4**: Chọn n giá trị xi phân biệt khác 0 (ví dụ x1 = 1, x2 = 2, ..., xn = n).
   Tính yi = f(xi) mod p.
   Giao cho mỗi thành viên Pi cặp giá trị bí mật riêng phần: **(xi, yi)**.

---

### 3.4 Giao thức phục hồi bí mật chung (Secret Reconstruction)
Khi có K thành viên (với K >= k) hợp tác, họ gom các cặp bí mật {(x1, y1), (x2, y2), ..., (xk, yk)} lại:
Áp dụng **Công thức nội suy Lagrange**:
```
f(x) ≡ Tổng_{i=1 đến k} [ y_i * L_i(x) ] (mod p)
```
Trong đó L_i(x) là đa thức cơ sở Lagrange:
```
L_i(x) = Tích_{j ≠ i} [ (x - x_j) / (x_i - x_j) ] (mod p)
```
Vì mục tiêu duy nhất là tìm lại bí mật S = f(0), ta chỉ cần tính tại x = 0:
```
S = f(0) ≡ Tổng_{i=1 đến k} [ y_i * Tích_{j ≠ i} ( -x_j / (x_i - x_j) ) ] (mod p)
```

---

### 3.5 Các ví dụ minh họa step-by-step theo slide (S = 5, k = 3, n = 5)

#### Thiết lập ban đầu (Trang 21 trong bài giảng):
- Bí mật cần chia sẻ: S = 5.
- Số thành viên: n = 5.
- Ngưỡng cần để phục hồi: k = 3 (cần đa thức bậc k - 1 = 2, tức dạng Parabol).
- Chọn số nguyên tố: p = 11 (xét trên trường Z_11).
- Chọn ngẫu nhiên hệ số: a1 = 2, a2 = 1.
  Đa thức bí mật có dạng:
  ```
  f(x) ≡ 5 + 2*x + x^2 (mod 11)
  ```
- Tính 5 bí mật thành phần cho 5 người:
  - x = 1: f(1) = 5 + 2(1) + 1^2 = 8 mod 11 => Điểm 1: (1, 8).
  - x = 2: f(2) = 5 + 2(2) + 2^2 = 13 ≡ 2 mod 11 => Điểm 2: (2, 2).
  - x = 4: f(4) = 5 + 2(4) + 4^2 = 5 + 8 + 16 = 29 ≡ 7 mod 11 => Điểm 3: (4, 7).
  - x = 7: f(7) = 5 + 2(7) + 7^2 = 5 + 14 + 49 = 68 ≡ 2 mod 11 => Điểm 4: (7, 2).
  - x = 10: f(10) = 5 + 2(10) + 10^2 = 5 + 20 + 100 = 125 ≡ 4 mod 11 => Điểm 5: (10, 4).

---

#### Trường hợp 1: Có đúng 3 người hợp tác (Ví dụ 1 - Slide trang 22)
Giả sử 3 người có các điểm {(1, 8), (4, 7), (7, 2)} cùng nhau mở khóa:
- Các điểm: (x1=1, y1=8), (x2=4, y2=7), (x3=7, y3=2).

Xây dựng công thức nội suy Lagrange tính f(0):
1. **Thành phần thứ nhất (ứng với x1 = 1, y1 = 8)**:
   ```
   L1(0) = ( (0 - 4) * (0 - 7) ) / ( (1 - 4) * (1 - 7) )
         = ( (-4) * (-7) ) / ( (-3) * (-6) )
         = 28 / 18
   ```
   Lấy modulo 11:
   28 mod 11 = 6.
   18 mod 11 = 7. Nghịch đảo của 7 modulo 11: vì 7 * 8 = 56 = 5 * 11 + 1 ≡ 1 => 7^(-1) ≡ 8 (mod 11).
   Do đó: L1(0) = 6 * 8 = 48 ≡ 4 (mod 11).
   Hạng tử 1: y1 * L1(0) = 8 * 4 = 32 ≡ 10 (mod 11).

2. **Thành phần thứ hai (ứng với x2 = 4, y2 = 7)**:
   ```
   L2(0) = ( (0 - 1) * (0 - 7) ) / ( (4 - 1) * (4 - 7) )
         = ( (-1) * (-7) ) / ( 3 * (-3) )
         = 7 / (-9) ≡ 7 / 2 (mod 11)
   ```
   Nghịch đảo của 2 modulo 11: vì 2 * 6 = 12 ≡ 1 => 2^(-1) ≡ 6 (mod 11).
   Do đó: L2(0) = 7 * 6 = 42 ≡ 9 (mod 11).
   Hạng tử 2: y2 * L2(0) = 7 * 9 = 63 ≡ 8 (mod 11).

3. **Thành phần thứ ba (ứng với x3 = 7, y3 = 2)**:
   ```
   L3(0) = ( (0 - 1) * (0 - 4) ) / ( (7 - 1) * (7 - 4) )
         = ( (-1) * (-4) ) / ( 6 * 3 )
         = 4 / 18 ≡ 4 / 7 (mod 11)
   ```
   Nghịch đảo của 7 modulo 11 là 8.
   Do đó: L3(0) = 4 * 8 = 32 ≡ 10 (mod 11).
   Hạng tử 3: y3 * L3(0) = 2 * 10 = 20 ≡ 9 (mod 11).

**Tổng hợp lại để tìm S = f(0)**:
```
S = f(0) ≡ (Hạng tử 1 + Hạng tử 2 + Hạng tử 3) (mod 11)
S ≡ (10 + 8 + 9) = 27 (mod 11)
S ≡ 5 (mod 11)
```
=> **Khôi phục chính xác tuyệt đối bí mật S = 5!**

---

#### Trường hợp 2: Chỉ có 2 người hợp tác (Ví dụ 2 - Slide trang 23)
Giả sử chỉ có 2 người mang điểm {(1, 8), (10, 4)} cố gắng phục hồi bí mật:
- Vì chỉ có 2 điểm, họ chỉ lập được đường thẳng bậc 1 đi qua 2 điểm:
  ```
  f(x) = [ (x - 10) / (1 - 10) ] * 8 + [ (x - 1) / (10 - 1) ] * 4
  ```
- Tính tại x = 0:
  ```
  f(0) = [ (-10) / (-9) ] * 8 + [ (-1) / 9 ] * 4
       = (10 / 9) * 8 + (-4 / 9)
       = (80 - 4) / 9 = 76 / 9
  ```
  Lấy modulo 11:
  76 mod 11 = 10.
  9 mod 11 = 9. Nghịch đảo của 9 modulo 11: vì 9 * 5 = 45 = 4 * 11 + 1 ≡ 1 => 9^(-1) ≡ 5 (mod 11).
  Do đó:
  ```
  f(0) ≡ 10 * 5 = 50 ≡ 6 (mod 11)  (Hoặc ra 3 tùy cách giải xấp xỉ)
  ```
  Dù tính cách nào, kết quả thu được **hoàn toàn khác S = 5**!
=> **Kết luận: Dưới ngưỡng (k < 3), hoàn toàn không thể giải mã được bí mật.**

---

#### Trường hợp 3: Có 4 người hợp tác (Ví dụ 3 - Slide trang 24)
Giả sử có 4 người cung cấp điểm {(1, 8), (4, 7), (7, 2), (10, 4)} (thừa người so với ngưỡng k = 3):
- Ta có thể chọn bất kỳ 3 điểm trong số 4 điểm để phục hồi, hoặc áp dụng công thức nội suy cho cả 4 điểm.
- Kết quả tính toán Lagrange tại x = 0 luôn luôn cho ra:
  ```
  f(0) ≡ 5 (mod 11)
  ```
=> **Bí mật S = 5 được phục hồi chính xác và nhất quán.**

---

## 4. PHỤ LỤC: CÔNG THỨC & CHỨNG MINH NỘI SUY LAGRANGE TỔNG QUÁT
*(Theo phụ lục trang 28-29 trong slide bài giảng)*

Xét bài toán: Tìm đa thức f(x) bậc n đi qua n + 1 điểm phân biệt:
```
{ (x0, y0), (x1, y1), ..., (xn, yn) }
```

Ta giả sử f(x) được biểu diễn dưới dạng tổ hợp tuyến tính:
```
f(x) = A0 * Tích_{i≠0} (x - xi) + A1 * Tích_{i≠1} (x - xi) + ... + An * Tích_{i≠n} (x - xi)
```
- Khi thay x = x0 vào: Mọi hạng tử từ A1 đến An đều có thừa số (x0 - x0) = 0 nên triệt tiêu hết:
  ```
  f(x0) = y0 = A0 * (x0 - x1) * (x0 - x2) * ... * (x0 - xn)
  => A0 = y0 / [ (x0 - x1) * (x0 - x2) * ... * (x0 - xn) ]
  ```
- Tương tự, khi thay x = x1 vào:
  ```
  f(x1) = y1 = A1 * (x1 - x0) * (x1 - x2) * ... * (x1 - xn)
  => A1 = y1 / [ (x1 - x0) * (x1 - x2) * ... * (x1 - xn) ]
  ```
- Tổng quát cho chỉ số i bất kỳ (i = 0, 1, ..., n):
  ```
  Ai = yi / Tích_{j ≠ i} (xi - xj)
  ```

Đặt Li(x) = Tích_{j ≠ i} (x - xj), ta có công thức nội suy Lagrange hoàn chỉnh:
```
f(x) = Tổng_{i=0 đến n} [ yi * Tích_{j ≠ i} ( (x - xj) / (xi - xj) ) ]
```

---

## 5. BẢNG SO SÁNH TỔNG HỢP & ĐÚC KẾT ÔN THI

### Bảng tóm tắt các ứng dụng mật mã trong Bài 4

| Ứng dụng | Mục tiêu bảo mật chính | Cơ sở toán học nền tảng | Đầu vào / Tham số chính | Kết quả đầu ra |
| :--- | :--- | :--- | :--- | :--- |
| **Chữ ký số DSA** | Toàn vẹn dữ liệu, Xác thực người gửi, Chống chối bỏ | Bài toán Logarit rời rạc (DLP) trên nhóm con bậc q | Khóa bí mật d, Khóa công khai e = g^d mod p, Thông điệp M | Cặp chữ ký (r, s) |
| **Bảo mật CSDL bằng CRT** | Phân quyền truy cập theo từng trường dữ liệu | Định lý Thặng dư Trung Hoa (CRT) | Các trường F1..Fn, Khóa đọc nguyên tố m1..mn | Bản mã duy nhất C; Giải mã: Fi = C mod mi |
| **Chia sẻ Bí mật Shamir (k, n)** | Bảo vệ bí mật trọng yếu, chống phản bội / mất mát khóa | Đa thức bậc k - 1 & Nội suy Lagrange | Bí mật S, số người n, ngưỡng tối thiểu k | n mảnh bí mật (xi, yi); Phục hồi: f(0) = S |

---

### Tóm tắt các công thức then chốt cần ghi nhớ khi làm bài thi

1. **Chữ ký số DSA**:
   - Ký:
     ```
     r ≡ (g^k mod p) (mod q)
     s ≡ k^(-1) * (H(M) + d * r) (mod q)
     ```
   - Xác minh:
     ```
     t ≡ s^(-1) (mod q)
     Kiểm tra: r == ( (g^(H(M)*t) * e^(r*t)) mod p ) (mod q)
     ```

2. **Mã hóa CSDL (CRT)**:
   - Điều kiện: m_i > F_i với mọi i.
   - M = m1 * m2 * ... * mn; M_i = M / m_i.
   - Hệ số ghi: e_i = M_i * (M_i^(-1) mod m_i).
   - Bản mã:
     ```
     C ≡ Tổng [ e_i * F_i ] (mod M)
     ```
   - Đọc dữ liệu:
     ```
     F_i = C mod m_i
     ```

3. **Ngưỡng Shamir (k, n)**:
   - Đa thức bí mật bậc k - 1:
     ```
     f(x) ≡ S + a1 * x + a2 * x^2 + ... + a_(k-1) * x^(k-1) (mod p)
     ```
   - Phục hồi bí mật dùng k điểm:
     ```
     S = f(0) ≡ Tổng_{i=1 đến k} [ y_i * Tích_{j ≠ i} ( -x_j / (x_i - x_j) ) ] (mod p)
     ```
