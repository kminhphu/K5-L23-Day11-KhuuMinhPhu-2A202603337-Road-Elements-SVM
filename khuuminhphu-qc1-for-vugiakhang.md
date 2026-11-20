# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): vugiakhang        Người kiểm (học viên): khuuminhphu  
Ngày: 2026-11-20                          Phiên bản guideline: Road v1.0  
File được kiểm (tên + `revision` trong manifest): vugiakhang-front.zip, vugiakhang-fisheye.zip (revision 1)  
Số ảnh kiểm: 6 (A01, A02, A05, A11, B02, B06; + 0 ảnh thêm, ghi riêng)   Số nhãn đã kiểm (shape + tag): 75 (51 shape + 24 tag)  

> **Ghi chú mẫu kiểm (6 ảnh):**
> - **Ảnh kiểm không có lỗi:** `A05` (`A05_b2576c8c-2de20b8a.jpg` — đủ 4 tag, `road_curb` và `drivable` hợp lệ; hai bên đường không có vạch sơn L1/R1 nên được miễn QC1-02 theo quy định).
> - **Ảnh phát hiện lỗi:** `A01`, `A02`, `A11`, `B02`, `B06`.

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 24 | 1 | nhẹ |
| QC1-02 đủ L1, R1 | bỏ sót | 10 | 0 | nặng |
| QC1-03 position | sai thuộc tính / thừa | 16 | 4 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 16 | 2 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 16 | 0 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 16 | 3 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 30 | 2 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 4 | 3 | nặng / chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 5 | 2 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 1 | 0 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 21 | 1 | chính |
| QC1-12 file | lỗi file | 75 | 0 | nhẹ / nặng |

## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-06 | A01 | `lane#1@(0,600)` | chính | Vạch trắng đôi bên trái nhưng gán `kind = single` (đúng là `kind = double`) |
| 2 | QC1-06 | A01 | `lane#2@(1279,708)` | chính | Vạch mép phải màu vàng nhưng gán `color = white` (đúng là `color = yellow`) |
| 3 | QC1-09 | A01 | `traffic_sign#3@(551,408)` | chính | Biển chỉ dẫn màu xanh lá trên cao tốc nhưng gán `group = prohibitory` (đúng là `information`) |
| 4 | QC1-03 | A02 | `lane#6@(251,512)` | nặng | Vạch ngoài cùng bên trái nhưng gán `position = L1` (đúng là `L2`) |
| 5 | QC1-03 | A02 | `lane#7@(511,569)` | nặng | Vạch đứt sát bên trái làn xe đang đi nhưng gán `position = R1` (đúng là `L1`) |
| 6 | QC1-03 | A02 | `lane#4@(1155,719)` | nặng | Vạch liền sát bên phải làn xe đang đi nhưng gán `position = R2` (đúng là `R1`) |
| 7 | QC1-04 | A02 | `lane#6@(251,512)` | chính | Điểm đầu polyline bắt đầu quá xa xe (`y = 512`), bỏ sót đoạn vạch gần xe |
| 8 | QC1-07 | A02 | `drivable#0@(2,716)` | chính | Gán nhầm `area_type = direct` cho làn bên trái (làn xe đang đi ở bên phải bị gán thành `alternative`) |
| 9 | QC1-01 | A11 | `tag:timeofday` | nhẹ | Ảnh chụp lúc hoàng hôn/chạng vạng nhưng gán `timeofday = day` (đúng là `dusk`) |
| 10 | QC1-03 | A11 | `lane#4@(66,715)` | nặng | Hai nét của vạch vàng đôi bên trái cùng là `L1` nhưng gán nét bên ngoài là `position = L2` (đúng là `L1`) |
| 11 | QC1-08 | A11 | `traffic_light#1@(367,312)` | nặng | Đèn giao thông bên trái hướng về xe (`facing = front`) đang sáng màu xanh nhưng gán `color = red` (đúng là `green`) |
| 12 | QC1-08 | A11 | `traffic_light#8@(624,310)` | nặng | Đèn giao thông bên phải hướng về xe (`facing = front`) đang sáng màu xanh nhưng gán `color = red` (đúng là `green`) |
| 13 | QC1-08 | B02 | `traffic_light#7@(1077,72)` | nặng | Đèn tín hiệu cột bên phải (`facing = front`) đang sáng hình người màu xanh nhưng gán `color = red` (đúng là `green`) |
| 14 | QC1-09 | B02 | `traffic_light#7@(1077,72)` | chính | Đèn dành cho người đi bộ qua đường nhưng gán `type = vehicle` (đúng là `pedestrian`) |
| 15 | QC1-06 | B06 | `lane#7@(923,495)` | chính | Vạch đứt dọc gờ phân cách nhưng gán `style = solid` (đúng là `dashed`) |
| 16 | QC1-07 | B06 | `crosswalk#6@(776,552)` | chính | Polygon `crosswalk` không bao trọn vùng vạch ngựa vằn (chỉ bao 2 vạch đầu, bỏ sót các vạch phía xa) |
| 17 | QC1-04 | B06 | `lane#10@(165,258)` | chính | Polyline dừng quá sớm và lệch khỏi tâm vạch đứt bên trái |
| 18 | QC1-11 | B06 | `lane#10@(165,258)` | chính | Polyline trên ảnh fisheye không bám theo cung cong của vạch đường (lệch > 5 px) |

## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| A05 | Hai bên làn đường chỉ có xe đỗ sát lề và vỉa hè, không có vạch sơn L1/R1 (lint báo QC1-02). Xác nhận miễn QC1-02 cho A05? | Đồng ý miễn QC1-02 vì ảnh thật sự không có vạch sơn L1/R1. |

## Quyết định
Lỗi nặng: 7   Lỗi chính: 10 / 75 nhãn = 13.3 %   Lỗi nhẹ: 1   Ca chờ lead: 0  
Quyết định (Release / Hold / Rework): **Rework**  
Lý do (theo luật của phiếu): Lô có 7 lỗi nặng (sai `position` của `lane` ở A02, A11 và sai màu đèn `facing = front` đang sáng xanh gán thành đỏ ở A11, B02) và tỉ lệ lỗi chính là 13.3 % (> 5 % số nhãn đã kiểm) → bắt buộc **Rework**.  

Loại lỗi: bỏ sót = thiếu nhãn phải có; thừa = gán cái không phải đối tượng; sai phạm vi = hình lệch, sai chiều, dừng sai chỗ, tràn vùng. Ba loại này theo cách chia lỗi gán nhãn của ISO/IEC 5259-4 (mục 8.4.2); "sai thuộc tính" và "lỗi file" là khóa học thêm. Cách xếp mức: [thang mức lỗi](../docs/qc_severity_road_v1.0.md).
