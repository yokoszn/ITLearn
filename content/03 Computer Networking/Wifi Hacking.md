---
title: Wifi Hacking
---
[[TryHackMe]]

We'll want to use aircrack-ng, airodump-ng and airmon-ng from the [[Aircrack-ng Suite]] to attack WPA networks.

To generate 5 random passwords from rockyou, you can use this command on Kali: `head /usr/share/wordlists/rockyou.txt -n 10000 | shuf -n 5 -`  
You will need a monitor mode NIC in order to capture the 4 way handshake. Many wireless cards support this, but it's important to note that not all of them do.

Injection mode helps, as you can use it to deauth a client in order to force a reconnect which forces the handshake to occur again. Otherwise, you have to wait for a client to connect normally.