\# 🔍 Task 5 — Information Gathering



> \*\*Objective:\*\* Perform Active and Passive reconnaissance on the target to identify open ports and running services.



\---



\## 📁 Repo Structure



```

CyberSecurity-Task-InfoGathering-FarhanShaikh/

├── 5. Information Gathering.docx.md

├── README.md

└── Information Gathering.docx

```



\---



\## 🛠️ Tools Used



| Tool | Type | Purpose |

|------|------|---------|

| `whois` | Passive | Domain registration lookup |

| `nmap -sV` | Active | Port scanning + service version detection |



\---



\## 🧪 Step 1 — Passive Recon (WHOIS)



\*\*Command:\*\*

```bash

whois tutedude.com

```



\*\*Output (relevant):\*\*

```

┌──(kali㉿kali)-\[\~]

└─$ whois tutedude.com

&#x20;  Domain Name: TUTEDUDE.COM

&#x20;  Registry Domain ID: 2458272606\_DOMAIN\_COM-VRSN

&#x20;  Registrar WHOIS Server: whois.godaddy.com

&#x20;  Registrar URL: http://www.godaddy.com

&#x20;  Updated Date: 2026-05-10T11:24:15Z

&#x20;  Creation Date: 2019-11-22T13:10:34Z

&#x20;  Registry Expiry Date: 2026-11-22T13:10:34Z

&#x20;  Registrar: GoDaddy.com, LLC

&#x20;  Name Server: CHRIS.NS.CLOUDFLARE.COM

&#x20;  Name Server: ELLY.NS.CLOUDFLARE.COM

&#x20;  DNSSEC: unsigned

```



✅ \*\*Answer:\*\* Domain registered on \*\*22/11/2019\*\*



\---



\## 🧪 Step 2 — Active Recon (Nmap)



\*\*Command:\*\*

```bash

nmap -sV 192.168.155.0/24

```



\*\*Output (target: 192.168.155.129):\*\*

```

┌──(kali㉿kali)-\[\~]

└─$ nmap -sV 192.168.155.0/24

Starting Nmap 7.98 ( https://nmap.org ) at 2026-06-25 04:15 -0400



Nmap scan report for 192.168.155.129

Host is up (0.00043s latency).

Not shown: 994 closed tcp ports (reset)

PORT     STATE  SERVICE      VERSION

21/tcp   open   ftp          vsftpd 3.0.5

22/tcp   open   ssh          OpenSSH 9.6p1 Ubuntu 3ubuntu13.16

80/tcp   open   http         Apache httpd 2.4.58 ((Ubuntu))

139/tcp  open   netbios-ssn  Samba smbd 4

445/tcp  open   netbios-ssn  Samba smbd 4

8080/tcp open   http         Apache httpd 2.4.58 ((Ubuntu))

MAC Address: 00:0C:29:E0:B3:45 (VMware)

Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux\_kernel

```



\---



\## ✅ Answers Summary



| Question | Answer |

|----------|--------|

| When was tutedude.com registered? | \*\*22/11/2019\*\* |

| How many ports are open on the target? | \*\*6\*\* |

| Which port is commonly used for SSH? | \*\*22\*\* |

| Which service is running on port 80? | \*\*HTTP (Apache httpd 2.4.58)\*\* |

| What is the Service Version on port 21? | \*\*vsftpd 3.0.5\*\* |



\---



\## 👤 Submitted By



\*\*Name:\*\* Farhan Shaikh

\*\*GitHub:\*\* \[YTxFSGAMERz](https://github.com/YTxFSGAMERz)

