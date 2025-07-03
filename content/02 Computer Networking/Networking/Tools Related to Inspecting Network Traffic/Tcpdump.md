---
title: Tcpdump
---

# Tcpdump Introductory Guide

**Tcpdump** is a powerful command-line packet analyzer used for network packet capturing. It allows users to display and capture packets being transmitted or received over a network. Below is a basic guide on how to use `tcpdump` effectively:

## 1. Basic Command Structure

- **Basic Command**:
  ```bash
  tcpdump
  ```
  This command will capture packets on the default network interface.

- **Specify an Interface**:
  ```bash
  tcpdump -i <interface_name>
  ```
  Example:
  ```bash
  tcpdump -i eth0
  ```

- **Capture Only a Certain Number of Packets**:
  ```bash
  tcpdump -c <packet_count> -i <interface_name>
  ```
  Example:
  ```bash
  tcpdump -c 10 -i eth0
  ```

## 2. Basic Filters

- **Capture Packets from a Specific Host**:
  ```bash
  tcpdump host <ip_address>
  ```
  Example:
  ```bash
  tcpdump host 192.168.1.1
  ```

- **Capture Packets from a Specific Port**:
  ```bash
  tcpdump port <port_number>
  ```
  Example:
  ```bash
  tcpdump port 80
  ```

- **Capture Traffic Only from Source or Destination**:
  ```bash
  tcpdump src <ip_address>
  tcpdump dst <ip_address>
  ```

- **Capture Traffic for a Specific Protocol**:
  ```bash
  tcpdump <protocol>
  ```
  Examples:
  ```bash
  tcpdump tcp
  tcpdump udp
  tcpdump icmp
  ```

## 3. Display Options

- **Verbose Mode**:
  ```bash
  tcpdump -v
  tcpdump -vv  # More verbose
  tcpdump -vvv # Most verbose
  ```

- **Print Packet Data in ASCII**:
  ```bash
  tcpdump -A
  ```

- **Print Packet Data in Hex and ASCII**:
  ```bash
  tcpdump -X
  ```

- **Timestamp Options**:
  ```bash
  tcpdump -tttt  # Human-readable timestamp
  ```

## 4. Saving and Reading Packet Captures

- **Save Packets to a File**:
  ```bash
  tcpdump -w <filename>.pcap -i <interface_name>
  ```
  Example:
  ```bash
  tcpdump -w capture.pcap -i eth0
  ```

- **Read Packets from a File**:
  ```bash
  tcpdump -r <filename>.pcap
  ```
  Example:
  ```bash
  tcpdump -r capture.pcap
  ```

## 5. Advanced Filters

- **Capture Packets Based on Network Range**:
  ```bash
  tcpdump net <network>/<CIDR>
  ```
  Example:
  ```bash
  tcpdump net 192.168.1.0/24
  ```

- **Logical Operators**:
  ```bash
  tcpdump host 192.168.1.1 and port 22
  tcpdump host 192.168.1.1 or host 10.0.0.1
  tcpdump not port 80
  ```

- **Filter by Packet Size**:
  ```bash
  tcpdump less <size>
  tcpdump greater <size>
  ```

## 6. Useful Tips and Best Practices

- **Run as Root/Administrator**:
  `tcpdump` typically requires elevated privileges to capture traffic.

- **Limit Packet Capture Size**:
  Use the `-s <snaplen>` option to limit the amount of data captured per packet:
  ```bash
  tcpdump -s 96 -i eth0
  ```

- **Review in Wireshark**:
  Use Wireshark to open `.pcap` files for a more user-friendly analysis.

- **Filter by Specific Keywords**:
  Apply filters for finer control, e.g., HTTP traffic:
  ```bash
  tcpdump -i eth0 'tcp port 80 and (((ip[2:2] - ((ip[0]&0xf)<<2)) - ((tcp[12]&0xf0)>>2)) != 0)'
  ```

This guide provides you with the foundational steps to start using `tcpdump` for network analysis and packet capturing.
