___
**Tags:** [[tools]] [[hacking]][[Cyber Security]]

**Links:** 

---
[[Meterpreter]]
## What Is Metasploit?

Metasploit is a popular open-source framework for creating, testing, and deploying exploits. It is used by hackers (ethical and otherwise) and security researchers to test the security of machines, networks, and infrastructure. 

Metasploit’s collection of exploits, payloads, and tools to conduct penetration testing can speed up the testing process and take on much of the heavy lifting. 

Most of the available tools and exploits only require filling in some basic information, such as the target ip address and port number and possibly operating system or software version of the target. Very little modification is required of the user.

It also has the ability to easily upload files to and download files from a target system, perform network scanning, routing network traffic, and manage multiple sessions at once.

Whether you're a security professional or a student learning about cybersecurity, Metasploit is a valuable tool to have in your arsenal.

[[Metasploit Cheat-Sheet]]

**Port Scanning**

Metasploit has a number of modules to scan open ports on the target system and network. You can list potential port scanning modules available using the `search portscan` command.

Search portscan

           `msf6 > search portscan  Matching Modules ================     #  Name                                              Disclosure Date  Rank    Check  Description    -  ----                                              ---------------  ----    -----  -----------    0  auxiliary/scanner/http/wordpress_pingback_access                   normal  No     Wordpress Pingback Locator    1  auxiliary/scanner/natpmp/natpmp_portscan                           normal  No     NAT-PMP External Port Scanner    2  auxiliary/scanner/portscan/ack                                     normal  No     TCP ACK Firewall Scanner    3  auxiliary/scanner/portscan/ftpbounce                               normal  No     FTP Bounce Port Scanner    4  auxiliary/scanner/portscan/syn                                     normal  No     TCP SYN Port Scanner    5  auxiliary/scanner/portscan/tcp                                     normal  No     TCP Port Scanner    6  auxiliary/scanner/portscan/xmas                                    normal  No     TCP "XMas" Port Scanner    7  auxiliary/scanner/sap/sap_router_portscanner                       normal  No     SAPRouter Port Scanner   Interact with a module by name or index, for example use 7 or use auxiliary/scanner/sap/sap_router_portscanner  msf6 >`
        

  

Port scanning modules will require you to set a few options:

Portscan options

           `msf6 auxiliary(scanner/portscan/tcp) > show options  Module options (auxiliary/scanner/portscan/tcp):     Name         Current Setting  Required  Description    ----         ---------------  --------  -----------    CONCURRENCY  10               yes       The number of concurrent ports to check per host    DELAY        0                yes       The delay between connections, per thread, in milliseconds    JITTER       0                yes       The delay jitter factor (maximum value by which to +/- DELAY) in milliseconds.    PORTS        1-10000          yes       Ports to scan (e.g. 22-25,80,110-900)    RHOSTS                        yes       The target host(s), range CIDR identifier, or hosts file with syntax 'file:'    THREADS      1                yes       The number of concurrent threads (max one per host)    TIMEOUT      1000             yes       The socket connect timeout in milliseconds  msf6 auxiliary(scanner/portscan/tcp) >`
        

  

- **CONCURRENCY:** Number of targets to be scanned simultaneously.
- **PORTS:** Port range to be scanned. Please note that 1-1000 here will not be the same as using Nmap with the default configuration. Nmap will scan the 1000 most used ports, while Metasploit will scan port numbers from 1 to 10000.
- **RHOSTS:** Target or target network to be scanned.
- **THREADS:** Number of threads that will be used simultaneously. More threads will result in faster scans.

You can directly perform Nmap scans from the msfconsole prompt as shown below faster:  

Using Nmap from the Msfconsole prompt

           `msf6 > nmap -sS 10.10.12.229 [*] exec: nmap -sS 10.10.12.229   Starting Nmap 7.60 ( https://nmap.org ) at 2021-08-20 03:54 BST Nmap scan report for ip-10-10-12-229.eu-west-1.compute.internal (10.10.12.229) Host is up (0.0011s latency). Not shown: 992 closed ports PORT      STATE SERVICE 135/tcp   open  msrpc 139/tcp   open  netbios-ssn 445/tcp   open  microsoft-ds 3389/tcp  open  ms-wbt-server 49152/tcp open  unknown 49153/tcp open  unknown 49154/tcp open  unknown 49158/tcp open  unknown MAC Address: 02:CE:59:27:C8:E3 (Unknown)  Nmap done: 1 IP address (1 host up) scanned in 64.19 seconds msf6 >`
        

  

As for information gathering, if your engagement requires a speedier approach to port scanning, Metasploit may not be your first choice. However, a number of modules make Metasploit a useful tool for the scanning phase.

**UDP service Identification**

The `scanner/discovery/udp_sweep` module will allow you to quickly identify services running over the UDP (User Datagram Protocol). As you can see below, this module will not conduct an extensive scan of all possible UDP services but does provide a quick way to identify services such as DNS or NetBIOS.

**UDP scan**

           `msf6 auxiliary(scanner/discovery/udp_sweep) > run  [*] Sending 13 probes to 10.10.12.229->10.10.12.229 (1 hosts) [*] Discovered NetBIOS on 10.10.12.229:137 (JON-PC::U :WORKGROUP::G :JON-PC::U :WORKGROUP::G :WORKGROUP::U :__MSBROWSE__::G :02:ce:59:27:c8:e3) [*] Scanned 1 of 1 hosts (100% complete) [*] Auxiliary module execution completed msf6 auxiliary(scanner/discovery/udp_sweep) >`
        

  

**SMB Scans**

Metasploit offers several useful auxiliary modules that allow us to scan specific services. Below is an example for the SMB. Especially useful in a corporate network would be `smb_enumshares` and `smb_version` but please spend some time to identify scanners that the Metasploit version installed on your system offers.

SMB scan

           `msf6 auxiliary(scanner/smb/smb_version) > run  [+] 10.10.12.229:445      - Host is running Windows 7 Professional SP1 (build:7601) (name:JON-PC) (workgroup:WORKGROUP ) (signatures:optional) [*] 10.10.12.229:445      - Scanned 1 of 1 hosts (100% complete) [*] Auxiliary module execution completed msf6 auxiliary(scanner/smb/smb_version) >`
        

  

When performing service scans, it would be important not to omit more "exotic" services such as NetBIOS. NetBIOS (Network Basic Input Output System), similar to SMB, allows computers to communicate over the network to share files or send files to printers. The NetBIOS name of the target system can give you an idea about its role and even importance (e.g. CORP-DC, DEVOPS, SALES, etc.). You may also run across some shared files and folders that could be accessed either without a password or protected with a simple password (e.g. admin, administrator, root, toor, etc.).

Remember, Metasploit has many modules that can help you have a better understanding of the target system and possibly help you find vulnerabilities. It is always worth performing a quick search to see if there are any modules that could be helpful based on your target system.

---

While it is not required when interacting with a single target on TryHackMe, an actual penetration testing engagement will likely have several targets. 

  

Metasploit has a database function to simplify project management and avoid possible confusion when setting up parameter values. 

  

You will first need to start the PostgreSQL database, which Metasploit will use with the following command: 

`systemctl start postgresql`

  

Then you will need to initialize the Metasploit Database using the `msfdb init` command. 

  

Starting Postgresql

           `root@attackbox:~# systemctl start postgresql  root@attackbox:~# msfdb init [i] Database already started [+] Creating database user 'msf' [+] Creating databases 'msf' [+] Creating databases 'msf_test' [+] Creating configuration file '/usr/share/metasploit-framework/config/database.yml' [+] Creating initial database schema /usr/share/metasploit-framework/vendor/bundle/ruby/2.7.0/gems/activerecord-4.2.11.3/lib/active_record/connection_adapters/abstract_adapter.rb:84: warning: deprecated Object#=~ is called on Integer; it always returns nil root@attackbox:~#`

  
You can now launch `msfconsole` and check the database status using the `db_status` command.

Checking the database status

           `msf6 > db_status [*] Connected to msf. Connection type: postgresql. msf6 >`
  

  
The database feature will allow you to create workspaces to isolate different projects. When first launched, you should be in the default workspace. You can list available workspaces using the `workspace` command. 

Listing workspaces

           `msf6 > workspace * default msf6 >`

  
You can add a workspace using the `-a` parameter or delete a workspace using the `-d` parameter, respectively. The screenshot below shows that a new workspace named "tryhackme" was created.

Adding a workspace

           `msf6 > workspace -a tryhackme [*] Added workspace: tryhackme [*] Workspace: tryhackme msf5 > workspace default * tryhackme msf6 >`

  
You will also notice that the new database name is printed in red, starting with a `*` symbol.

You can use the workspace command to navigate between workspaces simply by typing `workspace` followed by the desired workspace name. 

Changing workspaces

           `msf6 > workspace default * tryhackme msf5 > workspace default [*] Workspace: default msf5 > workspace  tryhackme * default msf6 >`

  
You can use the `workspace -h` command to list available options for the `workspace` command. 

Workspace help menu

           `msf6 > workspace -h Usage: workspace                  List workspaces workspace -v               List workspaces verbosely workspace [name]           Switch workspace workspace -a [name] ...    Add workspace(s) workspace -d [name] ...    Delete workspace(s) workspace -D               Delete all workspaces workspace -r     Rename workspace workspace -h               Show this help information`

  
Different from regular Metasploit usage, once Metasploit is launched with a database, the `help` command, you will show the Database Backends Commands menu.

Database backend commands

           `Database Backend Commands =========================  Command           Description -------           ----------- analyze           Analyze database information about a specific address or address range db_connect        Connect to an existing data service db_disconnect     Disconnect from the current data service db_export         Export a file containing the contents of the database db_import         Import a scan result file (filetype will be auto-detected) db_nmap           Executes nmap and records the output automatically db_rebuild_cache  Rebuilds the database-stored module cache (deprecated) db_remove         Remove the saved data service entry db_save           Save the current data service connection as the default to reconnect on startup db_status         Show the current data service status hosts             List all hosts in the database loot              List all loot in the database notes             List all notes in the database services          List all services in the database vulns             List all vulnerabilities in the database workspace         Switch between database workspaces`

  
If you run a Nmap scan using the `db_nmap` shown below, all results will be saved to the database. 

The db_nmap command

           `msf6 > db_nmap -sV -p- 10.10.12.229 [*] Nmap: Starting Nmap 7.80 ( https://nmap.org ) at 2021-08-20 03:15 UTC [*] Nmap: Nmap scan report for ip-10-10-12-229.eu-west-1.compute.internal (10.10.12.229) [*] Nmap: Host is up (0.00090s latency). [*] Nmap: Not shown: 65526 closed ports [*] Nmap: PORT      STATE SERVICE            VERSION [*] Nmap: 135/tcp   open  msrpc              Microsoft Windows RPC [*] Nmap: 139/tcp   open  netbios-ssn        Microsoft Windows netbios-ssn [*] Nmap: 445/tcp   open  microsoft-ds       Microsoft Windows 7 - 10 microsoft-ds (workgroup: WORKGROUP) [*] Nmap: 3389/tcp  open  ssl/ms-wbt-server? [*] Nmap: 49152/tcp open  msrpc              Microsoft Windows RPC [*] Nmap: 49153/tcp open  msrpc              Microsoft Windows RPC [*] Nmap: 49154/tcp open  msrpc              Microsoft Windows RPC [*] Nmap: 49158/tcp open  msrpc              Microsoft Windows RPC [*] Nmap: 49162/tcp open  msrpc              Microsoft Windows RPC [*] Nmap: MAC Address: 02:CE:59:27:C8:E3 (Unknown) [*] Nmap: Service Info: Host: JON-PC; OS: Windows; CPE: cpe:/o:microsoft:windows [*] Nmap: Service detection performed. Please report any incorrect results at https://nmap.org/submit/ . [*] Nmap: Nmap done: 1 IP address (1 host up) scanned in 94.91 seconds msf6 >`

  
You can now reach information relevant to hosts and services running on target systems with the `hosts` and `services` commands, respectively. 

Hosts and services

           `msf6 > hosts  Hosts =====  address       mac                name                                        os_name  os_flavor  os_sp  purpose  info  comments -------       ---                ----                                        -------  ---------  -----  -------  ----  -------- 10.10.12.229  02:ce:59:27:c8:e3  ip-10-10-12-229.eu-west-1.compute.internal  Unknown                    device           msf6 > services Services ========  host          port   proto  name               state  info ----          ----   -----  ----               -----  ---- 10.10.12.229  135    tcp    msrpc              open   Microsoft Windows RPC 10.10.12.229  139    tcp    netbios-ssn        open   Microsoft Windows netbios-ssn 10.10.12.229  445    tcp    microsoft-ds       open   Microsoft Windows 7 - 10 microsoft-ds workgroup: WORKGROUP 10.10.12.229  3389   tcp    ssl/ms-wbt-server  open    10.10.12.229  49152  tcp    msrpc              open   Microsoft Windows RPC 10.10.12.229  49153  tcp    msrpc              open   Microsoft Windows RPC 10.10.12.229  49154  tcp    msrpc              open   Microsoft Windows RPC 10.10.12.229  49158  tcp    msrpc              open   Microsoft Windows RPC 10.10.12.229  49162  tcp    msrpc              open   Microsoft Windows RPC  msf6 >`

  
The `hosts -h` and `services -h` commands can help you become more familiar with available options. 

Once the host information is stored in the database, you can use the `hosts -R` command to add this value to the RHOSTS parameter. 

  

**Example Workflow**

1. We will use the vulnerability scanning module that finds potential MS17-010 vulnerabilities with the `use auxiliary/scanner/smb/smb_ms17_010` command.
2. We set the RHOSTS value using `hosts -R`.
3. We have typed `show options` to check if all values were assigned correctly. (In this example, 10.10.138.32 is the IP address we have scanned earlier using the `db_nmap` command)
4. Once all parameters are set, we launch the exploit using the `run` or `exploit` command. 

Using saved hosts

           `msf6 > use auxiliary/scanner/smb/smb_ms17_010  msf5 auxiliary(scanner/smb/smb_ms17_010) > hosts -R   Hosts =====  address       mac                name                                        os_name  os_flavor  os_sp  purpose  info  comments -------       ---                ----                                        -------  ---------  -----  -------  ----  -------- 10.10.12.229  02:ce:59:27:c8:e3  ip-10-10-12-229.eu-west-1.compute.internal  Unknown                    device           RHOSTS => 10.10.12.229  msf6 auxiliary(scanner/smb/smb_ms17_010) > show options   Module options (auxiliary/scanner/smb/smb_ms17_010):  Name         Current Setting                                                 Required  Description ----         ---------------                                                 --------  ----------- CHECK_ARCH   true                                                            no        Check for architecture on vulnerable hosts CHECK_DOPU   true                                                            no        Check for DOUBLEPULSAR on vulnerable hosts CHECK_PIPE   false                                                           no        Check for named pipe on vulnerable hosts NAMED_PIPES  /usr/share/metasploit-framework/data/wordlists/named_pipes.txt  yes       List of named pipes to check RHOSTS       10.10.12.229                                                    yes       The target host(s), range CIDR identifier, or hosts file with syntax 'file:' RPORT        445                                                             yes       The SMB service port (TCP) SMBDomain    .                                                               no        The Windows domain to use for authentication SMBPass                                                                      no        The password for the specified username SMBUser                                                                      no        The username to authenticate as THREADS      1                                                               yes       The number of concurrent threads (max one per host)  msf6 auxiliary(scanner/smb/smb_ms17_010) > run`

  
If there is more than one host saved to the database, all IP addresses will be used when the `hosts -R` command is used.   

In a typical penetration testing engagement, we could have the following scenario: 

- Finding available hosts using the `db_nmap` command
- Scanning these for further vulnerabilities or open ports (using a port scanning module) 

  

The services command used with the `-S` parameter will allow you to search for specific services in the environment.

Querying the database for services

           `msf6 > services -S netbios                                                                                        Services                                                                                                              ========                                                                                                                                                                                                                               host          port  proto  name         state  info                                                                               ----          ----  -----  ----         -----  ----                                                                               10.10.12.229  139   tcp    netbios-ssn  open   Microsoft Windows netbios-ssn  msf6 >`

  
You may want to look for low-hanging fruits such as:

- HTTP: Could potentially host a web application where you can find vulnerabilities like SQL injection or Remote Code Execution (RCE). 
- FTP: Could allow anonymous login and provide access to interesting files. 
- SMB: Could be vulnerable to SMB exploits like MS17-010
- SSH: Could have default or easy to guess credentials
- RDP: Could be vulnerable to Bluekeep or allow desktop access if weak credentials were used. 

  

As you can see, Metasploit has many features to aid in engagements such as the ability to compartmentalize your engagements into workspaces, analyze your results at a high level, and quickly import and explore data.

---

You will first need to start the PostgreSQL database, which Metasploit will use with the following command:

`systemctl start postgresql`

Then you will need to initialize the Metasploit Database using the `msfdb init` command.

Read the information carefully and keep some notes :

- HTTP: Could potentially host a web application where you can find vulnerabilities like SQL injection or Remote Code Execution (RCE).
- FTP: Could allow anonymous login and provide access to interesting files.
- SMB: Could be vulnerable to SMB exploits like MS17–010
- SSH: Could have default or easy to guess credentials
- RDP: Could be vulnerable to Bluekeep or allow desktop access if weak credentials were used.