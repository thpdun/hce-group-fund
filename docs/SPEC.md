# SPEC — HCE CLASS FUND

## 1. Mục đích

HCE Class Fund là hệ thống hỗ trợ quản lý quỹ lớp bằng Smart Contract.

Hệ thống được xây dựng nhằm tạo một quy trình minh bạch hơn cho việc quản lý
các khoản thu, yêu cầu chi, xác nhận yêu cầu và thực hiện khoản chi của lớp.

HCE Class Fund cho phép:

- ghi nhận tiền được gửi vào quỹ;
- theo dõi số dư quỹ;
- tạo yêu cầu chi;
- ghi nhận xác nhận của ban cán sự;
- kiểm soát thời hạn xử lý yêu cầu;
- chỉ thực hiện khoản chi khi đáp ứng đủ điều kiện;
- lưu lại lịch sử giao dịch để sinh viên có thể theo dõi.

Luồng nghiệp vụ chính:

Nạp tiền vào quỹ
→ Tạo yêu cầu chi
→ Ban cán sự kiểm tra thông tin
→ Xác nhận yêu cầu
→ Đạt đủ ngưỡng xác nhận
→ Thực hiện khoản chi
→ Ghi nhận lịch sử.

Hệ thống không nhằm thay thế vai trò của giảng viên hoặc ban cán sự,
mà sử dụng Smart Contract để kiểm soát các điều kiện thực hiện khoản chi
và giúp thông tin quỹ có thể kiểm tra lại.

---

## 2. Đầu vào

### 2.1. Các nhóm người dùng

Hệ thống có ba nhóm người dùng chính:

1. Sinh viên.
2. Giảng viên.
3. Ban cán sự quản lý quỹ.

Ngoài ra, Smart Contract chịu trách nhiệm tự động kiểm tra các quy tắc nghiệp vụ.

---

### 2.2. Sinh viên

Sinh viên trong lớp là nhóm người dùng theo dõi thông tin quỹ.

Sinh viên có thể:

- xem số dư quỹ;
- xem các khoản tiền đã được nạp;
- xem danh sách yêu cầu chi;
- xem nội dung từng yêu cầu;
- xem số tiền;
- xem địa chỉ người nhận;
- xem người tạo yêu cầu;
- xem số lượng xác nhận;
- xem trạng thái của yêu cầu;
- xem lịch sử các khoản đã được thực hiện.

Sinh viên thông thường không có quyền:

- tạo yêu cầu chi;
- xác nhận yêu cầu;
- thực hiện khoản chi;
- thay đổi thông tin của yêu cầu.

---

### 2.3. Giảng viên

Giảng viên được cấp quyền Requester.

Giảng viên có thể trực tiếp tạo yêu cầu chi trong trường hợp phát sinh
một khoản chi mà lớp cần thực hiện.

Ví dụ:

- chi phí in tài liệu;
- chi phí phục vụ hoạt động học tập;
- một khoản chi chung được giảng viên thông báo cho lớp.

Giảng viên được quyền:

- tạo yêu cầu chi;
- nhập nội dung yêu cầu;
- nhập số tiền;
- nhập địa chỉ người nhận;
- theo dõi trạng thái xử lý yêu cầu.

Giảng viên không có quyền:

- xác nhận yêu cầu;
- thực hiện khoản chi trực tiếp;
- tự động được tính một lượt xác nhận khi tạo yêu cầu.

---

### 2.4. Ban cán sự quản lý quỹ

Ban cán sự quản lý quỹ gồm 5 thành viên:

1. Lớp trưởng.
2. Lớp phó 1.
3. Lớp phó 2.
4. Bí thư.
5. Phó Bí thư.

Mỗi thành viên được đại diện bởi một địa chỉ ví riêng.

Ban cán sự có quyền:

- tạo yêu cầu chi nội bộ của lớp;
- kiểm tra thông tin của yêu cầu;
- xác nhận yêu cầu;
- theo dõi trạng thái;
- thực hiện khoản chi khi yêu cầu đã đủ điều kiện.

Ban cán sự không được thay đổi nội dung tài chính của một yêu cầu
sau khi yêu cầu đó đã được tạo.

---

### 2.5. Ngưỡng xác nhận

Một yêu cầu phải được ít nhất 2/3 tổng số thành viên ban cán sự xác nhận.

Ban cán sự có 5 người.

Ngưỡng tối thiểu được tính:

ceil(5 × 2 / 3) = 4.

Do đó:

- 0/5: chưa đủ điều kiện.
- 1/5: chưa đủ điều kiện.
- 2/5: chưa đủ điều kiện.
- 3/5: chưa đủ điều kiện.
- 4/5: đủ điều kiện.
- 5/5: đủ điều kiện.

---

### 2.6. Thông tin của một yêu cầu chi

Mỗi yêu cầu chi phải lưu tối thiểu các thông tin:

- mã yêu cầu;
- địa chỉ người tạo;
- vai trò người tạo;
- nội dung khoản chi;
- địa chỉ người nhận;
- số tiền;
- thời điểm tạo;
- thời hạn xử lý;
- số lượng xác nhận;
- danh sách địa chỉ đã xác nhận;
- trạng thái yêu cầu.

---

### 2.7. Thời hạn xử lý

Mỗi yêu cầu có thời hạn hiệu lực là:

7 ngày kể từ thời điểm tạo.

Khi tạo yêu cầu:

createdAt = thời điểm hiện tại.

deadline = createdAt + 7 ngày.

---

### 2.8. Tiền sử dụng trong phiên bản thử nghiệm

Phiên bản thử nghiệm sử dụng Sepolia ETH.

Sepolia ETH chỉ được sử dụng để mô phỏng cơ chế vận hành của quỹ lớp.

Hệ thống chưa sử dụng tiền VNĐ thật.

---

## 3. Quy tắc nghiệp vụ

### R1 — Nạp tiền vào quỹ

Hệ thống cho phép gửi ETH vào Smart Contract.

Số tiền gửi phải lớn hơn 0.

Mỗi lần nạp tiền phải ghi nhận:

- địa chỉ người gửi;
- số tiền;
- thời điểm giao dịch.

Việc gửi tiền vào quỹ không làm thay đổi quyền của người gửi.

Một sinh viên gửi tiền vào quỹ không tự động trở thành thành viên
có quyền xác nhận.

---

### R2 — Quyền xem thông tin

Thông tin công khai của quỹ phải có thể được đọc để phục vụ việc theo dõi.

Sinh viên có thể xem:

- số dư quỹ;
- các yêu cầu chi;
- người tạo;
- nội dung;
- số tiền;
- người nhận;
- số lượt xác nhận;
- trạng thái;
- lịch sử giao dịch.

Việc xem thông tin không yêu cầu quyền xác nhận.

---

### R3 — Người được tạo yêu cầu chi

Chỉ các địa chỉ thuộc một trong hai nhóm sau được tạo yêu cầu chi:

1. Giảng viên đã được cấp quyền Requester.
2. Thành viên ban cán sự quản lý quỹ.

Sinh viên thông thường không được tạo yêu cầu chi.

---

### R4 — Yêu cầu do giảng viên tạo

Khi giảng viên tạo một yêu cầu chi,
ban cán sự không có vai trò quyết định có đồng ý hay không đồng ý
với yêu cầu của giảng viên.

Thao tác của ban cán sự được hiểu là:

Confirm Request — Xác nhận yêu cầu.

Việc xác nhận có ý nghĩa:

- đã kiểm tra đúng nội dung;
- đã kiểm tra đúng số tiền;
- đã kiểm tra đúng địa chỉ người nhận;
- xác nhận yêu cầu đã sẵn sàng để thực hiện bằng quỹ lớp.

---

### R5 — Yêu cầu do ban cán sự tạo

Ban cán sự có thể tạo các yêu cầu chi phát sinh từ hoạt động nội bộ của lớp.

Ví dụ:

- mua vật dụng chung;
- tổ chức hoạt động lớp;
- chi phí phục vụ sinh hoạt lớp.

Yêu cầu do ban cán sự tạo cũng phải tuân thủ toàn bộ cơ chế xác nhận giống
các yêu cầu do giảng viên tạo.

---

### R6 — Nội dung bắt buộc của yêu cầu

Một yêu cầu chỉ được tạo khi:

- địa chỉ người nhận hợp lệ;
- số tiền lớn hơn 0;
- nội dung chi không rỗng.

Nếu thiếu một trong các thông tin trên,
hệ thống phải từ chối tạo yêu cầu.

---

### R7 — Tạo yêu cầu không được tính là một lượt xác nhận

Việc tạo yêu cầu không tự động được tính là một lượt xác nhận.

Ví dụ:

Giảng viên tạo yêu cầu
→ số xác nhận ban đầu là 0/5.

Nếu lớp trưởng là người tạo yêu cầu
→ số xác nhận ban đầu vẫn là 0/5.

Nếu lớp trưởng muốn xác nhận yêu cầu,
lớp trưởng phải thực hiện thao tác Confirm riêng.

---

### R8 — Người được quyền xác nhận

Chỉ 5 thành viên ban cán sự được quyền Confirm:

- lớp trưởng;
- lớp phó 1;
- lớp phó 2;
- bí thư;
- phó bí thư.

Giảng viên không có quyền Confirm.

Sinh viên thông thường không có quyền Confirm.

Địa chỉ không thuộc danh sách ban cán sự cố Confirm
phải bị từ chối.

---

### R9 — Một thành viên chỉ được xác nhận một lần

Một thành viên ban cán sự chỉ được Confirm cùng một yêu cầu đúng một lần.

Ví dụ:

Lớp trưởng Confirm lần đầu
→ hợp lệ.

Lớp trưởng Confirm lần thứ hai
→ từ chối.

Mỗi địa chỉ chỉ được tính tối đa một lượt xác nhận cho mỗi yêu cầu.

---

### R10 — Ngưỡng xác nhận

Một yêu cầu chỉ đủ điều kiện thực hiện khi có ít nhất:

4 trong 5 thành viên ban cán sự xác nhận.

Các trường hợp:

0/5
→ Pending.

1/5
→ Pending.

2/5
→ Pending.

3/5
→ Pending.

4/5
→ Ready.

5/5
→ Ready.

---

### R11 — Thời hạn xác nhận

Mỗi yêu cầu có thời hạn 7 ngày kể từ thời điểm tạo.

Trong thời gian yêu cầu còn hiệu lực,
ban cán sự có thể thực hiện Confirm.

Sau thời hạn 7 ngày,
nếu yêu cầu vẫn chưa đạt tối thiểu 4/5 xác nhận:

→ yêu cầu được xem là Expired.

Yêu cầu Expired:

- không được Confirm thêm;
- không được Execute;
- không được khôi phục lại.

Nếu khoản chi vẫn cần thực hiện,
phải tạo một yêu cầu mới.

---

### R12 — Đủ xác nhận trước hạn

Không cần chờ đủ 7 ngày để Execute.

Nếu yêu cầu đạt 4/5 hoặc 5/5 xác nhận
trước thời hạn:

→ trạng thái chuyển thành Ready.

Ví dụ:

Ngày 1:
Giảng viên tạo yêu cầu.

Ngày 2:
Lớp trưởng Confirm.
→ 1/5.

Ngày 3:
Lớp phó 1 Confirm.
→ 2/5.

Ngày 4:
Bí thư Confirm.
→ 3/5.

Ngày 5:
Phó Bí thư Confirm.
→ 4/5.

Kết quả:

Request chuyển sang Ready ngay ngày 5.

Không cần chờ đến ngày thứ 7.

---

### R13 — Không được thay đổi yêu cầu sau khi tạo

Sau khi yêu cầu được tạo,
không được thay đổi:

- địa chỉ người nhận;
- số tiền;
- nội dung chính của khoản chi.

Quy tắc này bảo đảm ban cán sự xác nhận đúng thông tin
mà họ đã kiểm tra.

Nếu thông tin bị nhập sai,
yêu cầu cũ không được chỉnh sửa để tiếp tục sử dụng.

Phải tạo một yêu cầu mới với thông tin chính xác.

---

### R14 — Kiểm tra số dư quỹ

Tại thời điểm Execute,
Smart Contract phải kiểm tra số dư hiện tại của quỹ.

Nếu:

số tiền yêu cầu > số dư quỹ

→ Execute phải bị từ chối.

Việc một yêu cầu đã đạt 4/5 xác nhận
không đảm bảo rằng quỹ luôn đủ tiền.

Do đó số dư phải được kiểm tra lại ngay tại thời điểm Execute.

---

### R15 — Người được quyền Execute

Chỉ một trong 5 thành viên ban cán sự được quyền Execute
một yêu cầu đã đủ điều kiện.

Giảng viên không trực tiếp Execute.

Sinh viên thông thường không được Execute.

Luồng đối với yêu cầu của giảng viên:

Giảng viên tạo yêu cầu
→ ban cán sự Confirm
→ đủ 4/5
→ một thành viên ban cán sự Execute.

---

### R16 — Điều kiện Execute

Một yêu cầu chỉ được Execute khi đồng thời thỏa mãn tất cả các điều kiện:

1. Yêu cầu tồn tại.
2. Yêu cầu chưa hết hạn.
3. Yêu cầu đã đạt tối thiểu 4/5 xác nhận.
4. Yêu cầu chưa từng được thực hiện.
5. Quỹ đủ số dư.
6. Địa chỉ người nhận hợp lệ.
7. Người gọi Execute thuộc ban cán sự.

Nếu thiếu bất kỳ điều kiện nào,
giao dịch phải bị từ chối.

---

### R17 — Một yêu cầu chỉ được thực hiện một lần

Sau khi khoản chi được thực hiện thành công:

trạng thái yêu cầu
→ Executed.

Một yêu cầu đã Executed không được Execute lần thứ hai.

Nếu có người cố thực hiện lại,
Smart Contract phải từ chối giao dịch.

---

### R18 — Trạng thái yêu cầu

Một yêu cầu có bốn trạng thái nghiệp vụ:

#### Pending

Yêu cầu:

- vẫn còn trong thời hạn 7 ngày;
- chưa đạt 4/5 xác nhận;
- chưa được thực hiện.

#### Ready

Yêu cầu:

- vẫn còn thời hạn;
- đã đạt tối thiểu 4/5 xác nhận;
- chưa được thực hiện.

#### Executed

Yêu cầu đã được thực hiện thành công.

Không thể thực hiện lại.

#### Expired

Yêu cầu đã quá thời hạn 7 ngày
mà chưa đạt đủ điều kiện thực hiện.

Không được Confirm hoặc Execute tiếp.

---

### R19 — Yêu cầu hết hạn

Smart Contract không cần tự thực hiện giao dịch
đúng thời điểm 7 ngày kết thúc.

Thay vào đó,
khi người dùng tiếp tục tương tác với yêu cầu,
hệ thống phải kiểm tra:

block.timestamp > deadline hay không.

Nếu đã quá deadline và chưa đủ 4/5:

→ yêu cầu được xem là Expired.

Web DApp cũng phải hiển thị yêu cầu đó là hết hạn.

---

### R20 — Theo dõi lịch sử

Hệ thống phải ghi nhận sự kiện khi:

- có tiền được gửi vào quỹ;
- một yêu cầu được tạo;
- một thành viên ban cán sự xác nhận;
- một yêu cầu được thực hiện.

Các sự kiện này được sử dụng để hỗ trợ
Web DApp hiển thị lịch sử hoạt động của quỹ.

---

## 4. Đầu ra

### 4.1. Thông tin tổng quan quỹ

Hệ thống phải cung cấp được:

- số dư quỹ hiện tại;
- tổng số yêu cầu đã tạo;
- số yêu cầu đang Pending;
- số yêu cầu Ready;
- số yêu cầu Executed;
- số yêu cầu Expired.

---

### 4.2. Thông tin từng yêu cầu

Mỗi yêu cầu phải có thể hiển thị:

- mã yêu cầu;
- địa chỉ người tạo;
- vai trò người tạo;
- nội dung khoản chi;
- địa chỉ người nhận;
- số tiền;
- thời điểm tạo;
- deadline;
- số lượng xác nhận;
- danh sách người đã xác nhận;
- trạng thái.

---

### 4.3. Thông tin phục vụ sinh viên

Web DApp dự kiến phải cho sinh viên theo dõi:

- số dư quỹ;
- lịch sử thu;
- lịch sử chi;
- yêu cầu đang chờ;
- yêu cầu đã đủ điều kiện;
- yêu cầu đã thực hiện;
- yêu cầu đã hết hạn.

Sinh viên không cần có quyền quản trị để xem các thông tin này.

---

### 4.4. Sự kiện của Smart Contract

Smart Contract dự kiến phát các sự kiện:

- FundDeposited.
- RequestCreated.
- RequestConfirmed.
- RequestExecuted.

Thông tin trạng thái Expired có thể được xác định dựa trên
deadline và thời điểm hiện tại.

---

## 5. Trường hợp ngoại lệ

### E1 — Sinh viên cố tạo yêu cầu

Kết quả:

Từ chối.

---

### E2 — Sinh viên cố Confirm

Kết quả:

Từ chối.

---

### E3 — Giảng viên cố Confirm

Kết quả:

Từ chối.

Giảng viên có quyền tạo yêu cầu
nhưng không thuộc nhóm xác nhận.

---

### E4 — Người ngoài ban cán sự cố Confirm

Kết quả:

Từ chối.

---

### E5 — Một thành viên Confirm hai lần

Ví dụ:

Lớp trưởng đã Confirm,
sau đó tiếp tục Confirm lần thứ hai.

Kết quả:

Lần thứ hai bị từ chối.

---

### E6 — Chưa đủ 4/5 nhưng cố Execute

Ví dụ:

Request có 3/5 xác nhận.

Một thành viên ban cán sự cố Execute.

Kết quả:

Từ chối vì chưa đạt ngưỡng tối thiểu.

---

### E7 — Quá 7 ngày nhưng mới có 3/5 xác nhận

Kết quả:

Request được xem là Expired.

Không được Confirm thêm.

Không được Execute.

---

### E8 — Cố Confirm yêu cầu đã Expired

Kết quả:

Từ chối.

---

### E9 — Cố Execute yêu cầu đã Expired

Kết quả:

Từ chối.

---

### E10 — Số tiền yêu cầu lớn hơn số dư quỹ

Ví dụ:

Số dư quỹ: 1 ETH.

Yêu cầu chi: 1.5 ETH.

Kết quả:

Execute bị từ chối.

---

### E11 — Execute cùng một yêu cầu lần thứ hai

Lần đầu:

Execute thành công.

Lần thứ hai:

Kết quả:
Từ chối.

---

### E12 — Tạo yêu cầu có số tiền bằng 0

Kết quả:

Không cho phép tạo yêu cầu.

---

### E13 — Địa chỉ người nhận không hợp lệ

Kết quả:

Không cho phép tạo yêu cầu.

---

### E14 — Nội dung yêu cầu rỗng

Kết quả:

Không cho phép tạo yêu cầu.

---

### E15 — Người tạo muốn sửa số tiền sau khi có xác nhận

Kết quả:

Không cho phép sửa.

Nếu thông tin không còn chính xác,
phải tạo yêu cầu mới.

---

### E16 — Giảng viên cố Execute

Kết quả:

Từ chối.

Giảng viên là Requester,
không phải người thực hiện khoản chi.

---

### E17 — Người ngoài ban cán sự cố Execute

Kết quả:

Từ chối.

---

## 6. Ngoài phạm vi

Phiên bản hiện tại chưa xử lý:

- tiền VNĐ thật;
- tài khoản ngân hàng;
- thanh toán qua ngân hàng;
- ứng dụng điện thoại native;
- bỏ phiếu của toàn bộ sinh viên trong lớp;
- chức năng Reject thủ công;
- sửa yêu cầu sau khi đã tạo;
- gia hạn yêu cầu đã Expired;
- thay đổi thời hạn 7 ngày cho từng yêu cầu;
- thay đổi thành viên ban cán sự sau khi contract đã triển khai;
- thêm hoặc xóa giảng viên sau khi contract đã triển khai;
- hóa đơn điện tử;
- chứng từ kế toán;
- nghiệp vụ kế toán quỹ đầy đủ;
- hoàn tiền tự động;
- quy đổi tự động giữa ETH và VNĐ.