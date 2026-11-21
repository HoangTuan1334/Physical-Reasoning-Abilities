# QuantiPhy / METER-4D

Kế hoạch hiện hành: [New_plan.md](New_plan.md). Đây là workspace nghiên cứu đang được chuẩn bị; pipeline METER-4D chưa được triển khai đầy đủ.

**Bản hợp nhất dùng chung dữ liệu và quyết định:** [thiết kế và kiểm chứng](docs/UNIFIED_THREE_LAYERS_VI.md), code tại `implementations/unified_three_layer/`. Xem bằng `python scripts/run_unified.py --describe`, chạy thử CPU với baseline bằng `python scripts/demo_unified.py`. Các công thức chuyên biệt được giữ bên trong để bảo toàn hành vi.

Bản refactor code ZIP thành **ba lớp thực thi** đã có tại [implementations/three_layer](implementations/three_layer/THREE_LAYERS.md); xem [thiết kế, backup và kiểm thử](docs/THREE_LAYER_REFACTOR_VI.md). Bản này giữ phương pháp cũ, độc lập với khung METER-4D. Xem nhanh bằng `python scripts/run_three_layers.py --describe`.

Đọc [báo cáo kiểm tra](reports/AUDIT_VI.md), [đánh giá cấu hình máy](reports/HARDWARE_VI.md) và [lộ trình triển khai](docs/IMPLEMENTATION_PLAN.md).

```text
New_plan.md                    Kế hoạch METER-4D gốc, giữ nguyên
archives/                      ZIP gốc
legacy/Submit/                 Toàn bộ 944 file giải nén, giữ nguyên nội dung
docs/plans/archive/            Ba bản thiết kế SPARK trước đây
docs/incoming/                 Thư mục Documet cũ (đang trống)
data/raw/quantiphy/            Arrow test, Arrow validation, assets validation gốc
data/raw/{iris,...}/           Vị trí dành cho dataset mới, hiện trống
data/processed/quantiphy/      CSV sạch và danh mục video đã kiểm tra
data/processed/legacy_verification/  Cache đã giải nén để kiểm chứng CPU
configs/                      Danh mục dataset và cấu hình dự kiến
src/meter4d/                   Khung module cho phương pháp mới
notebooks/                    Hướng dẫn phân chia notebook theo giai đoạn
models/                       Vị trí trọng số của pipeline mới, hiện trống
scripts/                      Công cụ kiểm tra dữ liệu, môi trường và cache
outputs/                      Kết quả chạy, gồm CSV E126 dựng lại từ cache
reports/                      Báo cáo, manifest SHA256 và danh sách dữ liệu thiếu
tmp/                          Vị trí tạm trong workspace
```

Các lệnh đã chạy được trong Python hiện tại, từ thư mục gốc:

```powershell
python scripts/check_environment.py
python scripts/audit_data.py
python scripts/verify_cached.py
python -m pytest -q legacy/Submit/tests -p no:cacheprovider
```

Lệnh test cuối hiện có **5 passed, 1 failed, 136 skipped**: lỗi so sánh float chính xác trong code cũ; xem báo cáo. Việc dựng lại E126 từ cache thành công không chứng minh inference từ video chạy đầy đủ.

Python mặc định Anaconda dùng torch CPU; đã tìm thấy môi trường Conda `mcstem-search` dùng torch GPU và kiểm chứng tính toán CUDA thành công. Xem báo cáo cấu hình để biết đường dẫn. Chưa cài lại package, tải model lớn hay dataset mới. `configs/local_cpu.json` chỉ là đề xuất vận hành, chưa có runner METER-4D đọc cấu hình đó.

CSV test gốc không có ID; file `data/processed/quantiphy/questions.csv` lấy ID từ metadata bản submission sau khi đối chiếu toàn bộ trường câu hỏi và thứ tự. Không sử dụng giá trị dự đoán làm nhãn. CSV validation gốc được giữ nguyên, bản sạch bỏ các cột spreadsheet thừa.

Lịch sử đổi đường dẫn và SHA256: `reports/reorganization_manifest.csv`. File ZIP giữ nguyên trong `archives/`. Các đường dẫn trong tài liệu cũ vẫn phản ánh môi trường của tác giả và cần điều chỉnh khi chạy.
"# Physical-Reasoning-Abilities" 
