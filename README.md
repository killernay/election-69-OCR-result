# election-69-OCR-result

Official 2026 Thai election results from the Election Commission of Thailand (กกต.), OCR-extracted from official Form สส.6/1 PDF announcements and structured as machine-readable JSON.

ผลคะแนนเลือกตั้ง 2569 อย่างเป็นทางการ แปลงจากแบบ สส.6/1 ที่ กกต. เผยแพร่เป็น PDF ให้อยู่ในรูปแบบ JSON

---

## ⚠️ Disclaimer

This dataset is produced through OCR processing with multi-model cross-validation using Google Cloud Vision API, Claude, Gemini, and other OCR engines and LLMs to ensure accuracy before publishing. We do not alter, modify, or manipulate any election data in any way.

This is an independent volunteer civic effort to help digitize official election results published by the Election Commission of Thailand (กกต.), which we believe may lack sufficient resources to do so at scale. All processing costs are self-funded by the author personally — this project has no affiliation with any business, political party, or civic organization whatsoever.

For official and authoritative results, please always refer to the original documents from กกต.

## ⚠️ ข้อสงวนสิทธิ์

ข้อมูลชุดนี้ถูกสร้างจากการอ่าน OCR โดยผ่านการตรวจสอบความถูกต้องข้ามระบบ (cross-validation) ด้วย Google Cloud Vision API, Claude, Gemini และ OCR engine และ LLM อื่นๆ เพื่อความแม่นยำก่อนเผยแพร่ เราไม่มีส่วนเกี่ยวข้องในการแก้ไข ดัดแปลง หรือบิดเบือนข้อมูลผลการเลือกตั้งใดๆ ทั้งสิ้น

โครงการนี้จัดทำขึ้นโดยสมัครใจเพื่อช่วย กกต. ในการ digitize ผลการเลือกตั้งที่เผยแพร่อย่างเป็นทางการ ซึ่งเราเชื่อว่า กกต. อาจมีทรัพยากรไม่เพียงพอในการดำเนินการด้วยตนเอง ค่าใช้จ่ายในการประมวลผลทั้งหมดเป็นทุนส่วนตัวของผู้จัดทำ — โครงการนี้ไม่มีความเกี่ยวข้องกับธุรกิจ พรรคการเมือง หรือองค์กรภาคประชาสังคมใดๆ ทั้งสิ้น

สำหรับผลการเลือกตั้งที่เป็นทางการ กรุณาอ้างอิงจากเอกสารต้นฉบับของ กกต. เสมอ

---

## 📊 Data Coverage / ความครอบคลุมของข้อมูล

ประมวลผลจาก **776 PDF scans** (แบบ สส.6/1) จาก กกต. → OCR → JSON **~800 files**

|  | สส.เขต (Constituency) | บัญชีรายชื่อ (Party List) |
|---|---|---|
| **เขตที่นำเข้าแล้ว** | 377 / 400 (94.3%) | 386 / 400 (96.5%) |
| **จังหวัด** | 76 | 76 |

### ตัวเลขสำคัญ — แบบแบ่งเขต (Constituency)

| รายการ | จำนวน |
|--------|-------|
| คะแนนรวมที่ถูกต้อง (valid votes) | 32,949,094 |
| ผู้มีสิทธิเลือกตั้ง (eligible voters) | 49,925,837 |
| บัตรเสีย (invalid votes) | 1,265,063 |
| ไม่เลือกผู้สมัครผู้ใด (no votes) | 1,520,450 |

### ตัวเลขสำคัญ — แบบบัญชีรายชื่อ (Party List) Top 5

| พรรค | คะแนน |
|------|-------|
| ประชาชน | 10,715,927 |
| ภูมิใจไทย | 5,967,124 |
| เพื่อไทย | 5,376,290 |
| ประชาธิปัตย์ | 3,910,896 |
| เศรษฐกิจ | 1,109,392 |
| **รวมทุกพรรค** | **33,903,675** |

---

## 📂 Data Structure / โครงสร้างข้อมูล

```
data/
├── csv/                            # CSV รวม — เปิดได้ด้วย Excel / Google Sheets
│   ├── constituency.csv            # ผลแบบแบ่งเขต ทุกผู้สมัคร (3,380 rows)
│   ├── party_list.csv              # ผลแบบบัญชีรายชื่อ ทุกพรรค (22,006 rows)
│   └── summary_winners.csv        # สรุปผู้ชนะแบบแบ่งเขต (387 rows)
├── matched/                        # JSON ที่ผ่าน validation + matched กับฐานข้อมูลผู้สมัคร
│   ├── constituency/               # แบบแบ่งเขต (377 files)
│   ├── party_list/                 # แบบบัญชีรายชื่อ (386 files)
│   ├── issues.json                 # รายการปัญหาที่พบ
│   └── validation_report.json      # สรุปผลการตรวจสอบ
└── ocr-output/                     # JSON ดิบจาก OCR (ครบกว่า matched)
    ├── constituency/               # แบบแบ่งเขต (387 files)
    └── party_list/                 # แบบบัญชีรายชื่อ (386 files)
```

### CSV Files (สำหรับเปิดด้วย Excel / Google Sheets)

| ไฟล์ | คำอธิบาย | คอลัมน์ |
|------|----------|---------|
| `constituency.csv` | ผลคะแนนแบบแบ่งเขต ทุกผู้สมัคร | จังหวัด, เขต, หมายเลข, ชื่อผู้สมัคร, พรรค, คะแนน |
| `party_list.csv` | ผลคะแนนแบบบัญชีรายชื่อ ทุกพรรค | จังหวัด, เขต, หมายเลข, พรรค, คะแนน |
| `summary_winners.csv` | สรุปผู้ชนะแบบแบ่งเขต | จังหวัด, เขต, ผู้ชนะ, พรรค, คะแนน, คะแนนรวมทั้งเขต |

### Matched JSON (แนะนำสำหรับนักพัฒนา)

ข้อมูลที่ผ่านการ validate และ match กับฐานข้อมูลผู้สมัครแล้ว มีข้อมูลเพิ่มเติม:

- `province_code` — รหัสจังหวัด
- `summary` — สรุปภาพรวม (eligible_voters, good_votes, invalid_votes, ฯลฯ)
- `matched_candidates` — ผู้สมัครที่ match ได้พร้อม `candidate_uuid`
- `unmatched_candidates` — ผู้สมัครที่ match ไม่ได้
- `issues.json` — รายการปัญหาที่พบระหว่าง validation
- `validation_report.json` — สรุปผลการตรวจสอบทั้งหมด

> ไฟล์ matched น้อยกว่า raw เล็กน้อย (763 vs 773) เพราะบางเขต match กับฐานข้อมูลไม่สำเร็จ

### Raw OCR JSON (ข้อมูลดิบ)

- **ocr-output/constituency/** — ผลคะแนนแบบแบ่งเขตเลือกตั้ง (387 files)
- **ocr-output/party_list/** — ผลคะแนนแบบบัญชีรายชื่อ (386 files)

---

## 🚫 Incomplete Data / ข้อมูลที่ยังไม่ครบถ้วน

### กกต. ยังไม่ประกาศผลอย่างเป็นทางการ (Not yet officially announced by ECT)

ตามประกาศ กกต. ประจำเขตเลือกตั้ง ผลการนับคะแนน **ยกเว้น** 3 เขตต่อไปนี้:

| จังหวัด | เขต | สถานะ |
|---------|------|--------|
| กรุงเทพมหานคร | เขตเลือกตั้งที่ 15 | กกต. ยังไม่ประกาศผล |
| น่าน | เขตเลือกตั้งที่ 1 | กกต. ยังไม่ประกาศผล |
| อุดรธานี | เขตเลือกตั้งที่ 6 | กกต. ยังไม่ประกาศผล |

> ดูประกาศต้นฉบับ: [`assets/ect-announcement.jpeg`](assets/ect-announcement.jpeg)

### เขตที่ขาดหาย (Missing Areas)

**สส.เขต (Constituency)** — ขาด 23 เขต | **บัญชีรายชื่อ (Party List)** — ขาด 14 เขต

| จังหวัด | เขตที่ขาด | หมายเหตุ |
|---------|----------|----------|
| บุรีรัมย์ (31) | ทั้ง 10 เขต | ไม่มี PDF จาก กกต. |
| กรุงเทพมหานคร (10) | เขต 15 | กกต. ยังไม่ประกาศ |
| ชัยภูมิ (11) | เขต 6, 8 | |
| ตราด (16) | เขต 4 | |
| นครพนม (20) | เขต 8 | |
| นราธิวาส (25) | เขต 2 | |
| ปัตตานี (32) | เขต 6 | |
| พระนครศรีอยุธยา (33) | เขต 8 | |
| แพร่ (41) | เขต 8 | |
| มุกดาหาร (44) | เขต 6 | |
| เชียงใหม่ (50) | เขต 8 | |
| น่าน (55) | เขต 1 | กกต. ยังไม่ประกาศ |
| สกลนคร (57) | เขต 6 | |
| สงขลา (90) | เขต 6 | |
| เพชรบูรณ์ (40) | เขต 7 | |
| แม่ฮ่องสอน (45) | เขต 6 | |
| ยะลา (47) | เขต 6 | |
| สมุทรปราการ (60) | เขต 6 | |

---

## 📅 Timeline

| วันที่ | เวลา | เหตุการณ์ |
|-------|------|----------|
| 2026-02-08 (8 ก.พ. 69) | — | วันเลือกตั้ง สส. 2569 |
| 2026-02-20 (20 ก.พ. 69) | — | กกต. ประกาศผลการนับคะแนนอย่างเป็นทางการ (แบบ สส.6/1) ยกเว้น 3 เขต: กทม.15, น่าน 1, อุดรธานี 6 |
| 2026-02-20 (20 ก.พ. 69) | — | เริ่มประมวลผล OCR จาก 776 PDF scans |
| 2026-02-20 (20 ก.พ. 69) | — | นำเข้าข้อมูล matched: สส.เขต 377/400 (94.3%), บัญชีรายชื่อ 386/400 (96.5%) |

> Timeline จะอัปเดตเมื่อ กกต. ประกาศผลเพิ่มเติม หรือเมื่อข้อมูลได้รับการแก้ไข

---

## 📌 Attribution / การอ้างอิง

If you use this dataset, please credit:

**ชานนท์ เงินทองดี (Chanon Ngernthongdee)**

or link back to this repository: [election-69-OCR-result](https://github.com/killernay/election-69-OCR-result)

หากนำข้อมูลชุดนี้ไปใช้ กรุณาให้เครดิต **นายชานนท์ เงินทองดี** หรืออ้างอิงกลับมาที่ repository นี้

---

## 🐛 Found an Error? / พบข้อผิดพลาด?

If you find any inaccuracies in the data, please report via:

**Twitter/X:** [@killernay](https://x.com/killernay)

หากพบข้อผิดพลาดในข้อมูล สามารถแจ้งได้ที่ [@killernay](https://x.com/killernay) บน Twitter/X — หากว่างจะรีบตรวจสอบและแก้ไขทันที

---

## 📄 Data Source / แหล่งข้อมูลต้นฉบับ

- แบบ สส.6/1 จากสำนักงานคณะกรรมการการเลือกตั้ง (กกต.)
- [https://www.ect.go.th](https://www.ect.go.th)

![ประกาศ กกต.](assets/ect-announcement.jpeg)

## 🛠️ Processing Pipeline

```
776 PDF scans (กกต.)
    │
    ▼
┌──────────────────┐     ┌──────────────────────┐
│  Gemini Vision   │     │  ฐานข้อมูลอ้างอิง      │
│  OCR + LLM       │     │  - อาสาสมัครวันเลือกตั้ง │
│  (หลายระบบ)       │     │  - เว็บไม่เป็นทางการ กกต. │
└────────┬─────────┘     └───────────┬──────────┘
         │                           │
         ▼                           │
┌──────────────────┐                 │
│  Cross-validation │                 │
│  ระหว่าง OCR/LLM  │◄────────────────┘
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│  Validate + Match │
│  Candidate UUIDs  │
└────────┬─────────┘
         │
         ▼
   JSON + CSV output
   (raw + matched)
```

1. **Source** — 776 PDF scans (แบบ สส.6/1) จาก กกต. ซึ่งเป็นเอกสารที่อ่านยากและจัดการได้ลำบาก
2. **OCR + LLM** — ประมวลผลด้วยหลายระบบ: Google Cloud Vision API, Claude, Gemini และ OCR engine/LLM อื่นๆ
3. **Cross-validation** — เปรียบเทียบผลข้ามระบบ OCR/LLM + เทียบกับฐานข้อมูลอาสาสมัครวันเลือกตั้ง และเว็บไม่เป็นทางการของ กกต.
4. **Validate + Match** — จับคู่ผู้สมัครกับฐานข้อมูล พร้อมระบุ `candidate_uuid` และรายงานปัญหาที่พบ
5. **Output** — JSON (raw ~800 files + matched ~763 files) และ CSV

## 📜 License

This data is derived from publicly available official government documents. The structured JSON output is provided freely for public use. Please attribute as noted above.
