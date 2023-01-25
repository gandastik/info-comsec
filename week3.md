## Security Concept Cont.

### Availability 📈
- ระบบงาน/ข้อมูล ต้องสามารถเรียกใช้งานได้ตามข้อกำหนดในการบริการ (SLA)
- แนวทางการรักษาคือ การออแบกระบบให้สามารถรองรับกับ
	- การเพิ่มของ load
	- การโจมตีระบบ
	- อุบัติเหตุ ภัยพิบัติต่างๆ
- ทำให้ต้องมี Resource >= Load (ทำให้เกิดมีการ predict load เพื่อที่จะจัดการกับ resource)
	- การ predict ที่ดีคือ ต้อง predict ให้มี gap ระหว่าง prediction กับ reality ให้น้อยที่สุด
	- 3 cases:
		- constantly load: Return of Investment (RoI) is good
		- load เพิ่มขึ้นแบบ linear: RoI is decent
		- sudden peak of load: ตัวอย่างเช่น สำนักทะเบียน -> ใช้ cloud
- incident ที่ส่งผลกระทบต่อ **resource** (HW, SW, Network, Data, People, Process)
	- พัง, หมดอายุ
	- ถูกโจมตี (Prevent, Detect, Reponse)

## AAA
### Authentication 🔐
- "การเข้าใช้งานระบบ/ ทรัพยากรใดๆ จะต้องเป็นผู้ที่สิทธิในการเข้าใช้งานระบบทรัพยากรนั้นๆ"
- แนวทาง of Authentication คือ
	- **what you know**: password ? การ matching ระหว่าง username & password
		- รองรับด้วยกฏหมายธรุกรรมอิเล็ก -> ธุรกรรมหลังจากทำ wyk แล้วจะถูกยอมรับโดยกฏหมาย
	- **what you have**: eg. id card
	- **what you are**: fingerprints, blood, dna, face?
- authen techniques in web technology
	- **sessions-based**: ให้ 'token' เพื่อเป็นการยืนยันว่า log-in แล้ว โดยให้ user ถือ token ไว้ตลอดเวลา มองที่  connection ถ้าเปลี่ยน connection จะเปลี่ยน session
	- **token-based**: ไม่สนใจ connection คือเป็นการให้ token กับ user แล้วถูกเก็บไว้ที่ cookies (for example)
	- **JSON web token (JWT)**: คือ token ในรูป token ซึ่งสามารถแปะ payload ไว้ในตัว token ได้

### Authorization 🙂
- "การเข้าใช้งานระบบ / ทรัพยากรใดๆ จะต้องเป็นผู้ที่มีสิทธิในการเข้าใช้งานระบบทรัพยากรนั้นๆ"
- แนวทาง of Authorization
	- การจัดการสิทธิ์กับแต่ละ user: ☢️ dumb alert! (more people more effort but why?)
	- **Role-based authorization**: การเพิ่มสิทธิ์ให้กับ role จะทำได้ง่ายขึ้น
		- eg. next gen firewall, proxy ^  etc.
	- Access Control Lists (ACLs): ในด้าน network คือจับ source ip, dest ip ว่าให้ผ่านได้มั้ย

### Accounting 📒
- "การทำงานใดๆ จะต้องสามารถตรวจสอบได้ว่าเกิดขึ้นได้อย่างไร โดยใครส่งผลอะไร ฯลฯ"
- แนวทาง
	- log เมื่อมีการเรียกใช้ อาจจะกำหนดว่า user เข้าถึง table ไหน เฉพาะ table นี้ให้ log เท่านั้น
- log ต้องตามกฏหมายที่ support คือ all electronics can be use in court
	- แต่จำเป็นต้อง log ถึง ip ว่าใครทำอะไร ที่ไหน เมื่อไหร่
	- dev more functions to store more log about usage of functions, data -> put it in requirement specs

## PDR

### Prevent
- "ภัยคุกคามที่ทราบว่าจะเกิดขึ้น จะต้องมีการกำหนดการป้องกัน"
- monitor -> collect **all** events
- ตั้งอุปกรณ์ป้องกัน eg. firewall, IPS (intrusion prevention system), proxy, anti-virus
	- firewall: pattern matching (network layer, transport layer)
	- IPS: เป็นการ follow tcp connection และ check pattern เพื่อดูความผิดปกติ (anomaly) in application layer check for (attack, virus) และยัง **สามารถดู volume** ได้ (eg. DNS record/s)
	- proxy: in application layer
	- anti-virus: มองเมื่อเป็นไฟล์ (application layer)

### Detect
- "ต้องมีกลไกในการตรวจาอบจับภัยคุกคาม และแจ้งเตือนให้ผู้ดูแลระบบ"
- why? - too much to prevent, cant be prevented
- คอยตรวจสอบที่ทรัพยากร ว่ามีความผิดปกติ -> alert -> แล้วค่อยแก้เมื่อเกิดปัญหา
- monitor -> alert when problem occurs
- detect from where?
	- network traffic
	- network request
	- I/O usage

### Response
- "เมื่อมีการแจ้งเตือนจากขั้นตอนการ detect จะต้องมีการตอบสนองอย่างทันท่วงที"
- เมื่อไหร่ก็ตามที่ gap ระหว่าง detect กับ response มันยาว ปัญหาจะเป็นแบบ exponential
- action/plan เมื่อไหร่ก็ตามที่เกิดเหตุ จะให้ทำอะไรบ้าง

#### Word from the wise 🤓
- **"security is process not product"**
- PDR คือ การจัดการสิ่งที่เกิดขึ้นในระบบ แสดงว่าต้องมี action

![](https://media.discordapp.net/attachments/1014398974649708624/1067665960229679134/image.png?width=1057&height=685)

to be cont. 😂