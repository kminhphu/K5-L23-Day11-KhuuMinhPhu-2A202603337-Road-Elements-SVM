# Báo cáo cá nhân — Ngày 11
Họ tên: Khưu Minh Phú               Mã học viên: 2A202603337  
Phiên bản CVAT (Help → About): CVAT v2.82.0  
Guideline: Road v1.0    Lần nộp (`revision` trong manifest): 1  
Thời điểm export (ngày giờ trên CVAT): 2026-11-20 18:17 UTC    Số lần nộp lại sau Rework: 0  

## 1. Kiểm project
| Mục | Đúng như guideline Road v1.0? | Ghi chú |
| --- | --- | --- |
| 6 label, đúng kiểu | Đúng | `lane` (polyline), `road_curb` (polyline), `crosswalk` (polygon), `drivable` (polygon), `traffic_light` (rectangle), `traffic_sign` (rectangle) |
| Thuộc tính và giá trị | Đúng | Khớp 100% với `configs/road_v1_labels.json` (`position`, `style`, `color`, `kind`, `area_type`, `type`, `group`, `facing`, `edge_zone`) |
| 4 tag ảnh | Đúng | `camera`, `timeofday`, `weather`, `source` đều là label kiểu Tag có thuộc tính select `value` |
Cách kết thúc polyline trên bản CVAT này: Nhấn phím **`N`** sau khi chấm xong điểm cuối cùng ở xa (hoặc bấm lại vào công cụ Draw new polyline trên thanh bên trái).  
Cách đặt tag ảnh trên bản CVAT này: Chọn biểu tượng **Tag** ở thanh công cụ bên trái → chọn tên tag (`camera` đặt đầu tiên, sau đó `timeofday`, `weather`, `source`) → bấm ** Tag ** → mở mục **Details** của từng tag ở bảng **Objects** bên phải để chọn đúng giá trị thuộc tính `value`.  

## 2. Số lượng đã gán
| Task | Ảnh | lane | road_curb | crosswalk | drivable | traffic_light | traffic_sign |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| front | 12 | 33 | 13 | 8 | 23 | 20 | 47 |
| front-extra (đã làm 0 / 4) | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| fisheye | 8 | 9 | 4 | 6 | 3 | 5 | 1 |
| fisheye-extra (đã làm 0 / 4) | 0 | 0 | 0 | 0 | 0 | 0 | 0 |

## 3. Bảng ca khó
| Ảnh | Nhãn | Phân vân giữa | Đã chọn | Lý do |
| --- | --- | --- | --- | --- |
| A05, A06, A09 | `lane` (`L1`, `R1`) | Vẽ thêm `L1`/`R1` dọc mép xe đỗ/vỉa hè để tránh cảnh báo `lint QC1-02` hay chỉ vẽ `road_curb` | Không vẽ `L1`/`R1` ở bên không có vạch sơn, chỉ vẽ `road_curb` | Theo Guideline mục 3 và Hướng dẫn CVAT mục 6: không vẽ vạch mà ảnh thật sự không có sơn; các ca này được miễn `QC1-02` sau khi xác nhận. |
| A09, A10 | `traffic_sign` (biển quay mặt lưng và biển chữ nhật đỏ-trắng dọc vỉa hè) | `group = other` vs `prohibitory` / `supplementary` | Biển cấm đỗ đỏ-trắng chọn `prohibitory`; tấm nhỏ gắn kèm dưới biển chính chọn `supplementary`; biển quay lưng không rõ hình dạng chọn `other` | Phân nhóm theo chức năng (biển No Parking/No Standing là biển cấm `prohibitory`, biển phụ dưới biển chính tách box riêng `supplementary`). |
| B04 | `tag:weather` và `traffic_light` ở gần rìa ảnh | `weather = clear` vs `overcast`; `edge_zone = true` vs `false` cho đèn ở `(1066, 239)` | `weather = overcast`; kiểm tra lại bán kính 80% (`r = 512 px`) cho `edge_zone` | Bầu trời B04 nhiều mây trắng âm u nhưng mặt đường khô nên chọn `overcast`. Đèn tại `(1066, 239)` có tâm cách tâm ảnh `(640, 483)` khoảng `491 px < 512 px` (nằm sát ranh giới trong 80% bán kính). |

## 4. Phiếu QC 1 nhận được
Bạn kiểm lô của tôi: vugiakhang    Quyết định nhận được: Release (đã tự rà soát và khắc phục các cảnh báo `lint` ngay trước khi chốt bài)  
| Mã lỗi | Số lỗi | Đồng ý? | Đã sửa? |
| --- | ---: | --- | --- |
| QC1-02 (cảnh báo lint thiếu L1/R1 ở A05, A06, A09 nơi không có vạch sơn; đã bổ sung R1 ở A07) | 1 | Đồng ý với A07 (thiếu R1 thật); miễn A05, A06, A09 vì thực tế chỉ có lề/xe đỗ | Đã sửa (đã vẽ bổ sung vạch `R1` trắng liền cho A07) |
| QC1-11 (cảnh báo số điểm polyline fisheye ở B03 và `edge_zone` ở B04) | 2 | Đồng ý | Đã kiểm tra và hiệu chỉnh trên CVAT |

## 5. Kiểm file export
| File | Mở lại được? | Số shape ảnh 1 (job / file) | Số shape ảnh 2 (job / file) | Tag camera có trong XML? |
| --- | --- | --- | --- | --- |
| `khuuminhphu-front.zip` | Có (`contains_images: false`) | 11 / 11 (`A01`) | 7 / 7 (`A02`) | Có (`<tag label="camera"><attribute name="value">front</attribute></tag>`) |
| `khuuminhphu-fisheye.zip` | Có (`contains_images: false`) | 3 / 3 (`B01`) | 5 / 5 (`B02`) | Có (`<tag label="camera"><attribute name="value">fisheye_front</attribute></tag>`) |

## 6. Ảnh chụp màn hình
1. Tab Labels của project:
   ![alt text](<Ảnh chụp màn hình 2026-11-20 164124.png>)
2. Một ảnh camera trước đã gán đủ (làn, vùng lái, đèn/biển):
   ![alt text](<Ảnh chụp màn hình 2026-11-21 024702.png>)
3. Một ảnh fisheye đã gán, phóng to đoạn polyline cong:
   ![alt text](<Ảnh chụp màn hình 2026-11-21 024825.png>)
4. Một đoạn XML có `<polyline label="lane">`:

```xml
<image id="0" name="A01_bc5fadac-fa6dd225.jpg" width="1280" height="720">
  <polyline label="lane" source="manual" occluded="0" points="654.30,678.30;582.57,627.09;531.98,594.12;509.37,578.16;487.19,562.60;476.24,554.39;466.33,546.28;458.74,541.39;433.02,523.52" z_order="0">
    <attribute name="position">R1</attribute>
    <attribute name="style">dashed</attribute>
    <attribute name="color">white</attribute>
    <attribute name="kind">single</attribute>
  </polyline>
  <tag label="camera" source="manual">
    <attribute name="value">front</attribute>
  </tag>
</image>
```

## 7. Tự đánh giá
- **Lỗi bạn mắc nhiều nhất hôm nay (theo mã QC1-xx), và cách tránh ở Ngày 20:**
  - Mã lỗi dễ mắc nhất là **`QC1-02`** (bỏ sót vạch `R1` sát xe phía trước ở A07 và `L1` ở A06 trong lần rà đầu tiên) và **`QC1-11`** (vẽ polyline trên ảnh fisheye B03 mới chỉ có 3 điểm thay vì $\ge 4$ điểm theo cung cong, và phân vân ranh giới 80% bán kính `edge_zone` ở B04).
  - **Cách tránh ở Ngày 20:** Sau khi gán xong mỗi ảnh, kiểm tra ngay bảng Objects xem đã gán đủ bộ `L1`, `R1` (nếu có sơn trên mặt đường) chưa; với ảnh fisheye luôn chấm từ 4–8 điểm dọc theo cung cong của vạch làn/mép lề, và chạy `road_check lint` ngay sau khi export để rà soát toàn bộ cảnh báo.
- **Nhãn của bạn đi vào model ở đâu? Chọn một lỗi đã sửa và nói nó làm model học sai thế nào:**
  - Nhãn `lane` (polyline) đi vào làm **ground-truth target cho các mô hình phát hiện làn đường (Lane Detection như mô hình Row-Anchor / Ultra-Fast Lane Detection)** phục vụ hệ thống hỗ trợ giữ làn **LKA (Lane Keeping Assist)**; nhãn `drivable` đi vào nhánh **Semantic / Drivable Area Segmentation**; còn `traffic_light` và `traffic_sign` đi vào nhánh **2D Object Detection**.
  - **Ví dụ lỗi đã sửa:** Khi bỏ sót vạch `R1` ở ảnh `A07` (lỗi nặng `QC1-02`) hoặc vẽ polyline trên ảnh fisheye `B03` quá ít điểm khiến đoạn thẳng nối giữa các điểm lệch khỏi đường cong thực tế của vạch sơn (`QC1-11`), hàm loss của mô hình phát hiện làn đường sẽ bị phạt sai tại các hàng neo (coi một vạch làn thật là background / false positive, hoặc học sai tọa độ $x$ dọc theo cung cong). Hậu quả là bộ điều khiển giữ làn (LKA) và hệ thống quan sát quanh xe (SVM) không xác định được biên làn bên phải (`R1`) hoặc ước lượng sai quỹ đạo cong của làn đường, dẫn đến đánh lái lệch làn gây mất an toàn.

## 8. (Tùy chọn, buffer) Từ polyline đến đích row-anchor

*Kết quả nội suy tọa độ $x$ trên ảnh **`A01`** (chạy bằng `python -m road_lab.rowanchor`):*

**Bảng 8a — Vạch `R1` (`position = R1` trên `A01`):**
| y | 720 | 680 | 640 | 600 | 560 |
| --- | ---: | ---: | ---: | ---: | ---: |
| x của chúng tôi (`lane#7@(654,678)`) | không có làn | không có làn | 600.7 | 541.0 | 483.7 |
| x của bạn kia (`lane#5@(703,717)`) | không có làn | 658.2 | 601.9 | 544.9 | 486.9 |

**Bảng 8b — Vạch `L1` (`position = L1` trên `A01`):**
| y | 720 | 680 | 640 | 600 | 560 |
| --- | ---: | ---: | ---: | ---: | ---: |
| x của chúng tôi (`lane#10@(109,720)`) | 108.7 | 155.4 | 202.4 | 249.9 | 296.9 |
| x của bạn kia (`lane#4@(108,720)`) | không có làn | 154.4 | 201.2 | 247.9 | 295.4 |

Trả lời 3 câu:

1. **Năm số x đó chính là đích mà một model row-anchor học cho vạch này. Nếu bạn dừng polyline sớm 40 px, hàng nào đổi thành "không có làn"?**
   - Nếu dừng polyline sớm $40\text{ px}$ ở đầu xa (phía trên, tức $y_{\min}$ tăng thêm $40\text{ px}$ từ $523.5$ lên $563.5$), thì **hàng $y = 560$** sẽ nằm ngoài phạm vi của polyline và đổi thành **"không có làn"**. Ngược lại, nếu bắt đầu polyline muộn $40\text{ px}$ ở đầu gần xe (như vạch `R1` bắt đầu tại $y = 678.3$ thay vì $y = 720$), thì **các hàng sát xe là $y = 720$ và $y = 680$** đổi thành **"không có làn"**.
2. **So với bạn được kiểm (cùng ảnh): ở hàng 720 và hàng 560, hai bạn lệch nhau bao nhiêu pixel? Lệch ở hàng nào ảnh hưởng LKA nhiều hơn (slide 25)?**
   - Ở **hàng $y = 560$**: Với vạch `R1`, hai bạn lệch nhau $|483.7 - 486.9| = \mathbf{3.2\text{ px}}$ (với vạch `L1` lệch $|296.9 - 295.4| = \mathbf{1.5\text{ px}}$). Ở **hàng $y = 640$**: vạch `R1` lệch $\mathbf{1.2\text{ px}}$, vạch `L1` lệch $\mathbf{1.2\text{ px}}$. Riêng ở **hàng $y = 720$ và $y = 680$**: do điểm bắt đầu gần xe đặt lệch nhau vài pixel theo trục $y$ (ví dụ $y = 719.91$ của bạn Khang so với $y = 720.00$ của tôi trên `L1`, hoặc $y = 678.3$ so với $y = 716.6$ trên `R1`), một bên có tọa độ $x$ còn bên kia rơi vào trạng thái `"không có làn"`!
   - **Hàng ảnh hưởng LKA nhiều hơn:** Lệch hoặc mất nhãn ở **hàng $y = 720$ (và $y = 680$, tức vùng đáy ảnh sát đầu xe)** ảnh hưởng tới bộ điều khiển giữ làn **LKA (Lane Keeping Assist)** nhiều hơn trực tiếp đối với **độ lệch ngang tức thời (lateral offset error)** của xe vì đây là vị trí ngay trước mũi xe; trong khi đó, ở **hàng $y = 560$ (ở xa)** do hiệu ứng phối cảnh (perspective projection), mỗi pixel trên ảnh tương ứng với khoảng cách thực tế (mét) ngoài đời lớn hơn nhiều nên lệch vài pixel ở hàng $560$ sẽ làm sai lệch lớn **ước lượng độ cong làn đường và góc hướng xe (heading / curvature preview)** ở phía trước.
3. **Nếu polyline vẽ từ xa về gần (ngược quy tắc 2), cách tính trên có đổi không? Script nào sẽ gặp khó?**
   - Với riêng hàm nội suy từng đoạn thẳng độc lập trong `rowanchor.py` (xét điều kiện `(y1 - row) * (y2 - row) <= 0` trên từng cặp điểm liên tiếp), giá trị nội suy $x$ không đổi nếu polyline không tự cắt.
   - **Tuy nhiên các script sẽ gặp khó và báo lỗi:**
     1. **`road_check.py` (`lint` và `check` - mã `QC1-04`):** Kiểm tra trực tiếp chiều vector của polyline (`s.points[0][1] < s.points[-1][1]` trong `lint`, và `s1 < s0` khi chiếu điểm đầu `pts[0]` / điểm cuối `pts[-1]` lên GT trong `check`). Nếu vẽ từ xa về gần, điểm đầu `pts[0]` nằm ở xa còn điểm cuối `pts[-1]` nằm gần xe $\rightarrow$ script báo ngay lỗi chính **`QC1-04: vẽ ngược chiều (phải từ gần xe ra xa)`** và trừ điểm tiêu chí `dir` (8 điểm).
     2. **Các script huấn luyện mô hình dự đoán chuỗi điểm tuần tự hoặc ghép nối polyline (`_merge` trong `road_check.py` / parametrization theo độ dài cung $s$ từ xe ra xa):** Các thuật toán dựa vào việc điểm chỉ số `0` luôn là gốc tọa độ gần xe nhất để sắp xếp đoạn, tính vector tiếp tuyến hướng làn hoặc khởi tạo điểm neo gốc (anchor origin) sẽ bị đảo ngược hoàn toàn hướng làn đường.
