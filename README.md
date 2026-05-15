# Metasploit-for-reconnaissance
# NAME-SRILAKSHMI BH
# REG.NO-212224100057
# Metasploit
Metasploit for reconnaissance in pentesting

# AIM:

To get introduced to Metasploit Framework and to  perform reconnaissance  in pentesting .

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode

### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## EXECUTION STEPS AND ITS OUTPUT:

Find out the ip address of the attackers system
## OUTPUT:

<img width="346" height="168" alt="Screenshot 2026-05-15 123107" src="https://github.com/user-attachments/assets/2c44548b-5650-417b-9d49-e7d4522be43f" />

Shows network interfaces eth0 and lo.
eth0 has IP 192.168.152.128 with MAC 00:0c:29:2f:45:b0.
Loopback lo uses 127.0.0.1 for local traffic.
No errors, drops, or collisions reported.


Invoke msfconsole:
## OUTPUT:

<img width="380" height="310" alt="Screenshot 2026-05-15 123142" src="https://github.com/user-attachments/assets/9141034c-fbc7-461e-bbcd-786e136da48a" />

Metasploit launches with its signature ASCII art.
Version 6.4.116‑dev loads exploits, payloads, modules.
Over 2,600 exploits and 1,700 payloads available.
Framework maintained as an open‑source Rapid7 project.


<img width="475" height="350" alt="Screenshot 2026-05-15 123153" src="https://github.com/user-attachments/assets/b40527f5-284f-4b7c-892e-3c023fbe5756" />

Help lists core commands like set, sessions, exit.
Supports plugins, routing, and variable management.
History and tips improve productivity in console use.
Version info available with version command.







Port Scanning:
Following command is executed for scanning the systems on our local area network with a TCP scan (-sT) looking for open ports between 1 and 1000 (-p1-1000).
msf >  nmap -sT 192.168.1810/24 -p1-1000  (Replace with appropriate IP Address)
## OUTPUT:


<img width="350" height="218" alt="Screenshot 2026-05-15 124010" src="https://github.com/user-attachments/assets/73281db8-3b6a-4006-ba6b-f31bcf1f7a6f" />

Scan targets 192.168.152.128/24 range.
Four VMware hosts detected as alive.
Ports mostly filtered or closed.
Latency shows quick responses under milliseconds.


step4:
use the db-nmap command to scan and save the results into Metasploit's postgresql attached database. In that way, you can use those results in the exploitation stage later.

scan the targets with the command db_nmap as follows.
msf > db_nmap 192.168.181.0/24
## OUTPUT:


<img width="587" height="59" alt="Screenshot 2026-05-15 124153" src="https://github.com/user-attachments/assets/49d0d0e8-9d17-4de4-9ccb-796587e09534" />

Focused on port 3306 with db_nmap.
Host 192.168.152.128 confirmed active.
Port state shows as filtered (blocked).
Firewall prevents service detection results.



Metasploit has a multitude of scanning modules built in. If we open another terminal, we can navigate to Metasploit's auxiliary modules and list all the scanner modules.
cd /usr/share /metasploit-framework/modules/auxiliary
kali > ls -l
## OUTPUT:

<img width="291" height="200" alt="Screenshot 2026-05-15 131543" src="https://github.com/user-attachments/assets/7f5884bc-055e-4231-8364-b6320dfa141d" />

Lists Metasploit auxiliary module folders.
Categories include admin, sql, spoof, fuzzers.
Two sample files: example.rb and example.py.
Shows extensible structure for scanning and exploitation.





Search is a powerful command in Metasploit that you can use to find what you want to locate. 
msf >search name:Microsoft type:exploit
## OUTPUT:


<img width="319" height="360" alt="Screenshot 2026-05-15 131612" src="https://github.com/user-attachments/assets/4fe3756b-9523-4748-9c54-b08bf7233bf1" />

Search lists exploits for Microsoft products.
Targets include Windows 2000, XP, and 2003.
Modules cover IIS and ARCServe vulnerabilities.
Each entry specifies supported service packs.



The info command provides information regarding a module or platform,

Before beginning, set up the Metasploit database by starting the PostgreSQL server and initialize msfconsole database as follows:
systemctl start postgresql
msfdb init
## OUTPUT:


<img width="326" height="334" alt="Screenshot 2026-05-15 131650" src="https://github.com/user-attachments/assets/a48f30a2-03b9-44ee-a9c3-3ff60e285462" />

MS10‑065 exploits IIS 5 NTFS streams.
Rank is normal, disclosed July 2010.
Options include RHOSTS, RPORT, SSL, TARGETURI.
Bypasses basic authentication on IIS servers.



## MYSQL ENUMERATION
Find the IP address of the Metasploitable machine first. Then, use the db_nmap command in msfconsole with Nmap flags to scan the MySQL database at 3306 port.
db_nmap -sV -sC -p 3306 <metasploitable_ip_address>

## OUTPUT:

<img width="361" height="74" alt="Screenshot 2026-05-15 131702" src="https://github.com/user-attachments/assets/86119ac8-43c1-4bba-a0a0-21516c64a741" />


Scan targets port 3306 on 192.168.152.128.
Host confirmed alive during detection.
Port state shows as filtered (blocked).
Service identified as MySQL, scan completed.


Use the search option to look for an auxiliary module to scan and enumerate the MySQL database.
search type:auxiliary mysql
## OUTPUT:


<img width="452" height="344" alt="Screenshot 2026-05-15 131744" src="https://github.com/user-attachments/assets/81af802c-6278-4027-a600-da1347a4d93c" />


Search lists modules for MySQL testing.
Includes login, hashdump, schemadump, and capture.
Modules support brute force and enumeration.
Useful for SQL injection and password analysis.


use the auxiliary/scanner/mysql/mysql_version module by typing the module name or associated number to scan MySQL version details.
use 11
Or:
use auxiliary/scanner/mysql/mysql_version
## OUTPUT:


<img width="446" height="197" alt="Screenshot 2026-05-15 131826" src="https://github.com/user-attachments/assets/a5966acc-e84b-468c-af6d-81f4ff8a0041" />

Module scanner/mysql/mysql_version is loaded.
Can target either a SESSION or RHOSTS.
Default port set to 3306 with threads = 1.
Used to detect MySQL server version remotely.



Use the set rhosts command to set the parameter and run the module, as follows:
## OUTPUT:

<img width="303" height="56" alt="Screenshot 2026-05-15 131908" src="https://github.com/user-attachments/assets/3a21e9ad-cc35-462d-84d4-a4299328fff2" />

Target set to 192.168.152.128.
Scan runs against port 3306.
Host scanned fully, 1 of 1 complete.
Execution finished without crash or errors.


After scanning, you can also brute force MySQL root account via Metasploit's auxiliary(scanner/mysql/mysql_login) module.
## OUTPUT:


<img width="458" height="292" alt="Screenshot 2026-05-15 132028" src="https://github.com/user-attachments/assets/9efbcd55-4332-4e1b-8950-3b93b933c09a" />

Module scanner/mysql/mysql_login is configured.
Supports blank passwords and wordlists.
Bruteforce speed adjustable from 0–5.
Can stop on success or continue scanning.


set the PASS_FILE parameter to the wordlist path available inside /usr/share/wordlists:
set PASS_FILE /usr/share/wordlistss/rockyou.txt
Then, specify the IP address of the target machine with the RHOSTS command.
set RHOSTS <metasploitable-ip-address>
Set BLANK_PASSWORDS to true in case there is no password set for the root account.
set BLANK_PASSWORDS true
## OUTPUT:

<img width="460" height="95" alt="Screenshot 2026-05-15 132752" src="https://github.com/user-attachments/assets/3936d6ab-ab2f-4c74-b06a-ca70995d27b3" />

Wordlist set to rockyou.txt.gz.
Target host defined as 192.168.152.128.
Blank passwords enabled, verbose disabled.
One credential successfully discovered.




## RESULT:
The Metasploit framework for reconnaissance is  examined successfully
