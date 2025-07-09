[[Penetration Testing Tools for Kali Linux]]
___
**Tags:** #tools #hacking [[Reconnaissance]] #Networking

**Links:** 

---


[Bettercap Tutorial & Top Commands (2024 Update) (stationx.net)](https://www.stationx.net/bettercap-tutorial/)

Bettercap is a versatile tool for network reconnaissance, enabling a range of activities, including seamless man-in-the-middle attacks.

In this Bettercap tutorial, we’ll explain what Bettercap is, briefly discuss ARP spoofing and man-in-the-middle attacks, and show you its most used features so you can utilize the tool effectively.

We’ll walk you through setting it up and then show you some of its functionalities, including ARP and DNS spoofing, port scanning, finding cleartext credentials when insecure protocols are used, and WiFi hacking.


## What Is Bettercap?

[Bettercap](https://www.bettercap.org/), a portable framework written in GO, is often considered a Swiss army knife for its extensive capabilities in performing reconnaissance, [attacking WiFi](https://www.stationx.net/how-to-hack-wifi-with-kali-linux/), and scanning Bluetooth low-energy devices and Ethernet networks.

It’s a tool used by many in cyber security, including [penetration testers](https://www.stationx.net/how-to-become-a-penetration-tester/), reverse engineers, and security researchers, to perform MitM (Man-in-the-Middle) attacks, also known as on-path attacks.

Bettercap allows you to leverage all the features needed to analyze networks and devices and builds upon classic tools like Ettercap to create an advanced modern suite for wired and wireless network attacks.

Some of its features include:

- IP host discovery and reconnaissance
- Network spoofing attacks via ARP, DNS, NDP, DHCPv6 poisoning
- Port scanning
- WiFi network scanning and attacks like de-authentication and WPA/WPA2 handshake capturing

Bettercap can be installed on [Windows](https://www.stationx.net/windows-command-line-cheat-sheet/), [Linux](https://www.stationx.net/linux-security-tools/), macOS, and Android.

---

## Pre-Installed Bettercap Commands and Modules

> [!NOTE]
>  To see a list of available commands and modules, you can enter `help`.

Bettercap comes installed with modules. Modules extend the capabilities of Bettercap and are based on the type of functionality they provide.

These modules can be loaded and used during a Bettercap session and include:

- **Various modules**: Essential for the framework's operation, such as events, UI, and API
- **Bluetooth LE**: Modules for Bluetooth Low Energy devices scanning, reconnaissance and attacks
- **WiFi**: Modules relating to WiFi networks, access points, client attacks, etc.
- **HID on 2.4 GHz**: MouseJacking and wireless HID attacks
- **IPv4/IPv6**: Network host/topology discovery, sniffing, spoofing IPv4/v6 networks
- **Proxies**: man-in-the-middle proxy modules
- **Servers**: modules to create various simple servers
- **Utils**: miscellaneous utility modules providing additional functionality