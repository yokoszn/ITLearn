Have you ever thought about any of the following questions?

## Learning Objectives

By the end of this room, you should have gained a solid understanding of the following processes and concepts:

- Identification
- Authentication
- Authorisation
- Accountability
- Access Control Models
- Single Sign-On

---

1. How can we uniquely identify the different system users?
2. How can a user prove who they are to the system?
3. How can we help prevent an attacker from pretending to be a legitimate user?
4. How can we decide what a user should access? How can we enforce such a decision?
5. How can we know what a user is doing after logging in so that we can hold them accountable for their actions?

In this room, we answer the above questions and others using formal technical terms. If you are curious, the answers to the questions above lie in the following concepts and processes:

1. Identification
2. Authentication
3. Strong passwords and Multi-Factor Authentication (MFA)
4. Authorisation and Access Control
5. Logging and Auditing


# IAAA Model

Identification, Authentication, Authorisation, and Accountability (IAAA) are four pillars of information security. Each of these elements plays an essential role in ensuring the confidentiality, integrity, and availability of sensitive information and resources.

![A block diagram shows the process: identification, authentication, authorisation, and accountability.](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/97c967ea1b1efd06260dbbf88ae5c19b.png)  

In the IAAA Model, IAAA stands for Identification, Authentication, Authorization, and Accountability. The four stages of the IAAA model are:

1. **Identification** is the process of verifying who the user is. It starts with the user claiming a specific identity. The identity can be represented by a unique identifier such as an email address, a username, or an ID number. Any identifier unique in the respective environment is a valid option; hence, many websites would rely on an email address for identification instead of asking the user to create a unique username.
2. **Authentication** is the process of ensuring that the user is who they claim to be. In other words, this step is about confirming the claimed identity. One way to authenticate would be by providing the correct password. Because of potential password weaknesses, many other methods, such as asking users to type the code sent to their email, are gaining popularity.
3. **Authorisation** determines what the user is allowed to access. In other words, they will be authorised to carry out specific operations based on their account privileges. This process is typically done by assigning roles and permissions based on the user’s job function or level of clearance. The risk of unauthorised access or data breaches is reduced by restricting access to only the resources necessary for the user to perform their duties.
4. **Accountability** tracks user activity to ensure they are responsible for their actions. After a user is granted access to a system, it is essential to have mechanisms that hold everyone accountable for their actions. This process is achieved by logging all user activity and storing it in a centralised location. In the event of a security incident, this information can be used to identify the source of the problem and take appropriate action.

---

**Accountability** ensures that users are accountable for the actions they perform on a system. In other words, after authenticating their identity and getting authorised to access a system, they can be held responsible for their actions. Accountability is possible if we have **auditing** capabilities, which usually require proper **logging** functionality.

Let’s start with a non-technical example: the gym. You have a gym membership and visit the gym thrice a week. Now that you are a regular there, the receptionist recognises you and does not ask you to show your membership card. It is like you are always “logged in” at the gym! You observe that everyone with “access” to the gym abides by certain rules. For instance, no one breaks the wall mirror if they are not satisfied with their progress speed. If they do that, they will have their membership revoked and pay for all damages. In other words, everyone is _accountable_ for their actions. This model makes it convenient for everyone to exercise safely.

Let’s consider a more technical example, such as a bank teller. Such an employee can view and conduct various transactions on a client’s account. How can we ensure that a rogue employee does not abuse such authorisation? We need to log all the transactions and the relevant details securely. We should be able to audit all conducted transactions and review who did what. Without such ability, we can neither rely on nor trust such a system.

## Logging

A critical aspect of accountability is logging. Logging is the process of recording events that occur within a system. This process includes user actions, system events, and errors. By logging user actions, an organisation can maintain a record of who accessed what information and when. This record is vital for regulatory compliance, incident response, and forensic investigations.

With a comprehensive logging system in place, an organisation can trace the actions of any user, identify any anomalies or unauthorised access, and take appropriate action. For example, if an unauthorised user attempts to access sensitive data, the logging system can generate an alert to notify security personnel.

Logging can also help organisations detect and respond to security incidents. By analysing log data, security teams can identify patterns of suspicious activity, such as repeated failed login attempts or unusual access patterns. This information can then be used to investigate and respond to potential security threats.

Because accountability is a crucial component of any secure infrastructure, proper care should be taken to ensure that logging is performed properly and securely. Furthermore, depending on the security requirements, logs should be tamper-proof. The reason is that you don’t want the attacker to delete or alter the logs and hide their actions on the network. This is why it is a good practice to set up a separate logging server with one task: receive and store the logs securely. Hence we have log forwarding.

**Log forwarding** is the process of sending log data from one system to another. This process often aggregates log data from multiple sources into a central location for more accessible analysis and management. Log forwarding can also be used to send log data to a cloud-based service for storage and analysis.

There are several benefits to log forwarding. By centralising log data, organisations can more easily analyse and correlate log events from different systems to identify potential security threats. This brings us to Security Information and Event Management (SIEM).

## Logging and SIEM

Security Information and Event Management (SIEM) is a technology that aggregates log data from multiple sources and analyses it for signs of security threats. SIEM solutions can help organisations identify anomalies, detect potential security incidents, and provide alerts to security teams.

By integrating logging and SIEM, organisations can better understand their system and network activity and oversee potential threats. This integration enables organisations to identify and respond to security threats more effectively.

Furthermore, the integration of logging and SIEM provides additional benefits such as compliance reporting and forensic investigations. Compliance reporting is an essential part of any organisation’s security framework, and logging helps organisations meet reporting requirements by collecting data necessary for audits. Forensic investigations are crucial in identifying the source and cause of a security incident. Logging and SIEM solutions enable organisations to conduct forensic investigations by providing a detailed system and network activity history.


---

Identity Management (IdM) includes all the necessary policies and technologies for identification, authentication, and authorisation. IdM aims to ensure that authorised people have access to the assets and resources needed for their work while unauthorised people are denied access. IdM requires that each user or device is assigned a digital identity.

IdM helps organisations protect sensitive data and maintain compliance with regulations. It also allows organisations to streamline user access processes, reduce costs associated with identity management, and improve user experience. By implementing an effective IdM strategy, organisations can ensure that their users are authenticated and authorised to securely access the resources they need.

Some sources refer to IdM and Identity and Access Management (IAM) interchangeably. Other sources consider IdM to be more focused on the security issues related to user identity, such as authentication and permissions. They state that IdM is concerned with managing the attributes and permissions of users, devices, and groups, while IAM is more concerned with evaluating the attributes and permissions and granting or denying access according to the company policy. In this task, we present them as different, although the line between them tends to be vague.

## Identity Management (IdM)

IdM is an essential component of cybersecurity that refers to the process of managing and controlling digital identities. It involves the management of user identities, their authentication, authorisation, and access control. The main goal of IdM is to ensure that only authorised individuals have access to specific resources and information. IdM systems are used to manage user identities across an organisation’s network.

IdM systems use a centralised database to store user identities and access rights. They also provide functionalities to manage and monitor user access to resources. IdM systems generally include features such as user provisioning, authentication, and authorisation. User provisioning refers to the process of creating and managing user accounts, while authentication and authorisation refer to verifying the identity of a user and granting access to specific resources.

IdM systems are critical in organisations where there are multiple systems and applications that require access control. They help to simplify the management of user identities, reducing the risk of unauthorised access to resources. In addition, IdM systems provide a single point of reference for user identity management, which makes it easier for organisations to manage user access rights.

## Identity and Access Management (IAM)

IAM is a more comprehensive concept than IdM. It encompasses all the processes and technologies to manage and secure digital identities and access rights. IAM systems include a variety of functions, such as user provisioning, access control, identity governance, and compliance management. IAM systems ensure that only authorised users have access to specific resources and data and that their access is monitored and controlled.

IAM systems provide a comprehensive solution to manage and secure access to resources in an organisation. They integrate with multiple systems and applications, providing a centralised view of user identities and access rights. IAM systems use various technologies to manage access, including role-based access control, multi-factor authentication, and single sign-on.

IAM systems help organisations comply with regulatory requirements such as HIPAA, GDPR, and PCI DSS. They provide functionalities to manage the lifecycle of user identities, including onboarding, offboarding, and access revocation. In addition, IAM systems allow organisations to track and audit user activity, which helps to prevent security breaches and ensure compliance with industry regulations.

IdM and IAM are essential components of cybersecurity. They ensure that only authorised individuals have access to specific resources and information. IdM systems manage user identities, while IAM systems encompass broader functions to manage and secure digital identities and access rights.

![[Single Sign-On]]
![[Replay Attack]]