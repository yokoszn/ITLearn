[[TryHackMe]] [[software]] #hacking #Learning #certification-prep #tools #knowledge-base 

---
# Nmap Introductory Guide

**Nmap (Network Mapper)** is a powerful, open-source tool used for network discovery and security auditing. It is widely used to identify live hosts, open ports, services, and operating systems on a network. Here's an introductory guide on how to use Nmap effectively through the command line:

## 1. Basic Nmap Commands

- **Scan a Single IP**:
  ```bash
  nmap <target_ip>
  ```

- **Scan Multiple IPs**:
  ```bash
  nmap <ip1> <ip2> <ip3>
  ```

- **Scan a Range of IPs**:
  ```bash
  nmap <target_ip_range>
  ```
  Example:
  ```bash
  nmap 192.168.1.1-10
  ```

- **Scan an Entire Subnet**:
  ```bash
  nmap 192.168.1.0/24
  ```

## 2. Port Scanning

- **Scan for Specific Ports**:
  ```bash
  nmap -p <port_number> <target_ip>
  ```
  Example:
  ```bash
  nmap -p 22,80,443 192.168.1.1
  ```

- **Scan All Ports**:
  ```bash
  nmap -p- <target_ip>
  ```

- **Scan Common Ports**:
  ```bash
  nmap <target_ip>
  ```
  This command scans the top 1,000 most common ports.

## 3. Service and Version Detection

- **Detect Versions of Services Running**:
  ```bash
  nmap -sV <target_ip>
  ```

- **Aggressive Scan (Includes OS Detection, Version Detection, and More)**:
  ```bash
  nmap -A <target_ip>
  ```

## 4. Operating System Detection

- **Detect Operating System**:
  ```bash
  nmap -O <target_ip>
  ```

- **Combined Scan with OS and Version Detection**:
  ```bash
  nmap -A -O <target_ip>
  ```

## 5. Saving Scan Results

- **Save Results to a File (Normal Format)**:
  ```bash
  nmap -oN <output_file> <target_ip>
  ```

- **Save Results to a File (XML Format)**:
  ```bash
  nmap -oX <output_file> <target_ip>
  ```

- **Save Results to a File (Grepable Format)**:
  ```bash
  nmap -oG <output_file> <target_ip>
  ```

## 6. Advanced Nmap Scans

- **Scan with Specific Timing Template (1-5, Slow to Fast)**:
  ```bash
  nmap -T4 <target_ip>
  ```

- **Scan with No DNS Resolution**:
  ```bash
  nmap -n <target_ip>
  ```

- **Scan with Spoofed Source IP**:
  ```bash
  nmap -S <spoofed_ip> <target_ip>
  ```

## 7. Useful Tips

- **Combine Options for More Comprehensive Scans**:
  ```bash
  nmap -p- -sV -O -A -T4 <target_ip>
  ```

This guide should help you get started with the fundamentals of Nmap and prepare you for more complex network discovery and security auditing tasks.

