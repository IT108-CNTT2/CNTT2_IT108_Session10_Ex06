# Phân tích Định dạng Tệp & Chuyển đổi Tài liệu Dự án GreenTech

---

## PHẦN 1: PHÂN TÍCH TƯ DUY & LỖI KỸ THUẬT CỦA NAM

### 1. Hai sai lầm chính trong tư duy dùng Rich Text (.docx) làm tài liệu mã nguồn

#### Sai lầm 1: Nhầm lẫn giữa Tệp nhị phân (Binary File) và Tệp văn bản thô (Plain Text)
* **Bản chất của file `.docx`:** Thực chất là một tập hợp các file XML, CSS, hình ảnh... được nén lại dưới dạng tệp nhị phân (Binary File). Trình duyệt hoặc GitHub không thể đọc trực tiếp nếu không qua bộ giải mã của Microsoft Word.
* **Hệ quả trên Git (Git Diff failure):** Git theo dõi thay đổi theo từng dòng văn bản (Line-by-line). Vì `.docx` là file nhị phân, Git coi toàn bộ file là một khối dữ liệu lớn. Khi Nam chỉ sửa một dấu phẩy, cấu trúc nén thay đổi hoàn toàn, làm Git đánh dấu toàn bộ file bị thay đổi. Điều này dẫn đến tình trạng báo xung đột (Conflict) liên tục và không thể xem lịch sử chỉnh sửa chi tiết.

#### Sai lầm 2: Nhầm lẫn về khả năng chống hư hại dữ liệu (Data Corruption & Reliability)
* **Bản chất cấu trúc:** File `.docx` phụ thuộc vào tính toàn vẹn của cấu trúc nén và các thẻ XML.
* **Hệ quả khi mất dữ liệu:** Nếu bị rớt mạng hoặc lỗi truyền tải làm mất dù chỉ $1\text{ byte}$ dữ liệu trong file `.docx`, toàn bộ cấu trúc mã hóa/nén bị phá vỡ, làm file bị lỗi hỏng (Corrupted) và không thể mở được nữa.

---

### 2. Ưu thế vượt trội của Markdown (Plain Text)

1. **An toàn và chống hư hại:** Markdown là **Plain Text** (Văn bản thô mã hóa UTF-8). Nếu rớt mạng và mất $1\text{ byte}$ dữ liệu, bạn chỉ bị mất đúng 1 ký tự tại vị trí đó, $99.9\%$ nội dung còn lại vẫn hoàn toàn đọc được bình thường.
2. **Dung lượng siêu nhẹ & Tương thích Git:**
   * File `.docx` thường tốn hàng trăm KB đến vài MB cho định dạng trang, font chữ, style.
   * File `.md` chỉ tốn vài KB (đúng bằng dung lượng của các ký tự chữ).
   * Cho phép xem trực tiếp trên GitHub/StackEdit và hỗ trợ Git Diff so sánh từng dòng thay đổi cực kỳ chính xác.

---

## PHẦN 2: CHUYỂN ĐỔI TÀI LIỆU SANG MARKDOWN (.MD)

Below is the converted content from the Word document into clean, standardized Markdown format:

```markdown
# 🌿 Dự án GreenTech - Hệ thống Nông nghiệp Thông minh

**GreenTech** là giải pháp ứng dụng công nghệ **IoT** và **Trí tuệ nhân tạo (AI)** vào quản lý trang trại nhằm tối ưu hóa lượng nước tưới, phân bón và theo dõi sức khỏe cây trồng theo thời gian thực.

---

## 🎯 Mục tiêu Dự án

* **Tối ưu tài nguyên:** Tiết kiệm đến $30\%$ lượng nước tưới và $20\%$ lượng phân bón.
* **Tự động hóa:** Giảm $50\%$ nhân công vận hành nhờ hệ thống điều khiển thông minh.
* **Cảnh báo sớm:** Phát hiện dịch bệnh trên lá cây nhờ mô hình Computer Vision.

---

## 🛠 Thách thức Kỹ thuật & Giải pháp

1. *Thách thức:* Môi trường trang trại có độ ẩm cao, sóng Wi-Fi kém.
   * *Giải pháp:* Sử dụng chuẩn truyền dữ liệu **LoRaWAN** tiết kiệm năng lượng và khoảng cách truyền xa.

2. *Thách thức:* Dữ liệu cảm biến gửi về bị nhiễu.
   * *Giải pháp:* Tích hợp bộ lọc **Kalman Filter** ngay tại vi điều khiển SoC.

---

> **Thông điệp dự án:** *"Công nghệ xanh cho tương lai bền vững."*

Để biết thêm chi tiết, vui lòng liên hệ nhóm phát triển tại [GreenTech GitHub Repository](https://github.com/greentech-ptit).
```
