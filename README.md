
บริบทโครงงานวิจัย
ข้อมูลผู้ทำโครงงาน
ผู้ทำโครงงานกำลังศึกษาปริญญาโท สาขา IT Management ภาคพิเศษวันเสาร์ ที่มหาวิทยาลัยมหิดล แผน ข (Information Systems)
ชื่อหัวข้อภาษาอังกฤษที่กำลังใช้
Development of a Human-in-the-Loop Multi-Agent Agentic AI System for Network Configuration Compliance
แนวคิดของโครงงาน
พัฒนาระบบต้นแบบในรูปแบบเว็บแอปพลิเคชัน ที่ใช้ AI Agents หลายตัวช่วยวิเคราะห์ requirement และข้อมูล configuration ของอุปกรณ์เครือข่าย พร้อมสร้างและตรวจสอบคำสั่งสำหรับจัดการ configuration
ผู้ใช้ระบุ requirement และเลือกอุปกรณ์เป้าหมาย จากนั้นระบบเชื่อมต่อไปอ่าน running-config ของอุปกรณ์ และส่ง requirement พร้อมข้อมูล configuration ให้ Agents ใช้วิเคราะห์ โดยไม่ส่ง credentials ของอุปกรณ์ให้ AI
Agent 1 วิเคราะห์ requirement และ context เพื่อสร้างคำสั่งหรือสคริปต์ ส่วน Agent 2 ตรวจผลงานของ Agent 1 ตามเกณฑ์ที่กำหนด หากพบปัญหา Agent 2 จะส่งข้อเสนอแนะกลับให้ Agent 1 ปรับแก้และส่งตรวจซ้ำ ภายใต้จำนวนรอบหรือเงื่อนไขหยุดที่กำหนด
เมื่อ Agent 2 เห็นว่าผลงานผ่านเกณฑ์ ระบบจะแสดงข้อเสนอให้มนุษย์ตรวจและอนุมัติ ก่อนที่เว็บแอปพลิเคชันจะเชื่อมต่อและ execute คำสั่งบนอุปกรณ์ ผู้ใช้ไม่ต้องคัดลอกคำสั่งไป SSH และตั้งค่าเอง
หลัง execute ระบบบันทึกสถานะการส่งคำสั่งและข้อความตอบกลับหรือ error จากอุปกรณ์ แล้วจัดทำ Audit Report จากข้อมูลที่ระบบบันทึก ระบบ ยังไม่ตรวจ configuration ซ้ำหลัง execute โดยอัตโนมัติ และ AI ไม่ได้เป็นผู้เขียนรายงาน
Workflow ที่ต้องการ
1. ผู้ใช้ระบุ requirement และเลือกอุปกรณ์เครือข่ายเป้าหมาย
2. ระบบเชื่อมต่อไปอ่าน running-config จากอุปกรณ์ และจัดเตรียมข้อมูลพร้อม requirement ให้ Agents
3. Agent 1 วิเคราะห์โจทย์และข้อมูล context แล้วสร้างคำสั่งหรือสคริปต์
4. Agent 2 ตรวจผลงานตามเกณฑ์ที่กำหนด เช่น ความถูกต้องของคำสั่งหรือโค้ด และความสอดคล้องกับ configuration compliance
5. หาก Agent 2 พบปัญหา จะส่งข้อเสนอแนะกลับให้ Agent 1 แก้ไข แล้วตรวจซ้ำจนผ่านหรือถึงเงื่อนไขหยุดที่กำหนด
6. เมื่อ Agent 2 เห็นว่าผลงานผ่านเกณฑ์ ระบบแสดงข้อเสนอให้มนุษย์พิจารณาและอนุมัติ
7. เมื่อมนุษย์อนุมัติ ระบบเชื่อมต่อไป execute คำสั่งบนอุปกรณ์ หากไม่อนุมัติ ระบบจะไม่ execute
8. หลัง execute ระบบบันทึกสถานะและข้อความตอบกลับหรือ error จากอุปกรณ์ พร้อมข้อมูลการตรวจของ Agents และการอนุมัติ แล้วสร้าง Audit Report และแสดงประวัติบนหน้าเว็บ
บทบาทของส่วนประกอบ
* Agent 1: วิเคราะห์ requirement และข้อมูลเครือข่าย แล้วสร้างหรือปรับปรุงคำสั่งหรือสคริปต์
* Agent 2: ตรวจผลงานของ Agent 1 ตามโจทย์ ความถูกต้อง และเกณฑ์ compliance พร้อมส่งข้อเสนอแนะกลับเมื่อพบปัญหา
* Human approver: ตรวจข้อเสนอที่ผ่านการตรวจของ Agents แล้วอนุมัติหรือไม่อนุมัติการ execute
* Web application / system: รับ requirement อ่าน running-config ประสานงานระหว่างผู้ใช้ Agents และอุปกรณ์ execute เมื่อมนุษย์อนุมัติ บันทึกผลตอบกลับจากอุปกรณ์ และสร้าง Audit Report
ข้อมูลใน Audit Report
ระบบสร้างรายงานจากข้อมูลการทำงานที่บันทึกไว้ รายงานอาจประกอบด้วย:
* วันเวลา ผู้เริ่มงาน และ requirement
* อุปกรณ์เป้าหมาย
* ผลตรวจของ Agent 2 และจำนวนรอบที่ Agents ปรับแก้
* ผลการอนุมัติของมนุษย์
* สถานะการ execute แยกตามอุปกรณ์
* ข้อความตอบกลับหรือ error จากอุปกรณ์
สถานะ execute ที่รายงานหมายถึงผลการส่งคำสั่งและข้อความตอบกลับจากอุปกรณ์ ไม่ได้ยืนยันว่า configuration หลัง execute ผ่าน compliance แล้ว
ความหมายของ Human-in-the-Loop ในโครงงานนี้
มนุษย์ไม่ต้องเข้ามาแทรกทุกครั้งที่ Agent 1 และ Agent 2 โต้ตอบกัน แต่จะพิจารณาข้อเสนอหลัง Agents ตรวจและปรับแก้จนผ่านเกณฑ์แล้ว มนุษย์ต้องอนุมัติก่อนที่ระบบจะ execute คำสั่งบนอุปกรณ์
ความหมายของ Agentic AI ในโครงงานนี้
ลักษณะ agentic อยู่ที่ Agents ทำงานตามเป้าหมายและใช้ผลตรวจของ Agent 2 ให้ Agent 1 ปรับปรุงผลงานเป็นรอบ ๆ จนผ่านเกณฑ์หรือถึงเงื่อนไขหยุด การรันงานตามเวลาและการแสดงประวัติเป็นความสามารถด้าน automation ของระบบ ไม่ใช่เหตุผลหลักที่ทำให้ระบบมีลักษณะ agentic
ขอบเขตและสิ่งที่คาดว่าจะศึกษา
* พัฒนาเว็บแอปพลิเคชันต้นแบบสำหรับช่วยวิเคราะห์และจัดการ configuration เครือข่าย
* ใช้ Agent 1 และ Agent 2 ทำงานวนตรวจและแก้ไข โดยให้มนุษย์อนุมัติก่อน execute
* ระบบอ่าน running-config จากอุปกรณ์เป้าหมายก่อนส่งบริบทให้ Agents
* หลังอนุมัติ ระบบเป็นผู้เชื่อมต่อและ execute คำสั่ง ผู้ใช้ไม่ต้องนำคำสั่งไปตั้งค่าด้วยตนเอง
* ทดสอบกับสถานการณ์และเกณฑ์ configuration compliance ที่กำหนด ไม่กล่าวอ้างว่าครอบคลุมอุปกรณ์ทุกยี่ห้อหรือ configuration ทุกประเภท
* ประเมินความถูกต้องของข้อเสนอหรือคำสั่งตามเกณฑ์ที่กำหนด และเปรียบเทียบเวลาทำงานกับการตรวจแบบ manual
* ระบบบันทึกผลการตรวจของ Agents การอนุมัติ สถานะ execute และข้อความตอบกลับหรือ error จากอุปกรณ์
* ยังไม่รวมการตรวจ configuration หลัง execute โดยอัตโนมัติ
* จำนวนรอบของ Agents และ token/API cost อาจเก็บเป็นข้อมูลประกอบ แต่ยังไม่กำหนดเป็นตัวชี้วัดหลัก
* Audit Report สร้างโดยระบบจาก log และผลการทำงาน ไม่ใช่รายงานที่ AI เขียน
ข้อควรระวังในการช่วยทำงานต่อ
* ยึดแนวทาง Human-in-the-Loop เป็นแนวทางปัจจุบัน
* อย่านำ Auto Execution ที่ไม่มีมนุษย์อนุมัติกลับมาเป็นแบบหลัก เว้นแต่ผู้ทำโครงงานจะเปลี่ยนแนวทาง
* แยกบทบาท Agent 2 ที่ตรวจข้อเสนอ ออกจากมนุษย์ที่อนุมัติให้ระบบ execute
* อย่าเขียนว่า Agents ทำงานวนซ้ำไม่จำกัด ควรกำหนดจำนวนรอบหรือเงื่อนไขหยุด
* อย่าเขียนว่าระบบตรวจ configuration หลัง execute อัตโนมัติ เพราะยังไม่อยู่ในขอบเขต
* แยกสถานะการ execute และข้อความตอบกลับจากอุปกรณ์ ออกจากการยืนยันว่า config ผ่าน compliance
* Audit Report เป็นรายงานที่ระบบรวบรวมจากข้อมูลที่บันทึก ไม่ใช่ AI สร้างเนื้อหารายงาน
* แยกข้อสรุปที่ตกลงแล้วออกจากข้อเสนอหรือประเด็นที่ยังไม่กำหนด
ทฤษฎีและแนวคิดที่กำลังพิจารณา
* Socio-Technical Systems Theory: ใช้อธิบายความสัมพันธ์ระหว่างระบบเทคนิค กระบวนการทำงาน และบทบาทของผู้ดูแลเครือข่าย
* Multi-Agent Systems: ใช้อธิบายการแบ่งบทบาทและการโต้ตอบระหว่าง Agent 1 กับ Agent 2
* Human–Automation Interaction / Appropriate Reliance: ใช้ประกอบแนวคิดการให้มนุษย์พิจารณาและอนุมัติก่อนระบบดำเนินการ
รายการนี้ยังเป็นแนวคิดที่กำลังพิจารณาสำหรับส่วน Related Theories and Concepts ไม่ใช่กรอบทฤษฎีที่ยืนยันขั้นสุดท้าย
ประเด็นที่ยังต้องกำหนดหรือยืนยัน
* อุปกรณ์และสภาพแวดล้อมทดลอง เช่น Cisco IOS/IOS XE และ network emulator
* ประเภท configuration, test cases และเกณฑ์ compliance ที่จะใช้
* ข้อมูล show อื่นนอกเหนือจาก running-config จำเป็นหรือไม่ในแต่ละสถานการณ์
* Agent 2 จะตรวจ syntax และ compliance ด้วย LLM, rule-based checks หรือใช้ร่วมกัน
* จำนวนรอบสูงสุดและการจัดการเมื่อยังไม่ผ่านเกณฑ์
* เมื่อมนุษย์ไม่อนุมัติ จะยกเลิกงานหรือส่งกลับไปปรับแก้






Page 1 | 25 วินาที

สวัสดีครับ วันนี้ผมขอนำเสนอโครงงานเรื่อง Development of a Human-in-the-Loop Multi-Agent Agentic AI System for Network Configuration Compliance

หรือการพัฒนาระบบ Agentic AI แบบ Multi-Agent ที่มีมนุษย์ร่วมในกระบวนการ สำหรับกำกับความสอดคล้องตามข้อกำหนดของการตั้งค่าเครือข่าย

โดยมีอาจารย์ที่ปรึกษาคือ รองศาสตราจารย์ ดร.สุภาภรณ์ เกียรติสิน ครับ

ก่อนอื่น ผมขอเริ่มจาก Background และปัญหาของการตรวจสอบ Network Configuration ในปัจจุบันครับ

Page 2 | 45 วินาที

ในปัจจุบัน Network Configuration มีความซับซ้อนมากขึ้น และต้องตรวจสอบให้สอดคล้องกับ Requirement รวมถึงมาตรฐานที่องค์กรกำหนด

เมื่อมีอุปกรณ์จำนวนมาก การไล่ตรวจ Configuration ทีละอุปกรณ์จะใช้เวลาค่อนข้างมาก และ Configuration ที่ไม่สอดคล้องกันอาจนำไปสู่ปัญหาด้าน Compliance ได้

LLM สามารถช่วยแปลง Network Requirement ให้เป็น Configuration Commands และรองรับ Workflow ที่มีหลายขั้นตอนได้

อย่างไรก็ตาม คำสั่งที่ AI สร้างขึ้นยังต้องได้รับการตรวจสอบอย่างรอบคอบ เพราะหากคำสั่งไม่ถูกต้อง อาจส่งผลกระทบต่อการทำงานของอุปกรณ์

ดังนั้น Human Oversight และความรับผิดชอบในการอนุมัติที่ชัดเจนจึงยังมีความสำคัญครับ

Page 3 | 55 วินาที

จาก Background ดังกล่าว Problem หลักของงานนี้คือ Configuration Commands ที่ AI สร้างขึ้นอาจมี Syntax Error ไม่รองรับอุปกรณ์เป้าหมาย หรือไม่สอดคล้องกับ Requirement และ Compliance Criteria ที่กำหนด

หากระบบนำคำสั่งที่ไม่ถูกต้องไป Execute อาจทำให้การเปลี่ยนแปลงไม่สำเร็จ หรือทำให้อุปกรณ์ตอบกลับในลักษณะที่ไม่คาดคิด

ดังนั้น โครงงานนี้จึงเสนอ Structured Workflow ที่ให้ AI Agents หลายตัวช่วยกันสร้าง ตรวจสอบ และปรับปรุง Proposed Commands

เมื่อ Agents ตรวจสอบจนผ่านเกณฑ์ที่กำหนดแล้ว ระบบจะยังไม่ Execute ทันที แต่ต้องให้มนุษย์ตรวจสอบและอนุมัติก่อน

หลังจากนั้น ระบบจึงจะนำคำสั่งไป Execute บนอุปกรณ์และบันทึกสถานะ Device Response หรือ Error เพื่อใช้สำหรับ Audit ครับ

Page 4 | 45 วินาที

Motivation ของโครงงานนี้มาจากการที่ Network Administrator ต้องเปรียบเทียบ Configuration ของอุปกรณ์กับ Requirement และมาตรฐานที่กำหนด

หากต้องตรวจสอบหลายอุปกรณ์ด้วยกระบวนการ Manual จะใช้เวลาและอาจทำให้การดำเนินการล่าช้า

LLM สามารถช่วยทำความเข้าใจ Requirement และสร้าง Configuration Commands ได้ ขณะที่ Multi-Agent Workflow สามารถเพิ่มขั้นตอน Review and Revision ก่อนนำข้อเสนอไปให้มนุษย์พิจารณา

งานวิจัยนี้จึงศึกษาว่าแนวทางดังกล่าวจะสามารถนำมาใช้กับ Selected Network Scenarios ได้หรือไม่ โดยประเมินทั้งความถูกต้องของคำสั่งและเวลาที่ใช้เมื่อเทียบกับ Manual Process ครับ

Page 5 | 70 วินาที

โครงงานนี้มีวัตถุประสงค์หลัก 3 ข้อครับ

ข้อแรก คือพัฒนาระบบ Human-in-the-Loop Multi-Agent Agentic AI สำหรับ Network Configuration Compliance

ข้อที่สอง คือประเมินว่า Commands ที่ AI สร้างขึ้นสอดคล้องกับ Configuration Requirements และ Compliance Criteria ที่กำหนดไว้หรือไม่

และข้อที่สาม คือเปรียบเทียบเวลาที่ใช้ระหว่าง Proposed System กับการตรวจสอบแบบ Manual ภายใต้ Scenario เดียวกัน

Corresponding Research Questions จะประกอบด้วย

ข้อแรก Multi-Agent Workflow จะประสานการสร้างและตรวจสอบคำสั่งแบบ Iterative พร้อม Human Approval ก่อน Execute บนอุปกรณ์ได้อย่างไร

ข้อที่สอง AI-generated Commands สอดคล้องกับ Requirement และ Compliance Criteria ในระดับใด

และข้อที่สาม เวลาที่ Proposed System ใช้แตกต่างจาก Manual Review อย่างไรครับ

Page 6 | 55 วินาที

ขอบเขตของโครงงานแบ่งออกเป็น 4 ส่วนครับ

ส่วนแรก คือพัฒนา Web Application สำหรับรับ Network Configuration Requirement เลือกอุปกรณ์เป้าหมาย และจัดการ Compliance Check

ส่วนที่สอง คือพัฒนา Multi-Agent Workflow โดย Agent 1 ทำหน้าที่สร้าง Configuration Recommendations หรือ Commands ส่วน Agent 2 ทำหน้าที่ตรวจสอบตาม Requirement และ Criteria พร้อมส่ง Feedback กลับให้ Agent 1 ปรับแก้แบบ Iterative

ส่วนที่สาม คือ Human-in-the-Loop โดยมนุษย์ต้องตรวจสอบและอนุมัติก่อนที่ระบบจะ Execute คำสั่ง

และส่วนสุดท้าย คือการประเมิน Prototype ด้วย Selected Configuration Scenarios โดยเปรียบเทียบ Correctness และ Task Completion Time กับ Manual Review ครับ

Page 7 | 35 วินาที

Expected Results ของโครงงานมี 3 ส่วนครับ

ส่วนแรก คือ Working Web Application ที่สามารถประสานการทำงานระหว่าง Agent 1 และ Agent 2 พร้อม Human Approval ก่อน Execute

ส่วนที่สอง คือ Evaluation Results เกี่ยวกับความถูกต้องของ Proposed Commands เมื่อเทียบกับ Criteria ที่กำหนด และเวลาที่ใช้เมื่อเทียบกับ Manual Review

ส่วนที่สาม คือ System Records and Logs ซึ่งประกอบด้วย Approval Decision, Execution Status, Device Response และ Error ที่เกิดขึ้น

ข้อมูลเหล่านี้จะถูกนำไปจัดทำเป็น Audit Report โดยระบบครับ

Page 8 | 50 วินาที

งานวิจัยที่เกี่ยวข้องชิ้นแรกคือ NetConfEval: Can LLMs Facilitate Network Configuration? ของ Wang และคณะ ในปี 2024

งานนี้ประเมินความสามารถของ LLM ในงาน Network Configuration Synthesis และ Translation

ผลการศึกษาพบว่า GPT-4 ทำงานได้ดีในการแปลง Natural-language Requirements ไปเป็น Formal Specifications และผู้วิจัยยังเสนอ Multi-stage Workflow ที่มี Verifier Feedback

อย่างไรก็ตาม Human Interaction ในงานนี้เป็นเพียง Optional Feature และไม่ได้ประเมินการ Execute คำสั่งบน Network Devices

จุดนี้จึงเชื่อมโยงกับโครงงานของผม ซึ่งกำหนดให้ Human Approval เป็นขั้นตอนบังคับก่อน Execute ครับ

Page 9 | 50 วินาที

งานถัดมาคือ Cornetto: Benchmarking LLM-Driven Network Configuration Repair ของ Protogerοs และคณะ ในปี 2026

งานนี้นำเสนอ Formal Verification Benchmark จำนวน 231 Misconfiguration Repair Scenarios บน Topology ขนาดตั้งแต่ 20 ถึง 754 Nodes

ผลการศึกษาจาก LLM จำนวน 9 Models พบว่า Single-pass Model มีโอกาสสร้าง Network Regression เพิ่มเติม และประสิทธิภาพลดลงเมื่อ Network มีขนาดใหญ่ขึ้น

อย่างไรก็ตาม งานนี้ประเมิน Configuration Repair ผ่าน Batfish-based Network Behavior Analysis และไม่ได้ประเมิน Human-approved Command Execution บนอุปกรณ์ใน Lab หรือ Emulated Environment

จึงแสดงให้เห็นว่าการใช้ AI เพียงรอบเดียวอาจไม่เพียงพอ และควรมีขั้นตอน Review and Revision ครับ

Page 10 | 60 วินาที

จากงานวิจัยที่เกี่ยวข้อง พบว่า LLM มีศักยภาพในการตีความ Requirement สร้าง Configuration และช่วยแก้ไข Misconfiguration

แต่ยังมีช่องว่างสำคัญ คือบางงานใช้ Single-pass Generation ขณะที่บางงานมี Verifier แต่ยังไม่ได้กำหนด Human Approval เป็น Mandatory Step ก่อน Execute

นอกจากนี้ ยังมีงานจำนวนจำกัดที่ประเมิน Workflow ตั้งแต่การอ่าน Running-config การสร้างและตรวจสอบ Commands การอนุมัติของมนุษย์ ไปจนถึงการ Execute บนอุปกรณ์ใน Test Environment

โครงงานนี้จึงเข้ามาเติมช่องว่างโดยใช้ Agent 1 และ Agent 2 ทำงานแบบ Iterative ภายใต้ Retry Limit มี Human Approval ก่อน Execute และบันทึก Execution Status, Device Response รวมถึง Error เพื่อรองรับการ Audit ครับ

Page 11 | 55 วินาที

โครงงานนี้พิจารณาแนวคิดที่เกี่ยวข้อง 3 ส่วนครับ

ส่วนแรกคือ Socio-Technical Systems ซึ่งมองการออกแบบระบบเทคนิคควบคู่กับกระบวนการและบทบาทของมนุษย์ ในโครงงานนี้จึงไม่ได้พิจารณาเฉพาะ AI Workflow แต่รวมถึงบทบาทของ Network Administrator ในการตรวจสอบและอนุมัติด้วย

ส่วนที่สองคือ Multi-Agent Systems ซึ่งนำมาใช้แบ่งหน้าที่ระหว่าง Agent 1 ที่สร้าง Commands และ Agent 2 ที่ตรวจสอบและส่ง Feedback กลับเป็น Iterative Loop

ส่วนสุดท้ายคือ Human-Automation Interaction ซึ่งสนับสนุนแนวคิด Appropriate Reliance โดยกำหนดให้มนุษย์ตรวจและอนุมัติก่อนที่ระบบจะ Execute คำสั่งบนอุปกรณ์ครับ

Page 12 | 45 วินาที

งานนี้เป็น Applied หรือ Development Research โดยนำ AI Agents, Network Configuration และ Web Application Development มาประยุกต์ใช้กับ Configuration Compliance

กระบวนการวิจัยแบ่งเป็น 5 ขั้นตอน

เริ่มจากการกำหนดปัญหาและทบทวน Literature

จากนั้นกำหนดแนวคิดและทฤษฎีที่เกี่ยวข้อง

ขั้นตอนที่สามคือออกแบบและพัฒนา Web Application รวมถึง Multi-Agent Workflow

ขั้นตอนที่สี่คือทดสอบ Correctness ตาม Compliance Criteria และเปรียบเทียบ Task Completion Time

และขั้นตอนสุดท้ายคือวิเคราะห์ผล สรุปข้อจำกัด และจัดทำรายงานการวิจัยครับ

Page 13 | 85 วินาที

สำหรับ Proposed System Workflow จะเริ่มจากผู้ใช้ระบุ Requirement และเลือก Network Devices เป้าหมาย

จากนั้น Web Application จะเชื่อมต่อไปยังอุปกรณ์เพื่ออ่าน Running-config และจัดเตรียม Running-config พร้อม Requirement ให้ Agents ใช้เป็น Context โดย Credentials ของอุปกรณ์จะไม่ถูกส่งให้ AI

Agent 1 จะวิเคราะห์ Requirement และ Context แล้วสร้าง Commands หรือ Script

Agent 2 จะตรวจสอบผลลัพธ์ตามเกณฑ์ที่กำหนด เช่น ความถูกต้องของคำสั่ง และความสอดคล้องกับ Configuration Compliance

หาก Agent 2 พบปัญหา จะส่ง Feedback กลับให้ Agent 1 ปรับแก้ แล้วส่งกลับมาตรวจสอบใหม่ กระบวนการนี้จะทำซ้ำจนกว่าจะผ่านเกณฑ์หรือถึง Retry Limit ที่กำหนด

เมื่อ Agent 2 เห็นว่าผ่านเกณฑ์แล้ว ระบบจะแสดง Proposed Commands ให้มนุษย์ตรวจสอบ

หากมนุษย์ไม่อนุมัติ ระบบจะไม่ Execute แต่หากอนุมัติ Web Application จะเชื่อมต่อและ Execute คำสั่งบนอุปกรณ์

หลังจากนั้น ระบบจะบันทึก Agent Reviews, Approval Decision, Execution Status, Device Response และ Error เพื่อนำไปจัดทำ Audit Report

อย่างไรก็ตาม Execution Status ในงานนี้หมายถึงผลการส่งคำสั่งและ Response จากอุปกรณ์ ยังไม่ได้หมายถึงการยืนยันว่า Configuration หลัง Execute ผ่าน Compliance แล้วครับ

Page 14 | 75 วินาที

สำหรับ Test Environment จะใช้ Network Lab หรือ Emulator ร่วมกับ Selected Network Devices

Input หลักประกอบด้วย User Requirement และ Initial Running-config ที่อ่านจากอุปกรณ์เป้าหมาย

ส่วน Test Scenarios จะเป็น Configuration Compliance Tasks ที่กำหนด Requirement และ Evaluation Criteria ไว้ล่วงหน้า

ในการเปรียบเทียบ จะใช้ Scenario, Starting Configuration และ Criteria ชุดเดียวกันกับทั้ง System-assisted Process และ Manual Process

จากนั้นจะประเมิน Proposed Commands ของทั้งสองวิธีด้วย Criteria เดียวกัน และจับ Task Completion Time โดยกำหนด Start Point และ End Point ให้สอดคล้องกัน

Measures หลักประกอบด้วย Output Correctness และ Task Completion Time

ส่วน Supporting Records จะเก็บผลตรวจของ Agent 2 จำนวน Revision Rounds, Human Approval Decision, Execution Status และ Device Response หรือ Error ครับ

Page 15 | 55 วินาที

ภาพรวม Research Activity แบ่งออกเป็น 5 Phases ครับ

Phase แรก คือ Problem Definition and Literature Review เพื่อกำหนดปัญหา วัตถุประสงค์ และงานวิจัยที่เกี่ยวข้อง

Phase ที่สอง คือ Requirements and Test Design เพื่อกำหนด Configuration Tasks, Compliance Criteria, Test Scenarios และ Starting Configurations

Phase ที่สาม คือ System Design and Development เพื่อพัฒนา Web Application, Agent Review Loop, Human Approval และ Execution Function

Phase ที่สี่ คือ System Demonstration and Evaluation โดยใช้ Scenario และ Starting Configuration เดียวกันกับทั้งระบบและ Manual Process

และ Phase สุดท้าย คือ Results and Reporting เพื่อวิเคราะห์ Correctness, Completion Time, Execution Records รวมถึงสรุปข้อจำกัดและข้อเสนอแนะครับ

Page 16 | 35 วินาที

สำหรับแผนการดำเนินงาน จะเริ่มจากการทบทวน Literature และกำหนด Requirements กับ Test Scenarios

จากนั้นจึงออกแบบ Architecture และพัฒนา Web Application รวมถึง Multi-Agent Workflow

เมื่อพัฒนา Prototype แล้ว จะทดสอบระบบใน Network Lab หรือ Emulator เก็บข้อมูล Correctness และ Task Completion Time แล้วนำผลมาวิเคราะห์

ขั้นตอนสุดท้ายคือสรุปผล ข้อจำกัด และจัดทำรายงานฉบับสมบูรณ์ตามกรอบเวลาที่กำหนดครับ

Page 17 | 10 วินาที

ทั้งหมดนี้คือแนวทางของโครงงานที่นำเสนอครับ

ขอบพระคุณอาจารย์ทุกท่านที่รับฟัง และยินดีรับคำแนะนำหรือข้อเสนอแนะครับ

จุดที่ควรแก้ในสไลด์ก่อนนำเสนอ

Page 1: ใช้ชื่อภาษาไทยที่ตกลงแล้วให้ตรงกันทั้งเอกสาร
 การพัฒนาระบบปัญญาประดิษฐ์เชิงตัวแทนแบบหลายเอเจนต์ที่มีมนุษย์ร่วมในกระบวนการ สำหรับการกำกับความสอดคล้องตามข้อกำหนดของการตั้งค่าเครือข่าย

Page 5: Research Question 1 แนะนำให้ใช้
 How can a multi-agent workflow coordinate iterative command generation and review, with human approval before execution on network devices?

Page 5: แก้ช่องว่าง devices ? เป็น devices?

Page 12: หากข้อความปัจจุบันคือ Test compliance, record execution times, and assess accuracy แนะนำเปลี่ยนเป็น
 Evaluate proposed-command compliance, record task completion time, and assess correctness.

Page 13: ต้องรักษาคำอธิบายให้ชัดว่า Agent 2 ตรวจ Proposed Commands ส่วน Human Approver เป็นผู้อนุมัติให้ระบบ Execute

ระหว่างนำเสนอ หลีกเลี่ยงการพูดว่าระบบ ยืนยัน Compliance หลัง Execute เพราะ Post-execution Verification ยังไม่อยู่ใน Scope ปัจจุบันครับ
* วิธีประเมินความถูกต้องและเวลาที่ใช้ รวมถึงวิธีเปรียบเทียบกับ manual อย่างเป็นธรรม
* รายละเอียดของ Audit Report และข้อมูลที่จะแสดงในประวัติบนหน้าเว็บ
* จะเก็บ token/API cost เป็นข้อมูลประกอบหรือไม่
* ชื่อหัวข้อภาษาไทยและการปรับถ้อยคำชื่อภาษาอังกฤษให้เหมาะกับรูปแบบวิชาการ
