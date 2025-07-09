___
**Tags:**
#software
#hacking
#tools
[[BeEF - Browser Exploitation Framework]]

[[Powershell Empire]]
[[Pivoting & Lateral Movement]]

**Links:** 

---

(https://www.stationx.net/how-to-use-bloodhound-active-directory/)

# How to Perform Kerberoasting Attacks: The Ultimate Guide

- This article showcased a variety of tools you can use to perform Kerberoating, and it is recommended that you build your own Active Directory environment to try these tools out for yourself. 

(https://www.stationx.net/how-to-perform-kerberoasting-attacks/)


### How Kerberos Authentication Works
![[Pasted image 20240911094248.png]]
1. The **user sends a request to the KDC asking for initial access** to the Active Directory environment. As part of this request, the user asks for a Ticket Granting Ticket (TGT) that allows them access to network resources within the Active Directory environment.
2. The **KDC verifies the user’s identity** and replies with an encrypted TGT and a session key. The TGT is encrypted using the KDC’s secret key.
3. When the user wants to access a network resource, they **send a request to the KDC asking for a service ticket**, known as a Ticket Granting Service ticket (TGS), for the service (network resource) they want to access. In this request are the user’s TGT, their session key, and the Service Principal Name (SPN) of the service they want to access.
4. The KDC verifies the user’s request by checking the authenticity of the TGT and **if the user is authorized to access the requested service**. If all checks are passed, the KDC replies with a TGS and the encrypted session key to the user.
5. When a user wants to access a Kerberos-enabled service, **they send the TGS to said service**.
6. The **service will verify the TGS** and allow the user to interact with the network resource.

**Ticket Granting Ticket (TGT)** verifies the user’s identity - who they are.

**Ticket Granting Service ticket (TGS)** verifies the user’s permissions - can they access this specific resource.

### The Advantages of Kerberos Authentication

Kerberos is the successor of the legacy NTLM authentication that Microsoft previously used to secure Active Directory. Kerberos offers several key advantages as an authentication protocol for Active Directory environments:

- **Single Sign-On (SSO)** - Users can authenticate once to the KDC and obtain multiple service tickets to access the various resources they want to access.
- **Strong Security** - Kerberos uses strong encryption techniques that make it resistant to replay attacks and password theft (so long as [a strong password](https://www.stationx.net/how-to-guess-a-password/) is used).
- **Mutual Authentication** - Both the client and network resource verify each other’s identity during the authentication process to ensure both parties are legitimate and prevent MitM attacks.
- **Scalability** - Kerberos supports large-scale Active Directory environments with thousands of users and services. Its ticket-based authentication approach helps minimize network traffic and improve performance.
- **Centralized Authentication** - A central KDC means authentication can be performed at a single point for the entire Active Directory environment. This simplifies the administration and management overhead. 
- **Ticket Expiration and Renewal** - Kerberos uses an expiration and renewal mechanism which limits the lifespan of tickets. This means that attackers cannot use compromised tickets indefinitely and have to re-authenticate regularly, reducing the impact of compromised tickets.
- **Interoperability** - Kerberos authentication can be used across various systems and platforms. This prevents compatibility issues in environments that use a variety of technologies.

Modern active directory environments still use NTLM authentication, but Kerberos is the preferred authentication protocol.

---
## Understanding Kerberoasting

Despite the secure nature of Kerberos, there is an inherent vulnerability that exists in the authentication protocol that allows an attacker to extract the password hash of service accounts. Once an attacker has this hash, they can perform lateral movement and impersonate the compromised service account. They can do this by either:

- Cracking the hash and revealing the plaintext password of the service account.
- Using the hash to authenticate directly as the service account.

Kerberoasting is when the attacker steals the password hash of a service account and cracks this hash offline to reveal the plaintext password. It is a very dangerous attack because any authenticated user can perform kerberoasting and, if the service account uses a weak password, the attack will likely be successful. 

A Kerberoasting attack follows these steps:

1. The attacker **impersonates a legitimate Active Directory user** and authenticates to the KDC in the Active Directory environment. They then **request a TGT from the KDC** to access network resources. The **KDC complies** because the attacker is impersonating a legitimate user. This is the same as Steps 1 and 2 in the Kerberos authentication diagram above.
2. The **attacker identifies active service accounts** in the Active Directory environment and collects a list of their associated SPNs. This is done through internal network reconnaissance.
3. The **attacker requests a service ticket (TGS) for a specific SPN** associated with a service account from the KDC. The **KDC will respond with an encrypted TGS** that contains the service account’s password (used to decrypt the ticket). This is the same as Steps 3 and 4 in the Kerberos authentication diagram above.
4. The **attacker takes this ticket and cracks it offline** (on their local machine) using a password cracking tool. 
5. Once the attacker cracks the password, they can use it to **impersonate the service account** and access any network resources it has permission to access.
![[Pasted image 20240911094350.png]]To perform a Kerberoast attack, the following requirements need to be met:

- You must have access to an authenticated user in the Windows Active Directory environment you are attacking.
- You must know the targeted service account’s SPN.
- You need a tool that can extract Kerberos tickets from the machine you have access to.
- You need a password cracking tool.
- You must be able to crack the service account’s password hash to reveal their plaintext password. This can be difficult if the account uses a complicated password.

Trying to kerberoast all service accounts is bad operational security. The blue team will often create fake service accounts that are never used (honey pot accounts). When a TGS is requested, the Windows event `4769 - A Kerberos service ticket was requested` is generated. If this relates to a honey pot account, the defenders will know an attacker is trying to perform Kerberoasting. **A better approach is to perform a targeted Kerberoast attack against specific accounts.**

---
PowerView
BloodHound
### Performing Kerberoasting With Invoke-Kerberoast

[Invoke-Kerberoast](https://powersploit.readthedocs.io/en/latest/Recon/Invoke-Kerberoast/) is a malicious PowerShell script that is part of the defunct [Empire framework](https://www.stationx.net/how-to-use-powershell-empire/). It automates the process of kerberoasting through PowerShell code that requests service tickets for kerberoast-able accounts and returns extracted ticket hashes. 

To use perform a Kerberoast attack with Invoke-Kerberoast, the following requirements need to be satisfied:

- Authenticated access to the Active Directory domain you are attacking.

Invoke-Kerberoast is a PowerShell script. As such, you can load it into your Meterpreter session the same way you loaded the PowerView script:

![[Pasted image 20240911094812.png]]Now you can execute the following command to use Invoke-Kerberoast to perform a Kerberoast attack:

`powershell_execute "Invoke-Kerberoast"`
![[Pasted image 20240911094824.png]]This PowerShell script finds vulnerable accounts, requests a TGS for that account, and then returns the crackable hash. There is no need to specify the account you want to target. This saves you a step but is **not** great for operational security.

If you want the hash in a specific format for cracking, you can use the `-OutputFormat` option. For instance, if you are going to use hashcat to crack the password hash, you can use the command:

`Invoke-Kerberoast -OutputFormat hashcat`

### What to Do With the Hash

Once you have captured the hash of the user account, you can use this to perform lateral movement in the targeted Active Directory environment.

In the Kerberoast attack, this is done by cracking the password hash returned in the TGS ticket using a password cracking tool and using the plaintext password to impersonate that service account to access any network resources the account has permission to access.

## Conclusion

Kerberoasting is an incredibly powerful attack for hackers to have in their arsenal. It allows them to impersonate service accounts in Active Directory environments and grants them access to any network resources this account has permission to access. If the environment is poorly configured, this could lead to an entire domain being compromised!

To perform this attack, a hacker needs access to any authenticated Active Directory account and the SPN of the service account they want to attack. With these two pieces of information and a good password-cracking tool, they can wreak havoc on enterprises. 

