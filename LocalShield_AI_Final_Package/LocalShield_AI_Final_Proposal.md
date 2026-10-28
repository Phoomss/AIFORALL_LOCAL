# LocalShield AI — Final Idea Proposal

> **ชื่อโครงการ:** LocalShield AI  
> **คำอธิบาย:** AI-Assisted Community Relief Coordination & Local Economic Continuity  
> **Tagline:** Protect Communities. Keep Local Economies Moving.  
> **เวอร์ชันเอกสาร:** 2.1 · 28 ตุลาคม 2026  
> **สถานะผลิตภัณฑ์:** Concept + Interactive HTML Prototype (Synthetic Data Only)

## Contents

1. Executive Summary
2. Problem Statement
3. Proposed Solution
4. Fit to AI Product / Hackathon Directions
5. Novelty & Competitive Differentiation
6. Technical Architecture
7. Current MVP and Scope Boundaries
8. Impact, KPIs & Validation Plan
9. Sustainability & Viability
10. Safety, Privacy & Reliability
11. Three-minute Demo Script
12. Team & Responsibilities
13. Evidence Ledger and References
14. Appendices: user journeys, data policy, planning logic, API blueprint, controls, delivery, risks, glossary

## Executive Summary

เมื่อเกิดน้ำท่วมหรือเหตุที่ทำให้ถนนบางช่วงใช้การไม่ได้ ชุมชนอาจยังมีร้านค้าที่มีน้ำดื่ม อาหารแห้ง และของจำเป็น แต่ผู้ประสานงานต้องรวบรวมข้อมูลคำขอ สต็อกสินค้า สถานะถนน และผู้ขนส่งจากหลายช่องทาง LocalShield AI เสนอระบบช่วยประสานข้อมูลเหล่านี้เป็นแผนจัดสรรและจัดส่งที่ตรวจสอบเหตุผลได้ พร้อมให้ผู้รับผิดชอบตรวจและอนุมัติก่อนดำเนินการ

LocalShield AI ไม่ใช่เพียงแอปแจ้งเตือนน้ำท่วม และไม่ได้อ้างว่าพยากรณ์ระดับน้ำรายซอยหรือรับรองเส้นทางปลอดภัยได้ ระบบมุ่งแก้ช่วงต่อระหว่าง **รู้ว่ามีความเสี่ยง → รู้ว่าใครต้องการอะไร → รู้ว่าร้านไหนมีสินค้า → ตรวจข้อจำกัดเส้นทาง → เสนอแผน → ให้คนอนุมัติ → ติดตามผล**

**One-line pitch:** LocalShield AI turns community needs, local inventory and verified road constraints into explainable, human-approved relief allocation plans—so essential goods can keep moving when normal routes are disrupted.

**Core workflow:** `Risk Context → Needs → Inventory Matching → Route Replanning → Human Approval → Tracking & Learning`

### Decision requested

เอกสารนี้เสนอให้เห็นชอบการพัฒนา **MVP เพื่อทดสอบ workflow** ไม่ใช่การเปิดใช้ระบบ dispatch จริงในภาคสนามทันที โดยเป้าหมายของรอบถัดไปคือพิสูจน์ 3 ประเด็น: (1) ผู้ประสานงานเข้าใจและใช้แผนที่ระบบเสนอได้หรือไม่ (2) แผนเคารพข้อจำกัดสต็อกและถนนตามข้อมูลที่ป้อนหรือไม่ และ (3) ร้านค้า/ผู้ขนส่งยอมอัปเดตข้อมูลในความถี่ที่ workflow ต้องใช้หรือไม่

### Assumptions for the MVP

| สมมติฐาน | ผลต่อการออกแบบ | สิ่งที่ต้องยืนยันก่อน pilot |
|---|---|---|
| มีผู้ประสานงานที่มีสิทธิ์อนุมัติภารกิจ | ระบบออกแบบให้ทุกแผนอยู่ในสถานะร่างก่อนอนุมัติ | บทบาท ผู้อนุมัติสำรอง และเวลาตอบรับ |
| ร้านค้ายินยอมแจ้งสต็อกที่จัดสรรได้ | สต็อกในระบบคือ `allocatable stock` ไม่ใช่สต็อกรวมทั้งหมดของร้าน | ความถี่อัปเดตและวิธีแก้ไขข้อมูลผิดพลาด |
| สถานะถนนมาจากแหล่งที่ระบุได้ | routing ใช้เฉพาะข้อจำกัดที่บันทึกเป็นข้อมูลโครงสร้าง | ผู้ยืนยันสถานะถนน อายุข้อมูลสูงสุด และช่องทางรายงาน |
| การส่งจริงยังอยู่ภายใต้หน่วยงาน/ผู้ขนส่ง | MVP ไม่สั่งงานหรือชำระเงินอัตโนมัติ | SOP การรับมอบ การยืนยันส่งสำเร็จ และการรับผิดชอบ |

## 1. Problem Statement

### Problem hypothesis

ในเหตุฉุกเฉิน ข้อมูลที่จำเป็นต่อการจัดสรรสิ่งของอาจแยกอยู่ในรายงานภัยพิบัติ โทรศัพท์หรือแชตของชุมชน รายการสินค้าของร้านค้า และข้อมูลสภาพถนน ผู้ประสานงานจึงอาจต้องรวมข้อมูลด้วยตนเองและปรับแผนซ้ำเมื่อเงื่อนไขเปลี่ยนไป

นี่เป็น **สมมติฐานปัญหาที่ต้องตรวจสอบกับผู้ใช้จริง** ไม่ใช่ข้อสรุปจากการสัมภาษณ์หรือสถิติที่ทีมยืนยันแล้ว

### Target users

- **ผู้ใช้หลัก:** ผู้ประสานงานชุมชนหรือองค์กรท้องถิ่นที่รับคำขอ จัดลำดับ และอนุมัติภารกิจ
- **ผู้ใช้รอง 1:** ร้านค้า SME ที่ลงทะเบียนสินค้า สต็อก เวลาทำการ และสถานะความพร้อม
- **ผู้ใช้รอง 2:** ผู้ขนส่งหรืออาสาสมัครที่ได้รับมอบหมาย ซึ่งต้องเห็นข้อมูลจุดรับส่งและข้อจำกัดถนนที่มีแหล่งที่มา
- **ผู้ได้รับประโยชน์:** ประชาชนที่ต้องการสินค้าจำเป็นและเข้าถึงข้อมูลสถานะคำขอ

### Current workflow vs proposed workflow

| ขั้นตอน | กระบวนการที่อาจเกิดขึ้นในปัจจุบัน (ต้องยืนยัน) | LocalShield AI ที่เสนอ |
|---|---|---|
| รับข้อมูลเหตุ | ตรวจข้อมูลจากหลายแหล่ง | รวมเหตุการณ์พร้อม source, timestamp และสถานะข้อมูล |
| รับคำขอ | รวมข้อมูลจากโทรศัพท์/แชต/แบบฟอร์ม | จัดคำขอเป็นรายการที่ตรวจสอบและติดตามได้ |
| หาสินค้า | ติดต่อร้านค้าเพื่อถามสต็อก | ค้นหาสต็อกที่ลงทะเบียน พร้อมเวลาปรับปรุงล่าสุด |
| วางแผนขนส่ง | ประสานผู้ขนส่งและเส้นทางแยกกัน | คำนวณทางเลือกจากกราฟถนนจำลองและข้อจำกัดที่ระบุ |
| อนุมัติและติดตาม | สถานะอาจกระจายหลายช่องทาง | ผู้ประสานงานตรวจ/อนุมัติ และบันทึกสถานะภารกิจ |

## 2. Proposed Solution

LocalShield AI เป็น **AI-assisted coordination workspace** สำหรับการจัดสรรสินค้าจำเป็นในสถานการณ์ที่การเดินทางถูกรบกวน โดยแบ่งเป็นสามเสาหลักของผลิตภัณฑ์ (เป็นการจัดกรอบแนวคิดของทีม ไม่ใช่การยืนยันว่าเป็นชื่อ Track อย่างเป็นทางการของทุกการแข่งขัน)

### A. Community Resilience
- รับข้อมูลเหตุการณ์และความต้องการของชุมชน
- แสดงแหล่งที่มา เวลาที่อัปเดต และสถานะข้อมูล เช่น `OBSERVED`, `FORECAST`, `ESTIMATED`, `SIMULATED`
- ช่วยแปลงข้อมูลเป็นรายการสิ่งที่ต้องตรวจสอบหรือเตรียมพร้อม

### B. Adaptive Mobility & Relief Logistics
- แสดงสถานะถนนจากข้อมูลที่มีแหล่งที่มาและระดับการยืนยัน
- คำนวณเส้นทางใหม่เมื่อมีการยืนยันว่าถนนปิด โดยตัด edge ที่ปิดออกจากกราฟ
- แสดงเหตุผลของแผนและแจ้งเมื่อไม่มีเส้นทางที่เป็นไปได้ แทนการสร้างคำตอบที่ดูมั่นใจโดยไม่มีหลักฐาน

### C. Local SME Continuity
- ให้ร้านค้าที่เข้าร่วมลงทะเบียนประเภทสินค้า จำนวนคงเหลือ และเวลาปรับปรุงสต็อก
- จับคู่คำขอกับร้านค้าที่มีสินค้าและเข้าถึงได้ตามข้อจำกัดที่ทราบ
- แสดงมูลค่าการจัดซื้อจำลองและสถานะร้านค้าเพื่อใช้วางแผนฟื้นตัว โดยไม่เรียกมูลค่าจัดซื้อว่าเป็นกำไรหรือรายได้เพิ่มสุทธิ

### Workflow

1. ผู้ประสานงานเลือกเหตุการณ์หรือสร้างสถานการณ์จำลอง
2. ระบบแสดงคำขอสินค้าและระดับความสำคัญตามกฎที่เปิดเผยได้
3. ระบบค้นหาร้านค้าที่มีสต็อกเพียงพอ โดยพิจารณาความสดของข้อมูล
4. Routing engine คำนวณเส้นทางบนกราฟถนนและตัดถนนที่ถูกปิดออก
5. AI ช่วยสรุปเหตุผล ข้อจำกัด และข้อมูลที่ยังขาด; การคำนวณเชิงปริมาณทำด้วย logic ที่ตรวจสอบได้
6. ผู้มีอำนาจตรวจและอนุมัติแผนก่อนเริ่มภารกิจ
7. ผู้ประสานงานติดตามสถานะและตรวจ KPI หลังการดำเนินงาน

## 3. Fit to AI Product / Hackathon Directions

การจับคู่ด้านล่างเป็น **การตีความเพื่ออธิบายแนวคิด** ไม่ใช่การอ้างว่า LocalShield ผ่านการรับรองจากผู้จัด

- **AI-Native Products & Operations:** AI อยู่ใน workflow การตีความคำขอ สรุปบริบท อธิบายทางเลือก และประสานเครื่องมือ ไม่ใช่เพียงกล่องแชตแยกจากการทำงาน
- **Deep Domain AI:** โฟกัสโดเมนเฉพาะ คือการจัดสรรสิ่งของจำเป็นและการประสานโลจิสติกส์ชุมชนภายใต้ข้อจำกัดสต็อก ถนน และความน่าเชื่อถือของข้อมูล
- **Autonomous & Adaptive AI (ขอบเขตจำกัด):** ระบบปรับแผนเมื่อเงื่อนไขเปลี่ยน เช่น มีการปิดถนนใหม่ แต่ใน MVP จะเสนอแผนให้คนอนุมัติ ไม่สั่งจ่ายของหรือส่งผู้ขนส่งโดยอัตโนมัติ

หากใช้กับการแข่งขันที่มีหมวดธีมหมายเลข 6 (ชุมชนมีภูมิคุ้มกัน), 5 (การเดินทาง/เมืองอัจฉริยะ), 2 (SME/เศรษฐกิจท้องถิ่น) แนวคิดนี้สามารถนำเสนอเป็น **6 เป็นเป้าหมายหลัก → 5 เป็นกลไกสนับสนุน → 2 เป็นผลลัพธ์ทางเศรษฐกิจ** แต่ต้องตรวจชื่อหมวดและข้อกำหนดจากเอกสารของการแข่งขันนั้นโดยตรงก่อนส่ง

## 4. Novelty & Competitive Differentiation

LocalShield AI ไม่อ้างว่าไม่มีระบบอื่นจัดการภัยพิบัติ แผนที่ หรือการประสานทรัพยากรมาก่อน จุดที่ต้องการทดสอบคือการรวม **คำขอ + สต็อก SME + ข้อจำกัดถนน + การอนุมัติของมนุษย์ + การติดตามมูลค่าจัดซื้อในพื้นที่** ไว้ใน workflow เดียวที่ผู้ประสานงานใช้ตัดสินใจได้

| ระบบ/แนวทางอ้างอิง | สิ่งที่มีอยู่ | ช่องว่างที่ LocalShield จะทดลองตอบ (ยังไม่ใช่ข้อได้เปรียบที่พิสูจน์แล้ว) |
|---|---|---|
| GISTDA Disaster Open API | มีเอกสารบริการข้อมูลเชิงพื้นที่เกี่ยวกับน้ำท่วมและข้อมูลที่เกี่ยวข้อง | นำบริบทเหตุการณ์ไปเชื่อมกับคำขอ สต็อก และการวางแผนภารกิจ โดยไม่ตีความชั้นข้อมูลน้ำท่วมว่าเป็นการยืนยันว่าถนนปลอดภัย |
| Sahana Eden | ระบบโอเพนซอร์สด้านการจัดการภัยพิบัติและการประสานงาน | ทดลอง workflow ที่ให้ SME ท้องถิ่นเป็นแหล่งสินค้าพร้อมข้อมูลสต็อก และติดตาม local procurement |
| แอปแผนที่/จัดส่งทั่วไป | ช่วยนำทางหรือจัดส่งตามความสามารถของผู้ให้บริการ | LocalShield มุ่งจัดสรรสิ่งของและควบคุมขั้นอนุมัติภายใต้บริบทวิกฤต ไม่ใช่แทนแอปนำทางทั่วไป |

**ข้อจำกัด:** การเปรียบเทียบนี้เป็น desk research เบื้องต้น ไม่ใช่ benchmark ด้านประสิทธิภาพหรือฟีเจอร์แบบครบถ้วน ต้องทดสอบ workflow กับผู้ใช้งานจริงก่อนกล่าวอ้างความแตกต่างเชิงผลลัพธ์

## 5. Technical Architecture

```text
External / Community Inputs
  Weather & flood references · verified road reports · SME inventory · requests
                              ↓
                 Ingestion & Data Validation
      source · timestamp · freshness · verification · access policy
                              ↓
                    PostgreSQL + PostGIS
                              ↓
                     AI Orchestrator
       intent/context interpretation · tool selection · explanation
                              ↓
          Deterministic Planning & Optimization Layer
       inventory constraints · request matching · graph routing
                              ↓
                 Evidence / Safety Validation
                              ↓
                  Human Approval & Audit Log
                              ↓
             Dashboard · Mission Tracking · Analytics
```

### Proposed stack (not yet integrated in the prototype)

| Layer | Proposed technology | Responsibility |
|---|---|---|
| Web UI | Next.js / React | Coordinator dashboard and role-based screens |
| API | FastAPI | Data validation, planning endpoints and AI orchestration |
| Database | PostgreSQL + PostGIS | Requests, businesses, inventory, spatial entities and audit records |
| AI | OpenAI API or Amazon Bedrock (choose based on event constraints) | Interpret intent, summarize evidence, explain options |
| Optimization | Graph algorithm / OR-Tools / pgRouting | Constraint-aware matching and routing |
| Storage & Analytics | S3 / Amazon QuickSight (optional future integration) | Documents and aggregate reporting |
| Security | RBAC, least privilege, audit logs | Access control and accountability |

### Clear separation of responsibilities

- **LLM:** ตีความคำถาม สรุปหลักฐาน สร้างคำอธิบายและแผนร่าง; ต้องไม่แต่งข้อมูลที่ไม่มีในแหล่งอ้างอิง
- **Deterministic logic:** ตรวจจำนวนสินค้า จัดสรรตามข้อจำกัด และคำนวณเส้นทางจากกราฟ
- **Evidence gate:** ตรวจความสดของข้อมูลและสถานะการยืนยัน; หากข้อมูลไม่พอให้แสดงว่าไม่สามารถยืนยันได้
- **Human approval:** ผู้ประสานงานรับผิดชอบอนุมัติภารกิจจริง โดยเฉพาะกรณีที่มีความเสี่ยงสูง

## 6. Current MVP and Scope Boundaries

### What the current HTML prototype demonstrates
- Dashboard และข้อมูลร้านค้า/ผู้ขนส่ง/จุดชุมชนแบบจำลอง
- คำขอสินค้าจำเป็นและการจับคู่สต็อกอย่างง่าย
- กราฟถนนสังเคราะห์และการคำนวณแผนใหม่เมื่อปิดถนนที่กำหนด
- ปุ่มอนุมัติ/รีเซ็ตและ KPI จากข้อมูลจำลอง
- การแสดงผลในไฟล์ HTML แบบ standalone

### What it does not do
- ไม่เชื่อม API พยากรณ์อากาศ น้ำท่วม หรือจราจรจริง
- ไม่เรียก LLM จริงจาก HTML prototype
- ไม่ยืนยันความปลอดภัยของเส้นทางหรือความลึกน้ำ
- ไม่ได้ส่งคำสั่งให้ร้านค้าหรือผู้ขนส่งจริง
- ไม่ได้วัดเวลาประหยัด ต้นทุนที่ลดลง รายได้เพิ่ม หรือผลลัพธ์กับชุมชนจริง
- ยังไม่มี production authentication, database, cloud deployment หรือ Amazon QuickSight integration

### Synthetic demo setup

ตัวเลขใน Demo เช่น **15 ร้านค้า, 5 ผู้ขนส่ง และ 3 จุดชุมชน** เป็นข้อมูลสมมติสำหรับทดสอบ workflow เท่านั้น ไม่ใช่ขนาดพื้นที่นำร่องจริงหรือหลักฐานความพร้อมใช้งาน

## 7. Impact, KPIs & Validation Plan

| KPI | นิยาม/สูตร | วิธีตรวจสอบ | สถานะปัจจุบัน |
|---|---|---|---|
| Request fulfillment rate | คำขอที่จัดสรรได้ ÷ คำขอที่เข้าเกณฑ์ × 100 | ทดสอบหลาย scenario และตรวจผลด้วยมือ | ยังไม่มีผลทดสอบภาคสนาม |
| Planning time | เวลาตั้งแต่โหลดสถานการณ์จนแสดงแผน | เทียบ manual baseline กับ prototype ใน scenario เดียวกัน | ยังไม่ได้วัด |
| Replanning correctness | จำนวนเส้นทางที่ยังใช้ edge ที่ปิดอยู่ (เป้าหมาย 0) | Unit tests บน synthetic graph | มี test เบื้องต้น; ต้องรันทดสอบ browser/QA เพิ่ม |
| Local procurement value | จำนวนสินค้าที่จัดสรร × ราคาต่อหน่วยที่กำหนด | ตรวจรายการจัดสรรและหน่วยราคา | เป็นมูลค่าจำลอง ไม่ใช่รายได้เพิ่มสุทธิ |
| Inventory freshness | สัดส่วนรายการสต็อกที่อัปเดตภายในช่วงเวลาที่กำหนด | ตรวจ timestamp ตาม policy | ยังไม่มีข้อมูลร้านค้าจริง |
| User task success | สัดส่วนผู้ใช้ที่ทำ task สำเร็จโดยไม่ต้องช่วย | ทดสอบกับผู้ประสานงาน/ร้านค้า 3–5 ราย | ยังไม่ได้สัมภาษณ์/ทดสอบ |

### Pilot plan

1. สัมภาษณ์ผู้ประสานงานชุมชนและร้านค้า 3–5 รายเพื่อยืนยัน workflow และคำศัพท์
2. กำหนดพื้นที่จำลองหนึ่งแห่งและสร้าง test cases ที่ระบุ input/expected output
3. ทดสอบการจับคู่สินค้า เส้นทางปิด และกรณีที่ไม่มีแผนที่เป็นไปได้
4. เปรียบเทียบเวลาและความถูกต้องกับ baseline ที่ผู้ประสานงานทำด้วยมือ
5. หากจะทดลองภาคสนาม ต้องทำข้อตกลงเรื่องข้อมูล ความรับผิดชอบ และขั้นอนุมัติกับหน่วยงานที่เกี่ยวข้องก่อน

## 8. Sustainability & Viability

### Year-round value hypothesis

- **Normal:** ร้านค้าอัปเดตสต็อก ค้นหาสินค้า และใช้เครือข่ายขนส่งในพื้นที่
- **Crisis:** ผู้ประสานงานจัดสรรสิ่งของและติดตามภารกิจภายใต้ข้อจำกัด
- **Recovery:** ติดตามการกลับมาเปิดร้าน ความต้องการสินค้า และบทเรียนหลังเหตุการณ์

### Possible funding models to validate

- ค่าบริการซอฟต์แวร์สำหรับองค์กร/เครือข่ายผู้ประสานงาน
- บริการจัดการสต็อกและคำสั่งซื้อสำหรับร้านค้าที่เลือกใช้ฟีเจอร์เสริม
- งบสนับสนุนจากองค์กรท้องถิ่น ผู้สนับสนุน หรือโครงการเพื่อสังคม

สิ่งเหล่านี้เป็น **สมมติฐานทางธุรกิจ** ยังไม่มีการยืนยัน willingness-to-pay, unit economics หรือพันธมิตรที่ลงนามแล้ว ห้ามให้ความสำคัญกับคำขอช่วยเหลือตามความสามารถในการจ่าย และห้ามสื่อว่าระบบช่วยหลีกเลี่ยงกฎการจัดซื้อจัดจ้างภาครัฐ

## 9. Safety, Privacy & Reliability

- แยก `OBSERVED`, `FORECAST`, `ESTIMATED` และ `SIMULATED` อย่างเห็นได้ชัด พร้อมแหล่งที่มาและเวลาที่ข้อมูลอัปเดต
- ห้ามสร้างระดับน้ำที่รถแต่ละชนิดสามารถผ่านได้อย่างปลอดภัยจากตัวเลขทั่วไป และห้ามรับรองว่าเส้นทางปลอดภัย
- หากข้อมูลถนนเก่าหรือยังไม่ยืนยัน ให้แสดงข้อจำกัดและขอการตรวจสอบ ไม่ควรแนะนำให้ผู้ใช้เดินทางผ่านพื้นที่เสี่ยง
- ห้ามแสดงพิกัดบ้าน ชื่อ เบอร์โทร หรือข้อมูลสุขภาพของผู้เปราะบางใน Dashboard สาธารณะ
- ใช้สิทธิ์ตามบทบาท เก็บ audit log และจำกัดการเข้าถึงข้อมูลส่วนบุคคล
- การจัดลำดับคำขอควรมีเกณฑ์ที่โปร่งใส ตรวจสอบย้อนหลังได้ และมีช่องทางแก้ไขข้อมูล
- Prototype เป็นการจำลองการวางแผน ไม่ใช่ระบบ dispatch หรือคำแนะนำฉุกเฉินที่ผ่านการรับรอง

## 10. Three-minute Demo Script

| เวลา | สิ่งที่นำเสนอ | ข้อความหลัก |
|---|---|---|
| 0:00–0:25 | เปิดด้วยปัญหาถนนถูกปิดและข้อมูลไม่เชื่อมกัน | สินค้าอาจยังอยู่ในชุมชน แต่การประสานงานทำได้ยาก |
| 0:25–0:50 | เปิด Dashboard และระบุว่าเป็นข้อมูล SIMULATED | นี่คือ workspace สำหรับประสานคำขอ สต็อก และเส้นทาง |
| 0:50–1:20 | กดคำนวณแผนจัดสรร | ระบบจับคู่คำขอกับร้านค้าที่มีสินค้าตามข้อจำกัดจำลอง |
| 1:20–1:55 | ปิดถนน B–D แล้วคำนวณใหม่ | เมื่อข้อจำกัดเปลี่ยน ระบบคำนวณทางเลือกใหม่จากกราฟ ไม่ใช่ให้ LLM เดาเส้นทาง |
| 1:55–2:25 | แสดงเหตุผลและอนุมัติแผน | ผู้ประสานงานยังเป็นผู้ตัดสินใจก่อนดำเนินการ |
| 2:25–2:45 | เปิด KPI | ตัวเลขเป็นผลลัพธ์จำลอง ไม่ใช่ผลกระทบจริง |
| 2:45–3:00 | ปิดด้วยแผนทดสอบต่อไป | ขั้นต่อไปคือ validate กับผู้ใช้และทดสอบในพื้นที่นำร่องที่ได้รับอนุญาต |

## 11. Team & Responsibilities

| สมาชิก | บทบาทตามข้อมูลทีม | ความรับผิดชอบที่เสนอในโครงการ |
|---|---|---|
| นรงศ์ศักดิ์ | Full-Stack Developer · DevOps · AI Engineer | Technical integration, system architecture, deployment planning, AI/tool orchestration |
| เกตุศรัณย์ | Full-Stack Developer · AI Engineer | AI workflow, prompt/tool design, evaluation scenarios and output validation |
| วัชรากร | Full-Stack Developer · System Analyst | Requirements, user flows, data model, acceptance criteria and test cases |
| สมหมาย | Full-Stack Developer · Advanced Frontend | UI/UX implementation, responsive dashboard, interaction states and demo experience |
| รติมา | Business English | English proofreading, pitch wording, presentation language and communication support |

บทบาทความรับผิดชอบด้านโครงการเป็นข้อเสนอเพื่อแบ่งงาน ไม่ได้เพิ่มคุณวุฒิหรือประสบการณ์ที่ทีมไม่ได้ระบุไว้ และ **Business English ไม่ได้หมายถึง Business Engineer**

## 12. Evidence Ledger

| Claim | Status | Notes |
|---|---|---|
| LocalShield combines requests, SME stock, route constraints and approval in one workflow | Design proposal | Must validate with users |
| Demo uses 15 stores, 5 transporters and 3 community points | SIMULATED | Synthetic data only |
| Replanning changes after closing a synthetic road edge | Prototype behavior | Run manual browser test before presenting |
| AI model is connected to the HTML prototype | NOT IMPLEMENTED | Prototype uses deterministic JavaScript; no LLM API call |
| Live flood/road data is integrated | NOT IMPLEMENTED | External sources are references only |
| QuickSight dashboard is connected | NOT IMPLEMENTED | Future integration idea |
| Real-world impact or revenue increase has been measured | NOT VERIFIED | Requires pilot and baseline comparison |
| GISTDA provides public disaster data documentation | DOCUMENTATION REFERENCE | API access and actual integration have not been tested |

## 13. References

- GISTDA Disaster Open API documentation: https://disaster.gistda.or.th/v2/services/open-api
- Sahana Eden disaster management project: https://eden-legacy.sahanafoundation.org/
- Sea x OpenAI Regional Codex Hackathon Thailand event page (official event information and current rules): https://luma.com/39zve8ph

External references provide background only; they do not establish that LocalShield has access to those APIs or has been tested against the referenced systems.

## Appendix A. Detailed User Journeys and Operational States

### A.1 Coordinator journey: from incoming request to approved mission

1. **Create or select incident.** ผู้ประสานงานสร้างเหตุการณ์ กำหนดพื้นที่ เวลาเริ่มต้น และเลือกว่าข้อมูลใดเป็น `SIMULATED` หรือมาจากแหล่งภายนอก ระบบต้องบันทึกผู้สร้างและเวลาเสมอ
2. **Triage requests.** ผู้ประสานงานบันทึกหรือ import คำขอ โดยเห็นข้อมูลขั้นต่ำที่จำเป็นต่อการวางแผน เช่น จุดส่ง ประเภทสินค้า ปริมาณ กรอบเวลา และข้อสังเกตด้านการเข้าถึง ข้อมูลส่วนบุคคลละเอียดอ่อนต้องถูกซ่อนไว้ตามสิทธิ์
3. **Review data quality.** ก่อนสร้างแผน ระบบสรุปจำนวนคำขอที่ยังไม่ครบ รายการสต็อกที่เก่า และข้อจำกัดถนนที่หมดอายุ ผู้ใช้สามารถเลือกหยุดแผนหรือดำเนินการต่อโดยมีเหตุผลที่บันทึกไว้
4. **Generate draft plan.** ระบบประมวลผลตามกฎการจัดสรรและแสดงแต่ละ assignment พร้อมเหตุผล ต้นทาง ปลายทาง สินค้า จำนวน สถานะความสด และข้อจำกัดเส้นทางที่นำมาคิด
5. **Review exceptions.** คำขอที่ไม่มีสินค้าเพียงพอ ไม่มีผู้ขนส่ง หรือไม่มีเส้นทางที่ระบบคำนวณได้ จะอยู่ใน exception queue แยกชัดเจน ไม่ถูกทำให้ดูเหมือน “สำเร็จ”
6. **Approve or revise.** ผู้มีสิทธิ์สามารถอนุมัติทั้งแผน แก้ไขรายการ หรือส่งกลับเพื่อขอข้อมูลเพิ่ม การ override ต้องระบุเหตุผล และระบบเก็บค่าเดิม/ค่าใหม่ใน audit log
7. **Dispatch outside or inside an approved integration.** ใน prototype ขั้นนี้เป็นเพียงการเปลี่ยนสถานะเท่านั้น หากในอนาคตเชื่อมช่องทางส่งงาน ต้องมีการยืนยันปลายทางและไม่ส่งข้อมูลเกินความจำเป็น
8. **Track and close.** ผู้รับผิดชอบอัปเดตสถานะรับงาน รับสินค้า ระหว่างทาง ส่งสำเร็จ หรือยกเลิก เมื่อปิดภารกิจ ระบบคืนสต็อกที่ไม่ได้ใช้และสรุปเหตุผลของงานที่ไม่สำเร็จ

### A.2 SME journey

| ช่วง | การกระทำของร้านค้า | การควบคุมที่ต้องมี |
|---|---|---|
| Onboarding | ยืนยันชื่อร้าน จุดรับสินค้า เวลาทำการ และผู้ติดต่อ | ผู้ประสานงานตรวจสอบก่อนเปิดใช้; จำกัดสิทธิ์ให้เห็นเฉพาะข้อมูลที่เกี่ยวข้อง |
| Stock update | ระบุ SKU/หมวดสินค้า หน่วย จำนวนที่พร้อมจัดสรร ราคาอ้างอิง และเวลาใช้ได้ | บังคับหน่วยมาตรฐาน, ตรวจจำนวนติดลบ, แสดงเวลาอัปเดตล่าสุด |
| Reservation | เห็นจำนวนที่ถูกจองในแผนร่าง/แผนอนุมัติ | ห้ามจองเกิน allocatable stock; การยกเลิกต้องคืนยอดอย่างตรวจสอบได้ |
| Fulfilment | ยืนยันการเตรียมสินค้า/ส่งมอบ หรือแจ้งสินค้าไม่พร้อม | ทุกการเปลี่ยนสถานะต้องมี timestamp และผู้ดำเนินการ |

### A.3 Mission state machine

```text
DRAFT → PENDING_REVIEW → APPROVED → ASSIGNED → IN_PROGRESS → DELIVERED → CLOSED
                  │             │              │                 │
                  └→ NEEDS_INFO └→ CANCELLED   └→ FAILED         └→ DISPUTED
```

- `DRAFT`: สร้างโดยระบบหรือผู้ใช้ ยังไม่ใช่คำสั่งปฏิบัติการ
- `PENDING_REVIEW`: มีข้อมูลขั้นต่ำครบเพื่อให้ผู้อนุมัติตรวจ
- `APPROVED`: ได้รับอนุมัติ; จึงจองสต็อกตามรายการที่อนุมัติ
- `FAILED` / `CANCELLED`: ต้องระบุ reason code เช่น `NO_STOCK`, `ROAD_UNCONFIRMED`, `TRANSPORT_UNAVAILABLE`, `RECIPIENT_UNREACHABLE`
- `CLOSED`: ตรวจสอบการส่งมอบและการกระทบยอดสต็อกแล้ว

## Appendix B. Data Model and Data Quality Policy

### B.1 Core entities

| Entity | ฟิลด์สำคัญ | หมายเหตุการออกแบบ |
|---|---|---|
| Incident | `id`, `name`, `area`, `starts_at`, `status`, `data_mode` | `data_mode` แยกการจำลองออกจากข้อมูลปฏิบัติการ |
| Request | `id`, `incident_id`, `dropoff_zone`, `items`, `priority_inputs`, `time_window`, `status` | เก็บข้อมูลระบุตัวบุคคลแยกจากข้อมูล planning |
| Business | `id`, `service_zone`, `operating_hours`, `verification_status` | ไม่เผยแพร่ข้อมูลติดต่อสาธารณะโดยค่าเริ่มต้น |
| InventorySnapshot | `business_id`, `sku`, `unit`, `allocatable_qty`, `price_reference`, `observed_at`, `expires_at` | เป็น snapshot ที่มีเวลา ไม่เขียนทับประวัติ |
| RoadConstraint | `edge_id`, `condition`, `source`, `observed_at`, `verified_at`, `valid_until` | `CLOSED` ตัด edge ออกจาก routing; `UNKNOWN` ไม่เท่ากับเปิดใช้ได้ |
| Plan / Assignment | `id`, `version`, `request_id`, `inventory_id`, `qty`, `route_version`, `explanation` | เก็บรุ่นแผนเพื่อเปรียบเทียบก่อน/หลัง replan |
| Mission | `assignment_id`, `transporter_id`, `state`, `proof_reference` | ไม่เก็บรูปหรือเอกสารยืนยันเกินความจำเป็น |
| AuditEvent | `actor`, `action`, `entity`, `before`, `after`, `reason`, `at` | เขียนเพิ่มอย่างเดียว; ใช้ตรวจสอบย้อนหลัง |

### B.2 Minimum data contract

ระบบต้องปฏิเสธหรือส่งเข้าคิวตรวจสอบ หากข้อมูลขาดฟิลด์ดังต่อไปนี้:

| ประเภทข้อมูล | ขั้นต่ำที่รับได้ | Validation ตัวอย่าง |
|---|---|---|
| คำขอ | พื้นที่ส่ง, รายการ, จำนวน, หน่วย, เวลาบันทึก | จำนวนต้องมากกว่า 0; หน่วยต้องอยู่ใน catalogue |
| สต็อก | ร้านค้า, สินค้า, จำนวนที่จัดสรรได้, หน่วย, เวลาอัปเดต | ห้ามจองมากกว่าคงเหลือ; snapshot หมดอายุตาม policy |
| ข้อจำกัดถนน | road edge, สถานะ, แหล่งที่มา, เวลารายงาน | ไม่มี source หรือ timestamp = ใช้คำนวณไม่ได้ |
| ผู้ขนส่ง | เขตบริการ, ความพร้อม, ความจุ (ถ้าจะใช้) | ไม่มีความพร้อม = ไม่ถูกเลือกอัตโนมัติ |

### B.3 Freshness policy (ค่าตั้งต้นเพื่อ pilot)

| ข้อมูล | Fresh | Stale | Expired / action required |
|---|---|---|---|
| สต็อกสินค้า | ไม่เกิน 4 ชั่วโมง | มากกว่า 4 ถึง 12 ชั่วโมง | มากกว่า 12 ชั่วโมง: ไม่จัดสรรอัตโนมัติ |
| สถานะถนนในเหตุการณ์ | ไม่เกิน 30 นาที | มากกว่า 30 ถึง 60 นาที | มากกว่า 60 นาที: ขอการยืนยันก่อนอนุมัติ |
| ความพร้อมผู้ขนส่ง | ไม่เกิน 60 นาที | มากกว่า 60 ถึง 120 นาที | มากกว่า 120 นาที: ไม่มอบหมายอัตโนมัติ |

ตัวเลขข้างต้นเป็นค่าเริ่มต้นเพื่อทดสอบ ไม่ใช่มาตรฐานความปลอดภัย ต้องปรับตามพื้นที่ ผู้ให้ข้อมูล และ SOP ของหน่วยงานเจ้าภาพ

## Appendix C. Planning Logic, Explainability and Fairness

### C.1 Deterministic allocation sequence

1. กรองข้อมูลที่ไม่ผ่าน validation หรือหมดอายุ และแยกรายการออกเป็น queue สำหรับตรวจสอบ
2. แปลงคำขอเป็น demand line ตาม `SKU/หมวดสินค้า + หน่วย + จำนวน + time window`
3. หา candidate inventory ที่ชนิด/หน่วยเข้ากัน มีปริมาณจัดสรรได้ และอยู่ใน policy freshness
4. ตรวจเส้นทางบน road graph โดยตัด edge ที่มีสถานะ `CLOSED` ออก และติดธงข้อมูล `UNKNOWN` หรือ stale ที่เกี่ยวข้อง
5. จัดอันดับ candidate ด้วย policy ที่ประกาศได้ เช่น ความเร่งด่วนที่ผ่านการตรวจ, ความครบของสินค้า, ความสดของข้อมูล, ระยะทาง/เวลาคำนวณ และการกระจายภาระระหว่างร้านค้า
6. สร้าง assignment โดยไม่เกินสต็อกและไม่เกินความจุ/ความพร้อมที่ระบุไว้; เก็บ reason เมื่อไม่สามารถจัดสรรได้
7. สรุปผลเป็นแผนร่าง พร้อม exception, uncertainty และผลของข้อจำกัด เพื่อให้คนอนุมัติ

### C.2 Priority policy: explainable, reviewable, non-financial

คะแนนความสำคัญเป็น **เครื่องมือจัดลำดับเพื่อให้มนุษย์ตรวจ** ไม่ใช่การตัดสินอัตโนมัติว่าใคร “สมควร” ได้รับความช่วยเหลือกว่า ตัวอย่าง input ที่อาจใช้หลังได้รับอนุมัติจากเจ้าภาพ: ประเภทสิ่งของจำเป็น, ความเร่งด่วนตามเวลาที่ร้องขอ, สถานะความครบถ้วนของข้อมูล, และสภาพการเข้าถึงที่ยืนยันแล้ว ระบบต้องแสดง input และน้ำหนักที่ใช้ในแต่ละแผน ห้ามใช้ความสามารถในการจ่าย รายได้ หรือสถานะร้านค้ามาเป็นปัจจัยลดลำดับความช่วยเหลือ

### C.3 Minimum explanation shown per assignment

- **What:** จัดสรรสินค้าอะไร กี่หน่วย จากร้านใด ไปยังจุดใด
- **Why this option:** ผ่านเงื่อนไขสินค้าพร้อม/ความสด/ข้อจำกัดเส้นทางใด
- **Evidence:** source และ timestamp ของสต็อกและข้อจำกัดถนนที่นำมาใช้
- **Uncertainty:** ข้อมูลใด stale, unverified หรือไม่อยู่ในขอบเขตของระบบ
- **Alternatives:** ตัวเลือกที่ไม่ถูกเลือกและเหตุผล เช่น สต็อกไม่พอ ถนนปิด หรือข้อมูลหมดอายุ
- **Human action:** สิ่งที่ผู้อนุมัติต้องตรวจ หรือเหตุผลที่ต้องยืนยันภาคสนาม

### C.4 LLM guardrails

LLM เข้าถึงผ่าน tool/function ที่คืนเฉพาะข้อมูลตามสิทธิ์ และตอบใน schema ที่กำหนด เช่น `summary`, `evidence_ids`, `uncertainties`, `questions_for_operator` เท่านั้น การตัดสินใจเชิงจำนวนต้องเรียก planning service ไม่ให้ LLM สร้างจำนวนสต็อก เส้นทาง หรือสถานะถนนขึ้นเอง หากโมเดลไม่มีหลักฐานอ้างอิง ระบบต้องตอบว่า `INSUFFICIENT_EVIDENCE` และส่งกลับให้ผู้ใช้ตรวจสอบ

## Appendix D. API and Integration Blueprint

### D.1 Example service boundaries

| Service | Example endpoint | Input | Output / control |
|---|---|---|---|
| Request service | `POST /incidents/{id}/requests` | request payload + actor | validation result, request ID, audit event |
| Inventory service | `POST /businesses/{id}/inventory-snapshots` | SKU, unit, allocatable qty, observed time | normalized snapshot or validation error |
| Road evidence service | `POST /road-constraints` | edge, condition, source, timestamp | evidence record with freshness status |
| Planning service | `POST /plans:generate` | incident, policy version, selected requests | versioned draft plan and exception list |
| Approval service | `POST /plans/{id}:approve` | approver, revision, reason | approved version or conflict response |
| Tracking service | `POST /missions/{id}:transition` | state, reason, proof reference | allowed state transition + audit event |

ทุก endpoint ที่เปลี่ยนสถานะต้องใช้ authenticated actor, role check, idempotency key และ server-side timestamp. การอนุมัติควรใช้ optimistic concurrency (`plan_version`) เพื่อป้องกันการอนุมัติข้อมูลเก่าหลังมีการ replan.

### D.2 External-data adapter pattern

การเชื่อมต่อข้อมูลภายนอกต้องทำผ่าน adapter แยกตาม provider และแปลงผลลัพธ์เป็น schema ภายในเดียวกัน: `source`, `source_record_id`, `observed_at`, `retrieved_at`, `geometry/edge`, `condition`, `confidence_or_verification`, `license`, `raw_reference` ไม่ควรให้ provider ใด provider หนึ่งเขียนข้อมูลเข้าสู่ planning tables โดยตรง และต้องเก็บ raw reference เท่าที่สิทธิ์อนุญาตเพื่อสืบค้นที่มาได้

### D.3 Integration readiness gates

ก่อนเปิด integration จริง ต้องผ่าน: การตรวจสิทธิ์ API และเงื่อนไขใช้ข้อมูล, rate-limit/backoff, mapping test กับข้อมูลตัวอย่างจริง, failure-mode test เมื่อ provider ล่ม, และการอนุมัติ privacy/security จากเจ้าของข้อมูล ไม่มี gate ใดผ่านแล้วใน prototype ปัจจุบัน

## Appendix E. Security, Privacy and Operational Controls

### E.1 Access model

| Role | สิทธิ์หลัก | ข้อจำกัดสำคัญ |
|---|---|---|
| System administrator | จัดการ tenant, role, integration | ไม่ควรเข้าถึงเนื้อหาคำขอโดยปริยาย |
| Coordinator | สร้าง/แก้คำขอ สร้างแผน ติดตามงาน | อนุมัติได้เฉพาะเมื่อได้รับ role เพิ่ม |
| Approver | ตรวจ อนุมัติ หรือปฏิเสธแผน | ต้องเห็น evidence และความต่างจากแผนก่อนหน้า |
| SME operator | อัปเดตเฉพาะข้อมูลร้าน/สต็อกของตน | ไม่เห็นคำขอหรือข้อมูลผู้รับที่ไม่เกี่ยวข้อง |
| Transporter / volunteer | เห็นงานที่ได้รับมอบหมาย | เห็นเฉพาะข้อมูลการส่งที่จำเป็นและมีอายุจำกัด |
| Auditor | อ่าน audit และรายงานที่ลดข้อมูลระบุตัวบุคคล | ไม่มีสิทธิ์แก้ข้อมูลปฏิบัติการ |

### E.2 Privacy-by-design controls

- เก็บตำแหน่งเป็นระดับ zone หรือจุดนัดหมายเมื่อเพียงพอต่อการวางแผน; เปิดที่อยู่ละเอียดให้ผู้รับงานที่ได้รับมอบหมายเท่านั้น
- แยก PII/contact data ออกจาก planning data, เข้ารหัสขณะส่งและขณะเก็บ, และใช้ token/reference ใน dashboard ทั่วไป
- กำหนด retention schedule ร่วมกับเจ้าของข้อมูลก่อน pilot; งานที่เสร็จแล้วควรถูกทำให้ลดการระบุตัวตนสำหรับ analytics เมื่อทำได้
- ทุกการ export ต้องบันทึกผู้ขอ วัตถุประสงค์ ขอบเขต และเวลา; ปิดการ export แบบกว้างเป็นค่าเริ่มต้น
- ห้ามใส่ข้อมูลสุขภาพหรือกลุ่มเปราะบางใน prompt ที่ส่งออกนอกขอบเขตการอนุมัติข้อมูล

### E.3 Incident response minimum

เมื่อพบข้อมูลผิด สำคัญ หรือการเข้าถึงผิดปกติ: (1) ระงับ token/session หรือ integration ที่เกี่ยวข้อง (2) ทำเครื่องหมายแผนที่ได้รับผลกระทบเป็น `NEEDS_REVIEW` (3) แจ้งเจ้าของระบบและผู้อนุมัติ (4) เก็บหลักฐาน audit (5) ประเมินการแจ้งผู้ได้รับผลกระทบตามข้อตกลงและกฎหมายที่ใช้บังคับ การแก้เหตุการณ์ต้องไม่ลบ audit trail เดิม

## Appendix F. Delivery Plan and Acceptance Criteria

### F.1 Phased roadmap

| ระยะ | ระยะเวลาโดยประมาณ | Deliverables | Exit criteria |
|---|---:|---|---|
| 0 — Discovery | 2 สัปดาห์ | interview guide, journey map, data dictionary, risk register | ผู้ใช้เป้าหมาย 3–5 รายยืนยัน/แก้สมมติฐานหลัก |
| 1 — MVP foundation | 3–4 สัปดาห์ | auth/RBAC, core data model, manual input, audit log | role tests และ CRUD validation ผ่าน |
| 2 — Planning engine | 2–3 สัปดาห์ | inventory matching, synthetic road graph, plan versioning, exceptions | test scenarios ครอบคลุมกรณีสำเร็จ/ถนนปิด/ไม่มีสต็อก |
| 3 — Explainability & UX | 2 สัปดาห์ | evidence panel, approval flow, status tracking, accessibility review | ผู้ใช้ทำ core task สำเร็จตามเกณฑ์ usability |
| 4 — Controlled pilot | 2–4 สัปดาห์ | SOP, onboarding, measurement dashboard, retrospective | เจ้าภาพอนุมัติ, ไม่มี critical safety/privacy issue ที่ค้างอยู่ |

ระยะเวลาเป็นประมาณการสำหรับทีมที่สามารถทำงานต่อเนื่องและยังไม่รวมการอนุมัติจากหน่วยงานภายนอก การเชื่อม API จริงอาจเพิ่มเวลาและความเสี่ยงอย่างมีนัยสำคัญ

### F.2 MVP acceptance criteria

| Capability | Acceptance criterion |
|---|---|
| Data provenance | รายการสต็อกและข้อจำกัดถนนทุกรายการที่ใช้ในแผนแสดง source และ timestamp ได้ |
| Inventory safety | ระบบไม่สร้าง assignment ที่ทำให้ยอดจองเกิน allocatable quantity ใน transaction เดียวกัน |
| Route constraint | เมื่อ edge เป็น `CLOSED` แผนที่สร้างหลังจากนั้นต้องไม่ใช้ edge นั้น; หากไม่มีทางเลือกต้องแสดง exception |
| Approval | แผนที่ยังไม่อนุมัติเปลี่ยนเป็น mission ที่ dispatchable ไม่ได้; override ต้องมี actor และ reason |
| Auditability | เปรียบเทียบแผนสองรุ่นและดูเหตุการณ์เปลี่ยนสถานะย้อนหลังได้ |
| Privacy | ผู้ใช้แต่ละ role ไม่เข้าถึง PII นอกภารกิจ/tenant ของตนใน authorization tests |
| Failure transparency | เมื่อข้อมูลหมดอายุหรือ planning service ล้มเหลว UI แสดงสถานะและไม่แสดงผลเก่าว่าเป็นแผนใหม่ |

### F.3 Test scenarios for demo and pilot

1. **Happy path:** คำขอหนึ่งรายการ สต็อกเพียงพอ ถนนเปิด → สร้างแผนร่าง อนุมัติ และปิดงานได้
2. **Road closure replan:** ปิด edge ที่อยู่บนเส้นทาง → ระบบเลือกเส้นทางอื่น หรือแสดงว่าไม่มีเส้นทาง พร้อมเหตุผล
3. **Stock contention:** สองคำขอใช้สินค้าเดียวกันเกินยอดคงเหลือ → ยอดรวมที่จองไม่เกิน snapshot และคำขอที่เหลือเข้าสู่ exception queue
4. **Stale evidence:** สถานะถนนหรือสต็อกเกิน policy → ต้องมี warning และไม่อนุมัติอัตโนมัติ
5. **Concurrent edit:** ผู้ใช้สองรายแก้แผนคนละหน้าจอ → การอนุมัติรุ่นเก่าถูกปฏิเสธด้วย version conflict
6. **Role boundary:** ผู้ขนส่งพยายามเปิดคำขอที่ไม่ได้รับมอบหมาย → ระบบตอบ `403` และบันทึกเหตุการณ์ความปลอดภัย

## Appendix G. Risks, Dependencies and Open Questions

| ความเสี่ยง/คำถาม | ผลกระทบ | Mitigation / decision needed | Owner ที่เสนอ |
|---|---|---|---|
| ข้อมูลสต็อกไม่สดหรือไม่ตรงจริง | แผนจัดสรรใช้การไม่ได้ | freshness policy, reservation, manual confirmation ก่อนรับสินค้า | SME operator + coordinator |
| รายงานถนนไม่ทันสถานการณ์ | เสี่ยงต่อการตัดสินใจผิด | ไม่รับรองเส้นทาง, evidence expiry, field verification SOP | Incident owner |
| นิยาม “priority” ไม่เป็นธรรม/ไม่เป็นที่ยอมรับ | ความเชื่อมั่นและความเป็นธรรมลดลง | co-design policy, expose weights, override + appeals path | Host organization |
| ผู้ใช้มีภาระอัปเดตข้อมูลสูง | adoption ต่ำ | ลดจำนวนฟิลด์, ใช้ template/import, วัดเวลาต่อ task | Product team |
| การเชื่อม API หรือกฎข้อมูลเปลี่ยน | roadmap ล่าช้า | adapter, mock provider, integration gate | Technical lead |
| PII รั่วไหลใน dashboard/prompt | ความเสียหายต่อผู้รับบริการ | RBAC, minimization, logging, prompt redaction | Security owner |
| ไม่มีผู้มีอำนาจอนุมัติชัดเจน | ระบบเป็นเพียง dashboard ที่ใช้การไม่ได้ | ระบุ RACI และ SOP ก่อน field pilot | Pilot sponsor |

### Open questions to resolve before real-world deployment

1. ใครเป็น data controller และใครอนุมัติการเก็บ/แชร์ข้อมูลในแต่ละพื้นที่?
2. ผู้ใดมีอำนาจประกาศหรือยืนยันสถานะถนน และใช้ SLA ความถี่เท่าใด?
3. หน่วยสินค้ากลาง, รายการของจำเป็น, และกติกาแบ่งสต็อกจะกำหนดร่วมกับชุมชนอย่างไร?
4. การรับมอบและ proof of delivery ที่ไม่เปิดเผยข้อมูลเกินจำเป็นควรเป็นรูปแบบใด?
5. เมื่อไม่มีเส้นทางที่ยืนยันได้ ระบบต้อง escalate ไปยังหน่วยใด และ SLA เท่าใด?
6. หากมีการจัดซื้อจากร้านค้าในพื้นที่ กระบวนการใดต้องปฏิบัติตามกฎการเงิน/จัดซื้อของเจ้าภาพ?

## Appendix H. Glossary

| คำ | ความหมายในเอกสารนี้ |
|---|---|
| Allocation | การกัน/กำหนดจำนวนสินค้าจากแหล่งหนึ่งให้คำขอหนึ่งรายการ; ไม่เท่ากับส่งสำเร็จ |
| Assignment | รายการเชื่อมคำขอ สต็อก และตัวเลือกการส่งในแผนรุ่นหนึ่ง |
| Evidence | ข้อมูลที่ระบุ source, timestamp และสถานะตรวจสอบได้ ซึ่งใช้สนับสนุนข้อเสนอของระบบ |
| Freshness | อายุข้อมูลเทียบกับ policy; ไม่ใช่ความถูกต้องของข้อมูลโดยตัวมันเอง |
| Road edge | ช่วงถนนในกราฟ routing ที่สามารถมีสถานะเปิด/ปิด/ไม่ทราบ |
| Replan | สร้างแผนรุ่นใหม่เมื่อข้อมูลหรือข้อจำกัดเปลี่ยน โดยเก็บความต่างจากรุ่นเดิม |
| SIMULATED | ข้อมูลที่สร้างเพื่อสาธิต/ทดสอบ ต้องไม่สื่อว่าเป็นข้อมูลสถานการณ์จริง |
