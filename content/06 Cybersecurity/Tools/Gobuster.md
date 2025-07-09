# Gobuster Introductory Guide

**Gobuster** is a command-line tool used for brute-forcing directories and files, DNS subdomains, and virtual hostnames on web servers. It's fast, written in Go, and commonly used during penetration testing to enumerate hidden files and directories that aren't easily visible.

**Gobuster** is an open-source offensive tool written in Golang. It enumerates web directories, DNS subdomains, vhosts, Amazon S3 buckets, and Google Cloud Storage by brute force, using specific wordlists and handling the incoming responses. Many security professionals use this tool for penetration testing, bug bounty hunting, and cyber security assessments. Looking at the phases of ethical hacking, we can place Gobuster between the reconnaissance and scanning phases.

## 1. Basic Command Structure

- **Basic Syntax**:
  ```bash
  gobuster <mode> -u <target_url> -w <wordlist_path> [options]
  ```
  - `<mode>`: The type of scan (`dir`, `dns`, or `vhost`).
  - `-u <target_url>`: The URL or IP to scan.
  - `-w <wordlist_path>`: The path to the wordlist used for brute-forcing.

## 2. Directory and File Enumeration

- **Basic Directory Scan**:
  ```bash
  gobuster dir -u http://example.com -w /path/to/wordlist.txt
  ```

- **Common Options**:
  - `-x <extensions>`: Specify file extensions (e.g., `-x php,html,txt`).
  - `-t <threads>`: Set the number of concurrent threads (default is 10).
  - `-o <output_file>`: Save the results to a file.
  - `-r`: Do not follow redirects.
  - `-q`: Suppress banner and only show output.

- **Example with Options**:
  ```bash
  gobuster dir -u http://example.com -w /path/to/wordlist.txt -x php,html -t 50 -o results.txt
  ```

## 3. DNS Subdomain Enumeration

`dns` mode. This mode allows Gobuster to brute force subdomains. During a penetration test,  checking the subdomains of your target’s top domain is essential. Just because something is patched in the regular domain, it doesn't mean it is also patched in the subdomain. An opportunity to exploit a vulnerability in one of these subdomains may exist. For example, if TryHackMe owns _tryhackme.thm_ and _mobile.tryhackme.thm_, there may be a vulnerability in _mobile.tryhackme.thm_ that is not present in _tryhackme.thm_. That is why it is important to search for subdomains as well!

## Help

If you want a complete overview of what the Gobuster dns command can offer, you can have a look at the help page. Seeing the extensive help page for the `dns` command can be intimidating. So, we will focus on the most important flags in this room. Type the following command to display the help: `gobuster dns --help`  

The `dns` mode offers fewer flags than the `dir` mode. But these are more than enough to cover most DNS subdomain enumeration scenarios. Let us have a look at some of the commonly used flags:

|Flag|Long Flag|Description|
|---|---|---|
|`-c`|`--show-cname`|Show CNAME Records (cannot be used with the `-i` flag).|
|`-i`|`--show-ips`|Including this flag shows IP addresses that the domain and subdomains resolve to.|
|`-r`|`--resolver`|This flag configures a custom DNS server to use for resolving.|
|`-d`|`--domain`|This flag configures the domain you want to enumerate.|

### How to Use dns Mode

To run Gobuster in dns mode, use the following command syntax:  
`gobuster dns -d example.thm -w /path/to/wordlist`  

Notice that the command also includes the flags `-d` and `-w`, in addition to the `dns` keyword. These two flags are required for the Gobuster subdomain enumeration to work. Let us look at an example of how to enumerate  subdomains with Gobuster dns mode:

`gobuster dns -d example.thm -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt`

- `gobuster dns` enumerates subdomains on the configured domain.  
    
- `-d example.thm` sets the target to the _example.thm_ domain.  
    
- `-w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt` sets the wordlist to s_ubdomains-top1million-5000.txt_. Gobuster uses each entry of this list to construct a new DNS query. If the first entry of this list is 'all', the query would be _all.example.thm._

- **DNS Mode**:
  ```bash
  gobuster dns -d example.com -w /path/to/wordlist.txt
  ```
  - `-d <domain>`: The domain to scan.
  - `-i`: Show only valid subdomains.

- **Example**:
  ```bash
  gobuster dns -d example.com -w /path/to/subdomains.txt -o dns_results.txt
  ```

## 4. Virtual Host Enumeration
The last and final mode we’ll focus on is the `vhost` mode. This mode allows Gobuster to brute force virtual hosts. Virtual hosts are different websites on the same machine. Sometimes, they look like subdomains, but don’t be deceived! Virtual hosts are IP-based and are running on the same server. Subdomains are set up in DNS. The  difference between `vhost` and `dns` mode is in the way Gobuster scans:

- `vhost` mode will navigate to the URL created by combining the configured HOSTNAME (-u flag) with an entry of a wordlist.
- `dns` mode will do a DNS lookup to the FQDN created by combining the configured domain name (-d flag) with an entry of a wordlist.

## Help

If you want a complete overview of what the Gobuster `vhost` command can offer, you can have a look at the help page. Seeing the extensive help page for the vhost command can be intimidating. So, we will focus on the most important flags in this room. Type the  following command to display the help: `gobuster vhost --help`  

The `vhost` mode offers flags similar to those of the dir mode. Let us have a look at some of the commonly used flags:

| **Short Flag** | **Long Flag**       | **Description**                                                                                       |
| -------------- | ------------------- | ----------------------------------------------------------------------------------------------------- |
| `-u`           | `--url`             | Specifies the base URL (target domain) for brute-forcing virtual hostnames.                           |
|                | `--append-domain`   | Appends the base domain to each word in the wordlist (e.g., word.example.com).                        |
| `-m`           | `--method`          | Specifies the HTTP method to use for the requests (e.g., GET, POST).                                  |
|                | `--domain`          | Appends a domain to each wordlist entry to form a valid hostname (useful if not provided explicitly). |
|                | `--exclude-length`  | Excludes results based on the length of the response body (useful to filter out unwanted responses).  |
| `-r`           | `--follow-redirect` | Follows HTTP redirects (useful for cases where subdomains may redirect).                              |

- **Vhost Mode**:
  ```bash
  gobuster vhost -u http://example.com -w /path/to/wordlist.txt
  ```

- **Example**:
  ```bash
  gobuster vhost -u http://192.168.1.1 -w /path/to/vhosts.txt -o vhost_results.txt
  ```


## 5. Additional Options

- **Set HTTP Headers**:
  ```bash
  gobuster dir -u http://example.com -w /path/to/wordlist.txt -H "User-Agent: CustomUserAgent"
  ```

- **Specify a Proxy**:
  ```bash
  gobuster dir -u http://example.com -w /path/to/wordlist.txt -p http://proxy:port
  ```

- **Add HTTP Basic Authentication**:
  ```bash
  gobuster dir -u http://example.com -w /path/to/wordlist.txt --username <username> --password <password>
  ```

## 6. Common Wordlists

- **Wordlists for Directory/File Enumeration**:
  - `/usr/share/wordlists/dirb/common.txt`
  - `/usr/share/seclists/Discovery/Web-Content/big.txt`

- **Wordlists for DNS Enumeration**:
  - `/usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt`

## 7. Example Scenarios

- **Enumerate Common Directories**:
  ```bash
  gobuster dir -u http://testsite.com -w /usr/share/wordlists/dirb/common.txt -x php,txt,html
  ```

- **Subdomain Enumeration with IPs Only**:
  ```bash
  gobuster dns -d testsite.com -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt -i
  ```

- **Vhost Enumeration for Hidden Virtual Hosts**:
  ```bash
  gobuster vhost -u http://10.10.10.10 -w /usr/share/wordlists/vhosts.txt -t 20
  ```

## 8. Best Practices

- **Use Appropriate Wordlists**:
  Choose wordlists based on the target's context (e.g., common web directories for a web server).

- **Monitor Load**:
  High numbers of concurrent threads (`-t`) can put significant load on the target server. Use responsibly and adjust as needed.

- **Combine with Other Tools**:
  Use results from Gobuster with other tools like Burp Suite or Nikto for further analysis.

This guide provides an overview of how to use Gobuster for directory, DNS, and vhost enumeration during penetration testing.


http://10.10.191.75/