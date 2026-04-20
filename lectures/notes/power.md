# Bài tập lớn: Thiết kế, tổng hợp và phân tích công suất cho khối RTL cơ bản

## 1. Mục tiêu

Sinh viên thực hiện quy trình thiết kế phần cứng số từ mức RTL đến implementation, sau đó phân tích tài nguyên và công suất tiêu thụ của thiết kế để phục vụ đánh giá **TLA (Trade-off giữa Timing – Logic/Area – Activity/Power)**.

## 2. Yêu cầu bài toán

Thiết kế một khối RTL cơ bản, ví dụ:

* **Khối nhân ma trận**
* Hoặc **MAC array**
* Hoặc **bộ nhân tích lũy đơn giản cho xử lý tín hiệu**

Khuyến nghị chọn bài toán sau để đồng nhất:

### Bài toán đề xuất

Thiết kế khối **Matrix Multiplication 2x2 hoặc 4x4** với dữ liệu đầu vào số nguyên không dấu 8-bit.

#### Chức năng

Cho hai ma trận:

* `A[m][n]`
* `B[n][p]`

Thiết kế phần cứng tính:

* `C = A x B`

#### Gợi ý cấu hình

* Mức cơ bản: ma trận **2x2**
* Mức nâng cao: ma trận **4x4**
* Mỗi phần tử: **8-bit unsigned**
* Kết quả đầu ra: chọn độ rộng phù hợp để tránh tràn số

---

## 3. Yêu cầu kỹ thuật

### 3.1. Thiết kế RTL

Sinh viên phải:

* Viết mã RTL bằng **Verilog** hoặc **VHDL**
* Thiết kế theo kiến trúc có thể tổng hợp được
* Có các tín hiệu cơ bản:

  * `clk`
  * `rst_n` hoặc `rst`
  * `start`
  * `done`
  * input matrix A
  * input matrix B
  * output matrix C

### 3.2. Kiến trúc

Sinh viên được chọn một trong hai hướng:

* **Kiến trúc tuần tự**: dùng ít phần cứng hơn, nhiều chu kỳ hơn
* **Kiến trúc song song**: dùng nhiều tài nguyên hơn, tốc độ cao hơn

Khuyến khích sinh viên giải thích lựa chọn kiến trúc của mình.

---

## 4. Các bước thực hiện

### Phần 1: Thiết kế và mô phỏng chức năng

* Viết RTL cho khối nhân ma trận
* Viết testbench kiểm tra chức năng
* Chạy mô phỏng chức năng
* Chứng minh đầu ra đúng với ít nhất 3 bộ test

### Phần 2: Tổng hợp và phân tích tài nguyên

Sau khi hoàn tất RTL, thực hiện tổng hợp trên công cụ FPGA/ASIC phù hợp.

Sinh viên cần trích xuất và báo cáo tối thiểu các thông tin sau:

* **Area / Utilization**

  * LUT
  * FF
  * DSP
  * BRAM
* **Timing**

  * Fmax
  * Critical path
* **Power**

  * Total power
  * Dynamic power
  * Static/Leakage power

### Phần 3: Mô phỏng sau implementation

* Thực hiện **post-synthesis** hoặc **post-implementation simulation**
* Thu thập switching activity (VCD/SAIF)
* Dùng activity này để ước lượng công suất chính xác hơn
* So sánh:

  * Power ước lượng mặc định
  * Power có activity từ mô phỏng sau implementation

### Phần 4: Vẽ đồ thị và phân tích TLA

Sinh viên cần vẽ đồ thị power để phục vụ phân tích trade-off.

---

## 5. Nội dung phân tích bắt buộc

### 5.1. Phân tích tài nguyên

So sánh giữa các lựa chọn thiết kế, ví dụ:

* 2x2 vs 4x4
* tuần tự vs song song
* có pipeline vs không pipeline

### 5.2. Phân tích công suất

Sinh viên cần phân tích công suất theo các tiêu chí:

* công suất tổng
* công suất động
* công suất tĩnh
* ảnh hưởng của tần số clock
* ảnh hưởng của mức độ hoạt động dữ liệu

### 5.3. Phân tích TLA

TLA ở đây có thể hiểu là phân tích đánh đổi giữa:

* **T – Timing**: tốc độ, số chu kỳ, độ trễ
* **L – Logic/Area**: mức sử dụng tài nguyên phần cứng
* **A – Activity/Power**: mức chuyển mạch và công suất tiêu thụ

Sinh viên cần rút ra nhận xét như:

* thiết kế song song nhanh hơn nhưng tốn area và power hơn
* thiết kế tuần tự tiết kiệm area nhưng latency lớn hơn
* pipeline có thể cải thiện timing nhưng làm tăng register và switching activity

---

## 6. Đồ thị yêu cầu

Sinh viên phải vẽ tối thiểu các đồ thị sau:

### Đồ thị 1: Total Power theo kiến trúc

* Trục X: phiên bản thiết kế
* Trục Y: total power

Ví dụ:

* Seq_2x2
* Parallel_2x2
* Seq_4x4
* Parallel_4x4

### Đồ thị 2: Dynamic Power theo tần số

* Trục X: tần số clock
* Trục Y: dynamic power

Ví dụ các mốc:

* 50 MHz
* 100 MHz
* 150 MHz
* 200 MHz

### Đồ thị 3: Area vs Power

* Trục X: LUT hoặc tổng tài nguyên quy đổi
* Trục Y: total power

### Đồ thị 4: Latency vs Power

* Trục X: số chu kỳ hoặc thời gian xử lý
* Trục Y: total power

---

## 7. Sản phẩm cần nộp

### 7.1. Mã nguồn

* RTL source
* Testbench
* File constraint
* Script tổng hợp/mô phỏng nếu có

### 7.2. Báo cáo

Báo cáo gồm các mục:

1. Giới thiệu bài toán
2. Kiến trúc thiết kế
3. Mô tả RTL
4. Kết quả mô phỏng chức năng
5. Kết quả tổng hợp và implementation
6. Kết quả phân tích power
7. Các đồ thị power/TLA
8. Nhận xét và kết luận

### 7.3. Minh chứng kết quả

* ảnh waveform
* báo cáo utilization
* báo cáo timing
* báo cáo power
* hình đồ thị

---

## 8. Tiêu chí đánh giá

### Thang điểm gợi ý

* **20%**: RTL đúng chức năng
* **15%**: testbench đầy đủ
* **20%**: tổng hợp và implementation thành công
* **15%**: báo cáo tài nguyên và timing
* **15%**: phân tích power có cơ sở
* **15%**: đồ thị và nhận xét TLA rõ ràng

---

## 9. Gợi ý mở rộng

Sinh viên khá/giỏi có thể làm thêm:

* so sánh nhiều kiểu coding RTL khác nhau
* thêm pipeline để tăng Fmax
* dùng DSP block thay vì LUT-based multiplier
* thay đổi bit-width đầu vào
* đánh giá ảnh hưởng của data pattern đến power
* so sánh power ở mức post-synthesis và post-implementation

---

## 10. Phiên bản ngắn gọn để giao trực tiếp cho sinh viên

**Đề bài:**
Thiết kế một khối RTL cơ bản thực hiện phép **nhân ma trận** (2x2 hoặc 4x4, dữ liệu 8-bit). Hoàn thành các bước:

1. Viết RTL và testbench kiểm tra chức năng
2. Tổng hợp thiết kế và báo cáo tài nguyên sử dụng (LUT/FF/DSP/BRAM hoặc area tương đương)
3. Phân tích timing và công suất tiêu thụ
4. Thực hiện mô phỏng sau implementation để lấy switching activity phục vụ phân tích power
5. Vẽ các đồ thị power và thực hiện phân tích **TLA trade-off** giữa:

   * Timing
   * Logic/Area
   * Activity/Power

**Yêu cầu đầu ra:**

* mã RTL
* testbench
* báo cáo tổng hợp/implementation
* báo cáo power
* đồ thị minh họa
* phần nhận xét, so sánh, đánh giá trade-off

---

Nếu bạn muốn, tôi có thể viết tiếp cho bạn một **bản giao bài dạng markdown chuẩn giảng viên**, kèm luôn:

* mục tiêu học phần
* rubric chấm điểm
* template báo cáo
* mẫu bảng kết quả power/area/timing cho sinh viên điền.
