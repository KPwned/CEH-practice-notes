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
<summary></summary>