<div align="center">

# 🤖 Workshop "Cầm tay chỉ AI"

### Landing page đăng ký workshop hướng dẫn dân văn phòng dùng AI từ con số 0

[![Live](https://img.shields.io/badge/Live-camtaychiai.vercel.app-6d28d9?style=for-the-badge)](https://camtaychiai.vercel.app)
[![Deploy](https://img.shields.io/badge/Deploy-Vercel-black?style=for-the-badge&logo=vercel)](https://vercel.com)
[![Made with](https://img.shields.io/badge/HTML%20%C2%B7%20CSS%20%C2%B7%20JS-no%20framework-f59e0b?style=for-the-badge)](#)

**[🔗 Xem trang trực tiếp →](https://camtaychiai.vercel.app)**

</div>

---

## ✨ Giới thiệu

Landing page một trang (single-file) cho workshop **"Cầm tay chỉ AI"** — khóa học **3 buổi (mỗi buổi 2 tiếng)** online qua Zoom, hướng dẫn dân văn phòng ứng dụng AI vào công việc. Trang thu thập đăng ký, đổ dữ liệu về Google Sheet và hiển thị mã QR cọc giữ chỗ tự động.

> Workshop miễn phí · cọc giữ chỗ 200.000đ · **hoàn 100%** khi hoàn thành ≥ 80% nhiệm vụ · giới hạn 99 suất.

## 🎯 Tính năng

- **Thiết kế hiện đại** — tông tím hoàng gia + vàng gold, font *Be Vietnam Pro* (đủ dấu tiếng Việt), responsive cho mobile.
- **Đồng hồ đếm ngược** tới giờ khai giảng (tự dừng khi hết hạn).
- **Form đăng ký** → gửi về **Google Sheet** (qua Google Form, không cần backend riêng).
- **Mã QR cọc động** — tự sinh QR VietQR đã gắn sẵn nội dung chuyển khoản kèm số điện thoại người đăng ký.
- **Thanh suất khan hiếm** đồng bộ từ một nguồn cấu hình.
- **Chống bot** bằng honeypot, validate số điện thoại 10–11 số, chống double-submit.

## 🏗️ Kiến trúc

```
Khách điền form  →  Google Form (formResponse)  →  Google Sheet
   (frontend)              (backend)                 (database)
   index.html        máy chủ Google nhận           lưu đăng ký
```

| Tầng | Thành phần | Nhiệm vụ |
|------|-----------|----------|
| **Frontend** | `index.html` | Giao diện khách nhìn & điền; sinh QR; validate |
| **Backend** | Google Form *(hoặc Apps Script `Code.gs`)* | Nhận & xử lý dữ liệu gửi lên |
| **Database** | Google Sheet | Lưu từng dòng đăng ký |

> Frontend **không** ghi thẳng vào Sheet vì lý do bảo mật (không thể để chìa khóa ghi trong mã công khai). Google Form đóng vai trò "nhân viên trung gian" giữ quyền ghi.

## ⚙️ Tùy chỉnh

Mọi cấu hình nằm trong khối `CONFIG` ở cuối `index.html`:

```js
const CONFIG = {
  GFORM: { action: "...formResponse", fields: { ... } }, // link Google Form + entry id
  BANK:  { bankCode: "VCB", account: "...", holder: "...", amount: 200000 }, // tài khoản nhận cọc
  SEATS: { total: 99, left: 27 }   // số suất hiển thị
};
// Đổi ngày sự kiện:
const EVENT_TIME = new Date(2026, 6, 18, 20, 0, 0).getTime();
```

- **Đổi tài khoản nhận cọc:** sửa `BANK.bankCode`, `BANK.account`, `BANK.holder`.
- **Đổi số suất:** sửa `SEATS.left`.
- **Đổi ngày khai giảng:** sửa `EVENT_TIME` và phần ngày trong HTML.
- **Đổi link Zalo/Fanpage:** sửa thẻ `<a>` ở footer.

## 🚀 Deploy

1. Đẩy `index.html` lên repo GitHub.
2. Vào [Vercel](https://vercel.com) → **Add New → Project** → import repo → **Deploy**.
3. Mỗi lần sửa `index.html` rồi commit, Vercel tự deploy lại.

## 📁 Cấu trúc

```
.
├── index.html      # Toàn bộ landing page (HTML + CSS + JS trong 1 file)
└── README.md       # Tài liệu này
```

## 🔒 Ghi chú bảo mật

- Google Sheet luôn để chế độ **Restricted** (chỉ người được mời), không bao giờ "Anyone with the link".
- Form công khai có honeypot chống bot; suất thật được tính theo **tiền cọc đã về**, không chỉ theo số dòng trong Sheet.
- Không commit file nội bộ (`Code.gs`, hướng dẫn riêng) lên repo public.

## 👤 Mentor

**Hưng Kescy** — CEO & Founder KesFlow · Giám đốc Chuyển đổi số JCI · [hungkescy.com](https://hungkescy.com)

---

<div align="center">
<sub>© 2026 Workshop "Cầm tay chỉ AI" · Built with ❤️</sub>
</div>
