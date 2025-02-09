## NMAP
nmap หรือ network mapper คือ เครื่องมือopen-sourceที่ใช้ในการแสกนโครงข่ายระบบเน็ตเวิร์ค ที่สามารถแสกนได้ทั้ง service ,name รวมไปถึง version (หากสามารถแสกนได้) 
###  Host Recovery
ในส่วนนี้จะพูดการค้นหา hosts ต่างที่เราต้องการจะทดสอบ วิธีที่ดีที่สุดในการค้าหา คือ มองหาจาก ICMP echo request (ICMP = Internet Control Message Protocol) และทุกครั้งที่ทำการแสกน แนะนำให้ทำการบันทึกไฟล์เหล่านั้นไว้ เพื่อที่จะสามารถนำข้อมูลเหล่านี้มาประกอบการเขียน report ในอนาคตได้
*single target* 
```shell-session
$ sudo nmap 10.129.2.0/24 -sn -oA tnet 
```
*maltiple target*
```shell-session
$ sudo nmap -sn -oA tnet 10.129.2.18 10.129.2.19 10.129.2.20
```

| **options** | **Description**         |
| ----------- | ----------------------- |
| -sn         | ปิดใช้งานการแสกน port   |
| -oA tnet    | บันทึกลงในไฟล์ชื่อ tnet |
### Host and Port scan
port เปรียบเสมือนถนนแต่ล่ะสาย ส่วน hosts เปรียบเสมือนเมืองใหญ่ ทุกสิ่งที่ต้องการเข้ามายัง hosts ต้องผ่าน port ที่เฉพาะเจาะจงสำหรับเรื่องนั้นๆโดยตรง ซึ่ง port จะถูกแบ่งออกเป็น 2 ชนิดหลักๆ ได้แก่ TCP(Transmission Control Protocol) และ UDP (User Datagram Protocol)
#### scanning TCP port
Transmission Control Protocol หรือ TCP -> port ที่มักจะถูกใช้ในการเชื่อมต่อที่ต้องการความน่าเขื่อถือ
สำหรับการใช้ nmap ในการแสกนหา port TCP จะเป็นไปดังนี้
```shell-session
$ nmap 10.129.2.28 -sT
```

```shell-session
$ sudo nmap 10.129.2.28 -sS
```
จากทั้งสองตัวอย่าง สามารถใช้ในการสแกนหา port TCP ได้เหมือนกัน แต่จะแตกต่างกันตรงที่ `-sS` จำเป็นต้องใช่สิทธิ์ `sudo` เพื่อเรียกใช้งานต่างจาก `-sT`ที่สามารถใช้งานได้เลย รวมทั้ง `-sS` ยังสามารถแสกนได้เร็วกว่าอีกด้วย หลักการทำงานของ `-sS`  คือจะทำการสร้างแพ็คเก็ตขึ้นมาแล้วส่งออกไป เพื่อเริ่มต้นการเชื่อมต่อ แต่จะำม่สร้างการเชื่อมต่อเป้นเต็มรูปแบบ ทำให้ในบางครั้ง server จะไม่สามารถบันทึก log ณ ส่วนนี้เอาไว้ได้ และสามารถผ่าน firewall ไปได้โดยไม่ถูกตรวจจับ
```shell-session
Starting Nmap 7.80 ( https://nmap.org ) at 2020-06-15 15:45 CEST
SENT (0.0381s) TCP 10.10.14.2:60277 > 10.129.2.28:139 S ttl=47 id=14523 iplen=44  seq=4175236769 win=1024 <mss 1460>
SENT (1.0411s) TCP 10.10.14.2:60278 > 10.129.2.28:139 S ttl=45 id=7372 iplen=44  seq=4175171232 win=1024 <mss 1460>
Nmap scan report for 10.129.2.28
Host is up.

PORT    STATE    SERVICE
139/tcp filtered netbios-ssn
MAC Address: DE:AD:00:00:BE:EF (Intel Corporate)
```
จากตัวอย่างข้างต้น จะสังเกตุเห็นได้ว่า มีการกรอง(filtered) จากส่วนนี้อาจมีหลายสาเหตุเช่น ถูกfirewall ตรวจจับ หรือ อาจจะตกหล่นไป โดยทั้วไปแล้ว nmap จะทำการส่งที่ 10 แพ็คเก็ต เพื่อดูว่า แพ็คเก็ตก่อนหน้าถูกจัดการหรือไม่
#### scanning UDP port
User Datagram Protocol หรือ UDP -> เป็นprotocol ที่เน้นความรวดเร็วแต่จะไม่รับประกันเรื่องความถูกต้องของข้อมูล protocol ชนิดนี้มักจะถูกใช้ในการส่งข้อมูล เช่น เกมออนไลน์
การแสกนเพื่อหา port UDP ที่เปิดอยู่ก็จะเป็นดังนี้
```shell-session
$ sudo nmap 10.129.2.28 -sU
```
#### version scan
เป้นการแสกนหา service และ version ของ service นั้นๆ โดยใช้ `-sV`
```shell-session
$ sudo nmap 10.129.2.28 -p445 -sV

Starting Nmap 7.80 ( https://nmap.org ) at 2022-11-04 11:10 GMT


PORT    STATE SERVICE     REASON         VERSION
445/tcp open  netbios-ssn syn-ack ttl 63 Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
Service Info: Host: Ubuntu
```

## Nmap Scripting Engine
Nmap Scripting Engine หรือ NSE เป็นอีกฟีเจอร์หนึ่งของ nmap ที่ช่วยให้เราสามารถใช้สคริปต์นั้นๆ เพื่อที่จะทราบข้อมูลที่เฉพาะเจาะจง 
```shell-session
$ sudo nmap <target> --script <category>
```

| **Category** | **Description**                                                            |
| ------------ | -------------------------------------------------------------------------- |
| `auth`       | ใช้ตรวจสอบหรือทดสอบกระบวนการยืนยันตัวตน                                    |
| `broadcast`  | ใช้ค้นหาอุปกรณ์หรือเซอร์วิสในเครือข่ายแบบอัตโนมัติ (ควรระมัดระวังในการใช้) |
| `brute`      | ใช้สุ่มชื่อผู้ใช้และรหัสผ่านในการล็อกอิน                                   |
| `default`    | เหมือนการใช้ `-sC`                                                         |
| `discovery`  | ค้นหา `service` ที่สามารถเข้าถึงได้                                        |
| `exploit`    | ใช้ในการค้นหาช่องโหว่ของพ port                                             |
| `safe`       | ป้องกันไม่ให้สคริปส่งผลกระทบต่อตัวระบบ                                     |
| `version`    | เป็น extention ของ `-sV`                                                   |
| `vuln`       | ใช้ระบุช่องโหว่ที่เฉพาะเจาะจง                                              |
