# ECONOMIC RULES — KTS CLASS FUND

## 1. Dòng tiền và quyền lợi

### 1.1. Mục đích của quỹ

KTS Class Fund mô phỏng một quỹ lớp được quản lý thông qua Smart Contract.

Quỹ được sử dụng để phục vụ các khoản chi chung của lớp, ví dụ:

- chi phí in tài liệu;
- chi phí phục vụ hoạt động học tập;
- mua vật dụng chung;
- tổ chức hoạt động lớp;
- các khoản chi được giảng viên hoặc ban cán sự đề xuất.

Phiên bản thử nghiệm sử dụng Sepolia ETH.

Sepolia ETH chỉ được sử dụng để mô phỏng cơ chế vận hành,
không đại diện cho tiền VNĐ thật.

---

### 1.2. Dòng tiền vào

Tiền được gửi vào Smart Contract KTS Class Fund.

Luồng tiền:

Người gửi
→ KTS Class Fund
→ số dư quỹ tăng.

Mỗi lần nạp tiền phải ghi nhận:

- địa chỉ người gửi;
- số tiền;
- thời gian;
- Transaction Hash.

Người gửi tiền vào quỹ không tự động nhận thêm quyền quản trị.

Ví dụ:

Một sinh viên gửi ETH vào quỹ
→ sinh viên đó vẫn chỉ có quyền theo dõi,
không được Confirm hoặc Execute.

---

### 1.3. Dòng tiền ra

Tiền chỉ được chuyển ra khỏi Smart Contract
thông qua một Request hợp lệ.

Luồng:

Create Request
→ Ban cán sự Confirm
→ đạt ít nhất 4/5
→ Ready
→ Execute
→ tiền chuyển tới người nhận.

Không được có cách khác để rút tiền trực tiếp khỏi Smart Contract
mà bỏ qua quy trình trên.

---

### 1.4. Quyền lợi của sinh viên

Sinh viên có quyền theo dõi:

- số dư quỹ;
- lịch sử tiền vào;
- lịch sử tiền ra;
- các Request đang chờ;
- người tạo Request;
- nội dung khoản chi;
- số tiền;
- người nhận;
- số lượt Confirm;
- trạng thái Request.

Sinh viên thông thường không có quyền:

- tạo Request;
- Confirm;
- Execute.

Mục tiêu là cho sinh viên quyền giám sát
mà không trao quyền trực tiếp chi tiền.

---

### 1.5. Quyền của giảng viên

Giảng viên được cấp vai trò Requester.

Giảng viên có thể:

- tạo yêu cầu chi;
- nhập nội dung;
- nhập số tiền;
- nhập địa chỉ người nhận;
- theo dõi trạng thái Request.

Việc giảng viên tạo Request không tự động làm tiền được chi.

Giảng viên không:

- Confirm;
- Execute.

Ban cán sự thực hiện bước Confirm
để kiểm tra thông tin trước khi khoản chi được thực hiện.

---

### 1.6. Quyền của ban cán sự

Ban cán sự quản lý quỹ gồm 5 người:

1. Lớp trưởng.
2. Lớp phó 1.
3. Lớp phó 2.
4. Bí thư.
5. Phó Bí thư.

Mỗi người được đại diện bởi một địa chỉ ví riêng.

Ban cán sự có thể:

- tạo Request nội bộ;
- Confirm Request;
- Execute Request khi đủ điều kiện.

Mỗi thành viên có quyền xác nhận ngang nhau.

Một Confirm tương ứng với một địa chỉ ví,
không phụ thuộc chức vụ.

---

## 2. Giới hạn chống lạm dụng

### 2.1. Không cho người ngoài Confirm

Chỉ 5 địa chỉ ban cán sự được quyền Confirm.

Nếu địa chỉ khác cố Confirm:

→ giao dịch phải bị từ chối.

Mục đích:

ngăn sinh viên hoặc người ngoài giả phiếu xác nhận.

---

### 2.2. Một người không được Confirm nhiều lần

Một địa chỉ chỉ được tính một lượt Confirm cho mỗi Request.

Nếu một người cố Confirm lần thứ hai:

→ giao dịch phải bị từ chối.

Mục đích:

ngăn một người giả tạo đủ số lượt xác nhận.

---

### 2.3. Ngưỡng tối thiểu 4/5

Nguyên tắc của đề tài là cần ít nhất 2/3 ban cán sự xác nhận.

Ban cán sự có 5 người.

Ngưỡng:

ceil(5 × 2 / 3) = 4.

Do đó:

- 0/5 → chưa đủ;
- 1/5 → chưa đủ;
- 2/5 → chưa đủ;
- 3/5 → chưa đủ;
- 4/5 → đủ;
- 5/5 → đủ.

Smart Contract không cho Execute nếu chưa đạt 4/5.

---

### 2.4. Tạo Request không tự động có phiếu

Người tạo Request không tự động được tính một lượt Confirm.

Ví dụ:

Lớp trưởng tạo Request
→ Confirmation = 0/5.

Nếu lớp trưởng muốn xác nhận,
phải thực hiện Confirm riêng.

Mục đích:

tách biệt hành động đề xuất khoản chi
với hành động xác nhận khoản chi.

---

### 2.5. Không thay đổi thông tin sau khi tạo

Sau khi Request được tạo,
không được thay đổi:

- số tiền;
- người nhận;
- nội dung chính của khoản chi.

Nếu nhập sai:

→ phải tạo Request mới.

Mục đích:

ngăn trường hợp ban cán sự đã Confirm một khoản
nhưng sau đó người tạo thay đổi thông tin.

---

### 2.6. Giới hạn thời gian 7 ngày

Mỗi Request có hiệu lực trong 7 ngày.

Nếu hết 7 ngày mà chưa đủ 4/5 Confirm:

→ Request được xem là Expired.

Request Expired:

- không được Confirm thêm;
- không được Execute;
- không được khôi phục.

Nếu khoản chi vẫn cần thiết:

→ tạo Request mới.

Mục đích:

tránh Request tồn tại vô thời hạn
và sau một thời gian dài bất ngờ được thực hiện.

---

### 2.7. Kiểm tra số dư trước khi Execute

Request có thể đã đủ 4/5
nhưng tại thời điểm Execute quỹ có thể không còn đủ tiền.

Do đó:

nếu amount > fund balance

→ Execute phải bị từ chối.

---

### 2.8. Một Request chỉ được Execute một lần

Sau khi Execute thành công:

Request → Executed.

Mọi lần Execute sau đó phải bị từ chối.

Mục đích:

ngăn cùng một khoản chi bị chuyển tiền nhiều lần.

---

### 2.9. Chỉ ban cán sự được Execute

Giảng viên có quyền tạo Request
nhưng không trực tiếp rút tiền khỏi quỹ.

Sinh viên cũng không được Execute.

Chỉ một trong 5 thành viên ban cán sự
được gọi Execute sau khi Request đủ điều kiện.

---

## 3. Quyền quản trị

### 3.1. Nhóm Requester

Giảng viên được cấp quyền Requester.

Requester có quyền tạo Request
nhưng không có quyền Confirm hoặc Execute.

---

### 3.2. Nhóm ban cán sự

Ban cán sự có 5 thành viên:

- Lớp trưởng.
- Lớp phó 1.
- Lớp phó 2.
- Bí thư.
- Phó Bí thư.

Các thành viên này có quyền:

- Confirm;
- Execute;
- tạo Request nội bộ.

---

### 3.3. Nguyên tắc nhiều người kiểm soát

Không một thành viên ban cán sự nào
có thể tự mình làm cho một Request đủ điều kiện Execute.

Cần ít nhất 4 địa chỉ khác nhau trong 5 địa chỉ ban cán sự.

Điều này làm giảm sự phụ thuộc vào một cá nhân.

---

### 3.4. Quyền của sinh viên

Sinh viên có quyền giám sát
nhưng không có quyền tác động trực tiếp tới tiền trong quỹ.

Điều này tách:

quyền xem
khỏi
quyền quản trị tiền.

---

### 3.5. Danh sách quản trị trong phiên bản v0.1

Trong phiên bản đầu,
các địa chỉ:

- giảng viên;
- lớp trưởng;
- lớp phó;
- bí thư;
- phó bí thư

được thiết lập khi triển khai Smart Contract.

Phiên bản hiện tại chưa hỗ trợ
thay đổi các địa chỉ quản trị sau khi deploy.

---

## 4. Tình huống người dùng có thể bị thiệt

### Tình huống 1 — Một thành viên cố tạo nhiều phiếu Confirm

Ví dụ:

Lớp trưởng cố Confirm 4 lần
để tự đạt đủ 4/5.

Người bị ảnh hưởng:

toàn bộ sinh viên có tiền trong quỹ.

Biện pháp:

mỗi địa chỉ chỉ được Confirm một lần cho mỗi Request.

---

### Tình huống 2 — Người ngoài cố Confirm

Một sinh viên không thuộc ban cán sự
cố tham gia xác nhận.

Người bị ảnh hưởng:

lớp và các thành viên đã đóng quỹ.

Biện pháp:

Smart Contract kiểm tra địa chỉ người gọi
có thuộc danh sách ban cán sự hay không.

---

### Tình huống 3 — Thay đổi số tiền sau khi đã được Confirm

Ví dụ:

Ban cán sự Confirm Request:

Chi 0.05 ETH.

Sau đó người tạo thay thành:

0.5 ETH.

Người bị ảnh hưởng:

sinh viên và quỹ lớp.

Biện pháp:

không cho sửa số tiền hoặc người nhận sau khi tạo Request.

---

### Tình huống 4 — Execute trước khi đủ số xác nhận

Ví dụ:

Request mới có 3/5 Confirm
nhưng một thành viên cố Execute.

Người bị ảnh hưởng:

toàn bộ lớp.

Biện pháp:

Smart Contract bắt buộc kiểm tra
confirmationCount >= 4.

Nếu chưa đủ:

→ từ chối.

---

### Tình huống 5 — Execute cùng một Request nhiều lần

Ví dụ:

Request chi 0.1 ETH.

Execute lần 1:
→ chuyển 0.1 ETH.

Người dùng cố Execute lần 2:
→ nếu không bị chặn, quỹ mất thêm 0.1 ETH.

Người bị ảnh hưởng:

toàn bộ sinh viên.

Biện pháp:

sau lần Execute đầu tiên:

executed = true.

Mọi lần Execute tiếp theo bị từ chối.

---

### Tình huống 6 — Request cũ được thực hiện quá muộn

Một Request được tạo từ lâu
nhưng chưa đủ xác nhận.

Sau nhiều tuần,
các thành viên tiếp tục Confirm
và thực hiện một khoản chi không còn phù hợp.

Người bị ảnh hưởng:

lớp và người quản lý quỹ.

Biện pháp:

mỗi Request chỉ có hiệu lực 7 ngày.

Sau deadline:

→ Expired.

---

### Tình huống 7 — Quỹ không đủ tiền

Request đã đủ 4/5 Confirm
nhưng quỹ hiện tại không còn đủ số dư.

Nếu vẫn chuyển tiền,
hệ thống có thể hoạt động không đúng quy tắc.

Biện pháp:

kiểm tra số dư ngay tại thời điểm Execute.

Nếu không đủ:

→ từ chối.

---

### Tình huống 8 — Giảng viên tự tạo và tự chi tiền

Nếu một Requester vừa có quyền tạo
vừa có quyền Execute,
quá trình kiểm soát nhiều người sẽ bị mất ý nghĩa.

Người bị ảnh hưởng:

sinh viên trong lớp.

Biện pháp:

tách quyền:

Giảng viên
→ Create Request.

Ban cán sự
→ Confirm và Execute.

---

## 5. Quy tắc kinh tế cốt lõi của sản phẩm

Quy tắc quan trọng nhất của KTS Class Fund là:

> Không một cá nhân nào có thể tự mình làm cho một khoản chi được thực hiện.

Một khoản chi phải đi qua:

Create Request
→ tối thiểu 4/5 ban cán sự Confirm
→ kiểm tra deadline
→ kiểm tra số dư
→ Execute một lần.

Đây là cơ chế chính giúp KTS Class Fund
tạo sự minh bạch và kiểm soát nhiều người đối với quỹ lớp.