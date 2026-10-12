# Information Gathering - Web Edition

## Overview

This module is mainly about information gathering on web applications and how we can use different tools to collect information about our target.

The main idea is that before trying to find vulnerabilities in a website, we should first understand how it works, what technologies it uses, what directories and files are accessible, and what information it exposes.

We should not just run random commands and hope that something useful comes out. We need to understand what we are looking for and use the right tool for that purpose.

Information gathering is important because the more we understand the target, the easier it becomes to identify possible weaknesses and decide what to investigate next.

---

## What is Web Information Gathering?

Web information gathering is the process of collecting information about a website or web application to understand its structure, technologies, and possible attack surface.

Some of the things we may look for are:

* Web server and its version
* Technologies and frameworks being used
* Domain and subdomain information
* Directories and files
* Virtual hosts
* Web pages and endpoints
* Login pages and input fields
* Exposed configuration files
* Possible information disclosure

This information helps us understand the application before moving towards vulnerability assessment.

---

## Website Fingerprinting

Website fingerprinting means identifying the technologies and software being used by a website.

This can include:

* Web server
* Programming language
* Content Management System (CMS)
* Frameworks
* JavaScript libraries
* Other technologies

Knowing which technologies are being used can help us decide what to investigate further.

We should not assume that a particular technology is vulnerable just because it is detected. We need to verify the information and investigate the actual configuration and version.

---

## HTTP Headers

HTTP headers provide information about communication between a client and a web server.

They can sometimes reveal details about the server, application, or security configuration.

We can inspect the response headers using:

```bash
curl -I http://<TARGET>
```

To send a request and view the response:

```bash
curl -i http://<TARGET>
```

The `-I` option requests the response headers, while `-i` includes the response headers in the output.

Headers can sometimes disclose server information or reveal missing security protections.

---

## WhatWeb

WhatWeb is a tool used to identify technologies used by websites.

Example:

```bash
whatweb http://<TARGET>
```

It can help identify technologies such as web servers, CMS platforms, and frameworks.

This gives us a starting point for further investigation.

---

## Robots.txt

The `robots.txt` file provides instructions to web crawlers about which parts of a website they should or should not crawl.

We can check it by visiting:

```text
http://<TARGET>/robots.txt
```

Or by using:

```bash
curl http://<TARGET>/robots.txt
```

It may reveal paths that the website owner does not want crawlers to access.

However, these paths are not automatically protected. The file is not an access control mechanism, so we should not assume that its contents are confidential.

---

## Directory and File Discovery

Sometimes a website has directories and files that are not linked directly from its main page.

Directory and file discovery helps us identify these resources.

One tool used for this purpose is Gobuster.

Example:

```bash
gobuster dir -u http://<TARGET> -w <WORDLIST>
```

Here:

* `dir` specifies directory and file discovery mode.
* `-u` specifies the target URL.
* `-w` specifies the wordlist to use.

A wordlist contains possible directory or file names that the tool checks against the target.

The results need to be analyzed carefully because not every discovered path is important, and some responses may be false positives.

---

## Virtual Host Discovery

A web server can host multiple websites on the same IP address. These are known as virtual hosts.

Sometimes accessing the IP address directly does not show all the websites hosted on that server.

Virtual host discovery helps us identify additional hostnames associated with the target.

For example, Gobuster supports virtual host discovery:

```bash
gobuster vhost -u http://<TARGET> -w <WORDLIST>
```

The results can help identify hostnames that should be investigated further.

---

## Crawling and Mapping a Website

A website may contain many pages, links, forms, and endpoints.

Crawling helps us discover these pages and understand how they are connected.

While exploring a website, we should pay attention to:

* Links between pages
* Forms and input fields
* Login and registration pages
* URL parameters
* File upload functionality
* API endpoints
* Redirects

This helps us understand the structure of the application and identify areas that may require further testing.

---

## Manual Investigation

Automated tools are useful, but we should not depend on them completely.

Sometimes we need to open pages manually, inspect the source code, check the HTTP responses, and understand how the application behaves.

For example, we can inspect a page's source code to look for comments, references to JavaScript files, hidden fields, or other useful information.

The information we collect manually can help us decide which tools and techniques to use next.

---

## Important Points

* Information gathering helps us understand the target before testing it for vulnerabilities.
* We should identify the technologies being used and investigate them further.
* HTTP headers can reveal useful information about a web server and its configuration.
* `robots.txt` may reveal interesting paths, but it does not protect those paths.
* Directory discovery can uncover resources that are not linked directly from the website.
* Virtual host discovery can reveal additional websites hosted on the same server.
* Automated tools can miss information, so manual investigation is also important.
* Every result should be analyzed instead of blindly assuming that it represents a vulnerability.

---

## My Methodology

When investigating a web application, I can follow this general process:

1. Identify the target and confirm the scope.
2. Check the website manually.
3. Identify the technologies using tools such as WhatWeb.
4. Inspect HTTP headers and common files such as `robots.txt`.
5. Discover directories and files.
6. Check for virtual hosts where appropriate.
7. Explore pages, forms, and endpoints.
8. Analyze the results and decide what to investigate next.
9. Document the findings.

---

## Things I Need to Review

* Website fingerprinting
* HTTP headers and responses
* WhatWeb usage
* `robots.txt`
* Gobuster directory discovery
* Virtual host discovery
* Wordlists and response codes
* Manual website investigation
