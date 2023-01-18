## CIA AAA PDR

### History of Security
![](https://media.discordapp.net/attachments/1014398974649708624/1065099098807615529/image.png?width=948&height=685)
- **1975** -> TCP/IP + some basic protocols
	- RFC of these protocols have **no security mentioned**. Only focused on connectivity
	- simple attacks eg. worms
- **Attacks** becoming more dangerous when e-commerce begin to rise
	- around when **NAT** (Network Address Translation) was born
- 1997 ~ 2000s -> **Security** are more and more mentioned 
	- but still is a **optional** choices
- more and more time passed. security problems are still becoming more popular because of the **old protocols** that are the backbone of the system
- **CIA/AAA/PDR** concepts were born to use in security assessment
- 1998s -> the concepts above still not a final answer to the problems because it only focuses on the IT devices
	- NIST SP8000 - Procedures
	- ISO17799 -> ISO27001 to becoming a security standard in the organization
		- determine the organization department eg. CISO, security personels
- **"now"** -> we have "un-secured" protocols and "secured" protocols working together so the  security problems are occured because of the "un-secured" protocols
	- now technoly based on the "un-secured" protocols
	- ISO270001 -> more jobs for security department
	- next upcoming tech will becoming based on **"secure design"**

### สภาวะที่ระบบมีความปลอดภัย
- **การบุกรุก**
- **การที่ระบบสามารถทำงานได้อย่างต่อเนื่อง**

### ภัยคุกคามสารสนเทศ
- **Incident**: เหตุฉุกเฉิน
	- เหตุเล็กๆที่ทำให้เกิดปัญหา**ชั่วคราว**
- **Disaster**: ภัยพิบัติ
	- เหตุที่ทำให้เกิดปัญหา**ระยะยาว** eg. flood, fire
- แล้วแต่ admin ว่าจะ declare เป็นระดับไหน

### Security Concept
#### CIA
- **Confidentiality**
	- "ข้อมูลใดที่เป็นความลับ จะต้องไม่ถูกเปิดเผยให้กับบุคคลอื่นที่ไม่มีสิทธิในการอ่านข้อมูลดังกล่าว"
	- แนวทาง -> "encryption" แล้วให้บุคคลที่มี key/password สามารถ "decryption" ข้อมูลได้
	- ชนิดข้อมูล
		- **stored data**
		- **network in-flight data**
	- **Encryption**: คือกระบวนการเปลี่ยน plain text -> cipher text
		- 2 Cryptography
		1. Symmetric Cryptography: use same key to encrypt and descrypt
			- the longer the key length the more secure it gets
			- problem is **the exchanging of key** to src. and dest.
			- algorithms: DES(52 bit) -> AES (128+ bit) ปลอดภัยกว่า Asymmetric
		2. Asymmetric Cryptography: use different key to encrypt and descrypt
			- one key to encrypt, one key to decrypt
			- private key to encrypt & public key to decrypt -> "verification of the src." public key จะรู้ว่าใครเป็นเจ้าของ
			- public key to encrypt & private key to decrypt -> เข้ารหัสข้อมูล
			- algorithms: **RSA**
	- Application
		- VPN, SSL, Email, File Encryption
	- ข้อมูลที่มีความสำคัญถูกเปลี่ยนเป็นข้อมูลที่อ่านไม่ออก
- **Integrity**
	- "ข้อมูลต้องมีความถูกต้อง สมบูรณ์ ไม่ถูกเปลี่ยนแปลง แก้ไข"
	- แนวทางคือ การเพิ่มข้อมูล/กลไก ในการตรวจสอบความถูกต้องของข้อมูล
		- Validate: เช็คว่าข้อมูลถูกต้องมั้ย
		- Verification: เช็คว่าใครเป็นเจ้าของ
	- digital signature: คือการ verify ว่าข้อมูลถูกต้องไม่มีการเปลี่ยนแปลง
		- **CA** (Certificate Authority): เป็นคนเดียวที่ gen key ได้เท่านั้น จะได้ = (public key + private key + cert)
		- **Sender** {public, private key}: (data) -> hash -> (fingerprint) -> encrypt w/private key -> (digital signature) -> send (data), (digital signature + public key)
		- **Receiver** {public key from Sender at the same time with digi sig.}: 
			- **verify the sender** by sending the given cert to the CA to verifed (the key are from whom?, the key is still valid, guarantee the sender existence)
			- (data) -> hash -> (fingerprint)
			- (digi sig.) -> decrypt w/public key -> (fingerprint)
			- then **compare the fingerprint** to **verify the integrity** + verify the sender
	- ถ้าต้องการ confidentiality ด้วยจะให้ฝั่ง dest. ส่ง public key + cert ไปยัง sender ตอนเริ่มต้น เพื่อให้นำไปใช้ในการ encrypt data
	- algorithm: hashing, msa, rsa
	- กลไกการทำงาน -> **Digital Signature** with **CA**
- **Availability** to be cont.