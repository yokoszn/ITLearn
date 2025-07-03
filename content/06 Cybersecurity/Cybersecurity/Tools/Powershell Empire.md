___
**Tags:** [[Powershell]] [[tools]] [[hacking]] [[frameworks]]

**Links:**(https://www.stationx.net/how-to-use-powershell-empire/)

---

owerShell Empire is a notorious Command and Control (C2) framework hackers use in real-world cyber attacks. It has been used to target large companies through phishing emails, public-facing IT system exploits, and watering-hole attacks. It is also one of the most used open-source C2 frameworks by penetration testers and red teamers.

This guide will teach you how to use PowerShell Empire to perform privilege escalation, install persistence mechanisms, and dump credentials. Along the way, you will discover why this C2 framework is so popular in the security community, its main components, and how to use them.

So put on your hacker hat, and let’s get started emulating adversaries in this comprehensive guide to the PowerShell Empire framework!

## What Is PowerShell Empire?

PowerShell Empire is an open-source post-exploitation framework that [penetration testers and red teams](https://www.stationx.net/red-teaming-vs-penetration-testing/) use to perform adversary emulation. It is designed to aid users in performing the [post-exploitation phase of an attack](https://www.stationx.net/penetration-testing-steps/), where they must maintain control over compromised systems, perform lateral movement, elevate privileges, and exfiltrate data.

The framework focuses on targeting Windows environments using the [PowerShell scripting language](https://www.stationx.net/powershell-cheat-sheet/) to automate attacks and execute malicious commands. PowerShell Empire has three main components:

- **Empire Server** - This is written in Python and comprises modules that add different functionality.
- **Empire Client** - This comes built-in with PowerShell Empire and lets you access the Empire Server remotely.
- **GUI Client** - This provides a graphical interface for accessing the Empire Server that is called Starkiller.

To use PowerShell Empire, you execute a _Stager_ on a target system. This _Stager_ is a small piece of code that communicates to the Empire Server and generates an _Agent_, providing you remote access to the target system. The Empire Client (or GUI Client) lets you connect to the Empire Server and interact with this _Agent_ through built-in commands or more complex Empire _Modules_.

---

**Advantages of PowerShell Empire:**

- Strong integration with PowerShell allows it to automate post-exploitation activities using Powershell scripts that are executed in memory, making it harder to detect.

- It is designed for the post-exploitation phase of an attack and has inbuil tooling for privilege escalation, lateral movement, and data exfiltration

- It has a modular architecture allowing you to extend the framework to suit your needs.

- It is backed by an active community that provides ongoing updates and new features.

**Disadvantage of PowerShell Empire:**

- It is Windows-centric and has limited functionality outside Windows environments.

- Modern security solutions that gather PowerShell logs (or block it entirely) severely impact PowerShell Empire’s capabilities.

- The framework has a learning curve for new users who need to understand PowerShell scripting and how the framework functions.