# Dragon Blue - iOS Cloud Build (GitHub Actions)

Kho chứa tự động biên dịch ứng dụng **Dragon Blue iOS (.IPA)** bằng **GitHub Actions macOS Runner** (hoàn toàn miễn phí, không cần sở hữu máy Mac).

---

## 🚀 Cách Thức Hoạt Động
1. **GitHub Actions** khởi động một máy ảo **macOS-14 (Apple Silicon)** có sẵn **Xcode 15.4**.
2. Workflow tự động tải bộ dự án Xcode đã export hoàn chỉnh từ CDN Dragon Blue:
   `https://dragonblue.online/downloads/DragonBlue_iOS_Xcode.zip`
3. Chạy `xcodebuild` xuất file binary cho kiến trúc **ARM64**.
4. Đóng gói cấu trúc `Payload/` thành file **`DragonBlue.ipa`**.
5. Đẩy file `DragonBlue.ipa` lên mục **Artifacts** của GitHub Actions (và tự động sync về VPS nếu có cấu hình Secrets).

---

## 🛠️ Hướng Dẫn Sử Dụng (Chỉ 2 Bước)

### Bước 1: Tạo Repository Trên GitHub
1. Đăng nhập [GitHub.com](https://github.com/) -> Bấm **New repository**.
2. Đặt tên (ví dụ: `dragonblue-ios-build`), chọn **Private** (hoặc Public).
3. Bấm **Create repository**.

### Bước 2: Đẩy Thư Mục Này Lên GitHub
Chạy các lệnh sau trong terminal tại thư mục `D:\1Vip\DragonBlue_iOS_Build`:
```bash
git init -b main
git add .
git commit -m "feat: setup cloud build workflow for Dragon Blue iOS IPA"
git remote add origin https://github.com/<tai-khoan-cua-ban>/dragonblue-ios-build.git
git push -u origin main
```

### Bước 3: Nhận File IPA
1. Vào tab **Actions** trên GitHub repo -> Chọn workflow **Build iOS IPA (Dragon Blue)** -> Bấm **Run workflow**.
2. Sau 5 - 7 phút, quá trình hoàn tất.
3. Tải file **`DragonBlue-iOS-IPA.zip`** trực tiếp tại mục **Artifacts** ở cuối trang chạy Actions.
4. Giải nén được file **`DragonBlue.ipa`** để cài qua **Scarlet, Esign, Sideloadly, hoặc TrollStore**.

---

## ⚡ (Tùy chọn) Tự Động Đẩy IPA Trực Tiếp Lên VPS Sau Khi Build
Nếu muốn GitHub Actions tự động upload file `DragonBlue.ipa` vào thư mục web tải game của server (`103.178.235.89`), vào:
**Settings** -> **Secrets and variables** -> **Actions** -> **New repository secret**:
- `VPS_PASSWORD`: `Cunlun123@`
(Các thông số `VPS_HOST=103.178.235.89`, `VPS_PORT=7952`, `VPS_USER=root` đã được đặt mặc định sẵn trong workflow).
