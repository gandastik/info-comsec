## Network Attack & Solution
- Threats (ภัยคุกคาม ☢️)
- Vulnerability (ช่องโหว่)
	- is a property
	- is an un-expected "feature" in the system
- Exploit (การอาศัยช่องโหว่เพื่อโจมตีระบบ)
	- has to be a vulnerability

### Type of Malware
- Spam
- Computer viruses
- Worms
- Trojan Horses
	- keylogger
	- cache
- spyware
	- "spy"
- ransomware
- adware
	- ads pop-up
	- everything that is free nowadays is consider to be "adware" (in-app purchase)

### Q: How can we prevent/fix the malware? 🤔
- ในปัจจุบันมีการใช้ IPS (Intrusion Prevention System) หรือต่างๆ โดยที่มีการใช้หลักการ **signature base**
	- antivirus "ez money"
	- คือการเก็บ pattern ต่างๆที่รู้ของ virus ต่างๆ
	- โดยจะรู้ virus signature ต่างๆได้ก็จำเป็นต้องเจอ virus ตัวๆนั้นก่อน แล้วส่ง update ต่างๆเรื่อยๆ
- **anomaly base** -> Firewall
	- แต่ทั้งหมดก็เกิด false positive กับ false negative ได้
- detection system (IDS, IPS, Antivirus) -> catch these mothersuckas
	- still error prone

### Sniffer
- sniff packets that is in-flight
	- catch from data-link layer
- NIC -> Promiscuous Mode - ทำให้เราได้ข้อมูลของ network
- HUB -> you just need to only install 1 sniffer at one of the interface in HUB
- Switch -> hard to choose a place to install (didnt broadcast to all port like HUB)
	- ถ้าในกรณีที่ switch ไม่สามารถเก็บ MAC addr. ได้ไม่ครบใน network -> switch จะทำหน้าที่คล้ายกับ HUB
	- **attacker** 😎 -> flood switch mac addr. -> switch turns to hub -> ez sniffer installed
	- **in present day** switch can detect ARP flood from which port and then disable that port 😎

### Q: how can we protect / prevent sniffing data ?
- using security concept about data -> **Confidentiality & Integrity**
	- encrypt data 🔥

### DoS
- SYN Flood
- Land Attack
- Smurf Attack
	- ปลอม src IP address -> "amplifies data"  make destination ip (broadcast)  and sent ICMP echo request
	- ทำให้ทุกเครื่องที่ได้รับ broadcast ส่งข้อมูลกลับมาหา IP address ที่ถูกปลอม
- Ping of Death
	- normal ping
- Ping Flod
	- normal ping but with more amount
- Teardrop Attack
	- ip fragmentation -> cant put together just eats up your ip buffer
- Fraggle

### DDoS
![](https://media.discordapp.net/attachments/1014398974649708624/1077803902793158696/image.png?width=994&height=685)

### Q: Protect/Prevent against DoS
- Firewall
- detection

### NMAP
- หา information ของ network of target
![](https://media.discordapp.net/attachments/1014398974649708624/1077804292917960744/image.png?width=707&height=685)
- TCP Syn Scan คือเป็นการส่ง packet syn เข้าไปหาข้อมูลในเครือข่าย แต่จะสามารถถูกป้องกันได้โดย firewall
- TCP Connect Scan คือเป็นการทำ 3-way handshake แบบจริงๆเลย ทำให้สามารถได้รับ banner มาด้วยได้ แต่จำเป็นต้องเปิดเผยตัวตน
- Fin Scan คือเป็นการส่ง fin packet ไป ซึ่งเป็นการปลอมตัวว่า "ภายในมีการ open connection  กับภายนอกแล้วส่งข้อมูลกันเสร็จแล้วทำให้ ภายนอกส่ง fin กลับมา" ทำให้วิธีนี้สามารถหลอก firewall ได้ ทำให้มีการเปิดช่องให้
	- สามารถเช็คได้ว่า port ไหนเปิดอยู่ หรือปิดอยู่

#### Buffer Overflow
![](https://media.discordapp.net/attachments/1014398974649708624/1077809563891404901/image.png?width=918&height=685)

### Q: How can we prevent/protect against Exploits
- we cant
- only way is to upgrade/update system

### TCP/IP Hijacking
![](https://media.discordapp.net/attachments/1014398974649708624/1077810144898977853/image.png?width=1130&height=685)
#### Session Hijacking Tool
![](https://media.discordapp.net/attachments/1014398974649708624/1077810689839747102/image.png?width=1196&height=685)
- prevent -> integrity : given the src generate hash code and send to dest to compare to check if the data has been changed or not

### Q: prevent/protect session hijack
- expire time

### Rouge Access Point
![](https://media.discordapp.net/attachments/1014398974649708624/1077812691852349460/image.png)
- access point - จะเป็นการส่ง beacon frame ออกมาตลอดเวลา
- หลักการ -> ปกติแล้วมีการเชื่อมต่อกับ access point ที่มีความเข้มสัญญาณสูงโดยอัตโนมัติ ทำให้มีการปลอม access point ที่มีสัญญาณแรงๆไว้ 
- จะมีการ set proxy แล้วเก็บข้อมูลต่างๆไว้
- prevent -> authentication

### Concludes
- theres a lot of network attack but all uses **"exploit"** 
- we need to understand what these "exploit" uses so we can came up with the defence mechanism
- and uses all those concepts that we learn CIA/AAA/PDR
