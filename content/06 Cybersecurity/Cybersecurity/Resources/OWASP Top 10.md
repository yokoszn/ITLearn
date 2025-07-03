#hacking #tools #software #Learning #certification-prep 
[[Cyber Security]]
[[hacking]]
[[TryHackMe]]

---

The **OWASP Top 10** is a list of the most critical web application security risks. Understanding these risks is essential for penetration testers to effectively evaluate and secure web applications. Below is a summary of the OWASP Top 10 vulnerabilities and pentesting tips for each:

## 1. **Broken Access Control**

- **Description**: Improper enforcement of user permissions allows unauthorized users to access restricted resources or perform actions beyond their intended privileges.
- **Pentesting Tips**:
  - Check for direct object reference vulnerabilities by manipulating URLs, IDs, or parameters.
  - Attempt accessing restricted endpoints without proper authentication.
  - Test for bypassing access controls by changing request methods (e.g., `GET` to `POST`).

Simply put, broken access control allows attackers to bypass **authorisation**, allowing them to view sensitive data or perform tasks they aren't supposed to.

For example, a [vulnerability was found in 2019](https://bugs.xdavidhu.me/google/2021/01/11/stealing-your-private-videos-one-frame-at-a-time/), where an attacker could get any single frame from a Youtube video marked as private. The researcher who found the vulnerability showed that he could ask for several frames and somewhat reconstruct the video. Since the expectation from a user when marking a video as private would be that nobody had access to it, this was indeed accepted as a broken access control vulnerability.

## 2. **Cryptographic Failures**

- **Description**: Weak or incorrect use of cryptography that compromises data security.
- **Pentesting Tips**:
  - Identify and analyze how sensitive data is transmitted and stored.
  - Verify if secure protocols (e.g., TLS) are properly implemented.
  - Test for weak encryption methods and inadequate key management.

## 3. **Injection**

- **Description**: Malicious data sent to an interpreter (e.g., SQL, NoSQL, LDAP) that alters the execution of a command.
- **Pentesting Tips**:
  - Use payloads to test for SQL, NoSQL, and command injection.
  - Check all input fields and headers (e.g., user-agent, cookies).
  - Look for error messages that may reveal vulnerabilities.
Injection flaws are very common in applications today. These flaws occur because the application interprets user-controlled input as commands or parameters. Injection attacks depend on what technologies are used and how these technologies interpret the input. Some common examples include:

- **SQL Injection:** This occurs when user-controlled input is passed to SQL queries. As a result, an attacker can pass in SQL queries to manipulate the outcome of such queries. This could potentially allow the attacker to access, modify and delete information in a database when this input is passed into database queries. This would mean an attacker could steal sensitive information such as personal details and credentials.
- **Command Injection:** This occurs when user input is passed to system commands. As a result, an attacker can execute arbitrary system commands on application servers, potentially allowing them to access users' systems.

The main defence for preventing injection attacks is ensuring that user-controlled input is not interpreted as queries or commands. There are different ways of doing this:

- **Using an allow list:** when input is sent to the server, this input is compared to a list of safe inputs or characters. If the input is marked as safe, then it is processed. Otherwise, it is rejected, and the application throws an error.
- **Stripping input:** If the input contains dangerous characters, these are removed before processing.

Dangerous characters or input is classified as any input that can change how the underlying data is processed. Instead of manually constructing allow lists or stripping input, various libraries exist that can perform these actions for you.
## 4. **Insecure Design**

- **Description**: Flaws in the application design that lead to security vulnerabilities.
- **Pentesting Tips**:
  - Assess the overall security architecture for weak points.
  - Review business logic flaws and validate how data flows through the application.
  - Test scenarios like race conditions and logic bypasses.

## 5. **Security Misconfiguration**

- **Description**: Improperly configured security settings, leading to vulnerabilities.
- **Pentesting Tips**:
  - Scan for exposed services, default accounts, and unpatched systems.
  - Analyze headers for missing security directives (e.g., `X-Frame-Options`, `Content-Security-Policy`).
  - Check for directory listings and publicly accessible files.

## 6. **Vulnerable and Outdated Components**

- **Description**: Using components (e.g., libraries, frameworks) with known vulnerabilities.
- **Pentesting Tips**:
  - Identify software versions and check for known CVEs.
  - Use tools like dependency scanners to find outdated libraries.
  - Verify if the application alerts or reacts when a vulnerable component is used.

## 7. **Identification and Authentication Failures**

- **Description**: Weak authentication and session management controls that can be exploited.
- **Pentesting Tips**:
  - Test for default credentials and weak password policies.
  - Check session tokens for predictability and hijacking.
  - Verify that multi-factor authentication is enforced where necessary.

## 8. **Software and Data Integrity Failures**

- **Description**: Code and infrastructure that do not protect against integrity violations, such as deserialization vulnerabilities.
- **Pentesting Tips**:
  - Test for untrusted deserialization attacks by crafting malicious serialized objects.
  - Inspect APIs for integrity checks and secure coding practices.
  - Validate that code repositories and package managers are secured.

## 9. **Security Logging and Monitoring Failures**

- **Description**: Lack of proper logging and monitoring that allows attackers to operate undetected.
- **Pentesting Tips**:
  - Confirm that logs capture important security events.
  - Test if alert mechanisms work when suspicious activities occur.
  - Check for proper protection of logs to prevent tampering.

## 10. **Server-Side Request Forgery (SSRF)**

- **Description**: The server makes HTTP requests to an unintended location, potentially leaking data.
- **Pentesting Tips**:
  - Test input fields that trigger server-side HTTP requests.
  - Try to redirect requests to internal resources (e.g., `127.0.0.1`).
  - Look for request manipulation that could allow access to sensitive backend services.

## Pentesting Best Practices

- **Use Automation and Manual Testing**: Utilize tools like Burp Suite, SQLMap, and Nmap while manually verifying findings.
- **Stay Updated**: Continuously review updates to the OWASP Top 10 and adapt to new techniques.
- **Document Findings**: Maintain detailed notes of identified vulnerabilities, attack methods, and potential impact for reporting.

This guide provides penetration testers with an overview of the OWASP Top 10 vulnerabilities and how to approach them during security assessments.
