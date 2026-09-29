# Thành viên và phân vai — Day11 SVM 360 Fisheye

## 1. Thông tin nhóm

- **Khóa/lớp:** 4
- **Tên nhóm:** Offer50M
- **Repo Public:** https://github.com/vothanhducdev/K4-DAY11-Offer50M
- **Máy giữ hồ sơ chính / người quản lý:** Võ Thành Đức
- **Slice chung lấy từ mode.json:** B4-edge
- **Tên định danh vai A dùng cho --self:** minhtuan
- **Kênh trao đổi nội bộ:** Zalo
- **Đại diện nộp (vai C):** Võ Thành Đức - 2A202602167
- **Commit chốt bài:** 93b4412

## 2. Ba vai chính

| Vai                           | Họ và tên          | MSSV        | Tên định danh trong mode | Trách nhiệm                                         | Bằng chứng đóng góp                                                                                                                                                                            |
| :---------------------------- | :----------------- | :---------- | :----------------------- | :-------------------------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **A · Gán nhãn**              | Hoàng Võ Minh Tuấn | 2A202602166 | minhtuan                 | Parking/C0/slice, self-QC, lock, rework             | Thực hiện gán nhãn slice B4-edge trên CVAT, xuất `annotations.xml`, khóa bản nhãn `r1_craft/lock.txt`, thực hiện sửa nhãn `rework/annotations-v2.xml`.                                         |
| **B · QA độc lập**            | Nguyễn Đức Tuấn    | 2A202602225 | ductuan                  | Review trước reference, finding QA, kiểm lại ca sửa | Thực hiện QA độc lập không xem reference, ghi nhận `qa_review.md`, tạo danh sách lỗi ban đầu trong `findings.csv` theo các `rule_id`.                                                          |
| **C · Chẩn đoán & điều phối** | Võ Thành Đức       | 2A202602167 | duc                      | Báo cáo, phân xử, kế hoạch, tích hợp, check và nộp  | Quản lý máy chính, chạy CLI phân tích lỗi `r3_diag`, lập `20_guideline_patch.md`, `30_escalation_ticket.md`, `40_decision_log.csv`, chạy nghiệm thu `lab11.py check` (exit 0) và push bài nộp. |

> _Bảng này xác định vai của nhóm. Vòng QA tự sinh trong team.json thuộc quy trình nhiều hồ sơ của CLI; nhóm dùng một slice chung và quy trình A → B → C đã nêu trong hướng dẫn._

## 3. Bàn giao theo pha

| Mốc                             | Người giao → nhận | File / commit / mã khóa                                                   | Người nhận đã kiểm gì?                                     | Trạng thái / vướng mắc                         |
| :------------------------------ | :---------------- | :------------------------------------------------------------------------ | :--------------------------------------------------------- | :--------------------------------------------- |
| **P0 · Chốt môi trường và vai** | C → A, B          | `00_setup/mode.json`, slice `B4-edge`                                     | Cấu hình camera, slice ID, quyền truy cập repo             | Hoàn thành, thống nhất slice B4-edge           |
| **P2 · Khóa bản đầu**           | A → B, C          | `r1_craft/annotations.xml`, `lock.txt` (SHA: `ee4f771f...`)               | Tính toàn vẹn XML, đủ số frame, mã băm sha256 đã khóa      | Khóa thành công lúc 15:37:51                   |
| **P3 · Chốt QA mù**             | B → C, A          | `r2_qa/qa_review.md`, `r2_qa/qa_overlay.html`                             | Quy tắc dán nhãn theo guideline, không dùng reference      | Ghi nhận các lỗi lệch box và sót nhãn          |
| **P4 · Quyết định sửa**         | C → A, B          | `findings.csv`, `40_decision_log.csv`, `20_guideline_patch.md`            | Bảng đối chiếu IOU, ma trận nhầm lẫn model và taxonomy lỗi | Thống nhất 4 quyết định xử lý và 1 ca escalate |
| **P5 · Kiểm bản sửa**           | A → B → C         | `rework/annotations-v2.xml`, `lock2.txt` (SHA: `dd10ddff...`), `delta.md` | So sánh delta v1 vs v2, kiểm tra khớp quy tắc mới          | Khóa thành công v2 lúc 16:07:08                |
| **P6 · Chốt nộp**               | A, B → C          | `manifest.json`, commit `93b4412`                                         | Chạy lệnh `py lab11.py check`, đối chiếu gates             | Hoàn tất (exit 0: Hồ sơ hình thức đầy đủ)      |

## 4. Bất đồng và phối hợp

- **Một ca đã phân xử:**
  - _Vấn đề:_ Bất đồng về việc gán nhãn phương tiện bị che khuất ở hậu cảnh xa và bóng râm trên vùng trung tâm (center zone) tại slice B2/B4.
  - _Ý kiến A/B:_ Vai A bỏ sót do nhầm với nền đường; Vai B phát hiện thiếu box nhưng chưa rõ ngưỡng kích thước tối thiểu.
  - _Quyết định:_ Vai C ban hành `20_guideline_patch.md` quy định rõ ngưỡng che khuất $\ge 20\%$ và kích thước tối thiểu $15 \times 15$ pixel; cập nhật quyết định vào `40_decision_log.csv` (DEC-01, DEC-02).
- **Ca còn mở:** Không còn ca mở. Toàn bộ 4 quyết định đã được phân loại rõ ràng (3 resolved, 1 escalated lên Lead theo đúng ticket `30_escalation_ticket.md`).
- **Đóng góp của A/B/C vào kế hoạch và exit ticket:**
  - Vai A đóng góp kinh nghiệm thực tế về thao tác gán nhãn trong `50_exit_ticket.md`.
  - Vai B xây dựng ma trận lấy mẫu kiểm định trong `45_sampling_plan.csv`.
  - Vai C hoàn thiện kế hoạch xây dựng bộ dữ liệu vàng trong `46_gold_set_plan.md` và quy trình review `45_review_plan.md`.
- **Thay đổi phân công nếu có:** Không thay đổi. Cả ba thành viên bám sát đúng phân vai đã đăng ký từ ban đầu.

## 5. Xác nhận trước khi nộp

- [x] **A xác nhận nhãn và export đúng phiên bản:** Hoàng Võ Minh Tuấn — Khóa bản export đúng định dạng CVAT 1.1, sinh file `lock.txt` và `lock2.txt` hợp lệ.
- [x] **B xác nhận đã QA độc lập trước reference và kiểm lại ca sửa:** Nguyễn Đức Tuấn — Hoàn thành review mù độc lập và kiểm tra đối chiếu delta giữa bản đầu và bản sửa.
- [x] **C xác nhận báo cáo đúng bản khóa, các file đầy đủ và check exit 0:** Võ Thành Đức — Chạy `py lab11.py check` xác nhận `✓ Hồ sơ hình thức đầy đủ`.
- [x] **`manifest.json` tại commit chốt có `failed_gates` rỗng.** (Đã xác minh `"failed_gates": []`).
- [x] **Repo nhóm Public, ảnh và các bằng chứng mở được.** (Đã kiểm tra repo `vothanhducdev/K4-DAY11-Offer50M` public).
- [x] **C đã push và gửi link repo nhóm + commit qua kênh lớp công bố.** (Đã push commit `93b4412` lên `main`).
