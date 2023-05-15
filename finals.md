## CIA/AAA/PDR

### CIA

#### Confidentiality
- "ข้อมูลใดที่เป็นความลับ จะต้องไม่ถูกเปิดเผยให้กับบุคคลอื่นที่ไม่มีสิทธิในการอ่านข้อมูลดังกล่าว"
- แนวทาง -> "encryption" แล้วให้บุคคลที่มี key/password สามารถ "decryption" ข้อมูลได้
	- ชนิดข้อมูลที่เกี่ยวข้อง: stored data, network in-flight data
- **Encryption**: process that change plain text -> cipher text (ข้อมูลที่มีความสำคัญถูกเปลี่ยนเป็นข้อมูลที่อ่านไม่ออก)
	- 2 type of Cryptography
	- Symmetric Cryptography: use same key to encrypt and decrypt
		- the longer the key length the more secure it gets
		- problem is that the exchanging of the key to src. and dest. is complicated
		- algorithms: DES(52 bit) -> AES(128+ bit) **ปลอดภัยกว่า Asymmetric**
	- Asymmetric Cryptography: use different key to encrypt and descrypt
		- one key to encrypt, one key to decrypt
			- private key to encrypt & public key to decrypt -> **"verification of the src."** public key ที่ปลดล็อกได้ หมายความว่าจะรู้ได้ว่ src คือใคร
			- public key to encrypt & private key to decrypt -> **"เข้ารหัสข้อมูล"**
			- algorithm: RSA
	- Application
		- VPN, SSL, Email, File Encryption

#### Integrity
- " ข้อมูลต้องมีความถูกต้อง สมบูรณ์ ไม่ถูกเปลี่ยนแปลง แก้ไข"
- แนวทาง -> การเพิ่มข้อมูล/กลไก ในการตรวจสอบความถูกต้องของข้อมูล
	- validate: เช็คว่าข้อมูลถูกต้องมั้ย
	- verification: เช็คว่าใครเป็นเจ้าของ
- **Digital Signature**: คือการ verify ว่าข้อมูลถูกต้องไม่มีการเปลี่ยนแปลง
	- CA (Certificate Authority) คือบุคคลเดียวที่ gen key ได้เท่านั้น ซึ่งจะได้ = (public key + private key + cert)
	- Sender มี public key, private key: data -> (hashing) = fingerprint -> (encrypt w/private key) = **digital signature** -> send *data* + *digital signature + public key*
	- Receiver ได้รับ data + public key & digital signature
		- verify the sender โดยส่ง cert ที่ได้รับไปให้ CA เพื่อ verify (the key are from whom?, the key is still valid, guarantee the sender existence)
		- data -> hash = *fingerprint*
		- digital signature -> decrypt w/public key = *fingerprint*
		- compare between the 2 fingerprints to **verify the integrity of data + verifty the sender**
	- ถ้าต้องการ confidentialiy ด้วยจะให้ฝั้ง dest. ส่ง public key + cert ไปยัง sender ตอนเริ่มต้น เพื่อให้นำไปใช้ในการ encrypt data
	- algorithm: hashing, msa, rsa
	- กลไกการทำงาน: Digital Signature with CA

#### Availability
- ระบบงาน/ข้อมูล ต้องสามารถเรียกใช้งานได้ตามข้อกำหนดในการบริการ (SLA: Service Level Agreement)
- แนวทาง -> การออกแบบระบบให้สามารถรองรับกับ
	- การเพิ่มของ load
	- การโจมตีของระบบ
	- อุบัติเหตุ ภัยพิบัติต่างๆ
- ทำให้ต้องมี Resource >= Load (มีการ predict load เพื่อที่จะจัดการกับ resource)
	- การ predict ที่ดีคือ ต้อง predict ให้มี gap ระหว่าง prediction กับ reality ให้น้อยที่สุด
	- 3 cases:
		- constantly load: return of investment (RoI) is good
		- load เพิ่มขึ้นแบบ linear: RoI is decent
		- suddent peak of load: ตัวอย่างเช่น สำนักทะเบียนวันลงทะเบียน -> ใช้ cloud
- incident ที่ส่งผลกระทบต่อ resource (HW, SW, Network, Data, People, Process)
	- พัง, หมดอายุ
	- ถูกโจมตี (Prevent, Detect, Response)

### AAA

#### Authentication
- "การเข้าใช้งานระบบ/ทรัพยากรใดๆ จะต้องเป็นผู้มีสิทธิ์ในการเข้าใช้งานระบบหรือทรัพยากรนั้นๆ"
- แนวทาง ->
	- what you know: password? การ matching ระหว่าง username & password
		- รองรับด้วยกฎหมายธุรกรรมอิเล็ก -> ธุรกรรมหลังจากทำ wyk แล้วจะถูกยอมรับโดยกฎหมาย
	- what you have: eg. id card
	- what you are: fingerprints, blood, dna, face?
- authen techniques in web technology
	- sessions-based: ให้ *token* เพื่อเป็นการยืนยันว่า log-in แล้ว โดยให้ user ถือ token ไว้ตลอดเวลา มองที่ connection ถ้าเปลี่ยน connection จะเปลี่ยน session
	- token-based: ไม่สนใจ connection คือเป็นการให้ token กับ user แล้วถูกเก็บไว้ที่ cookies
	- JSON web token (JWT): คือ token ในรูบที่สามารถแปะ payload ไว้ในตัว token ได้

#### Authorization
- "การเข้าใช้งานระบบหรือทรัพยากรใดๆ จะต้องระบุสิทธิการเข้าถึง และมอบสิทธิในการเข้าถึงนั้นกับผู้ใช้งาน"
- แนวทาง ->
	- การจัดการสิทธิ์กับแต่ละ user: วิธีที่แย่ เพราะเป็นการให้สิทธิ์ที่ละคน
	- Roled-based authorization: การเพิ่มสิทธิ์ให้กับ role จะทำง่ายขึ้น
		- eg. next gen firewall, proxy etc.
	- Access Control Lists (ACLs): ในด้าน network คือจับ src ip, dest ip แล้วกำหนด policy ว่า allow หรือ deny กับ service ต่างๆ

#### Accounting
- "การทำงานใดๆ จะต้องสามารถตรวจสอบได้ว่าเกิดขึ้นได้อย่างไร โดยใครส่งผลอะไร ฯลฯ"
- แนวทาง ->
	- log เมื่อมีการเรียกใช้คำสั่ง หรือเข้าถึงข้อมูล อาจจะกำหนดว่า user เข้าถึง table ไหน เฉพาะ table นี้ให้ log เท่านั้น
- log ต้องตามกฎหมายที่ support คือ all electronics can be use in court
	- แต่จำเป็นต้อง log ถึง ip ว่าใครทำอะไร ที่ไหน เมื่อไหร่
	- dev more functions to store more log about usage of functions, data -> put it in requirement specs

### PDR

#### Prevent
- "ภัยคุกคามที่ทราบว่าจะเกิดขึ้น จะต้องมีการกำหนดการป้องกัน"
- monitor -> collect all events
- ตั้งอุปกรณ์ป้องกัน eg. firewall, IPS (Intrusion Prevention System), Proxy, Anti-virus
	- firewall: pattern matching (network layer, transport layer)
	- IPS: เป็นการ follow tcp connection และ check pattern เพื่อดูความผิดปกติ (anomaly) in application layer check for attack, virus, และยังสามารถดู volume ได้ eg. DNS record per sec
	- proxy: in application layer
	- anti-virus: มองเหมือนเป็นไฟล์ (application layer)

#### Detect
- "ต้องมีกลไกในการตรวจสอบจับภัยคุกคาม และแจ้งเตือนให้ผู้ดูแลระบบ"
- why? - too much to prevent, not everything can be prevented
- คอยตรวจสอบที่ทรัพยากร ว่ามีความผิดปกติ -> alert -> แล้วค่อยแก้ปัญหา
- monitor -> alert when problem occurs
- detect from where?
	- network traffic
	- network request
	- I/O usage

#### Response
- "เมื่อมีการแจ้งเตือนจากขั้นตอนการ detect จะต้องมีการตอบสนองอย่างทันท่วงที"
- เมื่อไหร่ก็ตามที่ gap ระหว่าง detect กับ response มันเยอะ จะเกิดปัญหาแบบ exponential
- action/plan เมื่อไหร่ก็ตามที่เกิดเหตุ จะให้ทำอะไรบ้าง
- PDR คือการจัดการสื่งที่เกิดขึ้นในระบบ แสดงว่าต้องมี action

### "security is process not product"

![](https://media.discordapp.net/attachments/1014398974649708624/1067665960229679134/image.png?width=1057&height=685)

## Computer Network & Network Attack

### Site Connection Diagram
![](https://media.discordapp.net/attachments/1014398974649708624/1075256211957616741/image.png?width=1229&height=702)

### Switch Network Diagram
- describe how switch connected to each other to describe **VLAN**
![](https://media.discordapp.net/attachments/1014398974649708624/1075256635649445969/image.png?width=1069&height=702)

#### Device Connection Diagram
![](https://media.discordapp.net/attachments/1014398974649708624/1075257049249742898/image.png)
- will come with seperate sheet to even give more detail about what device connected to what device at which port
![](https://media.discordapp.net/attachments/1014398974649708624/1075257241927692319/image.png)
- implementing VLAN คือการที่ทำ virtual lan ด้วย switch โดยที่กำหนด segment ของ port ของ switch ให้มองว่าอยู่ network เดียวกัน โดย switch ก็จะถูกเชื่อมด้วย router ตัวเดียวกัน โดยให้ทางที่เชื่อมต่อกันระหว่าง router เป็น trunk link (allow all VLAN) (sadly I kinda forgot all of this 😢)
![](https://media.discordapp.net/attachments/1014398974649708624/1075259495028105286/image.png?width=748&height=702)

#### Example of Physical Diagram
![](https://media.discordapp.net/attachments/1014398974649708624/1075261652385144882/image.png?width=990&height=702)

![](https://media.discordapp.net/attachments/1014398974649708624/1075262826110787593/image.png?width=1440&height=679)

### Network Attack & Solution
- Threats: ภัยคุกคาม
- Vulnerability
	- is a property
	- is an un-expected "feature" in the system
- Exploit: การอาศัยช่องโหว่เพื่อโจมตีระบบ
	- has to be a vulnerability

#### Type of Malware
- spam
- computer viruses
- worms
- trojan horses
	- key logger
	- cache
- spyware
- ransomeware
- adware
	- ads pop-up
	- everything that is free nowadys is consider to be "adware" (in-app purchase)


#### Q: How can we prevent/fix the malware? 🤔
- ในปัจจุบันมีการใช้ IPS (Intrusion Prevention System) หรือต่างๆ โดยที่มีการใช้หลักการ **signature base**
	- antivirus "ez money"
	- คือการเก็บ pattern ต่างๆที่รู้ของ virus ต่างๆ
	- โดยจะรู้ virus signature ต่างๆได้ก็จำเป็นต้องเจอ virus ตัวๆนั้นก่อน แล้วส่ง update ต่างๆเรื่อยๆ
- **anomaly base** -> Firewall
	- แต่ทั้งหมดก็เกิด false positive กับ false negative ได้
- detection system (IDS, IPS, Antivirus) -> catch these mothersuckas
	- still error prone

#### Sniffer
- sniff packets that is in-flight
	- catch from data-link layer
- NIC -> Promiscuous Mode - ทำให้เราได้ข้อมูลของ network
- HUB -> you just need to only install 1 sniffer at one of the interface in HUB
- Switch -> hard to choose a place to install (didnt broadcast to all port like HUB)
	- ถ้าในกรณีที่ switch ไม่สามารถเก็บ MAC addr. ได้ไม่ครบใน network -> switch จะทำหน้าที่คล้ายกับ HUB
	- **attacker** 😎 -> flood switch mac addr. -> switch turns to hub -> ez sniffer installed
	- **in present day** switch can detect ARP flood from which port and then disable that port 😎

#### Q: how can we protect / prevent sniffing data ?
- using security concept about data -> **Confidentiality & Integrity**
	- encrypt data 🔥

#### DoS
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

#### DDoS
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

#### Q: How can we prevent/protect against Exploits
- we cant
- only way is to upgrade/update system

#### TCP/IP Hijacking
![](https://media.discordapp.net/attachments/1014398974649708624/1077810144898977853/image.png?width=1130&height=685)
#### Session Hijacking Tool
![](https://media.discordapp.net/attachments/1014398974649708624/1077810689839747102/image.png?width=1196&height=685)
- prevent -> integrity : given the src generate hash code and send to dest to compare to check if the data has been changed or not

#### Q: prevent/protect session hijack
- expire time

#### Rouge Access Point
![](https://media.discordapp.net/attachments/1014398974649708624/1077812691852349460/image.png)
- access point - จะเป็นการส่ง beacon frame ออกมาตลอดเวลา
- หลักการ -> ปกติแล้วมีการเชื่อมต่อกับ access point ที่มีความเข้มสัญญาณสูงโดยอัตโนมัติ ทำให้มีการปลอม access point ที่มีสัญญาณแรงๆไว้ 
- จะมีการ set proxy แล้วเก็บข้อมูลต่างๆไว้
- prevent -> authentication

#### Concludes
- theres a lot of network attack but all uses **"exploit"** 
- we need to understand what these "exploit" uses so we can came up with the defence mechanism
- and uses all those concepts that we learn CIA/AAA/PDR

## Firewall
- is both hardware and software
- listen to network layer (or other layer too)
- firewall - สามารถมอง "network data" ที่ส่งผ่านกันใน network ได้ทั้งใน physical, data link, network, application
	- prevent
	- detect
	- response: drop packet

#### Q: what are the important header fields during a network transmission
- A: in data link layer protocol is IEEE 802.3 -> MAC address (src, dest)
- network layer: IP address (src, dest), ID, offset, fragment flag (when MTU between 2 side is different) and ICMP: type, code
- transport layer: TCP, UDP -> port (src, dest), seq#, ack#, window size, flag (tcp state machine)
#### Q: what are the attacks, invades of the network ⚔
 - แต่ละการโจมตีมันเกี่ยวข้องกับ header field ใดบ้าง มีลักษณะเป็นอย่างไร
- DoS:
	- SYN Flood: ส่ง packet ปริมาณมากที่มีการตั้ง SYN flag
	- Land Attack: ส่ง ICMP ที่มี src ip = dest ip
	- Fragmentation Attack: ส่ง IP ที่มีการ fragment แต่ประกอบกันไม่ได้ (id, fragment flag, offset)

![](https://media.discordapp.net/attachments/1014398974649708624/1080328555818405969/image.png?width=990&height=685)

### Firewall = Network Filtering
- filter **"data"** in network
![](https://media.discordapp.net/attachments/1014398974649708624/1080328884672794634/image.png)
- ป้องกันภัยคุกคาม และกำหนดนโยบายการเชื่อมต่อ
	- deny the pattern of the attack
	- กำหนด network A ห้ามเข้าไป network B
	- สามารถมองภาพรวมได้ว่า มีการส่ง packet ที่แยกๆกันมา แต่พอมารวมกันแล้วเป็นอันตรายได้ ก็จะเกิดการห้ามไม่ให้ส่งต่อ

#### Which one is Firewall
![](https://media.discordapp.net/attachments/1014398974649708624/1080331009020678184/image.png)
- you cant tell yet! - **need to see datasheet** (if filtering or access control available)
- but incase of a managment switch (L2) -> there will be some kind of filtering
	- MAC address filtering
- layer 3 switch -> packet filtering firewall (mostly)

### ลักษณะทางกายภาพของ Network Firewall
- **appliance**, **switch based**
- looks like switch
- has multiple interfaces (firewall switch based)
- ทำได้ทั้ง L2 -> VLAN, L3 -> routing + filtering
- **switch based**
	- firmware
	- from the switch industry
	- pros
		- fast
		- multiple ports (switch based)
	- cons
		- simple policy (cant detect/prevent complex attack)
- **appliance based**
	- from board industry
	- with OS (Linux) customized to support network operation
	- slow forwarding rate, low bandwidth, less ports, low **firewall bandwitdh**
	- can config complex policy
	- can link with other systems (eg. authen)
- 😵 wtf is a firewall bandwidth you may ask .... its a **amount of traffic after being filtered by a firewall per second ** 🤓
- **host based firewall** - firewall at your device (3 layers needed: transports, network, data link)
	- sits inbetween network layer and transport layer
	- program or service that runs on the pc
	- personal firewall

#### Q: can firewall prevent viruses ?
- in some case
- firewall is different than antivirus
- when something pass firewall - firewall cant do shit anymore
	- so if some shady shit do some shady thing to pass firewall then we're fucked so thats why antivirus comes in

#### Q: what are the threats firewall can and can't prevent
- network attack that has pattern. header and shit
- firewall can only prevent network attack from network layer, transport layer
- can't interfere with content of application layer

![](https://media.discordapp.net/attachments/1014398974649708624/1080338767547748372/image.png)
#### Q: can firewall control the connection between A -> B
- no because A and B are in the same network
#### Q: can firewall control the connection between A -> D
- yes

#### Q: when was firewall policy developed, before or after the threats
- firewall happened because of the attack. in the present time firewall can't event prevent all threats (mostly 60-70%)

### Types of Firewall
- packet filtering
	- มองดู header ของ packet (src ip, dest ip) on network layer
	- basic and simple -> fast
	- literally just a router feature
- stateful inspection
	- กำหนด state ใน policy ได้
- application proxy
	- "proxy"
- next generation firewall
	- integrated system
	- behavior-based

### Firewal Policy
- **allow all / deny some**
	- ใช้กับอุปกรณ์ที่ง่ายต่อการใช้งาน - "plug and play"
- **deny all / allow some**
	- default last rules -> deny any:any (src:dest) (cisco)
- which way is more secure?
	- obviously **deny all / allow some**

#### Packet Filtering Policy
- filter zone to zone
- ip, port, flag, action (allow, deny)
![](https://media.discordapp.net/attachments/1014398974649708624/1080343996984995942/image.png)

#### Stateful Inspection Policy
- ip
- port
- protocol
	- TCP, UDP, ICMP, application level (FTP, HTTP, multimedia)
- state
- action (allow, deny)
- use cases: block ragnarok
	- สามารถกำหนดให้ block port เฉพาะของมัน แล้ว block หลังจาก state == connected ไป + เพิ่ม delay ได้อีกด้วย

### Application Proxy Policy
![](https://media.discordapp.net/attachments/1014398974649708624/1085409543711883415/image.png?width=674&height=685)
- src ip, dest ip 
- application protocol (http, mail, dns, any)
- application services (kazza, edonkey, facebook, google-talk)
- action (allow, deny)
- act as a "proxy"
	- เชื่อมต่อกับ src. ให้เสร็จก่อน
	- หลังจากนั้นสร้าง connection ไปยัง dest.
	- กัน DoS attack ได้ (prevent ~70%)
	- cons: dest. จะไม่รู้ว่าใคร connect มา
- เช็ค application แล้วกำหนดได้ว่าให้ใช้ application อะไรที่กำหนดไว้ใน rule-set ได้
- use-case: block bittorrent (detected by application firewall)

### Next Generation Firewall
- classify all traffic, across all ports, all the time
- reduce the threat footprint, prevent cyber attacks
- map appliation traffice and associated threats to users and devices
- applications, contents, users, and devices - **all under control**
![](https://media.discordapp.net/attachments/1014398974649708624/1085410236996780032/image.png)
- map between user and application column
- profile column is an action responding to the policy
- implement with authentication + role-based user => need identity management

### Activity
![](https://media.discordapp.net/attachments/1014398974649708624/1085410811675168798/image.png)
- threats             |  packet filtering   |  stateful inspection  |  application proxy | firewall NG |
- port scans:      |            no              |                yes             |              yes            |        yes
- virus (scripted):            no              |                no              |               no             |         no
- DoS | no | yes | yes | yes
- Bittorrent: no | no | yes | yes

### Assignment (?) 🤯
![](https://media.discordapp.net/attachments/1014398974649708624/1085417504567988315/image.png?width=652&height=702)

#### Hints
![](https://media.discordapp.net/attachments/1014398974649708624/1085418949396680734/IMG20230315112650.jpg?width=1248&height=702)

### Q:
![](https://media.discordapp.net/attachments/1014398974649708624/1085420415482085466/image.png)
- any firewall R1, R2, R3
	- best recommended at input interface of R1 Firewall 🔥

### Q:
![](https://media.discordapp.net/attachments/1014398974649708624/1085420935357677588/image.png)
- input inteface of both R1 and R4 firewall 🔥

### Q: if Firewall has too many policies how to prioritize the policy
- use money

### Q: Duplicate policy in firewall 
- เมื่อก่อนมีปัญหาทำให้ต้องเกิดการเช็ค policy ซ้ำ อาจจะทำให้เกิดการทำงานช้า
- ในปัจจุบันมีความฉลาดมาก สามารถเช็คการ conflict ของ policy ได้

### Firewall Zone 🔥
- แยก Zone ของเครือข่ายตามความเสี่ยง หรือบทบาทแล้วนำ firewall กั้นระหว่างเครือข่าย เพื่อกำหนดกฏรักษาความปลอดภัย
- recommend: ให้มีการแบ่ง 3 zone ตามนี้
	- กำหนดให้ untrusted <-> DMZ <-> trust เป็น flow ที่ปลอดภัย
- **Untrusted Zone**
	- cann't control user
	- anyone can use the network
	- eg. public service server, webserver, FTP server, wifi network
- **DMZ Zone**
	- demilitarized zone: 50/50 zone
	- eg. proxy,
- **Trust Zone**
	- รู้ user
	- รู้การใช้งาน function ต่างๆ

### Firewall Design

#### Multi-leg
![](https://media.discordapp.net/attachments/1014398974649708624/1085425211358318632/image.png)
- need to deny all connection between **untrusted and trusted network** -> cons of multi-leg firewall
- everything from **untrusted network** need to pass through **DMZ zone** before enter **internal trusted zone**

#### Sandwich (recommended)
![](https://media.discordapp.net/attachments/1014398974649708624/1085425956770041977/image.png)
- very secure -> basically like 2 doors
- basically forces **untrusted zone** reach **DMZ** before reaching **trusted zone**

#### Layered Firewall
![](https://media.discordapp.net/attachments/1014398974649708624/1085426467539787816/image.png?width=938&height=702)
- aka multi-layered firewall
- **high availability** and **high security**
	- HA: firewalls need to be the same
- "layered" -> layer of untrusted, 
- **recommended**: firewall should be different provider/manufacturors
	- bc if all fws are the same -> 1 bad vulnerability is all it takes 🃏

#### Deployment
- @Router
- In-Line mode (best recommended)

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

## Incident and Response
- การวางแผนรับมือสำหรับเหตุการณ์ฉุกเฉิน -> ความพร้อม 😎
- การจัดเตรียมอุปกรณ์ในสารสนเทศให้พร้อมกับ incidents

### เหตุฉุกเฉิน vs ภัยพิบัติ
- เหตุฉุกเฉิน (incident) ทำให้บริการหยุดชะงักไปชั่วคราว หรือทำงานได้ช้าลง แต่ยังสามารถไปยังถึงเป้าหมายได้อยู่
	- เสียหายวงจำกัด
	- requirement in ISO27001
- ภัยพิบัติ ทำให้ sw/hw/network/process/data/people ทุกอย่างสูญเสีย สูญหายไม่สามารถทำงานต่อได้
	- eg. ภูเขาไฟ, ไฟไหม้, สึนามิ

### แผนรับมือเหตุฉุกเฉิน
- incident response plan -> automatic, readiness
- รายละเอียดของระบบงาน
- บุคคลกร
	- ตำแหน่ง: ความสามารถ
- การเตรียมการก่อนเหตุเกิด (สถานะของเครื่องมือ, กระบวนการเตรียมความพร้อมรับมือ)
- เหตุฉุกเฉิน 1
	- การระบุเหตุฉุกเฉิน
	- การดำเนินการเมื่อตรวจพบเหตุฉุกเฉิน
	- การดำเนินการหลังจัดการเหตุฉุกเฉิน
- เหตุฉุกเฉิน 2
	- การระบุเหตุฉุกเฉิน
	- การดำเนินการเมื่อตรวจพบเหตุฉุกเฉิน
	- การดำเนินการหลังจัดการเหตุฉุกเฉิน

## Web Security
![](https://media.discordapp.net/attachments/1014398974649708624/1093003106893168731/image.png?width=931&height=685)
- **proxy**
	- **forwarding proxy** (client side) (middle man)
		- filtering (acls)
		- redirector
		- caching
	- **reveres proxy** (server side): client ต้อง request เข้าหา proxy เท่านั้น
		- load balancing (for redundancy)
		- security
		- DDoS protection
		- session management (ระหว่าง client A กับ server A)

### การบุกรุกระบบ
- web app: session, etc.
- server 
- find vulnerability using scanning software such as nmap 
	- find version of the software -> find the vulnearbilty of that version
- exploit the vulnerability: what can we do next?

### What is vulnerability
- ความเสี่ยงที่หลีกเลี่ยงไม่ได้
- patch ช่องโหว่ โดย dev
- แค่เป็นช่องโหว่ ยังไม่มีความเสียหายมากมาย

### What is exploit
- อาศัยช่องโหว่ ไปทำอะไรบางอย่างได้
- ต่อยอด
- eg. heartbleed - openSSL exploit, shellshock - bash exploit

### Activity
#### find CVE that has CVSS > 8.0
1. php v 7.4.27, 8.0.14, 8.1.1
	- CVE-2018-19518 CVSS: 8.5 [url](https://www.cvedetails.com/cve/CVE-2018-19518/)
2. apache 2.4.52
	- CVE-2022-24705 CVSS: 10.0 [url](https://www.cvedetails.com/cve/CVE-2022-24706/)
	- CVE-2022-22720 CVSS: 7.5 [url](https://www.cvedetails.com/cve/CVE-2022-22720/)
3. mariadb 10.4.22
	- CVE-2021-27928 CVSS: 9.0 [url](https://www.cvedetails.com/cve/CVE-2021-27928/)
4. perl 5.32.1 (none found > 8.0)
5. openssl 1.1.1m (unix only)
	- CVE-2016-6309 CVSS: 10.0 [url](https://www.cvedetails.com/cve/CVE-2016-6309/)
6. phpMyAdmin 5.1.1
	- CVE-2016-6629 CVSS: 10.0 [url](https://www.cvedetails.com/cve/CVE-2016-6629/)

## Wireless LAN Security
### Wireless LAN model
![](https://media.discordapp.net/attachments/1014398974649708624/1098061696750321744/image.png)
- เน้นไปที่ **IEEE802.11** (Protocol for wireless network)
- ทำงานอยู่บน Physical Layer && Data link layer (MAC)
- **2 mode**
	- **ad-hoc mode** : connect automatically (no need for switch)
		 - 4 set of MAC address (to make it connect automatically)
	- **infrastructure mode**:
- **access point**: เปลี่ยน 802.11 (wireless) <-> 802.3 (wired)
	- "bridge": ระหว่าง protocol ที่ต่างกัน
- **802.11** -> need Authentication, Authorization + there will be a MITM attacks

### IEEE 802.11
![](https://media.discordapp.net/attachments/1014398974649708624/1098076331478106252/image.png)
- 802.11a : freq = 5GHz
- 802.11n : 2008, 72 - 600 Mb/s, 2.4or5GHz
- 802.11ac : 2014, 433 - 6933 Mb/s, 5GHz

#### Channel
![](https://media.discordapp.net/attachments/1014398974649708624/1107719655965073490/image.png)
- จากรุปเป็นของ 2.4GHz
- AP ทำงานตาม channel ที่เลือกไว้
	- ถ้าเกิดมี device ที่ใช้ channel เดียวกัน จะเกิดการกวนกัน
	- ทำให้เกิดการใช้ข้าม 1->6->11
 
#### Tools
- wifi analyzer: check the health of wifi signal around the area
- vistumbler

#### Keywords
- Wi-Fi: alliance of the network กลุ่มเจ้าของผลิตภัณฑ์คอยตรวจเช็ค -> wifi certificated
- CSMA/CA: Carrier Senses Multiple Access (Collision Avoidance) 
- MAC Filtering: data link layer (filter the mac ip -> allow or deny)

### Basic Security of 802.11
- Authentication -> WEP
- Encryption -> WEP
- Integrity -> WEP
- Access Control -> Mac Filtering

### Discovery
#### Open Network
- AP: regulary send **beacon signals**
- devices received the info(SSID) -> send association req
- AP *accepts* (check Mac Filtering - allow or deny) -> send association resp 
- connected
#### Close Network
- AP: not sending **beacon signals**
- node need to send **probe req**
- AP check SSID -> send **probe resp**
- sender association req - ap association resp
- connected

### User Authentication
- Open System Authentication
	- authentication ให้กับทุกคนที่ request
	- ไม่มีรหัสผ่าน
- shared-key authentication
	- use key to authentication
![](https://media.discordapp.net/attachments/1014398974649708624/1107724913399320747/image.png)
- cons: MITM

### WEP: Wire Equivalent Privacy (WEP)
- 802.11b
- confidentiality: 40bit encryption key
	- RC4 algorithm
- access control
	- shared-key authentication + encryption
- data integrity
	- checksum every message
![](https://media.discordapp.net/attachments/1014398974649708624/1107726126379450388/image.png)
- vulnerability
	- find 2 message that have the same 2 key id -> reverse to find key > we all doomed 💀
- 802.11 need to evolve
	- increase length of id (less chance to have same id)
	- WiFi -> announce to use WPA (WiFi Protected Access) in 2003 
	- in 2004 -> WPA2 IEEE 802.11i

### WPA
- fix vulnerabilty in WEP
- update firmware from the old device of 802.11
- user authentication
- 2 mode:
	- WPA enterprise: TKIP/MIC ; 802.1X/EAP
	- WPA personal: TKIP/MIC ; PSK
- Authentication ใช้ 802.1x/EAP
	- ดูแลตั้งแต่ src ถึง access point
- RADIUS protocols ในการทำ AAA -> key distributions
	- passwords and digital certificates
	- eg. TLS, TLLS: cerficates based methods or PEAP, LEAP: passwords based methods
- encryption: TKIP
	- encapsulate (based on) WEP
	- use RC4-Engine like WEP
	- protect spoofing
	- pros: separate key of encryption in differnt packets
		- longer keys
![](https://media.discordapp.net/attachments/1014398974649708624/1107728186839670904/image.png)

### WPA2
- 802.11i
- use AES encryption algorithms -> utilizing Hardware
- enterprise mode -> 802.1X/EAP authenticaion, AES-CCMP for encryption
- personal mode -> PSK for authentication, AES-CCMP for encryption
- AES key 128bits
- encryption loop 10 times
- AES uses CCMP protocols
![](https://media.discordapp.net/attachments/1014398974649708624/1107728863611584522/image.png)

### Comparision of the standards
![](https://media.discordapp.net/attachments/1014398974649708624/1107729028070264873/image.png)

### Q: Wireless affects IT system?
- wireless is exposes to public -> untrusted
### Q: 802.11 is good enough for IT system?
- yes
- authenticaion and shits 
### Q: 802.11 can not deal with what?
- other layer, eg. sessions hijacking, application layer (virsus etc.)
- only deal with physical layer, data link layer
- make wireless network more like wire network (cannot just sniffs stuff out of thin air anymore)

### Q: x devices what wireless security standards should be implemented 🥱 (probably on exams)
- 1-10: 
- 20-60: 
- 200+: 

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
![](https://media.discordapp.net/attachments/1014398974649708624/1107522614341152819/687474703a2f2f656c6561726e696e672e6c616d70616e6776632e61632e74682f6d6f6f646c652f706c7567696e66696c652e7068702f393538302f6d6f645f706167652f636f6e74656e742f312f726177636f6d2e6a7067.png)
