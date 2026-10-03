# PROJECT PLAN — KTS Class Fund

## 1. Thành viên và vai trò

| Họ tên | Vai chính Lab 8–11 | Vai chính Lab 12–15 |
|---|---|---|
| Trần Hoàng Phương Dung | Đặc tả nghiệp vụ & Kiểm thử | Hợp đồng & Giao diện |
| Võ Ngọc Tâm Phúc | Hợp đồng & Giao diện | Đặc tả nghiệp vụ & Kiểm thử |

Hai thành viên phối hợp kiểm tra chéo công việc của nhau.
Vai trò được thay đổi ở giai đoạn sau để cả hai đều hiểu toàn bộ sản phẩm.

## 2. Người dùng và vấn đề

### Người dùng chính

Sinh viên trong một lớp học có quỹ chung.

### Vấn đề cần giải quyết

Quỹ lớp truyền thống thường do một người, chẳng hạn thủ quỹ, trực tiếp quản lý.
Thông tin về đề nghị chi, người đồng ý, số tiền và lịch sử chuyển tiền có thể
nằm rải rác trên tin nhắn, Excel và tài khoản của người giữ quỹ.

KTS Class Fund hướng tới việc ghi nhận các đề nghị chi và việc phê duyệt
trên Smart Contract để một cá nhân không thể tự quyết định khoản chi.

### Sản phẩm cuối nhìn thấy được

Một Web DApp cho phép:

- Xem số dư quỹ.
- Xem các đề nghị chi và trạng thái của chúng.
- Tạo đề nghị chi.
- Thành viên có quyền thực hiện phê duyệt.
- Chỉ thực hiện khoản chi khi đạt ít nhất 2/3 phiếu phê duyệt.
- Xem lịch sử giao dịch và Transaction Hash.

Smart Contract được triển khai thử nghiệm trên mạng Sepolia.

## 3. Luồng cốt lõi

Nạp tiền vào quỹ
→ Tạo đề nghị chi
→ Ban quản lý quỹ xem xét
→ Phê duyệt
→ Đủ ít nhất 2/3
→ Thực hiện khoản chi một lần

## 4. Mốc bắt buộc

### Lab 8
- Repo nhóm được thiết lập.
- Có PROJECT_PLAN.md.
- Có SPEC.md v0.1.
- Có ECONOMIC_RULES.md.
- Có AI_JOURNAL.md.

### Lab 9
- ProjectCore.sol biên dịch được.
- Có ít nhất một luồng cốt lõi của KTS Class Fund.

### Lab 10
- Audit mã nguồn.
- Phát hiện và sửa lỗi có bằng chứng.

### Lab 11
- Cài quy tắc phê duyệt 2/3 vào sản phẩm.
- Có ca hợp lệ và ca vi phạm bị từ chối.

### Lab 12
- Gate Review 1.

### Lab 13
- Kiểm thử ca tấn công hoặc gian lận.
- Hardening ProjectCore.sol.

### Lab 14
- Audit chéo với nhóm khác.

### Lab 15
- Kết nối Web DApp với ProjectCore.sol.
- Deploy sản phẩm.
- Có URL công khai và Transaction Hash.