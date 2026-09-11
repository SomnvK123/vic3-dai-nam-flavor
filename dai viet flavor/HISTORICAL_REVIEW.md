# Thẩm Định Lịch Sử & Đề Xuất Cải Tiến Mod Dai Viet Flavor

> **Mục đích:** Đối chiếu nội dung mod với sử liệu triều Nguyễn (1836-1885), chỉ ra chỗ chưa ổn, đề xuất cải tiến cụ thể có thể thực hành từng bước. Dùng làm tài liệu tham khảo lâu dài.

---

## Phần A. THẨM ĐỊNH ĐỘ CHÍNH XÁC LỊCH SỬ

### A.1. Ngày sinh / ngày mất nhân vật lịch sử

Nhiều `birth_date` đang đặt tạm ở `YYYY.1.1` — game không crash nhưng gây lệch tuổi khi so với event trigger. Sửa cho đúng để mọi tính toán trưởng thành/thăng chức bằng game_date đều khớp.

| Nhân vật | Trong mod | Sử liệu (Đại Nam Thực Lục / Đại Nam Liệt Truyện) | Ghi chú |
|---|---|---|---|
| Nguyễn Phúc Hồng Nhậm (Tự Đức) | 1829.9.22 | **1829.9.22** | ✅ Chính xác |
| Nguyễn Phúc Hồng Bảo (An Phong Công) | 1825.1.1 | **1825.5.4** (âm lịch: Ất Dậu, tháng 4) | ⚠️ Nên chỉnh |
| Nguyễn Phúc Hồng Cai (Kiên Thái Vương) | 1845.1.1 | **1847.6.11** — cha ruột 3 vua Kiến Phúc, Hàm Nghi, Đồng Khánh | ⚠️ Sai 2 năm |
| Miên Thẩm (Tùng Thiện Vương) | 1819.1.1 | **1819.12.24** | ⚠️ Nên chỉnh |
| Miên Trinh (Tuy Lý Vương) | 1820.1.1 | **1820.2.3** | ⚠️ Nên chỉnh |
| Miên Định (Thọ Xuân Vương) | 1810.1.1 | **1810.7.15** | ⚠️ Nên chỉnh |
| Trương Đăng Quế | 1793.1.1 | **1793.11.1** — mất 1865.4.1 (73 tuổi) | Thêm `death_date = 1865.4.1` |
| Nguyễn Tri Phương | 1800.1.1 | **1800.9.21 (25/7 Canh Thân)** — mất 1873.12.20 | Thêm `death_date` |
| Nguyễn Trường Tộ | 1828.1.1 | **1828.1.1 hoặc 1830** (chưa thống nhất, gia phả 1830) — mất 1871.11.22 | Cân nhắc 1830.1.1 + `death_date` |
| Phạm Phú Thứ | 1821.1.1 | **1821.12.24** — mất 1882.2.5 | ⚠️ Nên chỉnh |
| Phan Thanh Giản | 1796.1.1 | **1796.11.12** — mất 1867.8.4 (uống thuốc độc) | Cần `death_date` |
| Đặng Huy Trứ | 1825.1.1 | **1825.5.16** — mất 1874.7.7 tại Đồn Vàng (Cần Thơ) | ⚠️ Nên chỉnh |
| Bùi Viện | 1839.1.1 | **1839.1.5** — mất 1878.11.1 | Gần đúng |
| Nguyễn Tư Giản | 1823.1.1 | **1823.10.13** — mất 1890.10 | ⚠️ Nên chỉnh |
| Đinh Văn Điền | 1833.1.1 | **1833** (chỉ biết năm), mất 1875 | ✅ Có thể giữ |
| Trần Đình Túc | 1805.1.1 | **1805.10** — mất 1892.12.15 | Gần đúng |
| Tôn Thất Thuyết | 1839.1.1 | **1839.5.12** — mất 1913.9.22 tại Long Châu, TQ | ⚠️ Nên chỉnh |
| Hoàng Diệu | 1829.1.1 | **1829.2.10** — tuẫn tiết 1882.4.25 | Cần `death_date` |
| Vũ Phạm Khải | 1807.1.1 | **1807.6.12** — mất 1872.10.8 | ⚠️ Nên chỉnh |
| Nguyễn Văn Tường | 1824.1.1 | **1824.9.16** — mất **1886.7.30** tại Tahiti (bị Pháp lưu đày) | Cần `death_date` |
| Trần Tiễn Thành | 1813.1.1 | **1813** (Quý Dậu) — bị Tôn Thất Thuyết giết 1883.11.30 | Cần `death_date` |

> **Thực hành:** Cập nhật birth_date + thêm `death_date` cho những nhân vật có ngày mất < 1936 (game endpoint). Điều này cho phép mod dùng `on_character_death` chuẩn xác thay vì phải check tuổi.

---

### A.2. Vai trò lịch sử vs Interest Group trong mod

Một số ánh xạ IG hiện tại chưa phản ánh đúng vai trò lịch sử:

| Nhân vật | IG trong mod | Đề xuất | Lý do |
|---|---|---|---|
| **Đặng Huy Trứ** | `ig_intelligentsia` | Có thể chuyển sang `ig_industrialists` khi IG này xuất hiện | Ông là **thương gia — nhà kỹ nghệ** đầu tiên của VN (sáng lập Ty Bình Chuẩn, xưởng ảnh Cảm Hiếu Đường, mua súng Hongkong). Không phải sĩ phu thuần túy. |
| **Bùi Viện** | `ig_armed_forces` | `ig_intelligentsia` hoặc chia đôi role | Ông là **quan văn kiêm ngoại giao** hơn là võ tướng. Vai trò xây thủy quân là thứ yếu. |
| **Nguyễn Văn Tường** | `ig_landowners` | `ig_intelligentsia` hoặc `ig_petty_bourgeoisie` | Không thuộc danh gia vọng tộc; ông xuất thân **con nhà nghèo, đỗ Cử nhân**, giỏi mưu lược chứ không phải địa chủ. Ideology `authoritarian` thì đúng. |
| **Trương Đăng Quế** | `ig_landowners` | ✅ Giữ | Đại địa chủ Quảng Ngãi, thuộc dòng dõi khoa cử lâu đời. |
| **Miên Định** | `ig_landowners` | `ig_intelligentsia` | Là hoàng thân, chức Tôn Nhân Phủ — thuộc nhóm trí thức triều đình hơn địa chủ. |
| **Vũ Phạm Khải** | `ig_landowners` | `ig_intelligentsia` | Ông là **sử quan** (Quốc Sử Quán), viết sử triều đình, không phải điền chủ. |

---

### A.3. Traits — Đã verify, KHÔNG cần sửa

> **Cập nhật 2026-09-12:** Nhận định ban đầu ở đây là SAI. Đã verify chéo bằng cách grep toàn bộ
> `dai viet flavor/common/character_templates/*.txt` trong mod 3219 (890 file, mod tham chiếu đã
> chạy ổn định) — tất cả các trait bị nghi ngờ dưới đây (`elder`, `stalwart_defender`,
> `master_bureaucrat`, `masterful_diplomat`, `expert_naval_commander`, `direct`, `wrathful`,
> `aesthete`, `imposing`, `imperious`, `innovative`) **đều được mod 3219 dùng thật sự bên trong
> block `traits = {...}`** của character template, và **không** được định nghĩa lại trong file
> custom trait của mod 3219 (`joi_skill_traits.txt`, `joi_special_personality_traits.txt`) — nghĩa
> là chúng là trait **vanilla gốc**, không phải trait tự chế. Ngược lại, `innovator` và
> `expert_diplomat` (thứ tôi từng đề xuất thay thế) có **0 lượt dùng** trong toàn bộ mod 3219.
>
> **Kết luận:** Không cần sửa gì trong `dvf_princes.txt` về traits. Bài học: đừng đoán tên
> trait từ trí nhớ — luôn grep một mod tham chiếu lớn đã chạy được trước khi kết luận.

**Bug thật đã tìm thấy và sửa (không phải trait):** `ideology = ideology_jingoist` (dùng cho
Tôn Thất Thuyết) — verify thấy trong TOÀN BỘ mod 3219, field `ideology` của character template
chỉ bao giờ dùng `ideology_jingoist_leader` (có hậu tố `_leader`), không bao giờ dùng bản
`ideology_jingoist` trơn (bản đó chỉ dùng cho Interest Group, khác namespace). Đã sửa.

> **Thực hành khi nghi ngờ 1 identifier (trait/ideology/building/trigger/effect):**
> ```bash
> grep -rn "\bidentifier_name\b" <mod_tham_chieu_lon>/
> ```
> Không có kết quả không chứng minh nó sai (có thể mod đó chỉ không dùng tới), nhưng CÓ kết quả
> ở đúng ngữ cảnh (VD: bên trong `traits = {...}`) là bằng chứng mạnh nó tồn tại thật.

---

### A.4. Sự kiện lịch sử — Timeline chuẩn cần đối chiếu

Timeline **đúng** của giai đoạn 1841-1885 mà mod nên bám sát:

```
1841.01.28 — Vua Minh Mạng băng hà.
1841.01.28 — Thiệu Trị lên ngôi (34 tuổi).
1842.08.29 — Hiệp ước Nam Kinh (Anh-Thanh). ✅ Mod có (Event 1)
1843.02.25 — Vụ Héroïne: tàu Pháp đòi thả 5 giáo sĩ.
1845.02    — Vụ Constitution: Đại tá Percival (Mỹ) bắn phá Đà Nẵng.
1847.04.15 — Thiệu Trị cự tuyệt Pháp; 2 tàu Gloire+Victorieuse
             (Lapierre + Rigault de Genouilly) đánh chìm 5 chiến
             thuyền bọc đồng Đại Nam, 230 lính chết. ✅ Mod có (Event 2)
1847.11.04 — Thiệu Trị băng hà.
1847.11.10 — Hồng Nhậm (Tự Đức, 18 tuổi) lên ngôi qua di chiếu do
             Trương Đăng Quế soạn — bỏ qua Hồng Bảo, Hồng Phò.
1848.03.21 — Tự Đức ra dụ cấm đạo lần 1 (nghiêm khắc hơn Minh Mạng).
1851.03    — Dụ cấm đạo lần 2 (chặt đầu giáo sĩ nước ngoài).
1851       — Hồng Bảo bắt đầu âm mưu, liên lạc với giáo sĩ Pellerin.
1854.01    — Âm mưu Hồng Bảo bại lộ. Ông bị đổi tên thành Đinh Đạo.
1854.08    — Hồng Bảo thắt cổ tự vẫn trong ngục (theo Đại Nam Thực Lục).
1855.07.21 — Dụ cấm đạo lần 3 (chuyên nghiêm hơn).
1856.09.26 — Chiến hạm Catinat (Le Lieur) nả pháo Đà Nẵng 1 ngày. ✅ Mod (Event 15)
1857.07.05 — Napoleon III chuẩn y kế hoạch viễn chinh Đông Dương.
1858.09.01 — Liên quân Pháp-Tây Ban Nha (14 tàu, 3.000 quân) do
             Rigault de Genouilly chỉ huy tấn công Đà Nẵng. ✅ Mod (Event 15)
1859.02.17 — Pháp chiếm Gia Định (Sài Gòn thất thủ).
1859.04    — Rigault rút khỏi Đà Nẵng, chuyển toàn lực vào Nam Kỳ.
1861.02.24-25 — Trận Đại đồn Chí Hòa: Nguyễn Tri Phương thua Charner.
1861.12.10  — Nguyễn Trung Trực đốt tàu Espérance ở Nhật Tảo.
1862.06.05 — Hiệp ước Nhâm Tuất: nhượng 3 tỉnh miền Đông + đảo
             Côn Lôn + bồi thường 4 triệu franc.
1863.06    — Sứ đoàn Phan Thanh Giản-Phạm Phú Thứ-Ngụy Khắc Đản
             sang Pháp chuộc đất, thất bại.
1864.08.19 — Trương Định tuẫn tiết tại Ao Vông (Gò Công).
1865       — Đặng Huy Trứ đi công cán Hongkong lần 1.
1866.05    — Loạn Chày Vôi ở Huế (thợ xây lăng Tự Đức nổi dậy) do
             Đoàn Trưng, Đoàn Hữu Ái cầm đầu — cực kỳ liên quan chuỗi
             Hồng Bảo vì phe nổi dậy đưa Đinh Đạo (con Hồng Bảo) làm vua.
1867.06.20-24 — Pháp chiếm 3 tỉnh miền Tây (Vĩnh Long, An Giang, Hà Tiên).
1867.08.04 — Phan Thanh Giản uống thuốc độc tự vẫn.
1868       — Đinh Văn Điền dâng điều trần (Ninh Bình).
1868       — Nguyễn Tư Giản đi sứ Bắc Kinh, viết "Yên Thiều Bút Lục".
1873.11.20 — Francis Garnier đánh chiếm Hà Nội lần 1.
1873.12.21 — Garnier tử trận tại Cầu Giấy (Lưu Vĩnh Phúc - Cờ Đen).
1873.12.20 — Nguyễn Tri Phương bị thương ở Hà Nội, tuyệt thực chết.
1874.03.15 — Hiệp ước Giáp Tuất: nhượng toàn bộ Nam Kỳ Lục Tỉnh.
1873/1875 — Bùi Viện sang Mỹ, gặp Tổng thống Grant, không có kết quả.
1882.04.25 — Henri Rivière chiếm Hà Nội lần 2, Hoàng Diệu tuẫn tiết.
1883.05.19 — Rivière tử trận tại Cầu Giấy (Cờ Đen).
1883.07.19 — Tự Đức băng hà.
1883.08.25 — Hiệp ước Quý Mùi (Harmand): Đại Nam nhận bảo hộ.
1884.06.06 — Hiệp ước Giáp Thân (Patenôtre): chính thức mất chủ quyền.
1885.07.05 — Kinh thành thất thủ; Tôn Thất Thuyết đưa Hàm Nghi ra Tân Sở,
             xuất Hịch Cần Vương.
```

**Sự kiện đang thiếu hoặc chưa mô hình hoá đủ:**

1. ⚠️ **Loạn Chày Vôi 1866** — cực kỳ quan trọng vì phe nổi dậy chính là hậu duệ Hồng Bảo. Đây có thể là "Bad Ending" của path đảo chính thất bại: Đinh Đạo (con trai Hồng Bảo, khoảng 15 tuổi năm 1866) làm cờ hiệu cho phe thợ xây lăng nổi dậy → thất bại → toàn gia bị giết.
2. ⚠️ **Cờ Đen (Lưu Vĩnh Phúc)** — Không có nhân vật/mechanism nào cho lực lượng biên phòng phía Bắc thuê từ tàn dư Thái Bình Thiên Quốc, dù họ giết 2 chỉ huy Pháp (Garnier 1873, Rivière 1883).
3. ⚠️ **Chuyện nội cung Tự Đức** — Ông không con (bị bệnh đậu mùa mất khả năng sinh dục), phải nhận 3 con nuôi từ Kiên Thái Vương (Ưng Chân=Dục Đức, Ưng Đường=Đồng Khánh, Ưng Đăng=Kiến Phúc). Khủng hoảng kế vị 1883-1884 (bốn tháng ba vua) là bi kịch có sẵn — nên có chuỗi.
4. ⚠️ **Trương Định, Nguyễn Trung Trực, Nguyễn Đình Chiểu** — Nam Kỳ có hàng loạt nhân vật kháng chiến bị bỏ qua.
5. ⚠️ **Tự Đức làm thơ** — Ông là một trong những vua làm thơ nhiều nhất VN (khoảng 4.000 bài chữ Hán + 100 bài Nôm). Flavor event tốt cho legitimacy.
6. ⚠️ **Xây lăng Tự Đức (Khiêm Lăng)** — Bắt đầu 1864, hoàn thành 1873, tiêu tốn ngân khố + gây oán thán → nguyên nhân trực tiếp Loạn Chày Vôi.

---

### A.5. Cấm đạo — Mô hình hoá quá đơn giản

Hiện tại mod chỉ dùng flag `law_state_religion` vs `law_freedom_of_conscience`. Điều này **bỏ qua toàn bộ phổ chính sách trung gian**:

Thực tế 1848-1862, có **5 mức độ cấm đạo** khác nhau:

| Mức | Nội dung | Năm | Hậu quả |
|---|---|---|---|
| 1 | Cấm rao giảng nơi công cộng | Minh Mạng 1833 | Không đủ để Pháp lấy cớ |
| 2 | Đuổi giáo sĩ nước ngoài | Thiệu Trị 1844 | Vụ Héroïne |
| 3 | Bắt giáo dân bước qua thập giá | Tự Đức 1848 | Bắt đầu chết chóc |
| 4 | Chém đầu giáo sĩ + tịch thu tài sản | Tự Đức 1851 | Hàng chục giáo sĩ Pháp/TBN chết |
| 5 | "Phân sáp": tách giáo dân khỏi làng, thích chữ "tả đạo" lên má | Tự Đức 1861 | 40.000+ giáo dân chết, Pháp lấy cớ chính thức |

**Đề xuất:** Thay vì binary trigger, dùng 1 variable `dvf_persecution_level` (0-5) tăng dần theo events, và **casus belli của Pháp scale theo mức này**. Có 1 sự kiện "Nới lỏng phân sáp" (giữ luật quốc giáo nhưng bỏ đàn áp) như con đường trung dung.

---

### A.6. Quan hệ triều cống — Đang thiếu

Đại Nam là **chư hầu Đại Thanh** đến năm 1885 (Hiệp ước Thiên Tân Pháp-Thanh). Chuyện triều cống 3 năm/lần với các món:

- Kim khí: 10 kg vàng, 100 kg bạc (danh nghĩa)
- Đặc sản: quế Thanh Hoá, ngà voi, sừng tê giác, gấm vóc
- Đổi lại: sách phong "An Nam Quốc Vương"

Việc **không mô hình hoá quan hệ này** dẫn đến 2 vấn đề:
1. Không có "chuyển giao chính danh" khi Đại Thanh yếu (1860s Loạn Thái Bình + Loạn Boxer).
2. Không có tension khi Pháp yêu cầu Đại Nam **cắt đứt triều cống** (điều khoản trong Hiệp ước Giáp Thân 1884).

**Đề xuất:** 1 subject_type mới `qing_tributary` với modifier nhỏ (+5 prestige, +5 legitimacy khi cống nạp) và JE "Đoạn tuyệt sách phong" khi Pháp ép.

---

## Phần B. RÀ SOÁT NỘI DUNG HIỆN CÓ

### B.1. Bug logic — ĐÃ SỬA (2026-09-12)

1. ✅ **`building_shipyards` (số nhiều)** → `building_shipyard` (số ít). Sửa ở 3 nơi: `dvf_opium_war_je.txt` (trigger `complete`/`fail`), `dvf_opium_war_scripted_values.txt` (`building_shipyards_count`), `dvf_opium_war_l_english.yml` (biến hiển thị `$building_shipyards$`). Trước đây khiến JE Tự Cường không complete được vì building id sai không bao giờ match.

2. ✅ **`ideology_jingoist`** (Tôn Thất Thuyết) → `ideology_jingoist_leader`. Verify: field `ideology` của MỌI character template trong mod 3219 chỉ dùng bản có hậu tố `_leader`; bản trơn `ideology_jingoist` chỉ tồn tại như 1 ideology cấp Interest Group, không dùng được cho character.

3. ✅ **`ideology_authoritarian` / `ideology_reformer`** — đã verify HỢP LỆ (dùng trực tiếp, không cần hậu tố `_leader`, xác nhận qua character_templates của mod 3219). Không cần sửa.

4. ⚠️ **`any_scope_building = { is_building_type = X count >= N }` ở country scope trực tiếp** (trong `je_dvf_self_strengthening`'s complete/fail) — CHƯA sửa, nhưng đánh giá lại: đây có khả năng là cú pháp ĐÚNG (khác mục đích với pattern `any_scope_state { count >= N any_scope_building {...} }` — một cái đếm tổng số building loại X trên toàn quốc, một cái đếm số STATE có building đó). Cần test in-game để chắc chắn 100%, nhưng không còn nghi ngờ cao như trước.

5. **`dvf_military_investment_score` scripted_value** — đã đọc file, cấu trúc hợp lệ (`value = 0` + `add = building_arms_industry_count` + `add = building_shipyards_count`), chỉ có building id sai đã sửa ở mục 1.

### B.2. Vấn đề cân bằng gameplay

> **Cập nhật 2026-09-12 — Đã sửa 3/3 mục dưới đây:**
> - `dvf_hong_bao_reform_court`: giảm buff/debuff từ ±0.50/±0.40/±0.35/±0.30 xuống ±0.25/±0.20/±0.15.
> - `dvf_great_modernization`: giảm còn ~60% giá trị gốc mọi dòng.
> - JE giờ có 2 mốc trung gian (Sơ Canh Tân ở 2/6 trụ cột, Trung Canh Tân ở 4/6 trụ cột) qua
>   scripted_value `dvf_pillars_completed_count`, modifier `dvf_hong_bao_milestone_bronze`/`_silver`,
>   và 2 event mới `dvf_hong_bao_restoration.3`/`.4` — người chơi thấy phần thưởng sớm thay vì
>   phải chờ hoàn thành hết 250-300 building level mới có gì.
>
> Yêu cầu hoàn thành đầy đủ 6 trụ cột (bảng dưới) **chưa đổi** — nếu vẫn thấy quá khó khi playtest,
> cân nhắc giảm số lượng building yêu cầu ở từng trụ cột (không chỉ thêm milestone).

**Journal Entry "Canh Tân Đất Nước" quá khó:**

Yêu cầu hiện tại:
- 5 trường đại học + 1 học viện mỹ thuật + literacy 40%
- 25 rice farm level 5+ (tương đương ~125 building levels)
- Coal 4+4, Iron 4, Paper 2+2, Textile 2+2, Railway 1+1
- 6 xưởng vũ khí + 3 xưởng đạn + 3 xưởng tàu
- 40 barracks + 10 naval base
- 3 port + 3 trade route + relations 20 với GP

**Ước tính:** Cần khoảng **250-300 building levels tổng**, tương đương 15-20 năm phát triển liên tục của một quốc gia bình thường. Đại Nam khởi đầu 1836 với ngân sách ~50k, tech tier 4, arable land hạn chế → khó đạt trong khung thời gian JE (nếu JE bắt đầu ~1848 sau đảo chính, kết thúc trước 1900 → 50 năm là khả thi nhưng phải chơi tối ưu).

**Đề xuất giãn:** Chia làm 3 giai đoạn (bronze/silver/gold), mỗi giai đoạn có phần thưởng:
- Bronze (Sơ Canh Tân): 5-10 building levels mỗi trụ cột → +5 innovation, +10% construction
- Silver (Trung Canh Tân): 15-20 building levels → +15 innovation, +5 diplo rep
- Gold (Đại Canh Tân): con số hiện tại → phần thưởng đầy đủ

**Modifier `dvf_hong_bao_reform_court` quá mạnh:**

Debuff -50% Landowners clout + -10 approval + -30% Devout **kéo dài đến khi JE hoàn thành** (có thể 30-50 năm) sẽ tạo **radicals cực nhiều** dẫn đến civil war không kiểm soát. Đề xuất:
- Giảm về ±0.20 (20%) thay vì 0.50
- Thời hạn 10-15 năm thay vì vô hạn
- Có 1 sub-event "Hoà giải Nho gia" ở giữa để giảm áp lực

**Modifier `dvf_great_modernization` quá hào phóng:**

15 dòng modifier vĩnh viễn với +25 innovation add, +30 max cap, +25% mult là stronger than **Meiji Restoration reward** của vanilla. Đề xuất scale xuống 60-70%.

---

### B.3. Character templates — Traits không tồn tại

Chạy check này để tìm traits invalid (từ trong game/common/character_traits/):

```bash
# Trong thư mục vanilla Victoria 3
grep -rn "^[a-z_]* = {" game/common/character_traits/*.txt | \
  awk -F: '{print $2}' | awk '{print $1}' | sort -u > /tmp/valid_traits.txt

# Traits dùng trong mod
grep -oP "^\s+\K[a-z_]+" "dai viet flavor/common/character_templates/dvf_princes.txt" | \
  sort -u > /tmp/mod_traits.txt

comm -23 /tmp/mod_traits.txt /tmp/valid_traits.txt
```

Trait không hợp lệ sẽ không crash nhưng nhân vật sẽ không có trait đó → mất commander bonus.

---

## Phần C. ĐỀ XUẤT NỘI DUNG MỞ RỘNG

### C.1. Nhân vật lịch sử cần bổ sung

**Nhóm Kháng chiến Nam Kỳ (1859-1868):**

| Tên | Sinh-Mất | Vai trò | IG đề xuất | Ideology |
|---|---|---|---|---|
| **Trương Định** | 1820-1864 | "Bình Tây Đại Nguyên Soái", tuẫn tiết Gò Công | ig_armed_forces | jingoist |
| **Nguyễn Trung Trực** | 1838-1868 | Đốt tàu Espérance 1861, "Bao giờ Tây nhổ hết cỏ nước Nam..." | ig_armed_forces | jingoist |
| **Nguyễn Đình Chiểu** | 1822-1888 | Nhà thơ mù, "Văn tế nghĩa sĩ Cần Giuộc" | ig_intelligentsia | reformer |
| **Nguyễn Hữu Huân** | 1830-1875 | "Thủ khoa Huân" — chỉ huy Mỹ Tho kháng Pháp | ig_intelligentsia | jingoist |
| **Võ Duy Dương** | 1827-1866 | "Thiên Hộ Dương" — Đồng Tháp Mười khởi nghĩa | ig_armed_forces | jingoist |

**Nhóm Cận thần Tự Đức:**

| Tên | Sinh-Mất | Vai trò |
|---|---|---|
| **Từ Dụ (Phạm Thị Hằng)** | 1810-1902 | Mẹ Tự Đức, thái hậu quyền uy nhất triều Nguyễn |
| **Nguyễn Bá Nghi** | 1807-1870 | Kinh lược sứ Nam Kỳ, ký hoà nghị Nhâm Tuất |
| **Đào Trí** | ?-? | Tổng trấn Đà Nẵng khi Pháp tấn công 1858 |

**Nhóm Lãnh đạo Cần Vương (1885+):**

| Tên | Sinh-Mất | Vai trò |
|---|---|---|
| **Phan Đình Phùng** | 1847-1895 | Khởi nghĩa Hương Khê (Hà Tĩnh) 1885-1896 |
| **Nguyễn Thiện Thuật** | 1844-1926 | Khởi nghĩa Bãi Sậy (Hưng Yên) |
| **Hoàng Hoa Thám** | 1858-1913 | "Đề Thám" — Khởi nghĩa Yên Thế 1884-1913 |
| **Tôn Thất Đàm** | 1863-1888 | Con trai Tôn Thất Thuyết, cố vấn Hàm Nghi |

**Nhóm Quốc tế liên quan:**

| Tên | Vai trò |
|---|---|
| **Lưu Vĩnh Phúc** | Thủ lĩnh Cờ Đen, giết Garnier và Rivière |
| **Francis Garnier** | Đại uý Pháp chiếm Hà Nội 1873, chết Cầu Giấy |
| **Henri Rivière** | Đại tá Pháp chiếm Hà Nội 1882, chết Cầu Giấy |
| **Léopold Pallu** | Đại tá Pháp, chỉ huy vây Đà Nẵng 1858-1859 |
| **Pigneau de Béhaine** | (đã chết) — nhưng vẫn có ảnh hưởng qua di sản Gia Long |

---

### C.2. Journal Entries đề xuất

**JE mới nên thêm:**

1. **`je_dvf_su_khac_qing`** — "Sứ Khác Đại Thanh": duy trì quan hệ triều cống với Thanh
   - Trigger: mỗi 3 năm
   - Complete: hoàn thành phái sứ đoàn (decision)
   - Reward: +10 prestige, legitimacy +5
   - Fail: -5 prestige với Đại Thanh, mất sách phong

2. **`je_dvf_xay_khiem_lang`** — "Xây Khiêm Lăng" (Lăng Tự Đức)
   - Trigger: game_date >= 1864, ruler = Tự Đức
   - Complete: chi 500k ngân khố + 6 năm
   - Reward: +50 prestige nhưng radicals +5%, kích hoạt Loạn Chày Vôi
   - Đây là **hard historical moment** — người chơi phải chọn giữa danh vọng và ổn định

3. **`je_dvf_lu_lut_song_hong`** — "Lũ Sông Hồng"
   - Trigger: random 1848, 1856, 1872 (các năm lũ lịch sử)
   - Complete: đầu tư đê điều (100k) hoặc chi tiền cứu tế (50k)
   - Fail: dân đói, radicals +10% miền Bắc, pop dead 5%

4. **`je_dvf_binh_dinh_nam_ky`** — "Bình Định Nam Kỳ" (chống du kích Trương Định-Nguyễn Trung Trực)
   - Chỉ trigger nếu Pháp CHƯA chiếm Nam Kỳ (alt-history sau khi đảo chính Hồng Bảo thành công)
   - Complete: dập tắt các cuộc khởi nghĩa nhỏ do phe Nho gia thù địch với Hồng Bảo tổ chức

5. **`je_dvf_can_vuong`** — "Chiếu Cần Vương"
   - Chỉ trigger nếu Pháp đã chiếm Kinh thành (worst outcome)
   - Trigger flag phong trào kháng chiến 1885-1896

6. **`je_dvf_khoa_cu_cai_cach`** — "Khoa Cử Cải Cách"
   - Con đường thay thế đến `law_appointed_bureaucrats`
   - Đấu tranh giữa phe cải cách và phe Nho gia trên nội dung thi cử

**JE cần refactor:**

- **`je_dvf_hong_bao_coup`**: Nên có 3 kết cục, không chỉ 2 (thành công 5/5 hoặc thất bại 0/5). Thêm kết cục **compromise** ở tiến trình 3/5: Hồng Bảo được ân xá, làm "thái thượng hoàng cải cách" bên cạnh Tự Đức (giống Nhật hoàng thời Minh Trị vs Shogun).

- **`je_dvf_self_strengthening`**: JE này hiện chồng chéo với `je_dvf_hong_bao_restoration` (cả hai đều bắt phát triển quân sự + công nghiệp). Nên gộp thành 1 JE có 2 phase hoặc phân định rõ:
  - Self-strengthening (1842-1858): giai đoạn PHẢN ỨNG khủng hoảng — tránh mất nước, tech basic
  - Restoration (post-coup, 1848+): giai đoạn CHỦ ĐỘNG canh tân — trở thành cường quốc

---

### C.3. Decision đề xuất

1. **`dvf_nop_cong_dai_thanh`** — Cống nạp Đại Thanh (mỗi 3 năm)
   - Cost: -20k treasury, -5 với Anh (không thích thần phục), +10 với Thanh, +5 prestige
   
2. **`dvf_khoi_cong_khiem_lang`** — Khởi công Khiêm Lăng
   - Trigger JE trên
   
3. **`dvf_du_di_hong_bao`** — Ân xá Hồng Bảo
   - Chỉ có nếu Hồng Bảo còn sống + tiến trình JE Coup 2-3/5
   - Kết thúc JE Coup ở compromise
   - Hồng Bảo chuyển từ agitator → advisor role

4. **`dvf_giao_thuong_hong_kong`** — Mở thương điếm Hongkong
   - Prerequisite: `law_mercantilism`, ngân khố 30k
   - Effect: gain trade route đặc quyền với Anh, spawn Dang Huy Tru event

5. **`dvf_thu_binh_khu_ngu_pho_binh`** — Cải cách quân dịch (kèm điều kiện tài chính)
   - Chuyển từ ngụ binh ư nông sang quân đội chuyên nghiệp
   - Đúng path để đến `law_professional_army`

6. **`dvf_muon_cua_hop_giao`** — "Rung Đông Kinh Nghĩa Thục" (nếu chơi late-game, 1907+)
   - Post-JE, phong trào canh tân dân sự

---

### C.4. Events flavor lịch sử đề xuất

**Nhóm cung đình:**
- `dvf_tu_duc_lam_tho` — Tự Đức làm thơ chữ Nôm (flavor +2 prestige)
- `dvf_tu_du_thai_hau_khuyen` — Từ Dụ khuyên Tự Đức
- `dvf_lang_khiem_khoi_cong` — Khởi công lăng
- `dvf_loan_chay_voi` — Nổi loạn thợ xây lăng 1866 (nếu chọn xây lăng)

**Nhóm quân sự:**
- `dvf_trang_dai_don_chi_hoa` — Trận Đại đồn Chí Hoà 1861
- `dvf_nguyen_trung_truc_dot_tau` — Đốt tàu Espérance
- `dvf_hoang_dieu_tuan_tiet` — Hoàng Diệu tuẫn tiết 1882
- `dvf_co_den_giet_garnier` — Cờ Đen giết Garnier tại Cầu Giấy

**Nhóm ngoại giao:**
- `dvf_su_doan_phan_thanh_gian` — Sứ đoàn 1863 sang Pháp
- `dvf_bui_vien_gap_grant` — Bùi Viện gặp Tổng thống Mỹ Grant
- `dvf_nguyen_tu_gian_di_su` — Sứ đoàn 1868 sang Thanh
- `dvf_phan_thanh_gian_uong_thuoc_doc` — Phan Thanh Giản tự vẫn 1867

**Nhóm văn hóa:**
- `dvf_nguyen_dinh_chieu_luc_van_tien` — Nguyễn Đình Chiểu viết Lục Vân Tiên
- `dvf_quoc_su_quan_xuat_ban_dnt_luc` — Quốc Sử Quán xuất bản Đại Nam Thực Lục
- `dvf_bao_chi_tieng_viet` — Ra đời báo Gia Định Báo 1865 (nếu Pháp chiếm Nam Kỳ)

---

### C.5. Cơ chế mới cần thiết kế

**1. Hệ thống "Phe Phái Triều Đình" (Court Factions)**

Hiện tại mod chỉ dùng IG vanilla nhưng thực tế triều Nguyễn có **các phe phái ngang IG**:

- **Phe Bảo thủ Nho gia** (Trương Đăng Quế, Vũ Phạm Khải): overlap `ig_landowners` + `ig_devout`
- **Phe Canh tân Trí thức** (Nguyễn Trường Tộ, Phạm Phú Thứ): overlap `ig_intelligentsia`
- **Phe Chủ chiến** (Tôn Thất Thuyết, Hoàng Diệu): overlap `ig_armed_forces`
- **Phe Ôn hoà Hoà nghị** (Phan Thanh Giản, Trần Tiễn Thành): trung dung
- **Phe Quyền thần Trung dung** (Nguyễn Văn Tường): opportunist

Có thể mô hình bằng **hidden variables** (điểm ảnh hưởng mỗi phe) + **scripted_gui** hiển thị dashboard.

**2. Hệ thống "Danh Vọng vs Ngân Khố" (Prestige/Treasury Tradeoff)**

Nhiều quyết định lịch sử triều Nguyễn là **đánh đổi ngân khố lấy chính danh** hoặc ngược lại:
- Xây lăng: -treasury +prestige +radicals
- Cống nạp Thanh: -treasury +prestige (với Thanh) -prestige (với Tây)
- Đàn áp Công giáo: +prestige (với Nho sĩ) -diplomatic reputation

**3. Hệ thống "Áp Lực Ngoại Xâm" (Foreign Pressure Meter)**

Một variable `dvf_foreign_pressure` (0-100) tăng theo thời gian và event, giảm khi:
- Thông qua Freedom of Conscience: -30
- Có Great Power làm đồng minh: -20
- Hải quân >= X ships: -10
- Ngân khố >= Y (có tiền bồi thường): -5

Khi >= 70: Pháp tự động fire `dvf_france.2` (invasion event).
Khi >= 90: Pháp tự động declare Diplomatic Play.

**4. Hệ thống "Kinh Tế Vùng" (Regional Economy)**

Vietnam có 3 vùng kinh tế khác biệt lịch sử — thay vì buff quốc gia thống nhất, nên có:
- **Bắc Kỳ (Tonkin)**: cần đê điều (flood modifier), tơ lụa, khai mỏ than
- **Trung Kỳ (Annam)**: kinh đô, thủ công mỹ nghệ, cảng chiến lược Đà Nẵng
- **Nam Kỳ (Cochinchina)**: khai hoang, xuất khẩu gạo, đa dạng cây công nghiệp

Mỗi vùng có 1 JE regional nhỏ + decision phát triển đặc thù.

---

## Phần D. VẤN ĐỀ KỸ THUẬT KHÁC

### D.1. Localization

Chưa review sâu, nhưng cần kiểm tra:
- Tất cả file `.yml` phải bắt đầu bằng BOM (UTF-8 with BOM)
- Dòng đầu phải là `l_english:` (không có dấu cách trước)
- Mỗi key format: ` key_name: "text"` (đúng 1 space đầu dòng, dấu `:` không cách)
- Kí tự tiếng Việt phải dùng UTF-8, không dùng escape sequence

### D.2. Icon paths

Nhiều event dùng path icon như `"gfx/interface/icons/event_icons/event_political.dds"` — phải verify các icon này **tồn tại trong vanilla** hoặc mod tự cung cấp. Icon thiếu → event chạy được nhưng không có ảnh.

### D.3. Videos

Path `video = "asia_court_politics"`, `video = "asia_westerners_arriving"` — vanilla Vic3 có collection video có tên khác. Cần grep `.bk2` files trong vanilla để verify:
```bash
find "vanilla/gfx/event_pictures/" -name "*asia*" -o -name "*orient*"
```

### D.4. Namespace conflicts

Cần đảm bảo tất cả `namespace` là unique so với vanilla + mod 3219:
- Đã dùng: `dvf_hong_bao`, `dvf_france`, `dvf_flavor`, `dvf_opium_war_events`, `dvf_hong_bao_restoration`, `dvf_hong_bao_restoration_chars`, `dvf_succession`, `transfer_state`
- Verify không conflict: `transfer_state` (dvf) vs bất kỳ vanilla namespace nào

### D.5. Character spawn conflict với `on_game_started`

Trong `dvf_power_bloc_on_actions.txt`, các character được spawn theo timeline. Nhưng nếu người chơi CHỌN đảo chính Hồng Bảo và Hồng Bảo lên ngôi trước khi các nhân vật spawn (VD Hồng Bảo lên ngôi 1849, Nguyễn Trường Tộ mới spawn 1861), thì Hồng Bảo chưa có cố vấn.

**Đề xuất:** Nếu Hồng Bảo là ruler → force spawn tất cả reformist characters ngay lập tức thay vì đợi timeline.

---

## Phần E. LỘ TRÌNH THỰC HÀNH ĐỀ XUẤT

Không nên làm tất cả một lúc. Chia thành 3 phase:

### Phase 1 (2-4 giờ) — Fix Bug + Historical Accuracy Cơ Bản
- [x] Sửa `building_shipyards` → `building_shipyard` (3 file: `dvf_opium_war_je.txt`,
      `dvf_opium_war_scripted_values.txt`, `dvf_opium_war_l_english.yml`)
- [x] Verify trait names — kết luận: TẤT CẢ đều hợp lệ, không cần sửa (xem A.3)
- [x] Verify ideology_authoritarian + ideology_reformer — hợp lệ, không cần sửa
- [x] Sửa `ideology_jingoist` → `ideology_jingoist_leader` (Tôn Thất Thuyết) — bug thật
- [x] Giảm modifier `dvf_hong_bao_reform_court` từ ±0.50/±0.40/±0.35/±0.30 → ±0.25/±0.20/±0.15
- [x] Giảm modifier `dvf_great_modernization` xuống ~60% giá trị gốc
- [x] Chia JE `je_dvf_hong_bao_restoration` thành milestone Sơ/Trung Canh Tân (2/6, 4/6 trụ cột)
      qua scripted_value `dvf_pillars_completed_count` + 2 modifier + 2 event mới
      (`dvf_hong_bao_restoration.3`/`.4`)
- [x] Cập nhật `birth_date` cho 18/20 nhân vật trong `dvf_princes.txt` theo bảng A.1 (2 nhân vật
      chỉ có năm sinh xác thực trong sử liệu, giữ nguyên `YYYY.1.1`/`YYYY.10.1`)
- [x] **KHÔNG thêm field `death_date`** — đã verify: field này **không tồn tại** trong Victoria 3
      (0/890 file mod 3219 dùng). Thay vào đó thêm **comment** ghi ngày mất thật trên mỗi nhân vật
      để tiện viết event `kill_character`/`on_character_death` sau này (cách duy nhất đúng để mô
      hình hoá cái chết trong Vic3 — xem mục A.3 cập nhật).
- [x] Đổi IG cho 4 nhân vật theo bảng A.2: Bùi Viện, Nguyễn Văn Tường, Miên Định, Vũ Phạm Khải
      → `ig_intelligentsia` (đã verify không có logic nào khác trong mod phụ thuộc IG cũ của họ)
- [x] **Phát hiện + xóa file hỏng ngoài kế hoạch:**
      `common/history/characters/DAI_dvf_characters.txt` dùng cú pháp **hoàn toàn không tồn tại**
      trong Victoria 3 (`character_template = { key = ... }`, `date_of_birth`, `date_of_death`,
      `is_ruler`, `ruler_type`, `agitator_type`, `traits = { X = yes }` — tất cả 0/890 file mod
      3219 dùng) và **định nghĩa trùng lặp** 6 nhân vật đã có đúng trong `dvf_princes.txt`
      (kể cả 1 key bị gõ nhầm `DAJ_truong_dang_que` mồ côi hoàn toàn). Đã xóa file, dữ liệu thật
      không mất vì đã tồn tại đúng ở `dvf_princes.txt` + `dvf_dai_princes.txt`.

### Phase 2 (1-2 ngày) — Nội dung Mở Rộng
- [ ] Thêm 5 nhân vật Nam Kỳ kháng chiến (Trương Định, Nguyễn Trung Trực, ...)
- [ ] Thêm nhân vật Từ Dụ (thái hậu)
- [ ] Viết JE `je_dvf_xay_khiem_lang` + event Loạn Chày Vôi
- [ ] Viết flavor event Tự Đức làm thơ
- [ ] Bổ sung 3-5 event kháng chiến lịch sử

### Phase 3 (1 tuần+) — Hệ thống Mới
- [ ] Thiết kế Court Faction system với scripted_gui
- [ ] Refactor JE Coup thành 3 kết cục (thất bại / compromise / thắng lợi)
- [ ] Foreign Pressure Meter thay cho hard-coded 1858 timer
- [ ] Regional Economy JEs (3 miền)
- [ ] Qing tributary system

---

## Phần F. TÀI LIỆU THAM KHẢO SỬ HỌC

Nên dùng khi viết event / character:

**Nguồn Sơ cấp:**
- **Đại Nam Thực Lục** (Quốc Sử Quán triều Nguyễn) — sử biên niên chính thống
- **Đại Nam Liệt Truyện** — tiểu sử nhân vật
- **Khâm Định Đại Nam Hội Điển Sự Lệ** — điển chế hành chính
- **Đại Nam Nhất Thống Chí** — địa lý hành chính
- **Minh Mệnh Chính Yếu** — chính sách Minh Mạng (làm nền cho các cải cách sau)
- **Nguyễn Trường Tộ Tòan Tập** (58 điều trần) — nguồn gốc trực tiếp của "Trụ Cột Canh Tân" trong mod
- **Tây Hành Nhật Ký** (Phạm Phú Thứ) — nhật ký sứ đoàn 1863
- **Đặng Hoàng Trứ Thi Văn Tập** — thi văn Đặng Huy Trứ

**Nguồn Thứ cấp uy tín:**
- Nguyễn Thế Anh, *Việt Nam Thời Pháp Đô Hộ*
- Đào Duy Anh, *Việt Nam Văn Hóa Sử Cương*
- Trần Trọng Kim, *Việt Nam Sử Lược* (từ Ch. XI)
- Trương Bá Cần, *Nguyễn Trường Tộ — Con Người và Di Thảo*
- Yoshiharu Tsuboi, *L'Empire vietnamien face à la France et à la Chine 1847-1885*
- Nguyễn Duy Chính, *Việt Thanh Chiến Dịch* (chi tiết quan hệ triều cống)
- Milton Osborne, *The French Presence in Cochinchina and Cambodia 1859-1905*

**Số liệu tài chính-quân sự:**
- Nola Cooke, *"Nineteenth-Century Vietnamese Confucianization in Historical Perspective"* (Journal of Southeast Asian Studies)
- Bảng thống kê ngân khố Nguyễn triều trong Đại Nam Thực Lục quyển 42-55 (thời Tự Đức)

---

## Phần G. NGUYÊN TẮC THIẾT KẾ (Lưu ý bản thân)

Rút ra từ quá trình xem xét mod:

1. **Tôn trọng determinism lịch sử nhưng cho phép agency** — Không phải mọi event là scripted "phải xảy ra"; cho người chơi ngã rẽ hợp lý.

2. **Balance != nerf** — Modifier +50%/-50% có thể "chuẩn xác lịch sử" nhưng game không chịu nổi. Scale xuống 10-20% và cộng dồn qua thời gian.

3. **Event chain phải có exit** — Nếu người chơi bỏ path Hồng Bảo (không đảo chính), toàn bộ content của mod vẫn phải chơi được → mọi variable dùng phải có fallback.

4. **Compat > Feature** — Với mod 3219 (JoI) đã bao phủ nhiều nội dung TQ, Pháp, Anh → không nên duplicate. Tập trung vào những gì JoI KHÔNG có (nội bộ triều Nguyễn, Nam Kỳ, kháng chiến).

5. **Verify trước khi viết** — Mọi `has_building_level`, `has_relations`, `set_country_flag`, `date` (bare), `activate_law` trong option: **grep trước** trong `game/common/` xem có tồn tại đúng cú pháp không. Đừng dựa vào EU4/HOI4 syntax cũ.

6. **1 lỗi cú pháp = 1 tính năng gãy** — Vic3 không crash khi gặp cú pháp sai, chỉ silent log vào `error.log`. Người chơi tưởng "feature không hoạt động" nhưng thực chất chưa bao giờ chạy.

7. **Localization gãy = chỉ có key hiện** — Nếu YAML sai, người chơi thấy `dvf_france.1.t` thay vì "French Warships Bombard Tourane". Test bằng cách chơi thật, không chỉ đọc file.

---

**Cập nhật lần cuối:** 2026-09-12 (Claude Opus 4.7 review pass).
