# CEH-practice-notes
# Reconnasiance/Footprinting
<details>
  <summary>To find the subdomain</summary>
  
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
