## Firewall 🔥🗿(Cont.)

### Application Proxy Policy
![](https://media.discordapp.net/attachments/1014398974649708624/1085409543711883415/image.png?width=674&height=685)

- src ip, dest ip 
- application protocol (http, mail, dns, any)
- application services (kazza, edonkey, facebook, google-talk)
- action (allow, deny)

### Next Generation Firewall
- classify all traffic, across all ports, all the time
- reduce the threat footprint, prevent cyber attacks
- map appliation traffice and associated threats to users and devices
- applications, contents, users, and devices - **all under control**

![](https://media.discordapp.net/attachments/1014398974649708624/1085410236996780032/image.png)
- map between user and application column
- profile column is an action responding to the policy

### Activity
![](https://media.discordapp.net/attachments/1014398974649708624/1085410811675168798/image.png)
- threats        |  packet filtering   |  stateful inspection  |  application proxy | firewall NG |
- port scans: no | yes | yes | yes
- virus (scripted): no | no | no | no

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
- Untrusted Zone
	- cann't control user
	- anyone can use the network
	- eg. public service server, webserver, FTP server, wifi network
- DMZ Zone
	- demilitarized zone: 50/50 zone
	- eg. proxy,
- Trust Zone
	- รู้ user
	- รู้การใช้งาน function ต่างๆ

### Firewall Design

#### Multi-leg
![](https://media.discordapp.net/attachments/1014398974649708624/1085425211358318632/image.png)
- need to deny all connection between **untrusted and trusted network** -> cons of multi-leg firewall
- everything from **untrusted network** need to pass through **DMZ zone** before enter **internal trusted zone**

#### Sandwich
![](https://media.discordapp.net/attachments/1014398974649708624/1085425956770041977/image.png)
- very secure -> basically like 2 doors


#### Layered Firewall
![](https://media.discordapp.net/attachments/1014398974649708624/1085426467539787816/image.png?width=938&height=702)
- "layered" -> layer of untrusted, 