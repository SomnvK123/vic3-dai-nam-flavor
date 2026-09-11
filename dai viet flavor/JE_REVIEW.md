# Thẩm Định Chi Tiết Journal Entries Của Mod

> **Mục đích:** Review từng JE trong `common/journal_entries/`, chấm điểm, chỉ chỗ sai/thiếu, đề xuất cải tiến hoặc loại bỏ. Đối chiếu chéo với ~40 JE trong mod tham chiếu JoI/3219 (mod đã chạy ổn định lâu dài).
>
> **Tình trạng file:** 4 JE (550 dòng tổng cộng).

---

## Bảng Xếp Hạng Nhanh

| JE | File | Điểm | Kết Luận |
|---|---|---|---|
| `je_dsk_dai_cambodia` | `dsk_dai_cambodia.txt` | 8/10 | **Tốt.** Là JE cân bằng nhất — có progress bar, có 2 nhánh thắng/thua, có JE mirror bên Xiêm. Chỉ vài lỗi nhỏ. |
| `je_dsk_sia_cambodia` | (cùng file trên) | 6/10 | **Ổn nhưng thụ động.** JE mirror bên SIA đọc trạng thái từ DAI — không có agency cho AI/player Xiêm. |
| `je_dvf_hong_bao_coup` | `dvf_hong_bao_coup_je.txt` | 7/10 | **Cấu trúc chuẩn.** Progress bar 0-5 hợp lý. Vài chỗ trigger có thể mượt hơn. |
| `je_dvf_hong_bao_restoration` | `dvf_hong_bao_restoration_je.txt` | 6/10 | **Đầy tham vọng nhưng nặng nề.** 6 trụ cột đòi hỏi 250-300 building level. Đã thêm milestone bronze/silver nhưng vẫn cần tinh chỉnh. |
| `je_dvf_self_strengthening` | `dvf_opium_war_je.txt` | 4/10 | **CHỒNG CHÉO nghiêm trọng với JE Canh Tân.** Cả hai đều bắt xây arms industry + shipyard. Cần refactor gộp hoặc phân định. |

---

## Phần A. Đánh Giá Từng JE

### A.1. `je_dsk_dai_cambodia` — Trấn Tây Thành (điểm 8/10)

**Đánh giá lịch sử:** Chính xác đến từng chi tiết. Vua Minh Mạng sáp nhập Cao Miên thành Trấn Tây Thành năm 1834-1835, dựng chính sách "Việt hóa" quá cứng gây khởi nghĩa Khmer 1840-1841 dưới thời Thiệu Trị, phải rút quân năm 1841 sau thất bại của tướng Trương Minh Giảng. Xiêm La (thời Rama III) lợi dụng đưa vua Ang Duong lên ngôi năm 1846 → Cao Miên trở thành đồng chư hầu Xiêm-Việt.

**Điểm mạnh:**
- ✅ Có progress bar (scripted_progress_bar) với hai đầu win/lose rõ ràng
- ✅ Có JE mirror bên Xiêm — tương tác giữa 2 country
- ✅ `on_fail` gọi `create_country { tag = CAM ... }` — mô hình đúng cách để "khôi phục" CAM khi DAI thua (đây là cách vanilla Vic3 handle secession)
- ✅ Set global variable `dsk_cambodia_resolved` chặn JE không tái kích hoạt
- ✅ Xét đủ 3 trường hợp: CAM là vassal của DAI / CAM không tồn tại / CAM khôi phục sau khi DAI thất bại

**Vấn đề:**
1. ⚠️ **`is_shown_when_inactive` và `possible` giống hệt nhau** — điều này có nghĩa JE **luôn active** ngay khi DAI+CAM đủ điều kiện, không bao giờ hiện ra ở panel "inactive". Sửa: `is_shown_when_inactive` nên rộng hơn `possible` (ví dụ chỉ cần `c:DAI = this`, không cần check subject state).
2. ⚠️ **Hardcode province ID trong `on_fail`**: dùng danh sách 16 province ID `x36D7BA xDF21D5 ...` để `set_owner_of_provinces`. Nếu Paradox hoặc mod 3219 đổi hash province thì logic hỏng ngay. Cách an toàn hơn: dùng `every_scope_state` iterate state region CAMBODIA và transfer từng state.
3. ⚠️ **Fail condition dùng `has_state_in_state_region = STATE_CAMBODIA`** ở dòng 72 — trigger này hợp lệ (đã verify) nhưng ngữ nghĩa hơi lạ: nó fail khi DAI **KHÔNG** có state Cambodia. Với alt-history mod Hồng Bảo, có thể muốn DAI cede Cambodia cho SIA vẫn giữ đất khác → fail này lỏng hợp lý.
4. ⚠️ **Không có `timeout`** — nếu progress bar cứ đứng yên ở 50 mãi (không có event push lên/xuống đủ), JE treo vô hạn. Đề xuất thêm `timeout = 3650` (10 năm ≈ khung lịch sử 1836-1846 khi Xiêm rút).
5. ⚠️ **`events = {...}` block trong `on_monthly_pulse` fire event 20/21/22/23** — không có trong file event nào tôi thấy. Cần verify các event này thực sự tồn tại.

**Đề xuất cải tiến:**
- Đổi `is_shown_when_inactive` thành `c:DAI ?= this` (đơn giản, chỉ để giới thiệu JE cho người chơi trước khi đủ điều kiện).
- Refactor `on_fail` dùng iterate state region thay vì hardcode province.
- Thêm `timeout = 3650` để tránh treo.
- Verify sự tồn tại của `dsk_dai_cambodia_events.{20,21,22,23}`.

---

### A.2. `je_dsk_sia_cambodia` — Xiêm La Chờ Đợi (điểm 6/10)

**Đánh giá lịch sử:** Hợp lý — Xiêm La quan sát Đại Nam vật lộn với Trấn Tây Thành. Nhưng lịch sử Xiêm chủ động hơn nhiều so với JE này: Rama III cử tướng Bodindecha 3 chiến dịch vào Cao Miên 1834-1841, không chỉ "chờ".

**Điểm mạnh:**
- ✅ Đối xứng với JE của DAI qua biến `dsk_cambodia_dai_won`
- ✅ Không phá vỡ AI vanilla — chỉ đọc, không ép SIA làm gì

**Vấn đề:**
1. ⚠️ **JE thụ động hoàn toàn** — SIA không có option, không có action, chỉ **quan sát** kết quả của JE bên DAI. Người chơi Xiêm nhận JE này chỉ để nhận vài prestige khi DAI thua. Đây là **JE trang trí**, không phải JE gameplay.
2. ⚠️ **Không có `on_monthly_pulse`** — không có event nào push tiến trình, không có gợi ý người chơi Xiêm nên can thiệp.
3. ⚠️ **Không phản ánh chiến dịch Bodindecha lịch sử** — Xiêm thực tế đưa quân sang Cao Miên chứ không chỉ ngồi chờ.

**Đề xuất:**
- **Option A (giữ nhẹ):** Coi đây là "narrative JE" cho SIA, thêm 1-2 event flavor về Rama III bàn với Bodindecha, +5 prestige nếu SIA khai chiến hỗ trợ Khmer.
- **Option B (biến thành active JE):** Thêm decision "Cử Bodindecha viễn chinh" khi Xiêm là player — khai chiến vào DAI để "giải phóng" Cao Miên. Nhưng option B xâm phạm AI của SIA và có thể phá compat với mod 3219 nếu 3219 có JE riêng cho SIA.
- **Option C (loại bỏ):** Nếu chỉ để +15 prestige khi DAI thua, có thể xóa và cho SIA nhận reward qua event thay vì JE riêng. Đỡ 1 slot JE cho AI Xiêm.

**Khuyến nghị của tôi:** Option A — giữ nhẹ như narrative. JE bên DAI đã đủ nặng, không cần JE mirror phức tạp.

---

### A.3. `je_dvf_hong_bao_coup` — Âm Mưu An Phong (điểm 7/10)

**Đánh giá lịch sử:** Đúng bối cảnh nhưng có thể sâu hơn. Hồng Bảo là con trưởng của Thiệu Trị, bị Trương Đăng Quế soạn di chiếu bỏ qua để đưa Hồng Nhậm (Tự Đức, con thứ) lên ngôi năm 1847. Hồng Bảo âm mưu 1851-1854, liên lạc với giáo sĩ Pellerin, bị lộ và tự vẫn trong ngục 1854. Progress bar 0-5 là mô hình gọn nhẹ, chấp nhận được.

**Điểm mạnh:**
- ✅ Cấu trúc progress bar chuẩn Vic3: `current_value` + `goal_add_value` + `progressbar = yes` — verify khớp với `00_autocracy.txt` của Vic3 base.
- ✅ Init `dvf_hong_bao_coup_progress = 1` (không phải 0) để tránh fail sớm — chú thích comment ghi rõ lý do, rất tốt.
- ✅ Fail condition thông minh: có 2 lối fail (Hồng Bảo chết / tiến trình về 0).
- ✅ `weight = 1000` + `should_be_pinned_by_default = yes` — đảm bảo JE hiện rõ với người chơi.
- ✅ Trigger event giới thiệu `dvf_hong_bao.1` qua guard `dvf_hong_bao_intro_fired` — không lặp.

**Vấn đề:**
1. ⚠️ **`is_shown_when_inactive` và `possible` lại giống hệt nhau** — cùng lỗi với JE Cambodia. Người chơi sẽ không thấy JE ở tab "Available" trước khi đủ điều kiện. Đề xuất `is_shown_when_inactive` chỉ cần `c:DAI ?= this` + `NOT = { has_global_variable = dvf_hong_bao_coup_resolved }`.
2. ⚠️ **Không có kết cục compromise (thoả hiệp)** — như đã đề xuất trong `HISTORICAL_REVIEW.md` Mục C.2. Chỉ có win/lose ở 5/5 hoặc 0/5. Thực tế lịch sử có nhiều khả năng trung gian: Hồng Bảo được ân xá, làm phó vương, hoặc bị đày ra Bắc.
3. ⚠️ **Không có `timeout`** — nếu vì lý do nào đó cả 2 event random `.2/.3` không fire (chỉ có 50/50 trên 200 mỗi tháng ≈ mất 4 tháng để có 1 event), JE có thể treo nhiều thập kỷ. Đề xuất `timeout = 3650` (10 năm — sau đó JE tự fail nếu không resolve).
4. ⚠️ **`on_fail` chỉ trigger event `dvf_hong_bao.5`, không set fail flag rõ** — nếu Hồng Bảo chết trong khi player tránh Tự Đức chết trước, sau đó Tự Đức chết → JE trigger lại? Kiểm tra: `dvf_hong_bao_coup_resolved` được set, nên JE `possible` sẽ false → OK, không lặp. Nhưng nếu sau reload/`console reload`, biến này có thể bị reset. Rủi ro nhỏ.
5. ⚠️ **Chỉ 2 event random trong `on_monthly_pulse`** (`.2/.3`) — cả hai có weight 50, tổng non-event weight 200. Nghĩa là mỗi tháng có ~33% event xảy ra. Cần **nhiều event random hơn** để chuỗi giằng co có cảm giác đa dạng.

**Đề xuất cải tiến:**
- Thêm `timeout = 3650` (10 năm, tương ứng lịch sử 1847-1854).
- Tách `is_shown_when_inactive` cho rộng hơn.
- Thêm 2-3 event random giằng co nữa (VD: Trương Đăng Quế phát giác một phần âm mưu, giáo sĩ Pellerin bị bắt, tướng lĩnh Bắc Kỳ ngả về phe nào).
- Thêm decision "Ân xá Hồng Bảo" (đã đề xuất trong `HISTORICAL_REVIEW.md`) để mở kết cục compromise ở tiến trình 2-3/5.

---

### A.4. `je_dvf_hong_bao_restoration` — Canh Tân Đất Nước (điểm 6/10)

**Đánh giá lịch sử:** Ý tưởng đúng — mô phỏng Minh Trị Duy Tân cho Đại Nam. Nhưng **quy mô yêu cầu vượt xa** khả năng thực tế của Đại Nam giai đoạn 1848-1900 (kể cả alt-history).

**Điểm mạnh:**
- ✅ Cấu trúc 6 trụ cột qua scripted_trigger (`dvf_pillar_N_done`) — modular, dễ tinh chỉnh
- ✅ Vừa mới thêm milestone Bronze/Silver (2/6, 4/6) — người chơi thấy phần thưởng sớm
- ✅ On_monthly_pulse có cả `effect` (check milestone) và `random_events` (character/flavor events)
- ✅ `on_complete` xóa modifier tạm và thay bằng vĩnh viễn — logic sạch
- ✅ Fail condition rõ: mất core state hoặc Hồng Bảo chết

**Vấn đề:**
1. ⚠️ **Fail khi ruler đổi** (`NOT = { ruler ?= { has_template = DAI_hong_bao } }`) — Hồng Bảo sinh 1825, nếu ông sống 60 năm thì chết ~1885. JE Canh Tân có thể mất 30-50 năm mới xong nếu chơi kỹ. → **Xác suất cao là Hồng Bảo chết vì tuổi già trước khi JE hoàn thành, JE fail sạch**, mất toàn bộ tiến trình. Đây là bug thiết kế nghiêm trọng.
   - **Sửa:** Thêm điều kiện fallback — nếu Hồng Bảo chết mà JE đã đạt ≥ 4/6 trụ cột (silver milestone), người kế vị (có thể là con Hồng Bảo, hoặc Kiên Thái Vương) tiếp tục JE với debuff nhỏ. Chỉ fail hoàn toàn khi đạt < 2/6 khi ông chết.
2. ⚠️ **`is_shown_when_inactive` và `possible` gần như trùng nhau** — cùng lỗi các JE khác. `is_shown_when_inactive` nên bỏ điều kiện `ruler ?= { has_template = DAI_hong_bao }` để JE hiện ra trong panel Available trước khi đảo chính (giới thiệu người chơi biết có option này).
3. ⚠️ **Không có `timeout`** — nếu JE stuck ở 3/6 trụ cột và Hồng Bảo còn sống, JE chạy vô hạn. Đề xuất `timeout = 18250` (50 năm).
4. ⚠️ **`weight = 1000` cho một JE khổng lồ** — hợp lý, nhưng nên có `weight = 5000` để nhất định ưu tiên vẽ trên UI.
5. ⚠️ **Random events weight quá cao** — 20+20+20+20+10+10+10+10+10+8+4 = 142/342 ≈ 41% event mỗi tháng. Có thể spam. Đề xuất tăng `no-event weight` từ 200 lên 400.
6. ⚠️ **6 trụ cột yêu cầu quá nặng** (~250-300 building levels tổng) — đã ghi trong `HISTORICAL_REVIEW.md`. Vẫn cần playtest để chỉnh xuống.
7. ⚠️ **Không có `desc`/`reason`/`event_outcome_completed_desc`** — thiếu localization keys, JE sẽ hiển thị tooltip auto-generated xấu. Cần thêm và viết localization.

**Đề xuất cải tiến:**
- Refactor fail condition với ruler-death fallback (mô tả ở #1).
- Thêm `timeout = 18250`.
- Rộng hóa `is_shown_when_inactive`.
- Giảm event spam (200→400 no-event weight).
- Thêm `desc`, `reason`, `event_outcome_completed_desc`, `event_outcome_failed_desc` fields để tooltip đẹp.
- Playtest và giảm building level requirement nếu vẫn quá khó.

---

### A.5. `je_dvf_self_strengthening` — Đầu Tư Quân Sự (điểm 4/10)

**Đánh giá lịch sử:** Ý tưởng đúng — mô phỏng phản ứng của Đại Nam sau cú sốc Nam Kinh 1842. Nhưng **thiết kế bị lỗi cấu trúc nghiêm trọng**.

**Điểm mạnh:**
- ✅ Trigger dựa vào biến `dvf_opium_shock_happened` (được set trong event chain rõ ràng)
- ✅ Progress bar dùng scripted_value `dvf_military_investment_score` — pattern tốt
- ✅ `on_complete` xóa 4 debuff modifier — hồi phục quốc gia sau đầu tư
- ✅ Fail có deadline 1858 — phản ánh áp lực lịch sử

**Vấn đề nghiêm trọng:**

1. 🔴 **CHỒNG CHÉO HOÀN TOÀN VỚI `je_dvf_hong_bao_restoration`** — Đây là vấn đề lớn nhất.
   - Trụ cột 5 của JE Canh Tân yêu cầu: **≥6 arms industry, ≥3 shipyard, ≥3 munition, ≥40 barracks, ≥10 naval base** + đầy đủ 6 tech quân sự
   - JE Self-Strengthening yêu cầu: **5 arms industry, 2 shipyard** + 3 tech (percussion_cap, line_infantry, paddle_steamer)
   - Nếu người chơi chọn path Hồng Bảo, họ sẽ có **CẢ HAI JE cùng lúc**, cả hai đều bắt xây arms/shipyard. Người chơi làm 1 lần, cả 2 tick, gây cảm giác dư thừa và mất focus.
   - **Sửa:** Xem đề xuất Refactor ở phần cuối.

2. 🔴 **`possible` không check tag DAI**: chỉ `has_variable = dvf_opium_shock_happened` — về lý thuyết country nào có biến đó cũng nhận JE. Sửa: thêm `c:DAI ?= this` hoặc `tag = DAI`.

3. ⚠️ **Không có `is_shown_when_inactive`** — JE không xuất hiện ở "Available JEs" trước khi Cú sốc Nam Kinh xảy ra. Người chơi bất ngờ khi JE pop up.

4. ⚠️ **`on_monthly_pulse = { random_events = {} }` rỗng** — hook thừa. Xóa hoặc thêm event thật vào.

5. ⚠️ **Không có `timeout`** — nếu 1858 đến mà không đủ điều kiện, JE fail. Nhưng nếu 1858 chưa đến (game start 1836), JE có thể chạy 22 năm không có sự kiện. Hợp lý theo lịch sử nhưng nên thêm hook feedback.

6. ⚠️ **Không có `desc`/`reason`/`event_outcome_*_desc`** — tooltip xấu. Loc key `je_dvf_self_strengthening_desc` được reference nhưng chưa verify có tồn tại (đã thấy trong `dvf_opium_war_l_english.yml` — OK).

7. ⚠️ **`weight = 1000`** + `should_be_pinned_by_default = yes` — hợp lý nhưng conflict với JE Canh Tân (cùng weight 1000, cùng pinned). Giảm 1 trong 2.

**Đề xuất Refactor lớn:**

Có **3 lựa chọn** để giải quyết vấn đề chồng chéo #1:

**Option A — Gộp thành 1 JE 2-phase (khuyến nghị):**
- Xóa `je_dvf_self_strengthening`.
- Thay bằng phase mở đầu của `je_dvf_hong_bao_restoration` — hoặc tạo JE mới `je_dvf_pre_reform_survival` chạy trước JE Canh Tân, complete → unlock JE Canh Tân.
- Ưu điểm: mạch câu chuyện liên tục, không chồng chéo.
- Nhược điểm: người chơi không đảo chính Hồng Bảo cũng cần JE này → phải split logic.

**Option B — Phân định rõ 2 con đường (đơn giản):**
- Giữ 2 JE nhưng làm **mutually exclusive**:
  - `je_dvf_self_strengthening` chỉ active khi Tự Đức còn ruler (path lịch sử — cố cải cách trong khuôn khổ cũ).
  - `je_dvf_hong_bao_restoration` chỉ active khi Hồng Bảo là ruler (path alt-history — cải cách triệt để).
- Thêm điều kiện vào `possible` của Self-Strengthening: `ruler ?= { has_template = DAI_tu_duc }`
- Ưu điểm: 2 con đường rõ ràng.
- Nhược điểm: nếu đảo chính giữa chừng, JE Self-Strengthening biến mất mất tiến trình.

**Option C — Bỏ hẳn Self-Strengthening (mạnh tay):**
- Xóa JE và toàn bộ event chain phụ thuộc (`dvf_opium_war_events.3/.4`).
- Chuyển các event `dvf_opium_war_events.7/.8` (mua bản quyền súng / dự án tàu hơi nước) sang trigger từ event chain Opium chính, không cần JE.
- Ưu điểm: giảm complexity, tránh chồng chéo.
- Nhược điểm: mất một feature quan trọng cho path lịch sử (không đảo chính).

**Khuyến nghị:** Option B — đơn giản, ít rủi ro, giữ được cả 2 path. Chỉ cần thêm 1-2 dòng vào `possible`.

---

## Phần B. Vấn đề Cắt Ngang (Xuất Hiện Ở Nhiều JE)

### B.1. Lỗi `is_shown_when_inactive == possible` (3/4 JE)

**Xuất hiện ở:** `je_dsk_dai_cambodia`, `je_dvf_hong_bao_coup`, `je_dvf_hong_bao_restoration`.

**Vấn đề:** Khi 2 field này giống nhau, JE **không bao giờ hiện ở panel "Available"** (tab các JE chưa active). JE nhảy thẳng từ ẩn sang active. Người chơi mất trải nghiệm "biết trước có JE sắp mở khoá".

**Sửa mẫu:**
```
is_shown_when_inactive = {
    c:DAI ?= this   # Chỉ cần điều kiện quốc gia
    NOT = { has_global_variable = dvf_hong_bao_coup_resolved }
}

possible = {
    c:DAI ?= this
    ruler ?= { has_template = DAI_tu_duc }
    any_scope_character = { has_template = DAI_hong_bao is_agitator = yes }
    NOT = { has_global_variable = dvf_hong_bao_coup_resolved }
}
```

### B.2. Thiếu `timeout` (4/4 JE)

Không JE nào có `timeout`. Vic3 vanilla có JE dùng timeout (1095 ngày = 3 năm, 5475 = 15 năm, 9000 = 24.6 năm). Nếu JE stuck vô hạn, kéo dài đến 1936 game end mà không resolve, có thể gây save bloat.

**Đề xuất:**
- `je_dsk_dai_cambodia`: `timeout = 3650` (10 năm)
- `je_dvf_hong_bao_coup`: `timeout = 3650`
- `je_dvf_hong_bao_restoration`: `timeout = 18250` (50 năm)
- `je_dvf_self_strengthening`: đã có deadline 1858 trong fail — không cần timeout riêng

### B.3. Thiếu `desc` / `reason` / `event_outcome_*_desc` (3/4 JE)

Chỉ `je_dvf_self_strengthening` có `desc` và `reason`. 3 JE còn lại thiếu hoàn toàn → tooltip trong game sẽ hiển thị auto-generated (từ complete/fail conditions), thường xấu và khó hiểu.

**Đề xuất:** Thêm cả 4 field vào mỗi JE + tạo localization keys tương ứng.

### B.4. Thiếu `weight_map` hoặc cấu trúc ưu tiên

Tất cả 4 JE dùng `weight = 1000` (hoặc 500 với SIA). Nhưng Vic3 có thể có xung đột UI khi nhiều JE cùng weight 1000. Đề xuất phân cấp:
- JE `restoration` (JE lớn nhất): `weight = 5000`
- JE `coup`: `weight = 3000`
- JE `self_strengthening`: `weight = 2000`
- JE `dai_cambodia`: `weight = 2000`
- JE `sia_cambodia`: `weight = 500` (giữ)

### B.5. Không có JE cho path không đảo chính (Tự Đức)

Nếu người chơi **không** đảo chính Hồng Bảo, mod chỉ có 2 JE: Trấn Tây Thành + Self-Strengthening. Đây là **con đường lịch sử** nhưng thiếu content. Đề xuất thêm JE (đã ghi trong `HISTORICAL_REVIEW.md` Mục C.2):

- `je_dvf_xay_khiem_lang` — Xây Khiêm Lăng (1864)
- `je_dvf_binh_dinh_nam_ky` — Chống du kích Trương Định
- `je_dvf_can_vuong` — Chiếu Cần Vương (post-1885)

---

## Phần C. Loại Bỏ / Hợp Nhất

### C.1. Không có JE nào nên xóa hoàn toàn

Cả 4 JE đều có giá trị lịch sử/gameplay. Nhưng:

### C.2. `je_dvf_self_strengthening` cần refactor GẤP

Chọn 1 trong 3 option A/B/C ở Mục A.5. **Khuyến nghị Option B**.

### C.3. `je_dsk_sia_cambodia` cân nhắc downgrade

Nếu JE quá thụ động, cân nhắc:
- Xóa và thay bằng vài event flavor cho SIA khi DAI resolve JE Cambodia.
- Giảm weight từ 500 xuống 100 để không chiếm slot UI của SIA.

---

## Phần D. Đề Xuất Thêm JE Mới (Tổng Hợp)

Để mod có đủ content cho cả 2 path (Tự Đức lịch sử vs Hồng Bảo alt), cần thêm:

| # | JE | Trigger | Loại |
|---|---|---|---|
| 1 | `je_dvf_xay_khiem_lang` | 1864, ruler=Tự Đức | Path lịch sử — hard historical moment |
| 2 | `je_dvf_binh_dinh_nam_ky` | Sau 1859, DAI mất Nam Kỳ | Path lịch sử — dập du kích |
| 3 | `je_dvf_can_vuong` | Sau 1885, kinh thành mất | Path lịch sử — kháng chiến |
| 4 | `je_dvf_su_khac_qing` | Định kỳ 3 năm | Cả 2 path — triều cống Đại Thanh |
| 5 | `je_dvf_lu_lut_song_hong` | Random 1848/1856/1872 | Cả 2 path — thiên tai |
| 6 | `je_dvf_khoa_cu_cai_cach` | Có ig_intelligentsia >= 20% | Path Hồng Bảo — cải cách khoa cử |

Chi tiết thiết kế xem `HISTORICAL_REVIEW.md` Mục C.2.

---

## Phần E. Kết Luận & Lộ Trình

> **Cập nhật 2026-09-12 — Đã xử lý Bước 1-3.** Trước khi sửa, đã re-verify lại từng claim
> bằng cách đọc lại nguyên văn code (không sửa mù theo review cũ) — phát hiện nhận định
> "`is_shown_when_inactive == possible` ở 3/4 JE" trong bản review gốc **chỉ đúng cho
> `je_dvf_hong_bao_coup`**; 2 JE còn lại (`dsk_dai_cambodia`, `dvf_hong_bao_restoration`)
> thực ra đã đúng từ đầu (is_shown rộng hơn possible). Đã sửa đúng 1 chỗ, không đụng vào
> 2 chỗ không có bug.

**Bước 1 (Fix nhanh) — ĐÃ XONG:**
- [x] Sửa `is_shown_when_inactive` cho `je_dvf_hong_bao_coup` (JE duy nhất thực sự bị trùng)
- [x] Thêm `timeout` + `on_timeout` cho 3 JE (coup: 10 năm, dai_cambodia: 10 năm,
      restoration: 50 năm) — có `on_timeout` đi kèm để dọn dẹp, không chỉ có `timeout` trơ
- [x] Thêm `c:DAI ?= this` vào `possible` của Self-Strengthening (trước đây bất kỳ nước nào
      có biến `dvf_opium_shock_happened` cũng nhận JE)

**Bước 2 (Refactor) — ĐÃ XONG:**
- [x] Option B cho Self-Strengthening: thêm `ruler ?= { has_template = DAI_tu_duc }` vào
      `possible`, và `ruler ?= { has_template = DAI_hong_bao }` vào `invalid` (+ `on_invalid`
      dọn debuff) — JE này giờ CHỈ chạy trên path lịch sử, tự động nhường sang JE Canh Tân
      Trụ Cột 5 khi đảo chính thành công
- [x] Ruler-death fallback cho Restoration JE: chỉ fail vì đổi ruler khi tiến trình
      < 2/6 trụ cột (dùng `dvf_pillars_completed_count`); từ mốc Sơ Canh Tân trở lên,
      người kế vị tiếp tục chương trình
- [x] Weight phân cấp: restoration=5000, coup=3000, self_strengthening=2000,
      dai_cambodia=2000, sia_cambodia=500 (giữ nguyên)
- [x] Giảm event spam của Restoration JE: no-event weight 200→400

**Bước 3 (Bổ sung) — ĐÃ XONG:**
- [x] Verify toàn bộ event ids `dsk_dai_cambodia_events.{1-7,20,21,22,23}` — **đều tồn tại**,
      không cần xóa reference nào
- [x] Thêm `je_dsk_dai_cambodia_desc` + `je_dsk_sia_cambodia_desc` (trước đây thiếu hoàn toàn)
- [x] **Phát hiện + sửa lỗi ngoài kế hoạch:** `je_dvf_hong_bao_coup` và
      `je_dvf_hong_bao_restoration` mỗi cái có **2 định nghĩa trùng lặp** ở 2 file
      localization khác nhau (1 bản tiếng Việt, 1 bản tiếng Anh, key giống hệt) — do
      duplicate key nên bản nào load sau sẽ ghi đè, trộn lẫn ngôn ngữ trong cùng 1 tooltip.
      Đã gộp về 1 file (`dvf_journal_entries_l_english.yml`), xóa 2 block trùng, chuyển field
      còn thiếu (`_reason`, `_progress_desc`) sang bản giữ lại.
- [x] Sửa lỗi mã hoá ký tự lẫn (tiếng Hàn/Tây Ban Nha bị dính vào text tiếng Việt do lỗi
      encoding khi soạn trước đó): "truyền교 sĩ"→"truyền giáo sĩ", "싱가포"→"Singapore",
      "在此"→"chỉ trong", "derrotar"→"đánh bại", "Xô viết thực dân"→"làn sóng thực dân"
- [x] Xóa 1 hook chết: `on_monthly_pulse = { random_events = {} }` rỗng trong Self-Strengthening

**Bước 4 (Content mới, CHƯA làm — quyết định của người dùng):**
- [ ] Viết 6 JE mới trong bảng D
- [ ] Playtest và cân bằng lại yêu cầu 6 trụ cột (vẫn còn ~250-300 building level, xem
      `HISTORICAL_REVIEW.md` B.2)

---

**Ghi chú:** Đánh giá này chỉ về **cấu trúc JE**. Về nội dung lịch sử chi tiết của từng chuỗi event mà JE gọi tới, đã có `HISTORICAL_REVIEW.md`. Về bug logic và cân bằng, đã fix trong Ưu tiên 1-3 (xem checklist trong `HISTORICAL_REVIEW.md` Mục E).

**Cập nhật:** 2026-09-12 (Claude Opus 4.7 JE review pass).
