# Getting Started

## Overview

This module took alot of time because i wanted to do every exercise it had and read it thoroughly. It introduced the basic environment and workflow used when working with Hack The Box Academy and penetration testing labs.

The main goal was to become comfortable with some of the  tools we gonna use and terminal, target machines, and basic methodology before moving into more advanced penetration testing topics.

---

## Key Concepts

### Target

A target is the machine/application that we are authorized to assess.

Before attacking a target, I need to know:

- Target IP address
- Available services
- Open ports
- Operating system 
- Technologies being used

---

### Pwnbox

Pwnbox is HTB's browser-based penetration testing environment.

It provides many of the tools needed for HTB labs without requiring me to install and configure everything locally.

Useful when:

- My Kali environment is not available
- I want a quick testing environment
- I am working directly inside HTB Academy

---

## Terminal Basics

The terminal is one of the main interfaces used during penetration testing.

I already had knowledge of using it and would hope you do too.

----

Working With Targets

When working with an HTB target, I should first identify the target information provided by the lab.

It goes like this

1. Start the target.
2. Identify the target IP.
3. Confirm connectivity.
4. Begin enumeration. I used nmap on the target and got valuable details. But we should not rely on one tool hence use other tools when we get some information. I used whatweb and gobuster to get further details i got from nmap.
5. Identify services and technologies by using the tool mentioned above or any other.
6. Investigate potential vulnerabilities. I did that by playing with the website after finding information from the tools, and it indeed helps in finding vulnerabiity.
7. Exploit vulnerabilities where appropriate. 
8. Continue with post-exploitation if required.
9. There are other methods to exploit vulnerability which are not mentioned in HTB lecture, you can practice them by searching or trying yourself.

-----
Mindset is important

The goal is to learn and know what you are doing and why.
Don't copy and paste the commands in tool but learn it by trying again and again. This is what i did because if I copy paste then it takes alot of time which I can use on other process like enumeration.

----
## Things I want to review
Reverse Shell. This was my weakest area and I spent the most time on it.
