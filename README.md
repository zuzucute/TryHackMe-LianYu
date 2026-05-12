# TryHackMe-LianYu

Objective
to find a hidden flag.


I downloaded vpn from tryhackme website.
<img width="944" height="844" alt="Screenshot 2026-04-27 010745" src="https://github.com/user-attachments/assets/716d5594-a936-4a91-be2a-aac759d09c8e" />

and then i run openvpn to connect with the vpn.
```
sudo openvpn ap-south-1-sitizulaika632-regular.ovpn
```
if it says 
```
Initialization Sequence Completed.
```
That means the vpn successfully connected.

And then, I open tryhackme-LianYu to find the target ip address.
<img width="699" height="228" alt="Screenshot 2026-04-27 010851" src="https://github.com/user-attachments/assets/25570f07-e942-4590-8adf-0e8b62b51360" />

```
target ip address : 10.48.176.245
```

<img width="968" height="372" alt="Screenshot 2026-04-27 213422" src="https://github.com/user-attachments/assets/0d324d72-76e8-4178-b899-e248ac6a12a7" />

to verify whether kali has connect with the vpn or not i run this command
```
ip a
```

i use nmap to scan open port.

```
nmap -sC -sV -Pn -vv 10.48.176.254
```
<img width="953" height="864" alt="Screenshot 2026-04-27 010932" src="https://github.com/user-attachments/assets/e4803dc5-858e-4b44-ab93-e205dca826f8" />

i visit http://target_ip then i found ARROWVERSE page.
```
http://10.48.176.254
```
<img width="1100" height="754" alt="image" src="https://github.com/user-attachments/assets/07a128ae-b87b-4778-b5b8-820b99fab7dc" />

i use gobuster to brute force hidden resource on a target ip.
```
gobuster dir -u http://10.48.176.254 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```
<img width="945" height="78" alt="Screenshot 2026-04-27 011009" src="https://github.com/user-attachments/assets/5fe51b96-c248-4071-9094-ce1901acfb30" />

finding :
* /sland
<img width="795" height="22" alt="Screenshot 2026-04-27 010714" src="https://github.com/user-attachments/assets/6659a5a3-09a0-42a0-9768-f6c674c429fb" />

Then i /island in the browser
```
http://10.48176.245/island
```

next i run brute force using the previous finding to find more clues
```
gobuster dir -u http://10.48.176.254/island -w /usr/share/worlists/dirbuster/directory-list-2.3-medium.txt
```
<img width="939" height="283" alt="Screenshot 2026-04-27 012640" src="https://github.com/user-attachments/assets/d04cd02d-4894-4218-9100-dfe9cb9e9fe0" />

Finding: 
* 2100

i open browser again to run
```
http://10.48.172.197/island/2100
```
Finding:
<img width="989" height="317" alt="image" src="https://github.com/user-attachments/assets/b491fd2a-34d5-4436-b9d5-8bc6b09a3db7" />

FInding(View page source):
<img width="1036" height="450" alt="image" src="https://github.com/user-attachments/assets/a75e2e88-5bc3-46c5-853a-31d6020a5ce0" />

Find hidden text : vigilante

<img width="1918" height="908" alt="Screenshot 2026-04-27 210016" src="https://github.com/user-attachments/assets/db83cd0d-6c86-403b-bc07-f5524d1b6219" />

the page says that that "Oliver has find it's way to Lian_Yu


I click on the page to view page source to find any clue.

<img width="838" height="539" alt="Screenshot 2026-05-03 114626" src="https://github.com/user-attachments/assets/2f4e591d-3530-4ede-a18b-9cd5c17f1278" />

Finding:

* found somthing off with the .ticket.Then, i run

```
gobuster dir -u http://10.48.176.254/island -w /usr/share/worlists/dirbuster/directory-list-2.3-medium.txt -x .ticket
```
<img width="941" height="524" alt="image" src="https://github.com/user-attachments/assets/e92fd473-fc45-44b0-b1de-48fc2461ffda" />

Finding:

* /green_arrow.ticket

i then visit http://10.48.188.25/island/2100/green_arrow.ticket adnd found code RTy8yhBQdscX

<img width="985" height="275" alt="Screenshot 2026-04-27 214040" src="https://github.com/user-attachments/assets/d7b03e3e-f2c0-425f-92ca-2c7819a714f0" />

i decode it and get !#th3h00d when decoding it as base58.

<img width="153" height="628" alt="Screenshot 2026-04-27 214647" src="https://github.com/user-attachments/assets/79888bbc-3ac7-484f-919c-36081c573a42" />

i test the ftp with credentials: vigilante and !#th3h00d as password

```
ftp vigilante@10.48.188.24
```

<img width="307" height="175" alt="Screenshot 2026-04-27 214811" src="https://github.com/user-attachments/assets/0efe6e01-793c-4af6-a0ee-b6bf5ef7a435" />



<img width="989" height="317" alt="Screenshot 2026-04-27 204648" src="https://github.com/user-attachments/assets/40f7421f-075f-4fdf-acf4-c8bcb03526bd" />

<img width="1036" height="450" alt="Screenshot 2026-04-27 204739" src="https://github.com/user-attachments/assets/a3b15aca-dbbe-4121-83f7-6e1a29f12372" />


<img width="968" height="605" alt="Screenshot 2026-04-27 213422" src="https://github.com/user-attachments/assets/59138102-6974-4862-8281-8aec699eb14f" />


<img width="619" height="229" alt="Screenshot 2026-04-27 214819" src="https://github.com/user-attachments/assets/0da16a47-5a95-47b0-801e-d98e35caedad" />

<img width="382" height="70" alt="Screenshot 2026-04-27 215306" src="https://github.com/user-attachments/assets/3a658ab1-e977-4329-a0a2-9174eb90d268" />

<img width="599" height="214" alt="Screenshot 2026-04-27 215316" src="https://github.com/user-attachments/assets/4dc2a0e2-dc8d-4357-b197-07b9251a3fb0" />

<img width="559" height="171" alt="Screenshot 2026-04-27 215324" src="https://github.com/user-attachments/assets/9beb4af2-22c2-42bc-88d5-cafc57f517bb" />

<img width="1910" height="524" alt="Screenshot 2026-04-27 215338" src="https://github.com/user-attachments/assets/2f15e025-bd20-4bf9-9f55-b251ffacab8d" />

<img width="926" height="283" alt="Screenshot 2026-04-28 160050" src="https://github.com/user-attachments/assets/4fd11e51-cf67-4dc1-b645-92b28e4c6a9c" />

<img width="201" height="39" alt="Screenshot 2026-04-28 160323" src="https://github.com/user-attachments/assets/381399f4-75df-49d0-8f90-973e336066b3" />

<img width="451" height="110" alt="Screenshot 2026-04-28 162034" src="https://github.com/user-attachments/assets/e5a7ba74-bc74-4acf-b31c-eb2dfb8e8c22" />

<img width="233" height="100" alt="Screenshot 2026-04-28 162121" src="https://github.com/user-attachments/assets/abed1c81-ef70-4aec-a544-a636eb2a4dfe" />

<img width="673" height="232" alt="Screenshot 2026-04-28 162156" src="https://github.com/user-attachments/assets/54a673bc-24ea-4a7f-8b93-959bffa7108b" />

<img width="184" height="80" alt="Screenshot 2026-04-28 162211" src="https://github.com/user-attachments/assets/edb68ca2-6c47-47ca-b687-f09ce255054f" />

<img width="656" height="509" alt="Screenshot 2026-04-28 162508" src="https://github.com/user-attachments/assets/4410f429-486e-407d-92e9-9938c4d65bb3" />

<img width="351" height="98" alt="Screenshot 2026-04-28 162535" src="https://github.com/user-attachments/assets/f38be2c8-9937-433b-81cc-2d3eeebd9fa2" />

<img width="885" height="118" alt="Screenshot 2026-04-28 162719" src="https://github.com/user-attachments/assets/5d706163-8e96-4e06-98f2-0a682fbe70d0" />

<img width="770" height="288" alt="Screenshot 2026-04-28 162901" src="https://github.com/user-attachments/assets/39d60bc6-19e9-4c95-822e-0aa9455d8d36" />


























