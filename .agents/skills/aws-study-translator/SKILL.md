---
name: aws-study-translator
description: >-
  Use this skill when the user asks to translate English sentences, bullet points,
  exam tips, or sections into Vietnamese while studying AWS SAA-C03 materials,
  or asks to add inline Vietnamese translations to study markdown files.
---

# AWS Study Translator (Song ngữ Anh - Việt Inline)

Skill này hỗ trợ dịch tài liệu học tập AWS SAA-C03 sang tiếng Việt theo định dạng chú thích nối tiếp (inline parenthetical translation), giữ nguyên câu gốc tiếng Anh và chèn bản dịch tiếng Việt trong ngoặc đơn `(...)` ngay phía sau.

## Quy tắc trình bày (Formatting Rules)

1. **Giữ nguyên 100% văn bản gốc tiếng Anh** (bao gồm cả markdown, bullet `-`, số thứ tự `1.`, emoji 🎯, in đậm `**...**`, code inline `` `...` ``).
2. **Chèn bản dịch tiếng Việt vào trong dấu ngoặc đơn `(...)` ở cuối dòng/câu**, cách câu gốc một khoảng trắng:
   - Mẫu chuẩn: `<Câu tiếng Anh gốc> (<Bản dịch tiếng Việt>)`
3. **Ví dụ chuẩn (từ tài liệu hiện tại)**:
   - Bullet thông thường:
     ```markdown
     - A geographical area containing multiple Availability Zones (Một khu vực địa lý bao gồm nhiều Vùng sẵn sàng (Availability Zones))
     - Completely independent and isolated from other regions (Hoàn toàn độc lập và tách biệt khỏi các khu vực khác)
     - Connected to other AZs via low-latency links (Được kết nối với các AZ khác thông qua các đường truyền có độ trễ thấp)
     ```
   - Danh sách đánh số có từ khóa:
     ```markdown
     1. Compliance - Data sovereignty requirements (Tuân thủ - Các yêu cầu về chủ quyền dữ liệu)
     2. Proximity - Latency to end users (Khoảng cách gần - Độ trễ đối với người dùng cuối)
     ```
   - Exam Tip / Ghi chú:
     ```markdown
     **Exam Tip**: 🎯 Choose the region closest to your users to minimize latency. (Hãy chọn khu vực gần người dùng của bạn nhất để giảm thiểu độ trễ.)
     ```

## Quy tắc dịch thuật ngữ AWS

- **Giữ nguyên tên riêng dịch vụ và viết tắt phổ biến của AWS**: `Region`, `AZ`, `Edge Location`, `VPC`, `EC2`, `S3`, `IAM`, `CloudFront`, `Route 53`, `Multi-AZ`, `Auto Scaling`, v.v.
- Nếu một thuật ngữ xuất hiện lần đầu hoặc mang tính khái niệm (như `Availability Zones`, `Data sovereignty`, `Fault tolerance`, `High availability`), dịch nghĩa tiếng Việt sát với ngữ cảnh Cloud/AWS và có thể giữ từ gốc trong ngoặc nếu cần làm rõ.
- Văn phong dịch: Tự nhiên, rõ nghĩa kỹ thuật, ngắn gọn, dễ ôn tập thi chứng chỉ SAA-C03.

## Quy trình thực hiện (Workflow)

1. **Trường hợp 1: Người dùng gửi câu/đoạn tiếng Anh trong khung chat hoặc yêu cầu dịch một số câu cụ thể đang đọc**
   - Nếu câu đó nằm trong file bài học hiện tại (ví dụ `01-AWS-Fundamentals/README.md`) và người dùng muốn cập nhật vào bài: dùng công cụ `edit_file` để thêm `(<Bản dịch tiếng Việt>)` trực tiếp vào dòng tương ứng trong file, đồng thời hiển thị kết quả trong chat.
   - Nếu người dùng chỉ hỏi nhanh hoặc dán câu lẻ vào chat: trả lời theo đúng định dạng `<Câu gốc> (<Bản dịch tiếng Việt>)` để người dùng có thể đọc hoặc copy ngay.

2. **Trường hợp 2: Người dùng chỉ định dịch một mục (section) hoặc các dòng trong file**
   - Đọc nội dung mục đó bằng `read_file`.
   - Chỉ dịch các dòng nội dung giải thích/ý chính (bỏ qua sơ đồ ASCII, block lệnh CLI, hoặc dòng chỉ chứa số liệu/mã vùng đơn giản như ``us-east-1`` trừ khi người dùng yêu cầu).
   - Dùng `edit_file` cập nhật trực tiếp vào file theo đúng định dạng `<Dòng gốc> (<Bản dịch tiếng Việt>)`.
