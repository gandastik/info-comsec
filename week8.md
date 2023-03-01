## Firewall 🔥
- is both hardware and software
- listen to **network layer** (or other layer too)
- firewall - สามารถมอง "network data" ที่ส่งผ่านกันใน network ได้ทั้งใน physical, data link, network, application 
	- prevent: เป็นการ prevent สิ่งที่รู้ว่าผิดปกติ
	- detect 
	- reponses: drop packet 📦
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
- switch based
	- from the switch industry
	- pros
		- fast
		- multiple ports (switch based)
	- cons
		- simple policy (cant detect/prevent complex attack)
- appliance based
	- from board industry
	- with OS (Linux) customized to support network operation
	- slow forwarding rate, low bandwidth, less ports, low **firewall bandwitdh**
	- can config complex policy
	- can link with other systems (eg. authen)
- 😵 wtf is a firewall bandwidth you may ask .... its a **amount of traffic after being filtered by a firewall per second ** 🤓
- **host based firewall** - firewall at your device (3 layers needed: transports, network, data link)
	- personal firewall

#### Q: can firewall prevent viruses ?
- in some case
- firewall is different than antivirus
- when something pass firewall - firewall cant do shit anymore
	- so if some shady shit do some shady thing to pass firewall then we're fucked so thats why antivirus comes in

#### Q: what are the threats firewall can and can't prevent
- network attack that has pattern. header shit
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
- stateful inspection
- application proxy
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