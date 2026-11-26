# OCEANBLUEselect — Thiết bị OceanBlue (PWA)

Ứng dụng web (PWA) tra cứu và chọn thiết bị OceanBlue (dàn ngưng bay hơi) theo điều kiện thiết kế, có hiệu chỉnh theo nhiệt độ ngưng tụ / bầu ướt nếu catalogue có bảng hiệu chỉnh. Chạy **offline** sau lần mở đầu tiên, có giỏ chọn
thiết bị và xuất phiếu yêu cầu báo giá (CSV / In-PDF / Word).

- Địa chỉ: https://decoolboy-source.github.io/OCEANBLUEselect/
- Hãng: **OceanBlue (Yantai OceanBlue Refrigeration)** — mỗi hãng là một app riêng (xem danh sách app trên
  https://decoolboy-source.github.io/cong-cu/).
- Tách ngày 2026-11-26 từ ECselect (app nhiều hãng, đã ngừng): giữ nguyên giao diện và
  cách tra, chỉ giữ dữ liệu của hãng này, trang chủ đi thẳng vào các dòng sản phẩm.

## Dữ liệu

`data.js` (hằng `DATABASE.sources`): 3 dòng sản phẩm, 102 model:

- Dàn ngưng bằng hơi kiểu dòng chéo ECB (OceanBlue) — 34 model
- Dàn ngưng bằng hơi kiểu ngược dòng ECE (OceanBlue) — 40 model
- Dàn ngưng bằng hơi kiểu tấm ECBP (OceanBlue) — 28 model

Số liệu trích từ catalogue của hãng, chỉ để **tham khảo sơ bộ** — đối chiếu tài liệu gốc
hoặc nhà cung cấp trước khi chọn thiết bị cho dự án thực tế.

## Cấu trúc thư mục

```
index.html      Giao diện
app.js          Logic tra cứu, giỏ báo giá, xuất phiếu
data.js         Dữ liệu thiết bị của hãng — sửa/thêm model ở đây
data-io.js      Xuất/Nhập dữ liệu JSON (chuẩn chung các app)
nasa-ui.css     Giao diện CHUNG các app chọn thiết bị (giống hệt nhau giữa các app)
icons.js        Bộ icon CHUNG (trích từ Lucide, chạy offline)
style.css       Phần riêng của app
manifest.json   Khai báo PWA
sw.js           Service worker — cache offline
icons/          Icon app
```

## Chạy thử trên máy

App là file tĩnh, không cần cài gói:

```
python -m http.server 8080
```

rồi mở http://localhost:8080/ (không mở bằng `file://` vì service worker không chạy).

## Triển khai

Repo GitHub `decoolboy-source/OCEANBLUEselect`, GitHub Pages từ nhánh `main`, thư mục gốc.
App chạy tại `/OCEANBLUEselect/` chung origin với site chính và các app khác, nên:

- Service worker đăng ký tương đối `./sw.js`, scope `./`.
- Cache tên `OCEANBLUEselect-v<số>`; khi kích hoạt chỉ xoá cache có tiền tố này.
- Khoá localStorage có tiền tố `OCEANBLUEselect:`.
- File xuất dữ liệu `OCEANBLUEselect_YYYYMMDD.json` (`app: "OCEANBLUEselect"`, `schemaVersion: 1`).

Cập nhật: sửa code/dữ liệu, tăng `CACHE_NAME` trong `sw.js` và `BUILD_VERSION` trong
`app.js`, push lên `main`. Dòng "build ..." cuối trang cho biết bản đang chạy.

## Lịch sử phiên bản

### 2026-11-26.1 — bản đầu `OCEANBLUEselect-v1`

Tách từ ECselect: chỉ dữ liệu OceanBlue (Yantai OceanBlue Refrigeration); khoá lưu trữ, cache,
file xuất dữ liệu dùng tiền tố `OCEANBLUEselect`.
