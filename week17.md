	week 16 idk

## IT Security Procedures

![](https://media.discordapp.net/attachments/1014398974649708624/1103171652000423976/image.png?width=916&height=685)

### ISO27001
- security is all of the organization
1. security policy
	- มีการประกาศการนโยบายความปลอดภัย eg. CIA
2. organization of information security
	- มีหน่วยงานที่เกี่ยวกับความปลอดภัยโดยตรง
![](https://media.discordapp.net/attachments/1014398974649708624/1103172590991843388/image.png?width=1101&height=685)
3. asset management
	- การจัดการความปลอดภัยกับอุปกรณ์ต่างๆ
4. human resources security
	- roles
	- screening
	- term and conditions
5. physical and enviromental security
	- securing offices, room, facilities
	- public access and loading areas
	- cabling security
	- equipment maintenance
6. communications and operations management
	- documented operating procedures
	- change management
	- segregation of duties
	- mointoring and review
	- network controls
7. access control
	- user registration
	- privilege management
	- user password management
8. information systems acquisition, development and maintenance
	- input data validation
	- key management
	- access control to program source code
	- change control procedures
9. information security incident management
	- reporting information security events
	- reporting security weaknesses
	- collection of evidence
10. business continuity management
	- business continuity and risk acessment
	- testing, maintaining and re-assessing buisness continuity plans
11. compliance
	- identification fo applicable legislation
	- intellectual property rights
- ISO emphasize on **เอกสาร**, **กระบวนการ**, **infrastructure**
- ISO มาตรฐานระดับพื้นฐาน
	- **เอกสาร**
		- กำหนด CISO (โครงสร้างผู้รับผิดชอบด้านการรักษาความปลอดภัย)
		- เอกสารความรับผิดชอบ
		- นโยบายการรักษาความมั่นคงความปลอดภัย
			- การเข้าถึงข้อมูลและระบบ
			- การสำรอง
			- การแลกเปลี่ยนข้อมูล
			- สอดคล้องตามกฎหมาย
			- ป้องกันไม่ให้มีการใช้งานระบบสารถสนเทศผิดวัตถุประสงค์
		- ข้อกำหนด
			- รักษาความมั่นคงปลอดภัย
			- หน้าที่ความรับผิดชอบ
		- คู่มือ,ขั้นตอนการปฎิบัติ,แผน,เกณฑ์ต่างๆ
	- **กระบวนการ**
		 - ทำสม่ำเสมอ
		 - ทำตามเงื่อนไข
	- **infrastructure**
		- ในระบบต้องมี SSL server
		- physical security: fire, flood, electric hazard
		- firewall, proxy, IPS
		- authentication, monitoring system, backup solution, log server
- ระดับกลาง (ต้องผ่านระดับพื้นฐานครบทุกข้อ)
	- กำหนดเนื้องานและความรับผิดชอบให้ชัดเจน (more detailed)
	- **เอกสาร**: เพิ่มเติมข้อกำหนดรักษาความมั่นปลอดภัย
	- **กระบวนการ/การทำงาน**: ติดตาม, วางแผน, ทบทวน, อบรม, สื่อสาร, จัดจ้าง, วิเคราะห์
	- **infrastructure**: +แบ่งแยกเครือข่ายผู้ใช้งานและควบคุมเส้นทางการไหลของข้อมูล (firewall design การ filter ตาม connection)

## IT Related LAW
- กฎหมายที่เกี่ยวกับ Digital Law มีจุดเริ่มต้นมาจาก **e-commerce** -> thailand was not ready for this shit 💀
- **secure transaction** & **legal transaction** is still a big problems for this shit
- government need to be on top of this -> make laws and rules to make it possible
- government ตั้งคณะกรรมการเทคโนโลยีสารสนเทศแห่งชาติ(กทสช)
![](https://media.discordapp.net/attachments/1014398974649708624/1103149390207651890/image.png)
- 2544 -> กฎหมายเกี่ยวกับธุรกรรมทางอิเล็กทรอนิกส์ (พรบ.ธุรกรรมอิเล็กทรอนิกส์) -> back other 5 laws later
	- "ธุรกรรมอะไรก็ตามที่เป็นอิเล็กทรอนิกส์ให้ถือว่าเหมือนกับธุรกรรมกระดาษ" -> no authen yet
	- no jail time
- 2550 -> กฏหมายเกี่ยวกับการกระทำความผิดเกี่ยวกับคอมพิวเตอร์ (พรบ.คอม)
	- all computer crime -> jail time (คดีอาญา)
	- no 'phishing' -> "นำเข้าข้อมูลอันเป็นเท็จ"

### พรก. vs พรบ.
- พรบ. - พระราชบัญญัติ -> signed by king - covered all in the country
- พรก. - พระราชกำหนด -> no need to pass all the party - บังคับใช้ด้อยกว่าพรบ. ไม่ควรขัดแย้งกัน 
แต่ยังบังคับกับปปช.ทุกคน
- พระราชกฤษฎีกา -> บังคับทุกคน
- ประกาศ -> ออกโดยหน่วยงานที่รับผิดชอบ อำนาจบังคับต่อคนที่เกี่ยวข้องตามหน่วยงาน

- คณะธุรกรรมทางอิเล็กทรอนิกส์ -> ประกาศ - มีการใช้แผนที่ให้รัฐมีผลบังคับด้วย -> ทำให้ประกาศมีผลบังคับทั้งเอกชนและรัฐ
- ประกาศคณะกรรมการธุรกรรมทางอิเล็กทรอนิกส์ เรื่อง มาตรฐานการรักษาความมั่นคงปลอดภัยของระบบสารสนเทศตามวิธีการแบบปลอดภัย พ.ศ. 2555 -> literally the copy of ISO27001
	- enforces the strict version to companys/departments

- กฏหมายเกี่ยวกับลายมือชื่ออิเล็กทรอนิกส์ (released)
	- to be able to identify a person online as a real life person (mapping)
	- 3rd party will verify **Digital Certificate**, **Certification Authority**

- กฏหมายเกี่ยวกับการคุ้มครองข้อมูลส่วนบุคคล -> pdpa
- กฎหมายเกี่ยวกับการโอนเงินทางอิเล็กทรอนิกส์ -> แบงค์ชาติไปทำต่อ

#### ความผิดของพรบ.คอมพิวเตอร์ 2550 (เบื้องต้น)
![](http://elearning.lampangvc.ac.th/moodle/pluginfile.php/9580/mod_page/content/1/rawcom.jpg)
