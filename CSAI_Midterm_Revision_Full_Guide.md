# BÍ KÍP ÔN THI GIỮA KỲ TOÀN DIỆN: CƠ SỞ TRÍ TUỆ NHÂN TẠO (CSAI)
**Trường Đại học Khoa học Tự nhiên - ĐHQG TP.HCM (HCMUS - FIT)**  
**Giảng viên:** ThS. Bùi Duy Đăng (`bddang@fit.hcmus.edu.vn`)  
**Hình thức thi:** Closed-book (Thi đóng - KHÔNG được sử dụng tài liệu)  
**Phạm vi ôn thi:** Từ Bài 1 đến Bài 5 (đến hết *Adversarial Search / Game Playing*)  

---

## MỤC LỤC TỔNG QUÁT
1. [THÔNG TIN KỲ THI & CHIẾN LƯỢC ÔN TẬP ĐẠT ĐIỂM TỐI ĐA](#1-thông-tin-kỳ-thi--chiến-lược-ôn-tập-đạt-điểm-tối-đa)
2. [CHƯƠNG 1: TỔNG QUAN VỀ TRÍ TUỆ NHÂN TẠO (INTRODUCTION TO AI)](#2-chương-1-tổng-quan-về-trí-tuệ-nhân-tạo-introduction-to-ai)
3. [CHƯƠNG 2: TÁC TỬ THÔNG MINH (INTELLIGENT AGENTS)](#3-chương-2-tác-tử-thông-minh-intelligent-agents)
   - *Phần bài tập & Quiz giải chi tiết:* Quiz 01 (PEAS Tennis match vs Practice against wall), Quiz 02 (Environment Properties), Quiz 03 (Learning Agent)
4. [CHƯƠNG 3 - PHẦN 1: GIẢI QUYẾT VẤN ĐỀ BẰNG TÌM KIẾM (PROBLEM SOLVING BY SEARCHING)](#4-chương-3---phần-1-giải-quyết-vấn-đề-bằng-tìm-kiếm-problem-solving-by-searching)
   - *Phần bài tập & Quiz giải chi tiết:* Quiz 01 & 02 (Hình thức hóa & Vẽ cây tìm kiếm Tháp Hà Nội)
5. [CHƯƠNG 3 - PHẦN 2: TÌM KIẾM MÙ / KHÔNG CÓ THÔNG TIN (UNINFORMED SEARCH STRATEGIES)](#5-chương-3---phần-2-tìm-kiếm-mù--không-có-thông-tin-uninformed-search-strategies)
   - *Phần bài tập & Quiz giải chi tiết:* Quiz 01 (BFS Graph Search), Quiz 02 (Uniform-Cost Search), Quiz 03 (DFS Graph Search) trên đồ thị mẫu có bảng trace từng bước
6. [CHƯƠNG 3 - PHẦN 3: TÌM KIẾM CÓ THÔNG TIN / HEURISTIC (INFORMED SEARCH STRATEGIES)](#6-chương-3---phần-3-tìm-kiếm-có-thông-tin--heuristic-informed-search-strategies)
   - *Phần bài tập & Ví dụ giải chi tiết:* Greedy Best-First Search & A* Search trên đồ thị mẫu, Phân tích tính Admissible & Consistent, Bài toán 8-puzzle
7. [CHƯƠNG 4: TÌM KIẾM CỤC BỘ VÀ BÀI TOÁN TỐI ƯU (LOCAL SEARCH & OPTIMIZATION PROBLEMS)](#7-chương-4-tìm-kiếm-cục-bộ-và-bài-toán-tối-ưu-local-search--optimization-problems)
   - *Phần bài tập & Quiz giải chi tiết:* Quiz 01 (4-queens Hill-Climbing qua từng Step), Quiz 02 (Tính Fitness & Xác suất chọn lọc Roulette Wheel trong Genetic Algorithm)
8. [CHƯƠNG 5: TÌM KIẾM ĐỐI KHÁNG VÀ TRÒ CHƠI (ADVERSARIAL SEARCH)](#8-chương-5-tìm-kiếm-đối-kháng-và-trò-chơi-adversarial-search)
   - *Phần bài tập & Ví dụ giải chi tiết:* Bài toán Minimax 2-ply, Cắt tỉa Alpha-Beta từng bước với cửa sổ [alpha, beta], Expectiminimax với nút Chance
9. [BẢNG TRA CỨU ĐỘ PHỨC TẠP VÀ TÍNH CHẤT CÁC THUẬT TOÁN TÌM KIẾM](#9-bảng-tra-cứu-độ-phức-tạp-và-tính-chất-các-thuật-toán-tìm-kiếm)
10. [NGÂN HÀNG CÂU HỎI TRẮC NGHIỆM VÀ TỰ LUẬN ÔN THI TRỌNG TÂM CÓ ĐÁP ÁN](#10-ngân-hàng-câu-hỏi-trắc-nghiệm-và-tự-luận-ôn-thi-trọng-tâm-có-đáp-án)

---

## 1. THÔNG TIN KỲ THI & CHIẾN LƯỢC ÔN TẬP ĐẠT ĐIỂM TỐI ĐA

### 1.1. Thông báo chính thức từ Giảng viên
> **Thông báo:**
> - **Ngày thi:** Thứ Ba, ngày 27/10
> - **Giờ thi:** Bắt đầu lúc **13:15** (Sinh viên bắt buộc phải có mặt trước 15 phút, tức 13:00, và mang theo giấy tờ tùy thân: Thẻ sinh viên hoặc CCCD).
> - **Hình thức thi:** **CLOSED-BOOK (Thi đóng)** – Tuyệt đối không sử dụng tài liệu. Bất kỳ hành vi gian lận nào sẽ bị 0 điểm toàn môn và chuyển lên Ban Chủ nhiệm Khoa xử lý kỷ luật.
> - **Phạm vi trọng tâm:** Bao gồm (nhưng không giới hạn ở) các bài học mới nhất đến hết **Adversarial Search** (Tìm kiếm đối kháng / Game Playing).

### 1.2. Phân tích cấu trúc đề thi dự kiến & Bẫy thường gặp
Đề thi giữa kỳ môn Cơ sở Trí tuệ Nhân tạo (CSAI) của FIT - HCMUS thường kết hợp giữa **Trắc nghiệm hiểu sâu bản chất lý thuyết** và **Tự luận / Bài tập tính toán từng bước**:
1. **Lý thuyết nền tảng (khoảng 30% - 40%):**
   - 4 định nghĩa AI & Bài kiểm tra Turing (Turing Test, Total Turing Test, CAPTCHA).
   - Mô tả môi trường theo PEAS và nhận diện 7-8 đặc trưng của môi trường nhiệm vụ.
   - 5 kiến trúc tác tử (đặc biệt là sự khác nhau giữa Goal-based và Utility-based, 4 thành phần của Learning agent).
   - Phân biệt Tree-Search vs Graph-Search (vấn đề chu trình lặp, tập `explored`, thời điểm kiểm tra đích).
   - Điều kiện tối ưu của A* (Admissibility cho Tree-search, Consistency cho Graph-search).
   - Cảnh quan tìm kiếm cục bộ (Local maxima, Ridges, Plateau) và công thức luyện kim $P = e^{\Delta E / T}$.
2. **Bài tập thuật toán & Bảng trace từng bước (khoảng 60% - 70%):**
   - **Vẽ cây tìm kiếm / Bảng trạng thái:** Bài toán Tháp Hà Nội (Towers of Hanoi), Robot hút bụi, 8-queens.
   - **Trace thuật toán tìm kiếm mù:** BFS, UCS, DFS trên đồ thị cho trước (lưu ý thứ tự mở rộng, danh sách Frontier, Explored, giải quyết hòa tie-breaking theo bảng chữ cái).
   - **Trace thuật toán Heuristic:** Greedy Best-First Search và A* Search (tính giá trị $f = g + h$, theo dõi việc cập nhật chi phí thấp hơn trong Frontier).
   - **Tìm kiếm cục bộ & Thuật giải di truyền (GA):** Tính số cặp hậu tấn công/không tấn công trong $n$-queens, tính hàm thích nghi $Fit(n)$, tính xác suất chọn lọc bánh xe Roulette $P(i) = Fit(i) / \sum Fit$.
   - **Minimax & Cắt tỉa Alpha-Beta:** Điền giá trị Minimax ngược từ lá lên gốc, xác định chính xác các nhánh bị cắt tỉa $\alpha$-cutoff và $\beta$-cutoff, ghi rõ giá trị $[\alpha, \beta]$ tại mỗi nút.
---

## 2. CHƯƠNG 1: TỔNG QUAN VỀ TRÍ TUỆ NHÂN TẠO (INTRODUCTION TO AI)

### 2.1. Trí tuệ (Intelligence) và Trí tuệ Nhân tạo (AI)
- **Trí tuệ tự nhiên (Intelligence):** Bao gồm năng lực tư duy logic, thấu hiểu, học hỏi, suy diễn lập luận, sáng tạo, giải quyết vấn đề và thích nghi với hoàn cảnh mới.
- **Trí tuệ nhân tạo (Artificial Intelligence - AI):** Ngành khoa học và kỹ thuật không chỉ nỗ lực tìm hiểu bản chất của trí tuệ mà còn chế tạo các thực thể thông minh (intelligent entities) có khả năng:
  + **Tư duy (Thinking):** Học tập, lập kế hoạch, suy diễn và tinh chỉnh tri thức.
  + **Tri giác (Perception):** Nhìn (Thị giác máy tính), nghe (Xử lý âm thanh/tiếng nói), cảm nhận xúc giác.
  + **Hành động (Action/Manipulation):** Điều khiển cơ cấu chấp hành, di chuyển và thao tác trên vật thể (Robotics).
  + **Giao tiếp (Communication):** Tương tác tự nhiên bằng ngôn ngữ con người (Xử lý ngôn ngữ tự nhiên - NLP).

### 2.2. Bốn góc nhìn / Định nghĩa về AI (The Four Categories of AI)
Các nhà nghiên cứu chia định nghĩa AI theo hai chiều kích: **Con người vs Tính duy lý** và **Tư duy vs Hành vi**:

| Góc nhìn | Tập trung vào CON NGƯỜI (Human-centered) | Tập trung vào TÍNH DUY LÝ (Rationality) |
| :--- | :--- | :--- |
| **Quy trình suy nghĩ (Thought processes & Reasoning)** | **Hệ thống suy nghĩ như con người** *(Systems that think like humans)*<br>- Tiếp cận Khoa học Nhận thức (Cognitive Science).<br>- Tìm hiểu cơ chế hoạt động của não bộ con người thông qua thực nghiệm tâm lý học hoặc quét não (fMRI), sau đó mô phỏng lại trên máy tính. | **Hệ thống suy nghĩ duy lý** *(Systems that think rationally)*<br>- Tiếp cận theo "Quy luật tư duy" (Laws of Thought).<br>- Dựa trên nền tảng Logic học hình thức (Aristotle, Logic vị từ, suy diễn tam đoạn luận).<br>- Đảm bảo các kết luận rút ra luôn đúng đắn và chặt chẽ nếu tiền đề đúng. |
| **Hành vi (Behavior)** | **Hệ thống hành động như con người** *(Systems that act like humans)*<br>- Tiêu biểu là **Bài kiểm tra Turing** (Turing Test).<br>- Mục tiêu: Hành vi bên ngoài của hệ thống không thể phân biệt được với hành vi của con người. | **Hệ thống hành động duy lý** *(Systems that act rationally)*<br>- Tiếp cận theo **Tác tử duy lý** (Rational Agent Approach).<br>- Tác tử hành động để đạt được kết quả kỳ vọng tốt nhất dựa trên mục tiêu và thông tin cảm nhận được.<br>- **Đây là cách tiếp cận trọng tâm của môn học CSAI và toàn bộ giáo trình hiện đại!** |

> **Bản chất của Tác tử duy lý (Rational Agent Approach):**
> - Hành động duy lý bao hàm cả suy nghĩ duy lý (suy diễn logic để ra quyết định đúng), nhưng rộng hơn: trong nhiều tình huống không thể suy diễn chắc chắn (môi trường bất định, thiếu thời gian), tác tử vẫn phải hành động để tối ưu hóa kết quả kỳ vọng (ví dụ: né phản xạ khi chạm vào vật nóng mà không cần chờ não suy luận).
> - Chuẩn mực duy lý có tính toán học, rõ ràng và tổng quát hơn nhiều so với việc bắt chước những hành vi đôi khi cảm tính, sai lầm của con người.

---

### 2.3. Bài kiểm tra Turing (Turing Test - Alan Turing, 1950)
- **Kịch bản gốc (Imitation Game):** Một người thẩm vấn (Interrogator) đặt câu hỏi bằng văn bản cho hai đối tượng ở phòng kín: một con người và một máy tính. Nếu người thẩm vấn không thể phân biệt được câu trả lời nào đến từ con người, câu trả lời nào đến từ máy tính thì máy tính đó **vượt qua bài kiểm tra Turing**.
- **Các năng lực AI cần có để vượt qua Turing Test:**
  1. *Natural Language Processing (NLP):* Giao tiếp trôi chảy bằng ngôn ngữ tự nhiên.
  2. *Knowledge Representation:* Lưu trữ những tri thức mà nó biết hoặc nghe được.
  3. *Automated Reasoning:* Sử dụng tri thức đã lưu để trả lời câu hỏi và rút ra kết luận mới.
  4. *Machine Learning:* Thích nghi với hoàn cảnh mới, phát hiện và ngoại suy các quy luật từ dữ liệu.
- **Biến thể của Turing Test:**
  + **Total Turing Test (Bài kiểm tra Turing toàn diện):** Bổ sung thêm tín hiệu hình ảnh và thao tác vật lý. Yêu cầu thêm 2 năng lực:
    5. *Computer Vision:* Nhận diện và tri giác thế giới thực qua hình ảnh/video.
    6. *Robotics:* Di chuyển và tương tác vật lý với đồ vật xung quanh.
  + **Reverse Turing Test (Bài kiểm tra Turing đảo ngược):** Hệ thống máy tính đóng vai trò người thẩm vấn để kiểm tra xem đối tượng tương tác là người hay máy (ví dụ điển hình: mã **CAPTCHA** trên các trang web).
- **Hạn chế của Turing Test:**
  + Chỉ kiểm tra hành vi bắt chước bên ngoài (human imitation), không kiểm tra trí tuệ thực chất hay tính duy lý.
  + Đôi khi máy tính phải "giả vờ ngốc nghếch" hoặc "giả vờ gõ chậm, tính toán sai" để giống con người, điều này đi ngược lại mục tiêu chế tạo hệ thống thông minh hữu ích.
  + Giới nghiên cứu AI hiện đại tập trung vào việc nghiên cứu các nguyên lý cốt lõi của tính duy lý thay vì cố gắng đánh lừa bài kiểm tra Turing.

---

### 2.4. Các ngành khoa học nền tảng của AI (Foundations of AI)
AI không hình thành đơn độc mà kế thừa thành tựu từ nhiều lĩnh vực:
1. **Triết học (Philosophy):** Các quy luật logic, phương pháp suy luận, lý thuyết nhận thức, mối quan hệ giữa thể xác và tâm trí (mind as a physical system), nền tảng của sự học và tính duy lý.
2. **Toán học (Mathematics):**
   - Biểu diễn hình thức và chứng minh logic (Formal logic).
   - Lý thuyết thuật toán, độ phức tạp tính toán (NP-completeness, bài toán giải được vs không giải được).
   - Lý thuyết xác suất và thống kê (xử lý tri thức không chắc chắn, học máy).
3. **Kinh tế học (Economics):** Lý thuyết độ lợi (Utility theory), lý thuyết ra quyết định (Decision theory), lý thuyết trò chơi (Game theory) trong môi trường đa tác tử, hành vi tối ưu hóa lợi ích kinh tế.
4. **Khoa học thần kinh (Neuroscience):** Cấu tạo và hoạt động của mạng lưới nơ-ron sinh học, cơ chế xử lý tín hiệu điện tử trong não bộ -> Khởi nguồn cho Mạng nơ-ron nhân tạo (Artificial Neural Networks).
5. **Tâm lý học & Khoa học nhận thức (Psychology & Cognitive Science):** Cách con người tri giác, xử lý thông tin, lưu trữ tri thức và đưa ra quyết định hành vi.
6. **Kỹ thuật máy tính (Computer Engineering):** Cung cấp phần cứng tốc độ cao (CPU, GPU, TPU), bộ nhớ lớn để triển khai các thuật toán AI quy mô lớn.
7. **Lý thuyết điều khiển & Điều khiển học (Control Theory & Cybernetics):** Thiết kế các hệ thống hồi tiếp tự điều chỉnh để tối ưu hóa hàm mục tiêu theo thời gian.
8. **Ngôn ngữ học (Linguistics):** Ngữ pháp hình thức, cấu trúc ngôn ngữ, biểu diễn ngữ nghĩa trong ngôn ngữ tự nhiên.

---

### 2.5. Tóm tắt các mốc lịch sử quan trọng của AI
- **1943:** Warren McCulloch & Walter Pitts đề xuất mô hình mạch logic boolean mô phỏng nơ-ron não bộ (mô hình nơ-ron đầu tiên).
- **1950:** Alan Turing xuất bản bài báo kinh điển *"Computing Machinery and Intelligence"*, giới thiệu bài kiểm tra Turing Test, khái niệm học máy, thuật toán di truyền.
- **1956:** **Hội thảo Dartmouth (Dartmouth Summer Research Project on AI):** Thuật ngữ **"Artificial Intelligence"** chính thức ra đời do John McCarthy đề xuất, cùng sự tham gia của các nhà tiên phong: Marvin Minsky, Claude Shannon, Allen Newell, Herbert Simon, Arthur Samuel.
- **1950s - 1960s:** Thời kỳ hưng thịnh ban đầu ("Look, Ma, no hands!"). Các chương trình chơi cờ đam tự học của Samuel, Logic Theorist, Geometry Engine. Năm 1965, Robinson phát minh thuật toán phân giải (Resolution algorithm) cho logic vị từ bậc một.
- **1970 - 1990:** Kỷ nguyên tiếp cận dựa trên tri thức (Knowledge-based approaches) và Hệ chuyên gia (Expert Systems như MYCIN, DENDRAL).
- **1988 - 1993:** **"Mùa đông AI" (AI Winter):** Các hệ chuyên gia bộc lộ điểm yếu (cứng nhắc, chi phí duy trì đắt đỏ, khó mở rộng), nguồn tài trợ bị cắt giảm.
- **1990 - nay:** Tiếp cận theo xác suất và học máy thống kê.
- **Các cột mốc vang dội:**
  + **1997:** Siêu máy tính **Deep Blue** của IBM đánh bại nhà vô địch cờ vua thế giới Garry Kasparov.
  + **2016:** **AlphaGo** của Google DeepMind đánh bại Lee Sedol với tỉ số 4-1 trong môn cờ Vây.
  + **2019:** **OpenAI Five** đánh bại nhà vô địch thế giới bộ môn Dota 2.
  + **2020s:** Kỷ nguyên của các Mô hình Ngôn ngữ Lớn (LLMs - GPT-4, Gemini) và AI tạo sinh.
---

## 3. CHƯƠNG 2: TÁC TỬ THÔNG MINH (INTELLIGENT AGENTS)

### 3.1. Các khái niệm cốt lõi về Tác tử (Agents)
- **Tác tử (Agent):** Bất cứ thực thể nào có khả năng **tri giác (perceiving)** môi trường xung quanh thông qua các **cảm biến (sensors)** và **hành động (acting)** tác động lên môi trường đó thông qua các **cơ cấu chấp hành / bộ kích hoạt (actuators)**.
  + *Ví dụ con người:* Cảm biến là mắt, tai, mũi, da; Cơ cấu chấp hành là tay, chân, thanh quản.
  + *Ví dụ tác tử phần mềm (Software agent):* Cảm biến là nhận chuỗi phím gõ, gói tin mạng, tập tin; Cơ cấu chấp hành là xuất ra màn hình, ghi dữ liệu đĩa, gửi gói tin.
- **Chuỗi cảm nhận (Percept Sequence):** Toàn bộ lịch sử các thông tin mà tác tử đã cảm nhận được từ trước đến thời điểm hiện tại.
- **Hàm tác tử (Agent Function):** Ánh xạ trừu tượng từ mọi chuỗi cảm nhận có thể có vào một hành động tương ứng:
  $$f: P^* \to A$$
  *(Trong đó $P^*$ là tập hợp tất cả các chuỗi cảm nhận, $A$ là tập hợp hành động).*
- **Chương trình tác tử (Agent Program):** Sự hiện thực hóa cụ thể của hàm tác tử chạy trên một kiến trúc phần cứng xác định:
  $$\text{Agent} = \text{Architecture} + \text{Program}$$
  *(Kiến trúc cung cấp cảm biến, cơ cấu chấp hành và năng lực tính toán; Chương trình tác tử thực thi thuật toán để chọn hành động).*

---

### 3.2. Tính Duy Lý (Rationality) vs Toàn Tri (Omniscience)
- **Định nghĩa Tác tử duy lý (Rational Agent):** Tác tử luôn chọn hành động nhằm **tối đa hóa giá trị kỳ vọng của thước đo hiệu quả (expected performance measure)**, dựa trên:
  1. **Thước đo hiệu quả (Performance Measure):** Tiêu chuẩn khách quan đánh giá mức độ thành công của hành vi tác tử.
  2. **Tri thức ban đầu (Prior Knowledge):** Hiểu biết sẵn có về môi trường được nạp vào lúc khởi tạo.
  3. **Chuỗi cảm nhận tích lũy (Percept Sequence):** Những gì tác tử đã quan sát được từ đầu đến nay.
  4. **Các hành động khả thi (Possible Actions):** Tập hợp hành động mà tác tử có thể thực hiện.
- **Phân biệt Duy lý (Rationality) vs Toàn tri (Omniscience):**
  + *Tác tử toàn tri (Omniscient):* Biết trước kết quả **thực tế tuyệt đối** của mọi hành động và hành động tương ứng (cần có khả năng tiên tri - điều bất khả thi trong thế giới thực).
  + *Tác tử duy lý (Rational):* Chỉ tối đa hóa **kết quả kỳ vọng (expected success)** dựa trên những gì nó biết. Hành vi duy lý không đòi hỏi phải biết trước tương lai hay không bao giờ thất bại (ví dụ: nhìn hai phía trước khi qua đường là duy lý, dù bất ngờ có thiên thạch rơi trúng).
- **Tính tự chủ (Autonomy):**
  + Tác tử có tính tự chủ nếu hành vi của nó được quyết định chủ yếu bởi **kinh nghiệm học hỏi của chính nó** (thông qua tri giác), thay vì chỉ phụ thuộc vào tri thức ban đầu do lập trình viên cài đặt cứng.
  + Tác tử thực sự duy lý bắt buộc phải có năng lực **Học hỏi (Learning)** và **Khám phá (Exploration)** để bổ sung và sửa chữa các hiểu biết ban đầu khi môi trường thay đổi.

---

### 3.3. Mô hình Môi trường Nhiệm vụ PEAS (PEAS Framework)
Khi thiết kế một tác tử thông minh, bước đầu tiên và quan trọng nhất là xác định đầy đủ 4 thành phần **PEAS**:
- **P - Performance Measure:** Thước đo hiệu quả (Độ an toàn, tốc độ, tiết kiệm năng lượng, điểm số, mức độ hài lòng,...).
- **E - Environment:** Môi trường hoạt động (Đường xá, thời tiết, bệnh nhân, người chơi đối kháng, bàn cờ,...).
- **A - Actuators:** Bộ cơ cấu chấp hành (Vô lăng, bàn đạp ga, cánh tay robot, màn hình hiển thị, cơ chế điều khiển,...).
- **S - Sensors:** Cảm biến (Camera, radar, cảm biến siêu âm, bàn phím, GPS, đồng hồ tốc độ,...).

#### Bảng ví dụ PEAS kinh điển trong bài học:
| Loại Tác tử | Performance Measure (P) | Environment (E) | Actuators (A) | Sensors (S) |
| :--- | :--- | :--- | :--- | :--- |
| **Tài xế taxi tự hành** *(Automated Taxi)* | An toàn, nhanh chóng, đúng luật, tối đa lợi nhuận, êm ái cho khách | Đường phố, các xe khác, người đi bộ, biển báo, thời tiết | Vô lăng, chân ga, chân phanh, còi, xi nhan, màn hình | Camera, Radar, Lidar, GPS, cảm biến tốc độ, cảm biến động cơ |
| **Hệ thống chẩn đoán y tế** *(Medical Diagnosis)* | Bệnh nhân khỏe mạnh, giảm chi phí, giảm thiểu chẩn đoán sai | Bệnh nhân, bệnh viện, nhân viên y tế | Hiển thị câu hỏi chẩn đoán, toa thuốc, phác đồ điều trị | Bàn phím nhập triệu chứng bệnh nhân, kết quả xét nghiệm |
| **Robot dọn vệ sinh** *(Vacuum-Cleaner)* | Độ sạch của sàn, thời gian dọn, mức tiêu thụ pin, tránh va chạm | Sàn nhà, phòng ốc, bụi bẩn, chướng ngại vật | Bánh xe di chuyển, chổi quét, động cơ hút bụi | Cảm biến bụi, cảm biến va chạm, cảm biến nhận diện phòng/vị trí |

---

### 3.4. Bảy đặc trưng của Môi trường Nhiệm vụ (Task Environment Properties)
Một môi trường nhiệm vụ được phân loại theo 7 chiều không gian cốt lõi (xác định phương pháp thuật toán phù hợp):

1. **Quan sát toàn phần (Fully Observable) vs. Quan sát một phần (Partially Observable):**
   - *Fully observable:* Cảm biến của tác tử thu nhận được **toàn bộ trạng thái thế giới** ở mỗi thời điểm cần ra quyết định (Ví dụ: Cờ vua). Tác tử không cần duy trì bộ nhớ trạng thái bên trong.
   - *Partially observable:* Cảm biến bị hạn chế, nhiễu hoặc có vùng khuất (Ví dụ: Lái xe ngoài đường có góc khuất, chơi Poker không thấy bài đối thủ). Tác tử phải lưu vết trạng thái nội tại (Internal state).
2. **Đơn tác tử (Single-Agent) vs. Đa tác tử (Multiagent):**
   - *Single-agent:* Chỉ có một tác tử tự hoạt động trong môi trường (Ví dụ: Chơi giải đố xếp hình Crossword, Robot hút bụi một mình).
   - *Multiagent:* Môi trường có các tác tử khác cùng hoạt động. Chia thành:
     + *Cạnh tranh (Competitive):* Tổng lợi ích triệt tiêu nhau, ví dụ cờ vua (Zero-sum game).
     + *Hợp tác (Cooperative):* Cùng phối hợp để đạt mục tiêu chung (Ví dụ: Hai xe tự hành tránh va chạm nhau).
3. **Xác định (Deterministic) vs. Ngẫu nhiên / Bất định (Stochastic):**
   - *Deterministic:* Trạng thái tiếp theo của môi trường hoàn toàn được xác định bởi **trạng thái hiện tại** và **hành động của tác tử** (Ví dụ: Bàn cờ vua, game 8-puzzle).
   - *Stochastic:* Trạng thái tiếp theo có yếu tố ngẫu nhiên, không chắc chắn (Ví dụ: Đổ xúc xắc trong Backgammon, điều khiển xe bị trượt bánh khi trời mưa).
4. **Theo từng tập đoạn (Episodic) vs. Tuần tự (Sequential):**
   - *Episodic:* Trải nghiệm của tác tử chia thành các tập đoạn riêng rẽ. Ở mỗi tập đoạn, tác tử nhận cảm nhận và chọn duy nhất một hành động. Chất lượng hành động chỉ phụ thuộc vào chính tập đoạn đó, **không ảnh hưởng đến các tập đoạn tương lai** (Ví dụ: Robot phân loại sản phẩm lỗi trên băng chuyền). Không cần suy tính đường dài.
   - *Sequential:* Quyết định ở hiện tại **sẽ ảnh hưởng trực tiếp đến tất cả các quyết định và trạng thái trong tương lai** (Ví dụ: Chơi cờ, lái xe). Bắt buộc phải suy nghĩ nhìn xa (look-ahead, planning).
5. **Tĩnh (Static) vs. Động (Dynamic):**
   - *Static:* Môi trường không đổi trong khi tác tử đang suy nghĩ ra quyết định (Ví dụ: Bàn cờ khi chưa hết thời gian).
   - *Dynamic:* Môi trường liên tục biến đổi ngay trong lúc tác tử đang tính toán (Ví dụ: Lái xe trên đường, chơi bóng bàn).
   - *Semidynamic:* Môi trường không đổi, nhưng điểm số hiệu quả của tác tử giảm dần theo thời gian suy nghĩ (Ví dụ: Cờ vua có đồng hồ bấm giờ).
6. **Rời rạc (Discrete) vs. Liên tục (Continuous):**
   - *Discrete:* Số lượng trạng thái, thời gian, cảm nhận và hành động là hữu hạn hoặc đếm được (Ví dụ: 64 ô cờ vua, từng lượt đi).
   - *Continuous:* Trạng thái, thời gian và hành động thay đổi liên tục theo thời gian thực (Ví dụ: Tọa độ, góc quay vô lăng, tốc độ xe).
7. **Đã biết (Known) vs. Chưa biết (Unknown):**
   - Phản ánh mức độ hiểu biết của tác tử/nhà thiết kế về "luật chơi" (quy luật vật lý của môi trường). Nếu unknown, tác tử phải học để hiểu luật.

> **Đúc kết quan trọng:** Môi trường khó khăn nhất cho tác tử là: **Partially observable, Multiagent, Stochastic, Sequential, Dynamic, Continuous, Unknown** (Ví dụ tiêu biểu: Lái xe tự hành trong đời thực).

---

### 3.5. Năm Kiến trúc Chương trình Tác tử (Agent Architectures)

```
                       +-----------------------------+
                       |       Learning Agent        |
                       +-----------------------------+
                                      |
         +----------------------------+----------------------------+
         |                                                         |
+-------------------+                                     +-------------------+
| Reflex-based      |                                     | Reasoning-based   |
+-------------------+                                     +-------------------+
  |               |                                         |               |
  v               v                                         v               v
Simple          Model-based                               Goal-based      Utility-based
Reflex Agent    Reflex Agent                              Agent           Agent
```

#### 1. Tác tử phản xạ đơn giản (Simple Reflex Agent)
- **Cơ chế:** Chọn hành động chỉ dựa vào cảm nhận tức thời ở hiện tại, thông qua tập **luật Điều kiện - Hành động (Condition-Action Rules)**:
  $$\text{if } \text{status} == \text{Dirty then } \text{action} = \text{Suck}$$
- **Ưu điểm:** Cực kỳ đơn giản, tốc độ phản ứng tức thì.
- **Nhược điểm & Bẫy thi:**
  + Chỉ hoạt động đúng nếu môi trường là **Quan sát toàn phần (Fully observable)**.
  + Nếu môi trường quan sát một phần, tác tử dễ rơi vào **vòng lặp vô tận (infinite loops)** do không phân biệt được các trạng thái có cùng cảm nhận bên ngoài. (Cách khắc phục một phần: Thêm yếu tố ngẫu nhiên - Randomization).

#### 2. Tác tử phản xạ dựa trên mô hình (Model-Based Reflex Agent)
- **Cơ chế:** Duy trì một **trạng thái nội tại (Internal State)** để lưu vết những phần của thế giới mà cảm biến hiện tại không nhìn thấy được.
- **Cần 2 loại tri thức về thế giới (Model):**
  1. *Transition model:* Thế giới tiến hóa theo thời gian như thế nào độc lập với tác tử, và các hành động của tác tử làm thay đổi thế giới ra sao.
  2. *Sensor model:* Trạng thái của thế giới phản ánh lên cảm nhận của cảm biến như thế nào.
- **Ý nghĩa:** Giải quyết được bài toán môi trường quan sát một phần.

#### 3. Tác tử dựa trên mục tiêu (Goal-Based Agent)
- **Cơ chế:** Kết hợp thông tin trạng thái hiện tại với **thông tin Mục tiêu (Goal)** mô tả các trạng thái mong muốn đạt được.
- **Đặc điểm:** Tác tử sử dụng các giải thuật **Tìm kiếm (Search)** và **Lập kế hoạch (Planning)** để tìm chuỗi hành động dẫn tới mục tiêu.
- **So sánh với Reflex agent:** Kém linh hoạt hơn về thời gian tính toán (phải suy tính), nhưng linh hoạt hơn rất nhiều khi mục tiêu thay đổi (chỉ cần đổi định nghĩa Goal, không cần viết lại toàn bộ tập luật if-else).

#### 4. Tác tử dựa trên hàm độ lợi / hữu dụng (Utility-Based Agent)
- **Bản chất:** Mục tiêu (Goal) chỉ phân biệt nhị phân giữa "thành công" hay "thất bại". Trong thực tế, có nhiều con đường đạt mục tiêu, một số con đường an toàn hơn, nhanh hơn, ít tốn chi phí hơn.
- **Hàm độ lợi (Utility function):** Ánh xạ một trạng thái vào một số thực biểu thị "mức độ hài lòng" (Degree of happiness/success):
  $$U: S \to \mathbb{R}$$
- **Hai ưu thế vượt trội khi dùng Utility function:**
  1. *Khi có các mục tiêu mâu thuẫn nhau:* Hàm độ lợi giúp định lượng sự đánh đổi tối ưu (Trade-off) giữa các yếu tố (ví dụ: tốc độ cao vs mức độ an toàn).
  2. *Khi có sự bất định (Stochastic environment):* Cho phép tính toán và tối đa hóa **Độ lợi kỳ vọng (Expected Utility)**:
     $$\text{Action}^* = \arg\max_{a} \sum_{s'} P(s' | s, a) U(s')$$

#### 5. Tác tử học hỏi (Learning Agent)
Được cấu thành từ **bốn thành phần khái niệm (Four conceptual components)**:
1. **Phần tử thực thi (Performance Element):** Tác tử hiện tại đảm nhận việc tiếp nhận cảm nhận và chọn hành động tác động ra môi trường bên ngoài.
2. **Bộ phận phê bình (Critic):** Đánh giá mức độ hiệu quả của hành vi tác tử dựa trên một **thước đo hiệu quả cố định bên ngoài (Fixed performance standard)**. Truyền phản hồi (feedback: khen/chê, điểm phạt) cho phần tử học.
3. **Phần tử học (Learning Element):** Tiếp nhận phản hồi từ Critic và dữ liệu trải nghiệm để thực hiện cải tiến, điều chỉnh các luật hoặc mô hình bên trong Performance Element.
4. **Bộ phận tạo vấn đề (Problem Generator):** Đề xuất các hành động thử nghiệm mới (Exploration) mang tính khám phá và tạo ra trải nghiệm mới giàu thông tin, thay vì chỉ chăm chăm chọn hành động quen thuộc an toàn nhất (Exploitation).

---

### 3.6. GIẢI CHI TIẾT CÁC BÀI TẬP VÀ QUIZ TRONG LECTURE 02

#### Bài tập 1 (Quiz 01 - Slide 32): Mô tả PEAS cho 2 hoạt động quần vợt
Đề bài: Cho hai hoạt động sau, hãy xây dựng bảng mô tả PEAS chi tiết cho môi trường nhiệm vụ:
- **Hoạt động A:** Chơi một trận đấu quần vợt trong một giải đấu *(Playing a tennis match in a tournament)*.
- **Hoạt động B:** Tập đánh quần vợt vào bức tường *(Practicing tennis against a wall)*.

**Lời giải chi tiết:**

| Thành phần PEAS | Hoạt động A: Chơi trận đấu trong giải đấu | Hoạt động B: Tập đánh vào bức tường |
| :--- | :--- | :--- |
| **P (Performance Measure)** | - Giành chiến thắng trong trận đấu (tối đa số set, game, điểm).<br>- Giảm thiểu số lỗi đánh bóng hỏng (unforced errors).<br>- Tối ưu hóa thể lực, tránh chấn thương.<br>- Tuân thủ đúng luật thi đấu và quyết định của trọng tài. | - Số lần đánh bóng chạm tường liên tiếp thành công.<br>- Độ chính xác của điểm bóng rơi vào ô mục tiêu trên tường.<br>- Tốc độ và lực đánh bóng ổn định.<br>- Cải thiện cảm giác bóng và phản xạ. |
| **E (Environment)** | - Sân thi đấu chuẩn (mặt sân đất nện/cỏ/cứng).<br>- Lưới, bóng tennis, vạch kẻ sân.<br>- **Đối thủ con người (có chiến thuật, tâm lý đối kháng)**.<br>- Trọng tài, khán giả, điều kiện thời tiết (gió, ánh sáng). | - Bức tường tập phản xạ, mặt sân trước tường.<br>- Quả bóng tennis.<br>- Không có đối thủ đối kháng.<br>- Không có trọng tài, môi trường ít biến động hơn. |
| **A (Actuators)** | - Cánh tay cầm vợt (điều khiển góc vợt, lực vung, xoáy bóng).<br>- Đôi chân di chuyển (chạy, trượt, nhảy, đổi hướng).<br>- Thanh quản (giao tiếp, gọi bóng). | - Cánh tay điều khiển vợt (lực đánh, góc vợt).<br>- Đôi chân di chuyển định vị đón bóng dội lại từ tường. |
| **S (Sensors)** | - Mắt (theo dõi quỹ đạo bóng, vị trí và tư thế của đối thủ).<br>- Tai (nghe tiếng chạm bóng, tiếng còi trọng tài).<br>- Cảm giác cơ học/khớp (proprioception) cảm nhận lực tiếp xúc. | - Mắt (quan sát bóng bay đến tường và nảy ngược lại).<br>- Cảm giác lực của tay khi tiếp xúc bóng. |

---

#### Bài tập 2 (Quiz 02 - Slide 42): Phân tích đặc trưng môi trường cho 2 hoạt động
Đề bài: Xác định và giải thích 7 đặc trưng của môi trường nhiệm vụ cho Hoạt động A và Hoạt động B ở Quiz 01.

**Lời giải chi tiết và phân tích:**

| Đặc trưng | Hoạt động A: Trận đấu giải | Hoạt động B: Tập vào tường | Giải thích đối chiếu bản chất |
| :--- | :--- | :--- | :--- |
| **1. Quan sát** | **Partially Observable** | **Fully Observable** *(hoặc gần như Fully)* | Ở trận đấu giải, tác tử không thể quan sát được suy nghĩ, chiến thuật nội tâm của đối thủ, hay tình trạng thể lực ẩn. Ở bài tập tường, toàn bộ trạng thái bóng và khoảng cách tới tường đều nằm trong tầm nhìn. |
| **2. Số lượng tác tử** | **Multiagent (Competitive)** | **Single-Agent** | Hoạt động A có sự tham gia của đối thủ cạnh tranh triệt tiêu điểm số. Hoạt động B bức tường chỉ là một vật thể thụ động của môi trường, không phải tác tử có mục tiêu riêng. |
| **3. Tính xác định** | **Stochastic** | **Deterministic** *(hoặc xấp xỉ)* | Trận đấu có gió, độ nảy bóng khó lường và phản xạ không đoán trước của đối thủ $\implies$ Stochastic. Tập vào tường tuân theo định luật phản xạ vật lý gần như xác định. |
| **4. Tính tập đoạn** | **Sequential** | **Sequential** | Trong cả hai trường hợp, cú đánh ở hiện tại quyết định vị trí tác tử phải đứng để đón cú đánh kế tiếp. Mỗi hành động đều ảnh hưởng đến chuỗi trạng thái sau đó. |
| **5. Tính động** | **Dynamic** | **Dynamic** | Quả bóng liên tục bay và đối thủ liên tục di chuyển trong khi tác tử suy nghĩ $\implies$ Môi trường biến đổi không ngừng theo thời gian thực. |
| **6. Tính rời rạc** | **Continuous** | **Continuous** | Quỹ đạo bóng, lực tác động, thời gian tiếp xúc và tọa độ di chuyển đều biến thiên liên tục. |
| **7. Hiểu biết luật** | **Known** | **Known** | Luật chơi quần vợt và các quy luật vật lý cơ bản về độ nảy của bóng đều đã được biết rõ từ trước. |

---

#### Bài tập 3 (Quiz 03 - Slide 64): Thiết kế Tác tử Học hỏi (Learning Agent)
Đề bài: Cho một ví dụ về tác tử duy lý có khả năng học tập, làm rõ 4 thành phần khái niệm:
1. Learning element
2. Performance element
3. Critic
4. Problem generator

**Ví dụ thiết kế: Tác tử Xe Taxi Tự Hành (Autonomous Taxi)**
1. **Performance Element (Phần tử thực thi):**
   - Chứa tập hợp các tri thức lái xe và thuật toán hiện có: thuật toán bám làn, quy tắc giữ khoảng cách an toàn 2 giây, cách thức phanh, ga và chuyển làn tại các giao lộ.
   - Trực tiếp nhận dữ liệu từ Camera/Radar và điều khiển vô lăng/phanh xe trên đường.
2. **Critic (Bộ phận phê bình):**
   - Quan sát phản ứng của môi trường và hành khách để đối chiếu với tiêu chuẩn:
     + Khách phàn nàn xe giật cục khi dừng đèn đỏ.
     + Các xe phía sau bấm còi inh ỏi khi taxi chuyển làn gấp qua 3 làn đường.
     + Điểm an toàn bị trừ khi phanh gấp.
   - Critic đóng gói các sự kiện này thành tín hiệu phản hồi tiêu cực: *"Hành động chuyển làn đột ngột tại đường đông là hành vi tồi!"*.
3. **Learning Element (Phần tử học):**
   - Nhận phản hồi từ Critic để cải tiến tri thức lái xe:
     + Rút ra luật mới: *"Không chuyển làn gấp qua nhiều làn liên tiếp nếu mật độ xe phía sau cao hơn ngưỡng $X$"*.
     + Cập nhật trọng số của mạng nơ-ron điều khiển lực phanh để tạo cảm giác dừng xe mượt mà hơn.
4. **Problem Generator (Bộ phận tạo vấn đề - Khám phá):**
   - Đề xuất các thử nghiệm mới để tích lũy kinh nghiệm trong điều kiện an toàn:
     + Gợi ý: *"Thử nghiệm kiểm tra độ bám đường của phanh với các lực phanh khác nhau trên các bề mặt đường khô vs đường ướt khi đường vắng"* nhằm cập nhật chính xác hệ số ma sát thực tế của lốp xe.
---

## 4. CHƯƠNG 3 - PHẦN 1: GIẢI QUYẾT VẤN ĐỀ BẰNG TÌM KIẾM (PROBLEM SOLVING BY SEARCHING)

### 4.1. Tác tử Giải quyết Vấn đề (Problem-Solving Agents)
- **Quy trình 4 bước của tác tử giải quyết vấn đề:**
  1. **Xác định mục tiêu (Goal formulation):** Dựa trên trạng thái hiện tại và thước đo hiệu quả, tác tử xác định tập hợp các trạng thái thế giới mong muốn đạt được (ví dụ: đang ở Arad, mục tiêu là có mặt tại Bucharest). Mục tiêu giúp giới hạn phạm vi hành động cần cân nhắc.
  2. **Hình thức hóa bài toán (Problem formulation):** Quá trình quyết định những trạng thái và hành động cụ thể nào cần đưa vào xem xét để đạt được mục tiêu.
  3. **Tìm kiếm (Search):** Tác tử mô phỏng trong tâm trí các chuỗi hành động khả thi (xây dựng cây tìm kiếm) để tìm ra một chuỗi hành động đưa từ trạng thái ban đầu tới đích gọi là **Giải pháp (Solution)**.
  4. **Thực thi (Execution):** Tác tử lần lượt thực hiện từng hành động trong chuỗi giải pháp đã tìm được ra thế giới thực.
- **Mã giả Tác tử giải quyết vấn đề đơn giản (Simple Problem-Solving Agent):**
  ```python
  function SIMPLE-PROBLEM-SOLVING-AGENT(percept) returns an action
    persistent: seq, một chuỗi hành động, ban đầu rỗng
                state, mô tả trạng thái thế giới hiện tại
                goal, một mục tiêu, ban đầu null
                problem, hình thức hóa bài toán
    
    state <- UPDATE-STATE(state, percept)
    if seq is empty then
        goal <- FORMULATE-GOAL(state)
        problem <- FORMULATE-PROBLEM(state, goal)
        seq <- SEARCH(problem)
        if seq == failure then return a null action
    action <- FIRST(seq)
    seq <- REST(seq)
    return action
  ```

---

### 4.2. Năm Thành Phần Hình Thức Hóa Bài Toán (Formal Problem Formulation)
Một bài toán tìm kiếm chuẩn chỉnh trong AI được xác định đầy đủ bởi **5 thành phần**:

1. **Trạng thái ban đầu (Initial State):** Trạng thái mà tác tử bắt đầu.
   - *Ví dụ bản đồ Romania:* $In(Arad)$.
2. **Tập hành động khả thi (Actions):** Tập hợp các hành động tác tử có thể thực hiện tại trạng thái $s$, ký hiệu $Actions(s)$.
   - *Ví dụ:* $Actions(In(Arad)) = \{Go(Sibiu), Go(Timisoara), Go(Zerind)\}$.
3. **Mô hình chuyển trạng thái (Transition Model):** Mô tả kết quả của việc thực hiện hành động $a$ tại trạng thái $s$, ký hiệu $Result(s, a)$.
   - *Ví dụ:* $Result(In(Arad), Go(Zerind)) = In(Zerind)$.
   - *(Trạng thái kế tiếp này được gọi là một Successor của $s$).*
4. **Kiểm tra mục tiêu (Goal Test):** Hàm kiểm tra xem một trạng thái $s$ có phải là trạng thái đích hay không.
   - Có thể là kiểm tra tường minh một trạng thái cụ thể: $s == In(Bucharest)$.
   - Hoặc kiểm tra trừu tượng qua một tính chất: $\text{CheckMate}(s) == \text{True}$.
5. **Chi phí đường đi (Path Cost):** Hàm số $g(n)$ gán một chi phí số học cho một chuỗi hành động.
   - Được cộng dồn từ **chi phí từng bước (Step Cost)**: $c(s, a, s')$.
   - Giả định chung trong AI: Chi phí từng bước luôn không âm, tức $c(s, a, s') \ge 0$.

> **Lời giải (Solution):** Một chuỗi các hành động đưa từ trạng thái ban đầu đến một trạng thái thỏa mãn kiểm tra mục tiêu.
> **Lời giải tối ưu (Optimal Solution):** Lời giải có chi phí đường đi nhỏ nhất trong tất cả các lời giải khả thi.

---

### 4.3. Sự Trừu Tượng Hóa Bài Toán (Abstraction)
- Thế giới thực vô cùng phức tạp với vô vàn chi tiết thừa (thời tiết, bạn đồng hành, vết lồi lõm trên mặt đường, lượng tiêu hao xăng từng mét,...).
- **Trừu tượng hóa (Abstraction):** Quá trình loại bỏ các chi tiết không cần thiết khỏi biểu diễn bài toán, chỉ giữ lại những yếu tố cốt lõi:
  + Trạng thái: Đại diện cho một tập hợp lớn các trạng thái thực tế chi tiết.
  + Hành động: Đại diện cho một tập hợp phức tạp các thao tác cấp thấp (ví dụ: $Go(Sibiu)$ trừu tượng hóa cho việc bật máy, đạp ga, bẻ lái hàng triệu lần).
- Một sự trừu tượng hóa là **hợp lệ (valid)** nếu ta có thể chuyển bất kỳ giải pháp trừu tượng nào thành một giải pháp thực tế.

---

### 4.4. Phân loại Bài toán: Toy Problems vs. Real-World Problems

| Tiêu chí | Bài toán Mô hình / Đồ chơi (Toy Problems) | Bài toán Thực tế (Real-World Problems) |
| :--- | :--- | :--- |
| **Mục đích** | - Dùng để thử nghiệm, minh họa giải thuật.<br>- So sánh hiệu quả giữa các phương pháp tìm kiếm. | - Giải quyết các vấn đề kinh tế, kỹ thuật thực tế.<br>- Mang lại giá trị ứng dụng trực tiếp. |
| **Mô tả** | Có mô tả toán học ngắn gọn, chính xác, hoàn toàn rõ ràng. | Không có một mô tả duy nhất; thường phức tạp và phải xấp xỉ. |
| **Ví dụ điển hình** | - **8-puzzle / 15-puzzle**<br>- **8-queens problem**<br>- **Tháp Hà Nội (Towers of Hanoi)**<br>- Bài toán Tu sĩ và Kẻ ăn thịt người (*Missionaries and Cannibals*)<br>- Thế giới robot hút bụi (*Vacuum-cleaner world*) | - Tìm đường đi trên bản đồ thực tế (Google Maps)<br>- Bài toán Người giao hàng (**TSP** - Traveling Salesperson Problem)<br>- Thiết kế bố trí vi mạch (**VLSI layout**)<br>- Định tuyến cánh tay robot công nghiệp (**Robot navigation**)<br>- Lập lịch chuỗi lắp ráp tự động (**Assembly sequencing**) |

#### Phân tích Bài toán 8-Queens: So sánh 2 cách hình thức hóa
Bài toán đặt 8 quân hậu lên bàn cờ vua $8 \times 8$ sao cho không có 2 quân hậu nào tấn công nhau (không cùng hàng, cùng cột, cùng đường chéo):
1. **Hình thức hóa tăng dần (Incremental formulation):**
   - Bắt đầu từ bàn cờ rỗng, đặt từng quân hậu vào ở mỗi bước.
   - *Cách ngây thơ (Naive):* Đặt quân hậu vào bất kỳ ô trống nào.
     + Không gian trạng thái: $64 \times 63 \times \dots \times 57 \approx 1.8 \times 10^{14}$ trạng thái!
   - *Cách cải tiến (Better abstraction):* Mỗi bước đặt 1 quân hậu vào cột trống ngoài cùng bên trái sao cho **không bị tấn công** bởi các quân hậu đã đặt trước đó.
     + Không gian trạng thái giảm mạnh từ $1.8 \times 10^{14}$ xuống chỉ còn **2,057 trạng thái**!
2. **Hình thức hóa toàn trạng thái (Complete-state formulation):**
   - Đặt sẵn cả 8 quân hậu lên bàn cờ ngay từ đầu (mỗi cột 1 quân), sau đó di chuyển các quân hậu trong cột của nó để giảm xung đột.
   - Đây là nền tảng cho các giải thuật **Tìm kiếm cục bộ (Local Search)** ở Chương 4!

---

### 4.5. Hạ Tầng của Thuật Toán Tìm Kiếm: Nút (Node) vs. Trạng Thái (State)

```
        Node (Search Tree Data Structure)
   +------------------------------------------+
   | STATE      : In(Sibiu)                  |
   | PARENT     : Pointer to Node(Arad)       |
   | ACTION     : Go(Sibiu)                   |
   | PATH-COST  : g(Sibiu) = g(Arad) + 140    |
   | DEPTH      : depth(Arad) + 1             |
   +------------------------------------------+
```

- **Phân biệt rạch ròi giữa Nút (Node) và Trạng thái (State):**
  + **Trạng thái (State):** Đại diện cho một cấu hình vật lý của thế giới (ví dụ: thành phố Arad). Trạng thái không có con trỏ cha, không có độ sâu.
  + **Nút (Node):** Cấu trúc dữ liệu cụ thể trong cây tìm kiếm dùng để theo dõi quá trình duyệt. Hai nút khác nhau trong cây tìm kiếm có thể chứa cùng một trạng thái thế giới (nếu có nhiều đường đi dẫn tới cùng một thành phố).
- **Cấu trúc 4 trường thành phần của một Node $n$:**
  1. `n.STATE`: Trạng thái trong không gian trạng thái mà nút đại diện.
  2. `n.PARENT`: Nút cha trong cây tìm kiếm đã sinh ra nút $n$.
  3. `n.ACTION`: Hành động áp dụng từ nút cha để tạo ra $n$.
  4. `n.PATH-COST`: Chi phí đường đi $g(n)$ tính từ gốc tới nút $n$.

- **Hàm mở rộng nút con (CHILD-NODE):**
  ```python
  function CHILD-NODE(problem, parent, action) returns a node
      return a node with
          STATE = problem.RESULT(parent.STATE, action),
          PARENT = parent,
          ACTION = action,
          PATH-COST = parent.PATH-COST + problem.STEP-COST(parent.STATE, action)
  ```

---

### 4.6. Tree-Search vs. Graph-Search: Đường đi dư thừa và Vòng lặp

```
           +-----------------------------------------------+
           |               TREE-SEARCH                     |
           | - Không lưu tập các đỉnh đã duyệt (explored).  |
           | - Dễ rơi vào chu trình lặp vô tận!            |
           +-----------------------------------------------+
                                  |
            Thêm cơ chế kiểm tra trạng thái lặp lại
                                  |
                                  v
           +-----------------------------------------------+
           |               GRAPH-SEARCH                    |
           | - Duy trì tập `explored` (Closed list).       |
           | - Chỉ đưa con vào `frontier` nếu trạng thái   |
           |   chưa có trong `frontier` và `explored`.     |
           +-----------------------------------------------+
```

- **Vấn đề đường đi dư thừa (Redundant paths & Repeated states):**
  + Xảy ra khi có nhiều hơn một cách để đi từ trạng thái này tới trạng thái khác (ví dụ: đồ thị có chu trình, đồ thị vô hướng).
  + Trên một lưới 2 chiều nơi mỗi ô có 4 hướng đi: Cây tìm kiếm độ sâu $d$ sinh ra $4^d$ nút lá, nhưng thực chất chỉ có khoảng $2d^2$ trạng thái phân biệt! Với $d = 20$, số nút lá là hơn $10^{12}$ (1 nghìn tỷ nút) nhưng chỉ có khoảng 800 trạng thái thực tế.
- **Thuật toán GRAPH-SEARCH:**
  ```python
  function GRAPH-SEARCH(problem) returns a solution, or failure
      initialize frontier using initial state of problem
      initialize explored set to be empty
      loop do
          if frontier is empty then return failure
          node <- choose a leaf node and remove it from frontier
          if node contains a goal state then return corresponding solution
          add node.STATE to explored set
          expand chosen node, adding resulting nodes to frontier
              only if not in frontier or explored set
  ```
- **Tính chất chia cắt của Graph-Search (Separation Property):**
  + Tập biên (`frontier`) đóng vai trò ranh giới ngăn cách không gian trạng thái thành 2 vùng riêng biệt: **Vùng đã khám phá (Explored region)** và **Vùng chưa khám phá (Unexplored region)**.
  + Mọi đường đi từ trạng thái khởi đầu đến một trạng thái chưa khám phá bắt buộc phải đi qua ít nhất một nút nằm trong `frontier`.

---

### 4.7. Bốn Tiêu Chí Đánh Giá Hiệu Năng Giải Thuật Tìm Kiếm
Các thuật toán tìm kiếm được đo lường dựa trên 4 chỉ số:
1. **Tính đầy đủ (Completeness):** Thuật toán có luôn luôn tìm thấy giải pháp hay không (nếu giải pháp tồn tại)?
2. **Độ phức tạp thời gian (Time Complexity):** Thuật toán mất bao lâu (hoặc sinh ra bao nhiêu nút) để tìm ra nghiệm?
3. **Độ phức tạp không gian (Space Complexity):** Thuật toán cần tiêu tốn bao nhiêu bộ nhớ trong quá trình tìm kiếm?
4. **Tính tối ưu (Optimality):** Thuật toán có luôn luôn tìm được lời giải có chi phí nhỏ nhất hay không?

#### Ba tham số định lượng không gian tìm kiếm:
- $b$ (*branching factor*): Hệ số phân nhánh tối đa của cây tìm kiếm (số con tối đa của một nút).
- $d$ (*depth*): Độ sâu của trạng thái đích nông nhất (shallowest goal node).
- $m$ (*maximum depth*): Độ sâu tối đa của không gian trạng thái (có thể là $\infty$ nếu đồ thị có chu trình lặp vô tận).

---

### 4.8. GIẢI CHI TIẾT CÁC BÀI TẬP VÀ QUIZ TRONG LECTURE 03 - PART 1

#### Bài tập 1 (Quiz 01 - Slide 30): Hình thức hóa Bài toán Tháp Hà Nội
Đề bài: Hãy hình thức hóa bài toán Tháp Hà Nội (*Towers of Hanoi*) với 3 cọc (ký hiệu $A, B, C$) và 3 chiếc đĩa có kích thước khác nhau ($1 < 2 < 3$) theo đúng chuẩn 5 thành phần.

**Lời giải chi tiết chuẩn 5 thành phần:**
1. **Biểu diễn trạng thái (State Representation):**
   - Một trạng thái được biểu diễn bằng bộ 3 vị trí cọc của 3 đĩa:
     $$s = (p_1, p_2, p_3) \quad \text{với } p_i \in \{A, B, C\}$$
     *(Trong đó $p_1$ là vị trí cọc của đĩa nhỏ nhất 1, $p_2$ của đĩa vừa 2, $p_3$ của đĩa lớn nhất 3).*
   - Tổng số trạng thái hợp lệ của bài toán 3 đĩa là $3^3 = 27$ trạng thái.
2. **Trạng thái ban đầu (Initial State):**
   - Cả 3 đĩa đều nằm trên cọc $A$:
     $$s_0 = (A, A, A)$$
3. **Tập hành động khả thi (Actions):**
   - Hành động di chuyển đĩa trên cùng từ cọc nguồn $X$ sang cọc đích $Y$, ký hiệu $Move(disk, X, Y)$ với $X, Y \in \{A, B, C\}, X \ne Y$.
   - **Ràng buộc điều kiện (Preconditions):**
     + Đĩa được di chuyển phải là **đĩa nằm trên cùng** của cọc $X$ (không có đĩa nào nhỏ hơn đang nằm trên nó ở cọc $X$).
     + Đĩa đó chỉ được đặt lên cọc $Y$ nếu cọc $Y$ đang rỗng hoặc đĩa trên cùng của cọc $Y$ **có kích thước lớn hơn** đĩa được di chuyển.
4. **Mô hình chuyển trạng thái (Transition Model):**
   - $Result((p_1, p_2, p_3), Move(i, X, Y))$ trả về trạng thái mới trong đó $p_i$ đổi từ $X$ thành $Y$, các đĩa khác giữ nguyên vị trí.
5. **Kiểm tra mục tiêu (Goal Test):**
   - Tất cả 3 đĩa đều được chuyển sang cọc đích (ví dụ cọc $C$):
     $$Goal\text{-}Test(s) \iff s == (C, C, C)$$
6. **Chi phí đường đi (Path Cost):**
   - Mỗi bước di chuyển 1 đĩa có chi phí bằng 1 ($c = 1$). Tổng chi phí bằng tổng số bước di chuyển. (Lời giải tối ưu cho 3 đĩa mất $2^3 - 1 = 7$ bước).

---

#### Bài tập 2 (Quiz 02 - Slide 42): Vẽ Cây Tìm Kiếm Tháp Hà Nội 2 Cọc 2 Đĩa
Đề bài: Vẽ 2 mức đầu tiên của cây tìm kiếm cho bài toán Tháp Hà Nội với 3 cọc ($A, B, C$) và 2 đĩa (đĩa 1 nhỏ, đĩa 2 lớn). Trạng thái ban đầu: cả 2 đĩa ở cọc $A$, tức $(A, A)$. Bỏ qua các trạng thái lặp lại ngay trên cùng một nhánh đường đi.

**Quá trình suy luận và dựng cây tìm kiếm:**
- **Mức 0 (Root - Độ sâu 0):**
  + Trạng thái gốc: `(A, A)` (Đĩa 1 ở A, Đĩa 2 ở A).
- **Mức 1 (Độ sâu 1):**
  + Tại `(A, A)`, chỉ có đĩa 1 (trên cùng) được phép di chuyển sang cọc $B$ hoặc cọc $C$. (Đĩa 2 bị đĩa 1 chặn nên không đi được).
  + Áp dụng hành động:
    1. $Move(1, A, B) \implies$ Sinh nút con **(B, A)**.
    2. $Move(1, A, C) \implies$ Sinh nút con **(C, A)**.
- **Mức 2 (Độ sâu 2):**
  - **Từ nút con (B, A):**
    + Đĩa 1 ở B có thể đi về A: $Move(1, B, A) \implies (A, A)$ (*bị loại vì lặp lại trạng thái cha*).
    + Đĩa 1 ở B có thể đi sang C: $Move(1, B, C) \implies$ Sinh nút **(C, A)**.
    + Đĩa 2 ở A hiện đã thông thoáng, cọc C đang rỗng nên đĩa 2 có thể sang C: $Move(2, A, C) \implies$ Sinh nút **(B, C)**.
  - **Từ nút con (C, A):**
    + Đĩa 1 ở C có thể đi về A: $Move(1, C, A) \implies (A, A)$ (*bị loại vì lặp lại trạng thái cha*).
    + Đĩa 1 ở C có thể đi sang B: $Move(1, C, B) \implies$ Sinh nút **(B, A)**.
    + Đĩa 2 ở A thông thoáng, cọc B rỗng nên đĩa 2 có thể sang B: $Move(2, A, B) \implies$ Sinh nút **(C, B)**.

**Sơ đồ Cây Tìm Kiếm (Dạng Text / Diagram):**
```
Level 0:                         [ (A, A) ]
                                /          \
Level 1:              [ (B, A) ]            [ (C, A) ]
                      /        \            /        \
Level 2:       [ (C, A) ]   [ (B, C) ]  [ (B, A) ]   [ (C, B) ]
```
*(Ghi chú: Lời giải tối ưu đưa cả 2 đĩa sang cọc C là: `(A, A) -> (B, A) -> (B, C) -> (C, C)` với chi phí 3 bước).*
---

## 5. CHƯƠNG 3 - PHẦN 2: TÌM KIẾM MÙ / KHÔNG CÓ THÔNG TIN (UNINFORMED SEARCH STRATEGIES)

### 5.1. Bản Chất của Tìm Kiếm Mù (Uninformed / Blind Search)
- **Định nghĩa:** Là chiến lược tìm kiếm **không có thêm bất kỳ thông tin nào** về trạng thái ngoài những gì đã được cung cấp trong định nghĩa bài toán.
- Tác tử chỉ biết: Trạng thái hiện tại có phải là Goal hay không, và từ trạng thái này có thể đi tới những trạng thái con nào.
- Tác tử **hoàn toàn không biết** một trạng thái con bất kỳ đang "ở gần" hay "ở xa" mục tiêu (không có hàm ước lượng khoảng cách).
- Các thuật toán tìm kiếm mù chỉ khác nhau ở **thứ tự lựa chọn nút nào trong tập `frontier` để mở rộng tiếp theo**.

---

### 5.2. Chi Tiết Sáu Thuật Toán Tìm Kiếm Mù

#### 1. Tìm kiếm theo chiều rộng (Breadth-First Search - BFS)
- **Cấu trúc dữ liệu:** Hàng đợi FIFO (`Queue` - First In First Out). Nút nào được đưa vào `frontier` trước sẽ được lấy ra mở rộng trước.
- **Thứ tự mở rộng:** Mở rộng nút gốc trước, sau đó mở rộng toàn bộ các nút con ở mức độ sâu 1, rồi đến tất cả các nút ở mức độ sâu 2, v.v... Luôn duyệt xong toàn bộ một tầng rồi mới sang tầng kế tiếp.
- **Thời điểm kiểm tra đích (Early Goal Test):**
  + Trong BFS, kiểm tra mục tiêu được thực hiện **ngay khi nút con được sinh ra (Upon Generation)**, chứ không đợi đến khi nó được lấy ra khỏi hàng đợi.
  + Nếu nút con là đích $\implies$ Dừng và trả về kết quả ngay lập tức (giúp tiết kiệm duyệt nguyên một tầng con).
- **Đánh giá hiệu năng:**
  + *Tính đầy đủ (Completeness):* **CÓ** (Nếu hệ số phân nhánh $b$ hữu hạn).
  + *Độ phức tạp thời gian:* $1 + b + b^2 + \dots + b^d = O(b^d)$.
  + *Độ phức tạp không gian (Bộ nhớ):* $O(b^d)$ (Tất cả các nút ở tầng $d$ đều phải nằm trong `frontier`).
  + *Tính tối ưu (Optimality):* **CÓ nếu chi phí mỗi bước bằng nhau** ($c = 1$). Không đảm bảo tối ưu nếu chi phí các bước khác nhau.
- **Tử huyệt của BFS:** **Bùng nổ bộ nhớ!** Bộ nhớ tăng theo hàm mũ $O(b^d)$ khiến BFS thường tràn RAM chỉ sau độ sâu $d \ge 10$ trong vòng vài giây.

---

#### 2. Tìm kiếm chi phí đồng nhất (Uniform-Cost Search - UCS)
- **Cấu trúc dữ liệu:** Hàng đợi ưu tiên (`Priority Queue`), được sắp xếp tăng dần theo **chi phí đường đi tích lũy $g(n)$**.
- **Cơ chế:** Luôn chọn lấy ra nút có $g(n)$ nhỏ nhất trong `frontier` để mở rộng.
  + Nếu chi phí các bước đều bằng nhau $\implies$ UCS hoạt động hoàn toàn giống BFS.
  + Trong lý thuyết đồ thị tổng quát $\implies$ UCS chính là **Thuật toán Dijkstra**!
- **Hai quy tắc sống còn trong mã giả UCS (Bẫy thi cực lớn!):**
  1. **Thời điểm kiểm tra đích (Late Goal Test):** Kiểm tra mục tiêu **chỉ khi nút được chọn lấy ra khỏi `frontier` để mở rộng (Upon Expansion)**. Tuyệt đối KHÔNG kiểm tra khi sinh ra!
     *(Lý do: Một nút đích có thể được sinh ra từ một nhánh đường đi dài có chi phí cao; nhưng sau đó có thể một đường đi khác ngắn hơn dẫn tới đích mới được duyệt tới. Nếu kiểm tra sớm, thuật toán sẽ trả về nghiệm dưới tối ưu!)*
  2. **Cập nhật đường đi tốt hơn trong Frontier:** Nếu sinh ra một nút con mà trạng thái của nó **đã tồn tại trong `frontier` với chi phí $g$ cao hơn**, thuật toán phải **thay thế nút cũ bằng nút mới có chi phí thấp hơn**.
- **Đánh giá hiệu năng:**
  + Gọi $C^*$ là chi phí của lời giải tối ưu. Giả sử mỗi bước đi tốn chi phí ít nhất là $\epsilon > 0$.
  + Số bước đi hiệu dụng là $\lfloor C^* / \epsilon \rfloor$.
  + *Tính đầy đủ:* **CÓ** (nếu $b$ hữu hạn và bước đi $\ge \epsilon > 0$).
  + *Thời gian & Không gian:* $O(b^{1 + \lfloor C^* / \epsilon \rfloor})$.
  + *Tính tối ưu:* **LUÔN LUÔN TỐI ƯU** với mọi đồ thị có trọng số không âm.
- **So sánh UCS vs BFS khi chi phí mọi bước đều bằng 1:**
  + UCS duyệt tốn kém hơn BFS! Vì BFS dừng ngay khi sinh ra đích ở tầng $d$ ($O(b^d)$), trong khi UCS phải duyệt hết toàn bộ các nút ở tầng $d$ rồi mới lấy nút đích ra ở tầng $d+1$, do đó độ phức tạp là $O(b^{d+1})$.

---

#### 3. Tìm kiếm theo chiều sâu (Depth-First Search - DFS)
- **Cấu trúc dữ liệu:** Ngăn xếp LIFO (`Stack` - Last In First Out). Nút con vừa sinh ra sẽ được đẩy lên đỉnh ngăn xếp và được mở rộng ngay lập tức.
- **Thứ tự mở rộng:** Luôn mở rộng nút sâu nhất chưa được khám phá trong cây tìm kiếm. Thuật toán đi thẳng một mạch xuống nhánh sâu nhất cho đến khi gặp ngõ cụt thì mới **quay lui (backtrack)**.
- **Đánh giá hiệu năng:**
  + *Tính đầy đủ:*
    * Tree-search: **KHÔNG đầy đủ** (bị lặp vô tận nếu đồ thị có chu trình hoặc nhánh có độ sâu vô hạn).
    * Graph-search: **CÓ đầy đủ** trên không gian trạng thái hữu hạn (nhờ tập `explored` chặn chu trình).
  + *Độ phức tạp thời gian:* Trường hợp xấu nhất phải duyệt toàn bộ không gian: $O(b^m)$ ($m$ là độ sâu tối đa, có thể $m \gg d$).
  + *Độ phức tạp không gian:* **ƯU THẾ VƯỢT TRỘI: $O(bm)$ (Bộ nhớ tuyến tính!)**
    *(Chỉ cần lưu vết đường đi từ gốc tới nút hiện tại cùng các nhánh rẽ chưa mở rộng).*
  + *Tính tối ưu:* **KHÔNG tối ưu** (có thể tìm thấy nghiệm rất sâu trước khi phát hiện nghiệm nông).

---

#### 4. Tìm kiếm giới hạn độ sâu (Depth-Limited Search - DLS)
- **Động lực:** Giải quyết nhược điểm rơi vào nhánh vô hạn của DFS bằng cách áp đặt một **ngưỡng giới hạn độ sâu $l$**.
- **Cơ chế:** Các nút ở độ sâu $l$ được xem như không có con (dừng duyệt nhánh đó).
- **Ba kết quả trả về của DLS:**
  1. `solution`: Tìm thấy lời giải.
  2. `failure`: Đã duyệt hết toàn bộ không gian trạng thái mà không có lời giải.
  3. `cutoff`: Không tìm thấy lời giải trong phạm vi độ sâu $l$ (nhưng có thể lời giải nằm ở độ sâu $> l$).
- **Đánh giá:**
  + Nếu chọn $l < d \implies$ Mất tính đầy đủ (không tìm thấy nghiệm).
  + Nếu chọn $l > d \implies$ Không tối ưu.
  + Thời gian: $O(b^l)$, Không gian: $O(bl)$.
  + *Trường hợp đặc biệt:* Khi $l = \infty$, DLS chính là DFS tiêu chuẩn.

---

#### 5. Tìm kiếm lặp sâu (Iterative Deepening Search - IDS)
- **Động lực:** Khi không biết trước độ sâu $d$ của lời giải, làm sao để vừa tiết kiệm bộ nhớ như DFS, vừa có tính đầy đủ và tối ưu như BFS?
- **Cơ chế:** Gọi liên tiếp thuật toán DLS với giới hạn $l$ tăng dần:
  $$\text{for } \text{limit} = 0, 1, 2, \dots, \infty \text{ do: } \text{result} = \text{DLS}(problem, \text{limit})$$
- **Nghi vấn về chi phí lặp lại:** Các tầng nông có bị sinh lại quá nhiều lần gây lãng phí không?
  + Ở tầng 0: được sinh $(d+1)$ lần.
  + Ở tầng 1: được sinh $d$ lần ($d \cdot b$).
  + Ở tầng $d$: được sinh 1 lần ($1 \cdot b^d$).
  + Tổng số nút sinh ra:
    $$N(\text{IDS}) = (d+1)1 + d b + (d-1) b^2 + \dots + 1 b^d = O(b^d)$$
  + Trong cây tìm kiếm, **đa số các nút tập trung áp đảo ở tầng đáy cùng**. Phần lặp lại ở các tầng nông chỉ chiếm một tỷ lệ rất nhỏ!
    *(Ví dụ với $b = 10, d = 5$: BFS sinh 111,111 nút; IDS sinh 123,456 nút -> IDS chỉ tốn thêm khoảng 11% phép toán nhưng đổi lại bộ nhớ chỉ tốn $O(bd)$ thay vì $O(b^d)$!).*
- **Đánh giá hiệu năng:**
  + *Tính đầy đủ:* **CÓ** (nếu $b$ hữu hạn).
  + *Độ phức tạp thời gian:* $O(b^d)$.
  + *Độ phức tạp không gian:* **$O(bd)$ (Tuyến tính, cực kỳ tiết kiệm bộ nhớ!)**.
  + *Tính tối ưu:* **CÓ** nếu chi phí các bước bằng nhau ($c = 1$).
- **Khuyến nghị:** IDS là phương pháp tìm kiếm mù **tối ưu nhất và được ưu tiên lựa chọn hàng đầu** khi không gian tìm kiếm lớn và chưa biết độ sâu của nghiệm.

---

#### 6. Tìm kiếm hai chiều (Bidirectional Search)
- **Cơ chế:** Chạy đồng thời 2 quá trình tìm kiếm: một từ trạng thái ban đầu đi tới (Forward), một từ trạng thái đích đi ngược lại (Backward).
- **Kiểm tra đích:** Khi biên (`frontier`) của hai tìm kiếm giao nhau tại một trạng thái $\implies$ Nối 2 nửa đường đi lại để tạo ra giải pháp hoàn chỉnh.
- **Hiệu quả:**
  + Thời gian và bộ nhớ giảm từ $O(b^d)$ xuống còn $O(b^{d/2}) + O(b^{d/2}) = O(b^{d/2})$.
  + *(Ví dụ $b = 10, d = 6$: BFS tốn $10^6 = 1,000,000$ nút; Tìm kiếm 2 chiều chỉ tốn $2 \times 10^3 = 2,000$ nút!).*
- **Khó khăn thực tế:** Phải tính được hành động ngược ($Predecessors$) từ trạng thái đích; cần giải pháp hiệu quả để kiểm tra giao điểm của hai biên.

---

### 5.3. BẢNG SO SÁNH TỔNG HỢP CÁC THUẬT TOÁN TÌM KIẾM MÙ

| Thuật toán | Tính đầy đủ (Complete) | Thời gian (Time) | Không gian (Space) | Tính tối ưu (Optimal) |
| :--- | :---: | :---: | :---: | :---: |
| **BFS** *(Breadth-First)* | **CÓ** *(nếu $b < \infty$)* | $O(b^d)$ | $O(b^d)$ | **CÓ** *(nếu chi phí bước $c=1$)* |
| **UCS** *(Uniform-Cost)* | **CÓ** *(nếu step cost $\ge \epsilon > 0$)* | $O(b^{1 + \lfloor C^* / \epsilon \rfloor})$ | $O(b^{1 + \lfloor C^* / \epsilon \rfloor})$ | **LUÔN TỐI ƯU** |
| **DFS** *(Depth-First Tree)* | **KHÔNG** *(vướng chu trình)* | $O(b^m)$ | $O(bm)$ | **KHÔNG** |
| **DFS** *(Depth-First Graph)* | **CÓ** *(nếu không gian hữu hạn)*| $O(b^m)$ | $O(b \cdot m)$ | **KHÔNG** |
| **DLS** *(Depth-Limited)* | **KHÔNG** *(nếu $l < d$)* | $O(b^l)$ | $O(bl)$ | **KHÔNG** |
| **IDS** *(Iterative Deepening)*| **CÓ** *(nếu $b < \infty$)* | $O(b^d)$ | $O(bd)$ | **CÓ** *(nếu chi phí bước $c=1$)* |
| **Bidirectional Search** | **CÓ** *(nếu $b < \infty$)* | $O(b^{d/2})$ | $O(b^{d/2})$ | **CÓ** *(nếu chi phí bước $c=1$)* |

---

### 5.4. GIẢI CHI TIẾT BÀI TẬP VÀ QUIZ TRONG LECTURE 03 - PART 2
*(Đề bài xuất hiện tại các Slide 21, 41, 48 của Lecture 03-P2. Cả ba Quiz đều sử dụng chung một đồ thị chuẩn bên dưới).*

#### Đồ thị chuẩn của Bài tập (Standard Problem Graph):
```
             (A, h=2)
            /        \
         2 /          \ 4
          /            \
    [Start]             (C, h=2) ------- 2 ------- [Goal]
       |  \             /                            /
     3 |   \ 5       1 /                            / 5
       |    \         /                            /
     (B)     ------- (D, h=1) ---------------------
     h=5        4
```
**Danh sách cạnh và trọng số chi phí $c$:**
- $\text{Start} - A: 2$
- $\text{Start} - B: 3$
- $\text{Start} - D: 5$
- $A - C: 4$
- $B - D: 4$
- $C - D: 1$
- $C - \text{Goal}: 2$
- $D - \text{Goal}: 5$

**Quy tắc giải hòa (Tie-breaking rule):**
> *"Assume ties resolve in such a way that states with earlier alphabetical order are expanded first."*  
> (Khi có nhiều nút có cùng độ ưu tiên trong Frontier, nút có tên theo thứ tự bảng chữ cái đứng trước sẽ được lấy ra mở rộng trước: $A < B < C < D < \text{Goal} < \text{Start}$).

---

#### BÀI TẬP 1 (QUIZ 01 - SLIDE 21): BREADTH-FIRST SEARCH (GRAPH SEARCH)
**Yêu cầu:** Xác định thứ tự các trạng thái được mở rộng và đường đi tìm được bằng giải thuật BFS (phiên bản Graph Search).

**Phân tích thuật toán BFS Graph Search chuẩn (Slide 10):**
- Sử dụng hàng đợi FIFO.
- Tập `explored` lưu các trạng thái đã mở rộng.
- **Kiểm tra đích sớm (Early goal test):** Kiểm tra ngay khi sinh ra nút con (`child`). Nếu trùng `Goal` thì dừng ngay!
- Khi sinh con từ nút cha, các con chưa nằm trong `explored` và chưa nằm trong `frontier` sẽ được đưa vào `frontier` theo thứ tự bảng chữ cái.

**Bảng trace chi tiết từng bước:**

| Bước | Lấy ra khỏi Frontier | Trạng thái Explored | Sinh các nút con (Kiểm tra đích & Đưa vào Frontier) | Trạng thái Frontier (FIFO) |
| :---: | :---: | :---: | :---: | :---: |
| **0** | *(Khởi tạo)* | $\emptyset$ | Nút gốc Start (g=0). Chưa phải Goal. | `[Start]` |
| **1** | **Start** | `{Start}` | - Con của Start: $A, B, D$.<br>- Kiểm tra: Chưa con nào là Goal.<br>- Đưa vào Frontier theo thứ tự chữ cái: $A, B, D$. | `[A, B, D]` |
| **2** | **A** | `{Start, A}` | - Láng giềng của $A$: Start (đã explored), $C$.<br>- Con mới: $C$. Chưa phải Goal.<br>- Đưa $C$ vào hàng đợi. | `[B, D, C]` |
| **3** | **B** | `{Start, A, B}` | - Láng giềng của $B$: Start (đã explored), $D$ (đang có trong Frontier).<br>- Không có con mới nào được thêm. | `[D, C]` |
| **4** | **D** | `{Start, A, B, D}` | - Láng giềng của $D$: Start (explored), $B$ (explored), $C$ (trong Frontier), **Goal**.<br>- Sinh con **Goal** $\implies$ **KIỂM TRA ĐÍCH THÀNH CÔNG!** Thuật toán DỪNG NGAY LẬP TỨC! | *(Dừng)* |

**Kết luận Quiz 01:**
- **Thứ tự các trạng thái được mở rộng (Expanded order):**
  $$\text{Start} \to A \to B \to D$$
- **Đường đi tìm thấy (Solution Path):**
  $$\mathbf{Start \to D \to Goal}$$
- **Tổng chi phí của đường đi:**
  $$\text{Cost} = c(\text{Start}, D) + c(D, \text{Goal}) = 5 + 5 = \mathbf{10}$$

*(Ghi chú: Nếu đề bài áp dụng kiểm tra đích trễ khi lấy ra khỏi hàng đợi, thứ tự mở rộng sẽ là $\text{Start} \to A \to B \to D \to C \to \text{Goal}$, đường đi vẫn là $\text{Start} \to D \to Goal$).*

---

#### BÀI TẬP 2 (QUIZ 02 - SLIDE 41): UNIFORM-COST SEARCH (GRAPH SEARCH)
**Yêu cầu:** Xác định thứ tự các trạng thái được mở rộng và đường đi trả về bởi giải thuật Uniform-Cost Search (Graph Search).

**Phân tích thuật toán UCS chuẩn (Slide 25):**
- Sử dụng `Priority Queue` sắp xếp theo chi phí tích lũy $g(n)$.
- **Kiểm tra đích trễ (Late goal test):** Chỉ kiểm tra khi nút được lấy ra (`pop`) khỏi Priority Queue.
- **Cập nhật Frontier:** Nếu sinh ra trạng thái đã có trong Frontier nhưng đường đi mới có chi phí $g$ nhỏ hơn $\implies$ Cập nhật giảm chi phí của nút đó trong Frontier.
- Giải hòa bằng thứ tự bảng chữ cái.

**Bảng trace chi tiết từng bước:**

| Bước | Lấy ra khỏi Frontier (Pop) | $g(n)$ | Trạng thái Explored | Sinh các nút con & Cập nhật Frontier | Trạng thái Frontier (Priority Queue) |
| :---: | :---: | :---: | :---: | :---: | :---: |
| **0** | *(Khởi tạo)* | - | $\emptyset$ | Nạp gốc Start với $g=0$. | `{(Start, g=0, path=[Start])}` |
| **1** | **Start** | 0 | `{Start}` | - Con $A$: $g = 0 + 2 = 2$. Path: Start-A.<br>- Con $B$: $g = 0 + 3 = 3$. Path: Start-B.<br>- Con $D$: $g = 0 + 5 = 5$. Path: Start-D. | `{(A: 2), (B: 3), (D: 5)}` |
| **2** | **A** | 2 | `{Start, A}` | - Láng giềng $C$: $g = 2 + 4 = 6$. Path: Start-A-C. Thêm $C$ vào PQ. | `{(B: 3), (D: 5), (C: 6)}` |
| **3** | **B** | 3 | `{Start, A, B}` | - Láng giềng $D$: $g = 3 + 4 = 7$. Trong PQ nút $D$ đang có $g=5 < 7 \implies$ Giữ nguyên $D(5)$. | `{(D: 5), (C: 6)}` |
| **4** | **D** | 5 | `{Start, A, B, D}` | - Láng giềng $C$: $g = 5 + 1 = 6$. Bằng $g(C)$ hiện tại $\implies$ Giữ nguyên nhánh $A \to C$.<br>- Láng giềng $\text{Goal}$: $g = 5 + 5 = 10$. Path: Start-D-Goal. Thêm $\text{Goal}(10)$. | `{(C: 6), (Goal: 10)}` |
| **5** | **C** | 6 | `{Start, A, B, D, C}` | - Láng giềng $\text{Goal}$: $g = 6 + 2 = 8$.<br>- Trong PQ, $\text{Goal}$ đang có chi phí 10. Vì $8 < 10 \implies$ **CẬP NHẬT $\text{Goal}$ với chi phí mới $g=8$** và đường đi mới: Start-A-C-Goal! | `{(Goal: 8)}` |
| **6** | **Goal** | **8** | - | **Kiểm tra đích: Goal reached! Thuật toán DỪNG.** | - |

**Kết luận Quiz 02:**
- **Thứ tự các trạng thái được mở rộng (Expanded order):**
  $$\mathbf{Start \to A \to B \to D \to C \to Goal}$$
- **Đường đi tối ưu tìm được (Optimal Solution Path):**
  $$\mathbf{Start \to A \to C \to Goal}$$
- **Tổng chi phí tối ưu:**
  $$\text{Cost} = 2 + 4 + 2 = \mathbf{8}$$

> **Nhận xét sâu sắc để ghi điểm tối đa:**
> - UCS đã tìm ra nghiệm thực sự tối ưu với chi phí **8**, khác biệt hoàn toàn với nghiệm dưới tối ưu chi phí **10** của BFS!
> - Việc kiểm tra đích trễ tại Bước 6 đã cho phép UCS mở rộng nút $C$ tại Bước 5, qua đó phát hiện đường đi tốt hơn $Start \to A \to C \to Goal$ ($g=8$) thay thế cho đường đi $Start \to D \to Goal$ ($g=10$).

---

#### BÀI TẬP 3 (QUIZ 03 - SLIDE 48): DEPTH-FIRST SEARCH (GRAPH SEARCH)
**Yêu cầu:** Xác định thứ tự các trạng thái được mở rộng và đường đi trả về bởi giải thuật Depth-First Search (phiên bản Graph Search). Giả sử giải hòa theo thứ tự bảng chữ cái đứng trước được duyệt trước.

**Phân tích thuật toán DFS Graph Search:**
- Duyệt theo chiều sâu: Từ trạng thái hiện tại, đi sâu vào láng giềng hợp lệ đầu tiên theo thứ tự chữ cái ($A < B < C < D < \text{Goal}$).
- Duy trì tập các đỉnh đã thăm (`visited`/`explored`) để không bao giờ đi lại đỉnh cũ.
- Khi một nút không còn láng giềng nào chưa thăm $\implies$ Quay lui (Backtrack) về nút cha.

**Quá trình duyệt chi tiết từng bước:**
1. **Bắt đầu tại Start:**
   - Các láng giềng: $A, B, D$.
   - Theo thứ tự chữ cái: Chọn **A** đi tiếp.
   - Trạng thái đã duyệt: `{Start, A}`. Đường đi tạm thời: `Start -> A`.
2. **Tại A:**
   - Các láng giềng: Start (đã duyệt), $C$.
   - Chọn **C** đi tiếp.
   - Trạng thái đã duyệt: `{Start, A, C}`. Đường đi: `Start -> A -> C`.
3. **Tại C:**
   - Các láng giềng chưa duyệt: $D$ và $\text{Goal}$.
   - Theo quy tắc giải hòa bảng chữ cái: **$D$ đứng trước $\text{Goal}$ trong bảng chữ cái ($D < G$)!**
   - Do đó, DFS bắt buộc phải chọn đi sâu vào **D** thay vì Goal!
   - Trạng thái đã duyệt: `{Start, A, C, D}`. Đường đi: `Start -> A -> C -> D`.
4. **Tại D:**
   - Các láng giềng của $D$: Start (đã duyệt), $C$ (đã duyệt), $B$ (chưa duyệt), $\text{Goal}$ (chưa duyệt).
   - Theo thứ tự chữ cái: **$B$ đứng trước $\text{Goal}$ ($B < G$)!**
   - Thuật toán chọn đi sâu vào **B**!
   - Trạng thái đã duyệt: `{Start, A, C, D, B}`. Đường đi: `Start -> A -> C -> D -> B`.
5. **Tại B:**
   - Các láng giềng của $B$: Start (đã duyệt), $D$ (đã duyệt).
   - Nút $B$ không còn bất kỳ láng giềng nào chưa thăm $\implies$ Ngõ cụt!
   - Thuật toán **quay lui (Backtrack)** về lại $D$.
6. **Quay lui về D:**
   - Xét tiếp láng giềng chưa thăm kế tiếp của $D$: chính là **Goal**!
   - Chọn đi tới **Goal**.
   - **Gặp đích Goal $\implies$ Thuật toán DỪNG!**

**Kết luận Quiz 03:**
- **Thứ tự các trạng thái được mở rộng (Expanded order):**
  $$\mathbf{Start \to A \to C \to D \to B \to Goal}$$
- **Đường đi tìm thấy (Solution Path):**
  $$\mathbf{Start \to A \to C \to D \to Goal}$$
- **Tổng chi phí của đường đi DFS:**
  $$\text{Cost} = c(Start, A) + c(A, C) + c(C, D) + c(D, Goal) = 2 + 4 + 1 + 5 = \mathbf{12}$$
---

## 6. CHƯƠNG 3 - PHẦN 3: TÌM KIẾM CÓ THÔNG TIN / HEURISTIC (INFORMED SEARCH STRATEGIES)

### 6.1. Khái Niệm Hàm Heuristic $h(n)$
- **Hàm Heuristic $h(n)$:** Hàm số ước lượng chi phí của đường đi rẻ nhất từ trạng thái tại nút $n$ đến một trạng thái đích (Goal):
  $$h(n) = \text{Chi phí ước lượng từ } n \to \text{Goal}$$
- **Quy ước chuẩn:**
  + $h(n) \ge 0$ với mọi nút $n$.
  + $h(\text{Goal}) = 0$ tại mọi trạng thái đích.
  + Heuristic mang tính đặc thù cho từng bài toán (Problem-specific knowledge).
  + *(Ví dụ bài toán tìm đường Romania:* $h_{SLD}(n)$ là khoảng cách đường chim bay thẳng từ thành phố $n$ đến Bucharest).*

---

### 6.2. Khung Thuật Toán Tìm Kiếm Tốt Nhất Đầu Tiên (Best-First Search)
- Sử dụng hàng đợi ưu tiên `Priority Queue` sắp xếp các nút theo một **hàm đánh giá (Evaluation function)** $f(n)$.
- Nút có giá trị $f(n)$ **nhỏ nhất** (được đánh giá là hứa hẹn nhất) sẽ được chọn lấy ra mở rộng trước.
- Sự khác nhau giữa các thuật toán Heuristic nằm ở cách định nghĩa hàm $f(n)$:
  + **Greedy Best-First Search:** $f(n) = h(n)$
  + **A\* Search:** $f(n) = g(n) + h(n)$

---

### 6.3. Tìm Kiếm Tham Lam (Greedy Best-First Search - GBFS)
- **Hàm đánh giá:** $f(n) = h(n)$.
- **Chiến lược:** Luôn mở rộng nút có vẻ như đang ở gần đích nhất theo ước lượng của Heuristic, hoàn toàn bỏ qua chi phí đường đi đã qua $g(n)$.
- **Đánh giá hiệu năng:**
  + *Tính đầy đủ:*
    * Tree-search: **KHÔNG đầy đủ** (có thể rơi vào vòng lặp vô tận nếu heuristic dẫn dụ tác tử đi vòng quanh).
    * Graph-search: **CÓ đầy đủ** trên không gian trạng thái hữu hạn.
  + *Độ phức tạp thời gian:* Trường hợp xấu nhất $O(b^m)$ (Heuristic tồi dẫn đi lạc vào toàn bộ các nhánh cụt).
  + *Độ phức tạp không gian:* $O(b^m)$ (Lưu toàn bộ các nút trong bộ nhớ).
  + *Tính tối ưu:* **KHÔNG TỐI ƯU!** Giống như một kẻ thiển cận chỉ nhìn thấy lợi ích trước mắt, dễ bị lừa bởi con đường ban đầu tưởng gần nhưng về sau chi phí lại cực lớn.

---

### 6.4. Thuật Toán Tìm Kiếm A\* (A\* Search Algorithm)
- **Hàm đánh giá cốt lõi:**
  $$f(n) = g(n) + h(n)$$
  + $g(n)$: Chi phí thực tế đã đi từ trạng thái bắt đầu tới nút $n$.
  + $h(n)$: Chi phí ước lượng từ nút $n$ đi tiếp tới đích.
  + $\implies f(n)$: **Chi phí ước lượng của lời giải rẻ nhất đi ngang qua nút $n$**.
- A\* kết hợp hoàn hảo ưu điểm của UCS (quan tâm đến chi phí thực tế $g$) và GBFS (dùng tri thức $h$ định hướng tới đích).

```
                     f(n) = g(n) + h(n)
             <------------ Total estimated cost ------------>
            +-------------------------+----------------------+
            |       g(n) (Đã đi)       |     h(n) (Ước tính)  |
            +-------------------------+----------------------+
          Start                     Node n                  Goal
```

---

### 6.5. Điều Kiện Để A\* Đạt Tính Tối Ưu (Conditions for Optimality)

#### 1. Heuristic chấp nhận được (Admissible Heuristic) - Dành cho Tree-Search
- **Định nghĩa:** Heuristic $h(n)$ được gọi là **Admissible (chấp nhận được)** nếu nó **không bao giờ đánh giá quá cao (never overestimates)** chi phí thực tế để đi từ $n$ tới đích:
  $$\forall n: \quad 0 \le h(n) \le h^*(n)$$
  *(Trong đó $h^*(n)$ là chi phí thực tế nhỏ nhất từ $n$ đến đích).*
- Heuristic admissible là một ước lượng lạc quan (optimistic).
- **Định lý 1:** Nếu $h(n)$ là admissible, thuật toán **A\* sử dụng TREE-SEARCH luôn luôn tìm được lời giải tối ưu**.
- **Ý tưởng chứng minh (Proof intuition):**
  + Giả sử một đích dưới tối ưu $G_2$ (với $g(G_2) > C^*$) đang nằm trong `frontier`.
  + Luôn tồn tại một nút $n$ là tổ tiên của đích tối ưu $G_1$ cũng đang nằm trong `frontier`.
  + Vì $h$ là admissible nên: $f(n) = g(n) + h(n) \le g(n) + h^*(n) = C^* < g(G_2) = f(G_2)$.
  + Vì $f(n) < f(G_2)$, thuật toán A\* sẽ luôn luôn lấy nút $n$ ra mở rộng trước khi kịp lấy $G_2$. Do đó, $G_2$ không bao giờ được chọn mở rộng trước $G_1$!

#### 2. Heuristic nhất quán / đơn điệu (Consistent / Monotonic Heuristic) - Dành cho Graph-Search
- **Động lực:** Trong Graph-Search, một khi trạng thái đã nằm trong tập `explored` thì nó sẽ không được đưa vào `frontier` nữa. Nếu một đường đi tốt hơn tới trạng thái đó được tìm thấy sau, đường đi tối ưu sẽ bị bỏ lỡ nếu heuristic không thỏa mãn tính nhất quán!
- **Định nghĩa (Bất đẳng thức tam giác - Triangle Inequality):** Heuristic $h(n)$ được gọi là **Consistent (nhất quán)** nếu với mọi nút $n$ và mọi nút con $n'$ của nó sinh ra bởi hành động $a$:
  $$h(n) \le c(n, a, n') + h(n')$$

```
                           n
                         /   \
           c(n, a, n')  /     \  h(n)
                       v       \
                      n' -----> Goal
                         h(n')
          Bất đẳng thức tam giác: h(n) <= c(n, a, n') + h(n')
```

- **Hệ quả quan trọng bậc nhất:** Giá trị hàm $f(n)$ **không bao giờ giảm** dọc theo bất kỳ nhánh đường đi nào trong cây tìm kiếm:
  $$f(n') = g(n') + h(n') = g(n) + c(n, a, n') + h(n') \ge g(n) + h(n) = f(n)$$
  $$\implies f(n') \ge f(n)$$
- **Định lý 2:** Nếu $h(n)$ là consistent, thuật toán **A\* sử dụng GRAPH-SEARCH luôn luôn tối ưu**!
- **Tính chất vàng:** Khi $h$ consistent, mỗi khi A\* chọn một nút $n$ để mở rộng, **đường đi tới $n$ được đảm bảo đã là đường đi tối ưu nhất tuyệt đối**! Do đó:
  + Không bao giờ cần phải "mở lại" (re-open) các trạng thái đã nằm trong `explored`.
  + Quá trình tìm kiếm của A\* Graph-search diễn ra hoàn toàn chặt chẽ và tuyến tính trên tập trạng thái.
- **Mối quan hệ:** **Mọi Heuristic nhất quán (Consistent) đều là Heuristic chấp nhận được (Admissible)!** Chiều ngược lại không phải lúc nào cũng đúng.

---

### 6.6. Hình Học của A\* và Tính Hiệu Quả Tối Đa (Optimally Efficient)
- **Đường đẳng mức ($f$-contours):**
  + A\* mở rộng các nút theo thứ tự giá trị $f$ tăng dần.
  + Trong khi UCS mở rộng theo các dải hình tròn đồng tâm lan tỏa đều về mọi hướng quanh điểm gốc (vì chỉ dựa vào $g$), thì A\* kéo dài dải đẳng mức **hướng tập trung về phía đích** nhờ có $h(n)$. Heuristic càng chính xác, dải đẳng mức của A\* càng thu hẹp thành một vệt mỏng bám sát đường đi tối ưu.
- **Tính tối ưu tuyệt đối (Optimally Efficient):**
  + A\* mở rộng toàn bộ các nút có $f(n) < C^*$.
  + Không có bất kỳ giải thuật tối ưu nào khác sử dụng cùng hàm heuristic $h$ mà có thể mở rộng **ít nút hơn A\***!

---

### 6.7. Các Biến Thể Tìm Kiếm Heuristic Giới Hạn Bộ Nhớ (Memory-Bounded Heuristic Search)
Nhược điểm lớn nhất của A\* là vẫn phải lưu toàn bộ các nút trong bộ nhớ $\implies$ Hết RAM trước khi hết CPU! Các biến thể giải quyết vấn đề bộ nhớ:

1. **IDA\* (Iterative-Deepening A\*):**
   - Tương tự như IDS, nhưng thay vì cắt theo độ sâu $l$, IDA\* cắt theo **ngưỡng giá trị $f$ (f-cutoff)**.
   - Ở mỗi lượt duyệt, ngưỡng $f$-cutoff cho lượt tiếp theo được đặt bằng **giá trị $f$ nhỏ nhất của các nút bị vượt ngưỡng** ở lượt trước.
   - Bộ nhớ chỉ tốn $O(b \cdot d)$.
2. **RBFS (Recursive Best-First Search):**
   - Thuật toán đệ quy mô phỏng tìm kiếm tốt nhất đầu tiên nhưng chỉ dùng bộ nhớ tuyến tính $O(bd)$.
   - Duy trì biến `f_limit` lưu vết giá trị $f$ của **nhánh thay thế tốt thứ nhì (best alternative path)** có sẵn từ bất kỳ tổ tiên nào. Nếu nút con hiện tại có $f > f\_limit$, thuật toán tự động quay lui để duyệt nhánh thay thế kia.
3. **SMA\* (Simplified Memory-Bounded A\*):**
   - Sử dụng tối đa dung lượng bộ nhớ được cấp phát.
   - Khi bộ nhớ đầy: Tự động **xóa nút lá xấu nhất** (có giá trị $f$ lớn nhất) khỏi cây tìm kiếm, đồng thời lưu lại giá trị $f$ của nút con bị xóa vào nút cha của nó (để khi cần có thể tái sinh lại).

---

### 6.8. Thiết Kế và So Sánh Hàm Heuristic

#### 1. Bài toán 8-Puzzle: So sánh 2 hàm Heuristic
- **$h_1(n)$ - Số ô sai vị trí (Misplaced tiles - Khoảng cách Hamming):** Đếm số lượng ô số không nằm đúng vị trí đích (không tính ô trống). $h_1$ luôn admissible vì mỗi ô sai vị trí phải di chuyển ít nhất 1 lần.
- **$h_2(n)$ - Tổng khoảng cách Manhattan (City block distance):** Tổng khoảng cách dịch chuyển theo chiều ngang và dọc của từng ô số từ vị trí hiện tại về vị trí đích:
  $$h_2(n) = \sum_{i=1}^{8} \left( |x_i - x_i^*| + |y_i - y_i^*| \right)$$
  $h_2$ luôn admissible vì mỗi bước di chuyển chỉ đưa 1 ô lại gần đích tối đa 1 đơn vị khoảng cách.

#### 2. Khái niệm Trội (Heuristic Dominance)
- Cho 2 heuristic admissible $h_1$ và $h_2$. Ta nói **$h_2$ trội hơn $h_1$ ($h_2$ dominates $h_1$)** nếu:
  $$\forall n: \quad h_2(n) \ge h_1(n)$$
- **Hệ quả vàng:** Khi $h_2$ trội hơn $h_1$, thuật toán A\* sử dụng $h_2$ được đảm bảo toán học là **không bao giờ mở rộng nhiều nút hơn** A\* sử dụng $h_1$! ($h_2$ luôn định hướng tìm kiếm tốt hơn và cắt giảm không gian tìm kiếm mạnh mẽ hơn).
- Trong bài toán 8-puzzle: Rõ ràng khoảng cách Manhattan luôn $\ge$ số ô sai vị trí: $h_2(n) \ge h_1(n) \implies h_2$ trội hơn $h_1$.

#### 3. Kỹ thuật Bài toán Nới Lỏng (Relaxed Problems)
- **Định nghĩa:** Một bài toán nới lỏng được tạo ra bằng cách **loại bỏ bớt các ràng buộc trên các hành động** của bài toán gốc.
- **Quy tắc thiết kế:** Chi phí của lời giải tối ưu cho bài toán nới lỏng **luôn là một Heuristic chấp nhận được (Admissible) và nhất quán (Consistent)** cho bài toán gốc!
  + *Ví dụ 8-puzzle:*
    * Ràng buộc gốc: Ô A có thể sang ô B nếu B kề A VÀ B đang trống.
    * Nới lỏng 1: Ô A có thể sang ô B nếu B kề A (bỏ ràng buộc B trống) $\implies$ Ra đời Heuristic khoảng cách Manhattan $h_2$!
    * Nới lỏng 2: Ô A có thể nhảy tới bất kỳ ô nào (bỏ cả kề và trống) $\implies$ Ra đời Heuristic số ô sai vị trí $h_1$!
- **Hợp nhiều Heuristic:** Nếu ta có tập hợp các heuristic admissible $h_1, h_2, \dots, h_k$, thì hàm:
  $$h(n) = \max\{h_1(n), h_2(n), \dots, h_k(n)\}$$
  vừa là một heuristic admissible, vừa **trội hơn tất cả các $h_i$ thành phần**!

---

### 6.9. BÀI TẬP ÁP DỤNG TRACE GIẢI THUẬT GREEDY BEST-FIRST VÀ A\* TRÊN ĐỒ THỊ MẪU

Áp dụng trên Đồ thị chuẩn của đề thi (Start, A, B, C, D, Goal) với các giá trị Heuristic $h$ có sẵn trên các đỉnh:
- $h(\text{Start}) = 0$
- $h(A) = 2$
- $h(B) = 5$
- $h(C) = 2$
- $h(D) = 1$
- $h(\text{Goal}) = 0$

#### BÀI TOÁN 1: TRACE GIẢI THUẬT GREEDY BEST-FIRST SEARCH (GBFS)
*(Tiêu chí ưu tiên: Nút có $f(n) = h(n)$ nhỏ nhất được lấy ra mở rộng trước).*

| Bước | Lấy ra khỏi Frontier (Pop) | $h(n)$ | Explored | Sinh các nút con | Trạng thái Frontier (Sắp xếp theo $h(n)$ tăng dần) |
| :---: | :---: | :---: | :---: | :---: | :---: |
| **0** | *(Khởi tạo)* | - | $\emptyset$ | Nạp gốc Start ($h=0$). | `{(Start, h=0)}` |
| **1** | **Start** | 0 | `{Start}` | - Con $A$: $h(A) = 2$.<br>- Con $B$: $h(B) = 5$.<br>- Con $D$: $h(D) = 1$. | `{(D: 1), (A: 2), (B: 5)}` |
| **2** | **D** | **1** | `{Start, D}` | - Láng giềng của $D$: $B(h=5)$, $C(h=2)$, $\mathbf{Goal(h=0)}$.<br>- Thêm $C(2)$ và $\text{Goal}(0)$ vào Frontier. | `{(Goal: 0), (A: 2), (C: 2), (B: 5)}` |
| **3** | **Goal** | **0** | - | **Kiểm tra đích: Goal reached! Thuật toán DỪNG.** | - |

**Kết luận Greedy Best-First Search:**
- **Thứ tự các trạng thái được mở rộng:**
  $$\mathbf{Start \to D \to Goal}$$
- **Đường đi tìm được:**
  $$\mathbf{Start \to D \to Goal}$$
- **Tổng chi phí đường đi thực tế:**
  $$\text{Cost} = 5 + 5 = \mathbf{10}$$
- **Nhận xét:** GBFS tìm đường rất nhanh (chỉ qua 3 bước), nhưng vì "tham lam" theo giá trị $h(D) = 1$ nên đã bỏ qua nhánh $A$ dẫn đến nghiệm tối ưu có chi phí $8$.

---

#### BÀI TOÁN 2: TRACE GIẢI THUẬT A\* SEARCH (GRAPH SEARCH)
*(Tiêu chí ưu tiên: Nút có $f(n) = g(n) + h(n)$ nhỏ nhất được lấy ra mở rộng trước. Giải hòa bằng thứ tự bảng chữ cái).*

**Bảng trace chi tiết từng bước:**

| Bước | Nút lấy ra (Pop) | $g(n)$ | $h(n)$ | $f(n)$ | Explored Set | Sinh nút con & Tính $f = g + h$ | Frontier (Sắp theo $f$ tăng dần) |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **0** | *(Init)* | 0 | 0 | 0 | $\emptyset$ | Start ($g=0, h=0, f=0$) | `{(Start, f=0, g=0)}` |
| **1** | **Start** | 0 | 0 | 0 | `{Start}` | - $A$: $g=2, h=2 \implies f = 4$. Path: S-A.<br>- $B$: $g=3, h=5 \implies f = 8$. Path: S-B.<br>- $D$: $g=5, h=1 \implies f = 6$. Path: S-D. | `{(A, f=4, g=2), (D, f=6, g=5), (B, f=8, g=3)}` |
| **2** | **A** | 2 | 2 | **4** | `{Start, A}` | - Láng giềng $C$: $g = 2 + 4 = 6$, $h(C) = 2 \implies f = 6 + 2 = 8$. Path: S-A-C. | `{(D, f=6, g=5), (B, f=8, g=3), (C, f=8, g=6)}` |
| **3** | **D** | 5 | 1 | **6** | `{Start, A, D}` | - Con $B$: $g = 5 + 4 = 9 > 3$ (bỏ qua).<br>- Con $C$: $g = 5 + 1 = 6$ (bằng $g(C)$ nhánh A-C, giữ nguyên).<br>- Con $\text{Goal}$: $g = 5 + 5 = 10, h=0 \implies f = 10$. Path: S-D-Goal. | `{(B, f=8, g=3), (C, f=8, g=6), (Goal, f=10, g=10)}` |
| **4** | **B** | 3 | 5 | **8** | `{Start, A, D, B}` | *(Ties giữa B và C cùng có $f=8$: chọn B vì $B < C$ trong bảng chữ cái). Láng giềng đã explored hoặc chi phí cao hơn. Không thêm nút.* | `{(C, f=8, g=6), (Goal, f=10, g=10)}` |
| **5** | **C** | 6 | 2 | **8** | `{Start, A, D, B, C}` | - Láng giềng $\text{Goal}$: $g = 6 + 2 = 8, h=0 \implies f = 8 + 0 = 8$. Path: S-A-C-Goal.<br>- Trong Frontier, $\text{Goal}$ đang có $f=10$ ($g=10$). Vì $8 < 10 \implies$ **CẬP NHẬT $\text{Goal}$ với $g=8, f=8$!** | `{(Goal, f=8, g=8)}` |
| **6** | **Goal** | 8 | 0 | **8** | - | **Kiểm tra đích KHI LẤY RA: Goal reached! Thuật toán DỪNG.** | - |

**Kết luận A\* Search:**
- **Thứ tự các trạng thái được mở rộng (Expanded order):**
  $$\mathbf{Start \to A \to D \to B \to C \to Goal}$$
- **Đường đi tối ưu tìm được (Optimal Solution Path):**
  $$\mathbf{Start \to A \to C \to Goal}$$
- **Tổng chi phí tối ưu:**
  $$\text{Cost} = 2 + 4 + 2 = \mathbf{8}$$

#### BÀI TOÁN 3: KIỂM TRA TÍNH CHẤP NHẬN ĐƯỢC (ADMISSIBLE) VÀ NHẤT QUÁN (CONSISTENT)
Đề bài: Các giá trị heuristic cho trên đồ thị ($h(A)=2, h(B)=5, h(C)=2, h(D)=1, h(Goal)=0$) có thỏa mãn tính Admissible và Consistent không? Hãy chứng minh!

**Lời giải chi tiết:**
1. **Kiểm tra tính Admissible ($0 \le h(n) \le h^*(n)$):**
   - Ta tính khoảng cách thực tế ngắn nhất $h^*(n)$ từ mỗi đỉnh tới Goal:
     + Từ $\text{Goal} \implies h^*(\text{Goal}) = 0$.
     + Từ $C \implies$ đi $C \to \text{Goal}$ có chi phí $2 \implies h^*(C) = 2$.
     + Từ $D \implies$ đi $D \to C \to \text{Goal}$ có chi phí $1 + 2 = 3$ (ngắn hơn đi thẳng $D \to \text{Goal}$ tốn 5) $\implies h^*(D) = 3$.
     + Từ $A \implies$ đi $A \to C \to \text{Goal}$ có chi phí $4 + 2 = 6 \implies h^*(A) = 6$.
     + Từ $B \implies$ đi $B \to D \to C \to \text{Goal}$ có chi phí $4 + 1 + 2 = 7 \implies h^*(B) = 7$.
   - Đối chiếu $h(n)$ với $h^*(n)$:
     + $h(A) = 2 \le h^*(A) = 6$ (Thỏa mãn)
     + $h(B) = 5 \le h^*(B) = 7$ (Thỏa mãn)
     + $h(C) = 2 \le h^*(C) = 2$ (Thỏa mãn, ước lượng hoàn hảo)
     + $h(D) = 1 \le h^*(D) = 3$ (Thỏa mãn)
     + $h(\text{Goal}) = 0 \le h^*(\text{Goal}) = 0$ (Thỏa mãn)
   - **Kết luận:** **$h(n)$ là Heuristic chấp nhận được (Admissible)!**

2. **Kiểm tra tính Consistent ($h(n) \le c(n, a, n') + h(n')$ trên mọi cạnh):**
   - Xét cạnh $A - C$:
     + $h(A) = 2 \le c(A, C) + h(C) = 4 + 2 = 6$ (Đúng).
     + $h(C) = 2 \le c(C, A) + h(A) = 4 + 2 = 6$ (Đúng).
   - Xét cạnh $C - \text{Goal}$:
     + $h(C) = 2 \le c(C, \text{Goal}) + h(\text{Goal}) = 2 + 0 = 2$ (Đúng, dấu bằng xảy ra).
   - Xét cạnh $C - D$:
     + $h(C) = 2 \le c(C, D) + h(D) = 1 + 1 = 2$ (Đúng, dấu bằng xảy ra).
     + $h(D) = 1 \le c(D, C) + h(C) = 1 + 2 = 3$ (Đúng).
   - Xét cạnh $D - \text{Goal}$:
     + $h(D) = 1 \le c(D, \text{Goal}) + h(\text{Goal}) = 5 + 0 = 5$ (Đúng).
   - Xét cạnh $B - D$:
     + $h(B) = 5 \le c(B, D) + h(D) = 4 + 1 = 5$ (Đúng, dấu bằng xảy ra).
     + $h(D) = 1 \le c(D, B) + h(B) = 4 + 5 = 9$ (Đúng).
   - Xét các cạnh nối với Start:
     + $h(\text{Start}) = 0 \le c(\text{Start}, A) + h(A) = 2 + 2 = 4$ (Đúng).
     + $h(\text{Start}) = 0 \le c(\text{Start}, B) + h(B) = 3 + 5 = 8$ (Đúng).
     + $h(\text{Start}) = 0 \le c(\text{Start}, D) + h(D) = 5 + 1 = 6$ (Đúng).
   - **Kết luận:** Tất cả các cạnh đều thỏa mãn bất đẳng thức tam giác $\implies$ **$h(n)$ là Heuristic nhất quán (Consistent)!**
---

## 7. CHƯƠNG 4: TÌM KIẾM CỤC BỘ VÀ BÀI TOÁN TỐI ƯU (LOCAL SEARCH & OPTIMIZATION PROBLEMS)

### 7.1. Phân Biệt Tìm Kiếm Toàn Cục (Global Search) vs. Tìm Kiếm Cục Bộ (Local Search)

| Tiêu chí | Tìm kiếm toàn cục (Global Search) | Tìm kiếm cục bộ (Local Search) |
| :--- | :--- | :--- |
| **Mục tiêu** | Tìm **con đường (Path)** đi từ trạng thái ban đầu tới đích. | Tìm **trạng thái đích / trạng thái tối ưu (State)** thỏa mãn hàm mục tiêu. Con đường dẫn tới trạng thái đó không quan trọng. |
| **Cơ chế lưu trữ** | Lưu toàn bộ cây tìm kiếm / đồ thị tìm kiếm, các nhánh đường đi, tập `frontier` và `explored`. | **Chỉ lưu giữ một trạng thái hiện tại duy nhất** (hoặc một số lượng rất ít trạng thái). Không lưu vết đường đi! |
| **Bộ nhớ (Space)** | Tốn kém từ $O(b \cdot d)$ tới $O(b^d)$. | **Cực kỳ tiết kiệm: $O(1)$ (Hằng số bộ nhớ!)**. |
| **Phạm vi ứng dụng** | Bản đồ, lập kế hoạch hành động theo chuỗi. | Bài toán tối ưu hóa, phân bổ tài nguyên, bài toán gán giá trị thỏa mãn ràng buộc (CSP - 8-queens, lập lịch thi đấu,...). |

---

### 7.2. Cảnh Quan Không Gian Trạng Thái (State-Space Landscape)
Tìm kiếm cục bộ hình dung không gian trạng thái như một địa hình đồi núi trong không gian đa chiều:
- **Tọa độ vị trí (Location):** Đại diện cho một trạng thái cụ thể của bài toán.
- **Độ cao (Elevation):** Giá trị của **hàm mục tiêu (Objective function)** hoặc hàm thích nghi (Fitness function). Nếu bài toán tìm cực tiểu (Cost function), độ cao là chi phí.

```
Elevation ^
          |                     Global Maximum
          |                         /\
          |     Local Maximum      /  \
          |         /\            /    \          Flat Local Maximum (Plateau)
          |        /  \          /      \         +---------------+
          |       /    \  Ridge /        \       /                 \
          |      /      \  /\  /          \     /                   \
          |     /        \/  \/            \---/  Shoulder           \
          +-------------------------------------------------------------> State
```

#### Các thành phần địa hình then chốt (Cạm bẫy của tìm kiếm cục bộ):
1. **Cực đại toàn cục (Global Maximum):** Trạng thái có giá trị hàm mục tiêu cao nhất trên toàn bộ không gian (Lời giải tối ưu hoàn hảo).
2. **Cực đại cục bộ (Local Maximum):** Đỉnh đồi có độ cao cao hơn tất cả các trạng thái láng giềng kề sát nó, nhưng thấp hơn Cực đại toàn cục. *(Khi tác tử leo tới đỉnh này, nhìn xung quanh mọi hướng đều thấy đi xuống $\implies$ Tác tử bị mắc kẹt tưởng đã tới đỉnh cao nhất!)*.
3. **Vùng phẳng / Bình nguyên (Plateau / Flat Local Maximum):** Một vùng đất bằng phẳng mà mọi trạng thái láng giềng đều có cùng độ cao, và không có lối thoát nào dẫn lên dốc.
4. **Bình nguyên vai (Shoulder):** Một vùng đất bằng phẳng nhưng từ đó vẫn tồn tại một hướng có thể tiếp tục leo dốc lên cao hơn.
5. **Dốc gồ ghề (Ridge):** Chuỗi các điểm dốc nhô cao tạo thành sống núi dốc ngược, hai bên sườn núi rất dốc khiến giải thuật leo đồi liên tục dao động zigzag qua lại hai bên sườn núi và tiến triển cực kỳ chậm chạp.

---

### 7.3. Thuật Toán Leo Đồi (Hill-Climbing Search)
- **Bản chất:** Còn gọi là *Tìm kiếm cục bộ tham lam (Greedy local search)*. Tác tử chỉ nhìn quanh các trạng thái láng giềng trực tiếp và luôn chọn bước sang trạng thái có độ dốc tăng cao nhất.
- **Mã giả Leo đồi dốc nhất (Steepest-Ascent Hill-Climbing):**
  ```python
  function HILL-CLIMBING(problem) returns a state that is a local maximum
      current <- problem.INITIAL-STATE
      loop do
          neighbor <- a highest-valued successor of current
          if neighbor.VALUE <= current.VALUE then return current.STATE
          current <- neighbor
  ```
- **Hạn chế:** Trong bài toán 8-queens, leo đồi dốc nhất bị mắc kẹt tại cực đại cục bộ tới **86% trường hợp** (chỉ thành công tìm thấy lời giải 14% số lần chạy)!

#### Các Biến Thể Cải Tiến của Leo Đồi:
1. **Leo đồi cho phép đi ngang (Hill-climbing with sideways moves):**
   - Khi không có láng giềng nào cao hơn, thuật toán cho phép bước sang láng giềng có cùng độ cao (`neighbor.VALUE == current.VALUE`) để cố gắng vượt qua vùng *Shoulder*.
   - *Nguy cơ:* Nếu rơi vào *Plateau* phẳng lì, thuật toán sẽ đi lang thang trong vòng lặp vô tận!
   - *Giải pháp:* Đặt giới hạn tối đa số bước đi ngang liên tiếp (ví dụ tối đa 100 bước). Với bài toán 8-queens, cải tiến này tăng tỷ lệ thành công từ 14% lên tới **94%**!
2. **Leo đồi ngẫu nhiên (Stochastic Hill-Climbing):**
   - Chọn ngẫu nhiên một trong các láng giềng có chiều hướng đi lên dốc, với xác suất được chọn tỷ lệ thuận với độ dốc.
3. **Leo đồi chọn lựa đầu tiên (First-Choice Hill-Climbing):**
   - Sinh ngẫu nhiên từng láng giềng một, ngay khi phát hiện láng giềng đầu tiên có giá trị tốt hơn trạng thái hiện tại thì lập tức bước sang láng giềng đó luôn (rất hiệu quả khi không gian có hàng nghìn láng giềng).
4. **Leo đồi khởi động lại ngẫu nhiên (Random-Restart Hill-Climbing):**
   - Triết lý: *"Nếu lần đầu không thành công, hãy thử lại nhiều lần từ các điểm xuất phát khác nhau!"*.
   - Chạy một chuỗi các lần tìm kiếm leo đồi độc lập, mỗi lần bắt đầu từ một trạng thái khởi tạo ngẫu nhiên.
   - **Tính đầy đủ:** Nếu không gian trạng thái hữu hạn, xác suất tìm ra cực đại toàn cục xấp xỉ $100\%$ khi số lần khởi động lại đủ lớn!

---

### 7.4. Thuật Toán Mô Phỏng Luyện Kim (Simulated Annealing)
- **Cảm hứng vật lý:** Bắt nguồn từ quá trình tôi luyện kim loại trong ngành luyện kim: Nung nóng chảy kim loại lên nhiệt độ rất cao (các nguyên tử dao động hỗn loạn, năng lượng tự do), sau đó **làm nguội từ từ theo một lịch trình kiểm soát** để các nguyên tử sắp xếp vào mạng tinh thể có mức năng lượng thấp nhất, tạo độ cứng cáp hoàn hảo.
- **Cơ chế hoạt động:**
  + Kết hợp giữa *Leo đồi* (khai thác) và *Bước đi ngẫu nhiên - Random walk* (khám phá).
  + Ở mỗi bước, chọn ngẫu nhiên một trạng thái láng giềng $next$.
  + Tính độ chênh lệch năng lượng / giá trị: $\Delta E = next.VALUE - current.VALUE$.
  + **Quy tắc chấp nhận nước đi:**
    1. Nếu $\Delta E > 0$ (Nước đi tốt hơn): **LUÔN LUÔN CHẤP NHẬN BƯỚC ĐI!**
    2. Nếu $\Delta E \le 0$ (Nước đi tồi hơn): Vẫn **chấp nhận với một xác suất $P$**:
       $$P = e^{\frac{\Delta E}{T}}$$
       *(Trong đó $T$ là Nhiệt độ hiện tại, được giảm dần theo thời gian qua hàm Lịch trình nhiệt độ `schedule(t)`).*

```
           Xác suất chấp nhận nước đi tồi: P = exp(delta_E / T)
           - Khi T rất lớn (mới bắt đầu): P xấp xỉ 1 (Nhảy tự do thoát cực tiểu cục bộ)
           - Khi T giảm dần về 0:        P xấp xỉ 0 (Hoạt động như leo đồi thuần túy)
```

- **Định lý hội tụ:** Nếu lịch trình làm nguội hạ nhiệt độ $T$ đủ chậm, thuật toán Simulated Annealing **được đảm bảo toán học sẽ tìm ra trạng thái tối ưu toàn cục** với xác suất tiệm cận 1!

---

### 7.5. Tìm Kiếm Chùm Cục Bộ (Local Beam Search)
- Thay vì chỉ giữ 1 trạng thái duy nhất, thuật toán duy trì đồng thời **$k$ trạng thái**.
- **Điểm khác biệt cốt lõi giữa Local Beam Search và $k$ lần chạy Random-Restart độc lập:**
  + Trong $k$ lần chạy độc lập: Các luồng tìm kiếm hoàn toàn cô lập, không trao đổi thông tin với nhau.
  + Trong Local Beam Search: **Có sự trao đổi và chia sẻ thông tin!** Ở mỗi bước, thuật toán sinh tất cả các láng giềng của cả $k$ trạng thái, sau đó tập hợp lại và chỉ giữ lấy **$k$ trạng thái tốt nhất trên toàn bộ tập láng giềng đó**.
  + Nếu một nhánh tìm thấy vùng đất màu mỡ hứa hẹn, toàn bộ chùm tìm kiếm sẽ tự động dồn trọng tâm về khu vực đó!
- **Stochastic Beam Search:** Thay vì chọn cứng $k$ trạng thái đứng đầu, thuật toán chọn $k$ trạng thái với xác suất tỷ lệ thuận với giá trị hàm mục tiêu (giống chọn lọc tự nhiên).

---

### 7.6. Thuật Giải Di Truyền (Genetic Algorithms - GA)
- **Bản chất:** Là một biến thể của *Stochastic Beam Search*, lấy cảm hứng từ thuyết tiến hóa tự nhiên của Charles Darwin (sự sống sót của cá thể thích nghi nhất).

```
          Quần thể P(t) ---> Đánh giá Fitness ---> Chọn lọc (Selection)
                                                        |
          Quần thể mới P(t+1) <-- Đột biến <-- Lai ghép (Crossover)
```

#### Bốn thành phần cốt lõi của Thuật giải Di truyền:
1. **Biểu diễn cá thể (Individual / Chromosome):** Mỗi trạng thái được mã hóa thành một chuỗi (chuỗi bit 0-1, hoặc chuỗi số nguyên).
   - *Ví dụ bài toán 4-queens:* Mã hóa bằng chuỗi 4 chữ số, mỗi chữ số biểu thị vị trí hàng của quân hậu trong cột đó (từ 1 đến 4). Trạng thái $S = 2341$ nghĩa là cột 1 hậu ở hàng 2, cột 2 ở hàng 3, cột 3 ở hàng 4, cột 4 ở hàng 1.
2. **Hàm thích nghi (Fitness Function $Fit(n)$):** Đánh giá mức độ sống sót của cá thể (càng cao càng tốt).
   - Trong bài toán $n$-queens, $Fit(n)$ được tính bằng **Số cặp quân hậu KHÔNG tấn công nhau**.
   - Với 4 quân hậu, tổng số cặp là $C_4^2 = \frac{4 \times 3}{2} = 6$.
     $$Fit(n) = 6 - (\text{Số cặp tấn công nhau})$$
     *(Cá thể tối ưu có $Fit(n) = 6$).*
3. **Toán tử Chọn lọc (Selection - Vòng quay Roulette Wheel):**
   - Các cá thể trong quần thể được chọn làm cha mẹ với xác suất tỷ lệ thuận với điểm thích nghi của chúng:
     $$P(i) = \frac{Fit(i)}{\sum_{j=1}^{k} Fit(j)}$$
   - Cá thể có điểm thích nghi càng cao thì diện tích ô trên vòng quay Roulette càng lớn $\implies$ Xác suất được nhân giống thế hệ sau càng cao.
4. **Toán tử Lai ghép (Crossover):**
   - Ghép cặp 2 cá thể cha mẹ ngẫu nhiên.
   - Chọn một **điểm cắt (Crossover point)** ngẫu nhiên trên chuỗi gen.
   - Hoán đổi đoạn đuôi gen cho nhau để sinh ra 2 cá thể con mới thừa hưởng phẩm chất của cả cha và mẹ.
5. **Toán tử Đột biến (Mutation):**
   - Với một xác suất rất nhỏ $p_m$ (ví dụ 0.1%), một gen bất kỳ trong chuỗi bị thay đổi giá trị ngẫu nhiên.
   - Ý nghĩa: Giữ gìn tính đa dạng di truyền của quần thể, ngăn ngừa quần thể bị hội tụ sớm vào cực trị cục bộ.

---

### 7.7. GIẢI CHI TIẾT BÀI TẬP VÀ QUIZ TRONG LECTURE 04

#### BÀI TẬP 1 (QUIZ 01 - SLIDE 19): BÀI TOÁN 4-QUEENS BẰNG FIRST-CHOICE / STEEPEST HILL-CLIMBING
Đề bài: Cho bài toán 4-queens, áp dụng giải thuật leo đồi để tìm lời giải, sử dụng hàm Heuristic là "Số cặp quân hậu tấn công nhau" (mục tiêu tối ưu hóa: Điểm số $\text{Score} = -\text{Số cặp tấn công nhau}$). Phân tích các bước chuyển trạng thái trong hình ảnh slide 19.

**Phân tích quá trình giải qua từng bước (Steps):**
- **Quy tắc tính số cặp hậu tấn công:** 2 quân hậu tại $(c_1, r_1)$ và $(c_2, r_2)$ tấn công nhau nếu:
  1. Cùng hàng: $r_1 == r_2$
  2. Cùng đường chéo: $|r_1 - r_2| == |c_1 - c_2|$

**Chi tiết từng bước chuyển trạng thái (Slide 19):**
1. **Step 0 (Trạng thái ban đầu):**
   - Cả 4 quân hậu đều nằm trên hàng 0: $(A0, B0, C0, D0)$.
   - Tất cả 4 quân hậu đều tấn công lẫn nhau trên cùng hàng 0.
   - Số cặp tấn công: $C_4^2 = 6$ cặp.
   - $\implies \mathbf{Score = -6}$.
2. **Step 1 (Di chuyển quân hậu cột B):**
   - Xem xét di chuyển quân hậu ở cột B xuống các hàng 1, 2, 3:
     + Chuyển B xuống hàng 1 $\implies$ Score = -4.
     + Chuyển B xuống hàng 2 $\implies$ Score = -4.
     + Chuyển B xuống hàng 3: Cấu hình $(A0, B3, C0, D0)$.
       * Các cặp tấn công: Hậu A0 tấn công C0, A0 tấn công D0, C0 tấn công D0 $\implies$ 3 cặp tấn công.
       * Hậu B3 không tấn công ai (hàng 3 độc lập, đường chéo không vướng hậu nào).
       * $\implies \mathbf{Score = -3}$ *(Bước đi tốt nhất, được khoanh tròn xanh!)*.
3. **Step 2 (Di chuyển quân hậu cột D):**
   - Từ trạng thái $(A0, B3, C0, D0)$ có Score = -3, di chuyển quân hậu cột D:
     + Chuyển D xuống hàng 2: Cấu hình $(A0, B3, C0, D2)$.
     * Kiểm tra xung đột:
       - Hàng: A0 và C0 cùng hàng 0 (1 cặp).
       - B3 và D2: $|3 - 2| = 1 \ne |2 - 4| = 2$ (không trùng đường chéo).
       - C0 và D2: $|0 - 2| = 2 == |3 - 4| = 1$ (sai, không trùng).
       - A0 và D2: $|0 - 2| = 2 \ne |1 - 4| = 3$.
     * Chỉ còn duy nhất 1 cặp tấn công giữa A0 và C0!
     * $\implies \mathbf{Score = -1}$ *(Nước đi tốt nhất, được khoanh tròn xanh!)*.
4. **Step 3 (Di chuyển quân hậu cột A):**
   - Từ trạng thái $(A0, B3, C0, D2)$ có Score = -1, di chuyển quân hậu cột A xuống hàng 1:
     + Cấu hình mới: $(A1, B3, C0, D2)$.
     + Kiểm tra:
       - Hàng: Các hàng là 1, 3, 0, 2 (hoàn toàn phân biệt, không trùng hàng!).
       - Đường chéo: Không có bất kỳ cặp nào thỏa $|r_i - r_j| == |c_i - c_j|$!
       - Số cặp tấn công = 0.
     + $\implies \mathbf{Score = 0}$ *(ĐẠT ĐÍCH TỐI ƯU TOÀN CỤC!)*.

---

#### BÀI TẬP 2 (QUIZ 02 - SLIDE 33): TÍNH ĐIỂM FITNESS VÀ XÁC SUẤT CHỌN LỌC ROULETTE WHEEL
Đề bài: Xét bài toán 4-queens, mỗi trạng thái được biểu diễn bởi một chuỗi 4 chữ số (vị trí hàng của hậu trong cột từ 1 đến 4).
Hàm thích nghi:
$$Fit(n) = \text{Số cặp quân hậu KHÔNG tấn công nhau} = 6 - (\text{Số cặp tấn công nhau})$$
Cho thế hệ hiện tại gồm 4 cá thể:
$$S_1 = 2341, \quad S_2 = 2132, \quad S_3 = 1232, \quad S_4 = 4321$$
Hãy tính giá trị $Fit(n)$ cho từng trạng thái và tính xác suất mỗi trạng thái được chọn trong bước Chọn lọc (Selection).

**Lời giải chi tiết từng cá thể:**

##### 1. Xét cá thể $S_1 = 2341$:
- Tọa độ 4 hậu: $(c_1=1, r_1=2)$, $(c_2=2, r_2=3)$, $(c_3=3, r_3=4)$, $(c_4=4, r_4=1)$.
- Kiểm tra toàn bộ 6 cặp:
  + Cặp (1, 2): $|2 - 3| = 1 == |1 - 2| = 1 \implies$ **Tấn công chéo!**
  + Cặp (1, 3): $|2 - 4| = 2 == |1 - 3| = 2 \implies$ **Tấn công chéo!**
  + Cặp (1, 4): $|2 - 1| = 1 \ne |1 - 4| = 3$ (An toàn).
  + Cặp (2, 3): $|3 - 4| = 1 == |2 - 3| = 1 \implies$ **Tấn công chéo!**
  + Cặp (2, 4): $|3 - 1| = 2 == |2 - 4| = 2 \implies$ **Tấn công chéo!**
  + Cặp (3, 4): $|4 - 1| = 3 \ne |3 - 4| = 1$ (An toàn).
- Tổng số cặp tấn công = 4 cặp.
- $\implies \mathbf{Fit(S_1) = 6 - 4 = 2}$.

##### 2. Xét cá thể $S_2 = 2132$:
- Tọa độ: $(1, 2), (2, 1), (3, 3), (4, 2)$.
- Kiểm tra các cặp:
  + Cặp (1, 2): $|2 - 1| = 1 == |1 - 2| = 1 \implies$ **Tấn công chéo!**
  + Cặp (1, 3): $|2 - 3| = 1 \ne |1 - 3| = 2$ (An toàn).
  + Cặp (1, 4): $r_1 = r_4 = 2 \implies$ **Tấn công cùng hàng 2!**
  + Cặp (2, 3): $|1 - 3| = 2 == |2 - 3| = 1$ (Sai, an toàn).
  + Cặp (2, 4): $|1 - 2| = 1 \ne |2 - 4| = 2$ (An toàn).
  + Cặp (3, 4): $|3 - 2| = 1 == |3 - 4| = 1 \implies$ **Tấn công chéo!**
- Tổng số cặp tấn công = 3 cặp.
- $\implies \mathbf{Fit(S_2) = 6 - 3 = 3}$.

##### 3. Xét cá thể $S_3 = 1232$:
- Tọa độ: $(1, 1), (2, 2), (3, 3), (4, 2)$.
- Kiểm tra các cặp:
  + Cặp (1, 2): $|1 - 2| = 1 == |1 - 2| = 1 \implies$ **Tấn công chéo!**
  + Cặp (1, 3): $|1 - 3| = 2 == |1 - 3| = 2 \implies$ **Tấn công chéo!**
  + Cặp (1, 4): $|1 - 2| = 1 \ne |1 - 4| = 3$ (An toàn).
  + Cặp (2, 3): $|2 - 3| = 1 == |2 - 3| = 1 \implies$ **Tấn công chéo!**
  + Cặp (2, 4): $r_2 = r_4 = 2 \implies$ **Tấn công cùng hàng 2!**
  + Cặp (3, 4): $|3 - 2| = 1 == |3 - 4| = 1 \implies$ **Tấn công chéo!**
- Tổng số cặp tấn công = 5 cặp.
- $\implies \mathbf{Fit(S_3) = 6 - 5 = 1}$.

##### 4. Xét cá thể $S_4 = 4321$:
- Tọa độ: $(1, 4), (2, 3), (3, 2), (4, 1)$.
- Cả 4 quân hậu nằm chính xác trên cùng một đường chéo chính giảm dần!
- Tất cả các cặp (1,2), (1,3), (1,4), (2,3), (2,4), (3,4) đều tấn công chéo lẫn nhau!
- Tổng số cặp tấn công = 6 cặp.
- $\implies \mathbf{Fit(S_4) = 6 - 6 = 0}$.

---

#### BẢNG TỔNG HỢP VÀ TÍNH XÁC SUẤT CHỌN LỌC ROULETTE WHEEL:
- **Tổng điểm thích nghi toàn quần thể:**
  $$\sum_{i=1}^{4} Fit(S_i) = Fit(S_1) + Fit(S_2) + Fit(S_3) + Fit(S_4) = 2 + 3 + 1 + 0 = \mathbf{6}$$

| Cá thể ($i$) | Mã hóa trạng thái | Số cặp tấn công | Điểm thích nghi $Fit(S_i)$ | Công thức xác suất $P(S_i)$ | Xác suất chọn lọc (%) |
| :---: | :---: | :---: | :---: | :---: | :---: |
| **$S_1$** | `2341` | 4 | **2** | $P(S_1) = \frac{2}{6} = \frac{1}{3}$ | **33.33%** |
| **$S_2$** | `2132` | 3 | **3** | $P(S_2) = \frac{3}{6} = \frac{1}{2}$ | **50.00%** |
| **$S_3$** | `1232` | 5 | **1** | $P(S_3) = \frac{1}{6}$ | **16.67%** |
| **$S_4$** | `4321` | 6 | **0** | $P(S_4) = \frac{0}{6} = 0$ | **0.00%** |
| **Tổng cộng** | - | - | **6** | $\sum P = 1.0$ | **100%** |

> **Nhận xét quan trọng:**
> - Cá thể $S_2$ có độ thích nghi cao nhất ($Fit = 3$) chiếm tới 50% cơ hội được chọn nhân giống.
> - Cá thể $S_4$ xung đột toàn bộ ($Fit = 0$) có 0% cơ hội được chọn $\implies$ Bị loại bỏ hoàn toàn khỏi quá trình tiến hóa tự nhiên theo đúng nguyên lý của Darwin!
---

## 8. CHƯƠNG 5: TÌM KIẾM ĐỐI KHÁNG VÀ TRÒ CHƠI (ADVERSARIAL SEARCH)

### 8.1. Khái Niệm Trò Chơi Trong Trí Tuệ Nhân Tạo
- **Môi trường đối kháng (Adversarial Environment):** Là môi trường đa tác tử có tính **cạnh tranh (Competitive)**, trong đó mục tiêu của các tác tử xung đột trực tiếp với nhau. Nước đi của tác tử này nhằm tối đa hóa lợi ích của mình đồng thời triệt tiêu lợi ích của đối thủ.
- **Phân loại trò chơi trong AI:**
  + **Xác định (Deterministic) vs. Ngẫu nhiên (Stochastic):**
    * *Xác định:* Cờ vua (Chess), Cờ đam (Checkers), Cờ vây (Go), Cờ ca-rô (Tic-Tac-Toe).
    * *Ngẫu nhiên:* Cờ cá ngựa, Cờ thỏ cáo (Backgammon), Monopoly (có đổ xúc xắc).
  + **Thông tin hoàn hảo (Perfect Information) vs. Thông tin không hoàn hảo (Imperfect Information):**
    * *Thông tin hoàn hảo:* Người chơi quan sát được toàn bộ bàn cờ tại mọi thời điểm (Chess, Go).
    * *Thông tin không hoàn hảo:* Có thông tin ẩn khuất, bài giấu kín (Poker, Tam cúc, Battleship).

---

### 8.2. Hình Thức Hóa Bài Toán Trò Chơi (Game Formalization)
Xét trò chơi đối kháng 2 người, tuần tự theo lượt, có tổng độ lợi bằng không (**Two-player Zero-Sum Game**), quy ước 2 người chơi là **MAX** (đại diện cho tác tử AI, muốn tối đa hóa điểm) và **MIN** (đại diện cho đối thủ, muốn tối thiểu hóa điểm của MAX):

1. **Trạng thái ban đầu ($s_0$):** Cấu hình bàn cờ ban đầu và lượt người đi trước.
2. **Hàm người chơi ($Player(s)$):** Xác định người chơi nào có lượt đi tại trạng thái $s$ (MAX hoặc MIN).
3. **Tập nước đi hợp lệ ($Actions(s)$):** Tập hợp các nước đi khả thi tại trạng thái $s$.
4. **Mô hình chuyển trạng thái ($Result(s, a)$):** Trạng thái bàn cờ sau khi người chơi thực hiện nước đi $a$.
5. **Kiểm tra kết thúc ($Terminal\text{-}Test(s)$):** Đúng nếu trò chơi đã kết thúc (thắng, thua, hòa); Sai nếu ván đấu vẫn đang tiếp tục.
   *(Các trạng thái kết thúc được gọi là Nút lá - Terminal States).*
6. **Hàm độ lợi ($Utility(s, p)$):** Trả về giá trị số học (Payoff) cho người chơi $p$ tại trạng thái kết thúc $s$.
   - *Ví dụ cờ vua:* $+1$ (MAX thắng), $-1$ (MIN thắng), $0$ (Hòa).

---

### 8.3. Thuật Toán Minimax (The Minimax Algorithm)
- **Mục tiêu:** Tìm ra nước đi tối ưu nhất cho người chơi MAX với giả định rằng **đối thủ MIN cũng là một người chơi thông minh tuyệt đối (Optimal Opponent)** luôn chọn nước đi có lợi nhất cho nó (tức gây hại nhất cho MAX).
- **Định nghĩa đệ quy Giá trị Minimax ($Minimax(s)$):**
  $$Minimax(s) = \begin{cases} Utility(s) & \text{nếu } Terminal(s) \\ \max_{a \in Actions(s)} Minimax(Result(s, a)) & \text{nếu } Player(s) = MAX \\ \min_{a \in Actions(s)} Minimax(Result(s, a)) & \text{nếu } Player(s) = MIN \end{cases}$$

```
                MAX                    /\  (Chọn giá trị MAX từ các con)
                                      /  \
                                     /    \
                MIN                 \/    \/ (Chọn giá trị MIN từ các con)
                                   /  \  /  \
                TERMINAL          3   12 2   6 (Giá trị Utility tại lá)
```

- **Mã giả Thuật toán Minimax:**
  ```python
  function MINIMAX-DECISION(state) returns an action
      return argmax a in ACTIONS(state) [ MIN-VALUE(RESULT(state, a)) ]

  function MAX-VALUE(state) returns a utility value
      if TERMINAL-TEST(state) then return UTILITY(state)
      v = -infinity
      for each a in ACTIONS(state) do
          v = max(v, MIN-VALUE(RESULT(state, a)))
      return v

  function MIN-VALUE(state) returns a utility value
      if TERMINAL-TEST(state) then return UTILITY(state)
      v = +infinity
      for each a in ACTIONS(state) do
          v = min(v, MAX-VALUE(RESULT(state, a)))
      return v
  ```
- **Tính chất của Minimax:**
  + *Tính đầy đủ:* **CÓ** nếu cây trò chơi hữu hạn.
  + *Tính tối ưu:* **CÓ** (khi đối đầu với đối thủ chơi tối ưu). Nếu đối thủ chơi dưới tối ưu, Minimax vẫn đảm bảo không thua và điểm số chỉ có thể tốt hơn hoặc bằng điểm kỳ vọng!
  + *Độ phức tạp thời gian:* $O(b^m)$ ($b$ là số nước đi hợp lệ mỗi lượt, $m$ là độ sâu tối đa của ván đấu). Duyệt toàn bộ cây theo cơ chế DFS.
  + *Độ phức tạp không gian:* $O(bm)$ (Bộ nhớ tuyến tính của DFS).

---

### 8.4. Thuật Toán Cắt Tỉa Alpha-Beta ($\alpha$-$\beta$ Pruning)
- **Ý nghĩa sống còn:** Cây trò chơi thực tế có kích thước khổng lồ ($b \approx 35, m \approx 80$ trong cờ vua $\implies 35^{80}$ trạng thái, lớn hơn số nguyên tử trong vũ trụ). Minimax thuần túy không thể duyệt hết!
- **Nguyên lý cắt tỉa:** Bỏ qua (cắt tỉa) các nhánh con mà ta **chắc chắn không ảnh hưởng đến quyết định cuối cùng của nút gốc**, qua đó tiết kiệm đáng kể thời gian tính toán mà **KHÔNG làm mất tính tối ưu**.

#### Định Nghĩa Hai Biến Alpha ($\alpha$) và Beta ($\beta$):
- **$\alpha$ (Alpha):** Giá trị của lựa chọn **tốt nhất (lớn nhất)** mà người chơi **MAX** đã tìm thấy từ đầu đến nay dọc theo đường đi từ gốc tới nút hiện tại.
  + Ban đầu: $\alpha = -\infty$.
  + Chỉ được cập nhật tăng lên tại các **Nút MAX**.
- **$\beta$ (Beta):** Giá trị của lựa chọn **tốt nhất (nhỏ nhất)** mà người chơi **MIN** đã tìm thấy từ đầu đến nay dọc theo đường đi từ gốc tới nút hiện tại.
  + Ban đầu: $\beta = +\infty$.
  + Chỉ được cập nhật giảm đi tại các **Nút MIN**.

```
    CỬA SỔ TÌM KIẾM: [alpha, beta]
    - Nút MAX: Luôn tìm cách nâng sàn alpha lên:    alpha = max(alpha, v)
    - Nút MIN: Luôn tìm cách hạ trần beta xuống:    beta  = min(beta,  v)
```

#### Quy Tắc Cắt Tỉa (Pruning Conditions):
1. **Cắt tỉa Alpha (Alpha Cutoff) tại Nút MIN:**
   - Tại một nút MIN, sau khi tính được giá trị con $v$, nếu:
     $$v \le \alpha$$
     $\implies$ **DỪNG MỞ RỘNG CÁC CON CÒN LẠI CỦA NÚT MIN NÀY NGAY LẬP TỨC!**
   - *Giải thích bản chất:* Vì nút cha (hoặc tổ tiên) là MAX đã có sẵn một lựa chọn khác mang lại giá trị ít nhất là $\alpha$. Tại nút MIN này, giá trị của nó chắc chắn sẽ $\le v \le \alpha$. Người chơi MAX ở trên sẽ không đời nào chọn đi vào nhánh này $\implies$ Khám phá thêm các con còn lại là vô ích!
2. **Cắt tỉa Beta (Beta Cutoff) tại Nút MAX:**
   - Tại một nút MAX, sau khi tính được giá trị con $v$, nếu:
     $$v \ge \beta$$
     $\implies$ **DỪNG MỞ RỘNG CÁC CON CÒN LẠI CỦA NÚT MAX NÀY NGAY LẬP TỨC!**
   - *Giải thích bản chất:* Vì tổ tiên MIN ở trên đã có một lựa chọn khác mang lại giá trị tối đa là $\beta$. Tại nút MAX này, nó sẽ chọn giá trị $\ge v \ge \beta$. Người chơi MIN ở trên chắc chắn sẽ né tránh nhánh này $\implies$ Cắt tỉa ngay!

- **Mã giả Cắt tỉa Alpha-Beta:**
  ```python
  function ALPHA-BETA-SEARCH(state) returns an action
      v = MAX-VALUE(state, -infinity, +infinity)
      return action in ACTIONS(state) with value v

  function MAX-VALUE(state, alpha, beta) returns a utility value
      if TERMINAL-TEST(state) then return UTILITY(state)
      v = -infinity
      for each a in ACTIONS(state) do
          v = max(v, MIN-VALUE(RESULT(state, a), alpha, beta))
          if v >= beta then return v     # Beta cutoff!
          alpha = max(alpha, v)
      return v

  function MIN-VALUE(state, alpha, beta) returns a utility value
      if TERMINAL-TEST(state) then return UTILITY(state)
      v = +infinity
      for each a in ACTIONS(state) do
          v = min(v, MAX-VALUE(RESULT(state, a), alpha, beta))
          if v <= alpha then return v    # Alpha cutoff!
          beta = min(beta, v)
      return v
  ```

#### Hiệu Quả và Tầm Quan Trọng của Thứ Tự Nước Đi (Move Ordering):
- Cắt tỉa Alpha-Beta **không làm thay đổi kết quả cuối cùng** so với Minimax.
- **Trường hợp xấu nhất:** Các nước đi tốt nhất lại nằm ở nhánh cuối cùng duyệt tới $\implies$ Không cắt tỉa được gì, độ phức tạp vẫn là $O(b^m)$.
- **Trường hợp lý tưởng (Nước đi hoàn hảo - Best moves examined first):**
  + Độ phức tạp thời gian giảm ngoạn mục xuống còn:
    $$O(b^{m/2}) = O\left((\sqrt{b})^m\right)$$
  + Hệ số phân nhánh hiệu dụng giảm từ $b$ xuống chỉ còn $\sqrt{b}$ (Với cờ vua: $b \approx 35 \implies \sqrt{35} \approx 6$).
  + **Ý nghĩa thực tiễn:** Cho phép AI **tìm kiếm sâu gấp đôi (2x depth)** trong cùng một quỹ thời gian tính toán!

---

### 8.5. Quyết Định Thời Gian Thực Không Hoàn Hảo (Heuristic Minimax)
Trong các trò chơi phức tạp, không thể duyệt cây đến tận nút lá kết thúc. Giải pháp:
1. **Hàm cắt tỉa độ sâu ($Cutoff\text{-}Test(s, d)$):** Thay vì $Terminal\text{-}Test$, dừng tìm kiếm khi đạt đến một độ sâu giới hạn $d$.
2. **Hàm đánh giá Heuristic ($Eval(s)$):** Thay thế cho $Utility(s)$ tại các nút bị cắt ngang. Ước lượng cơ hội chiến thắng của trạng thái đó.
   - Thường biểu diễn dưới dạng tổng tuyến tính có trọng số các đặc trưng bàn cờ:
     $$Eval(s) = w_1 f_1(s) + w_2 f_2(s) + \dots + w_n f_n(s)$$
     *(Ví dụ cờ vua: $f_i$ là số lượng từng loại quân cờ: tốt $w=1$, mã/tượng $w=3$, xe $w=5$, hậu $w=9$; độ an toàn của vua; quyền kiểm soát trung tâm).*
3. **Các cạm bẫy và kỹ thuật khắc phục:**
   - **Tìm kiếm tĩnh lặng (Quiescence Search):** Không được dừng ngắt độ sâu đột ngột tại các trạng thái đang có biến động mạnh (ví dụ: đang trong chuỗi bắt quân qua lại). Phải tiếp tục duyệt thêm các nước đi ăn quân cho đến khi thế cờ đạt trạng thái "tĩnh lặng" (quiescent) thì mới áp dụng $Eval(s)$.
   - **Hiện tượng đường chân trời (Horizon Effect):** Xảy ra khi một biến cố thảm họa không thể tránh khỏi (ví dụ mất quân hậu) bị trì hoãn tạm thời bằng cách thực hiện các nước chiếu vô nghĩa, đẩy biến cố ra sau "đường chân trời" của độ sâu tìm kiếm.

---

### 8.6. Trò Chơi Ngẫu Nhiên và Thuật Toán Expectiminimax
- Trong các trò chơi có yếu tố may rủi (đổ xúc xắc, chia bài), cây trò chơi xuất hiện thêm một tầng nút mới gọi là **Nút ngẫu nhiên (Chance Nodes)**, thường được vẽ bằng hình tròn.
- **Công thức Expectiminimax:**
  $$Expectiminimax(s) = \begin{cases} Utility(s) & \text{nếu } Terminal(s) \\ \max_a Expectiminimax(Result(s, a)) & \text{nếu } Player(s) = MAX \\ \min_a Expectiminimax(Result(s, a)) & \text{nếu } Player(s) = MIN \\ \sum_{r} P(r) \cdot Expectiminimax(Result(s, r)) & \text{nếu } Player(s) = CHANCE \end{cases}$$
  *(Trong đó $P(r)$ là xác suất xảy ra của kết quả ngẫu nhiên $r$).*
- **Độ phức tạp:** $O(b^m \cdot n^m)$ (với $n$ là số kết quả ngẫu nhiên có thể có tại mỗi nút Chance).

---

### 8.7. GIẢI CHI TIẾT BÀI TẬP VÀ VÍ DỤ TRONG LECTURE 05

#### BÀI TẬP 1 (SLIDE 19): TÍNH TOÁN MINIMAX TRÊN CÂY TRÒ CHƠI 2-PLY
Đề bài: Cho cây trò chơi 2 tầng (2-ply) như hình ảnh Slide 19. Gốc là nút MAX $A$.
- Nút $A$ có 3 nhánh rẽ: $a_1$ (dẫn tới nút MIN $B$), $a_2$ (dẫn tới nút MIN $C$), $a_3$ (dẫn tới nút MIN $D$).
- Nút MIN $B$ có 3 nút con lá với giá trị: $\{3, 12, 8\}$.
- Nút MIN $C$ có 3 nút con lá với giá trị: $\{2, 4, 6\}$.
- Nút MIN $D$ có 3 nút con lá với giá trị: $\{14, 5, 2\}$.
Hãy tính giá trị Minimax cho tất cả các nút và xác định nước đi tối ưu của MAX.

```
                         MAX A [ ? ]
                       /      |      \
                  a1  /    a2 |    a3 \
                     v        v        v
          MIN     B [ ? ]  C [ ? ]  D [ ? ]
                 /   |  \  /  |  \  /  |  \
          LEAF  3   12  8 2   4  6 14  5  2
```

**Quá trình tính toán chi tiết từ dưới lên:**
1. **Tại các nút tầng MIN (Chọn giá trị nhỏ nhất của các con):**
   - Giá trị tại nút $B$:
     $$V(B) = \min(3, 12, 8) = \mathbf{3}$$
   - Giá trị tại nút $C$:
     $$V(C) = \min(2, 4, 6) = \mathbf{2}$$
   - Giá trị tại nút $D$:
     $$V(D) = \min(14, 5, 2) = \mathbf{2}$$
2. **Tại nút gốc tầng MAX (Chọn giá trị lớn nhất của các con):**
   - Nút $A$ nhận 3 giá trị truyền lên từ $B, C, D$:
     $$V(A) = \max(V(B), V(C), V(D)) = \max(3, 2, 2) = \mathbf{3}$$
3. **Quyết định nước đi tối ưu của MAX:**
   - Nút $A$ đạt giá trị lớn nhất là 3 khi đi theo nhánh $a_1$ tới nút $B$.
   - $\implies$ **Nước đi tối ưu của MAX là $a_1$**.

---

#### BÀI TẬP 2 (SLIDE 27 & 28): TRACE CHI TIẾT CẮT TỈA ALPHA-BETA TỪNG BƯỚC
Đề bài: Áp dụng giải thuật Cắt tỉa Alpha-Beta trên cây trò chơi ở Bài tập 1. Thể hiện chi tiết sự biến thiên của khoảng $[\alpha, \beta]$ tại mỗi nút và chỉ ra chính xác các nhánh bị cắt tỉa.

**Quá trình duyệt chi tiết theo 6 giai đoạn (tương ứng (a) đến (f) trong Slide 27):**

1. **Giai đoạn (a): Khởi tạo và đi xuống nhánh trái nhất (Nút B):**
   - Nút gốc $A$ khởi tạo: $\alpha = -\infty, \beta = +\infty$.
   - Truyền cửa sổ $[\alpha = -\infty, \beta = +\infty]$ xuống nút MIN $B$.
   - Duyệt lá đầu tiên của $B$ có giá trị **3**:
     + $B$ là nút MIN $\implies$ Cập nhật $\beta = \min(+\infty, 3) = 3$.
     + Khoảng tại $B$ hiện tại là: $[\alpha = -\infty, \beta = 3]$.
2. **Giai đoạn (b): Duyệt tiếp các lá của B:**
   - Duyệt lá thứ hai có giá trị **12**:
     + $B$ là nút MIN: $\beta = \min(3, 12) = 3$ (Không đổi).
3. **Giai đoạn (c): Hoàn tất nút B và trả về gốc A:**
   - Duyệt lá thứ ba có giá trị **8**:
     + $\beta = \min(3, 8) = 3$.
   - Nút $B$ duyệt xong toàn bộ con, trả giá trị $V(B) = 3$ về cho $A$.
   - **Tại nút MAX A:**
     + Cập nhật $\alpha = \max(\alpha, V(B)) = \max(-\infty, 3) = \mathbf{3}$.
     + Cửa sổ tìm kiếm tại $A$ trở thành: $[\mathbf{\alpha = 3}, \beta = +\infty]$.
4. **Giai đoạn (d): Đi xuống nhánh giữa (Nút C) - XẢY RA CẮT TỈA!**
   - Nút $A$ truyền cửa sổ $[\alpha = 3, \beta = +\infty]$ xuống nút MIN $C$.
   - Nút $C$ bắt đầu với $\alpha = 3, \beta = +\infty$.
   - Duyệt lá đầu tiên của $C$ có giá trị **2**:
     + $C$ là nút MIN $\implies$ Cập nhật $\beta = \min(+\infty, 2) = \mathbf{2}$.
     + Lúc này tại nút $C$: $\alpha = 3$ và $\beta = 2$.
     + **KIỂM TRA ĐIỀU KIỆN CẮT TỈA TẠI NÚT MIN:**
       $$\beta \le \alpha \quad (2 \le 3) \implies \mathbf{ALPHA\ CUTOFF!}$$
     + **CẮT TỈA TOÀN BỘ CÁC NHÁNH CÒN LẠI CỦA NÚT C!**
     + Hai nút lá có giá trị **4** và **6** **HOÀN TOÀN BỊ LOẠI BỎ, KHÔNG CẦN DUYỆT!**
     + Nút $C$ lập tức dừng và trả giá trị $\le 2$ (cụ thể là 2) về cho $A$.
5. **Giai đoạn (e): Cập nhật tại A và đi xuống nhánh phải (Nút D):**
   - Tại $A$: $\alpha = \max(\alpha, V(C)) = \max(3, 2) = 3$ (Không đổi).
   - Truyền cửa sổ $[\alpha = 3, \beta = +\infty]$ xuống nút MIN $D$.
   - Nút $D$ duyệt lá đầu tiên có giá trị **14**:
     + $D$ là nút MIN: $\beta = \min(+\infty, 14) = 14$.
     + Tại $D$: $[\alpha = 3, \beta = 14]$. Vì $\beta > \alpha$ ($14 > 3$), chưa cắt tỉa.
6. **Giai đoạn (f): Duyệt tiếp nhánh D và kết thúc:**
   - Duyệt lá thứ hai của $D$ có giá trị **5**:
     + $D$ cập nhật $\beta = \min(14, 5) = 5$.
     + Tại $D$: $[\alpha = 3, \beta = 5]$ ($5 > 3$, chưa cắt tỉa).
   - Duyệt lá thứ ba của $D$ có giá trị **2**:
     + $D$ cập nhật $\beta = \min(5, 2) = 2$.
     + Tại $D$: $\beta \le \alpha$ ($2 \le 3$). Đây là con cuối cùng nên $D$ kết thúc, trả giá trị 2 về cho $A$.
   - Tại gốc $A$: $\alpha = \max(3, 2) = 3$.

**Bảng tổng kết so sánh Minimax vs Alpha-Beta:**

| Thuật toán | Tổng số nút lá trên cây | Số nút lá phải duyệt thực tế | Các nút lá bị cắt tỉa | Giá trị trả về tại gốc | Nước đi tối ưu |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Minimax** | 9 | **9** | Không có | **3** | **$a_1$** |
| **Alpha-Beta** | 9 | **7** | **Lá 4 và Lá 6 (nhánh C)** | **3** | **$a_1$** |

> **Phân tích mở rộng câu hỏi điểm 10:**
> - Nếu nhánh $D$ có thứ tự các con được sắp xếp hoàn hảo là $\{2, 5, 14\}$ (duyệt con giá trị 2 trước):
>   + Khi $D$ duyệt lá 2, $\beta$ của $D$ lập tức thành $2 \le \alpha = 3 \implies$ Cắt tỉa ngay lập tức hai lá 5 và 14!
>   + Khi đó số lá cần duyệt của cả cây giảm xuống chỉ còn $3 + 1 + 1 = \mathbf{5}$ lá (cắt tỉa được 4/9 lá, gần 50% khối lượng tính toán)! Điều này chứng minh sức mạnh sống còn của **Thứ tự nước đi (Move Ordering)** trong giải thuật Alpha-Beta.

---

#### BÀI TẬP 3 (SLIDE 42 & 43): TÍNH TOÁN EXPECTIMINIMAX CÓ NÚT NGẪU NHIÊN (CHANCE NODE)
Đề bài: Xét một tình huống trong trò chơi Cờ thỏ cáo (Backgammon) ở Slide 42. Nút Chance $C$ biểu diễn việc tung 2 con xúc xắc.
Giả sử nút Chance $C$ có 3 kết quả khả dĩ:
- Kết quả 1: Đôi 1 (Xác suất $P_1 = \frac{1}{36}$), dẫn tới nút con có giá trị $Utility = +2$.
- Kết quả 2: Mặt 1 và 2 (Xác suất $P_2 = \frac{2}{36} = \frac{1}{18}$), dẫn tới nút con có giá trị $Utility = -1$.
- Kết quả 3: Các mặt khác còn lại (Xác suất $P_3 = 1 - \frac{1}{36} - \frac{2}{36} = \frac{33}{36}$), dẫn tới nút con có giá trị $Utility = +1$.
Hãy tính giá trị Expectiminimax tại nút Chance $C$.

**Lời giải chi tiết:**
- Theo công thức kỳ vọng toán học tại nút Chance:
  $$V(C) = \sum_{r} P(r) \cdot V(Result(C, r))$$
- Thay các giá trị và xác suất vào công thức:
  $$V(C) = \left(\frac{1}{36} \times 2\right) + \left(\frac{2}{36} \times (-1)\right) + \left(\frac{33}{36} \times 1\right)$$
  $$V(C) = \frac{2 - 2 + 33}{36} = \frac{33}{36} = \frac{11}{12} \approx \mathbf{0.9167}$$
- Giá trị $0.9167$ này sẽ được truyền ngược lên nút cha (MAX hoặc MIN) để tiếp tục thực hiện phép lấy $\max$ hoặc $\min$.
---

## 9. BẢNG TRA CỨU ĐỘ PHỨC TẠP VÀ TÍNH CHẤT CÁC THUẬT TOÁN TÌM KIẾM

Đây là bảng tổng hợp "vũ khí tối thượng" giúp bạn trả lời chính xác 100% các câu hỏi trắc nghiệm và tự luận so sánh trong phòng thi:

| Thuật toán | Cấu trúc dữ liệu Frontier | Thời điểm kiểm tra đích | Tính đầy đủ (Complete) | Độ phức tạp Thời gian | Độ phức tạp Không gian | Tính tối ưu (Optimal) |
| :--- | :--- | :--- | :---: | :---: | :---: | :---: |
| **BFS** *(Breadth-First)* | Hàng đợi FIFO (`Queue`) | **Khi sinh ra (Early)** | **CÓ** *(nếu $b < \infty$)* | $O(b^d)$ | $O(b^d)$ *(Bùng nổ bộ nhớ)* | **CÓ** *(nếu chi phí bước $c=1$)* |
| **UCS** *(Uniform-Cost)* | Hàng đợi ưu tiên theo $g(n)$ | **Khi lấy ra (Late)** | **CÓ** *(nếu $c \ge \epsilon > 0$)* | $O(b^{1 + \lfloor C^* / \epsilon \rfloor})$ | $O(b^{1 + \lfloor C^* / \epsilon \rfloor})$ | **LUÔN TỐI ƯU** *(mọi chi phí $\ge 0$)* |
| **DFS (Tree)** | Ngăn xếp LIFO (`Stack`) | Khi lấy ra / Khi sinh | **KHÔNG** *(vướng chu trình)* | $O(b^m)$ | **$O(bm)$** *(Tuyến tính)* | **KHÔNG** |
| **DFS (Graph)** | Ngăn xếp LIFO + `Explored` | Khi lấy ra | **CÓ** *(không gian hữu hạn)* | $O(b^m)$ | $O(bm)$ | **KHÔNG** |
| **DLS** *(Depth-Limited)* | Ngăn xếp LIFO + Giới hạn $l$ | Khi lấy ra | **KHÔNG** *(nếu $l < d$)* | $O(b^l)$ | **$O(bl)$** | **KHÔNG** *(nếu $l > d$)* |
| **IDS** *(Iterative Deepening)*| Lặp DLS với $l = 0, 1, 2...$ | Tương tự DLS | **CÓ** *(nếu $b < \infty$)* | $O(b^d)$ | **$O(bd)$** *(Tối ưu bộ nhớ)* | **CÓ** *(nếu chi phí bước $c=1$)* |
| **Bidirectional Search** | 2 Hàng đợi FIFO (tiến & lùi)| Khi 2 biên giao nhau | **CÓ** *(nếu $b < \infty$)* | $O(b^{d/2})$ | $O(b^{d/2})$ | **CÓ** *(nếu chi phí bước $c=1$)* |
| **Greedy Best-First** | Hàng đợi ưu tiên theo $h(n)$ | Khi lấy ra | **CÓ** *(Graph hữu hạn)* | $O(b^m)$ | $O(b^m)$ | **KHÔNG** |
| **A\* (Tree-Search)** | Hàng đợi ưu tiên $f = g + h$ | Khi lấy ra | **CÓ** | Số mũ trong trường hợp xấu | Số mũ $O(b^d)$ | **CÓ nếu $h$ là Admissible** |
| **A\* (Graph-Search)** | Hàng đợi ưu tiên $f = g + h$ | Khi lấy ra | **CÓ** | Số mũ trong trường hợp xấu | Số mũ $O(b^d)$ | **CÓ nếu $h$ là Consistent** |
| **IDA\*** | Đệ quy cắt theo ngưỡng $f$ | Khi lấy ra | **CÓ** | Phụ thuộc số giá trị $f$ | **$O(bd)$** | **CÓ nếu $h$ là Admissible** |
| **RBFS** | Đệ quy lưu vết $f$ tốt thứ 2 | Khi lấy ra | **CÓ** | Phụ thuộc độ chính xác $h$| **$O(bd)$** | **CÓ nếu $h$ là Admissible** |
| **Minimax** | Đệ quy cây trò chơi (DFS) | Tại nút lá | **CÓ** *(cây hữu hạn)* | $O(b^m)$ | **$O(bm)$** | **CÓ** *(đối thủ chơi tối ưu)* |
| **Alpha-Beta Pruning** | Đệ quy cắt tỉa $[\alpha, \beta]$ | Tại nút lá | **CÓ** *(cây hữu hạn)* | $O(b^{m/2})$ *(Nước đi tối ưu)* | **$O(bm)$** | **CÓ** *(Không đổi so với Minimax)*|

---

## 10. NGÂN HÀNG CÂU HỎI TRẮC NGHIỆM VÀ TỰ LUẬN ÔN THI TRỌNG TÂM CÓ ĐÁP ÁN

### PHẦN I: CÂU HỎI TRẮC NGHIỆM ĐIỂN HÌNH (CÓ GIẢI THÍCH CHI TIẾT)

#### Câu 1: Bài kiểm tra Turing (Turing Test) nguyên bản kiểm tra điều gì ở hệ thống máy tính?
- A. Năng lực tư duy logic và suy diễn hình thức không bao giờ mắc lỗi.
- B. Năng lực hành động và mô phỏng hành vi bên ngoài không phân biệt được với con người qua giao tiếp văn bản.
- C. Cấu trúc mô phỏng chính xác mạng lưới nơ-ron sinh học trong não người.
- D. Năng lực tự động lập trình và chứng minh các định lý toán học.
> **Đáp án đúng: B**  
> *Giải thích:* Alan Turing đề xuất Turing Test tập trung vào góc nhìn "Hành động như con người" (Acting humanly). Hệ thống vượt qua bài kiểm tra nếu người thẩm vấn không thể phân biệt được câu trả lời bằng văn bản là của người hay máy.

#### Câu 2: Biến thể nào của bài kiểm tra Turing được ứng dụng phổ biến nhất trên Internet ngày nay để ngăn chặn bot tự động?
- A. Total Turing Test
- B. Cognitive Turing Test
- C. Reverse Turing Test (CAPTCHA)
- D. Semantic Turing Test
> **Đáp án đúng: C**  
> *Giải thích:* CAPTCHA (*Completely Automated Public Turing test to tell Computers and Humans Apart*) là một phép thử Turing đảo ngược (Reverse Turing Test), trong đó máy tính đóng vai trò người thẩm vấn để kiểm tra đối tượng truy cập là con người hay bot tự động.

#### Câu 3: Một tác tử hút bụi hoạt động trong phòng chỉ có 2 ô. Môi trường là quan sát một phần (cảm biến hỏng không biết mình đang ở ô nào). Nếu sử dụng kiến trúc Simple Reflex Agent, tác tử sẽ gặp nguy cơ gì?
- A. Luôn luôn tìm ra giải pháp tối ưu.
- B. Bị rơi vào vòng lặp vô tận (Infinite loop) do hai trạng thái khác nhau có cùng cảm nhận bên ngoài.
- C. Hỏng bộ nhớ do bùng nổ dữ liệu.
- D. Tự động chuyển đổi thành Goal-based agent.
> **Đáp án đúng: B**  
> *Giải thích:* Tác tử phản xạ đơn giản không có bộ nhớ trạng thái nội tại. Khi môi trường quan sát một phần, các tình huống khác nhau nhưng có cùng một cảm nhận (ví dụ ô hiện tại sạch) sẽ dẫn tới cùng một hành động lặp đi lặp lại $\implies$ Bị kẹt trong vòng lặp vô tận.

#### Câu 4: Điểm khác biệt mấu chốt giữa Tác tử dựa trên mục tiêu (Goal-based Agent) và Tác tử dựa trên độ lợi (Utility-based Agent) là gì?
- A. Goal-based agent xử lý được môi trường ngẫu nhiên, Utility-based agent thì không.
- B. Goal-based agent chỉ đánh giá nhị phân đạt/không đạt mục tiêu, trong khi Utility-based agent lượng hóa mức độ hạnh phúc/thành công và giải quyết được xung đột giữa các mục tiêu.
- C. Utility-based agent không cần cảm biến.
- D. Goal-based agent luôn tối ưu hơn Utility-based agent.
> **Đáp án đúng: B**  
> *Giải thích:* Mục tiêu (Goal) chỉ mang tính "đạt được hay chưa". Hàm độ lợi (Utility) ánh xạ trạng thái thành số thực, cho phép so sánh mức độ mong muốn giữa các trạng thái, cân bằng đánh đổi (trade-off) giữa tốc độ và độ an toàn, và tối đa hóa độ lợi kỳ vọng trong môi trường bất định.

#### Câu 5: Thành phần nào trong Tác tử học hỏi (Learning Agent) chịu trách nhiệm đề xuất các hành động thử nghiệm mới lạ (Exploration) nhằm tích lũy kinh nghiệm?
- A. Performance element
- B. Learning element
- C. Critic
- D. Problem generator
> **Đáp án đúng: D**  
> *Giải thích:* Problem generator (Bộ phận tạo vấn đề) có nhiệm vụ đề xuất các hành động khám phá mới (dù có thể dưới tối ưu trong ngắn hạn) để đưa tác tử vào các tình huống mới giàu thông tin học hỏi.

#### Câu 6: Trong thuật toán tìm kiếm UCS, vì sao việc kiểm tra mục tiêu (Goal Test) bắt buộc phải thực hiện khi lấy nút ra khỏi hàng đợi (`pop`) thay vì khi sinh nút?
- A. Để tiết kiệm bộ nhớ RAM.
- B. Vì nếu kiểm tra khi sinh nút, thuật toán có thể dừng sớm và trả về một đường đi dưới tối ưu có chi phí cao hơn.
- C. Để đảm bảo hàng đợi không bị rỗng.
- D. Vì hàm chi phí $g(n)$ có thể nhận giá trị âm.
> **Đáp án đúng: B**  
> *Giải thích:* Một nút đích có thể được sinh ra rất sớm từ một nhánh đường đi có chi phí lớn. Nếu kiểm tra sớm, thuật toán dừng ngay sẽ mất tính tối ưu. Khi kiểm tra lúc lấy ra khỏi Priority Queue, ta chắc chắn rằng mọi nút khác trong hàng đợi đều có chi phí $\ge$ chi phí của nút đích này, đảm bảo tính tối ưu tuyệt đối.

#### Câu 7: Khi chi phí của mọi bước đi trong bài toán đều bằng nhau ($c=1$), so sánh số lượng nút được khám phá giữa BFS và UCS:
- A. UCS khám phá ít nút hơn BFS.
- B. BFS và UCS khám phá số lượng nút hoàn toàn bằng nhau.
- C. UCS khám phá nhiều nút hơn BFS vì UCS kiểm tra đích trễ ở tầng $d+1$, trong khi BFS dừng ngay ở tầng $d$.
- D. Không thể so sánh được.
> **Đáp án đúng: C**  
> *Giải thích:* Với $c=1$, BFS kiểm tra đích ngay khi sinh nên dừng ở tầng $d$ ($O(b^d)$ nút). UCS kiểm tra khi lấy ra nên phải duyệt qua toàn bộ các nút ở tầng $d$ rồi mới lấy nút đích ra ở tầng $d+1$, tốn độ phức tạp $O(b^{d+1})$ nút.

#### Câu 8: Thuật toán tìm kiếm mù nào được xem là lựa chọn tối ưu hàng đầu khi không gian tìm kiếm lớn và chưa biết trước độ sâu của nghiệm?
- A. Depth-First Search (DFS)
- B. Breadth-First Search (BFS)
- C. Iterative Deepening Search (IDS)
- D. Depth-Limited Search với $l = 5$
> **Đáp án đúng: C**  
> *Giải thích:* IDS kết hợp trọn vẹn ưu điểm bộ nhớ tuyến tính $O(bd)$ của DFS và tính đầy đủ, tối ưu $O(b^d)$ của BFS.

#### Câu 9: Điều kiện để giải thuật A\* sử dụng TREE-SEARCH đảm bảo luôn tìm được lời giải tối ưu là gì?
- A. $h(n)$ phải là hàm hằng số.
- B. $h(n)$ phải là Heuristic chấp nhận được (Admissible): $0 \le h(n) \le h^*(n)$.
- C. $h(n)$ phải lớn hơn chi phí thực tế.
- D. Không gian trạng thái phải hữu hạn.
> **Đáp án đúng: B**  
> *Giải thích:* Với Tree-search, tính chất Admissible (ước lượng lạc quan không vượt quá chi phí thực tế) là điều kiện cần và đủ để đảm bảo tính tối ưu của A\*.

#### Câu 10: Điều kiện để giải thuật A\* sử dụng GRAPH-SEARCH đảm bảo luôn tìm được lời giải tối ưu mà không cần mở lại các nút trong `explored` là gì?
- A. $h(n)$ chỉ cần Admissible.
- B. $h(n)$ phải là Heuristic nhất quán (Consistent / Monotonic): $h(n) \le c(n, a, n') + h(n')$.
- C. $h(n)$ phải bằng 0 với mọi nút.
- D. Chi phí các cạnh phải bằng nhau.
> **Đáp án đúng: B**  
> *Giải thích:* Trong Graph-search, các nút đã nằm trong tập `explored` sẽ không được đưa lại vào `frontier`. Tính chất Consistent đảm bảo giá trị $f(n)$ không giảm dọc theo mọi đường đi, giúp A\* luôn tìm thấy đường đi tối ưu tới một trạng thái ngay trong lần đầu tiên mở rộng nó.

#### Câu 11: Cho hai Heuristic admissible $h_1$ và $h_2$. Nếu với mọi nút $n$, $h_2(n) \ge h_1(n)$ thì kết luận nào sau đây là CHÍNH XÁC?
- A. $h_1$ thống trị (dominates) $h_2$.
- B. A\* sử dụng $h_1$ luôn tìm ra đường đi ngắn hơn A\* sử dụng $h_2$.
- C. $h_2$ thống trị (dominates) $h_1$, và A\* sử dụng $h_2$ không bao giờ mở rộng nhiều nút hơn A\* sử dụng $h_1$.
- D. Cả hai heuristic đều không tối ưu.
> **Đáp án đúng: C**  
> *Giải thích:* Theo định nghĩa tính trội (Dominance), $h_2(n) \ge h_1(n)$ nghĩa là $h_2$ sát với chi phí thực tế $h^*(n)$ hơn, do đó định hướng tìm kiếm chính xác hơn và mở rộng tập nút con nhỏ hơn hoặc bằng $h_1$.

#### Câu 12: Trong thuật toán Mô phỏng luyện kim (Simulated Annealing), khi nhiệt độ $T \to 0$, thuật toán sẽ hoạt động tương đương với:
- A. Bước đi ngẫu nhiên thuần túy (Pure random walk).
- B. Thuật toán tìm kiếm theo chiều rộng (BFS).
- C. Thuật toán leo đồi dốc nhất thuần túy (Steepest ascent hill climbing).
- D. Thuật giải di truyền (Genetic algorithm).
> **Đáp án đúng: C**  
> *Giải thích:* Khi $T \to 0$, xác suất chấp nhận nước đi tồi $P = e^{\Delta E / T} \to e^{-\infty} = 0$. Thuật toán sẽ hoàn toàn từ chối mọi nước đi làm giảm giá trị và chỉ chấp nhận nước đi cải thiện $\implies$ Hoạt động y hệt leo đồi thuần túy.

#### Câu 13: Trong thuật giải di truyền (GA), cá thể có điểm thích nghi $Fit(n) = 0$ khi áp dụng chọn lọc theo bánh xe Roulette (Roulette Wheel Selection) sẽ có xác suất được chọn là:
- A. $50\%$
- B. Tùy thuộc vào số lượng cá thể trong quần thể.
- C. $0\%$ (Chắc chắn không được chọn).
- D. Bằng mức xác suất trung bình của quần thể.
> **Đáp án đúng: C**  
> *Giải thích:* Công thức xác suất chọn lọc là $P(i) = Fit(i) / \sum Fit$. Khi $Fit = 0 \implies P = 0 / \sum Fit = 0$. Cá thể này không chiếm bất kỳ diện tích nào trên vòng quay Roulette nên không bao giờ được chọn.

#### Câu 14: Trong giải thuật Cắt tỉa Alpha-Beta, điều kiện nào sau đây dẫn tới Cắt tỉa Alpha (Alpha Cutoff) tại một nút MIN?
- A. $v \ge \beta$
- B. $v \le \alpha$
- C. $\alpha > \beta$
- D. $v == 0$
> **Đáp án đúng: B**  
> *Giải thích:* Tại nút MIN, ta đang tìm cách thu nhỏ giá trị $\beta$. Nếu một nút con trả về giá trị $v \le \alpha$, điều này có nghĩa là nút MIN này sẽ có giá trị tối đa là $v \le \alpha$. Nhưng tổ tiên MAX phía trên đã có một lựa chọn khác tốt hơn với giá trị ít nhất là $\alpha$. Do đó MAX sẽ không bao giờ chọn nhánh này $\implies$ Cắt tỉa Alpha!

#### Câu 15: Trong điều kiện lý tưởng (thứ tự nước đi hoàn hảo - Best moves examined first), độ phức tạp thời gian của Cắt tỉa Alpha-Beta giảm xuống còn bao nhiêu so với $O(b^m)$ của Minimax?
- A. $O(m^b)$
- B. $O(b \cdot m)$
- C. $O(b^{m/2}) = O((\sqrt{b})^m)$
- D. $O(b/2 \cdot m)$
> **Đáp án đúng: C**  
> *Giải thích:* Khi nước đi tốt nhất luôn được duyệt đầu tiên, Alpha-Beta cắt tỉa tối đa các nhánh còn lại, giúp giảm hệ số phân nhánh hiệu dụng xuống $\sqrt{b}$, đưa độ phức tạp về $O(b^{m/2})$, cho phép tìm kiếm sâu gấp đôi trong cùng thời gian.

---

### PHẦN II: CÂU HỎI TỰ LUẬN & BÀI TẬP TỔNG HỢP ÔN THI ĐẠT ĐIỂM 10

#### Câu hỏi Tự luận 1: Phân tích bản chất và chứng minh: "Mọi Heuristic nhất quán (Consistent) đều là Heuristic chấp nhận được (Admissible)".
**Lời giải chi tiết:**
- Cho đồ thị bài toán với trạng thái đích $Goal$, trong đó $h(Goal) = 0$.
- Giả sử $h(n)$ thỏa mãn tính chất nhất quán (Consistent): Với mọi nút $n$ và láng giềng $n'$ nối bởi hành động $a$, ta có:
  $$h(n) \le c(n, a, n') + h(n')$$
- Xét một đường đi tối ưu từ nút $n$ bất kỳ tới đích $Goal$: $n = n_0 \to n_1 \to n_2 \to \dots \to n_k = Goal$.
- Áp dụng liên tiếp bất đẳng thức nhất quán dọc theo từng bước trên đường đi tối ưu này:
  $$h(n_0) \le c(n_0, n_1) + h(n_1)$$
  $$h(n_1) \le c(n_1, n_2) + h(n_2)$$
  $$\dots$$
  $$h(n_{k-1}) \le c(n_{k-1}, n_k) + h(n_k)$$
- Cộng vế theo vế toàn bộ $k$ bất đẳng thức trên:
  $$h(n_0) + \sum_{i=1}^{k-1} h(n_i) \le \sum_{i=0}^{k-1} c(n_i, n_{i+1}) + \sum_{i=1}^{k} h(n_i)$$
- Triệt tiêu các số hạng $h(n_1), \dots, h(n_{k-1})$ ở hai vế, ta thu được:
  $$h(n_0) \le \sum_{i=0}^{k-1} c(n_i, n_{i+1}) + h(n_k)$$
- Chú ý rằng $\sum_{i=0}^{k-1} c(n_i, n_{i+1})$ chính là tổng chi phí của đường đi tối ưu từ $n_0$ tới đích, tức $h^*(n_0)$; và $h(n_k) = h(Goal) = 0$.
- Do đó:
  $$h(n_0) \le h^*(n_0) + 0 \implies h(n_0) \le h^*(n_0)$$
- Kết hợp với điều kiện $h(n) \ge 0 \implies 0 \le h(n) \le h^*(n)$ với mọi $n$.
- $\implies$ **Chứng minh hoàn tất: Mọi Heuristic nhất quán bắt buộc phải là Heuristic chấp nhận được!**

---

#### Câu hỏi Tự luận 2: Phân tích bài toán thiết kế Heuristic cho Bài toán 8-Puzzle.
Đề bài: Cho trạng thái xuất phát $S$ và trạng thái đích $G$ của bài toán 8-puzzle như sau:
```
Trạng thái S:          Trạng thái đích G:
+---+---+---+          +---+---+---+
| 7 | 2 | 4 |          | 1 | 2 | 3 |
+---+---+---+          +---+---+---+
| 5 |   | 6 |          | 4 | 5 | 6 |
+---+---+---+          +---+---+---+
| 8 | 3 | 1 |          | 7 | 8 |   |
+---+---+---+          +---+---+---+
```
Hãy tính:
1. Giá trị Heuristic $h_1(S)$ (Số ô sai vị trí).
2. Giá trị Heuristic $h_2(S)$ (Tổng khoảng cách Manhattan).
3. Chứng minh vì sao $h_2(S) \ge h_1(S)$ và ý nghĩa của tính trội trong tìm kiếm A\*.

**Lời giải chi tiết:**
1. **Tính $h_1(S)$ (Số ô sai vị trí so với đích, không tính ô trống):**
   - Ô 1: Hiện ở (hàng 3, cột 3); Đích ở (hàng 1, cột 1) $\implies$ **Sai vị trí**.
   - Ô 2: Hiện ở (hàng 1, cột 2); Đích ở (hàng 1, cột 2) $\implies$ **Đúng vị trí**.
   - Ô 3: Hiện ở (hàng 3, cột 2); Đích ở (hàng 1, cột 3) $\implies$ **Sai vị trí**.
   - Ô 4: Hiện ở (hàng 1, cột 3); Đích ở (hàng 2, cột 1) $\implies$ **Sai vị trí**.
   - Ô 5: Hiện ở (hàng 2, cột 1); Đích ở (hàng 2, cột 2) $\implies$ **Sai vị trí**.
   - Ô 6: Hiện ở (hàng 2, cột 3); Đích ở (hàng 2, cột 3) $\implies$ **Đúng vị trí**.
   - Ô 7: Hiện ở (hàng 1, cột 1); Đích ở (hàng 3, cột 1) $\implies$ **Sai vị trí**.
   - Ô 8: Hiện ở (hàng 3, cột 1); Đích ở (hàng 3, cột 2) $\implies$ **Sai vị trí**.
   - Các ô nằm sai vị trí: $\{1, 3, 4, 5, 7, 8\}$ (tổng cộng 6 ô sai vị trí).
   - $\implies \mathbf{h_1(S) = 6}$.

2. **Tính $h_2(S)$ (Tổng khoảng cách Manhattan):**
   Khoảng cách Manhattan của ô $i$ là $d_i = |r_{hiện\_tại} - r_{đích}| + |c_{hiện\_tại} - c_{đích}|$:
   - Ô 1: $|3 - 1| + |3 - 1| = 2 + 2 = 4$.
   - Ô 2: Đúng vị trí $\implies d_2 = 0$.
   - Ô 3: $|3 - 1| + |2 - 3| = 2 + 1 = 3$.
   - Ô 4: $|1 - 2| + |3 - 1| = 1 + 2 = 3$.
   - Ô 5: $|2 - 2| + |1 - 2| = 0 + 1 = 1$.
   - Ô 6: Đúng vị trí $\implies d_6 = 0$.
   - Ô 7: $|1 - 3| + |1 - 1| = 2 + 0 = 2$.
   - Ô 8: $|3 - 3| + |1 - 2| = 0 + 1 = 1$.
   - Tổng khoảng cách Manhattan:
     $$h_2(S) = 4 + 0 + 3 + 3 + 1 + 0 + 2 + 1 = \mathbf{14}$$

3. **So sánh và Ý nghĩa:**
   - Ta thấy $h_2(S) = 14 > h_1(S) = 6$.
   - Tổng quát: Mỗi ô sai vị trí đóng góp vào $h_1$ đúng 1 đơn vị, nhưng trong $h_2$, ô đó phải di chuyển ít nhất 1 bước (và thường là $\ge 2$ bước) mới về đích. Do đó luôn có $h_2(n) \ge h_1(n)$ với mọi trạng thái $n$.
   - Vì $h_2$ trội hơn $h_1$, khi giải bài toán này bằng thuật toán A\*, Heuristic khoảng cách Manhattan $h_2$ sẽ giúp A\* loại bỏ được số lượng rất lớn các nút không tiềm năng và tìm ra lời giải nhanh hơn gấp nhiều lần so với $h_1$!

---

#### LỜI CHÚC THI TỐT DÀNH CHO BẠN:
Tài liệu này đã bao quát **100% lượng kiến thức cốt lõi** từ Lecture 01 đến Lecture 05 của ThS. Bùi Duy Đăng. Trước khi vào phòng thi vào chiều ngày 27/10:
1. Đọc kỹ lại bảng trace của 3 bài tập BFS, UCS, DFS trong Chương 3 - Phần 2.
2. Nắm chắc từng bước cập nhật cửa sổ $[\alpha, \beta]$ và điều kiện cắt tỉa trong Chương 5.
3. Nhớ chính xác công thức tính xác suất chọn lọc Roulette Wheel $P(i) = Fit(i) / \sum Fit$ trong Chương 4.

**Chúc bạn ôn tập tự tin và đạt điểm 10 tuyệt đối trong kỳ thi giữa kỳ môn Cơ sở Trí tuệ Nhân tạo!**
