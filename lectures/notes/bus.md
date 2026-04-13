# HỆ THỐNG BUS TRONG SoC
## System Bus for SoC FPGA
- Môn học: Thiết kế hệ thống SoC trên FPGA
- Chủ đề: APB, AHB, AXI, Avalon
- Mục tiêu:
  - Nhận biết các bus phổ biến trong SoC
  - Hiểu chức năng, tín hiệu cơ bản
  - So sánh và chọn bus phù hợp
  - Gợi ý đề tài nhỏ cho sinh viên

---

# 1. Mục tiêu bài học
Sau bài này, sinh viên có thể:
- Kể tên các hệ thống bus phổ biến trong SoC
- Phân biệt bus điều khiển và bus dữ liệu hiệu năng cao
- Giải thích được vai trò của APB, AHB, AXI, Avalon
- Chọn bus phù hợp cho một IP tự thiết kế
- Đề xuất kiến trúc bus cho một SoC đơn giản

---

# 2. Bus là gì?
- Bus là hệ thống kết nối giữa các thành phần trong SoC
- Dùng để truyền:
  - Địa chỉ
  - Dữ liệu
  - Tín hiệu điều khiển
  - Tín hiệu trạng thái / phản hồi
- Bus kết nối:
  - CPU
  - Bộ nhớ
  - DMA
  - Ngoại vi
  - IP tự thiết kế

---

# 3. Vai trò của bus trong SoC
- Đảm bảo các khối giao tiếp đúng chuẩn
- Giảm độ phức tạp khi tích hợp hệ thống
- Tăng khả năng tái sử dụng IP
- Hỗ trợ mở rộng hệ thống
- Ảnh hưởng trực tiếp đến:
  - Độ trễ
  - Băng thông
  - Tài nguyên phần cứng
  - Độ phức tạp thiết kế

---

# 4. Danh mục các bus phổ biến trong SoC
## Họ AMBA
- APB
- AHB / AHB-Lite
- AXI4
- AXI4-Lite
- AXI4-Stream
- ACE / CHI (nâng cao)

## Họ Intel / Altera
- Avalon-MM
- Avalon-ST
- Avalon Conduit
- Avalon Interrupt
- Avalon Clock / Reset

---

# 5. Phân loại bus theo chức năng
## Bus điều khiển
- APB
- AXI4-Lite
- Avalon-MM

## Bus hệ thống / bộ nhớ
- AHB
- AXI4
- Avalon-MM

## Bus truyền luồng dữ liệu
- AXI4-Stream
- Avalon-ST

## Bus tín hiệu tùy chỉnh
- Avalon Conduit

---

# 6. APB là gì?
## APB - Advanced Peripheral Bus
- Bus đơn giản trong họ AMBA
- Tối ưu cho ngoại vi tốc độ thấp
- Không nhắm tới băng thông cao
- Thường dùng để truy cập thanh ghi điều khiển

## Ứng dụng
- UART
- GPIO
- Timer
- SPI control
- I2C control

---

# 7. Tín hiệu cơ bản của APB
- PCLK: clock
- PRESETn: reset
- PADDR: địa chỉ
- PWRITE: chọn đọc / ghi
- PWDATA: dữ liệu ghi
- PRDATA: dữ liệu đọc
- PSEL: chọn slave
- PENABLE: enable transfer
- PREADY: slave sẵn sàng
- PSLVERR: báo lỗi

## Đặc điểm
- Mỗi giao dịch thường cần ít nhất 2 chu kỳ
- Giao thức đơn giản, dễ thiết kế

---

# 8. AHB là gì?
## AHB - Advanced High-performance Bus
- Bus hiệu năng cao hơn APB
- Dùng cho CPU, DMA, bộ nhớ, ngoại vi nhanh
- Có pha địa chỉ và pha dữ liệu
- Hỗ trợ burst và pipeline cơ bản

## Ứng dụng
- CPU ↔ SRAM
- CPU ↔ bộ điều khiển nhớ
- DMA ↔ memory
- Bus hệ thống nhúng

---

# 9. Tín hiệu cơ bản của AHB
## Nhóm địa chỉ / điều khiển
- HADDR
- HWRITE
- HSIZE
- HTRANS
- HSEL
- HBURST
- HPROT

## Nhóm dữ liệu / phản hồi
- HWDATA
- HRDATA
- HREADY
- HREADYOUT
- HRESP

## Đặc điểm
- Nhanh hơn APB
- Phù hợp bus hệ thống mức trung bình

---

# 10. AXI là gì?
## AXI - Advanced eXtensible Interface
- Bus hiệu năng cao, rất phổ biến trong SoC hiện đại
- Tách kênh đọc và ghi độc lập
- Hỗ trợ burst dài
- Hỗ trợ nhiều giao dịch chờ đồng thời
- Tối ưu cho tần số cao và băng thông lớn

## Ứng dụng
- CPU ↔ DDR
- DMA ↔ memory
- CPU ↔ accelerator
- SoC chạy Linux
- AI / DSP / video pipeline

---

# 11. 5 kênh của AXI4
## Kênh ghi địa chỉ
- AWADDR, AWVALID, AWREADY

## Kênh ghi dữ liệu
- WDATA, WSTRB, WVALID, WREADY, WLAST

## Kênh phản hồi ghi
- BRESP, BVALID, BREADY

## Kênh đọc địa chỉ
- ARADDR, ARVALID, ARREADY

## Kênh đọc dữ liệu
- RDATA, RRESP, RVALID, RREADY, RLAST

---

# 12. AXI4-Lite
- Phiên bản đơn giản của AXI4
- Không hỗ trợ burst
- Dùng chủ yếu cho truy cập thanh ghi điều khiển

## Ứng dụng
- Control register của IP
- Cấu hình accelerator
- Giao tiếp CPU với IP tự thiết kế

## Ưu điểm
- Dễ dùng hơn AXI4 full
- Dễ tích hợp với CPU

---

# 13. AXI4-Stream
- Chuẩn truyền dữ liệu dạng luồng
- Không dùng địa chỉ bộ nhớ
- Truyền dữ liệu liên tục theo handshake

## Tín hiệu phổ biến
- TVALID
- TREADY
- TDATA
- TLAST
- TKEEP / TSTRB
- TUSER

## Ứng dụng
- Video stream
- Audio stream
- DSP
- AI accelerator pipeline

---

# 14. Avalon là gì?
## Avalon Bus
- Bus phổ biến trong hệ Intel / Altera FPGA
- Tích hợp chặt với Nios II và Platform Designer
- Có nhiều biến thể cho memory-mapped và streaming

## Các chuẩn Avalon hay gặp
- Avalon-MM
- Avalon-ST
- Avalon Conduit
- Avalon Interrupt
- Avalon Clock / Reset

---

# 15. Avalon-MM
## Avalon Memory-Mapped
- Truy cập theo địa chỉ
- Dùng để kết nối CPU, memory, peripheral, IP custom

## Tín hiệu phổ biến
- address
- read
- write
- writedata
- readdata
- waitrequest
- byteenable
- readdatavalid

## Ứng dụng
- Nios II ↔ IP
- Nios II ↔ memory
- Peripheral register interface

---

# 16. Avalon-ST
## Avalon Streaming
- Truyền dữ liệu luồng liên tục
- Tương tự AXI4-Stream về ý tưởng

## Tín hiệu phổ biến
- data
- valid
- ready
- startofpacket
- endofpacket
- empty
- channel
- error

## Ứng dụng
- DSP
- Packet processing
- Image / audio / video stream

---

# 17. Avalon Conduit / Interrupt
## Avalon Conduit
- Kết nối tín hiệu tùy chỉnh
- Không áp khuôn giao thức chặt như bus chuẩn

## Dùng cho
- GPIO
- enable / done / status
- signal riêng giữa các IP

## Avalon Interrupt
- Truyền tín hiệu ngắt về CPU
- Dùng cho timer, UART, IP báo hoàn thành

---

# 18. So sánh nhanh các bus
| Bus | Mục tiêu | Hiệu năng | Độ phức tạp | Kiểu truyền | Ứng dụng chính |
|---|---|---|---|---|---|
| APB | Ngoại vi chậm | Thấp | Thấp | Memory-mapped | UART, GPIO, timer |
| AHB | Bus hệ thống | Trung bình | Trung bình | Memory-mapped, burst | CPU, SRAM, DMA |
| AXI4 | Hiệu năng cao | Rất cao | Cao | Memory-mapped, burst | DDR, DMA, accelerator |
| AXI4-Lite | Điều khiển IP | Thấp | Thấp | Memory-mapped | Control register |
| AXI4-Stream | Dữ liệu luồng | Cao | Trung bình | Streaming | Video, DSP, AI |
| Avalon-MM | Bus hệ Intel | Trung bình | Trung bình | Memory-mapped | Nios II, IP custom |
| Avalon-ST | Stream hệ Intel | Cao | Trung bình | Streaming | DSP, packet, image |

---

# 19. So sánh APB vs AHB vs AXI
| Tiêu chí | APB | AHB | AXI |
|---|---|---|---|
| Mục tiêu | Ngoại vi đơn giản | Bus hệ thống | Hệ hiệu năng cao |
| Tốc độ | Thấp | Trung bình-khá | Cao |
| Burst | Không | Có | Có |
| Pipeline | Không đáng kể | Có | Mạnh |
| Đọc/ghi đồng thời | Không | Hạn chế | Có |
| Độ phức tạp | Thấp | Trung bình | Cao |
| Ví dụ dùng | GPIO, UART | SRAM, DMA | DDR, accelerator |

---

# 20. So sánh AXI4-Lite vs AXI4-Stream vs Avalon-MM
| Tiêu chí | AXI4-Lite | AXI4-Stream | Avalon-MM |
|---|---|---|---|
| Dựa trên địa chỉ | Có | Không | Có |
| Truy cập thanh ghi | Rất phù hợp | Không phù hợp | Phù hợp |
| Truyền dữ liệu liên tục | Kém | Rất phù hợp | Trung bình |
| Dễ tích hợp IP control | Cao | Thấp | Cao |
| Hệ sinh thái | Xilinx/AMD | Xilinx/AMD | Intel/Altera |

---

# 21. Quy tắc chọn bus trong thiết kế
## Chọn APB khi:
- Ngoại vi đơn giản
- Ít dữ liệu
- Ưu tiên dễ thiết kế

## Chọn AHB khi:
- Bus hệ thống nhúng mức vừa
- Cần nhanh hơn APB

## Chọn AXI4 khi:
- Cần băng thông cao
- Giao tiếp DDR / DMA / accelerator

## Chọn AXI4-Lite khi:
- Chỉ cấu hình thanh ghi IP

## Chọn AXI4-Stream / Avalon-ST khi:
- Truyền luồng dữ liệu liên tục

## Chọn Avalon-MM khi:
- Thiết kế trên Intel/Altera với Nios II

---

# 22. Ví dụ kiến trúc SoC đơn giản
## Một hệ thống minh họa
- CPU
- On-chip memory
- UART
- GPIO
- Timer
- IP xử lý tự thiết kế
- DMA
- Bus interconnect

## Gợi ý bus
- CPU ↔ DDR: AXI4
- CPU ↔ control regs: AXI4-Lite
- Camera / stream ↔ IP: AXI4-Stream
- Nios II ↔ IP: Avalon-MM

---

# 23. Lỗi sinh viên thường gặp
- Nhầm bus điều khiển và bus dữ liệu
- Dùng AXI4 full cho bài toán chỉ cần vài thanh ghi
- Không tách control path và data path
- Không hiểu vai trò handshake
- Không xử lý wait / ready đúng
- Quên timing khi tích hợp nhiều slave
- Chọn bus quá phức tạp cho bài toán nhỏ

---

# 24. Kết luận
- Không có bus nào “tốt nhất” cho mọi bài toán
- Mỗi bus sinh ra cho một mục tiêu khác nhau
- APB: đơn giản
- AHB: bus hệ thống mức trung bình
- AXI: hiệu năng cao
- Avalon: rất phù hợp hệ Intel/Altera
- Cần chọn bus theo:
  - băng thông
  - độ trễ
  - độ phức tạp
  - công cụ hỗ trợ
  - nền tảng FPGA

---

# 25. Đề tài nhóm 1
## Thiết kế GPIO Slave dùng APB
- Mục tiêu:
  - Tạo IP GPIO có thanh ghi điều khiển
- Yêu cầu:
  - Hỗ trợ đọc / ghi LED và switch
- Kiến thức:
  - APB slave
  - thanh ghi memory-mapped
- Mở rộng:
  - thêm interrupt

---

# 26. Đề tài nhóm 2
## Thiết kế Timer/Counter dùng APB hoặc AXI4-Lite
- Mục tiêu:
  - Tạo timer có ngắt định kỳ
- Yêu cầu:
  - thanh ghi period, enable, status
- Kiến thức:
  - register map
  - interrupt
  - bus control

---

# 27. Đề tài nhóm 3
## Thiết kế UART đơn giản nối với bus
- Mục tiêu:
  - Xây IP UART có thể điều khiển từ CPU
- Yêu cầu:
  - TX, RX, status register
- Kiến thức:
  - UART
  - bus slave
  - polling hoặc interrupt

---

# 28. Đề tài nhóm 4
## Thiết kế IP tính y = a*x + b dùng AXI4-Lite
- Mục tiêu:
  - CPU ghi a, x, b vào thanh ghi
  - IP trả về kết quả y
- Kiến thức:
  - AXI4-Lite
  - register mapping
  - testbench

---

# 29. Đề tài nhóm 5
## Thiết kế FIFO stream dùng AXI4-Stream hoặc Avalon-ST
- Mục tiêu:
  - Truyền dữ liệu dạng luồng giữa 2 IP
- Yêu cầu:
  - valid / ready / last
- Kiến thức:
  - streaming protocol
  - backpressure
  - buffer

---

# 30. Đề tài nhóm 6
## Thiết kế bộ lọc FIR stream
- Mục tiêu:
  - Nhận dữ liệu luồng vào, xuất luồng ra
- Giao tiếp:
  - AXI4-Stream hoặc Avalon-ST
- Kiến thức:
  - DSP cơ bản
  - stream interface
  - latency / throughput

---

# 31. Đề tài nhóm 7
## Thiết kế DMA mô phỏng đơn giản
- Mục tiêu:
  - Truyền block dữ liệu từ memory sang IP
- Gợi ý:
  - Mô hình hóa thay vì làm DMA hoàn chỉnh
- Kiến thức:
  - burst
  - memory-mapped transfer
  - master/slave

---

# 32. Đề tài nhóm 8
## So sánh hiệu năng APB vs AHB vs AXI bằng mô phỏng
- Mục tiêu:
  - Đo số chu kỳ truyền cho cùng khối dữ liệu
- Kết quả:
  - bảng số liệu
  - đồ thị
  - phân tích ưu nhược điểm
- Kiến thức:
  - timing
  - throughput
  - latency

---

# 33. Đề tài nhóm 9
## Tích hợp Nios II với IP tự thiết kế qua Avalon-MM
- Mục tiêu:
  - CPU điều khiển IP custom
- Yêu cầu:
  - có chương trình C đọc/ghi thanh ghi
- Kiến thức:
  - Platform Designer
  - Avalon-MM
  - embedded software

---

# 34. Đề tài nhóm 10
## Hệ thống mini SoC: CPU + Bus + UART + Timer + IP custom
- Mục tiêu:
  - Xây một SoC nhỏ hoàn chỉnh
- Thành phần:
  - CPU mềm
  - memory
  - bus interconnect
  - 2 peripheral
  - 1 IP tự thiết kế
- Kết quả:
  - block design
  - demo chạy trên board hoặc simulation

---

# 35. Tiêu chí đánh giá đề tài nhóm
- Đúng chức năng bus
- Có sơ đồ khối rõ ràng
- Có mô phỏng testbench
- Có giải thích tín hiệu chính
- Có báo cáo:
  - mục tiêu
  - thiết kế
  - kết quả
  - khó khăn
  - hướng mở rộng

---

# 36. Câu hỏi thảo luận cuối buổi
- Vì sao APB không phù hợp cho truyền dữ liệu lớn?
- Khi nào nên chọn AXI4-Lite thay vì AXI4 full?
- AXI4-Stream khác gì với AXI4 memory-mapped?
- Vì sao Avalon-MM thuận tiện với Nios II?
- Nếu thiết kế IP CNN mini, nên dùng bus nào cho control? bus nào cho data?

---

# 37. Tài liệu tham khảo chính
- Chương 1: Tổng quan hệ thống SoC
- Chương 4: Hệ thống kết nối
- Giáo trình: Thiết kế hệ thống SoC trên FPGA
- Chủ đề liên quan:
  - APB
  - AHB
  - AXI4 / AXI4-Lite / AXI4-Stream
  - Avalon bus

---

# 38. Hết
## Câu hỏi?
