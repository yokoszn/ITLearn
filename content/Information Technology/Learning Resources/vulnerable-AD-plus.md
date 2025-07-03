simulated AD environment to play around with. 
[[GOAD]]

[vulnerable-AD-plus/WriteUp at master · WaterExecution/vulnerable-AD-plus · GitHub](https://github.com/WaterExecution/vulnerable-AD-plus/tree/master/WriteUp)
[Writeup · WaterExecution/vulnerable-AD-plus Wiki · GitHub](https://github.com/WaterExecution/vulnerable-AD-plus/wiki/Writeup)

---

# Vulnerable-AD-Plus  

[](https://github.com/WaterExecution/vulnerable-AD-plus/blob/master/README.md#--vulnerable-ad-plus--)

Create a vulnerable active directory that's allowing you to test most of active directory attacks in local lab

### Main Features

[](https://github.com/WaterExecution/vulnerable-AD-plus/blob/master/README.md#main-features)

- Randomize Attacks
- Full Coverage of the mentioned attacks
- you need run the script in DC with Active Directory installed
- Some of attacks require client workstation

### Supported Attacks

[](https://github.com/WaterExecution/vulnerable-AD-plus/blob/master/README.md#supported-attacks)

- Abusing ACLs/ACEs
- Kerberoasting
- AS-REP Roasting
- Abuse DnsAdmins (...)
- Password in AD User comment
- Password Spraying
- DCSync (...)
- Silver Ticket (...)
- Golden Ticket (...)
- Pass-the-Hash (...)
- Pass-the-Ticket (...)
- SMB Signing Disabled
- Bad WinRM permission
- Anonymous LDAP query
- Public SMB Share
- Zerologon (Check version)