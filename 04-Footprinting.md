# Footprinting

## Overview

This module was mainly about footprinting different services and how we can gather as much information as possible before trying to exploit anything.

### Enumeration

Enumeration is the part where we gather information about a target using either:

- **Active methods** — such as scans and direct interaction with the target
- **Passive methods** — such as gathering information from third-party sources without directly interacting with the target

This is a very important part of penetration testing and should be done carefully and properly.

One thing I learned from this module is that it is very important to first understand the infrastructure of the target rather than blindly attacking it.

A proper plan should be developed before trying to infiltrate the target. If we just force our way in without understanding what we are dealing with, it can lead to a waste of time, energy, and resources.

The main idea I understood from this module is that enumeration is not just running one automated scan and hoping it gives us everything. We have to understand the service, know what protocols it uses, what information it may expose, and then use the right tools for it.

Sometimes the most useful information is not directly visible in the first scan, so we have to manually interact with the service and inspect it more deeply.

---

## Enumeration Principles

While enumerating a target, we should keep asking ourselves questions like:

- What can we see?
- Why are we able to see it?
- What does this information tell us about the target?
- What can we gain from it?
- How can we use it?
- What can we not see?
- Why can we not see it?
- What can the missing information tell us?

This is important because penetration testing is not only about what is directly visible. Sometimes what we cannot see can also give us useful information about the target.

---

## Enumeration Levels

The enumeration process can be divided into three main levels:

1. **Infrastructure-based enumeration**
2. **Host-based enumeration**
3. **OS-based enumeration**

These levels help us understand the target from different perspectives instead of looking at everything in the same way.

---

## Footprinting

Footprinting means gathering information about the target and the services running on it.

The more information we collect, the easier it becomes to understand the attack surface.

Things we may look for:

- Open ports
- Running services
- Service versions
- Hostnames
- Domain information
- Users
- Shares
- Configuration information
- Authentication methods
- Possible credentials
- Internal network information

------------------------------------

# Footprinting

## Overview

This module was mainly about footprinting different services and how we can gather as much information as possible before trying to exploit anything.

The main idea I understood from this module is that enumeration is not just running one automated scan and hoping it gives us everything. We have to understand the service, know what protocols it uses, what information it may expose, and then use the right tools for it.

Sometimes the most useful information is not directly visible in the first scan, so we have to manually interact with the service and inspect it more deeply.

---

## Footprinting

Footprinting means gathering information about the target and the services running on it.

The more information we collect, the easier it becomes to understand the attack surface.

Things we may look for:

- Open ports
- Running services
- Service versions
- Hostnames
- Domain information
- Users
- Shares
- Configuration information
- Authentication methods
- Possible credentials
- Internal network information

---

## Important Point

We should not depend only on Nmap.

Nmap gives us a good starting point, but after identifying a service, we should use tools made specifically for that service.

For example:

```bash
nmap -sC -sV <TARGET_IP>
```

After finding the service, we can move towards more specific enumeration.

---

## FTP

FTP is used for transferring files.

Default port:

```text
21
```

We can connect using:

```bash
ftp <TARGET_IP>
```

One important thing to check is whether anonymous login is enabled.

Example:

```text
Username: anonymous
Password: anonymous
```

Useful commands inside FTP:

```bash
ls
```

Lists files.

```bash
get <filename>
```

Downloads a file.

```bash
put <filename>
```

Uploads a file if we have permission.

FTP can sometimes expose important files, configuration files, backups, or other information.

---

## SMB

SMB is commonly used for file sharing in Windows environments.

Common ports:

```text
139
445
```

We can enumerate SMB using tools like:

```bash
smbclient
```

List available shares:

```bash
smbclient -L //<TARGET_IP> -N
```

Connect to a share:

```bash
smbclient //<TARGET_IP>/<share> -N
```

Another useful tool is:

```bash
rpcclient
```

This can be used to gather information about users, groups, and other Windows-related details.

SMB enumeration can provide a lot of useful information, especially in Active Directory environments.

---

## NFS

NFS stands for Network File System and is mainly used in Linux/Unix environments to share directories over a network.

Default port:

```text
2049
```

We can check exported shares using:

```bash
showmount -e <TARGET_IP>
```

If a share is available, it can be mounted locally:

```bash
sudo mount -t nfs <TARGET_IP>:/<share> /mnt/nfs
```

After mounting it, we can inspect the files and permissions.

Misconfigured NFS shares may expose sensitive data.

---

## DNS

DNS is used to translate domain names into IP addresses.

Default port:

```text
53
```

Tools like `dig` can be used for DNS enumeration.

Example:

```bash
dig <domain>
```

We can query different record types:

```bash
dig A <domain>
dig MX <domain>
dig TXT <domain>
dig NS <domain>
```

Zone transfers can also be checked if they are misconfigured:

```bash
dig axfr <domain> @<DNS_SERVER>
```

A successful zone transfer can expose a large amount of internal DNS information.

---

## SMTP

SMTP is used for sending emails.

Default port:

```text
25
```

We can interact with SMTP manually using:

```bash
telnet <TARGET_IP> 25
```

or:

```bash
nc <TARGET_IP> 25
```

SMTP enumeration can sometimes help us identify valid users or understand the mail server configuration.

---

## SNMP

SNMP is used for monitoring and managing network devices.

Common port:

```text
161 UDP
```

SNMP can sometimes expose a lot of information if it is misconfigured.

Common community strings may include:

```text
public
private
```

Tools such as `snmpwalk` can be used:

```bash
snmpwalk -v2c -c public <TARGET_IP>
```

This can reveal information such as:

- Hostname
- Interfaces
- Installed software
- Running processes
- Network configuration
- User-related information

SNMP is very useful because one misconfiguration can reveal a lot about the target.

---

## MySQL

MySQL is a database management system.

Default port:

```text
3306
```

We can connect using:

```bash
mysql -h <TARGET_IP> -u <username> -p
```

After connecting, useful commands include:

```sql
show databases;
```

```sql
use <database>;
```

```sql
show tables;
```

```sql
select * from <table>;
```

Databases can contain credentials, user information, configuration data, or other sensitive information.

---

## MSSQL

Microsoft SQL Server is commonly used in Windows environments.

Default port:

```text
1433
```

Tools from Impacket can be useful for connecting to MSSQL.

Example:

```bash
impacket-mssqlclient <username>:<password>@<TARGET_IP>
```

MSSQL can sometimes provide more than database access depending on its configuration and user privileges.

---

## Oracle TNS

Oracle TNS is used by Oracle databases.

Default port:

```text
1521
```

Enumeration can help identify:

- Oracle version
- Service names
- SIDs
- Database information

Oracle databases may require specific tools and more targeted enumeration.

---

## IPMI

IPMI is used for remote management of servers.

Default port:

```text
623 UDP
```

Because IPMI is related to hardware management, weak configurations can be dangerous.

It is important to identify the version and authentication methods being used.

---

## LDAP

LDAP is used to access directory services and is very important in Active Directory environments.

Common ports:

```text
389
636
```

LDAP can reveal:

- Users
- Groups
- Computers
- Domain information
- Organizational Units
- Other directory objects

LDAP enumeration becomes especially important later when working with Active Directory.

---

## RDP

RDP is used for remote graphical access to Windows systems.

Default port:

```text
3389
```

We can identify whether RDP is available and later connect if valid credentials are found.

Example:

```bash
xfreerdp /v:<TARGET_IP> /u:<username> /p:<password>
```

---

## WinRM

WinRM is used for remote management of Windows systems.

Common ports:

```text
5985
5986
```

If valid credentials are available, tools like Evil-WinRM can be used:

```bash
evil-winrm -i <TARGET_IP> -u <username> -p <password>
```

---

## SSH

SSH is used for secure remote access to Linux/Unix systems.

Default port:

```text
22
```

Connection syntax:

```bash
ssh <username>@<TARGET_IP>
```

SSH can also reveal useful information through service banners and version detection.

---

## What I Learned

- Enumeration should be service-specific.
- Nmap is mainly the starting point, not the complete solution.
- Each service has its own tools and commands for deeper enumeration.
- Misconfigurations can expose much more information than actual software vulnerabilities.
- Services such as SMB, SNMP, LDAP, DNS, and databases can reveal a large amount of useful information.
- Manual enumeration is important because automated scans can miss details.
- I should first understand what a service is used for before trying random commands against it.
- The information collected during footprinting can later help with exploitation, privilege escalation, and lateral movement.

---

## My Methodology

When I find an open port:

```text
Open Port
   ↓
Identify Service
   ↓
Identify Version
   ↓
Understand What the Service Does
   ↓
Use Service-Specific Tools
   ↓
Check Configuration
   ↓
Look for Information Leakage
   ↓
Look for Misconfigurations
   ↓
Document Everything
```

---

## Things I Need to Review

- SMB enumeration commands
- SNMP OIDs and enumeration
- LDAP enumeration
- DNS zone transfers
- Database enumeration
- Difference between anonymous access and authenticated access
- Service-specific Nmap NSE scripts