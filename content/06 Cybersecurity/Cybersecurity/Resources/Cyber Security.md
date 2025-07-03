---
{}
---

Tags:
[[Information Technology]]
[[Personal Learning]]

# **Resources**



---

Welcome to the central repository for all things related to cybersecurity. This note provides links and summaries for major domains in cybersecurity, from threat intelligence to user education, organized for quick reference and deeper exploration.


[[Purple Team]]

#### Security Architecture

Security architecture is a comprehensive security design that considers both the requirements and potential hazards present in a particular situation or environment. Additionally, it details where and when to implement security controls.

- **Network Security:** Assuring the confidentiality, integrity, and availability (referred to as [the CIA Triad](https://www.stationx.net/what-is-the-cia-triad/)) of a network or system. Penetration testers will attempt to counterman the protections clients and vendors put into place to keep the CIA Triad in place.
- **Patch Management:** Ensuring all the latest updates and security fixes are in place on systems and programs. Penetration testers often look for out-of-date systems and missing security patches to attack and gain a foothold on a system.
- **Baseline Configuration:** “A set of specifications for a system, or Configuration Item (CI) within a system, that has been formally reviewed and agreed on at a given point in time, and which can be changed only through change control procedures. The baseline configuration is used as a basis for future builds, releases, and/or changes.” (NIST SP 800-128 under Baseline Configuration). Pentesters will test the security of baseline configurations and help create one that is more secure for the client.
- **DDoS Protection**: [DDoS, or Distributed Denial of Service](https://www.stationx.net/ddos-statistics/), is an attack where a system is flooded with malicious junk data, usually ping requests, to slow the service for legitimate users. The goal is to make the system unusable or crash due to its inability to manage the flood of requests. These attacks are often performed through botnets (a vast network of infected and enslaved computers managed by a single hacker). Pentesters may be asked to perform a controlled simulation to test a client’s ability to handle such an attack.
- **Secure System Build**: The design and implementation of a “hardened” network, software, machine instance, or other infrastructure. A penetration test's purpose is to audit a system's security and assist clients in closing holes in their security.
- **Certificate Management**: Monitoring, enabling, and executing digital SSL certificates are all parts of certificate administration. It is essential to the continued operation, encryption, and security of client-server connections.
- **Cryptography**: The use of complex math to obfuscate digital communication or documents and make them unreadable by anyone other than the intended recipients. The method is referred to as “encryption.” Any time you require a password to read a document or see the little padlock icon in your web browser's URL address bar, encryption is used to secure the information. Pen testers will use a variety of tools to try and brute force or bypass this encryption.
- **Access Contro**l: By validating various login credentials, such as usernames and passwords, PINs, biometric scans, and security tokens, “access control” identifies users. Pentesters will attempt to circumvent access controls to gain access to systems.
- **Key and Secret Management**: Key and secret management is the safe and easy storing of API keys, passwords, certificates, and other private information. Use it to manage, access, and audit information meant to be kept secret.
- **Cloud Security**: Cloud is currently the fastest-growing networking technology. Public cloud systems (such as Amazon Web Services (AWS), Microsoft Azure, and Google Cloud) and private cloud systems (such as those offered by Oracle and VMWare) are replacing traditional physical on-premises systems due to their low startup costs and ability to quickly expand and decrease resources as needed. The growing popularity of cloud-based systems has made them an attractive target for hackers and bad actors. Pen testers have unique methods to test and protect these systems.
- **Identity and Access Management**: “Identity management (IdM), also known as identity and access management (IAM), ensures that authorized people – and only authorized people – have access to the technology resources they need to perform their job functions.” ([VMWare](https://www.vmware.com/topics/glossary/content/identity-management.html)) Pen Testers see if they can beat identity management by forging/assuming the necessary identity, creating a new one with authorization, or bypassing it entirely.
- ---

#### Application Security

The process of developing and testing application security features to prevent vulnerabilities and defend against attacks.

- **Source Code Scan**: When performing a “white-box test,” penetration testers are given access to internal information not available to the public, including the source code of the systems and software they are testing. This allows them to review the code and more efficiently look for security vulnerabilities resulting from mistakes in the programming.
- **API Security**: Application Programming Interface (API) is the interface between software and a user. Most Software-as-a-Service (such as Google Maps and Twitter) are considered APIs. Some companies create public APIs that programmers can call back to and use in their software, such as facial or voice recognition systems. APIs have become a common part of web app pentesting.
- --
#### Frameworks and Standards

A set of rules, recommendations, and best practices for controlling hazards in the digital sphere. Security goals, such as preventing unauthorized system access, are often matched with controls, such as proper password policies, etc.

- **OWASP Top 10**: A [reference standard](https://owasp.org/www-project-top-ten/) for the most critical web application security risks. Ethical hackers will use this standard as a reference guide to test a client’s system.
- **NIST Cyber Security Framework**: A set of [best practices and recommendations](https://www.nist.gov/cyberframework) for cyber security from the National Institute of Standards and Technology.
- ---
#### Physical Security

Physical Security limits access to areas where data and system controls are located. Fences, gates, security personnel, cameras, RFID badges, locks, etc., can keep out cyber criminals who wish to get on-premises and access data/devices directly.

- **SCADA/ICS**: Supervisory Control and Data Acquisition / Industrial Control Systems, such as those used in power plants, manufacturing, water treatment, etc. Attacks on these systems have become a terrifying favorite among nation-states and must be secured.
- **IoT Security**: The testing and security of Internet of Things (IoT) devices such as “smart home” systems. IoT devices are notoriously insecure, many lacking proper encryption and security controls or using very simple default passwords. Penetration testers will test the security of these systems and attempt to use them as a springboard into other client systems.
---
#### Risk Assessment

Determining a system's security risks, including the vulnerability's severity and potential impact if exploited.

- **Vulnerability Scan**: A wide scan, usually using an automated tool such as [Nessus](https://www.tenable.com/products/nessus), to look for known vulnerabilities and security risks; often one of the early steps in a penetration test.
- **Red Team**: A specific penetration testing team of ethical hackers who attempts to fully simulate a real attack and stay undetected. A standard penetration test can be similar to a house inspection where people know you are there and your purpose; in a red team test, you stay hidden from the security team and do not leave any traces. As a result, red team engagements often run longer than a standard pentest but more accurately simulate a real threat actor.
- **Penetration Test**: The assessment of a system’s security through a simulated attack.
- **DAST**: Dynamic Application Security Testing - analyzing web applications to find vulnerabilities.
- **Application Pen Tests**: The security testing of an “application,” typically a website, but can extend to applications used for blockchain, eCommerce, APIs, front and back-end servers, etc.
- **Social Engineering**: The manipulation of a human to convince them to act against their own self-interest or the interest of the company through deception.
- **Bug Bounty**: The [**open call for testing vulnerabilities or bugs in an application**](https://www.stationx.net/bug-bounty-programs-for-beginners/). These are often held by either the client organization directly or through a broker, such as [Bugcrowd](https://bugcrowd.com/).
---
#### User Education

Educating end-users on cyber security practices and training individuals in any of the cyber security domains, such as ethical hacking, cyber forensics, and malware analysis.

- **Cyber Security Table-Top Exercise**: Meetings used to walk through security incidents, how to prepare for them, and how to respond when they occur. Usually the domain of the defensive security team, this can be done as part of the pentest debrief or as a stand-in for systems too sensitive to risk active testing.
---
#### Governance

Establishing a system for cybersecurity governance guarantees that a company's security programs align with its business goals, adhere to rules and regulations, and meet goals for managing security and risk.

**Compliance and Enforcement**
- Some countries require private companies to perform a penetration test as part of legal compliance for particular industries or systems, often when sensitive information is involved, such as credit cards and medical personal identifiable information (PII).