___
**Tags:** 

**Links:** 

---
[[Network Forensics]]
[[Digital Forensics]]


**NetworkMiner in a Nutshell**

  

|   |   |
|---|---|
|**Capability**|**Description**|
|Traffic sniffing|It can intercept the traffic, sniff it, and collect and log packets that pass through the network.|
|Parsing PCAP files|It can parse pcap files and show the content of the packets in detail.|
|Protocol analysis|It can identify the used protocols from the parsed pcap file.|
|OS fingerprinting|It can identify the used OS by reading the pcap file. This feature strongly relies on [Satori](https://github.com/xnih/satori/) and [p0f](https://lcamtuf.coredump.cx/p0f3/).|
|File Extraction|It can extract images, HTML files and emails from the parsed pcap file.|
|Credential grabbing|It can extract credentials from the parsed pcap file.|
|Clear text keyword parsing|It can extract cleartext keywords and strings from the parsed pcap file.|

  

**We are using NetworkMiner free edition in this room, but a Professional edition has much more features. You can see the differences between free and professional versions** [**here**](https://www.netresec.com/?page=NetworkMiner)**.**  

Operating Modes

  

There are two main operating modes;

  

- Sniffer Mode: Although it has a sniffing feature, it is not intended to use as a sniffer. The sniffier feature is available only on Windows. However, the rest of the features are available in Windows and Linux OS. Based on experience, the sniffing feature is not as reliable as other features. Therefore we suggest not using this tool as a primary sniffer. Even the official description of the tool mentions that this tool is a "Network Forensics Analysis Tool", but it can be used as a "sniffer". In other words, it is a Network Forensic Analysis Tool with but has a sniffer feature, but it is not a dedicated sniffer like Wireshark and tcpdump. 

- Packet Parsing/Processing: NetworkMiner can parse traffic captures to have a quick overview and information on the investigated capture. This operation mode is mainly suggested to grab the "low hanging fruit" before diving into a deeper investigation.

  

**Pros and Cons** 

As mentioned in the previous task, NetworkMiner is mainly used to gain an overview of the network. Before starting to investigate traffic data, let's look at **the pros and cons of the NetworkMiner.**  

**Pros  
  
**

- OS fingerprinting
- Easy file extraction  
    
- Credential grabbing
- Clear text keyword parsing
- Overall overview

**Cons**

- Not useful in active sniffing
- Not useful for large pcap investigation
- Limited filtering
- Not built for manual traffic investigation

Differences Between Wireshark and NetworkMiner  

  

NetworkMiner and Wireshark have similar base features, but they separate in use purpose. Although main functions are identical, some of the features are much stronger for specific use cases.  


The best practice is to record the traffic for offline analysis, quickly overview the pcap with NetworkMiner and go deep with Wireshark for further investigation.  
  

|                             |                                                      |                   |
| --------------------------- | ---------------------------------------------------- | ----------------- |
| **Feature**                 | **NetworkMiner**                                     | **Wireshark**     |
| Purpose                     | Quick overview, traffic mapping, and data extraction | In-Depth analysis |
| GUI                         | ✅                                                    | ✅                 |
| Sniffing                    | ✅                                                    | ✅                 |
| Handling PCAPS              | ✅                                                    | ✅                 |
| OS Fingerprinting           | ✅                                                    | ❌                 |
| Parameter/Keyword Discovery | ✅                                                    | Manual            |
| Credential Discovery        | ✅                                                    | ✅                 |
| File Extraction             | ✅                                                    | ✅                 |
| Filtering Options           | Limited                                              | ✅                 |
| Packet Decoding             | Limited                                              | ✅                 |
| Protocol Analysis           | ❌                                                    | ✅                 |
| Payload Analysis            | ❌                                                    | ✅                 |
| Statistical Analysis        | ❌                                                    | ✅                 |
| Cross-Platform Support      | ✅                                                    | ✅                 |
| Host Categorisation         | ✅                                                    | ❌                 |
| Ease of Management          | ✅                                                    | ✅                 |
