> week11 aj. cancled class

## Network Security Tools

### การทำงานของผู้ดูแลระบบ
- ทำยังไงก็ได้ให้ระบบอยู่ได้ 🤷🏻‍♂️
- admin -> ทำทุกอย่างที่ให้ระบบยืนอยู่ได้ 🤯
	- set up system
	- see who's attacking
	- patch software's bug
	- rollback software etc. etc.

### มาตรฐานการดูแลระบบ
- ISO/IEC 20000
	- international standard for IT service management
	- supporting frameworks: ITIL, COBIT
	- policies, plans, processes, procedures: ทำให้เกิดมาตรฐาน
![](https://media.discordapp.net/attachments/1014398974649708624/1090470793231749141/image.png?width=1008&height=685)
- **ITIL** (closes to what admins do)
	- information technology infrastructure library
	- ตั้งเป้าหมายทางกลยุทธ์ (service strategy) เหมาะกับ business 🤓-> เป้าหมายนั้นจะมี service อะไรบ้าง
	- ถ้าได้ service มาแล้วก็เข้าสู่ software life cycle: design -> implement -> test -> deploy blah blah 🥱
	- **service design**: ต้องทำ supplier management, service level management(SLA in softarch), service catalouge management
	- **service transition**: กรณี 1: ถ้ายังไม่มี service ทำไงให้เกิด กรณี 2: มี service เก่าอยู่ทำไงให้ไม่พัง (microservices)
	- **service operation**: เน้นการ monitor การเก็บผลตาม strategy ต่างๆ เพื่อนำมาวิเคราะห์แล้ววนกลับไป service design ต่อ
![](https://media.discordapp.net/attachments/1014398974649708624/1090468399571812414/image.png?width=984&height=685)
- **COBIT**
	- control objectives for information and related technology
	- **มุ่งเน้นการตั้งเป้าหมาย** แล้วจะควบคุมยังไงให้ได้เป้าหมายนั้นๆ
	- cons: ไม่ได้บอกขั้นตอนการไปสู่เป้าหมาย
![](https://media.discordapp.net/attachments/1014398974649708624/1090468741340467270/image.png?width=980&height=685)

### IT Systems Management
- based on ITIL (outside tasks)
- organization & staff
- availability
- system monitoring: (application, network, system)
- change management
- problem management
- network management
- storage management
- capacity planning
- performance tuning
- security

### Performance Tuning
![](https://media.discordapp.net/attachments/1014398974649708624/1090478429683580959/image.png?width=1090&height=685)
- จากรูป: out of memory -> virtual memory
	- เพิ่ม ram, ลด latency ของ disk, ซื้อใหม่ จากค่าเสื่อมราคา

#### CACTI
- system monitoring tool
![](https://media.discordapp.net/attachments/1014398974649708624/1090481605434429532/image.png?width=1000&height=685)
![](https://media.discordapp.net/attachments/1014398974649708624/1090482838840815636/image.png?width=934&height=685)
- load average <= cpu core
- traffic peaks -> every hours might meaning that a script is running 👀

#### Solar wind
![](https://media.discordapp.net/attachments/1014398974649708624/1090484046037000192/image.png?width=761&height=685)


### IPS
- network-based IPS
- host-based IPS
#### Detection Methods
- **signature-based detection**: pattern matching (eg. snort) ตั้งกฏต่างๆ
- **statistical anomaly-based detection**: นับและตั้ง threshold eg. DNS 10reg/mins something beyond that -> _"anomaly"_
- **stateful protocol analysis detection**:  set state -> chain (คล้ายๆ stateful inspection firewall)