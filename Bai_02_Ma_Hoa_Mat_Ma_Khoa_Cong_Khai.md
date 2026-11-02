# BÀI 2: MÃ HÓA KHÓA CÔNG KHAI (PUBLIC-KEY CRYPTOGRAPHY)
> **Tài liệu tham khảo chuyên sâu & Giải thích chi tiết toàn bộ kiến thức theo slide bài giảng Môn Mã hóa - Mật mã (Khoa CNTT - ĐH Khoa học Tự nhiên).**

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
- **Mật mã đối xứng (Symmetric Cryptography)**: Hai bên liên lạc (Alice & Bob) dùng chung **một khóa bí mật duy nhất** $K$ cho cả hai quá trình mã hóa $E_K(M)$ và giải mã $D_K(C)$.
  - *Hạn chế chí mạng*: Bài toán phân phối khóa (Key Distribution Problem). Làm thế nào để hai bên chưa từng gặp nhau có thể thống nhất một khóa bí mật an toàn qua một kênh truyền công khai bị nghe lén? Hơn nữa, nếu có $N$ người dùng trong mạng, số lượng khóa cần quản lý là $\frac{N(N-1)}{2} = \mathcal{O}(N^2)$ — quá lớn khi mạng mở rộng.
- **Mật mã bất đối xứng / Khóa công khai (Asymmetric / Public-Key Cryptography)**:
  - Mỗi thực thể sở hữu một **cặp khóa (Key pair)** có liên hệ toán học mật thiết:
    - **Khóa công khai ($e$ - Public Key)**: Được công bố rộng rãi cho toàn thế giới biết, ai cũng có thể dùng để mã hóa thông điệp gửi cho người đó.
    - **Khóa bí mật ($d$ - Private Key)**: Được giữ bí mật tuyệt đối, chỉ người nhận mới sở hữu để giải mã thông điệp.
  - *Mục tiêu tối thượng*: Cho dù kẻ tấn công biết rõ thuật toán, khóa công khai $e$, và bản mã $c$, kẻ đó **vẫn không thể suy ngược ra khóa bí mật $d$ hay thông điệp gốc $m$ trong thời gian đa thức**.

---

### 1.2 Hàm một chiều có cửa mật (Trapdoor One-Way Function)
Đây là "trái tim" của mọi hệ mã hóa khóa công khai.

Một hàm số $f: D \to R$ được gọi là **Hàm một chiều có cửa mật** nếu thỏa mãn 3 điều kiện:
1. **Chiều thuận dễ tính (Easy forward)**: Cho trước $x \in D$, việc tính $y = f(x)$ có độ phức tạp tính toán thấp (chạy trong thời gian đa thức $\mathcal{O}(n^k)$).
2. **Chiều nghịch cực khó tính (Hard backward without trapdoor)**: Cho trước $y \in R$, việc tìm lại $x = f^{-1}(y)$ là bất khả thi về mặt tính toán (độ phức tạp siêu đa thức hoặc hàm mũ $\mathcal{O}(2^n)$, đòi hỏi hàng ngàn năm tính toán của siêu máy tính).
3. **Chiều nghịch dễ tính nếu có "cửa mật" (Easy backward with trapdoor)**: Nếu được cung cấp thêm một thông tin phụ bí mật $K$ (gọi là *Trapdoor* hay cửa mật), ta có thể tính ngược $x = f^{-1}_K(y)$ một cách dễ dàng và nhanh chóng.

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
  - Khóa công khai $e$ chính là thông số để thực hiện hàm $f(x)$.
  - Khóa cá nhân $d$ chính là thông tin cửa mật (Trapdoor) giúp đảo ngược hàm $f$.

---

### 1.3 Các bài toán khó kinh điển trong Mật mã học
Độ an toàn của các thuật toán mật mã không dựa trên sự bí mật của giải thuật, mà dựa vào độ khó nội tại của các bài toán toán học chưa có lời giải hiệu quả:

#### 1. Bài toán phân tích ra thừa số nguyên tố (Integer Factorization Problem - IFP)
- **Định lý cơ bản của số học (Fundamental Theorem of Arithmetic)**:
  Mọi số nguyên dương $n \in \mathbb{N}^+ \setminus \{0, 1\}$ đều có thể biểu diễn một cách duy nhất (không kể thứ tự các thừa số) dưới dạng tích các lũy thừa của số nguyên tố:
  $$n = p_1^{e_1} \cdot p_2^{e_2} \cdots p_k^{e_k}$$
- **Tính một chiều**:
  - Cho hai số nguyên tố rất lớn $p, q$ (ví dụ mỗi số dài 1024 hoặc 2048 bit). Việc nhân $n = p \cdot q$ diễn ra trong vài phần triệu giây.
  - Nhưng cho trước số $n$ (độ dài 2048 hoặc 4096 bit), việc tìm lại hai thừa số nguyên tố $p$ và $q$ là một thách thức cực kỳ lớn đối với các siêu máy tính hiện đại (bài toán IFP).
  - Ánh xạ $(p, q) \mapsto n = pq$ là hàm một chiều, và thông tin $p$ hoặc $q$ chính là cửa mật.
  - *Ứng dụng tiêu biểu*: **RSA**.

#### 2. Bài toán Logarit rời rạc (Discrete Logarithm Problem - DLP)
- Xét trên một nhóm cyclic hữu hạn (ví dụ nhóm nhân modulo số nguyên tố lớn $\mathbb{Z}_p^*$, với phần tử sinh $g$):
  $$y = g^x \pmod p$$
- **Tính một chiều**:
  - Cho $p, g$ và số nguyên $x$, việc tính $y = g^x \pmod p$ cực kỳ nhanh thông qua thuật toán lũy thừa nhanh bình phương và nhân (Square-and-Multiply) với độ phức tạp $\mathcal{O}(\log x)$.
  - Nhưng khi cho trước $p, g$ và giá trị $y$, bài toán tìm lại số mũ $x = \log_g(y) \pmod{p-1}$ trên tập số nguyên rời rạc lớn được công nhận là bài toán khó. Hiện chưa có thuật toán đa thức cổ điển nào giải được tổng quát.
  - Ánh xạ $(g, p, x) \mapsto g^x \pmod p$ là hàm một chiều, với $x$ là cửa mật bí mật.
  - *Ứng dụng tiêu biểu*: **Diffie-Hellman**, **ElGamal**, **DSA**.

#### 3. Các bài toán khó khác
- **Bài toán Tổng con (Subset Sum Problem - SSP / Knapsack)**: Ứng dụng trong hệ mã Merkle-Hellman.
- **Bài toán Phân tích Ma trận (Matrix Factorization Problem - MFP)**.
- *Lưu ý*: Cho đến nay, **IFP** và **DLP** vẫn là 2 bài toán nền tảng cốt lõi được ứng dụng rộng rãi và kiểm nghiệm thực tế vững chắc nhất trong mật mã hiện đại.

---

### 1.4 Lược đồ tổng quát thiết kế hệ mã (General Scheme - GS)
Để thiết kế một hệ mã công khai đạt chuẩn, quy trình gồm 3 bước:
1. **Bước 1**: Chọn hoặc xây dựng một bài toán khó toán học $P$ (như IFP hoặc DLP).
2. **Bước 2**: Thiết kế một hàm một chiều với cửa mật $f$.
3. **Bước 3**: Thiết kế hàm mã hóa và giải mã:
   - Các thông tin công bố được của hàm $f$ sẽ tạo thành **Khóa công khai (Public Key)**.
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
 Tính d = e^-1 mod phi(n)
 Public Key: (e, n)  ============================> Nhận (e, n)
 Private Key: d                                    Thông điệp m < n
                                                   Mã hóa: c = m^e mod n
 Nhận bản mã c       <============================ Gửi bản mã c
 Giải mã: m = c^d mod n
```

### 2.1 Định lý RSA & Giao thức hoàn chỉnh

#### Định lý RSA
> Cho $p$ và $q$ là 2 số nguyên tố phân biệt ($p \neq q$).
> Đặt $n = pq$, và hàm số Euler $\varphi(n) = (p - 1)(q - 1)$.
> Chọn hai số nguyên $e$ và $d$ thỏa mãn điều kiện đồng dư:
> $$e \cdot d \equiv 1 \pmod{\varphi(n)}$$
> Với mọi thông điệp $m \in \mathbb{Z}_n = \{0, 1, \dots, n-1\}$, nếu tính bản mã:
> $$c \equiv m^e \pmod n$$
> Thì bản rõ $m$ được phục hồi hoàn hảo bằng phép tính:
> $$m \equiv c^d \pmod n$$

#### Chi tiết Giao thức RSA

##### Giai đoạn I: Sinh khóa – $\text{KeyGen}(\lambda)$
1. **Chọn hai số nguyên tố ngẫu nhiên** độc lập $p$ và $q$, mỗi số có độ dài khoảng $\lambda / 2$ bit ($p \neq q$).
2. **Tính modulo RSA**: $n = p \cdot q$. (Độ dài của $n$ là $\lambda$ bit, ví dụ 2048 bit).
3. **Tính hàm phi Euler**: $\varphi(n) = (p - 1)(q - 1)$.
4. **Chọn số mũ công khai $e$**: Sao cho $1 < e < \varphi(n)$ và nguyên tố cùng nhau với $\varphi(n)$:
   $$\gcd(e, \varphi(n)) = 1$$
   *(Trong thực tế, người ta thường chọn $e = 65537 = 2^{16} + 1$ vì là số Fermat nguyên tố, biểu diễn nhị phân chỉ có 2 bit 1 giúp việc tính toán cực nhanh).*
5. **Tính số mũ bí mật $d$**: Là phần tử nghịch đảo nhân modulo của $e$ theo modulo $\varphi(n)$:
   $$d \equiv e^{-1} \pmod{\varphi(n)} \iff e \cdot d \equiv 1 \pmod{\varphi(n)}$$
   *(Tính bằng Thuật toán Euclid mở rộng).*
6. **Xuất kết quả**:
   - **Khóa công khai (Public Key)**: $PK = (e, n)$ (công bố rộng rãi).
   - **Khóa cá nhân (Private Key)**: $SK = (d, n)$ hoặc $(d, p, q)$ (giữ bí mật tuyệt đối).

##### Giai đoạn II: Mã hóa – $\text{Encryption}(e, n, m)$
- Bob muốn gửi thông điệp $m$ cho Alice ($0 \le m < n$):
- Sử dụng khóa công khai $(e, n)$ của Alice, Bob tính:
  $$c = m^e \pmod n$$
- Bob gửi bản mã $c$ cho Alice.

##### Giai đoạn III: Giải mã – $\text{Decryption}(d, n, c)$
- Alice nhận được bản mã $c$:
- Sử dụng khóa cá nhân $d$ của mình, Alice tính:
  $$m = c^d \pmod n$$
- Alice khôi phục được thông điệp gốc $m$.

---

### 2.2 Độ an toàn & Tấn công toàn phần (Full Attack)
- **Tấn công toàn phần (Full Attack)**: Kẻ tấn công (Eve) có trong tay khóa công khai $(e, n)$ và muốn tìm ra khóa bí mật $d$.
- Theo định nghĩa:
  $$e \cdot d \equiv 1 \pmod{\varphi(n)}$$
  Để tìm được $d$, Eve bắt buộc phải tính được:
  $$\varphi(n) = (p - 1)(q - 1) = pq - (p + q) + 1 = n - (p + q) + 1$$
- Nhưng để biết được tổng $(p + q)$, Eve phải biết được riêng lẻ từng số nguyên tố $p$ và $q$.
- Điều này tương đương với việc **phải giải bài toán phân tích thừa số nguyên tố (IFP)** của số lớn $n = pq$.
- Khi $n$ có kích thước từ 2048 đến 4096 bit, các thuật toán phân tích thừa số tốt nhất hiện nay (như General Number Field Sieve - GNFS) đòi hỏi thời gian tính toán vượt xa tuổi thọ vũ trụ. Do đó, RSA an toàn trước tấn công toàn phần nếu độ dài khóa đủ lớn.

---

### 2.3 Cài đặt tính toán số lớn (BigInteger Implementation)
Vì RSA làm việc với các số nguyên hàng trăm đến hàng ngàn chữ số (vượt quá kiểu dữ liệu 64-bit chuẩn của CPU), ta bắt buộc phải cài đặt các cấu trúc và giải thuật số lớn:

#### 1. Phép cộng modulo: `addMod(a, b, n)`
$$c \equiv a + b \pmod n = \begin{cases} a + b & \text{nếu } a + b < n \\ a + b - n & \text{nếu } a + b \ge n \end{cases}$$
*(Cách này giúp tránh phép chia lấy dư `% n` vốn tốn nhiều chu kỳ máy).*

#### 2. Phép nhân modulo: `mulMod(x, y, n)`
Biểu diễn $y$ dưới dạng nhị phân $b$ bit: $y = \sum_{i=0}^{b-1} y_i 2^i$ với $y_i \in \{0, 1\}$.
Ta có: $x \cdot y \pmod n = \sum_{i=0}^{b-1} y_i (x \cdot 2^i) \pmod n$.
Nhận xét: $x \cdot 2^{i+1} \equiv 2 \cdot (x \cdot 2^i) \pmod n$.

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

#### 3. Phép lũy thừa modulo: `powerMod(x, a, n)` (Thuật toán Bình phương và Nhân - Square-and-Multiply)
Để tính $x^a \pmod n$ với số mũ $a$ hàng ngàn bit:
Biểu diễn số mũ $a = \sum_{i=0}^{b-1} a_i 2^i$.

**Cách 1: Quét từ bit thấp nhất đến cao nhất (LSB $\to$ MSB)**
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

**Cách 2: Quét từ bit cao nhất đến thấp nhất (MSB $\to$ LSB)**
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
*Độ phức tạp*: Chỉ cần tối đa $2b$ phép nhân modulo, thay vì $2^b$ phép tính nếu nhân tuần tự!

#### 4. Thuật toán Euclid và Euclid nhị phân (Binary GCD)
Tìm ước chung lớn nhất $\gcd(x, y)$ mà không cần thực hiện phép chia lấy dư chậm chạp:
- **Nguyên lý nhị phân**:
  - Nếu cả $x, y$ đều chẵn: $\gcd(x, y) = 2 \cdot \gcd(x/2, y/2)$.
  - Nếu $x$ chẵn, $y$ lẻ: $\gcd(x, y) = \gcd(x/2, y)$.
  - Nếu $x$ lẻ, $y$ chẵn: $\gcd(x, y) = \gcd(x, y/2)$.
  - Nếu cả $x, y$ đều lẻ: $\gcd(x, y) = \gcd(|x - y|/2, \min(x, y))$.

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
- **Định lý Bézout**: Với hai số nguyên dương $a, b$, luôn tồn tại các số nguyên $x, y \in \mathbb{Z}$ sao cho:
  $$a \cdot x + b \cdot y = \gcd(a, b)$$
- Áp dụng tìm nghịch đảo modulo:
  Khi $\gcd(e, \varphi) = 1$, ta có:
  $$e \cdot d + \varphi \cdot y = 1 \implies e \cdot d \equiv 1 \pmod \varphi \implies d \equiv e^{-1} \pmod \varphi$$

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
Nếu $p$ là số nguyên tố thì với mọi số nguyên cơ sở $b$ không chia hết cho $p$:
$$b^{p-1} \equiv 1 \pmod p$$

#### 2. Số giả nguyên tố (Pseudo-prime) & Số giả nguyên tố mạnh (Strong Pseudo-prime)
- Nếu $p$ là số nguyên tố lẻ lớn hơn 2, ta có thể viết $p - 1 = 2^r \cdot m$ (với $m$ là số lẻ).
- Xét dãy bình phương liên tiếp từ $b^m \pmod p$:
  $$b^m, b^{2m}, b^{4m}, \dots, b^{2^r m} \equiv b^{p-1} \pmod p$$
- Theo tính chất số học trên trường nguyên tố: Số duy nhất có bình phương đồng dư 1 modulo $p$ là $1$ và $-1 \equiv p - 1$.
- Do đó, nếu $p$ là số nguyên tố, thì:
  - Hoặc $b^m \equiv 1 \pmod p$ hoặc $b^m \equiv -1 \pmod p$.
  - Hoặc tồn tại một số $k \in \{0, 1, \dots, r-1\}$ sao cho $b^{2^k m} \equiv -1 \pmod p$.
- Nếu kiểm tra qua nhiều cơ sở ngẫu nhiên $b$ mà $p$ vẫn thỏa mãn điều kiện trên, $p$ được gọi là **số giả nguyên tố mạnh (Strong Pseudo-prime)**. Xác suất một hợp số vượt qua được $t$ vòng kiểm tra ngẫu nhiên là nhỏ hơn $(\frac{1}{4})^t$. Khi $t = 50$, xác suất sai số là $2^{-100}$ (nhỏ hơn xác suất thiên thạch va vào máy tính).

```python
def is_prime_miller_rabin(p, iterations=40):
    if p < 2: return False
    if p in (2, 3): return True
    if p % 2 == 0: return False
    
    # Bước 1: Phân tích p - 1 = 2^r * m (với m lẻ)
    r = 0
    m = p - 1
    while m % 2 == 0:
        r += 1
        m //= 2
        
    # Bước 2: Kiểm tra qua nhiều cơ sở b ngẫu nhiên
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
Mục tiêu là chứng minh rằng với $ed \equiv 1 \pmod{\varphi(n)}$ và $c \equiv m^e \pmod n$, ta luôn có:
$$c^d \equiv (m^e)^d \equiv m^{ed} \equiv m \pmod n$$

**Chứng minh chi tiết:**
Vì $ed \equiv 1 \pmod{\varphi(n)}$, theo định nghĩa phép chia dư, tồn tại số nguyên $k$ sao cho:
$$ed = k \cdot \varphi(n) + 1 = k(p - 1)(q - 1) + 1$$
Do đó:
$$m^{ed} = m^{k(p-1)(q-1) + 1} = m \cdot \left(m^{p-1}\right)^{k(q-1)}$$

Ta xét modulo cho từng số nguyên tố $p$ và $q$:
1. **Xét modulo $p$**:
   - *Trường hợp 1*: Nếu $\gcd(m, p) = 1$ (tức $m$ không chia hết cho $p$), theo Định lý Fermat nhỏ ta có $m^{p-1} \equiv 1 \pmod p$:
     $$m^{ed} \equiv m \cdot (1)^{k(q-1)} \equiv m \pmod p$$
   - *Trường hợp 2*: Nếu $p \mid m$, nghĩa là $m \equiv 0 \pmod p$. Khi đó:
     $$m^{ed} \equiv 0^{ed} \equiv 0 \equiv m \pmod p$$
   $\implies$ Trong mọi trường hợp, ta luôn có:
   $$m^{ed} \equiv m \pmod p$$

2. **Xét modulo $q$**: Hoàn toàn tương tự:
   $$m^{ed} \equiv m \pmod q$$

3. **Kết hợp bằng Định lý Thặng dư Trung Hoa (CRT)**:
   Ta có hệ phương trình đồng dư:
   $$\begin{cases} m^{ed} \equiv m \pmod p \\ m^{ed} \equiv m \pmod q \end{cases}$$
   Vì $p$ và $q$ là 2 số nguyên tố phân biệt nên $\gcd(p, q) = 1$. Theo Định lý Thặng dư Trung Hoa, nghiệm của hệ trên là duy nhất modulo $n = pq$:
   $$m^{ed} \equiv m \pmod{pq} \iff m^{ed} \equiv m \pmod n$$
   *(Chứng minh hoàn tất).* $\blacksquare$

---

### 2.6 Kỹ thuật giải mã nhanh RSA (RSA Fast Decryption with CRT)
Trong RSA, việc giải mã đòi hỏi tính $m = c^d \pmod n$. Do $d$ và $n$ là những số rất lớn, phép tính này tốn nhiều tài nguyên.
Tuy nhiên, người sở hữu khóa cá nhân biết rõ $p$ và $q$. Kỹ thuật **RSA-CRT** cho phép giảm đáng kể kích thước số mũ và modulo tính toán!

#### Các bước thuật giải Giải mã nhanh:
1. **Tiền tính toán các số mũ rút gọn**:
   $$d_1 = d \pmod{p - 1}$$
   $$d_2 = d \pmod{q - 1}$$
2. **Tính toán trên các modulo nhỏ**:
   $$a_1 = c^{d_1} \pmod p$$
   $$a_2 = c^{d_2} \pmod q$$
   *(Vì $d_1, d_2$ và $p, q$ chỉ dài bằng một nửa $d$ và $n$, phép lũy thừa trên các số nửa bit nhanh hơn gấp ~8 lần).*
3. **Phục hồi $m$ bằng công thức CRT (Garner's Formula)**:
   Tìm $m$ thỏa mãn $\begin{cases} m \equiv a_1 \pmod p \\ m \equiv a_2 \pmod q \end{cases}$:
   $$h = (a_1 - a_2) \cdot q^{-1} \pmod p$$
   $$m = a_2 + h \cdot q$$

```python
def rsa_fast_decryption(c, d, p, q):
    # 1. Rút gọn số mũ
    d1 = d % (p - 1)
    d2 = d % (q - 1)
    
    # 2. Lũy thừa modulo nhỏ
    a1 = pow(c, d1, p)
    a2 = pow(c, d2, q)
    
    # 3. Kết hợp CRT
    q_inv = pow(q, -1, p) # Nghịch đảo của q mod p
    h = ((a1 - a2) * q_inv) % p
    m = a2 + h * q
    return m
```
- **Hiệu năng**: Kỹ thuật này giúp tốc độ giải mã tăng trung bình **gấp 4 lần** so với tính toán trực tiếp $c^d \pmod n$.

---

## 3. GIAO THỨC TRAO ĐỔI KHÓA DIFFIE – HELLMAN

Được đề xuất bởi Whitfield Diffie và Martin Hellman năm 1976, đây là giao thức đặt nền móng cho mật mã khóa công khai, giải quyết hoàn hảo vấn đề thỏa thuận khóa bí mật qua kênh truyền không tin cậy.

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

### 3.1 Mục tiêu và Quy trình giao thức
- **Mục tiêu**: Alice và Bob muốn cùng sở hữu một khóa bí mật $K$ để sau đó dùng cho mã hóa đối xứng tốc độ cao (như AES), mà không ai khác trên mạng có thể tính được $K$.

#### Các bước thực hiện:
1. **Thiết lập thông số dùng chung công khai**:
   - Chọn một số nguyên tố lớn $p$ (độ dài $b$ bit, thường $\ge 2048$ bit).
   - Chọn một phần tử sinh $g$ của nhóm $\mathbb{Z}_p^*$.
   - Các giá trị $(p, g)$ được công khai cho cả thế giới biết.
2. **Alice chọn bí mật và trao đổi**:
   - Alice chọn ngẫu nhiên một số nguyên bí mật $x \in \{1, 2, \dots, p - 2\}$.
   - Alice tính giá trị công khai: $k_A = g^x \pmod p$.
   - Alice gửi $k_A$ cho Bob.
3. **Bob chọn bí mật và trao đổi**:
   - Bob chọn ngẫu nhiên một số nguyên bí mật $y \in \{1, 2, \dots, p - 2\}$.
   - Bob tính giá trị công khai: $k_B = g^y \pmod p$.
   - Bob gửi $k_B$ cho Alice.
4. **Thiết lập khóa bí mật chung**:
   - Alice nhận $k_B$, dùng số bí mật $x$ của mình để tính:
     $$K = (k_B)^x \pmod p \equiv (g^y)^x \equiv g^{xy} \pmod p$$
   - Bob nhận $k_A$, dùng số bí mật $y$ của mình để tính:
     $$K' = (k_A)^y \pmod p \equiv (g^x)^y \equiv g^{xy} \pmod p$$
   - Kết quả: $K = K' = g^{xy} \pmod p$. Hai bên đã có chung khóa bí mật $K$ mà kẻ nghe lén (chỉ thấy $p, g, k_A, k_B$) không thể tính được nếu không tìm được $x$ hoặc $y$.

---

### 3.2 Cơ sở toán học: Cấu trúc Nhóm (Group) & Nhóm tuần hoàn (Cyclic Group)

#### 1. Định nghĩa Cấu trúc Nhóm (Group)
Một tập hợp khác rỗng $G$ cùng với một phép toán 2 ngôi $*: G \times G \to G$ được gọi là một **Nhóm $(G, *)$** nếu thỏa mãn 4 tiên đề:
1. **Tính đóng (Closure)**: $\forall x, y \in G \implies x * y \in G$.
2. **Phần tử đơn vị (Identity element)**: Tồn tại duy nhất $e \in G$ sao cho:
   $$\forall x \in G: x * e = e * x = x$$
3. **Phần tử nghịch đảo (Inverse element)**: Với mọi $x \in G$, tồn tại $x^{-1} \in G$ sao cho:
   $$x * x^{-1} = x^{-1} * x = e$$
4. **Tính kết hợp (Associativity)**: $\forall x, y, z \in G$:
   $$(x * y) * z = x * (y * z)$$

*Ví dụ:*
- $(\mathbb{Z}, +)$: Tập số nguyên với phép cộng thông thường là một nhóm (phần tử đơn vị là 0, nghịch đảo của $x$ là $-x$).
- $(\mathbb{Z}_p^*, \cdot \pmod p)$: Với $p$ là số nguyên tố, tập hợp $\mathbb{Z}_p^* = \{1, 2, \dots, p - 1\}$ cùng với phép nhân modulo $p$ là một nhóm Abel (phần tử đơn vị là 1, mọi phần tử đều khả nghịch vì $\gcd(x, p) = 1$).

#### 2. Nhóm con (Subgroup) & Phép lũy thừa
- Cho nhóm $(G, *)$, tập con $H \subseteq G$ ($H \neq \emptyset$) được gọi là **nhóm con** nếu $(H, *)$ tự thân là một nhóm.
- **Phép lũy thừa**: Với phần tử $x \in (G, *)$, $x^k = \underbrace{x * x * \dots * x}_{k \text{ lần}}$, quy ước $x^0 = e$.

#### 3. Nhóm tuần hoàn (Cyclic Group) & Phần tử sinh (Generator)
- Nhóm con sinh bởi phần tử $x$, ký hiệu $\langle x \rangle = \{x^k \mid k \in \mathbb{Z}\}$.
- Nếu $G$ hữu hạn, luôn tồn tại số nguyên dương $k$ nhỏ nhất sao cho $x^k = e$. Số $k$ này gọi là **bậc của phần tử $x$**, ký hiệu $o(x) = k$.
- Nếu tồn tại một phần tử $g \in G$ sao cho $\langle g \rangle = G$, thì $G$ được gọi là **nhóm tuần hoàn (Cyclic Group)**, và $g$ được gọi là **phần tử sinh (Generator)** của nhóm.
- Khi $g$ là phần tử sinh của $G$ (có kích thước $|G|$), thì tập hợp:
  $$\{g^0, g^1, g^2, \dots, g^{|G|-1}\}$$
  chính là một hoán vị đầy đủ của tất cả các phần tử trong $G$.

---

### 3.3 Thuật toán tìm phần tử sinh (Generator)
Trong nhóm nhân $\mathbb{Z}_p^*$ (với $p$ nguyên tố), bậc của nhóm là $| \mathbb{Z}_p^* | = p - 1$.
Một phần tử $g \in \mathbb{Z}_p^*$ là phần tử sinh khi và chỉ khi bậc của nó bằng $p - 1$:
$$o(g) = p - 1$$

*Ví dụ minh họa (trên $\mathbb{Z}_7^*$ có bậc $7 - 1 = 6$)*:
- Với $x = 2$:
  $$2^0 = 1, 2^1 = 2, 2^2 = 4, 2^3 = 8 \equiv 1 \implies \langle 2 \rangle = \{1, 2, 4\}$$
  $\implies o(2) = 3 \neq 6 \implies 2$ **không phải** là phần tử sinh.
- Với $x = 3$:
  $$3^0=1, 3^1=3, 3^2=2, 3^3=6, 3^4=4, 3^5=5, 3^6=1 \implies \langle 3 \rangle = \{1, 2, 3, 4, 5, 6\} = \mathbb{Z}_7^*$$
  $\implies o(3) = 6 \implies 3$ **chính là** phần tử sinh.

#### Thuật toán kiểm tra và tìm phần tử sinh:
Giả sử ta biết phân tích thừa số nguyên tố của $p - 1$:
$$p - 1 = p_1^{e_1} p_2^{e_2} \cdots p_n^{e_n}$$
Để kiểm tra $g$ có phải là phần tử sinh hay không, ta **chỉ cần kiểm tra** điều kiện:
$$g^{\frac{p-1}{p_i}} \not\equiv 1 \pmod p \quad (\forall i = 1, 2, \dots, n)$$

```python
def find_generator(p, prime_factors_of_p_minus_1):
    # prime_factors_of_p_minus_1 là tập các ước số nguyên tố {p1, p2, ..., pn} của p - 1
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
Kẻ tấn công biết $(p, g)$ và các khóa công khai $k_A = g^x \pmod p$, $k_B = g^y \pmod p$.
Để tính được khóa chung $K = g^{xy} \pmod p$, kẻ tấn công đối mặt với **Bài toán Diffie-Hellman tính toán (Computational Diffie-Hellman - CDH)**. Cách tự nhiên nhất để giải CDH là giải bài toán DLP:
$$x = \log_g(k_A) \pmod p$$
Khi $p$ đủ lớn ($\ge 2048$ bit), bài toán này là bất khả thi với các thuật toán ngây thơ.

#### Các tính chất của Logarit rời rạc:
Với $g$ là phần tử sinh của $\mathbb{Z}_p^*$, và $a, b$ là các số nguyên không chia hết cho $p$:
1. $\log_g(1) \equiv 0 \pmod{p - 1}$.
2. $\log_g(a \cdot b \pmod p) \equiv \log_g(a) + \log_g(b) \pmod{p - 1}$.
3. $\log_g(a^k \pmod p) \equiv k \cdot \log_g(a) \pmod{p - 1}$.

---

### 3.5 Tấn công DLP bằng thuật toán Index-Calculus (Có ví dụ từng bước chi tiết)
Thuật toán **Index-Calculus** là một trong những phương pháp tấn công mạnh nhất vào bài toán Logarit rời rạc trên trường $\mathbb{Z}_p^*$.

#### Quy trình thuật toán:
Cho trước $p, g$ và mục tiêu $b$. Ta cần tìm $x$ sao cho $g^x \equiv b \pmod p$.
- **Bước 1 (Chọn Factor Base)**: Chọn một tập con gồm $t$ số nguyên tố nhỏ $S = \{p_1, p_2, \dots, p_t\}$ (gọi là cơ sở thừa số - Factor Base).
- **Bước 2 (Thu thập quan hệ)**: Chọn ngẫu nhiên số mũ $j$ ($0 \le j < p - 1$), tính $A = g^j \pmod p$. Thử phân tích $A$ hoàn toàn ra các thừa số chỉ thuộc tập $S$:
  $$g^j \equiv p_1^{e_1} p_2^{e_2} \cdots p_t^{e_t} \pmod p$$
- **Bước 3 (Lấy logarit 2 vế)**:
  $$j \equiv e_1 \log_g(p_1) + e_2 \log_g(p_2) + \dots + e_t \log_g(p_t) \pmod{p - 1}$$
- **Bước 4 (Giải hệ phương trình tuyến tính)**: Lặp lại Bước 2 và 3 để thu thập ít nhất $t$ phương trình độc lập tuyến tính. Giải hệ phương trình modulo $(p - 1)$ để tìm các giá trị ẩn số: $\log_g(p_1), \log_g(p_2), \dots, \log_g(p_t)$.
- **Bước 5 (Giải logarit cho mục tiêu $b$)**: Chọn ngẫu nhiên số $k$, tính $B = b \cdot g^k \pmod p$. Thử phân tích $B$ theo tập $S$:
  $$b \cdot g^k \equiv p_1^{d_1} p_2^{d_2} \cdots p_t^{d_t} \pmod p$$
  Lấy logarit 2 vế:
  $$\log_g(b) + k \equiv d_1 \log_g(p_1) + \dots + d_t \log_g(p_t) \pmod{p - 1}$$
  $$\implies x = \log_g(b) \equiv \sum_{i=1}^t d_i \log_g(p_i) - k \pmod{p - 1}$$

---

#### VÍ DỤ TỪNG BƯỚC CHI TIẾT (Theo bài giảng)
**Đề bài**: Tìm số nguyên $x$ sao cho:
$$6^x \equiv 57 \pmod{107}$$
*(Ở đây: cơ số $g = 6$, modulo $p = 107 \implies p - 1 = 106$, mục tiêu $b = 57$).*

##### Bước 1: Chọn Factor Base
Chọn $S = \{2, 3, 5, 7\}$.

##### Bước 2 & 3: Tìm quan hệ và lập hệ phương trình
Sau khi thử các số mũ ngẫu nhiên $j$, ta tìm được 4 giá trị trơn trên $S$:
1. Với $j = 24$:
   $$6^{24} \equiv 42 \pmod{107}$$
   Phân tích: $42 = 2 \cdot 3 \cdot 7$.
   Lấy log cơ số 6 modulo 106:
   $$\log_6(2) + \log_6(3) + \log_6(7) \equiv 24 \pmod{106} \quad (1)$$

2. Với $j = 6$:
   $$6^6 \equiv 4 \pmod{107}$$
   Phân tích: $4 = 2^2$.
   Lấy log:
   $$2 \log_6(2) \equiv 6 \pmod{106} \quad (2)$$

3. Với $j = 33$:
   $$6^{33} \equiv 15 \pmod{107}$$
   Phân tích: $15 = 3 \cdot 5$.
   Lấy log:
   $$\log_6(3) + \log_6(5) \equiv 33 \pmod{106} \quad (3)$$

4. Với $j = 34$:
   $$6^{34} \equiv 90 \pmod{107}$$
   Phân tích: $90 = 2 \cdot 3^2 \cdot 5$.
   Lấy log:
   $$\log_6(2) + 2\log_6(3) + \log_6(5) \equiv 34 \pmod{106} \quad (4)$$

##### Bước 4: Giải hệ phương trình tuyến tính modulo 106
- Từ phương trình (2): $2 \log_6(2) \equiv 6 \pmod{106} \implies \log_6(2) = 3$ (hoặc 56, kiểm tra $6^3 = 216 \equiv 2 \pmod{107} \implies \log_6(2) = 3$).
- Trừ phương trình (4) cho phương trình (3):
  $$\left[\log_6(2) + 2\log_6(3) + \log_6(5)\right] - \left[\log_6(3) + \log_6(5)\right] \equiv 34 - 33 \pmod{106}$$
  $$\implies \log_6(2) + \log_6(3) \equiv 1 \pmod{106}$$
  Thay $\log_6(2) = 3$ vào:
  $$3 + \log_6(3) \equiv 1 \implies \log_6(3) \equiv -2 \equiv 104 \pmod{106}$$
- Thay $\log_6(3) = 104$ vào phương trình (3):
  $$104 + \log_6(5) \equiv 33 \pmod{106} \implies \log_6(5) \equiv 33 - 104 = -71 \equiv 35 \pmod{106}$$
- Thay vào phương trình (1):
  $$\log_6(2) + \log_6(3) + \log_6(7) \equiv 24 \pmod{106}$$
  $$3 + 104 + \log_6(7) \equiv 24 \implies 1 + \log_6(7) \equiv 24 \implies \log_6(7) \equiv 23 \pmod{106}$$

**Kết quả trung gian**:
$$\begin{cases} \log_6(2) \equiv 3 \pmod{106} \\ \log_6(3) \equiv 104 \pmod{106} \\ \log_6(5) \equiv 35 \pmod{106} \\ \log_6(7) \equiv 23 \pmod{106} \end{cases}$$

##### Bước 5: Tính logarit cho mục tiêu $b = 57$
- Thử chọn ngẫu nhiên $k$: sau nhiều lần, chọn được $k = 38$:
  $$57 \cdot 6^{38} \equiv 35 \pmod{107}$$
- Ta thấy $35$ phân tích được trên $S$: $35 = 5 \cdot 7$.
- Lấy logarit cơ số 6 hai vế modulo 106:
  $$\log_6(57) + 38 \equiv \log_6(5) + \log_6(7) \pmod{106}$$
- Thay các giá trị log đã tìm được ở Bước 4 vào:
  $$\log_6(57) + 38 \equiv 35 + 23 = 58 \pmod{106}$$
  $$\implies \log_6(57) \equiv 58 - 38 = 20 \pmod{106}$$

**Đáp số**: $x = 20$.
*(Kiểm tra lại: $6^{20} \pmod{107} = 57$, hoàn toàn chính xác!)*

---

## 4. HỆ MÃ CÔNG KHAI ELGAMAL

Được phát minh bởi Taher Elgamal năm 1985, hệ mã ElGamal là bước phát triển xuất sắc chuyển đổi giao thức trao đổi khóa Diffie-Hellman thành một **hệ mã hóa bất đối xứng hoàn chỉnh**.

```
           Khởi tạo khóa:
           p: số nguyên tố lớn, g: phần tử sinh
           Khóa riêng: x in {1, ..., p - 2}
           Khóa công khai: h = g^x mod p
           Public Key: (p, g, h) | Private Key: x

       Alice (Người nhận)                               Bob (Người gửi)
 -----------------------------                     -----------------------------
 Công bố (p, g, h)           ====================> Nhận (p, g, h)
                                                   Thông điệp M in Zp
                                                   Chọn ngẫu nhiên k (phù du)
                                                   C1 = g^k mod p
                                                   C2 = M * (h^k) mod p
 Nhận (C1, C2)               <==================== Gửi bản mã: (C1, C2)
 Tính bí mật chung:
   s = (C1)^x = g^(kx) mod p
 Tính nghịch đảo: s^-1 mod p
 Phục hồi:
   M = C2 * s^-1 mod p
```

### 4.1 Ý tưởng và Mục tiêu
- **Ý tưởng**: Sử dụng phép lũy thừa modulo và bảo mật dựa trên bài toán khó Logarit rời rạc (DLP).
- **Tính chất đặc sắc (Mã hóa xác suất - Probabilistic Encryption)**:
  - Mỗi lần mã hóa cùng một thông điệp $M$, Bob chọn một số ngẫu nhiên $k$ mới (gọi là *khóa phù du - ephemeral key*).
  - Kết quả là bản mã $(C_1, C_2)$ sẽ hoàn toàn khác nhau qua mỗi lần mã hóa!
  - Điều này giúp ElGamal chống lại kiểu tấn công phân tích thống kê bản rõ đã biết (Chosen Plaintext Attack - CPA), vượt trội hơn RSA thuần túy (RSA deterministic).

---

### 4.2 Giao thức ElGamal: Sinh khóa, Mã hóa, Giải mã

#### 1. Sinh khóa – KeyGen
1. Chọn một số nguyên tố lớn $p$.
2. Chọn một phần tử sinh $g$ của nhóm $\mathbb{Z}_p^*$.
3. Chọn khóa bí mật $x$ ngẫu nhiên: $x \in \{1, 2, \dots, p - 2\}$ *(Lưu ý: Không chọn $x = p - 1$ hoặc các giá trị tầm thường)*.
4. Tính khóa công khai:
   $$h = g^x \pmod p$$
5. **Đầu ra**:
   - **Khóa công khai (Public Key)**: $(p, g, h)$.
   - **Khóa bí mật (Private Key)**: $x$.

#### 2. Mã hóa thông điệp – $\text{Encryption}(p, g, h, M)$
Để gửi thông điệp số nguyên $M \in \mathbb{Z}_p^*$ cho Alice:
1. Bob chọn một số nguyên ngẫu nhiên bí mật $k \in \{1, 2, \dots, p - 2\}$.
2. Bob tính hai thành phần của bản mã:
   - Thành phần 1 (gợi ý khóa chung):
     $$C_1 = g^k \pmod p$$
   - Thành phần 2 (thông điệp bị che mặt nạ bởi $h^k$):
     $$C_2 = M \cdot h^k \pmod p$$
3. Bob gửi cặp bản mã $C = (C_1, C_2)$ cho Alice.

#### 3. Giải mã thông điệp – $\text{Decryption}(x, p, C_1, C_2)$
Khi Alice nhận được $(C_1, C_2)$:
1. Alice dùng khóa bí mật $x$ để tính lại giá trị "mặt nạ bí mật" đã được dùng để nhân với $M$:
   $$C_1^x \equiv (g^k)^x \equiv g^{kx} \equiv (g^x)^k \equiv h^k \pmod p$$
2. Alice tìm phần tử nghịch đảo nhân của $C_1^x$ modulo $p$:
   $$(C_1^x)^{-1} \pmod p$$
3. Alice khôi phục lại thông điệp gốc $M$:
   $$M = C_2 \cdot (C_1^x)^{-1} \pmod p$$
   *(Vì $C_2 \cdot (C_1^x)^{-1} \equiv (M \cdot h^k) \cdot (h^k)^{-1} \equiv M \pmod p$).*

---

### 4.3 Ví dụ minh họa step-by-step & Bài tập tính toán

#### Ví dụ minh họa 1 (Theo slide trang 64)
- **Thông số ban đầu**:
  - Số nguyên tố $p = 11$, phần tử sinh $g = 2$.
  - Khóa bí mật của Alice: $x = 3$.
  - Khóa công khai của Alice: $h = g^x \pmod p = 2^3 \pmod{11} = 8$.
  - Public Key: $(p=11, g=2, h=8)$.
- **Mã hóa**:
  - Bob muốn gửi thông điệp $M = 7$.
  - Bob chọn số ngẫu nhiên $k = 4$.
  - Tính $C_1 = g^k \pmod p = 2^4 \pmod{11} = 16 \equiv 5 \pmod{11}$.
  - Tính $C_2 = M \cdot h^k \pmod p = 7 \cdot 8^4 \pmod{11}$:
    Ta có $8 \equiv -3 \pmod{11} \implies 8^4 \equiv (-3)^4 = 81 \equiv 4 \pmod{11}$.
    $\implies C_2 = 7 \cdot 4 = 28 \equiv 6 \pmod{11}$.
  - Bản mã gửi đi: $(C_1 = 5, C_2 = 6)$.
- **Giải mã**:
  - Alice nhận $(C_1 = 5, C_2 = 6)$ và dùng khóa bí mật $x = 3$:
  - Tính $C_1^x \pmod p = 5^3 = 125 \equiv 4 \pmod{11}$.
  - Tìm nghịch đảo của $4$ modulo 11:
    Vì $4 \cdot 3 = 12 \equiv 1 \pmod{11} \implies 4^{-1} \equiv 3 \pmod{11}$.
  - Khôi phục thông điệp:
    $$M = C_2 \cdot (C_1^x)^{-1} \pmod{11} = 6 \cdot 3 = 18 \equiv 7 \pmod{11}$$
  - Kết quả: $M = 7$ (chính xác tuyệt đối).

---

#### Ví dụ minh họa 2 (Bài tập slide trang 65)
- **Cho trước**:
  - Khóa công khai: $(p=31, g=11, h=6)$.
  - Khóa bí mật: $x = 5$ *(Kiểm tra: $11^5 \equiv 6 \pmod{31}$)*.
  - Thông điệp cần mã hóa: $M = 3$.
  - Chọn số ngẫu nhiên: $k = 4$.
- **Thực hiện Mã hóa**:
  1. $C_1 = g^k \pmod p = 11^4 \pmod{31}$:
     $11^2 = 121 \equiv 28 \equiv -3 \pmod{31}$.
     $11^4 \equiv (-3)^2 = 9 \pmod{31} \implies C_1 = 9$.
  2. $C_2 = M \cdot h^k \pmod p = 3 \cdot 6^4 \pmod{31}$:
     $6^2 = 36 \equiv 5 \pmod{31} \implies 6^4 \equiv 5^2 = 25 \pmod{31}$.
     $C_2 = 3 \cdot 25 = 75 \equiv 13 \pmod{31} \implies C_2 = 13$.
  - Bản mã: $(C_1 = 9, C_2 = 13)$.
- **Thực hiện Giải mã**:
  1. Tính $C_1^x \pmod p = 9^5 \pmod{31}$:
     $9^2 = 81 \equiv 19 \equiv -12 \pmod{31}$.
     $9^4 \equiv (-12)^2 = 144 \equiv 20 \equiv -11 \pmod{31}$.
     $9^5 = 9^4 \cdot 9 \equiv (-11) \cdot 9 = -99 \equiv 25 \pmod{31} \implies C_1^x = 25$.
  2. Tìm nghịch đảo $25^{-1} \pmod{31}$:
     Vì $25 \equiv -6 \pmod{31}$. Ta tìm $y$ sao cho $-6y \equiv 1 \pmod{31} \iff 6y \equiv 30 \pmod{31} \implies y = 5$.
     Kiểm tra: $25 \cdot 5 = 125 = 4 \cdot 31 + 1 \equiv 1 \pmod{31}$.
     $\implies 25^{-1} \equiv 5 \pmod{31}$.
  3. Khôi phục $M$:
     $$M = C_2 \cdot (C_1^x)^{-1} \pmod{31} = 13 \cdot 5 = 65 = 2 \cdot 31 + 3 \equiv 3 \pmod{31}$$
  - Kết quả: $M = 3$ (khôi phục chính xác).

---

## 5. LỖ HỔNG KINH ĐIỂN: TẤN CÔNG NGƯỜI ĐỨNG GIỮA (MAN-IN-THE-MIDDLE - MITM) & GIẢI PHÁP

Dù các hệ mã công khai (RSA, Diffie-Hellman, ElGamal) có độ an toàn toán học rất cao, chúng đều có chung một điểm yếu chết người: **Tính xác thực của khóa công khai (Public Key Authenticity)**.

```
       Alice                        Eve (Kẻ tấn công)                     Bob
 ------------------               ---------------------             ------------------
 (eA, dA)                         (eE, dE)                          (eB, dB)

 Gửi eA --------->                Chặn eA, thay bằng eE -----------> Nhận eE (tưởng của Alice)
                   <---------     Chặn eB, thay bằng eE <----------- Gửi eB
 Nhận eE (tưởng của Bob)

 Mã hóa:                          Giải mã bằng dE:                  Mã hóa bằng eE:
 c = m^eE -------->               m = c^dE                          c' = m^eE
                                  (Eve đọc trọn thông điệp!)
                                  Mã hóa lại bằng eA:
                   <---------     c'' = m^eA
 Nhận c'', giải mã:
 m = (c'')^dA
 (Alice tưởng nhận từ Bob!)
```

### Bản chất cuộc tấn công
- Kẻ tấn công Eve đứng trên đường truyền giữa Alice và Bob.
- Khi Alice gửi khóa công khai $e_A$ cho Bob, Eve chặn lại và tráo bằng khóa công khai $e_E$ của chính Eve.
- Tương tự, khi Bob gửi khóa công khai $e_B$, Eve cũng chặn lại và gửi $e_E$ cho Alice.
- Kết quả: Alice và Bob đều đang mã hóa thông tin bằng khóa công khai của Eve! Eve dễ dàng giải mã bằng khóa cá nhân $d_E$ của mình để xem trộm toàn bộ nội dung, sau đó mã hóa lại gửi cho bên còn lại mà hai bên không hề hay biết.

### Giải pháp khắc phục
1. **Chữ ký số (Digital Signatures)**: Dùng khóa riêng để ký lên thông điệp, chứng thực người gửi.
2. **Cơ sở hạ tầng khóa công khai (PKI - Public Key Infrastructure)**:
   - Sử dụng một bên thứ ba đáng tin cậy gọi là **Nhà cung cấp chứng chỉ số (Certificate Authority - CA)**.
   - CA ký xác nhận số vào một chứng chỉ (Digital Certificate theo chuẩn X.509), gắn chặt danh tính của người sở hữu (Alice) với khóa công khai $e_A$ của người đó.
   - Khi nhận khóa công khai, Bob chỉ cần kiểm tra chữ ký của CA trên chứng chỉ để đảm bảo khóa đó thực sự là của Alice chứ không phải của kẻ mạo danh Eve.

---

## 6. BẢNG SO SÁNH TỔNG HỢP & ĐÚC KẾT ÔN THI

### Bảng so sánh 3 hệ thống mật mã công khai cốt lõi

| Tiêu chí so sánh | RSA | Diffie – Hellman | ElGamal |
| :--- | :--- | :--- | :--- |
| **Năm công bố** | 1977 | 1976 | 1985 |
| **Bài toán khó nền tảng** | Phân tích số nguyên ra thừa số nguyên tố (**IFP**) | Logarit rời rạc (**DLP**) | Logarit rời rạc (**DLP**) |
| **Không gian tính toán** | Vành $\mathbb{Z}_n$ với $n = pq$ | Nhóm nhân $\mathbb{Z}_p^*$ ($p$ nguyên tố) | Nhóm nhân $\mathbb{Z}_p^*$ ($p$ nguyên tố) |
| **Mục đích chính** | Mã hóa dữ liệu & Ký số | Thỏa thuận / Trao đổi khóa bí mật | Mã hóa dữ liệu & Ký số |
| **Tính xác định / ngẫu nhiên** | Xác định (Deterministic - Cùng $M$ ra cùng $C$) | Không áp dụng trực tiếp | Xác suất (Probabilistic - Cùng $M$ ra khác $C$) |
| **Kích thước bản mã** | Bằng kích thước khối bản rõ ($|c| = |n|$) | Trao đổi khóa ($k_A, k_B$) | Gấp đôi kích thước khối ($C_1, C_2$) |
| **Tối ưu hóa hiệu năng** | Giải mã nhanh bằng CRT (~gấp 4 lần) | Chọn số mũ nhỏ/Elliptic Curve (ECDH) | Tái sử dụng bảng nhân lũy thừa |
| **Lỗ hổng phổ biến** | Phân tích $n$ nếu $p, q$ quá gần nhau, tấn công MITM | Tấn công Man-in-the-Middle (MITM), Index-Calculus | Tấn công MITM, lộ số ngẫu nhiên $k$ |

---

### Tóm tắt các công thức then chốt cần ghi nhớ khi làm bài thi

1. **RSA**:
   - $n = pq$, $\varphi(n) = (p - 1)(q - 1)$.
   - $e \cdot d \equiv 1 \pmod{\varphi(n)}$.
   - Mã hóa: $c = m^e \pmod n$.
   - Giải mã: $m = c^d \pmod n$.
   - Giải mã nhanh CRT: $d_1 = d \pmod{p-1}$, $d_2 = d \pmod{q-1}$, $a_1 = c^{d_1} \pmod p$, $a_2 = c^{d_2} \pmod q$.
2. **Diffie – Hellman**:
   - Tham số chung: $p, g$.
   - Khóa công khai: $k_A = g^x \pmod p$, $k_B = g^y \pmod p$.
   - Khóa chung: $K = (k_B)^x = (k_A)^y = g^{xy} \pmod p$.
3. **ElGamal**:
   - Khóa: Public $(p, g, h = g^x \pmod p)$, Private $x$.
   - Mã hóa: $C_1 = g^k \pmod p$, $C_2 = M \cdot h^k \pmod p$.
   - Giải mã: $M = C_2 \cdot (C_1^x)^{-1} \pmod p$.
4. **Logarit rời rạc & Index-Calculus**:
   - $\log_g(ab) \equiv \log_g(a) + \log_g(b) \pmod{p - 1}$.
   - $\log_g(a^k) \equiv k \log_g(a) \pmod{p - 1}$.
