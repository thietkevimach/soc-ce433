# Bài tập lớn: Thiết kế RTL và mô phỏng phục vụ đánh giá rò rỉ bằng TVLA

Thiết kế một khối RTL cơ bản và thực hiện quy trình từ RTL đến gate/post-implementation simulation. Thu thập switching/activity traces từ nhiều lần mô phỏng với hai nhóm dữ liệu **fixed** và **random**, sau đó dùng các trace này để thực hiện **TVLA** nhằm đánh giá sơ bộ rò rỉ kênh bên của thiết kế.
## 1. Mục tiêu

Sinh viên thiết kế một khối RTL cơ bản, thực hiện tổng hợp và mô phỏng ở mức gate/post-implementation để thu được **power/activity traces**, sau đó dùng các trace này để thực hiện **TVLA (Test Vector Leakage Assessment)** nhằm đánh giá sơ bộ khả năng rò rỉ thông tin bên kênh.

## 2. Bài toán

Thiết kế một khối tính toán cơ bản, ví dụ:

* Matrix multiplication 2x2 / 4x4
* MAC engine
* FIR filter nhỏ
* Montgomery/NTT toy block đơn giản
* AES-like round toy module hoặc multiplier-accumulator

Nếu muốn gắn rõ với SCA hơn, nên chọn:

* **khối nhân cộng tuần tự**
* hoặc **khối xử lý dữ liệu có nhiều phép chuyển trạng thái nội bộ**

vì dễ quan sát khác biệt switching activity.

---

## 3. Yêu cầu kỹ thuật

### 3.1. Thiết kế RTL

Sinh viên phải:

* viết RTL bằng Verilog/VHDL
* có `clk`, `rst`, `start`, `done`
* có dữ liệu đầu vào, đầu ra rõ ràng
* có thanh ghi nội bộ hoặc datapath đủ để quan sát hoạt động chuyển mạch

### 3.2. Tổng hợp và implementation

Sinh viên phải:

* chạy synthesis
* chạy implementation/place-and-route
* xuất netlist sau tổng hợp hoặc sau implementation
* chuẩn bị mô phỏng mức gate/post-implementation

### 3.3. Mô phỏng phục vụ TVLA

Sinh viên phải tạo môi trường mô phỏng để thu **switching traces theo thời gian**, ví dụ:

* VCD
* SAIF
* hoặc dạng waveform activity tương đương

Lưu ý:
Mục tiêu ở đây không phải chỉ lấy một con số power trung bình, mà là lấy **dấu vết hoạt động theo từng chu kỳ/thời điểm** để phân tích thống kê.

---

## 4. Yêu cầu riêng cho TVLA

## 4.1. Tạo hai tập mẫu

Sinh viên phải xây dựng hai nhóm input:

### Nhóm 1: Fixed input set

* một phần dữ liệu được giữ cố định
* ví dụ: cùng một vector đầu vào hoặc cùng một ma trận A

### Nhóm 2: Random input set

* dữ liệu thay đổi ngẫu nhiên qua nhiều lần chạy

Mỗi lần chạy mô phỏng tạo ra một trace activity/power theo thời gian.

---

## 4.2. Số lượng mẫu

* Mỗi nhóm cần có số lượng trace đủ lớn để làm kiểm định thống kê
* Khuyến nghị:

  * tối thiểu: **200–500 traces mỗi nhóm**
  * tốt hơn: **1000 traces mỗi nhóm**

---

## 4.3. Dữ liệu cần thu

Ở mỗi lần mô phỏng, sinh viên cần lưu ít nhất một trong các đại lượng sau:

* tổng switching activity theo từng chu kỳ
* toggle count của các nút nội bộ theo thời gian
* power estimate theo time window
* hoặc giá trị activity suy ra từ VCD/SAIF

Sau đó chuẩn hóa thành dạng:

* mỗi trace = một vector số theo thời gian
* ví dụ: `[p1, p2, p3, ..., pn]`

---

## 4.4. Phân tích TVLA

Sinh viên dùng hai tập trace để thực hiện kiểm định thống kê kiểu **fixed-vs-random t-test**.

### Mục tiêu

Kiểm tra xem tại thời điểm nào trong quá trình xử lý:

* activity/power của hai nhóm có khác biệt có ý nghĩa thống kê hay không

### Kết quả cần báo cáo

* đồ thị trị số **t-value theo thời gian**
* xác định các vùng thời gian có dấu hiệu rò rỉ
* nhận xét module nào / pha nào của thiết kế có khả năng gây lộ thông tin nhiều hơn

---

## 5. Đồ thị yêu cầu

### Đồ thị 1: Trace activity/power mẫu

* vẽ 5–10 trace đại diện
* để quan sát hình dạng tín hiệu theo thời gian

### Đồ thị 2: Trung bình của hai nhóm

* trung bình nhóm Fixed
* trung bình nhóm Random
* so sánh trực quan

### Đồ thị 3: TVLA t-value theo thời gian

* trục X: thời gian hoặc chỉ số mẫu
* trục Y: t-value
* đánh dấu ngưỡng phát hiện rò rỉ

### Đồ thị 4: So sánh kiến trúc

Ví dụ:

* tuần tự vs song song
* pipeline vs không pipeline
* bit-width thấp vs cao

và so sánh:

* peak |t|
* số điểm vượt ngưỡng
* vùng rò rỉ kéo dài bao lâu

---

## 6. Nội dung phân tích bắt buộc

### 6.1. Phân tích chức năng

* thiết kế có chạy đúng không
* waveform đúng với mong đợi không

### 6.2. Phân tích tài nguyên

* LUT / FF / DSP / BRAM hoặc area tương đương
* timing / Fmax

### 6.3. Phân tích hoạt động chuyển mạch

* phần nào của thiết kế hoạt động mạnh nhất
* giai đoạn nào có activity lớn
* input pattern có ảnh hưởng thế nào

### 6.4. Phân tích TVLA

* có xuất hiện rò rỉ hay không
* rò rỉ mạnh ở giai đoạn nào
* kiến trúc nào có xu hướng rò rỉ cao hơn
* có mối liên hệ gì giữa area / latency / switching / leakage

---

## 7. Kết quả đầu ra sinh viên phải nộp

* RTL source
* Testbench sinh dữ liệu fixed/random
* Script mô phỏng
* File trace hoặc dữ liệu trích xuất từ VCD/SAIF
* Script phân tích TVLA
* Báo cáo tổng hợp tài nguyên
* Báo cáo đồ thị TVLA
* Kết luận về mức độ rò rỉ

---
**Các bước chính**

1. Viết RTL và testbench
2. Tổng hợp và implementation
3. Mô phỏng sau tổng hợp hoặc sau implementation
4. Thu activity/power traces từ nhiều lần chạy
5. Chia thành hai nhóm fixed và random
6. Thực hiện kiểm định TVLA
7. Vẽ đồ thị t-value theo thời gian
8. Phân tích mối liên hệ giữa kiến trúc, switching activity và leakage

---
