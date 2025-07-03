---
title: Wireshark
---

[[TryHackMe]]


[[software]] #tools #software #hacking 

---
# Wireshark Introductory Guide

**Wireshark** is a powerful network protocol analyzer used to capture and inspect data packets on a network. It’s widely utilized for troubleshooting, network analysis, and cybersecurity training. Below is an introductory guide to using Wireshark effectively:

## 1. Getting Started with Wireshark

- **Installation**:
  - For **Linux**: Install via your package manager (e.g., `sudo apt install wireshark`).
  - For **Windows/macOS**: Download from the [official Wireshark website](https://www.wireshark.org/).

- **Starting Wireshark**:
  Launch Wireshark from your applications menu or by typing `wireshark` in your terminal/command prompt (may require root/administrator privileges).

## 2. Basic Packet Capture

1. **Select a Network Interface**:
   - Open Wireshark and choose the network interface you wish to monitor (e.g., `eth0`, `wlan0`).
   - Click on the interface to start capturing packets.

2. **Start and Stop Capture**:
   - **Start**: Click the blue shark fin button or press `Ctrl + E`.
   - **Stop**: Click the red square button or press `Ctrl + E` again.

3. **Saving Capture Files**:
   - **Save**: `File > Save As` or `Ctrl + S` to save the captured packets as a `.pcap` file for later analysis.

## 3. Basic Navigation and Filters

- **Display Filter**:
  - Filters refine what packets are shown in the capture. Example filters:
    - **HTTP Traffic**: `http`
    - **TCP Traffic**: `tcp`
    - **IP Address Filter**: `ip.addr == 192.168.1.10`
    - **Port Filter**: `tcp.port == 80`
    - **Specific Protocol**: `dns`, `ftp`, `icmp`
  - Apply filters by typing them into the filter bar and pressing `Enter`.

- **Common Filter Examples**:
  ```plaintext
  ip.addr == 192.168.1.10   # Filter packets with this IP address
  tcp.port == 22            # Show only SSH traffic
  http.request              # Display only HTTP requests
  ```

## 4. Analyzing Packet Details

- **Packet List Pane**: Shows a summary of all captured packets.
- **Packet Details Pane**: Displays protocol layers of the selected packet.
- **Packet Bytes Pane**: Shows raw data of the packet in hexadecimal and ASCII format.

## 5. Capturing Specific Data

- **Capture Filters**:
  - Apply capture filters before starting a capture to limit what data is recorded. Example:
    ```plaintext
    host 192.168.1.10   # Capture only traffic to/from this IP
    port 80             # Capture only traffic on port 80
    ```

- **Setting Capture Filters**:
  - Go to `Capture > Options` and enter the desired filter under "Capture Filter".

## 6. Useful Features and Tools

- **Follow Streams**:
  - Right-click a packet and choose `Follow > TCP Stream` or `Follow > HTTP Stream` to view an entire conversation between two endpoints.

- **Color-Coding**:
  - Wireshark uses color-coding to make packet analysis easier. For example, TCP traffic may appear in a different color than UDP traffic.
  - Customize colors under `View > Coloring Rules`.

- **Statistics**:
  - Access tools under `Statistics` for deeper analysis like protocol hierarchy, conversations, and IO graphs.

## 7. Saving and Exporting Data

- **Exporting Packets**:
  - `File > Export Specified Packets` to export specific packets based on a filter.
- **Saving Packet Bytes**:
  - Right-click a packet and select `Export Packet Bytes` to save the raw data of a packet.

## 8. Best Practices and Tips

- **Run as Administrator/Root**:
  - To capture all network traffic, Wireshark may require administrator or root privileges.

- **Use Display Filters Effectively**:
  - Mastering display filters will make your analysis much more efficient.

- **Limit Capture Size**:
  - Capturing on busy networks can generate large files. Use capture filters and limit capture duration to manage file size.

This guide provides you with the foundational steps to start using Wireshark for network analysis and troubleshooting.
