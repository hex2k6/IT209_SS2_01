# Bài 1: Khởi tạo Droplet trên DigitalOcean và kết nối bằng SSH Key

> **Trạng thái: Chưa hoàn thành — đây là mẫu báo cáo.**
> Thay các mục `[Điền ...]` bằng thông tin thực tế. Chỉ đánh dấu hoàn thành sau khi đã thực hiện và có bằng chứng.

## 1. Thông tin bài làm

- Họ tên: [Điền họ tên]
- Ngày thực hiện: [Điền ngày]
- Mục tiêu: Tạo Droplet Ubuntu tại Singapore với cấu hình tiết kiệm và kết nối từ máy cá nhân bằng tài khoản `root`, xác thực bằng SSH key.

## 2. Cấu hình Droplet thực tế

| Hạng mục | Thông tin |
| --- | --- |
| Tên Droplet | [Điền tên] |
| Hệ điều hành | [Điền phiên bản Ubuntu; yêu cầu Ubuntu 22.04 LTS hoặc mới hơn] |
| Region | [Điền region đã chọn; yêu cầu Singapore] |
| Gói | [Điền gói đã chọn; yêu cầu Basic, Shared CPU, Regular SSD] |
| CPU / RAM / Disk | [Điền cấu hình] |
| Giá hiển thị khi tạo | [Điền giá thực tế trên Console] |
| Authentication | [Điền phương thức đã chọn; yêu cầu SSH Keys] |
| Địa chỉ IP | [Điền IP hoặc che một phần khi công khai] |

## 3. Các bước thực hiện

### Bước 1: Tạo cặp khóa SSH trên máy cá nhân

Chạy trong Terminal hoặc PowerShell:

```sh
ssh-keygen -t ed25519 -C "your_email@example.com"
```

Thay email ví dụ bằng thông tin của bạn. Chọn đường dẫn lưu khóa; nếu đã có khóa ở đường dẫn đó, chọn tên mới để tránh ghi đè. Có thể đặt passphrase để bảo vệ private key.

- Đường dẫn khóa công khai: [Điền đường dẫn tệp có đuôi `.pub`]
- Tên khóa dùng trong bài: [Điền tên]

Xem khóa công khai trên Windows PowerShell (điều chỉnh đường dẫn nếu dùng tên khác):

```powershell
Get-Content "$env:USERPROFILE\.ssh\id_ed25519.pub"
```

Hoặc trên Linux/macOS:

```sh
cat ~/.ssh/id_ed25519.pub
```

Chỉ sao chép nội dung **public key** để thêm vào DigitalOcean. Không đưa private key, mật khẩu hoặc access token vào repository hay ảnh chụp.

### Bước 2: Tạo Droplet

1. Đăng nhập DigitalOcean và mở phần tạo Droplet.
2. Chọn Ubuntu 22.04 LTS hoặc phiên bản mới hơn theo yêu cầu bài.
3. Chọn Singapore và cấu hình Basic / Shared CPU / Regular SSD tiết kiệm nhất phù hợp. Ghi lại giá thực tế hiển thị.
4. Tại Authentication, chọn **SSH Keys**; thêm toàn bộ nội dung public key `.pub`, đặt tên và chọn khóa đó cho Droplet.
5. Đặt tên Droplet, kiểm tra cấu hình và tạo máy chủ.
6. Khi máy chủ sẵn sàng, lấy địa chỉ IP để kết nối.

Ghi chú thực tế: [Điền các thao tác hoặc khác biệt trên giao diện, nếu có]

### Bước 3: Kết nối SSH từ máy cá nhân

Linux/macOS:

```sh
ssh -i ~/.ssh/id_ed25519 root@<IP_ADDRESS_DROPLET>
```

Windows PowerShell:

```powershell
ssh -i "$env:USERPROFILE\.ssh\id_ed25519" root@<IP_ADDRESS_DROPLET>
```

Thay `<IP_ADDRESS_DROPLET>` bằng IP thật và dùng đúng đường dẫn private key đã tạo. Khi kết nối lần đầu, kiểm tra fingerprint của máy chủ qua nguồn tin cậy trước khi chấp nhận. Nếu khóa có passphrase, SSH có thể yêu cầu passphrase; đây không phải mật khẩu tài khoản `root`.

Sau khi đăng nhập, có thể kiểm tra:

```sh
whoami
cat /etc/os-release
```

Kết quả thực tế: [Điền tài khoản, phiên bản Ubuntu và tình trạng kết nối; chưa thực hiện thì ghi chưa thực hiện]

## 4. Bằng chứng thực hiện

Đính kèm ảnh Console thể hiện Droplet đã tạo **hoặc** log Terminal kết nối thành công theo yêu cầu bài. Kiểm tra và che thông tin nhạy cảm trước khi công khai.

### Ảnh chụp (nếu sử dụng)

Lưu ảnh thật vào thư mục `images/` cạnh README này. Sau đó thêm liên kết, ví dụ: `![Droplet trên Console](images/droplet-console.png)`.

[Chưa đính kèm ảnh thực tế]

### Log kết nối (nếu sử dụng)

```text
[Dán log thực tế tại đây, gồm lệnh kết nối và thông tin chào mừng Ubuntu hoặc kết quả kiểm tra. Không dùng log giả lập.]
```

## 5. Kiểm tra trước khi nộp

- [ ] Đã tạo Droplet Ubuntu đúng yêu cầu.
- [ ] Đã chọn region Singapore và ghi cấu hình, giá thực tế.
- [ ] Đã chọn SSH Keys và gán đúng public key khi khởi tạo.
- [ ] Đã kết nối thành công từ máy cá nhân bằng `root` và SSH key, không dùng mật khẩu tài khoản máy chủ.
- [ ] Đã bổ sung ảnh chụp hoặc log thực tế.
- [ ] Đã thay các mục cần điền và cập nhật trạng thái bài làm.
- [ ] Đã kiểm tra không có private key, mật khẩu hoặc token trong nội dung nộp.
- [ ] Đã lưu bài trong `homework/session_02/ex1/README.md` trên GitHub.

Đường dẫn bài nộp: [Điền URL thư mục `homework/session_02/ex1/` trên GitHub sau khi đưa lên]

