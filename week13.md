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