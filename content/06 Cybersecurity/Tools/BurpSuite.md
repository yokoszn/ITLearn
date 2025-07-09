___
**Tags:**
[[hacking]]
[[Linux]]
[[Cyber Security]]
[[information]]
[[tools]]
[[Career]]

**Links:** 

---
(https://www.stationx.net/how-to-use-burp-suite/)
[[BurpSuite - Guide]]
## What Is Burp Suite?

Burp Suite was developed by PortSwigger and started in 2003 by creator Dafydd Stuttard, who wrote the first version of Burp, with actual burping sounds. A favorite of **[bug bounty hunters](https://www.stationx.net/bug-bounty-programs-for-beginners/)**, Burp is a collection of web application testing tools designed for penetration testing.

At its core, Burp functions as an interception proxy, allowing users to redirect browser traffic through the Burp proxy server while targeting specific web applications, making it an essential tool for identifying and addressing web application vulnerabilities.

Burp Suite tools include features such as Proxy, Repeater, Intruder, Comparer, Extender, and Extensions, which allow for rapid and versatile testing of web applications.

By intercepting and modifying HTTP/HTTPS traffic between a user's browser and a target web application, it enables security professionals to identify vulnerabilities and potential attack vectors.

---

- **Proxy**: The Burp Proxy is the most renowned aspect of Burp Suite. It enables interception and modification of requests and responses while interacting with web applications.
- **Repeater**: Another well-known feature. [Repeater](https://tryhackme.com/room/burpsuiterepeater) allows for capturing, modifying, and resending the same request multiple times. This functionality is particularly useful when crafting payloads through trial and error (e.g., in SQLi - Structured Query Language Injection) or testing the functionality of an endpoint for vulnerabilities.
- **Intruder**: Despite rate limitations in Burp Suite Community, [Intruder](https://tryhackme.com/room/burpsuiteintruder) allows for spraying endpoints with requests. It is commonly utilized for brute-force attacks or fuzzing endpoints.
- **Decoder**: [Decoder](https://tryhackme.com/room/burpsuiteom) offers a valuable service for data transformation. It can decode captured information or encode payloads before sending them to the target. While alternative services exist for this purpose, leveraging Decoder within Burp Suite can be highly efficient.
- **Comparer**: As the name suggests, [Comparer](https://tryhackme.com/room/burpsuiteom) enables the comparison of two pieces of data at either the word or byte level. While not exclusive to Burp Suite, the ability to send potentially large data segments directly to a comparison tool with a single keyboard shortcut significantly accelerates the process.
- **Sequencer**: [Sequencer](https://tryhackme.com/room/burpsuiteom) is typically employed when assessing the randomness of tokens, such as session cookie values or other supposedly randomly generated data. If the algorithm used for generating these values lacks secure randomness, it can expose avenues for devastating attacks.

Beyond the built-in features, the Java codebase of Burp Suite facilitates the development of extensions to enhance the framework's functionality. These extensions can be written in Java, Python (using the Java Jython interpreter), or Ruby (using the Java JRuby interpreter). The **Burp Suite Extender** module allows for quick and easy loading of extensions into the framework, while the marketplace, known as the **BApp Store**, enables downloading of third-party modules. While certain extensions may require a professional license for integration, there are still a considerable number of extensions available for Burp Community. For instance, the **Logger++** module can extend the built-in logging functionality of Burp Suite.
## Burp Proxy

To get started using Burp Suite, we need to turn on its proxy and start intercepting traffic.

### How a Proxy Works

A proxy, in simple terms, is a server between a client (such as a browser) and a server (such as a web application).

You can think of a proxy like a translator between two people who speak different languages. The translator (proxy) listens to one person (client), translates their message, and relays it to the other person (target server). Then, the translator listens to the response, translates it, and forwards it to the first person.

In this analogy, the translator can modify the message or response as needed, just like a proxy can manipulate network traffic between a client and a server.

![[Pasted image 20240911103901.png]]


When using Burp Suite, it's crucial to understand how to work with its proxy feature effectively. The Burp Proxy will enable you to intercept HTTP requests to inspect and modify the network traffic between your browser and the target application.

From this point forward, we will use the [DVWA](https://www.kali.org/tools/dvwa/) (Damn Vulnerable Web Application) as our target to show you how to use the tools in Burp Suite. There are many other programs to help you learn web application testing using Burp Suite, such as [OWASP juice shop](https://owasp.org/www-project-juice-shop/) and [bWAPP](http://www.itsecgames.com/) to name a few.

If you are looking for a way to set up your own virtual hacking lab, see our [How to Create a Virtual Hacking Lab: The Ultimate Hacker Setup.](https://www.stationx.net/how-to-create-a-virtual-hacking-lab/)

### Setting Target Scope

The next step in our Burp Suite tutorial is setting the scope. The target scope defines the range of the project and ensures that the test is performed only on the specified domains, subdomains, and URL paths, rather than the entire internet.

To define the target scope in Burp Suite, follow these steps:

1. Go to the **Target** tab at the top of the interface.
2. Select the **Scope settings** sub-tab to define your target application's scope.
3. Click the **Add** button in the "Target scope" section to specify which URLs or domains to include in the target scope.
---

## Burp Repeater

In this section of our Burp Suite tutorial, we will discuss how to use the Repeater tool and its use in manual vulnerability assessments.

The Repeater tool allows you to modify and resend HTTP or WebSocket messages. This can be useful to test for input-based vulnerabilities or varying parameter values.

We can grab a request with the Burp Proxy, make changes, and then send the same request over and over as many times as we want, such as when we create requests from scratch using a command line tool like cURL.
![[Pasted image 20240911103929.png]]

---

## Burp Intruder

Burp Suite's Intruder is a powerful tool for automating customized attacks against web applications. You can use it to test various inputs and identify potential vulnerabilities. For example, by intercepting a request using a login attempt, we could use Intruder to switch out the username and password fields for values from a wordlist.

![[Pasted image 20240911103959.png]]
To fully utilize the speed of Intruder, Burp Professional is required. Although Intruder can still be used with Burp Community, it is significantly rate-limited. Therefore most people use alternative tools for this task.
	There are four common attack types in Intruder:

- **Sniper:** Uses one payload set and injects the payloads one by one into all selected positions.
- **Battering ram:** Uses one payload set and injects the same payload into all selected positions simultaneously.
- **Pitchfork:** Requires two or more payload sets and uses corresponding payloads from each set for each position.
- **Cluster bomb:** Requires multiple payload sets and tests payloads in all combinations for each position.
---
## Burp Extensions

There are numerous free extensions available in the BApp Store, compatible with the Burp Suite Community edition. Some popular examples include:

**Param Miner**: Useful for discovering hidden parameters in web applications.

**Hackvertor**: A tool that will transform, interpret, encode, decode, cipher, decipher, generate hashes, condense, expand, modify, and manage data.

**CO2**: A collection of tools, including SQL Mapper, JWT Decoder, and Hasher, designed to simplify and automate various tasks in the testing process.

Remember to explore the BApp Store regularly, as new extensions are added frequently. Try different extensions to find the ones that best suit your needs.