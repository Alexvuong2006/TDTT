# BÀI 2: MÃ HÓA KHÓA CÔNG KHAI (PUBLIC-KEY CRYPTOGRAPHY)
> **Tài liệu tham khảo chuyên sâu & Diễn giải chi tiết toàn bộ công thức, mệnh đề toán học theo slide bài giảng Môn Mã hóa - Mật mã (Khoa CNTT - ĐH Khoa học Tự nhiên).**

---

## MỤC LỤC TỔNG QUAN

1. [Tổng quan & Nguyên lý thiết kế Hệ mã Công khai](#1-tổng-quan--nguyên-lý-thiết-kế-hệ-mã-công-khai)
   - [Sự chuyển dịch từ mã đối xứng sang mã công khai](#11-sự-chuyển-dịch-từ-mã-đối-xứng-sang-mã-công-khai)
   - [Hàm một chiều có cửa mật (Trapdoor One-Way Function)](#12-hàm-một-chiều-có-cửa-mật-trapdoor-one-way-function)
   - [Các bài toán khó kinh điển trong Mật mã học](#13-các-bài-toán-khó-kinh-điển-trong-mật-mã-học)
   - [Lược đồ tổng quát thiết kế hệ mã (General Scheme - GS)](#14-lược-đồ-tổng-quát-thiết-kế-hệ-mã-general-scheme---gs)
2. [Hệ mã công khai RSA (Rivest – Shamir – Adleman)](#2-hệ-mã-công-khai-rsa-rivest--shamir--adleman)
   - [Định lý RSA & Giao thức hoàn chỉnh](#21-định-lý-rsa--giao-thức-hoàn-chỉnh)
   - [Độ an toàn & Tấn công toàn phần (Full Attack)](#22-độ-an-toàn--tấn-công-toàn-phần-full-attack)
   - [Cài đặt tính toán số lớn (BigInteger Implementation)](#23-cài-đặt-tính-toán-số-lớn-biginteger-implementation)
   - [Thuật toán sinh số nguyên tố lớn & Kiểm tra Miller-Rabin](#24-thuật-toán-sinh-số-nguyên-tố-lớn--kiểm-tra-miller-rabin)
   - [Chứng minh Định lý RSA (Dùng CRT & Fermat nhỏ)](#25-chứng-minh-định-lý-rsa-dùng-crt--fermat-nhỏ)
   - [Kỹ thuật giải mã nhanh RSA (RSA Fast Decryption with CRT)](#26-kỹ-thuật-giải-mã-nhanh-rsa-rsa-fast-decryption-with-crt)
3. [Giao thức Trao đổi Khóa Diffie – Hellman](#3-giao-thức-trao-đổi-khóa-diffie--hellman)
   - [Mục tiêu và Quy trình giao thức](#31-mục-tiêu-và-quy-trình-giao-thức)
   - [Cơ sở toán học: Cấu trúc Nhóm (Group) & Nhóm tuần hoàn (Cyclic Group)](#32-cơ-sở-toán-học-cấu-trúc-nhóm-group--nhóm-tuần-hoàn-cyclic-group)
   - [Thuật toán tìm phần tử sinh (Generator)](#33-thuật-toán-tìm-phần-tử-sinh-generator)
   - [Phân tích an toàn: Bài toán Logarit rời rạc (DLP)](#34-phân-tích-an-toàn-bài-toán-logarit-rời-rạc-dlp)
   - [Tấn công DLP bằng thuật toán Index-Calculus (Có ví dụ từng bước chi tiết)](#35-tấn-công-dlp-bằng-thuật-toán-index-calculus-có-ví-dụ-từng-bước-chi-tiết)
4. [Hệ mã công khai ElGamal](#4-hệ-mã-công-khai-elgamal)
   - [Ý tưởng và Mục tiêu](#41-ý-tưởng-và-mục-tiêu)
   - [Giao thức ElGamal: Sinh khóa, Mã hóa, Giải mã](#42-giao-thức-elgamal-sinh-khóa-mã-hóa-giải-mã)
   - [Ví dụ minh họa step-by-step & Bài tập tính toán](#43-ví-dụ-minh-họa-step-by-step--bài-tập-tính-toán)
5. [Lỗ hổng kinh điển: Tấn công Người đứng giữa (Man-in-the-Middle - MITM) & Giải pháp](#5-lỗ-hổng-kinh-điển-tấn-công-người-đứng-giữa-man-in-the-middle---mitm--giải-pháp)
6. [Bảng so sánh tổng hợp & Đúc kết ôn thi](#6-bảng-so-sánh-tổng-hợp--đúc-kết-ôn-thi)

---

## 1. TỔNG QUAN & NGUYÊN LÝ THIẾT KẾ HỆ MÃ CÔNG KHAI

### 1.1 Sự chuyển dịch từ mã đối xứng sang mã công khai
- **Mật mã đối xứng (Symmetric Cryptography)**: Hai bên liên lạc (Alice & Bob) dùng chung **một khóa bí mật duy nhất K** cho cả hai quá trình mã hóa E_K(M) và giải mã D_K(C).
  - *Hạn chế chí mạng*: Bài toán phân phối khóa (Key Distribution Problem). Làm thế nào để hai bên chưa từng gặp nhau có thể thống nhất một khóa bí mật an toàn qua một kênh truyền công khai bị nghe lén? Hơn nữa, nếu có N người dùng trong mạng, số lượng khóa cần quản lý là N(N-1)/2 = O(N^2) — quá lớn khi mạng mở rộng.
- **Mật mã bất đối xứng / Khóa công khai (Asymmetric / Public-Key Cryptography)**:
  - Mỗi thực thể sở hữu một **cặp khóa (Key pair)** có liên hệ toán học mật thiết:
    - **Khóa công khai (e - Public Key)**: Được công bố rộng rãi cho toàn thế giới biết, ai cũng có thể dùng để mã hóa thông điệp gửi cho người đó.
    - **Khóa bí mật (d - Private Key)**: Được giữ bí mật tuyệt đối, chỉ người nhận mới sở hữu để giải mã thông điệp.
  - *Mục tiêu tối thượng*: Cho dù kẻ tấn công biết rõ thuật toán, khóa công khai e, và bản mã c, kẻ đó **vẫn không thể suy ngược ra khóa bí mật d hay thông điệp gốc m trong thời gian đa thức**.

---

### 1.2 Hàm một chiều có cửa mật (Trapdoor One-Way Function)
Đây là "trái tim" của mọi hệ mã hóa khóa công khai.

Một hàm số f: D -> R được gọi là **Hàm một chiều có cửa mật** nếu thỏa mãn 3 điều kiện:
1. **Chiều thuận dễ tính (Easy forward)**: Cho trước x thuộc D, việc tính y = f(x) có độ phức tạp tính toán thấp (chạy trong thời gian đa thức O(n^k)).
2. **Chiều nghịch cực khó tính (Hard backward without trapdoor)**: Cho trước y thuộc R, việc tìm lại x = f^(-1)(y) là bất khả thi về mặt tính toán (độ phức tạp siêu đa thức hoặc hàm mũ O(2^n), đòi hỏi hàng ngàn năm tính toán của siêu máy tính).
3. **Chiều nghịch dễ tính nếu có "cửa mật" (Easy backward with trapdoor)**: Nếu được cung cấp thêm một thông tin phụ bí mật K (gọi là *Trapdoor* hay cửa mật), ta có thể tính ngược x = f^(-1)_K(y) một cách dễ dàng và nhanh chóng.

```
                      [ Dễ tính: y = f(x) ]
         x -----------------------------------------> y
         |                                            |
         |                                            |
[ Trapdoor K ]                                [ Không có Trapdoor ]
         |                                            |
         <--------------------------------------------+
                    [ Khó tính: f^-1(y) = ??? ]
                    [ Dễ tính nếu có Trapdoor K ]
```

- **Ứng dụng vào hệ mã**:
  - Khóa công khai e chính là thông số để thực hiện hàm f(x).
  - Khóa cá nhân d chính là thông tin cửa mật (Trapdoor) giúp đảo ngược hàm f.

---

### 1.3 Các bài toán khó kinh điển trong Mật mã học
Độ an toàn của các thuật toán mật mã không dựa trên sự bí mật của giải thuật, mà dựa vào độ khó nội tại của các bài toán toán học chưa có lời giải hiệu quả:

#### 1. Bài toán phân tích ra thừa số nguyên tố (Integer Factorization Problem - IFP)
- **Định lý cơ bản của số học (Fundamental Theorem of Arithmetic)**:
  Mọi số nguyên dương n thuộc N+ \ {0, 1} đều có thể biểu diễn một cách duy nhất (không kể thứ tự các thừa số) dưới dạng tích các lũy thừa của số nguyên tố:
  ```
  n = (p1^e1) * (p2^e2) * ... * (pk^ek)
  ```
- **Tính một chiều**:
  - Cho hai số nguyên tố rất lớn p, q (ví dụ mỗi số dài 1024 hoặc 2048 bit). Việc nhân n = p * q diễn ra trong vài phần triệu giây.
  - Nhưng cho trước số n (độ dài 2048 hoặc 4096 bit), việc tìm lại hai thừa số nguyên tố p và q là một thách thức cực kỳ lớn đối với các siêu máy tính hiện đại (bài toán IFP).
  - Ánh xạ (p, q) -> n = p * q là hàm một chiều, và thông tin p hoặc q chính là cửa mật.
  - *Ứng dụng tiêu biểu*: **RSA**.

#### 2. Bài toán Logarit rời rạc (Discrete Logarithm Problem - DLP)
- Xét trên một nhóm cyclic hữu hạn (ví dụ nhóm nhân modulo số nguyên tố lớn Z_p^*, với phần tử sinh g):
  ```
  y ≡ g^x (mod p)
  ```
- **Tính một chiều**:
  - Cho p, g và số nguyên x, việc tính y ≡ g^x (mod p) cực kỳ nhanh thông qua thuật toán lũy thừa nhanh bình phương và nhân (Square-and-Multiply) với độ phức tạp O(log x).
  - Nhưng khi cho trước p, g và giá trị y, bài toán tìm lại số mũ x = log_g(y) (mod p - 1) trên tập số nguyên rời rạc lớn được công nhận là bài toán khó. Hiện chưa có thuật toán đa thức cổ điển nào giải được tổng quát.
  - Ánh xạ (g, p, x) -> g^x (mod p) là hàm một chiều, với x là cửa mật bí mật.
  - *Ứng dụng tiêu biểu*: **Diffie-Hellman**, **ElGamal**, **DSA**.

#### 3. Các bài toán khó khác
- **Bài toán Tổng con (Subset Sum Problem - SSP / Knapsack)**: Ứng dụng trong hệ mã Merkle-Hellman.
- **Bài toán Phân tích Ma trận (Matrix Factorization Problem - MFP)**.
- *Lưu ý*: Cho đến nay, **IFP** và **DLP** vẫn là 2 bài toán nền tảng cốt lõi được ứng dụng rộng rãi và kiểm nghiệm thực tế vững chắc nhất trong mật mã hiện đại.

---

### 1.4 Lược đồ tổng quát thiết kế hệ mã (General Scheme - GS)
Để thiết kế một hệ mã công khai đạt chuẩn, quy trình gồm 3 bước:
1. **Bước 1**: Chọn hoặc xây dựng một bài toán khó toán học P (như IFP hoặc DLP).
2. **Bước 2**: Thiết kế một hàm một chiều với cửa mật f.
3. **Bước 3**: Thiết kế hàm mã hóa và giải mã:
   - Các thông tin công bố được của hàm f sẽ tạo thành **Khóa công khai (Public Key)**.
   - Thông tin cửa mật sẽ được giữ làm **Khóa cá nhân (Private Key)**.

---

## 2. HỆ MÃ CÔNG KHAI RSA (RIVEST – SHAMIR – ADLEMAN)

Hệ mã RSA ra đời năm 1977 bởi Ron Rivest, Adi Shamir và Leonard Adleman tại MIT, là hệ mã hóa khóa công khai nổi tiếng và được sử dụng rộng rãi nhất trên thế giới.

```
       Alice (Tạo khóa)                                  Bob (Người gửi)
 -----------------------------                     -----------------------------
 Sinh 2 số nguyên tố p, q
 n = p * q
 phi(n) = (p - 1)(q - 1)
 Chọn e: gcd(e, phi(n)) = 1
 Tính d = e^(-1) mod phi(n)
 Public Key: (e, n)  ============================> Nhận (e, n)
 Private Key: d                                    Thông điệp m < n
                                                   Mã hóa: c = m^e mod n
 Nhận bản mã c       <============================ Gửi bản mã c
 Giải mã: m = c^d mod n
```

### 2.1 Định lý RSA & Giao thức hoàn chỉnh

#### Định lý RSA
> Cho p và q là 2 số nguyên tố phân biệt (p ≠ q).
> Đặt n = p * q, và hàm số Euler phi(n) = (p - 1)(q - 1).
> Chọn hai số nguyên e và d thỏa mãn điều kiện đồng dư:
> ```
> e * d ≡ 1 (mod phi(n))
> ```
> Với mọi thông điệp m thuộc Z_n = {0, 1, ..., n-1}, nếu tính bản mã:
> ```
> c ≡ m^e (mod n)
> ```
> Thì bản rõ m được phục hồi hoàn hảo bằng phép tính:
> ```
> m ≡ c^d (mod n)
> ```

#### Chi tiết Giao thức RSA

##### Giai đoạn I: Sinh khóa – KeyGen(lambda)
1. **Chọn hai số nguyên tố ngẫu nhiên** độc lập p và q, mỗi số có độ dài khoảng lambda / 2 bit (p ≠ q).
2. **Tính modulo RSA**: n = p * q. (Độ dài của n là lambda bit, ví dụ 2048 bit).
3. **Tính hàm phi Euler**: phi(n) = (p - 1)(q - 1).
4. **Chọn số mũ công khai e**: Sao cho 1 < e < phi(n) và nguyên tố cùng nhau với phi(n):
   ```
   gcd(e, phi(n)) = 1
   ```
   *(Trong thực tế, người ta thường chọn e = 65537 = 2^16 + 1 vì là số Fermat nguyên tố, biểu diễn nhị phân chỉ có 2 bit 1 giúp việc tính toán cực nhanh).*
5. **Tính số mũ bí mật d**: Là phần tử nghịch đảo nhân modulo của e theo modulo phi(n):
   ```
   d ≡ e^(-1) (mod phi(n))   <=>   e * d ≡ 1 (mod phi(n))
   ```
   *(Tính bằng Thuật toán Euclid mở rộng).*
6. **Xuất kết quả**:
   - **Khóa công khai (Public Key)**: PK = (e, n) (công bố rộng rãi).
   - **Khóa cá nhân (Private Key)**: SK = (d, n) hoặc (d, p, q) (giữ bí mật tuyệt đối).

##### Giai đoạn II: Mã hóa – Encryption(e, n, m)
- Bob muốn gửi thông điệp m cho Alice (0 <= m < n):
- Sử dụng khóa công khai (e, n) của Alice, Bob tính:
  ```
  c = m^e (mod n)
  ```
- Bob gửi bản mã c cho Alice.

##### Giai đoạn III: Giải mã – Decryption(d, n, c)
- Alice nhận được bản mã c:
- Sử dụng khóa cá nhân d của mình, Alice tính:
  ```
  m = c^d (mod n)
  ```
- Alice khôi phục được thông điệp gốc m.

---

### 2.2 Độ an toàn & Tấn công toàn phần (Full Attack)
- **Tấn công toàn phần (Full Attack)**: Kẻ tấn công (Eve) có trong tay khóa công khai (e, n) và muốn tìm ra khóa bí mật d.
- Theo định nghĩa:
  ```
  e * d ≡ 1 (mod phi(n))
  ```
  Để tìm được d, Eve bắt buộc phải tính được:
  ```
  phi(n) = (p - 1)(q - 1) = p*q - (p + q) + 1 = n - (p + q) + 1
  ```
- Nhưng để biết được tổng (p + q), Eve phải biết được riêng lẻ từng số nguyên tố p và q.
- Điều này tương đương với việc **phải giải bài toán phân tích thừa số nguyên tố (IFP)** của số lớn n = p * q.
- Khi n có kích thước từ 2048 đến 4096 bit, các thuật toán phân tích thừa số tốt nhất hiện nay (như GNFS) đòi hỏi thời gian tính toán vượt xa tuổi thọ vũ trụ. Do đó, RSA an toàn trước tấn công toàn phần nếu độ dài khóa đủ lớn.

---

### 2.3 Cài đặt tính toán số lớn (BigInteger Implementation)
Vì RSA làm việc với các số nguyên hàng trăm đến hàng ngàn chữ số, ta bắt buộc phải cài đặt các cấu trúc và giải thuật số lớn:

#### 1. Phép cộng modulo: addMod(a, b, n)
```
c ≡ (a + b) (mod n) =
   a + b        (nếu a + b < n)
   a + b - n    (nếu a + b >= n)
```
*(Cách này giúp tránh phép chia lấy dư % n vốn tốn nhiều chu kỳ máy).*

#### 2. Phép nhân modulo: mulMod(x, y, n)
Biểu diễn y dưới dạng nhị phân b bit: y = y_(b-1) ... y_1 y_0.
Nhận xét: x * 2^(i+1) ≡ 2 * (x * 2^i) (mod n).

```python
def mulMod(x, y, n):
    P = 0
    # Xét từng bit của y từ thấp đến cao (LSB sang MSB)
    for i in range(b):
        if (y >> i) & 1:
            P = (P + x) % n
        x = (x * 2) % n  # Nhân đôi sau mỗi bước
    return P
```

#### 3. Phép lũy thừa modulo: powerMod(x, a, n) (Square-and-Multiply)
Để tính x^a (mod n) với số mũ a hàng ngàn bit:

**Cách 1: Quét từ bit thấp nhất đến cao nhất (LSB -> MSB)**
```python
def powerMod_LSB(x, a, n):
    y = 1
    if a == 0:
        return y
    A = x
    for i in range(b):
        if (a >> i) & 1:
            y = (y * A) % n
        A = (A * A) % n  # Bình phương cơ số
    return y
```

**Cách 2: Quét từ bit cao nhất đến thấp nhất (MSB -> LSB)**
```python
def powerMod_MSB(x, a, n):
    y = 1
    # Quét từ bit b - 1 về 0
    for i in range(b - 1, -1, -1):
        y = (y * y) % n  # Luôn bình phương kết quả trung gian
        if (a >> i) & 1:
            y = (y * x) % n  # Nhân thêm x nếu bit hiện tại là 1
    return y
```
*Độ phức tạp*: Chỉ cần tối đa 2b phép nhân modulo, thay vì 2^b phép tính nếu nhân tuần tự!

#### 4. Thuật toán Euclid và Euclid nhị phân (Binary GCD)
Tìm ước chung lớn nhất gcd(x, y) không cần phép chia dư:
- **Nguyên lý nhị phân**:
  - Nếu cả x, y đều chẵn: gcd(x, y) = 2 * gcd(x/2, y/2).
  - Nếu x chẵn, y lẻ: gcd(x, y) = gcd(x/2, y).
  - Nếu x lẻ, y chẵn: gcd(x, y) = gcd(x, y/2).
  - Nếu cả x, y đều lẻ: gcd(x, y) = gcd(|x - y|/2, min(x, y)).

```python
def binary_gcd(x, y):
    g = 1
    while (x % 2 == 0) and (y % 2 == 0):
        x //= 2
        y //= 2
        g *= 2
    while x > 0:
        while x % 2 == 0:
            x //= 2
        while y % 2 == 0:
            y //= 2
        t = abs(x - y) // 2
        if x >= y:
            x = t
        else:
            y = t
    return g * y
```

#### 5. Định lý Bézout & Euclid mở rộng (Extended Euclidean Algorithm)
- **Định lý Bézout**: Với hai số nguyên dương a, b, luôn tồn tại các số nguyên x, y thuộc Z sao cho:
  ```
  a * x + b * y = gcd(a, b)
  ```
- Áp dụng tìm nghịch đảo modulo:
  Khi gcd(e, phi) = 1, ta có:
  ```
  e * d + phi * y = 1  =>  e * d ≡ 1 (mod phi)  =>  d ≡ e^(-1) (mod phi)
  ```

```python
def extended_gcd(a, b):
    if b == 0:
        return a, 1, 0
    gcd, x1, y1 = extended_gcd(b, a % b)
    x = y1
    y = x1 - (a // b) * y1
    return gcd, x, y

def mod_inverse(e, phi):
    gcd, x, y = extended_gcd(e, phi)
    if gcd != 1:
        raise ValueError("Không tồn tại nghịch đảo modulo!")
    return (x % phi + phi) % phi
```

---

### 2.4 Thuật toán sinh số nguyên tố lớn & Kiểm tra Miller-Rabin

#### 1. Định lý Fermat nhỏ (Fermat's Little Theorem)
Nếu p là số nguyên tố thì với mọi số nguyên cơ sở b không chia hết cho p:
```
b^(p-1) ≡ 1 (mod p)
```

#### 2. Số giả nguyên tố & Số giả nguyên tố mạnh (Miller-Rabin)
- Nếu p là số nguyên tố lẻ lớn hơn 2, ta có thể viết:
  ```
  p - 1 = (2^r) * m   (với m là số lẻ)
  ```
- Xét dãy bình phương liên tiếp từ b^m (mod p):
  ```
  b^m,  b^(2m),  b^(4m),  ...,  b^((2^r)*m) ≡ b^(p-1) (mod p)
  ```
- Nếu p là số nguyên tố, thì:
  - Hoặc b^m ≡ 1 (mod p) hoặc b^m ≡ -1 (mod p).
  - Hoặc tồn tại một số k thuộc {0, 1, ..., r-1} sao cho b^((2^k)*m) ≡ -1 (mod p).
- Thuật toán kiểm tra Miller-Rabin lặp lại với t cơ sở b ngẫu nhiên. Xác suất sai số nhỏ hơn (1/4)^t. Với t = 50, xác suất sai số là 2^(-100).

```python
def is_prime_miller_rabin(p, iterations=40):
    if p < 2: return False
    if p in (2, 3): return True
    if p % 2 == 0: return False
    
    r = 0
    m = p - 1
    while m % 2 == 0:
        r += 1
        m //= 2
        
    import random
    for _ in range(iterations):
        b = random.randint(2, p - 2)
        z = pow(b, m, p)
        if z == 1 or z == p - 1:
            continue
        composite = True
        for _ in range(r - 1):
            z = pow(z, 2, p)
            if z == p - 1:
                composite = False
                break
        if composite:
            return False
    return True
```

---

### 2.5 Chứng minh Định lý RSA (Dùng CRT & Fermat nhỏ)
Mục tiêu là chứng minh rằng với e * d ≡ 1 (mod phi(n)) và c ≡ m^e (mod n), ta luôn có:
```
c^d ≡ (m^e)^d ≡ m^(ed) ≡ m (mod n)
```

**Chứng minh chi tiết:**
Vì e * d ≡ 1 (mod phi(n)), tồn tại số nguyên k sao cho:
```
ed = k * phi(n) + 1 = k*(p - 1)*(q - 1) + 1
```
Do đó:
```
m^(ed) = m^(k*(p-1)*(q-1) + 1) = m * (m^(p-1))^(k*(q-1))
```

1. **Xét modulo p**:
   - Nếu gcd(m, p) = 1, theo Fermat nhỏ m^(p-1) ≡ 1 (mod p):
     ```
     m^(ed) ≡ m * (1)^(k*(q-1)) ≡ m (mod p)
     ```
   - Nếu p chia hết m, tức m ≡ 0 (mod p):
     ```
     m^(ed) ≡ 0^(ed) ≡ 0 ≡ m (mod p)
     ```
   => Trong mọi trường hợp, luôn có: m^(ed) ≡ m (mod p).

2. **Xét modulo q**: Hoàn toàn tương tự:
   ```
   m^(ed) ≡ m (mod q)
   ```

3. **Kết hợp bằng Định lý Thặng dư Trung Hoa (CRT)**:
   Hệ phương trình:
   ```
   m^(ed) ≡ m (mod p)
   m^(ed) ≡ m (mod q)
   ```
   Vì p, q là hai số nguyên tố phân biệt (gcd(p, q) = 1), theo CRT hệ có nghiệm duy nhất modulo n = p * q:
   ```
   m^(ed) ≡ m (mod p*q)   <=>   m^(ed) ≡ m (mod n)
   ```
   *(Chứng minh hoàn tất).* ■ (Q.E.D)

---

### 2.6 Kỹ thuật giải mã nhanh RSA (RSA Fast Decryption with CRT)
Người sở hữu khóa riêng biết rõ p và q. Kỹ thuật **RSA-CRT** giúp tăng tốc giải mã gấp ~4 lần:
1. **Tiền tính toán các số mũ rút gọn**:
   ```
   d1 = d mod (p - 1)
   d2 = d mod (q - 1)
   ```
2. **Lũy thừa trên modulo nhỏ**:
   ```
   a1 = c^d1 (mod p)
   a2 = c^d2 (mod q)
   ```
3. **Kết hợp CRT (Công thức Garner)**:
   ```
   h = (a1 - a2) * (q^(-1) mod p) mod p
   m = a2 + h * q
   ```

```python
def rsa_fast_decryption(c, d, p, q):
    d1 = d % (p - 1)
    d2 = d % (q - 1)
    a1 = pow(c, d1, p)
    a2 = pow(c, d2, q)
    q_inv = pow(q, -1, p)
    h = ((a1 - a2) * q_inv) % p
    m = a2 + h * q
    return m
```

---

## 3. GIAO THỨC TRAO ĐỔI KHÓA DIFFIE – HELLMAN

### 3.1 Mục tiêu và Quy trình giao thức
Alice và Bob muốn cùng sở hữu một khóa bí mật K để mã hóa đối xứng qua kênh công khai.

```
       Alice                                                    Bob
 -----------------------------                     -----------------------------
 Chọn khóa riêng: x thuộc Zp                       Chọn khóa riêng: y thuộc Zp
 Tính khóa công khai:                              Tính khóa công khai:
   kA = g^x mod p                                    kB = g^y mod p
                    ----------- kA ----------->
                    <---------- kB ------------
 Tính khóa chung:                                  Tính khóa chung:
   K = (kB)^x mod p                                  K' = (kA)^y mod p
   K = (g^y)^x = g^(xy) mod p                        K' = (g^x)^y = g^(xy) mod p
                          ====> K == K' <====
```

---

### 3.2 Cơ sở toán học: Cấu trúc Nhóm (Group) & Nhóm tuần hoàn (Cyclic Group)
1. **Cấu trúc Nhóm (G, *)**: Thỏa mãn 4 tiên đề: Tính đóng, Phần tử đơn vị, Phần tử nghịch đảo, Tính kết hợp.
2. **Nhóm nhân Z_p^* = {1, 2, ..., p - 1}**: Có bậc p - 1 với p là số nguyên tố.
3. **Phần tử sinh (Generator g)**: Phần tử có bậc o(g) = p - 1, sinh ra toàn bộ nhóm Z_p^*.

---

### 3.3 Thuật toán tìm phần tử sinh (Generator)
Giả sử p - 1 có các ước số nguyên tố {p1, p2, ..., pn}. Một số g là phần tử sinh khi và chỉ khi:
```
g^((p - 1) / pi) ≠ 1 (mod p)    với mọi i = 1, 2, ..., n
```

```python
def find_generator(p, prime_factors_of_p_minus_1):
    import random
    while True:
        g = random.randint(2, p - 2)
        is_gen = True
        for pi in prime_factors_of_p_minus_1:
            power = (p - 1) // pi
            if pow(g, power, p) == 1:
                is_gen = False
                break
        if is_gen:
            return g
```

---

### 3.4 Phân tích an toàn: Bài toán Logarit rời rạc (DLP)
Tìm x khi biết y ≡ g^x (mod p).
Các tính chất của Logarit rời rạc:
1. log_g(1) ≡ 0 (mod p - 1).
2. log_g(a * b mod p) ≡ log_g(a) + log_g(b) (mod p - 1).
3. log_g(a^k mod p) ≡ k * log_g(a) (mod p - 1).

---

### 3.5 Tấn công DLP bằng thuật toán Index-Calculus (Có ví dụ từng bước chi tiết)

#### VÍ DỤ TỪNG BƯỚC: Giải phương trình 6^x ≡ 57 (mod 107)
Tham số: g = 6, p = 107 => p - 1 = 106, mục tiêu b = 57.

##### Bước 1: Chọn Factor Base
Chọn tập số nguyên tố nhỏ S = {2, 3, 5, 7}.

##### Bước 2 & 3: Tìm quan hệ và lập hệ phương trình
1. Với j = 24: 6^24 ≡ 42 = 2 * 3 * 7 (mod 107)
   ```
   log_6(2) + log_6(3) + log_6(7) ≡ 24 (mod 106)      (1)
   ```
2. Với j = 6: 6^6 ≡ 4 = 2^2 (mod 107)
   ```
   2 * log_6(2) ≡ 6 (mod 106)                         (2)
   ```
3. Với j = 33: 6^33 ≡ 15 = 3 * 5 (mod 107)
   ```
   log_6(3) + log_6(5) ≡ 33 (mod 106)                 (3)
   ```
4. Với j = 34: 6^34 ≡ 90 = 2 * (3^2) * 5 (mod 107)
   ```
   log_6(2) + 2 * log_6(3) + log_6(5) ≡ 34 (mod 106)  (4)
   ```

##### Bước 4: Giải hệ phương trình tuyến tính modulo 106
- Từ (2): 2 * log_6(2) ≡ 6 => log_6(2) = 3.
- Lấy (4) trừ (3):
  ```
  log_6(2) + log_6(3) ≡ 34 - 33 = 1 (mod 106)
  3 + log_6(3) ≡ 1 => log_6(3) ≡ -2 ≡ 104 (mod 106).
  ```
- Thay vào (3):
  ```
  104 + log_6(5) ≡ 33 => log_6(5) ≡ 33 - 104 = -71 ≡ 35 (mod 106).
  ```
- Thay vào (1):
  ```
  3 + 104 + log_6(7) ≡ 24 => log_6(7) ≡ 23 (mod 106).
  ```
Kết quả:
```
log_6(2) ≡ 3,    log_6(3) ≡ 104,    log_6(5) ≡ 35,    log_6(7) ≡ 23  (mod 106)
```

##### Bước 5: Tính logarit cho mục tiêu b = 57
Chọn được số mũ k = 38 sao cho:
```
57 * (6^38) ≡ 35 = 5 * 7 (mod 107)
```
Lấy logarit hai vế:
```
log_6(57) + 38 ≡ log_6(5) + log_6(7) ≡ 35 + 23 = 58 (mod 106)
=> x = log_6(57) ≡ 58 - 38 = 20 (mod 106)
```
**Đáp số**: x = 20. (Kiểm tra: 6^20 mod 107 = 57, hoàn toàn chính xác!).

---

## 4. HỆ MÃ CÔNG KHAI ELGAMAL

### 4.1 Ý tưởng và Giao thức
Mã hóa xác suất (Probabilistic Encryption) dựa trên DLP:
- **Sinh khóa (KeyGen)**:
  - Chọn số nguyên tố p, phần tử sinh g.
  - Chọn khóa bí mật x thuộc {1, 2, ..., p - 2}.
  - Tính khóa công khai: h ≡ g^x (mod p).
  - Public Key: (p, g, h), Private Key: x.
- **Mã hóa (Encryption)**:
  - Chọn số ngẫu nhiên k thuộc {1, 2, ..., p - 2}.
  - Tính C1 ≡ g^k (mod p).
  - Tính C2 ≡ M * (h^k) (mod p).
  - Bản mã gửi đi: (C1, C2).
- **Giải mã (Decryption)**:
  - Tính bí mật chung: C1^x ≡ (g^k)^x ≡ h^k (mod p).
  - Tìm nghịch đảo: (C1^x)^(-1) (mod p).
  - Khôi phục bản rõ:
    ```
    M ≡ C2 * ((C1^x)^(-1)) (mod p)
    ```

---

### 4.2 Ví dụ minh họa tính toán chi tiết

#### Ví dụ 1 (Slide trang 64):
- Cho p = 11, g = 2, x = 3 => h = 2^3 = 8 (mod 11).
- Mã hóa M = 7, chọn k = 4:
  - C1 = 2^4 = 16 ≡ 5 (mod 11).
  - C2 = 7 * (8^4) ≡ 7 * 4 = 28 ≡ 6 (mod 11).
  - Bản mã: (C1 = 5, C2 = 6).
- Giải mã:
  - C1^x = 5^3 = 125 ≡ 4 (mod 11).
  - Tìm 4^(-1) mod 11: 4 * 3 = 12 ≡ 1 (mod 11) => 4^(-1) ≡ 3 (mod 11).
  - M = 6 * 3 = 18 ≡ 7 (mod 11). (Chính xác!).

#### Ví dụ 2 (Slide trang 65):
- Khóa công khai (p = 31, g = 11, h = 6), Khóa bí mật x = 5.
- Thông điệp M = 3, chọn k = 4:
  - C1 = 11^4 ≡ 9 (mod 31).
  - C2 = 3 * (6^4) = 3888 ≡ 13 (mod 31).
- Giải mã:
  - C1^x = 9^5 ≡ 25 (mod 31).
  - Tìm 25^(-1) mod 31: 25 * 5 = 125 = 4 * 31 + 1 ≡ 1 (mod 31) => 25^(-1) ≡ 5 (mod 31).
  - M = 13 * 5 = 65 ≡ 3 (mod 31). (Chính xác!).

---

## 5. LỖ HỔNG KINH ĐIỂN: TẤN CÔNG NGƯỜI ĐỨNG GIỮA (MAN-IN-THE-MIDDLE - MITM) & GIẢI PHÁP
- **Kịch bản**: Kẻ tấn công Eve chặn khóa công khai eA của Alice và eB của Bob, thay thế bằng eE của mình. Cả hai bên đều mã hóa dữ liệu gửi cho Eve mà không hề hay biết.
- **Giải pháp**:
  - Chữ ký số (Digital Signature).
  - Hạ tầng khóa công khai (PKI - Public Key Infrastructure) và Chứng chỉ số X.509 do Nhà cung cấp chứng chỉ (CA - Certificate Authority) phát hành.

---

## 6. BẢNG SO SÁNH TỔNG HỢP & ĐÚC KẾT ÔN THI

### Bảng so sánh 3 hệ thống mật mã công khai cốt lõi

| Tiêu chí so sánh | RSA | Diffie – Hellman | ElGamal |
| :--- | :--- | :--- | :--- |
| **Năm công bố** | 1977 | 1976 | 1985 |
| **Bài toán khó nền tảng** | Phân tích thừa số nguyên tố (IFP) | Logarit rời rạc (DLP) | Logarit rời rạc (DLP) |
| **Không gian tính toán** | Vành Z_n với n = p * q | Nhóm nhân Z_p^* (p nguyên tố) | Nhóm nhân Z_p^* (p nguyên tố) |
| **Mục đích chính** | Mã hóa dữ liệu & Ký số | Thỏa thuận / Trao đổi khóa bí mật | Mã hóa dữ liệu & Ký số |
| **Tính xác định / ngẫu nhiên** | Xác định (Cùng M ra cùng C) | Trao đổi khóa | Xác suất (Cùng M ra khác C) |
| **Kích thước bản mã** | Bằng kích thước khối | Trao đổi khóa | Gấp đôi kích thước khối (C1, C2) |
| **Tối ưu hóa hiệu năng** | Giải mã nhanh bằng CRT (~gấp 4 lần) | Chọn số mũ nhỏ/ECC (ECDH) | Tái sử dụng bảng nhân lũy thừa |
| **Lỗ hổng phổ biến** | Phân tích n nếu p, q gần nhau, MITM | MITM, Index-Calculus | MITM, lộ số ngẫu nhiên k |
