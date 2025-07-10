___
**Tags:** #cyber-security #best-practices #system-security #security-tools 

**Links:** 

---
(https://www.stationx.net/osint-framework/)

[[Sock Puppets]]
## What Is OSINT?

Open-source intelligence (OSINT) refers to publicly available information that can be collected from various sources. These sources include search engines, social media platforms, and even breached databases. In addition to these, intelligence can be gathered through geographical tools like maps, public government records, commercial databases, registries, job postings, and many other methods.

![[Pasted image 20240911101009.png]]

## Why Is OSINT Useful?

OSINT is extremely useful when performing a penetration test. This is part of the second step in the penetration testing process, known as reconnaissance, as it allows for the comprehensive gathering of publicly available information, setting the stage for more targeted and informed subsequent assessment phases.

## Understanding the OSINT Framework

[The OSINT framework](https://osintframework.com/) is a collection of resources and tools that can be used to perform intelligence gathering. It presents the information in a structured, hierarchal manner. The site's main purpose is to provide a resource for anyone seeking guidance on the tools and resources available in OSINT.
![[Pasted image 20240911101000.png]]


---

## How to Use the OSINT Framework Effectively

For this section, we will assume that we are working for E-Corp and are tasked with performing the reconnaissance phase of a penetration test by using OSINT, with our main objective of gaining initial access to the network. 

### Domain Information 

**Objective:** Discover subdomains and related resources of E-Corp to gather potential targets and identify patterns like common naming conventions.

![[Pasted image 20240911101118.png]]#### Subdomains - Discovery

**Objective**: Enumerate E-Corp's active and historical subdomains to map the digital footprint and expose hidden entry points.

**Tools to Use:**

- [theHarvester](https://github.com/laramies/theHarvester) (T): Extracts subdomains, emails, and more from different public sources.
- [Sublist3r](https://github.com/aboul3la/Sublist3r) (T): Integrates data from multiple sources to enumerate subdomains.
- [Recon-ng](https://github.com/lanmaster53/recon-ng) (T): A full-fledged reconnaissance tool. The framework has specific modules for subdomain discovery.
- [XRay](https://github.com/evilsocket/xray) (T): A tool that will bruteforce subdomains using a wordlist and DNS requests.

#### Certificate Search

**Objective**: Investigate SSL/TLS certificates associated with E-Corp to uncover subdomains and, based on those, infer certain aspects of its online infrastructure.

**Tools to Use:**

- [Crt.sh](https://crt.sh/?): Lists all the SSL certificates for a given domain name, which can expose subdomains.

#### Passive DNS

**Objective**: Collect historical DNS data related to E-Corp, track domain changes, and find potential areas of interest for further vulnerability assessment.

**Tools to Use:**

- [DNS Dumpster](https://dnsdumpster.com/): A domain research tool that can discover hosts related to a domain, providing DNS recon and intelligence gathering.
- [DNS History](https://dnshistory.org/): Provides historical DNS data, showing how a domain's DNS settings have evolved over time.
- [Mnemonic](https://passivedns.mnemonic.no/): A security service provider that offers PassiveDNS data.

With a list of potential subdomains and resources, our next steps could be validating their active status and scanning and enumeration to identify potential vulnerabilities. 

Simultaneously, we'll move on to sourcing valid email addresses associated with E-Corp. These email addresses could be vital if we come across any login portals, email servers, VPNs, etc., as they could potentially provide us entry points or further avenues for assessing E-Corp's security posture.

### Email Addresses

**Objective**: Identify and validate email addresses associated with E-Corp to determine potential points of contact or entry, which can be critical for [social engineering](https://www.stationx.net/social-engineering-penetration-testing/) campaigns targeting the company's employees or to be used to authenticate with different services.

#### Common Email Formats

**Objective**: Determine E-Corp's standard email address format to guess or generate a list of probable email addresses. By understanding the company's email format, we can make educated guesses about employee email addresses, even if we don't have any.

**Tools to Use:**

- [Email Format](https://www.email-format.com/): Provides insights into E-Corp's email naming conventions.
- [Email Permutator](http://metricsparrow.com/toolkit/email-permutator/): Assists in generating possible email combinations for E-Corp's employees based on known formats.

#### Email Search

**Objective**: Search for and compile a list of email addresses associated with E-Corp that can be used for later social engineering attempts or login attempts. 

**Tools to Use:**

- [Hunter](https://hunter.io/search): Discovers email addresses associated with E-Corp's domain, enabling a more targeted approach in communication attempts.
- [VoilaNorbert](https://www.voilanorbert.com/): Searches for specific email addresses connected to E-Corp employees, which can be essential for spear-phishing campaigns.
- theHarvester (T): Gathers emails associated with E-Corp and its subdomains, broadening the scope of potential contacts.

#### Email Verification

**Objective**: Confirm the authenticity of the email addresses associated with E-Corp. Verifying emails ensures we don't waste resources targeting inactive or incorrect addresses during our penetration or phishing tests.

**Tools to Use:**

- [MailboxValidator](https://www.mailboxvalidator.com/): Validates the format and genuineness of E-Corp's email addresses.
- [Email Hippo](https://tools.emailhippo.com/): Although not included in the framework, it’s a tool we recommend for verifying an email address. 

#### Breach Data

**Objective**: Assess if any of the identified email addresses from E-Corp have been compromised in public data breaches. This sensitive data can be leveraged to understand potential vulnerabilities or weaknesses in the company's security posture.

**Tools to Use:**

- [Have I been pwned?](https://haveibeenpwned.com/): Checks if E-Corp's email addresses have been part of known data breaches, potentially indicating compromised credentials.
- [DeHashed](https://dehashed.com/): Helps determine if E-Corp's email addresses or credentials have been exposed in any breaches.

With a list of email addresses associated with E-Corp compiled, our next reconnaissance step could include gathering intelligence from social media. Social platforms contain a trove of data on companies, employees, and relationships. 

### Social Networks

**Objective**: Identify profiles, connections, and digital footprints of E-Corp and its employees on social media platforms. This can give insights into the company's operations, staff, and potential vulnerabilities that can be exploited.

#### Facebook

**Tools to Use:**

- [FB Lookup ID](https://lookup-id.com/): Retrieves the numerical ID of a Facebook account or page. This ID can be crucial for certain automated tools that target Facebook profiles.
- [FB Email Search](https://www.facebook.com/search/top/?q=email%40gmail.com): Searches for Facebook profiles associated with a specific email address, potentially linking E-Corp emails to personal or professional Facebook accounts.

#### X (Formerly Twitter)

**Tools to Use:**

- [Twitter Advanced Search](https://twitter.com/search-advanced): Allows for detailed queries, which can be used to find tweets from E-Corp, its employees, or about specific topics related to the company.
- [Twitter Location Search](https://twitter.com/search?q=geocode%3A36.1143855%2C-115.1727518%2C1km&src=typd): Enables searches for tweets from specific locations, potentially revealing E-Corp events, employee activities, or sensitive information shared near the company premises.

#### Reddit

**Tools to Use:**

- [Reddit Comment History](https://roadtolarissa.com/javascript/reddit-comment-visualizer/): This allows you to explore a user's comment history on Reddit. We can gain insights into internal discussions or personal interests by analyzing comments from E-Corp's employees or official accounts.

With the information we have gathered from social networks, we can gain valuable insights into E-Corp's operations, upcoming events, employee details, and more. This data can be important for creating more effective [phishing campaigns](https://www.stationx.net/social-engineer-toolkit/), identifying key targets, or understanding the company's internal and external connections.

### Next Steps

While we can’t show you every tool or section in the framework, we have given you a great idea of how to use the OSINT framework effectively. 

From this point, you could perform further reconnaissance in other areas, such as username enumeration, document search, and using geolocation information to locate important public locations or business records to uncover more about the company's operations and potential weak points.

Once we have located relevant information, we could move into the next penetration testing phase: [scanning and enumeration](https://www.stationx.net/how-to-scan-vulnerabilities-with-nmap/), where we will actively probe the target's systems to discover vulnerabilities and potential entry points. We could also use any information gathered about employees and begin any phishing assessments if the company requests. 

### Gather And Organize Information

When performing your OSINT research, it's a good idea to keep all of your data organized so that you can further analyze this important information. You can use tools, note-taking apps, and mind maps to help you stay organized and maintain a clear overview of your findings.

#### Tools

**Hunchly**:

A tool built for online investigations. As you browse the web, [Hunchly](https://www.hunch.ly/) captures and organizes web pages automatically, ensuring you never miss important information.

#### Note Taking

**Obsidian:** A powerful knowledge base that works on top of a local folder of plain text Markdown files. [Obsidian’s](https://obsidian.md/) link-based structure is excellent for connecting various bits of information.

**Notion:** A versatile workspace where you can write, plan, collaborate, and organize. [Notion’s](https://www.notion.so/) templating feature can be particularly useful for OSINT, helping standardize how you document findings.

**CherryTree**:

[CherryTree](https://www.giuspen.net/cherrytree/) is a hierarchical note-taking application that also supports syntax highlighting.

**OneNote**:

Microsoft's digital note-taking app. [OneNote](https://www.microsoft.com/en-ca/microsoft-365/onenote/digital-note-taking-app) is great for organizing, storing, and sharing notes.

#### MindMaps

**MindMeister**:

A cloud-based mind mapping tool that allows you to easily access your mind maps from anywhere and share them with others. [MindMeiser](https://www.mindmeister.com/) offers real-time collaboration features, which can be especially helpful during team-based OSINT investigations.

**XMind**:

One of the most popular mind-mapping tools available. It offers a free version and is available across multiple platforms. [XMind](https://xmind.app/) is particularly useful for organizing thoughts and managing complex information, such as that found when performing OSINT.

### Analyze Data

After compiling and organizing all of your data, an important next step is to combine all of the information, make connections, and establish any links that can help identify vulnerabilities, streamline the penetration testing process, and provide a comprehensive overview of potential attack vectors within E-Corp's infrastructure. A great tool that can help you with this is [Maltego](https://www.maltego.com/).

Maltego is a powerful graph-based tool for collecting, visualizing, and understanding interconnected information. Maltego is highly effective for creating a visual map of relationships and connections.

## Legal and Ethical Considerations

What are the legal and ethical considerations you must consider when performing OSINT? 

Legally, you must adhere to privacy laws, data regulations, and other frameworks governing acquiring and handling information. 

Ethically, you should respect privacy, get consent if required, and use data fairly without ill intent - even if the law is unclear. 

When performing OSINT, you must balance gathering enough data to inform decisions while avoiding crossing legal or ethical boundaries.

Here are some important things to keep in mind.

- While the data sources in OSINT are public, the collection methods can sometimes violate terms of service. For example, web scraping might be against the terms of service of some websites.
- Some regions have stringent data protection regulations even if the information is publicly available. Collecting, storing, or processing personal data without consent might breach laws like the General Data Protection Regulation (GDPR) in Europe.
- In penetration testing, always ensure you have explicit permission to gather information. Even if OSINT is passive, collecting information without a client's consent can lead to legal complications. All of this should be included in the scope of the pentest.

Next, let’s quickly discuss the difference between passive and active OSINT. 

**Passive** OSINT involves collecting publicly available information without directly interacting with it. You are purely observing the information. Some examples include:

- Browsing the public sections of a company's website to gather information about its services, technologies used, and employees.
- Observing posts, followers, comments, and other details from public profiles on platforms like X (Twitter), LinkedIn, and Facebook.
- Using services like WHOIS to check domain ownership details.

In **active** OSINT, you directly interact with a person or system and can include:

- Sending friend requests, messages, or connection requests to targets on social networks.
- Scanning ports on a system. While typically associated with more active forms of recon beyond just OSINT, scanning a company's IP addresses to determine open ports is a direct interaction and is often illegal without explicit permission.

As a general rule, passive information gathering is permissible in many jurisdictions. Active information gathering, on the other hand, can result in legal issues without explicit consent.

## Conclusion

The OSINT framework is an invaluable resource when you're seeking a collection of tools to gather publicly available information from various sources efficiently.

You should now understand how to use the OSINT framework and what kind of information can be gathered.

[[Using Maltego]]