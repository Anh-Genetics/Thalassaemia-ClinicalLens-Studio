# 🏥 Thalassaemia-ClinicalLens Studio (Version 5.0 Enterprise)

> **Hệ sinh thái Y tế số Lâm sàng, Phân tích Cây Phả hệ Di truyền Chuẩn Quốc tế NSGC-2.5, Dự báo Đột biến Gen Giải thích được (Hybrid XAI-CDSS) & Tư vấn Di truyền Thalassemia Toàn diện**

* **Đơn vị phát triển & triển khai**: **BỆNH VIỆN NHI HÀ NỘI (HANOI CHILDREN'S HOSPITAL)** — **Đơn nguyên Di truyền và Sinh học phân tử**

* **Tác giả & Kiến trúc sư Hệ thống**: **ThS. Trần Tuấn Anh**

* **Hệ sinh thái kế thừa**:

  1. **`NSGC_Pedigree_GAS_Project`** *(ThS. Trần Tuấn Anh)*: Động cơ dựng hình và suy luận cây phả hệ chuẩn quốc tế [NSGC-2.5 (Bennett et al. 2008 / 2025 Update)](https://pmc.ncbi.nlm.nih.gov/articles/PMC11926493/), tô màu 4 góc phần tư đa alen ($\alpha^0, \alpha^+/\text{HbCS}, \beta^0/\beta^+, \text{HbE}$), xuất đồ họa Vector SVG 300 DPI và tính toán ma trận lai Mendel 16 ô ($\alpha \times \beta$).

  2. **`TTA_PediaInfect-clinical`** *(ThS. Trần Tuấn Anh)*: Kiến trúc phân quyền đa cấp độ **4-Tier RBAC** (`SCOPE_ALL`, `SCOPE_CLINICAL`, `SCOPE_LAB`, `SCOPE_SCREENING`), mã hóa dữ liệu định danh **AES-256 Auth-Stream**, tìm kiếm qua **Blind Index HMAC-SHA256**, và nhật ký kiểm toán chuỗi băm bất biến (**Chained-HMAC Audit Trail**) tuân thủ [Nghị định 85/2016/NĐ-CP](https://thuvienphapluat.vn/van-ban/Cong-nghe-thong-tin/Nghi-dinh-85-2016-ND-CP-bao-dam-an-toan-he-thong-thong-tin-theo-cap-do-317475.aspx) và Nghị định 13/2023/NĐ-CP.

## 1. ĐIỂM MỚI ĐỘT PHÁ CỦA PHIÊN BẢN v5.0 (BỆNH VIỆN NHI HÀ NỘI)

1. **Thuật toán Dự báo Đa tầng Nhi khoa & Sản khoa (`Pediatric & Adult Age-Stratified Hybrid Engine v5.0`)**:

   * Phân tầng tự động ngưỡng thiếu máu Hemoglobin theo sinh lý lứa tuổi Nhi khoa và Sản khoa: Nhũ nhi & trẻ nhỏ $6\text{ tháng} \text{--} 5\text{ tuổi}$ ($\text{Hb} < 110\text{ g/L}$), Trẻ em $6\text{--}15\text{ tuổi}$ ($\text{Hb} < 115\text{ g/L}$), Thai phụ ($\text{Hb} < 110\text{ g/L}$), Nữ trưởng thành ($\text{Hb} < 115\text{ g/L}$) và Nam trưởng thành ($\text{Hb} < 120\text{ g/L}$) theo [Quyết định 1807/QĐ-BYT](https://thuvienphapluat.vn/van-ban/The-thao-Y-te/Quyet-dinh-1807-QD-BYT-2020-chuyen-mon-ky-thuat-sang-loc-chan-doan-dieu-tri-truoc-sinh-so-sinh-440595.aspx) và [Quyết định 1832/QĐ-BYT](https://thuvienphapluat.vn/van-ban/The-thao-Y-te/Quyet-dinh-1832-QD-BYT-2022-tai-lieu-huong-dan-chan-doan-dieu-tri-benh-ly-huyet-hoc-520596.aspx).

   * **Vá triệt để lỗi "Hố đen số thực"** $\text{MCH} \in (18.0, 19.0)\text{ pg}$ **và khoảng trống** $\text{HbA}_2 \in [3.3\%, 4.4\%]$ trong các công thức cũ; kết hợp điểm bậc thang **`TS2_v2`** với điểm nội suy liên tục **`TS2_continuous` (Spline Score)** và **Điểm Độ tin cậy (`Confidence Score %`)** theo chuẩn [TRIPOD+AI](https://www.bmj.com/content/385/bmj-2023-078378).

   * **Tích hợp 09 Chỉ số Phân biệt Hồng cầu Kinh điển (Consensus Voting** $0/9 \rightarrow 9/9$**)**: `Mentzer`, `Green & King`, `Srivastava`, `Shine & Lal`, `RDWI`, `Ehsani`, `Sirdah`, `England & Fraser` và `Ricerca (RDW/RBC)`.

2. **Giao diện Y tế Số Chuyên nghiệp Mang Nhận diện Thương hiệu Bệnh viện Nhi Hà Nội**:

   * Tích hợp chính thức Logo **Bệnh viện Nhi Hà Nội (Hanoi Children's Hospital)**, **Đơn nguyên Di truyền và Sinh học phân tử**, và chữ ký chuyên môn **ThS. Trần Tuấn Anh** trên cả thanh Header điều hướng lẫn Biểu mẫu Phiếu Tư vấn Di truyền in PDF.

   * Thiết kế nổi bật các dải tiêu đề phân mục lớn (**`I. THÔNG TIN LÂM SÀNG & XÉT NGHIỆM SÀNG LỌC`**, **`II. BẢNG ĐỐI CHIẾU CHỈ SỐ TRỌNG SỐ TS2_V2 & 09 CHỈ SỐ PHÂN BIỆT KINH ĐIỂN`**, **`III. KIỂU GEN ĐỘT BIẾN DỰ BÁO (CHUẨN HGVS) & CHỈ ĐỊNH XÉT NGHIỆM PHÂN TỬ 3 TẦNG`**) và các tiểu mục (`1.`, `2.`, `3.`) bằng dải màu Y tế Nhi Hà Nội (`#00529B` $\rightarrow$ `#00ACC1`).

3. **Bộ Kiểm thử Tự động 18 Kịch bản Lâm sàng & Bảo mật (`18/18 Automated Clinical QA Suite`)**:

   * Đạt chuẩn `100% PASS` ngay trên giao diện (Tab 6), bao gồm kiểm thử phân tầng Nhi khoa (`QA-07`), đồng thuận 9 chỉ số hồng cầu (`QA-14`), nội suy liên tục (`QA-15`), ma trận lai 16 ô (`QA-16`), mã hóa AES-256/RBAC (`QA-17`) và kiểm định nhận diện thương hiệu (`QA-18`).

## 2. CẤU TRÚC KHO MÃ NGUỒN GITHUB CHUẨN (`Thalassaemia-ClinicalLens-Studio`)

Cấu trúc thư mục được chuẩn hóa đồng bộ với hai dự án `NSGC_Pedigree_GAS_Project` và `TTA_PediaInfect-clinical` để hỗ trợ đẩy mã nguồn tự động từ GitHub lên Google Apps Script qua công cụ `@google/clasp` và GitHub Actions:

```
Thalassaemia-ClinicalLens-Studio/
├── .github/
│   └── workflows/
│       └── deploy-gas.yml                          # GitHub Actions CI/CD tự động push lên GAS khi git push main
├── src/
│   ├── appsscript.json                             # Cấu hình Google Apps Script V8 Runtime & OAuth Scopes
│   ├── Code.gs                                     # Đổi tên từ Thalassaemia_ClinicalLens_GAS_Backend_Full.gs
│   └── Index.html                                  # Giao diện SPA v5.0 (nhúng sẵn Logo BV Nhi Hà Nội Base64)
├── etl/
│   └── ETL_Migration_13334_Cases_To_12Sheets.py    # Kịch bản Python làm sạch & mã hóa AES-256 cho 13,334 ca
├── docs/
│   └── Architecture_And_Mega_Prompt_v5.md          # Tài liệu kiến trúc & Siêu Siêu Prompt
├── .clasp.json                                     # Tệp cấu hình liên kết Script ID của Google Apps Script
├── .claspignore                                    # Loại trừ các thư mục không đẩy lên GAS (etl/, docs/)
└── README.md                                       # Tài liệu hướng dẫn triển khai GitHub & Clasp

```

## 3. HƯỚNG DẪN TRIỂN KHAI TỪNG BƯỚC LÊN GITHUB & GOOGLE APPS SCRIPT (CLASP WORKFLOW)

### Bước 1: Tạo tệp cấu hình `src/appsscript.json` và `.claspignore`

Tại thư mục `src/`, tạo tệp `appsscript.json` với nội dung sau:

```
{
  "timeZone": "Asia/Ho_Chi_Minh",
  "dependencies": {},
  "webapp": {
    "executeAs": "USER_DEPLOYING",
    "access": "ANYONE_WITHIN_DOMAIN"
  },
  "exceptionLogging": "STACKDRIVER",
  "runtimeVersion": "V8",
  "oauthScopes": [
    "https://www.googleapis.com/auth/spreadsheets",
    "https://www.googleapis.com/auth/drive",
    "https://www.googleapis.com/auth/script. storage",
    "https://www.googleapis.com/auth/userinfo.email"
  ]
}

```

Tại thư mục gốc, tạo tệp `.claspignore`:

```
**/**
!src/Code.gs
!src/Index.html
!src/appsscript.json

```

### Bước 2: Khởi tạo Kho mã nguồn GitHub & Đẩy Code lên GitHub

Mở Terminal / PowerShell tại thư mục dự án và chạy các lệnh:

```
git init
git branch -M main
git add .
git commit -m "feat(v5.0): Release Thalassaemia-ClinicalLens Studio v5.0 - BV Nhi Ha Noi (ThS. Tran Tuan Anh)"
git remote add origin https://github.com/<Ten_Tai_Khoan_GitHub>/Thalassaemia-ClinicalLens-Studio.git
git push -u origin main

```

### Bước 3: Kết nối và Đẩy Trực tiếp lên Google Apps Script bằng `clasp`

Giống như quy trình của `NSGC_Pedigree_GAS_Project` và `TTA_PediaInfect-clinical`:

```
# 1. Cài đặt Google Clasp toàn cục (nếu chưa cài)
npm install -g @google/clasp

# 2. Đăng nhập tài khoản Google của Đơn nguyên Di truyền & SHPT
clasp login

# 3. Tạo mới Google Spreadsheet kèm dự án Apps Script gắn liền (Container-bound Script)
clasp create --type sheets --title "HCH_Thalassaemia_ClinicalLens_DB_v5" --rootDir ./src

# 4. Đẩy toàn bộ mã nguồn từ thư mục ./src lên Google Apps Script
clasp push -f

# 5. Mở Apps Script Editor để chạy hàm khởi tạo 12 Sheet lần đầu
clasp open

```

Trong cửa sổ Apps Script Editor vừa mở:

1. Chọn hàm **`bootstrapDatabaseSheets`** trên thanh công cụ và nhấn **Run (Chạy)** $\rightarrow$ Cấp quyền truy cập Google Sheets để hệ thống tự động tạo 12 bảng chuẩn hóa (`SYS_USERS`, `SYS_AUDIT_LOGS`, `PATIENTS`, `CLINICAL_ENCOUNTERS`, `LAB_CBC_RESULTS`, `LAB_BIOCHEM_IRON`, `LAB_HB_ELECTROPHORESIS`, `MOLECULAR_GENOTYPES`, `CDSS_PREDICTIONS`, `FAMILIES`, `PEDIGREE_NODES`, `COUPLE_ASSESSMENTS`).

2. Nhấn **Deploy (Triển khai)** $\rightarrow$ **New deployment (Tạo triển khai mới)** $\rightarrow$ **Web app** (hoặc chạy lệnh `clasp deploy --description "Production v5.0 - BV Nhi Ha Noi"` trong Terminal) để nhận đường dẫn WebApp chính thức.

### Bước 4: Thiết lập Tự động Triển khai (GitHub Actions CI/CD `.github/workflows/deploy-gas.yml`)

Để mỗi lần cập nhật thuật toán trên GitHub thì Google Apps Script tự động được cập nhật:

```
name: Deploy Thalassaemia-ClinicalLens Studio to Google Apps Script

on:
  push:
    branches: [ main ]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '20'

      - name: Install Google Clasp & Push to GAS
        env:
          CLASPRC_JSON: ${{ secrets.CLASPRC_JSON }}
          SCRIPT_ID: ${{ secrets.GAS_SCRIPT_ID }}
        run: |
          npm install -g @google/clasp
          echo "$CLASPRC_JSON" > ~/.clasprc.json
          echo "{\"scriptId\":\"$SCRIPT_ID\",\"rootDir\":\"./src\"}" > .clasp.json
          clasp push -f

```

*(Lưu ý: Sao chép nội dung tệp `~/.clasprc.json` ở máy cá nhân sau khi `clasp login` vào mục `Settings -> Secrets and variables -> Actions -> CLASPRC_JSON` trên GitHub).*